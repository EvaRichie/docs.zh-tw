---
title: 通道處理站和快取
ms.date: 03/30/2017
ms.assetid: 954f030e-091c-4c0e-a7a2-10f9a6b1f529
ms.openlocfilehash: 5b8348a98b484ca08e3dbeba141dc49825c8c071
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587361"
---
# <a name="channel-factory-and-caching"></a><span data-ttu-id="a8322-102">通道處理站和快取</span><span class="sxs-lookup"><span data-stu-id="a8322-102">Channel Factory and Caching</span></span>

<span data-ttu-id="a8322-103">WCF 用戶端應用程式會使用 <xref:System.ServiceModel.ChannelFactory%601> 類別來建立與 WCF 服務的通訊通道。</span><span class="sxs-lookup"><span data-stu-id="a8322-103">WCF client applications use the <xref:System.ServiceModel.ChannelFactory%601> class to create a communication channel with a WCF service.</span></span>  <span data-ttu-id="a8322-104">建立 <xref:System.ServiceModel.ChannelFactory%601> 執行個體會產生額外負荷，因為這涉及到下列作業：</span><span class="sxs-lookup"><span data-stu-id="a8322-104">Creating <xref:System.ServiceModel.ChannelFactory%601> instances incurs some overhead because it involves the following operations:</span></span>

- <span data-ttu-id="a8322-105">建構 <xref:System.ServiceModel.Description.ContractDescription> 樹狀</span><span class="sxs-lookup"><span data-stu-id="a8322-105">Constructing the <xref:System.ServiceModel.Description.ContractDescription> tree</span></span>

- <span data-ttu-id="a8322-106">反映所有必要的 CLR 型別</span><span class="sxs-lookup"><span data-stu-id="a8322-106">Reflecting all of the required CLR types</span></span>

- <span data-ttu-id="a8322-107">建構通道堆疊</span><span class="sxs-lookup"><span data-stu-id="a8322-107">Constructing the channel stack</span></span>

- <span data-ttu-id="a8322-108">處置資源</span><span class="sxs-lookup"><span data-stu-id="a8322-108">Disposing of resources</span></span>

<span data-ttu-id="a8322-109">為了盡量減少這種負荷，WCF 可以在您使用 WCF 用戶端 Proxy 時快取通道處理站。</span><span class="sxs-lookup"><span data-stu-id="a8322-109">To help minimize this overhead, WCF can cache channel factories when you are using a WCF client proxy.</span></span>

> [!TIP]
> <span data-ttu-id="a8322-110">直接使用 <xref:System.ServiceModel.ChannelFactory%601> 類別時，您可以直接控制通道處理站的建立作業。</span><span class="sxs-lookup"><span data-stu-id="a8322-110">You have direct control over channel factory creation when you use the <xref:System.ServiceModel.ChannelFactory%601> class directly.</span></span>

<span data-ttu-id="a8322-111">使用[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)所產生的 WCF 用戶端 proxy 衍生自 <xref:System.ServiceModel.ClientBase%601> 。</span><span class="sxs-lookup"><span data-stu-id="a8322-111">WCF client proxies generated with [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) are derived from <xref:System.ServiceModel.ClientBase%601>.</span></span> <span data-ttu-id="a8322-112"><xref:System.ServiceModel.ClientBase%601> 會定義用於定義通道處理站快取行為的靜態 <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="a8322-112"><xref:System.ServiceModel.ClientBase%601> defines a static <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> property that defines channel factory caching behavior.</span></span> <span data-ttu-id="a8322-113">快取設定會針對特定類型來設定。</span><span class="sxs-lookup"><span data-stu-id="a8322-113">Cache settings are made for a specific type.</span></span> <span data-ttu-id="a8322-114">例如，將設定 `ClientBase<ITest>.CacheSettings` 為以下定義的其中一個值，只會影響類型的 proxy/ClientBase `ITest` 。</span><span class="sxs-lookup"><span data-stu-id="a8322-114">For example, setting  `ClientBase<ITest>.CacheSettings` to one of the values defined below will affect only those proxy/ClientBase of type `ITest`.</span></span> <span data-ttu-id="a8322-115">第一個 Proxy/ClientBase 執行個體一經建立，特定 <xref:System.ServiceModel.ClientBase%601> 的快取設定就會是不可變的。</span><span class="sxs-lookup"><span data-stu-id="a8322-115">The cache setting for a particular <xref:System.ServiceModel.ClientBase%601> is immutable as soon as the first proxy/ClientBase instance is created.</span></span>

## <a name="specifying-caching-behavior"></a><span data-ttu-id="a8322-116">指定快取行為</span><span class="sxs-lookup"><span data-stu-id="a8322-116">Specifying Caching Behavior</span></span>

<span data-ttu-id="a8322-117">快取行為是藉由將 <xref:System.ServiceModel.ClientBase%601.CacheSetting> 屬性設定為下列其中一個值所指定。</span><span class="sxs-lookup"><span data-stu-id="a8322-117">Caching behavior is specified by setting the <xref:System.ServiceModel.ClientBase%601.CacheSetting> property to one of the following values.</span></span>

|<span data-ttu-id="a8322-118">快取設定值</span><span class="sxs-lookup"><span data-stu-id="a8322-118">Cache Setting Value</span></span>|<span data-ttu-id="a8322-119">描述</span><span class="sxs-lookup"><span data-stu-id="a8322-119">Description</span></span>|
|-------------------------|-----------------|
|<xref:System.ServiceModel.CacheSetting.AlwaysOn>|<span data-ttu-id="a8322-120">應用程式定義域內 <xref:System.ServiceModel.ClientBase%601> 的所有執行個體都可以參與快取。</span><span class="sxs-lookup"><span data-stu-id="a8322-120">All instances of <xref:System.ServiceModel.ClientBase%601> within the app-domain can participate in caching.</span></span> <span data-ttu-id="a8322-121">開發人員已經確定對快取沒有不利的安全性影響。</span><span class="sxs-lookup"><span data-stu-id="a8322-121">The developer has determined that there are no adverse security implications to caching.</span></span> <span data-ttu-id="a8322-122">即使存取上的「安全性敏感」屬性，也不會關閉快取 <xref:System.ServiceModel.ClientBase%601> 。</span><span class="sxs-lookup"><span data-stu-id="a8322-122">Caching will not be turned off even if "security-sensitive" properties on <xref:System.ServiceModel.ClientBase%601> are accessed.</span></span> <span data-ttu-id="a8322-123">的「安全性敏感」屬性 <xref:System.ServiceModel.ClientBase%601> 為 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 、 <xref:System.ServiceModel.ClientBase%601.Endpoint%2A> 和 <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A> 。</span><span class="sxs-lookup"><span data-stu-id="a8322-123">The "security-sensitive" properties of <xref:System.ServiceModel.ClientBase%601> are <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>, <xref:System.ServiceModel.ClientBase%601.Endpoint%2A> and <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A>.</span></span>|
|<xref:System.ServiceModel.CacheSetting.Default>|<span data-ttu-id="a8322-124">只有從定義於組態檔之端點建立的 <xref:System.ServiceModel.ClientBase%601> 執行個體才會在應用程式定義域中參與快取。</span><span class="sxs-lookup"><span data-stu-id="a8322-124">Only instances of <xref:System.ServiceModel.ClientBase%601> created from endpoints defined in configuration files participate in caching within the app-domain.</span></span> <span data-ttu-id="a8322-125">任何以程式設計方式在應用程式定義域內建立的 <xref:System.ServiceModel.ClientBase%601> 執行個體都不會參與快取。</span><span class="sxs-lookup"><span data-stu-id="a8322-125">Any instances of <xref:System.ServiceModel.ClientBase%601> created programmatically within that app-domain will not participate in caching.</span></span> <span data-ttu-id="a8322-126">此外， <xref:System.ServiceModel.ClientBase%601> 一旦存取任何其「安全性敏感」屬性，就會停用實例的快取。</span><span class="sxs-lookup"><span data-stu-id="a8322-126">Also, caching will be disabled for an instance of <xref:System.ServiceModel.ClientBase%601> once any of its "security-sensitive" properties is accessed.</span></span>|
|<xref:System.ServiceModel.CacheSetting.AlwaysOff>|<span data-ttu-id="a8322-127">在相關應用程式定義域內，特定類型之所有 <xref:System.ServiceModel.ClientBase%601> 執行個體的快取都會關閉。</span><span class="sxs-lookup"><span data-stu-id="a8322-127">Caching is turned off for all instances of <xref:System.ServiceModel.ClientBase%601> of a particular type within the app-domain in question.</span></span>|

<span data-ttu-id="a8322-128">下列程式碼片段說明如何使用 <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="a8322-128">The following code snippets illustrate how to use the <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> property.</span></span>

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase<ITest>.CacheSettings = CacheSettings.AlwaysOn;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient (new BasicHttpBinding(), new EndpointAddress(address)))
         {
            // ...
            proxy.Test(msg);
            // ...
         }
      }
   }
}
// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest { }
```

<span data-ttu-id="a8322-129">在上述程式碼中，`TestClient` 的所有執行個體都將使用相同的通道處理站。</span><span class="sxs-lookup"><span data-stu-id="a8322-129">In the above code, all instances of `TestClient` will use the same channel factory.</span></span>

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase.CacheSettings = CacheSettings.Default;
      int i = 1;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))
         {
            if (i == 4)
            {
               ServiceEndpoint endpoint = proxy.Endpoint;
               ... // use endpoint in some way
            }
            proxy.Test(msg);
         }
         i++;
   }
}

// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}
```

<span data-ttu-id="a8322-130">在上述範例中，除了執行個體 #4 以外，`TestClient` 的所有執行個體都會使用相同的通道處理站。</span><span class="sxs-lookup"><span data-stu-id="a8322-130">In the example above, all instances of `TestClient` would use the same channel factory except instance #4.</span></span> <span data-ttu-id="a8322-131">執行個體 #4 會使用專門針對其用途建立的通道處理站。</span><span class="sxs-lookup"><span data-stu-id="a8322-131">Instance #4 would use a channel factory that is created specifically for its use.</span></span> <span data-ttu-id="a8322-132">這個設定適用於特定端點需要的安全性設定與通道處理站類型 (在本例中為 `ITest`) 相同之其他端點所需安全性設定有所不同時的情節。</span><span class="sxs-lookup"><span data-stu-id="a8322-132">This setting would work for scenarios where a particular endpoint needs different security settings from the other endpoints of the same channel factory type (in this case `ITest`).</span></span>

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase.CacheSettings = CacheSettings.AlwaysOff;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))
         {
            proxy.Test(msg);
         }
      }
   }
}

// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}
```

<span data-ttu-id="a8322-133">在上述範例中，`TestClient` 的所有執行個體都會使用不同的通道處理站。</span><span class="sxs-lookup"><span data-stu-id="a8322-133">In the example above, all instances of `TestClient` would use different channel factories.</span></span> <span data-ttu-id="a8322-134">當每個端點各有不同的安全性需求，而進行快取沒有意義時，這種方式非常有用。</span><span class="sxs-lookup"><span data-stu-id="a8322-134">This is useful when each endpoint has different security requirements and it makes no sense to cache.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8322-135">請參閱</span><span class="sxs-lookup"><span data-stu-id="a8322-135">See also</span></span>

- <xref:System.ServiceModel.ClientBase%601>
- [<span data-ttu-id="a8322-136">建置用戶端</span><span class="sxs-lookup"><span data-stu-id="a8322-136">Building Clients</span></span>](../building-clients.md)
- [<span data-ttu-id="a8322-137">用戶端</span><span class="sxs-lookup"><span data-stu-id="a8322-137">Clients</span></span>](clients.md)
- [<span data-ttu-id="a8322-138">使用 WCF 用戶端存取服務</span><span class="sxs-lookup"><span data-stu-id="a8322-138">Accessing Services Using a WCF Client</span></span>](../accessing-services-using-a-wcf-client.md)
- [<span data-ttu-id="a8322-139">如何：使用 ChannelFactory</span><span class="sxs-lookup"><span data-stu-id="a8322-139">How to: Use the ChannelFactory</span></span>](how-to-use-the-channelfactory.md)

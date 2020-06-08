---
title: 管理連接
description: 瞭解針對資料資源使用 HTTP 的應用程式如何使用 .NET Framework ServicePoint 和 ServicePointManager 類別來管理連接。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, connections
- HTTP, classes for connecting
- requesting data from Internet, connections
- sending data, connections
- receiving data, connections
- ServicePoint class, about ServicePoint class
- response to Internet request, connections
- connections [.NET Framework], classes
- network resources, connections
- downloading Internet resources, connections
- ServicePointManager class, about ServicePointManager class
ms.assetid: 9b3d3de7-189f-4f7d-81ae-9c29c441aaaa
ms.openlocfilehash: 124dff1b104e323b929d13f73cf17d740e747c32
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502284"
---
# <a name="managing-connections"></a><span data-ttu-id="b7e2f-103">管理連接</span><span class="sxs-lookup"><span data-stu-id="b7e2f-103">Managing Connections</span></span>
<span data-ttu-id="b7e2f-104">使用 HTTP 連線至資料資源的應用程式可以使用 .NET Framework 的 <xref:System.Net.ServicePoint> 和 <xref:System.Net.ServicePointManager> 類別管理網際網路連線，以及協助它們達到最佳規模和效能。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-104">Applications that use HTTP to connect to data resources can use the .NET Framework's <xref:System.Net.ServicePoint> and <xref:System.Net.ServicePointManager> classes to manage connections to the Internet and to help them achieve optimum scale and performance.</span></span>  
  
 <span data-ttu-id="b7e2f-105">**ServicePoint** 類別所提供的應用程式具有應用程式可連線以存取網際網路資源的端點。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-105">The **ServicePoint** class provides an application with an endpoint to which the application can connect to access Internet resources.</span></span> <span data-ttu-id="b7e2f-106">每個 **ServicePoint** 都會包含資訊來協助最佳化與網際網路伺服器的連線，方法是在連線之間共用最佳化資訊來改善效能。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-106">Each **ServicePoint** contains information that helps optimize connections with an Internet server by sharing optimization information between connections to improve performance.</span></span>  
  
 <span data-ttu-id="b7e2f-107">每個 **ServicePoint** 都是透過統一資源識別項 (URI) 進行識別，並且根據 URI 的配置識別碼和主機片段來進行分類。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-107">Each **ServicePoint** is identified by a Uniform Resource Identifier (URI) and is categorized according to the scheme identifier and host fragments of the URI.</span></span> <span data-ttu-id="b7e2f-108">例如，相同的 **ServicePoint** 執行個體會提供 URI `http://www.contoso.com/index.htm` 和 `http://www.contoso.com/news.htm?date=today` 的要求，因為它們具有相同的配置識別碼 (http) 和主機片段 (`www.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-108">For example, the same **ServicePoint** instance would provide requests to the URIs `http://www.contoso.com/index.htm` and `http://www.contoso.com/news.htm?date=today` since they have the same scheme identifier (http) and host fragments (`www.contoso.com`).</span></span> <span data-ttu-id="b7e2f-109">如果應用程式已持續連線至伺服器 `www.contoso.com`，則會使用該連線來擷取這兩個要求，避免需要建立兩個連線。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-109">If the application already has a persistent connection to the server `www.contoso.com`, it uses that connection to retrieve both requests, avoiding the need to create two connections.</span></span>  
  
 <span data-ttu-id="b7e2f-110">**ServicePointManager** 是靜態類別，可管理 **ServicePoint** 執行個體的建立和解構。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-110">**ServicePointManager** is a static class that manages the creation and destruction of **ServicePoint** instances.</span></span> <span data-ttu-id="b7e2f-111">應用程式要求不在現有 **ServicePoint** 執行個體集合中的網際網路資源時，**ServicePointManager** 會建立 **ServicePoint**。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-111">The **ServicePointManager** creates a **ServicePoint** when the application requests an Internet resource that is not in the collection of existing **ServicePoint** instances.</span></span> <span data-ttu-id="b7e2f-112">**ServicePoint** 執行個體在超過其最大閒置時間或是現有 **ServicePoint** 執行個體數目超過應用程式的最大 **ServicePoint** 執行個體數目時即會予以終結。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-112">**ServicePoint** instances are destroyed when they have exceeded their maximum idle time or when the number of existing **ServicePoint** instances exceeds the maximum number of **ServicePoint** instances for the application.</span></span> <span data-ttu-id="b7e2f-113">預設最大閒置時間和最大 **ServicePoint** 執行個體數目的控制方式是在 **ServicePointManager** 上設定 <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A> 和 <xref:System.Net.ServicePointManager.MaxServicePoints%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-113">You can control both the default maximum idle time and the maximum number of **ServicePoint** instances by setting the <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A> and <xref:System.Net.ServicePointManager.MaxServicePoints%2A> properties on the **ServicePointManager**.</span></span>  
  
 <span data-ttu-id="b7e2f-114">用戶端與伺服器之間的連線數目會對應用程式輸送量造成很大的影響。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-114">The number of connections between a client and server can have a dramatic impact on application throughput.</span></span> <span data-ttu-id="b7e2f-115">根據預設，使用 <xref:System.Net.HttpWebRequest> 類別的應用程式最多會使用兩個與指定伺服器的持續性連線，但您可以設定個別應用程式的最大連線數目。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-115">By default, an application using the <xref:System.Net.HttpWebRequest> class uses a maximum of two persistent connections to a given server, but you can set the maximum number of connections on a per-application basis.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b7e2f-116">HTTP/1.1 規格會將應用程式的連線數目限制成一部伺服器有兩個連線。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-116">The HTTP/1.1 specification limits the number of connections from an application to two connections per server.</span></span>  
  
 <span data-ttu-id="b7e2f-117">最佳連線數目取決於實際執行應用程式的條件。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-117">The optimum number of connections depends on the actual conditions in which the application runs.</span></span> <span data-ttu-id="b7e2f-118">增加應用程式的可用連線數目，可能不會影響應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-118">Increasing the number of connections available to the application may not affect application performance.</span></span> <span data-ttu-id="b7e2f-119">若要判斷多個連線的影響，請執行效能測試，同時改變連線數目。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-119">To determine the impact of more connections, run performance tests while varying the number of connections.</span></span> <span data-ttu-id="b7e2f-120">您可以在應用程式初始化時變更 **ServicePointManager** 類別上的靜態 <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 屬性，以變更應用程式所使用的連線數目，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-120">You can change the number of connections that an application uses by changing the static <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> property on the **ServicePointManager** class at application initialization, as shown in the following code sample.</span></span>  
  
```csharp  
// Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4;  
```  
  
```vb  
' Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4  
```  
  
 <span data-ttu-id="b7e2f-121">變更 **ServicePointManager.DefaultConnectionLimit** 屬性並不會影響先前初始化的 **ServicePoint** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-121">Changing the **ServicePointManager.DefaultConnectionLimit** property does not affect previously initialized **ServicePoint** instances.</span></span> <span data-ttu-id="b7e2f-122">下列程式碼示範如何將伺服器 `http://www.contoso.com` 之現有 **ServicePoint** 的連線限制變更為 `newLimit` 中所儲存的值。</span><span class="sxs-lookup"><span data-stu-id="b7e2f-122">The following code demonstrates changing the connection limit on an existing **ServicePoint** for the server `http://www.contoso.com` to the value stored in `newLimit`.</span></span>  
  
```csharp  
Uri uri = new Uri("http://www.contoso.com/");  
ServicePoint sp = ServicePointManager.FindServicePoint(uri);  
sp.ConnectionLimit = newLimit;  
```  
  
```vb  
Dim uri As New Uri("http://www.contoso.com/")  
Dim sp As ServicePoint = ServicePointManager.FindServicePoint(uri)  
sp.ConnectionLimit = newLimit  
```  
  
## <a name="see-also"></a><span data-ttu-id="b7e2f-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7e2f-123">See also</span></span>

- [<span data-ttu-id="b7e2f-124">連線群組</span><span class="sxs-lookup"><span data-stu-id="b7e2f-124">Connection Grouping</span></span>](connection-grouping.md)
- [<span data-ttu-id="b7e2f-125">使用應用程式通訊協定</span><span class="sxs-lookup"><span data-stu-id="b7e2f-125">Using Application Protocols</span></span>](using-application-protocols.md)

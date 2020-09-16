---
title: 選擇篩選
ms.date: 03/30/2017
ms.assetid: 67ab5af9-b9d9-4300-b3b1-41abb5a1fd10
ms.openlocfilehash: 2f96e7001a41682ef595d003e87daa06d0244f3b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559385"
---
# <a name="choosing-a-filter"></a><span data-ttu-id="def77-102">選擇篩選</span><span class="sxs-lookup"><span data-stu-id="def77-102">Choosing a Filter</span></span>
<span data-ttu-id="def77-103">設定路由服務時，務必選取正確的訊息篩選條件，並將它們設定為可針對您所接收的訊息進行正確的比對。</span><span class="sxs-lookup"><span data-stu-id="def77-103">When configuring the Routing Service, it is important to select correct message filters and configure them to allow you to make exact matches against the messages you receive.</span></span> <span data-ttu-id="def77-104">如果您選取的篩選條件在比對中過度廣泛，或設定不正確，則無法正確傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-104">If the filters you select are overly broad in their matches or are incorrectly configured, messages are routed incorrectly.</span></span> <span data-ttu-id="def77-105">如果篩選條件過於嚴格，則部分訊息可能會沒有可用的有效路由。</span><span class="sxs-lookup"><span data-stu-id="def77-105">If the filters are too restrictive, you may not have any valid routes available for some of your messages.</span></span>

## <a name="filter-types"></a><span data-ttu-id="def77-106">篩選條件類型</span><span class="sxs-lookup"><span data-stu-id="def77-106">Filter Types</span></span>

<span data-ttu-id="def77-107">選取由路由服務所使用的篩選條件時，務必了解每個篩選條件的運作方式，以及傳入訊息中有何可用的資訊。</span><span class="sxs-lookup"><span data-stu-id="def77-107">When selecting the filters that are used by the Routing Service, it is important that you understand how each filter works as well as what information is available as part of the incoming messages.</span></span> <span data-ttu-id="def77-108">例如，如果所有的訊息都是由相同的端點接收，Address 和 EndpointName 篩選條件的用處便不大，因為所有的訊息都符合這些篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-108">For instance, if all messages are received over the same endpoint, the Address and EndpointName filters are not useful because all messages match these filters.</span></span>

### <a name="action"></a><span data-ttu-id="def77-109">動作</span><span class="sxs-lookup"><span data-stu-id="def77-109">Action</span></span>

<span data-ttu-id="def77-110">Action 篩選條件會檢查 <xref:System.ServiceModel.Channels.MessageHeaders.Action%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="def77-110">The Action filter inspects the <xref:System.ServiceModel.Channels.MessageHeaders.Action%2A> property.</span></span> <span data-ttu-id="def77-111">如果訊息中的 Action 標頭內容符合在篩選組態中指定的篩選資料值，則此篩選條件會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="def77-111">If the contents of the Action header in the message match the filter data value specified in the filter configuration, then this filter returns `true`.</span></span> <span data-ttu-id="def77-112">下列範例 `FilterElement` 會定義，它會使用動作篩選準則來比對包含值為之動作標頭的訊息 `http://namespace/contract/operation/` 。</span><span class="sxs-lookup"><span data-stu-id="def77-112">The following example defines a `FilterElement` that uses the Action filter to match messages with an action header that contains a value of `http://namespace/contract/operation/`.</span></span>

```xml
<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation/" />
```

```csharp
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });
```

<span data-ttu-id="def77-113">當路由訊息包含唯一的動作標頭時，應該使用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-113">This filter should be used when routing messages that contain a unique Action header.</span></span>

### <a name="endpointaddress"></a><span data-ttu-id="def77-114">EndpointAddress</span><span class="sxs-lookup"><span data-stu-id="def77-114">EndpointAddress</span></span>

<span data-ttu-id="def77-115">EndpointAddress 篩選條件會檢查收到訊息的 EndpointAddress。</span><span class="sxs-lookup"><span data-stu-id="def77-115">The EndpointAddress filter inspects the EndpointAddress that the message was received on.</span></span> <span data-ttu-id="def77-116">如果訊息到達的位址完全符合在篩選組態中指定的篩選位址，則此篩選條件會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="def77-116">If the address that the message arrives at exactly matches the filter address specified in the filter configuration, then this filter returns `true`.</span></span> <span data-ttu-id="def77-117">下列範例 `FilterElement` 會定義，它使用位址篩選準則來比對任何定址為 "HTTP:// \<hostname> /vdir/s.svc/b" 的訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-117">The following example defines a `FilterElement` that uses the Address filter to match any messages addressed to "http://\<hostname>/vdir/s.svc/b".</span></span>

```xml
<filter name="address1" filterType="EndpointAddress" filterData="http://host/vdir/s.svc/b" />
```

```csharp
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
```

> [!NOTE]
> <span data-ttu-id="def77-118">請務必注意，位址的主機名稱部分可根據用戶端是否使用完全合格的網域名稱、NetBIOS 名稱、IP 位址或其他名稱，而有所不同。</span><span class="sxs-lookup"><span data-stu-id="def77-118">It is important to note that the host name portion of an address can differ based on whether the client uses the fully qualified domain name, NetBIOS name, IP address, or other name.</span></span> <span data-ttu-id="def77-119">因為不同的值可代表相同的主機，此項比較的預設行為在執行比對時，不會使用位址的主機名稱部分。</span><span class="sxs-lookup"><span data-stu-id="def77-119">Because differing values can refer to the same host, the default behavior for this comparison is to not use the host name portion of the address when performing matches.</span></span>
>
> <span data-ttu-id="def77-120">此行為可加以修改，以便在以程式設計方式設定路由服務時，讓比較評估主機名稱。</span><span class="sxs-lookup"><span data-stu-id="def77-120">This behavior can be modified to allow the comparison to evaluate the host name when configuring the Routing Service programmatically.</span></span>

<span data-ttu-id="def77-121">當傳入訊息為唯一位址時，應該使用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-121">This filter should be used when the incoming messages are addressed to a unique address.</span></span>

### <a name="endpointaddressprefix"></a><span data-ttu-id="def77-122">EndpointAddressPrefix</span><span class="sxs-lookup"><span data-stu-id="def77-122">EndpointAddressPrefix</span></span>

<span data-ttu-id="def77-123">EndpointAddressPrefix 篩選條件與 EndpointAddress 篩選條件類似。</span><span class="sxs-lookup"><span data-stu-id="def77-123">The EndpointAddressPrefix filter is similar to the EndpointAddress filter.</span></span> <span data-ttu-id="def77-124">EndpointAddressPrefix 篩選條件會檢查收到訊息的 EndpointAddress。</span><span class="sxs-lookup"><span data-stu-id="def77-124">The EndpointAddressPrefix filter inspects the EndpointAddress that the message was received on.</span></span> <span data-ttu-id="def77-125">不過，EndpointAddressPrefix 篩選條件會藉由比對以在篩選組態中指定之值開始的位址，以萬元字元的方式呈現。</span><span class="sxs-lookup"><span data-stu-id="def77-125">However the EndpointAddressPrefix filter acts as a wildcard by matching addresses that begin with the value specified in the filter configuration.</span></span> <span data-ttu-id="def77-126">下列範例 `FilterElement` 會定義，其使用 EndpointAddressPrefix 篩選準則來比對任何定址的訊息 `http://<hostname>/vdir*` 。</span><span class="sxs-lookup"><span data-stu-id="def77-126">The following example defines a `FilterElement` that uses the EndpointAddressPrefix filter to match any messages addressed to `http://<hostname>/vdir*`.</span></span>

```xml
<filter name="prefix1" filterType="EndpointAddressPrefix" filterData="http://host/vdir" />
```

```csharp
PrefixEndpointAddressMessageFilter prefix1 = new PrefixEndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
```

> [!NOTE]
> <span data-ttu-id="def77-127">請務必注意，位址的主機名稱部分可根據用戶端是否使用完全合格的網域名稱、NetBIOS 名稱、IP 位址或其他名稱，而有所不同。</span><span class="sxs-lookup"><span data-stu-id="def77-127">It is important to note that the host name portion of an address can differ based on whether the client uses the fully qualified domain name, NetBIOS name, IP address, or other name.</span></span> <span data-ttu-id="def77-128">因為不同的值可代表相同的主機，此項比較的預設行為在執行比對時，不會使用位址的主機名稱部分。</span><span class="sxs-lookup"><span data-stu-id="def77-128">Because differing values can refer to the same host, the default behavior for this comparison is to not use the host name portion of the address when performing matches.</span></span>

<span data-ttu-id="def77-129">當路由共用通用位址首碼的傳入訊息時，應該使用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-129">This filter should be used when routing incoming messages that share a common address prefix.</span></span>

### <a name="and"></a><span data-ttu-id="def77-130">AND</span><span class="sxs-lookup"><span data-stu-id="def77-130">AND</span></span>

<span data-ttu-id="def77-131">AND 篩選條件不會直接在訊息的值中篩選，不過可讓您結合兩種其他篩選條件以建立 `AND` 條件，其中兩種篩選條件必須在 AND 篩選條件評估為 `true` 前比對訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-131">The AND filter does not directly filter on a value within a message, but allows you to combine two other filters to create an `AND` condition where both filters must match the message before the AND filter evaluates to `true`.</span></span> <span data-ttu-id="def77-132">這樣做可讓您建立複雜篩選，僅在所有子篩選符合時才比對。</span><span class="sxs-lookup"><span data-stu-id="def77-132">This allows you to create complex filters that only match if all the sub-filters match.</span></span> <span data-ttu-id="def77-133">下列範例定義位址篩選和動作篩選，然後定義針對位址和動作篩選評估訊息的 AND 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-133">The following example defines an address filter and an action filter, and then defines an AND filter that evaluates a message against both the address and action filters.</span></span> <span data-ttu-id="def77-134">如果位址和動作篩選符合，則 AND 篩選條件會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="def77-134">If both the address and the action filters match, then the AND filter returns `true`.</span></span>

```xml
<filter name="address1" filterType="AddressPrefix" filterData="http://host/vdir"/>
<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation/"/>
<filter name="and1" filterType="And" filter1="address1" filter2="action1" />
```

```csharp
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });
StrictAndMessageFilter and1=new StrictAndMessageFilter(address1, action1);
```

<span data-ttu-id="def77-135">當您必須從多個篩選條件中結合邏輯，以便決定何時進行比對時，應使用此篩選。</span><span class="sxs-lookup"><span data-stu-id="def77-135">This filter should be used when you must combine the logic from multiple filters to determine when a match should be made.</span></span> <span data-ttu-id="def77-136">例如，如果您有多個必須接收僅部分動作和特定位址訊息結合的目的地，便可使用 AND 篩選條件來結合必要的 Action 和 Address 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-136">For example, if you have multiple destinations that must receive only certain combinations of actions and messages to particular addresses, you can use an AND filter to combine the necessary Action and Address filters.</span></span>

### <a name="custom"></a><span data-ttu-id="def77-137">自訂</span><span class="sxs-lookup"><span data-stu-id="def77-137">Custom</span></span>

<span data-ttu-id="def77-138">選取自訂篩選器類型時，您必須提供 customType 值，其中包含包含要用於此篩選之 **MessageFilter** 執行的元件類型。</span><span class="sxs-lookup"><span data-stu-id="def77-138">When selecting the Custom filter type, you must provide a customType value that contains the type of the assembly that contains the **MessageFilter** implementation to be used for this filter.</span></span> <span data-ttu-id="def77-139">另外，filterData 必須包含自訂篩選在其訊息評估中可能需要的任何值。</span><span class="sxs-lookup"><span data-stu-id="def77-139">Additionally, filterData must contain any values that the custom filter may require in its evaluation of messages.</span></span> <span data-ttu-id="def77-140">下列範例會定義 `FilterElement`，其使用 `CustomAssembly.MyCustomMsgFilter` MessageFilter 實作。</span><span class="sxs-lookup"><span data-stu-id="def77-140">The following example defines a `FilterElement` that uses the `CustomAssembly.MyCustomMsgFilter` MessageFilter implementation.</span></span>

```xml
<filter name="custom1" filterType="Custom" customType="CustomAssembly.MyCustomMsgFilter, CustomAssembly" filterData="Custom Data" />
```

```csharp
MyCustomMsgFilter custom1=new MyCustomMsgFilter("Custom Data");
```

<span data-ttu-id="def77-141">如果您需要對所提供的篩選準則所未涵蓋的訊息執行自訂比對邏輯 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] ，則必須建立 **MessageFilter** 類別的自訂篩選準則。</span><span class="sxs-lookup"><span data-stu-id="def77-141">If you need to perform custom matching logic against a message that is not covered by the filters provided with [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)], you must create a custom filter that is an implementation of the **MessageFilter** class.</span></span> <span data-ttu-id="def77-142">例如，您可能要建立自訂篩選條件，此篩選條件會針對做為組態之篩選的已知值清單，在傳入訊息中比較欄位；或建立特定訊息項目雜湊，然後檢查該值以決定篩選是否應傳回 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="def77-142">For example, you might create a custom filter that compares a field in the incoming message against a list of known values given to the filter as configuration, or that hashes a particular message element and then examines that value to determine whether the filter should return `true` or `false`.</span></span>

### <a name="endpointname"></a><span data-ttu-id="def77-143">EndpointName</span><span class="sxs-lookup"><span data-stu-id="def77-143">EndpointName</span></span>

<span data-ttu-id="def77-144">EndpointName 篩選條件會檢查已接受到訊息的端點名稱。</span><span class="sxs-lookup"><span data-stu-id="def77-144">The EndpointName filter inspects the name of the endpoint that received the message.</span></span> <span data-ttu-id="def77-145">下列範例 `FilterElement` 會定義，它會使用「點」篩選準則來路由傳送「SvcEndpoint」上所收到的訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-145">The following example defines a `FilterElement` that uses the EndpointName filter to route messages received on the "SvcEndpoint".</span></span>

```xml
<filter name="name1" filterType="Endpoint" filterData="SvcEndpoint" />
```

```csharp
EndpointNameMessageFilter name1 = new EndpointNameMessageFilter("SvcEndpoint");
```

<span data-ttu-id="def77-146">當路由服務公開一個以上的已命名服務端點時，此篩選條件便非常有用。</span><span class="sxs-lookup"><span data-stu-id="def77-146">This filter is useful when the Routing Service exposes more than one named service endpoint.</span></span> <span data-ttu-id="def77-147">例如，您可能會公開兩個路由服務用來接收訊息的端點，一個是由有優先權，需要即時處理訊息的客戶所使用，另一個端點則可接收較無時間緊迫性的訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-147">For example, you might expose two endpoints that the Routing Service uses to receive messages; one is used by priority customers who require real-time processing of their messages, while the other endpoint receives messages that are not time sensitive.</span></span>

<span data-ttu-id="def77-148">當您可時常使用完整位址比對來決定要接收訊息的端點時，使用定義的端點名稱會是較方便的捷徑，因為較不易有錯誤，尤其是在使用組態檔設定路由服務時 (在組態檔中，端點名稱為必要屬性)。</span><span class="sxs-lookup"><span data-stu-id="def77-148">While you can often use full address matching to determine which endpoint a message was received on, using the defined endpoint name instead is a convenient shortcut that is often less error prone, especially when configuring a Routing Service using a configuration file (where endpoint names are a required attribute).</span></span>

### <a name="matchall"></a><span data-ttu-id="def77-149">MatchAll</span><span class="sxs-lookup"><span data-stu-id="def77-149">MatchAll</span></span>

<span data-ttu-id="def77-150">MatchAll 篩選條件會比對所有收到的訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-150">The MatchAll filter matches any received message.</span></span> <span data-ttu-id="def77-151">如果您必須時常傳送所有收到的訊息至特定端點 (例如儲存所有已接收訊息複本的記錄服務) 此篩選條件便非常有用。</span><span class="sxs-lookup"><span data-stu-id="def77-151">It is useful if you must always route all received messages to a specific endpoint, such as a logging service that stores a copy of all received messages.</span></span> <span data-ttu-id="def77-152">下列範例會定義 `FilterElement`，其使用 MatchAll 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="def77-152">The following example defines a `FilterElement` that uses the MatchAll filter.</span></span>

```xml
<filter name="matchAll1" filterType="MatchAll" />
```

```csharp
MatchAllMessageFilter matchAll1 = new MatchAllMessageFilter();
```

### <a name="xpath"></a><span data-ttu-id="def77-153">XPath</span><span class="sxs-lookup"><span data-stu-id="def77-153">XPath</span></span>

<span data-ttu-id="def77-154">XPath 篩選條件可讓您指定 XPath 查詢，該查詢是用來檢查訊息中的特定項目。</span><span class="sxs-lookup"><span data-stu-id="def77-154">The XPath filter allows you to specify an XPath query that is used to inspect a specific element within the message.</span></span> <span data-ttu-id="def77-155">XPath 篩選是相當強大的篩選選項，可讓您直接檢查訊息中的任何 XML 位址項目，不過您必須對所接收之訊息的結構有一定程度的了解。</span><span class="sxs-lookup"><span data-stu-id="def77-155">XPath filtering is a powerful filtering option that allows you to directly inspect any XML addressable entry within the message; however it requires that you have specific knowledge of the structure of the messages that you are receiving.</span></span> <span data-ttu-id="def77-156">下列範例 `FilterElement` 會定義，它會使用 XPath 篩選準則，在 "ns" 命名空間前置詞所參考的命名空間中檢查名為 "element" 的專案訊息。</span><span class="sxs-lookup"><span data-stu-id="def77-156">The following example defines a `FilterElement` that uses the XPath filter to inspect the message for an element named "element" within the namespace referenced by the "ns" namespace prefix.</span></span>

```xml
<filter name="xpath1" filterType="XPath" filterData="//ns:element" />
```

```csharp
XPathMessageFilter xpath1=new XPathMessageFilter("//ns:element");
```

<span data-ttu-id="def77-157">如果您知道正在接收的訊息包含特定值時，此篩選便非常有用。</span><span class="sxs-lookup"><span data-stu-id="def77-157">This filter is useful if you know that the messages you are receiving contain a specific value.</span></span> <span data-ttu-id="def77-158">例如，如果您正在裝載相同服務的兩個不同版本，而且知道傳送到較新服務版本的訊息，在自訂標頭中包含唯一的值，便可建立使用 XPath 的篩選條件來導覽至此標頭，並將出現在標頭中的值與篩選組態中另一個值進行比較，以決定篩選條件是否相符。</span><span class="sxs-lookup"><span data-stu-id="def77-158">For example, if you are hosting two versions of the same service and you know that messages addressed to the newer version of the service contain a unique value in a custom header, you can create a filter that uses XPath to navigate to this header and compares the value present in the header to another given in the filter configuration to determine if the filter matches.</span></span>

<span data-ttu-id="def77-159">由於 XPath 查詢通常包含唯一的命名空間，而該空間通常有冗長或複雜的字串值，因此 XPath 篩選條件可讓您使用命名空間資料表來為您的命名空間定義唯一的前置詞。</span><span class="sxs-lookup"><span data-stu-id="def77-159">Because XPath queries often contain unique namespaces, which are often lengthy or complex string values, the XPath filter allows you to use the namespace table to define unique prefixes for your namespaces.</span></span> <span data-ttu-id="def77-160">如需命名空間資料表的詳細資訊，請參閱 [訊息篩選器](message-filters.md)。</span><span class="sxs-lookup"><span data-stu-id="def77-160">For more information about the namespace table, see [Message Filters](message-filters.md).</span></span>

<span data-ttu-id="def77-161">如需有關設計 XPath 查詢的詳細資訊，請參閱 [Xpath 語法](/previous-versions/dotnet/netframework-4.0/ms256471(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="def77-161">For more information about designing XPath queries, see [XPath Syntax](/previous-versions/dotnet/netframework-4.0/ms256471(v=vs.100)).</span></span>

## <a name="see-also"></a><span data-ttu-id="def77-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="def77-162">See also</span></span>

- [<span data-ttu-id="def77-163">訊息篩選條件</span><span class="sxs-lookup"><span data-stu-id="def77-163">Message Filters</span></span>](message-filters.md)
- [<span data-ttu-id="def77-164">如何：使用篩選器</span><span class="sxs-lookup"><span data-stu-id="def77-164">How To: Use Filters</span></span>](how-to-use-filters.md)

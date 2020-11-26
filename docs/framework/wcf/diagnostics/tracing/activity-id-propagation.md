---
title: 活動識別碼傳播
ms.date: 03/30/2017
ms.assetid: cd1c1ae5-cc8a-4f51-90c9-f7b476bcfe70
ms.openlocfilehash: 0f0478b16bf2ca0975ae0290a8855756ecfc383e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236100"
---
# <a name="activity-id-propagation"></a><span data-ttu-id="ab1bb-102">活動識別碼傳播</span><span class="sxs-lookup"><span data-stu-id="ab1bb-102">Activity ID Propagation</span></span>

<span data-ttu-id="ab1bb-103">傳播會在 ServiceModel 活動追蹤啟用 (ServiceModel 傳播) 或停用 (使用者對使用者活動傳播) 時發生。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-103">Propagation happens when ServiceModel activity tracing is enabled (ServiceModel propagation) or disabled (User-to-User activity propagation).</span></span>  
  
## <a name="servicemodel-activity-tracing-is-enabled"></a><span data-ttu-id="ab1bb-104">已啟用 ServiceModel 活動追蹤</span><span class="sxs-lookup"><span data-stu-id="ab1bb-104">ServiceModel Activity Tracing is Enabled</span></span>  

 <span data-ttu-id="ab1bb-105">如果已啟用 ServiceModel ActivityTracing，則傳播會在 ProcessAction 活動之間發生。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-105">If ServiceModel ActivityTracing is enabled, propagation happens between ProcessAction activities.</span></span>  
  
### <a name="server"></a><span data-ttu-id="ab1bb-106">伺服器</span><span class="sxs-lookup"><span data-stu-id="ab1bb-106">Server</span></span>  

 <span data-ttu-id="ab1bb-107">當 `propagateActivity` `true` 用戶端和伺服器上的屬性設定為時， `ProcessAction` 伺服器中活動的識別碼會與傳播訊息標頭中的識別碼相同 `ActivityId` 。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-107">When the `propagateActivity` attribute is set to `true` on both the client and server, the ID of the `ProcessAction` activity in the server is identical to the ID in the propagated `ActivityId` message header.</span></span>  
  
 <span data-ttu-id="ab1bb-108">當 `ActivityId` 訊息中沒有標頭時 (也就是 `propagateActivity` = `false` 在用戶端) 上，或是 `propagateActivity` = `false` 在伺服器上，伺服器會產生新的活動識別碼。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-108">When no `ActivityId` header is present in the message (that is, `propagateActivity`=`false` on the client), or when `propagateActivity`=`false` on the server, the server generates a new activity ID.</span></span>  
  
### <a name="client"></a><span data-ttu-id="ab1bb-109">用戶端</span><span class="sxs-lookup"><span data-stu-id="ab1bb-109">Client</span></span>  

 <span data-ttu-id="ab1bb-110">如果用戶端為同步單一執行緒，則用戶端會忽略用戶端或伺服器的任何 `propagateActivity` 設定，</span><span class="sxs-lookup"><span data-stu-id="ab1bb-110">If the client is synchronously single threaded, the client disregards any settings of `propagateActivity` at the client or server.</span></span> <span data-ttu-id="ab1bb-111">所以回應會改而在要求活動中處理。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-111">Instead, the response is handled in the request activity.</span></span> <span data-ttu-id="ab1bb-112">如果用戶端是非同步或同步多執行緒，則 `propagateActivity` = `true` 在用戶端中，如果伺服器傳送的訊息中有活動識別碼標頭，用戶端就會從訊息中抓取活動識別碼，並傳輸至包含已傳播活動識別碼的「處理動作」活動。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-112">If the client is asynchronous or synchronous multithreaded, `propagateActivity`=`true` in the client, and there is an activity ID header in the message sent by the server, the client retrieves the activity ID from the message, and transfers to the Process Action activity that contains the propagated activity ID.</span></span> <span data-ttu-id="ab1bb-113">否則，用戶端會從「處理訊息」活動傳輸至新的「處理動作」活動。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-113">Otherwise, the client transfers from Process Message activity to a new Process Action activity.</span></span> <span data-ttu-id="ab1bb-114">傳輸至新的「處理動作」活動是為了求得一致性才進行的額外動作。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-114">This extra transfer to a new Process Action activity is done for consistency.</span></span> <span data-ttu-id="ab1bb-115">在這個活動內，用戶端會從本機執行緒內容中擷取 BeginCall 活動的活動識別碼，同時執行緒也會配置用來處理回應訊息。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-115">Inside this activity, the client retrieves the activity ID of the BeginCall activity from the local thread context, when the thread is allocated for response message processing.</span></span> <span data-ttu-id="ab1bb-116">然後，用戶端會傳輸至初始「處理動作」活動。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-116">It then transfers to the initial Process Action activity.</span></span>  
  
 <span data-ttu-id="ab1bb-117">如果用戶端為雙工，則可當做伺服器接收訊息。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-117">If the client is duplex, the client acts as server on receiving the message.</span></span>  
  
### <a name="propagation-in-fault-messages"></a><span data-ttu-id="ab1bb-118">錯誤訊息中的傳播</span><span class="sxs-lookup"><span data-stu-id="ab1bb-118">Propagation in Fault Messages</span></span>  

 <span data-ttu-id="ab1bb-119">處理有效和錯誤訊息之間並無差異。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-119">There is no difference in handling valid and fault messages.</span></span> <span data-ttu-id="ab1bb-120">如果為 `propagateActivity` = `true` ，則新增至 SOAP 錯誤訊息標頭的活動識別碼與環境活動相同。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-120">If `propagateActivity`=`true`, the activity ID added to the SOAP fault message headers is identical to the ambient activity.</span></span>  
  
## <a name="servicemodel-activity-tracing-is-disabled"></a><span data-ttu-id="ab1bb-121">已停用 ServiceModel 活動追蹤</span><span class="sxs-lookup"><span data-stu-id="ab1bb-121">ServiceModel Activity Tracing is Disabled</span></span>  

 <span data-ttu-id="ab1bb-122">如果已停用 ServiceModel ActivityTracing，則傳播會直接在使用者程式碼活動之間發生，而不會經過 ServiceModel 活動。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-122">If ServiceModel ActivityTracing is disabled, propagation occurs between user code activities directly without going through ServiceModel activities.</span></span> <span data-ttu-id="ab1bb-123">使用者定義的活動識別碼也會透過訊息活動識別碼標頭進行傳播。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-123">A user-defined activity ID is also propagated through the message activity ID header.</span></span>  
  
 <span data-ttu-id="ab1bb-124">如果對 `propagateActivity` = `true` 等 `ActivityTracing` = `off` 量追蹤接聽程式 (，不論是否已在 system.servicemodel) 上啟用追蹤，用戶端或伺服器上都會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="ab1bb-124">If `propagateActivity`=`true` and `ActivityTracing`=`off` for a ServiceModel trace listener (regardless of whether tracing is enabled on ServiceModel), the following happen on either the client or server:</span></span>  
  
- <span data-ttu-id="ab1bb-125">在作業要求或傳送回應時，TLS 中的活動識別碼會傳播至使用者程式碼外，直到形成訊息為止。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-125">On operation request or sending response, the activity ID in TLS is propagated out of user code until a message is formed.</span></span> <span data-ttu-id="ab1bb-126">傳送活動識別碼標頭之前，也會將該標頭插入訊息。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-126">An activity ID header is also inserted into the message before it is sent.</span></span>  
  
- <span data-ttu-id="ab1bb-127">在接收要求或接收回應時，只要一建立收到的訊息物件，就會從訊息標頭擷取活動識別碼。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-127">On receiving request or receiving response, the activity ID is retrieved from the message header as soon as the received message object is created.</span></span> <span data-ttu-id="ab1bb-128">只要訊息一從範圍內消失，就會傳播 TLS 中的活動識別碼，直到到達使用者程式碼為止。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-128">The activity ID in TLS is propagated as soon as the message disappears from scope until user code is reached.</span></span>  
  
 <span data-ttu-id="ab1bb-129">這些動作可確保只要開啟傳播，相同的活動中就會出使用者追蹤。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-129">These actions guarantee that user traces will appear in the same activity if propagation is on.</span></span> <span data-ttu-id="ab1bb-130">不過，ServiceModel 追蹤則不一定如此。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-130">However, it makes no guarantee on ServiceModel traces.</span></span> <span data-ttu-id="ab1bb-131">只有在設定使用者程式碼活動的相同執行緒上處理 ServiceModel 追蹤時，這些追蹤才會發生在使用者程式碼活動中。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-131">ServiceModel traces occur in a user code activity only if the processing of those traces is executed on the same thread where the user code activity was set.</span></span>  
  
 <span data-ttu-id="ab1bb-132">一般來說，ServiceModel 追蹤會出現在下列位置：</span><span class="sxs-lookup"><span data-stu-id="ab1bb-132">In general, ServiceModel traces can be observed in the following places:</span></span>  
  
- <span data-ttu-id="ab1bb-133">如果已停用 ServiceModel 追蹤，則所有發出的追蹤都會出現在使用者活動中。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-133">If ServiceModel tracing is disabled, all emitted traces appear in user activities.</span></span> <span data-ttu-id="ab1bb-134">如果已在伺服器和用戶端上啟用傳播，這些追蹤就會位於相同活動中。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-134">If propagation is enabled at both the server and client, these traces will be in the same activity.</span></span>  
  
- <span data-ttu-id="ab1bb-135">如果已啟用 ServiceModel 追蹤但停用 ActivityTracing，則在兩端皆啟用傳播時，使用者追蹤會出現在相同的活動中。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-135">If ServiceModel tracing is enabled, but ActivityTracing is disabled, user traces appear in the same activity if propagation is enabled on both ends.</span></span> <span data-ttu-id="ab1bb-136">ServiceModel 追蹤會出現在預設的 0000 活動中，除非這些追蹤是發生在與使用者程式碼處理過程相同的執行緒中，而活動一開始會在這個過程中設定。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-136">ServiceModel traces appear in the default 0000 activity, unless they occur in the same thread as the user code processing where the activity is initially set.</span></span>  
  
- <span data-ttu-id="ab1bb-137">如果已同時啟用 ServiceModel 追蹤和 ActivityTracing，則使用者追蹤會出現在使用者定義的活動中，而 ServiceModel 追蹤則會出現在 ServiceModel 定義的活動中。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-137">If both ServiceModel tracing and ActivityTracing are enabled, user traces appear in user-defined activities, and ServiceModel traces appear in ServiceModel-defined activities.</span></span> <span data-ttu-id="ab1bb-138">傳播會發生在 ServiceModel 層級。</span><span class="sxs-lookup"><span data-stu-id="ab1bb-138">Propagation happens at ServiceModel level.</span></span>

---
title: 批次處理異動中的訊息
ms.date: 03/30/2017
helpviewer_keywords:
- batching messages [WCF]
ms.assetid: 53305392-e82e-4e89-aedc-3efb6ebcd28c
ms.openlocfilehash: c18d5a36f4263a93589b75129517d66df80ce463
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96247456"
---
# <a name="batching-messages-in-a-transaction"></a><span data-ttu-id="00535-102">批次處理異動中的訊息</span><span class="sxs-lookup"><span data-stu-id="00535-102">Batching Messages in a Transaction</span></span>

<span data-ttu-id="00535-103">佇列的應用程式會使用異動來確保訊息的正確性與可靠的傳遞。</span><span class="sxs-lookup"><span data-stu-id="00535-103">Queued applications use transactions to ensure correctness and reliable delivery of messages.</span></span> <span data-ttu-id="00535-104">不過，異動是昂貴的作業，而且可能大幅降低訊息的處理能力。</span><span class="sxs-lookup"><span data-stu-id="00535-104">Transactions, however, are expensive operations and can dramatically reduce message throughput.</span></span> <span data-ttu-id="00535-105">要改善訊息處理能力的其中一種方式，就是讓應用程式在單一異動內讀取和處理多個訊息。</span><span class="sxs-lookup"><span data-stu-id="00535-105">One way to improve message throughput is to have an application read and process multiple messages within a single transaction.</span></span> <span data-ttu-id="00535-106">效能與復原之間的取捨：隨著批次中訊息數目的增加，交易復原時所需的復原工作量也會增加。</span><span class="sxs-lookup"><span data-stu-id="00535-106">The trade-off is between performance and recovery: as the number of messages in a batch increases, so does the amount of recovery work that required if transactions are rolled back.</span></span> <span data-ttu-id="00535-107">務必注意的是，在交易和工作階段中批次處理訊息之間的差異。</span><span class="sxs-lookup"><span data-stu-id="00535-107">It is important to note the difference between batching messages in a transaction and sessions.</span></span> <span data-ttu-id="00535-108">*會話* 是一組相關的訊息，由單一應用程式處理並認可為單一單位。</span><span class="sxs-lookup"><span data-stu-id="00535-108">A *session* is a grouping of related messages that are processed by a single application and committed as a single unit.</span></span> <span data-ttu-id="00535-109">工作階段通常是在有一組相關訊息必須一併處理時使用。</span><span class="sxs-lookup"><span data-stu-id="00535-109">Sessions are generally used when a group of related messages must be processed together.</span></span> <span data-ttu-id="00535-110">這類工作的範例為線上購物網站。</span><span class="sxs-lookup"><span data-stu-id="00535-110">An example of this is an online shopping Web site.</span></span> <span data-ttu-id="00535-111">*批次* 是用來處理多個不相關的訊息，並以增加訊息輸送量的方式來處理。</span><span class="sxs-lookup"><span data-stu-id="00535-111">*Batches* are used to process multiple, unrelated messages in a way that increases message throughput.</span></span> <span data-ttu-id="00535-112">如需會話的詳細資訊，請參閱 [在會話中群組佇列訊息](grouping-queued-messages-in-a-session.md)。</span><span class="sxs-lookup"><span data-stu-id="00535-112">For more information about sessions, see [Grouping Queued Messages in a Session](grouping-queued-messages-in-a-session.md).</span></span> <span data-ttu-id="00535-113">批次中的訊息同樣是由單一應用程式處理，並且以單一單位進行認可，但是批次中的訊息可能沒有任何關聯性。</span><span class="sxs-lookup"><span data-stu-id="00535-113">Messages in a batch are also processed by a single application and committed as a single unit, but there may be no relationship between the messages in the batch.</span></span> <span data-ttu-id="00535-114">將異動中的訊息批次處理是最佳的方法，而且不會改變應用程式執行的方式。</span><span class="sxs-lookup"><span data-stu-id="00535-114">Batching messages in a transaction is an optimization that does not change how the application runs.</span></span>  
  
## <a name="entering-batching-mode"></a><span data-ttu-id="00535-115">進入批次處理模式</span><span class="sxs-lookup"><span data-stu-id="00535-115">Entering Batching Mode</span></span>  

 <span data-ttu-id="00535-116"><xref:System.ServiceModel.Description.TransactedBatchingBehavior> 端點行為會控制批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-116">The <xref:System.ServiceModel.Description.TransactedBatchingBehavior> endpoint behavior controls batching.</span></span> <span data-ttu-id="00535-117">將此端點行為加入至服務端點，會告知 Windows Communication Foundation (WCF) 批次處理交易中的訊息。</span><span class="sxs-lookup"><span data-stu-id="00535-117">Adding this endpoint behavior to a service endpoint tells Windows Communication Foundation (WCF) to batch messages in a transaction.</span></span> <span data-ttu-id="00535-118">並非所有的訊息都需要交易，因此只會在批次中放置需要交易的訊息，而且只 `TransactionScopeRequired`  =  `true` `TransactionAutoComplete`  =  `true` 會針對批次考慮從標示為和的作業傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="00535-118">Not all messages require a transaction, so only messages that require a transaction are placed in a batch, and only messages sent from operations marked with `TransactionScopeRequired` = `true` and `TransactionAutoComplete` = `true` are considered for a batch.</span></span> <span data-ttu-id="00535-119">如果服務合約上的所有作業都標示了 `TransactionScopeRequired`  =  `false` 和 `TransactionAutoComplete`  =  `false` ，則永遠不會輸入批次處理模式。</span><span class="sxs-lookup"><span data-stu-id="00535-119">If all operations on the service contract are marked with `TransactionScopeRequired` = `false` and `TransactionAutoComplete` = `false`, then batching mode is never entered.</span></span>  
  
## <a name="committing-a-transaction"></a><span data-ttu-id="00535-120">認可交易</span><span class="sxs-lookup"><span data-stu-id="00535-120">Committing a Transaction</span></span>  

 <span data-ttu-id="00535-121">批次處理的異動會根據下列原則進行認可：</span><span class="sxs-lookup"><span data-stu-id="00535-121">A batched transaction is committed based on the following:</span></span>  
  
- <span data-ttu-id="00535-122">`MaxBatchSize`.</span><span class="sxs-lookup"><span data-stu-id="00535-122">`MaxBatchSize`.</span></span> <span data-ttu-id="00535-123"><xref:System.ServiceModel.Description.TransactedBatchingBehavior> 行為的屬性。</span><span class="sxs-lookup"><span data-stu-id="00535-123">A property of the <xref:System.ServiceModel.Description.TransactedBatchingBehavior> behavior.</span></span> <span data-ttu-id="00535-124">此屬性會決定放入批次中的訊息數目上限。</span><span class="sxs-lookup"><span data-stu-id="00535-124">This property determines the maximum number of messages that are placed into a batch.</span></span> <span data-ttu-id="00535-125">當到達此數目時，就會認可批次。</span><span class="sxs-lookup"><span data-stu-id="00535-125">When this number is reached, the batch is committed.</span></span> <span data-ttu-id="00535-126">這個值並不是一項嚴格的限制，因此可以在收到此訊息數目之前認可批次。</span><span class="sxs-lookup"><span data-stu-id="00535-126">This is value is not a strict limit, it is possible to commit a batch before receiving this number of messages.</span></span>  
  
- <span data-ttu-id="00535-127">`Transaction Timeout`.</span><span class="sxs-lookup"><span data-stu-id="00535-127">`Transaction Timeout`.</span></span> <span data-ttu-id="00535-128">在經過 80% 的異動逾時之後，就會認可批次並且建立新批次。</span><span class="sxs-lookup"><span data-stu-id="00535-128">After 80 percent of the transaction's time-out has elapsed, the batch is committed and a new batch is created.</span></span> <span data-ttu-id="00535-129">這表示，如果完成交易的指定時間只剩不到 20%，就會認可交易。</span><span class="sxs-lookup"><span data-stu-id="00535-129">This means that if 20 percent or less of the time given for a transaction to complete remains, the batch is committed.</span></span>  
  
- <span data-ttu-id="00535-130">`TransactionScopeRequired`.</span><span class="sxs-lookup"><span data-stu-id="00535-130">`TransactionScopeRequired`.</span></span> <span data-ttu-id="00535-131">處理一批訊息時，如果 WCF 找到具有的訊息批次， `TransactionScopeRequired`  =  `false` 則會認可批次，並在收到第一個具有和的訊息時重新開啟新批次 `TransactionScopeRequired`  =  `true` `TransactionAutoComplete`  =  `true` 。</span><span class="sxs-lookup"><span data-stu-id="00535-131">When processing a batch of messages, if WCF finds one that has `TransactionScopeRequired` = `false`, it commits the batch and reopens a new batch on receipt of the first message with `TransactionScopeRequired` = `true` and `TransactionAutoComplete` = `true`.</span></span>  
  
- <span data-ttu-id="00535-132">如果佇列中已沒有任何訊息，即使尚未到達 `MaxBatchSize` 或尚未經過交易逾時的 80%，仍會認可目前的批次。</span><span class="sxs-lookup"><span data-stu-id="00535-132">If no more messages exist in the queue, then the current batch is committed, even if the `MaxBatchSize` has not been reached or 80 percent of the transaction's time-out has not elapsed.</span></span>  
  
## <a name="leaving-batching-mode"></a><span data-ttu-id="00535-133">離開批次處理模式</span><span class="sxs-lookup"><span data-stu-id="00535-133">Leaving Batching Mode</span></span>  

 <span data-ttu-id="00535-134">如果批次中的訊息造成異動中止，則會發生下列步驟：</span><span class="sxs-lookup"><span data-stu-id="00535-134">If a message in a batch causes the transaction to abort, the following steps occur:</span></span>  
  
1. <span data-ttu-id="00535-135">整個批次的訊息都會復原。</span><span class="sxs-lookup"><span data-stu-id="00535-135">The entire batch of messages is rolled back.</span></span>  
  
2. <span data-ttu-id="00535-136">一次讀取一個訊息，直到已讀取的訊息數目超過最大批次大小的兩倍。</span><span class="sxs-lookup"><span data-stu-id="00535-136">Messages are read one at a time until the number of messages read exceeds twice the maximum batch size.</span></span>  
  
3. <span data-ttu-id="00535-137">重新進入批次處理模式。</span><span class="sxs-lookup"><span data-stu-id="00535-137">Batch mode is re-entered.</span></span>  
  
## <a name="choosing-the-batch-size"></a><span data-ttu-id="00535-138">選擇批次大小</span><span class="sxs-lookup"><span data-stu-id="00535-138">Choosing the Batch Size</span></span>  

 <span data-ttu-id="00535-139">批次大小視應用程式而定。</span><span class="sxs-lookup"><span data-stu-id="00535-139">The size of a batch is application-dependent.</span></span> <span data-ttu-id="00535-140">經驗判斷通常是達到應用程式最佳批次大小的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="00535-140">The empirical method is the best way to arrive at an optimal batch size for the application.</span></span> <span data-ttu-id="00535-141">不過務必記得，選擇批次大小時，應根據應用程式的實際部署模型選擇大小。</span><span class="sxs-lookup"><span data-stu-id="00535-141">It is important to remember when choosing a batch size to choose the size according to your application's actual deployment model.</span></span> <span data-ttu-id="00535-142">例如，部署應用程式時，如果需要遠端電腦上 SQL 伺服器，而且需要擴展佇列和 SQL 伺服器的異動，則批次大小最好是經過執行此組態後再決定。</span><span class="sxs-lookup"><span data-stu-id="00535-142">For example, when deploying the application, if you need an SQL server on a remote machine and a transaction that spans the queue and the SQL server, then the batch size is best determined by running this exact configuration.</span></span>  
  
## <a name="concurrency-and-batching"></a><span data-ttu-id="00535-143">並行處理和批次處理</span><span class="sxs-lookup"><span data-stu-id="00535-143">Concurrency and Batching</span></span>  

 <span data-ttu-id="00535-144">若要提升處理能力，您也可以並行處理多個批次。</span><span class="sxs-lookup"><span data-stu-id="00535-144">To increase throughput, you can also have many batches run concurrently.</span></span> <span data-ttu-id="00535-145">您可以藉由設定 `ConcurrencyMode.Multiple` 中的 `ServiceBehaviorAttribute`，啟用並行批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-145">By setting `ConcurrencyMode.Multiple` in `ServiceBehaviorAttribute`, you enable concurrent batching.</span></span>  
  
 <span data-ttu-id="00535-146">*服務節流* 是一種服務行為，用來指出可在服務上進行的並行呼叫數上限。</span><span class="sxs-lookup"><span data-stu-id="00535-146">*Service throttling* is a service behavior that is used to indicate how many maximum concurrent calls can be made on the service.</span></span> <span data-ttu-id="00535-147">搭配批次處理使用時，這種行為會解譯為可以同時執行的批次數。</span><span class="sxs-lookup"><span data-stu-id="00535-147">When used with batching, this is interpreted as how many concurrent batches can be run.</span></span> <span data-ttu-id="00535-148">如果未設定服務節流，WCF 會預設為16的同時呼叫數目上限。</span><span class="sxs-lookup"><span data-stu-id="00535-148">If the service throttling is not set, WCF defaults the maximum concurrent calls to 16.</span></span> <span data-ttu-id="00535-149">因此，如果預設會加入批次處理行為，則最多有 16 個批次可以同時為作用中。</span><span class="sxs-lookup"><span data-stu-id="00535-149">Thus, if batching behavior were added by default, a maximum of 16 batches can be active at the same time.</span></span> <span data-ttu-id="00535-150">建議您最好根據容量調整服務節流和批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-150">It is best to tune the service throttling and batching based on your capacity.</span></span> <span data-ttu-id="00535-151">例如，如果佇列擁有 100 個訊息，而一個批次需要 20 個，那麼將同步呼叫數的上限設為 16 便不實際，因為根據處理能力，可以有 16 個異動是作用中的，所以這相當於是未啟動批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-151">For example, if the queue has 100 messages and a batch of 20 is desired, having the maximum concurrent calls set to 16 is not useful because, depending on throughput, 16 transactions could be active, similar to not having batching turned on.</span></span> <span data-ttu-id="00535-152">因此在調整效能時，可選擇不要同步批次處理，或是使用正確的服務節流大小搭配同步批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-152">Therefore, when fine-tuning for performance, either do not have concurrent batching or have concurrent batching with the correct service throttle size.</span></span>  
  
## <a name="batching-and-multiple-endpoints"></a><span data-ttu-id="00535-153">批次處理和多個端點</span><span class="sxs-lookup"><span data-stu-id="00535-153">Batching and Multiple Endpoints</span></span>  

 <span data-ttu-id="00535-154">端點是由位址和合約所組成。</span><span class="sxs-lookup"><span data-stu-id="00535-154">An endpoint is composed of an address and a contract.</span></span> <span data-ttu-id="00535-155">因此可能會有多個端點共用同一個繫結。</span><span class="sxs-lookup"><span data-stu-id="00535-155">There may be multiple endpoints that share the same binding.</span></span> <span data-ttu-id="00535-156">兩個端點可以共用同一個繫結，並且接聽統一資源識別元 (URI) 或佇列位址。</span><span class="sxs-lookup"><span data-stu-id="00535-156">It is possible for two endpoints to share the same binding and listen Uniform Resource Identifier (URI), or queue address.</span></span> <span data-ttu-id="00535-157">如果兩個端點從同一個佇列讀取，而且交易的批次處理行為會加入至這兩個端點，則指定的批次大小可能會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="00535-157">If two endpoints are reading from the same queue, and transacted batching behavior is added to both endpoints, a conflict in the batch sizes specified could arise.</span></span> <span data-ttu-id="00535-158">這種情況可藉由使用在兩個交易批次處理行為之間所指定的最小批次大小，實作批次處理的方式予以解決。</span><span class="sxs-lookup"><span data-stu-id="00535-158">This is resolved by implementing batching using the minimal batch size specified between the two transacted batching behaviors.</span></span> <span data-ttu-id="00535-159">在此案例中，如果其中一個端點未指定交易的批次處理，則兩個端點都不會使用批次處理。</span><span class="sxs-lookup"><span data-stu-id="00535-159">In this scenario, if one of the endpoints does not specify transacted batching, then both endpoints would not use batching.</span></span>  
  
## <a name="example"></a><span data-ttu-id="00535-160">範例</span><span class="sxs-lookup"><span data-stu-id="00535-160">Example</span></span>  

 <span data-ttu-id="00535-161">以下範例將示範如何在組態檔中指定 `TransactedBatchingBehavior`。</span><span class="sxs-lookup"><span data-stu-id="00535-161">The following example shows how to specify the `TransactedBatchingBehavior` in a configuration file.</span></span>  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="TransactedBatchingBehavior"
              maxBatchSize="100" />
  </endpointBehaviors>
</behaviors>
```  
  
 <span data-ttu-id="00535-162">以下範例將示範如何在程式碼中指定 <xref:System.ServiceModel.Description.TransactedBatchingBehavior>。</span><span class="sxs-lookup"><span data-stu-id="00535-162">The following example shows how to specify the <xref:System.ServiceModel.Description.TransactedBatchingBehavior> in code.</span></span>  
  
```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
     ServiceEndpoint sep = ServiceHost.AddServiceEndpoint(typeof(IOrderProcessor), new NetMsmqBinding(), "net.msmq://localhost/private/ServiceModelSamplesTransacted");
     sep.Behaviors.Add(new TransactedBatchingBehavior(100));

     // Open the ServiceHost to create listeners and start listening for messages.
    serviceHost.Open();
  
    // The service can now be accessed.
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.WriteLine();
    Console.ReadLine();
  
    // Close the ServiceHostB to shut down the service.
    serviceHost.Close();
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="00535-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="00535-163">See also</span></span>

- [<span data-ttu-id="00535-164">佇列概觀</span><span class="sxs-lookup"><span data-stu-id="00535-164">Queues Overview</span></span>](queues-overview.md)
- [<span data-ttu-id="00535-165">WCF 中的佇列</span><span class="sxs-lookup"><span data-stu-id="00535-165">Queuing in WCF</span></span>](queuing-in-wcf.md)

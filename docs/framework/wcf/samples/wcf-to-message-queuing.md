---
title: Windows Communication Foundation 至訊息佇列
ms.date: 03/30/2017
ms.assetid: 78d0d0c9-648e-4d4a-8f0a-14d9cafeead9
ms.openlocfilehash: a6e322936740f7d88d30b9a205ac937a807bedc1
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90552923"
---
# <a name="windows-communication-foundation-to-message-queuing"></a><span data-ttu-id="a8698-102">Windows Communication Foundation 至訊息佇列</span><span class="sxs-lookup"><span data-stu-id="a8698-102">Windows Communication Foundation to Message Queuing</span></span>

<span data-ttu-id="a8698-103">這個範例會示範 Windows Communication Foundation (WCF) 應用程式如何將訊息傳送至訊息佇列 (MSMQ) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8698-103">This sample demonstrates how a Windows Communication Foundation (WCF) application can send a message to a Message Queuing (MSMQ) application.</span></span> <span data-ttu-id="a8698-104">這個服務是自我裝載的主控台應用程式，可讓您觀察接收佇列訊息的服務。</span><span class="sxs-lookup"><span data-stu-id="a8698-104">The service is a self-hosted console application to enable you to observe the service receiving queued messages.</span></span> <span data-ttu-id="a8698-105">服務與用戶端不需要在相同時間執行。</span><span class="sxs-lookup"><span data-stu-id="a8698-105">The service and client do not have to be running at the same time.</span></span>

 <span data-ttu-id="a8698-106">服務會接收佇列訊息，然後處理訂單。</span><span class="sxs-lookup"><span data-stu-id="a8698-106">The service receives messages from the queue and processes orders.</span></span> <span data-ttu-id="a8698-107">服務會建立交易式佇列，然後設定已接收訊息的訊息處理常式，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="a8698-107">The service creates a transactional queue and sets up a message received message handler, as shown in the following sample code.</span></span>

```csharp
static void Main(string[] args)
{
    if (!MessageQueue.Exists(
              ConfigurationManager.AppSettings["queueName"]))
       MessageQueue.Create(
           ConfigurationManager.AppSettings["queueName"], true);
        //Connect to the queue
        MessageQueue Queue = new
    MessageQueue(ConfigurationManager.AppSettings["queueName"]);
    Queue.ReceiveCompleted +=
                 new ReceiveCompletedEventHandler(ProcessOrder);
    Queue.BeginReceive();
    Console.WriteLine("Order Service is running");
    Console.ReadLine();
}
```

 <span data-ttu-id="a8698-108">當訊息是由佇列接收時，就會叫用訊息處理常式 `ProcessOrder`。</span><span class="sxs-lookup"><span data-stu-id="a8698-108">When a message is received in the queue, the message handler `ProcessOrder` is invoked.</span></span>

```csharp
public static void ProcessOrder(Object source,
    ReceiveCompletedEventArgs asyncResult)
{
    try
    {
        // Connect to the queue.
        MessageQueue Queue = (MessageQueue)source;
        // End the asynchronous receive operation.
        System.Messaging.Message msg =
                     Queue.EndReceive(asyncResult.AsyncResult);
        msg.Formatter = new System.Messaging.XmlMessageFormatter(
                                new Type[] { typeof(PurchaseOrder) });
        PurchaseOrder po = (PurchaseOrder) msg.Body;
        Random statusIndexer = new Random();
        po.Status = PurchaseOrder.OrderStates[statusIndexer.Next(3)];
        Console.WriteLine("Processing {0} ", po);
        Queue.BeginReceive();
    }
    catch (System.Exception ex)
    {
        Console.WriteLine(ex.Message);
    }

}
```

 <span data-ttu-id="a8698-109">服務會從 MSMQ 訊息本文擷取 `ProcessOrder`，然後處理訂單。</span><span class="sxs-lookup"><span data-stu-id="a8698-109">The service extracts the `ProcessOrder` from the MSMQ message body, and processes the order.</span></span>

 <span data-ttu-id="a8698-110">MSMQ 佇列名稱是指定在組態檔的 appSettings 區段中，如下面的範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="a8698-110">The MSMQ queue name is specified in an appSettings section of the configuration file, as shown in the following sample configuration.</span></span>

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

> [!NOTE]
> <span data-ttu-id="a8698-111">佇列名稱會使用點 (.) 來代表本機電腦，並在其路徑中使用反斜線分隔符號。</span><span class="sxs-lookup"><span data-stu-id="a8698-111">The queue name uses a dot (.) for the local computer and backslash separators in its path.</span></span>

 <span data-ttu-id="a8698-112">用戶端會建立採購單，然後在異動範圍內提交採購單，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="a8698-112">The client creates a purchase order and submits the purchase order within the scope of a transaction, as shown in the following sample code.</span></span>

```csharp
// Create the purchase order
PurchaseOrder po = new PurchaseOrder();
// Fill in the details
...

OrderProcessorClient client = new OrderProcessorClient("OrderResponseEndpoint");

MsmqMessage<PurchaseOrder> ordermsg = new MsmqMessage<PurchaseOrder>(po);
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{
    client.SubmitPurchaseOrder(ordermsg);
    scope.Complete();
}
Console.WriteLine("Order has been submitted:{0}", po);

//Closing the client gracefully closes the connection and cleans up resources
client.Close();
```

 <span data-ttu-id="a8698-113">用戶端會依序使用自訂用戶端，將 MSMQ 訊息傳送至佇列。</span><span class="sxs-lookup"><span data-stu-id="a8698-113">The client uses a custom client in-order to send the MSMQ message to the queue.</span></span> <span data-ttu-id="a8698-114">因為接收和處理訊息的應用程式是 MSMQ 應用程式，而不是 WCF 應用程式，所以這兩個應用程式之間並沒有隱含的服務合約。</span><span class="sxs-lookup"><span data-stu-id="a8698-114">Because the application that receives and processes the message is an MSMQ application and not a WCF application, there is no implicit service contract between the two applications.</span></span> <span data-ttu-id="a8698-115">因此，我們無法在這個案例中使用 Svcutil.exe 工具來建立 Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8698-115">So, we cannot create a proxy using the Svcutil.exe tool in this scenario.</span></span>

 <span data-ttu-id="a8698-116">所有使用系結傳送訊息的 WCF 應用程式，自訂用戶端基本上都相同 `MsmqIntegration` 。</span><span class="sxs-lookup"><span data-stu-id="a8698-116">The custom client is essentially the same for all WCF applications that use the `MsmqIntegration` binding to send messages.</span></span> <span data-ttu-id="a8698-117">與其他用戶端不同的是，它並不包含服務作業的範圍，</span><span class="sxs-lookup"><span data-stu-id="a8698-117">Unlike other clients, it does not include a range of service operations.</span></span> <span data-ttu-id="a8698-118">而只是一項送出訊息的作業。</span><span class="sxs-lookup"><span data-stu-id="a8698-118">It is a submit message operation only.</span></span>

```csharp
[System.ServiceModel.ServiceContractAttribute(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}

public partial class OrderProcessorClient : System.ServiceModel.ClientBase<IOrderProcessor>, IOrderProcessor
{
    public OrderProcessorClient(){}

    public OrderProcessorClient(string configurationName)
        : base(configurationName)
    { }

    public OrderProcessorClient(System.ServiceModel.Channels.Binding binding, System.ServiceModel.EndpointAddress address)
        : base(binding, address)
    { }

    public void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg)
    {
        base.Channel.SubmitPurchaseOrder(msg);
    }
}
```

 <span data-ttu-id="a8698-119">當您執行範例時，用戶端與服務活動都會顯示在服務與用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="a8698-119">When you run the sample, the client and service activities are displayed in both the service and client console windows.</span></span> <span data-ttu-id="a8698-120">您可以查看來自用戶端的服務接收訊息。</span><span class="sxs-lookup"><span data-stu-id="a8698-120">You can see the service receive messages from the client.</span></span> <span data-ttu-id="a8698-121">在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。</span><span class="sxs-lookup"><span data-stu-id="a8698-121">Press ENTER in each console window to shut down the service and client.</span></span> <span data-ttu-id="a8698-122">請注意，因為佇列正在使用中，所以用戶端與服務不需要同時啟動與執行。</span><span class="sxs-lookup"><span data-stu-id="a8698-122">Note that because queuing is in use, the client and service do not have to be up and running at the same time.</span></span> <span data-ttu-id="a8698-123">例如，您可以執行用戶端，關閉用戶端，然後再啟動服務，服務還是會收到訊息。</span><span class="sxs-lookup"><span data-stu-id="a8698-123">For example, you could run the client, shut it down, and then start up the service and it would still receive its messages.</span></span>

> [!NOTE]
> <span data-ttu-id="a8698-124">這個範例需要安裝訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="a8698-124">This sample requires the installation of Message Queuing.</span></span> <span data-ttu-id="a8698-125">請參閱 [訊息佇列](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))中的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="a8698-125">See the installation instructions in [Message Queuing](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85)).</span></span>

## <a name="set-up-build-and-run-the-sample"></a><span data-ttu-id="a8698-126">設定、建立及執行範例</span><span class="sxs-lookup"><span data-stu-id="a8698-126">Set up, build, and run the sample</span></span>

1. <span data-ttu-id="a8698-127">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="a8698-127">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="a8698-128">如果服務優先執行，它就會檢查以確定佇列存在。</span><span class="sxs-lookup"><span data-stu-id="a8698-128">If the service is run first, it will check to ensure that the queue is present.</span></span> <span data-ttu-id="a8698-129">如果佇列不存在，服務將建立一個佇列。</span><span class="sxs-lookup"><span data-stu-id="a8698-129">If the queue is not present, the service will create one.</span></span> <span data-ttu-id="a8698-130">您可以先執行服務來建立佇列，也可以透過 MSMQ 佇列管理員建立佇列。</span><span class="sxs-lookup"><span data-stu-id="a8698-130">You can run the service first to create the queue, or you can create one via the MSMQ Queue Manager.</span></span> <span data-ttu-id="a8698-131">請依照下列步驟，在 Windows 2008 中建立佇列。</span><span class="sxs-lookup"><span data-stu-id="a8698-131">Follow these steps to create a queue in Windows 2008.</span></span>

    1. <span data-ttu-id="a8698-132">在 Visual Studio 2012 中開啟伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="a8698-132">Open Server Manager in Visual Studio 2012.</span></span>

    2. <span data-ttu-id="a8698-133">展開 [ **功能** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a8698-133">Expand the **Features** tab.</span></span>

    3. <span data-ttu-id="a8698-134">在 [**私用訊息佇列**] 上按一下滑鼠右鍵，然後選取 [**新增**  >  **私用佇列**]。</span><span class="sxs-lookup"><span data-stu-id="a8698-134">Right-click **Private Message Queues**, and then select **New** > **Private Queue**.</span></span>

    4. <span data-ttu-id="a8698-135">檢查 **交易** 式方塊。</span><span class="sxs-lookup"><span data-stu-id="a8698-135">Check the **Transactional** box.</span></span>

    5. <span data-ttu-id="a8698-136">輸入 `ServiceModelSamplesTransacted` 做為新佇列的名稱。</span><span class="sxs-lookup"><span data-stu-id="a8698-136">Enter `ServiceModelSamplesTransacted` as the name of the new queue.</span></span>

3. <span data-ttu-id="a8698-137">若要建立方案的 c # 或 Visual Basic 版本，請遵循 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="a8698-137">To build the C# or Visual Basic edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

4. <span data-ttu-id="a8698-138">若要在單一電腦設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="a8698-138">To run the sample in a single-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

## <a name="run-the-sample-across-computers"></a><span data-ttu-id="a8698-139">跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="a8698-139">Run the sample across computers</span></span>

1. <span data-ttu-id="a8698-140">將語言特定資料夾下 \service\bin\ 資料夾中的服務程式檔複製到服務電腦中。</span><span class="sxs-lookup"><span data-stu-id="a8698-140">Copy the service program files from the \service\bin\ folder, under the language-specific folder, to the service computer.</span></span>

2. <span data-ttu-id="a8698-141">將語言特定資料夾下 \client\bin\ 資料夾中的用戶端程式檔案複製到用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="a8698-141">Copy the client program files from the \client\bin\ folder, under the language-specific folder, to the client computer.</span></span>

3. <span data-ttu-id="a8698-142">在 Client.exe.config 檔案中，變更用戶端端點位址以取代 "." 指定服務電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="a8698-142">In the Client.exe.config file, change the client endpoint address to specify the service computer name instead of ".".</span></span>

4. <span data-ttu-id="a8698-143">在服務電腦上，從命令提示字元啟動 Service.exe。</span><span class="sxs-lookup"><span data-stu-id="a8698-143">On the service computer, launch Service.exe from a command prompt.</span></span>

5. <span data-ttu-id="a8698-144">在用戶端電腦上，從命令提示字元啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="a8698-144">On the client computer, launch Client.exe from a command prompt.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8698-145">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a8698-145">The samples may already be installed on your computer.</span></span> <span data-ttu-id="a8698-146">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="a8698-146">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="a8698-147">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="a8698-147">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="a8698-148">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="a8698-148">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\WcfToMsmq`

## <a name="see-also"></a><span data-ttu-id="a8698-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8698-149">See also</span></span>

- [<span data-ttu-id="a8698-150">作法：與 WCF 端點和訊息佇列應用程式交換訊息</span><span class="sxs-lookup"><span data-stu-id="a8698-150">How to: Exchange Messages with WCF Endpoints and Message Queuing Applications</span></span>](../feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- <span data-ttu-id="a8698-151">[訊息佇列](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="a8698-151">[Message Queuing](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))</span></span>

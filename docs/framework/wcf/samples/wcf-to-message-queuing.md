---
title: Windows Communication Foundation 至訊息佇列
ms.date: 03/30/2017
ms.assetid: 78d0d0c9-648e-4d4a-8f0a-14d9cafeead9
ms.openlocfilehash: 872632dc7d0a8a94f8829ffb3fe8eea2607697c8
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602333"
---
# <a name="windows-communication-foundation-to-message-queuing"></a>Windows Communication Foundation 至訊息佇列

這個範例會示範 Windows Communication Foundation （WCF）應用程式如何將訊息傳送至訊息佇列（MSMQ）應用程式。 這個服務是自我裝載的主控台應用程式，可讓您觀察接收佇列訊息的服務。 服務與用戶端不需要在相同時間執行。

 服務會接收佇列訊息，然後處理訂單。 服務會建立交易式佇列，然後設定已接收訊息的訊息處理常式，如下列範例程式碼所示。

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

 當訊息是由佇列接收時，就會叫用訊息處理常式 `ProcessOrder`。

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

 服務會從 MSMQ 訊息本文擷取 `ProcessOrder`，然後處理訂單。

 MSMQ 佇列名稱是指定在組態檔的 appSettings 區段中，如下面的範例組態所示。

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

> [!NOTE]
> 佇列名稱會使用點 (.) 來代表本機電腦，並在其路徑中使用反斜線分隔符號。

 用戶端會建立採購單，然後在異動範圍內提交採購單，如下列範例程式碼所示。

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

 用戶端會依序使用自訂用戶端，將 MSMQ 訊息傳送至佇列。 因為接收和處理訊息的應用程式是 MSMQ 應用程式，而不是 WCF 應用程式，所以這兩個應用程式之間不會有隱含的服務合約。 因此，我們無法在這個案例中使用 Svcutil.exe 工具來建立 Proxy。

 針對使用系結來傳送訊息的所有 WCF 應用程式，自訂用戶端基本上都相同 `MsmqIntegration` 。 與其他用戶端不同的是，它並不包含服務作業的範圍， 而只是一項送出訊息的作業。

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

 當您執行範例時，用戶端與服務活動都會顯示在服務與用戶端主控台視窗中。 您可以查看來自用戶端的服務接收訊息。 在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。 請注意，因為佇列正在使用中，所以用戶端與服務不需要同時啟動與執行。 例如，您可以執行用戶端，關閉用戶端，然後再啟動服務，服務還是會收到訊息。

> [!NOTE]
> 這個範例需要安裝訊息佇列。 請參閱[訊息佇列](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))中的安裝指示。

## <a name="set-up-build-and-run-the-sample"></a>設定、建立和執行範例

1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 如果服務優先執行，它就會檢查以確定佇列存在。 如果佇列不存在，服務將建立一個佇列。 您可以先執行服務來建立佇列，也可以透過 MSMQ 佇列管理員建立佇列。 請依照下列步驟，在 Windows 2008 中建立佇列。

    1. 在 Visual Studio 2012 中開啟伺服器管理員。

    2. 展開 [**功能**] 索引標籤。

    3. 以滑鼠右鍵按一下 [**私人訊息佇列**]，然後選取 [**新增**  >  **私用佇列**]。

    4. 選取 [**交易**式] 方塊。

    5. 輸入 `ServiceModelSamplesTransacted` 做為新佇列的名稱。

3. 若要建立方案的 c # 或 Visual Basic 版，請遵循[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示。

4. 若要在單一電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

## <a name="run-the-sample-across-computers"></a>跨電腦執行範例

1. 將語言特定資料夾下 \service\bin\ 資料夾中的服務程式檔複製到服務電腦中。

2. 將語言特定資料夾下 \client\bin\ 資料夾中的用戶端程式檔案複製到用戶端電腦。

3. 在 Client.exe.config 檔案中，變更用戶端端點位址以取代 "." 指定服務電腦名稱。

4. 在服務電腦上，從命令提示字元啟動 Service.exe。

5. 在用戶端電腦上，從命令提示字元啟動 Client.exe。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\WcfToMsmq`

## <a name="see-also"></a>請參閱

- [如何：與 WCF 端點和訊息佇列應用程式交換訊息](../feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [訊息佇列](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))

---
title: 訊息佇列至 Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 6d718eb0-9f61-4653-8a75-d2dac8fb3520
ms.openlocfilehash: 82e71afc911bff2504be15f7f9f2e736d943972b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584957"
---
# <a name="message-queuing-to-windows-communication-foundation"></a>訊息佇列至 Windows Communication Foundation

這個範例會示範訊息佇列（MSMQ）應用程式如何將 MSMQ 訊息傳送至 Windows Communication Foundation （WCF）服務。 這個服務是自我裝載的主控台應用程式，可讓您觀察接收佇列訊息的服務。

 服務合約為 `IOrderProcessor`，這會定義適合與佇列搭配使用的單向服務。 MSMQ 訊息沒有 Action 標頭，所以不可能自動將不同 MSMQ 訊息對應到作業合約。 因此，這時只能有一個作業合約。 如果您想要為服務定義一個以上的作業合約，應用程式就必須提供資訊，說明 MSMQ 訊息中的哪個標頭 (例如，標籤或 correlationID) 可以用來決定分派哪個作業合約。

 MSMQ 訊息不會包含有關作業合約的不同參數各自對應到哪個標頭的資訊。 參數的型別是 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>(`MsmqMessage<T>`)，其中包含基礎 MSMQ 訊息。 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>(`MsmqMessage<T>`) 類別中的型別 "T" 代表已序列化為 MSMQ 訊息本文的資料。 在這個範例中，`PurchaseOrder` 型別會序列化為 MSMQ 訊息本文。

 下列範例程式碼會示範訂單處理服務的服務合約。

```csharp
// Define a service contract.
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
[ServiceKnownType(typeof(PurchaseOrder))]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}
```

 服務會自我裝載。 使用 MSMQ 時，必須事先建立使用的佇列。 這個動作可手動或透過程式碼完成。 在這個範例中，服務會檢查佇列的存在，並在需要時建立佇列。 佇列名稱會從組態檔中讀取。

```csharp
public static void Main()
{
    // Get the MSMQ queue name from the application settings in
    // configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];
    // Create the MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName, true);
    …
}
```

 服務會建立並開啟 <xref:System.ServiceModel.ServiceHost> 的 `OrderProcessorService`，如下列範例程式碼所示。

```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
    serviceHost.Open();
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.ReadLine();
    serviceHost.Close();
}
```

 MSMQ 佇列名稱是指定在組態檔的 appSettings 區段中，如下面的範例組態所示。

> [!NOTE]
> 佇列名稱會使用點 (.) 來代表本機電腦，並在其路徑中使用反斜線分隔符號。 WCF 端點位址會指定 msmq.formatname 配置，並使用 localhost 作為本機電腦。 每個 MSMQ 格式名稱定址方針的佇列位址會遵循 msmq.formatname 配置。

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

 用戶端應用程式是使用 <xref:System.Messaging.MessageQueue.Send%2A> 方法將永久和異動訊息傳送至佇列的 MSMQ 應用程式，如下列範例程式碼所示。

```csharp
//Connect to the queue.
MessageQueue orderQueue = new MessageQueue(ConfigurationManager.AppSettings["orderQueueName"]);

// Create the purchase order.
PurchaseOrder po = new PurchaseOrder();
po.CustomerId = "somecustomer.com";
po.PONumber = Guid.NewGuid().ToString();

PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();
lineItem1.ProductId = "Blue Widget";
lineItem1.Quantity = 54;
lineItem1.UnitCost = 29.99F;

PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();
lineItem2.ProductId = "Red Widget";
lineItem2.Quantity = 890;
lineItem2.UnitCost = 45.89F;

po.orderLineItems = new PurchaseOrderLineItem[2];
po.orderLineItems[0] = lineItem1;
po.orderLineItems[1] = lineItem2;

// Submit the purchase order.
Message msg = new Message();
msg.Body = po;
//Create a transaction scope.
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{

    orderQueue.Send(msg, MessageQueueTransactionType.Automatic);
    // Complete the transaction.
    scope.Complete();

}
Console.WriteLine("Placed the order:{0}", po);
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 當您執行範例時，用戶端與服務活動都會顯示在服務與用戶端主控台視窗中。 您可以查看來自用戶端的服務接收訊息。 在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。 請注意，因為佇列正在使用中，所以用戶端與服務不需要同時啟動與執行。 例如，您可以執行用戶端，關閉用戶端，然後再啟動服務，服務還是會收到訊息。

## <a name="set-up-build-and-run-the-sample"></a>設定、建立和執行範例

1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 如果服務優先執行，它就會檢查以確定佇列存在。 如果佇列不存在，服務將建立一個佇列。 您可以先執行服務來建立佇列，也可以透過 MSMQ 佇列管理員建立佇列。 請依照下列步驟，在 Windows 2008 中建立佇列。

    1. 在 Visual Studio 2012 中開啟伺服器管理員。

    2. 展開 [**功能**] 索引標籤。

    3. 以滑鼠右鍵按一下 [**私人訊息佇列**]，然後選取 [**新增**]、[**私用佇列**]。

    4. 選取 [**交易**式] 方塊。

    5. 輸入 `ServiceModelSamplesTransacted` 做為新佇列的名稱。

3. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

4. 若要在單一電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

## <a name="run-the-sample-across-computers"></a>跨電腦執行範例

1. 將語言特定資料夾下 \service\bin\ 資料夾中的服務程式檔複製到服務電腦中。

2. 將語言特定資料夾下 \client\bin\ 資料夾中的用戶端程式檔案複製到用戶端電腦。

3. 在 Client.exe.config 檔案中，變更 orderQueueName 以取代 "." 指定服務電腦名稱。

4. 在服務電腦上，從命令提示字元啟動 Service.exe。

5. 在用戶端電腦上，從命令提示字元啟動 Client.exe。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MsmqToWcf`

## <a name="see-also"></a>請參閱

- [WCF 中的佇列](../feature-details/queues-in-wcf.md)
- [如何：與 WCF 端點和訊息佇列應用程式交換訊息](../feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [訊息佇列](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))

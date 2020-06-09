---
title: MSMQ 啟用
ms.date: 03/30/2017
ms.assetid: e3834149-7b8c-4a54-806b-b4296720f31d
ms.openlocfilehash: 0dbd24a612d56c0fe88066f625be2a8369b7df5b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602531"
---
# <a name="msmq-activation"></a><span data-ttu-id="b41d0-102">MSMQ 啟用</span><span class="sxs-lookup"><span data-stu-id="b41d0-102">MSMQ Activation</span></span>

<span data-ttu-id="b41d0-103">這個範例示範如何在 Windows Process Activation Service (WAS) 中裝載可從訊息佇列讀取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-103">This sample demonstrates how to host applications in Windows Process Activation Service (WAS) that are read from a message queue.</span></span> <span data-ttu-id="b41d0-104">這個範例會使用 `netMsmqBinding` ，而且是以[雙向通訊](two-way-communication.md)範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="b41d0-104">This sample uses the `netMsmqBinding` and is based on the [Two-Way Communication](two-way-communication.md) sample.</span></span> <span data-ttu-id="b41d0-105">本例中的服務是 Web 裝載的應用程式，而用戶端則會自我裝載並輸出至主控台，以便觀察所送出採購單的狀態。</span><span class="sxs-lookup"><span data-stu-id="b41d0-105">The service in this case is a Web-hosted application and the client is self-hosted and outputs to the console to observe the status of purchase orders submitted.</span></span>

> [!NOTE]
> <span data-ttu-id="b41d0-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="b41d0-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="b41d0-107">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b41d0-107">The samples may already be installed on your computer.</span></span> <span data-ttu-id="b41d0-108">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="b41d0-108">Check for the following (default) directory before continuing.</span></span>
>
> <span data-ttu-id="b41d0-109">\<InstallDrive>： \ WF_WCF_Samples</span><span class="sxs-lookup"><span data-stu-id="b41d0-109">\<InstallDrive>:\WF_WCF_Samples</span></span>
>
> <span data-ttu-id="b41d0-110">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （WCF）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WCF 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="b41d0-110">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all WCF and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="b41d0-111">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="b41d0-111">This sample is located in the following directory.</span></span>
>
> <span data-ttu-id="b41d0-112">\<InstallDrive>:\Samples\WCFWFCardSpace\WCF\Basic\Services\Hosting\WASHost\MsmqActivation.</span><span class="sxs-lookup"><span data-stu-id="b41d0-112">\<InstallDrive>:\Samples\WCFWFCardSpace\WCF\Basic\Services\Hosting\WASHost\MsmqActivation.</span></span>

<span data-ttu-id="b41d0-113">Windows 進程啟用服務（WAS）是適用于 Windows Server 2008 的新進程啟用機制，提供先前僅供 HTTP 應用程式使用非 HTTP 通訊協定之應用程式的類似 IIS 功能。</span><span class="sxs-lookup"><span data-stu-id="b41d0-113">Windows Process Activation Service (WAS), the new process activation mechanism for Windows Server 2008, provides IIS-like features that were previously only available to HTTP-based applications to applications that use non-HTTP protocols.</span></span> <span data-ttu-id="b41d0-114">Windows Communication Foundation （WCF）會使用接聽程式介面卡介面，來傳達透過 WCF 支援的非 HTTP 通訊協定（例如 TCP、具名管道和 MSMQ）接收的啟用要求。</span><span class="sxs-lookup"><span data-stu-id="b41d0-114">Windows Communication Foundation (WCF) uses the Listener Adapter interface to communicate activation requests that are received over the non-HTTP protocols supported by WCF, such as TCP, Named Pipes, and MSMQ.</span></span> <span data-ttu-id="b41d0-115">SMSvcHost.exe 中執行的 Managed Windows 服務會裝載可透過非 HTTP 通訊協定接收要求的功能。</span><span class="sxs-lookup"><span data-stu-id="b41d0-115">The functionality for receiving requests over non-HTTP protocols is hosted by managed Windows services running in SMSvcHost.exe.</span></span>

<span data-ttu-id="b41d0-116">Net.Msmq 接聽程式配接器服務 (NetMsmqActivator) 會根據佇列中的訊息啟動佇列應用程式。</span><span class="sxs-lookup"><span data-stu-id="b41d0-116">The Net.Msmq Listener Adapter service (NetMsmqActivator) activates queued applications based on messages in the queue.</span></span>

<span data-ttu-id="b41d0-117">用戶端會將採購單從異動範圍內傳送至服務。</span><span class="sxs-lookup"><span data-stu-id="b41d0-117">The client sends purchase orders to the service from within the scope of a transaction.</span></span> <span data-ttu-id="b41d0-118">服務則在交易中接收訂單，然後加以處理。</span><span class="sxs-lookup"><span data-stu-id="b41d0-118">The service receives the orders in a transaction and processes them.</span></span> <span data-ttu-id="b41d0-119">服務以訂單的狀態來回呼用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-119">The service then calls back the client with the status of the order.</span></span> <span data-ttu-id="b41d0-120">為了促進雙向通訊，用戶端與服務都會使用佇列將採購單和訂單狀態加入佇列。</span><span class="sxs-lookup"><span data-stu-id="b41d0-120">To facilitate two-way communication the client and service both use queues to enqueue purchase orders and order status.</span></span>

<span data-ttu-id="b41d0-121">服務合約 `IOrderProcessor` 會定義適合與佇列一起使用的單向服務作業。</span><span class="sxs-lookup"><span data-stu-id="b41d0-121">The service contract `IOrderProcessor` defines the one-way service operations that work with queuing.</span></span> <span data-ttu-id="b41d0-122">服務作業使用回覆端點，將訂單狀態傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-122">The service operation uses the reply endpoint to send order statuses to the client.</span></span> <span data-ttu-id="b41d0-123">回覆端點的位址是用來將訂單狀態傳回用戶端的佇列 URI。</span><span class="sxs-lookup"><span data-stu-id="b41d0-123">The reply endpoint's address is the URI of the queue used to send the order status back to the client.</span></span> <span data-ttu-id="b41d0-124">訂單處理應用程式會實作這個合約。</span><span class="sxs-lookup"><span data-stu-id="b41d0-124">The order processing application implements this contract.</span></span>

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true)]
    void SubmitPurchaseOrder(PurchaseOrder po,
                                           string reportOrderStatusTo);
}
```

<span data-ttu-id="b41d0-125">用戶端會指定要將訂單狀態傳送到其中的回覆合約。</span><span class="sxs-lookup"><span data-stu-id="b41d0-125">The reply contract to send order status to is specified by the client.</span></span> <span data-ttu-id="b41d0-126">用戶端會實作訂單狀態合約。</span><span class="sxs-lookup"><span data-stu-id="b41d0-126">The client implements the order status contract.</span></span> <span data-ttu-id="b41d0-127">服務則使用這個合約產生的用戶端將訂單狀態傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-127">The service uses the generated client of this contract to send order status back to the client.</span></span>

```csharp
[ServiceContract]
public interface IOrderStatus
{
    [OperationContract(IsOneWay = true)]
    void OrderStatus(string poNumber, string status);
}
```

<span data-ttu-id="b41d0-128">服務作業會處理已送出的採購單。</span><span class="sxs-lookup"><span data-stu-id="b41d0-128">The service operation processes the submitted purchase order.</span></span> <span data-ttu-id="b41d0-129"><xref:System.ServiceModel.OperationBehaviorAttribute> 會套用至服務作業以便在用來從佇列接收訊息的異動中指定自動進行登記，以及在服務作業完成時自動完成異動。</span><span class="sxs-lookup"><span data-stu-id="b41d0-129">The <xref:System.ServiceModel.OperationBehaviorAttribute> is applied to the service operation to specify automatic enlistment in the transaction that is used to receive the message from the queue and automatic completion of the transaction on completion of the service operation.</span></span> <span data-ttu-id="b41d0-130">`Orders` 類別會封裝訂單處理功能。</span><span class="sxs-lookup"><span data-stu-id="b41d0-130">The `Orders` class encapsulates order processing functionality.</span></span> <span data-ttu-id="b41d0-131">在本例中，這個類別會將採購單新增至字典。</span><span class="sxs-lookup"><span data-stu-id="b41d0-131">In this case, it adds the purchase order to a dictionary.</span></span> <span data-ttu-id="b41d0-132">`Orders` 類別中的作業可以使用服務作業所登記的交易。</span><span class="sxs-lookup"><span data-stu-id="b41d0-132">The transaction that the service operation enlisted in is available to the operations in the `Orders` class.</span></span>

<span data-ttu-id="b41d0-133">服務作業除了處理已送出的採購單外，也會將訂單狀態回覆至用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-133">The service operation, in addition to processing the submitted purchase order, replies back to the client about the status of the order.</span></span>

```csharp
public class OrderProcessorService : IOrderProcessor
{
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
    public void SubmitPurchaseOrder(PurchaseOrder po, string reportOrderStatusTo)
    {
        Orders.Add(po);
        Console.WriteLine("Processing {0} ", po);
        Console.WriteLine("Sending back order status information");
        NetMsmqBinding msmqCallbackBinding = new NetMsmqBinding();
        msmqCallbackBinding.Security.Mode = NetMsmqSecurityMode.None;
        OrderStatusClient client = new OrderStatusClient(msmqCallbackBinding, new EndpointAddress(reportOrderStatusTo));
        // please note that the same transaction that is used to dequeue purchase order is used
        // to send back order status
        using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
        {
            client.OrderStatus(po.PONumber, po.Status);
            scope.Complete();
        }
    }
}
```

<span data-ttu-id="b41d0-134">您可以使用組態檔來指定要使用的用戶端繫結。</span><span class="sxs-lookup"><span data-stu-id="b41d0-134">The client binding to use is specified using a configuration file.</span></span>

<span data-ttu-id="b41d0-135">MSMQ 佇列名稱是指定在組態檔的 appSettings 區段中。</span><span class="sxs-lookup"><span data-stu-id="b41d0-135">The MSMQ queue name is specified in an appSettings section of the configuration file.</span></span> <span data-ttu-id="b41d0-136">服務端點會定義在組態檔的 System.serviceModel 區段中。</span><span class="sxs-lookup"><span data-stu-id="b41d0-136">The endpoint for the service is defined in the System.serviceModel section of the configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="b41d0-137">MSMQ 佇列名稱與端點位址會使用稍微不同的定址慣例。</span><span class="sxs-lookup"><span data-stu-id="b41d0-137">The MSMQ queue name and endpoint address use slightly different addressing conventions.</span></span> <span data-ttu-id="b41d0-138">MSMQ 佇列名稱會使用點 (.) 來代表本機電腦，並在其路徑中使用反斜線分隔符號。</span><span class="sxs-lookup"><span data-stu-id="b41d0-138">The MSMQ queue name uses a dot (.) for the local computer and backslash separators in its path.</span></span> <span data-ttu-id="b41d0-139">WCF 端點位址會指定一個 net.tcp：配置、使用 "localhost" 代表本機電腦，並在其路徑中使用正斜線。</span><span class="sxs-lookup"><span data-stu-id="b41d0-139">The WCF endpoint address specifies a net.msmq: scheme, uses "localhost" for the local computer, and uses forward slashes in its path.</span></span> <span data-ttu-id="b41d0-140">若要讀取裝載於遠端電腦的佇列，請將 "." 和 "localhost" 取代成遠端電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="b41d0-140">To read from a queue that is hosted on the remote computer, replace the "." and "localhost" to the remote computer name.</span></span>

<span data-ttu-id="b41d0-141">帶有類別名稱的 .svc 檔案會用來裝載 WAS 中的服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="b41d0-141">A .svc file with the name of the class is used to host the service code in WAS.</span></span>

<span data-ttu-id="b41d0-142">Service.svc 檔案本身含有要建立 `OrderProcessorService` 的指示詞。</span><span class="sxs-lookup"><span data-stu-id="b41d0-142">The Service.svc file itself contains a directive to create the `OrderProcessorService`.</span></span>

`<%@ServiceHost language="c#" Debug="true" Service="Microsoft.ServiceModel.Samples.OrderProcessorService"%>`

<span data-ttu-id="b41d0-143">Service.svc 檔案還包含組件指示詞，可確保載入 System.Transactions.dll。</span><span class="sxs-lookup"><span data-stu-id="b41d0-143">The Service.svc file also contains an assembly directive to ensure that System.Transactions.dll is loaded.</span></span>

`<%@Assembly name="System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"%>`

<span data-ttu-id="b41d0-144">用戶端會建立一個交易範圍。</span><span class="sxs-lookup"><span data-stu-id="b41d0-144">The client creates a transaction scope.</span></span> <span data-ttu-id="b41d0-145">與服務的通訊會在異動範圍內進行，形成不可部分完成的原子單位 (Atomic Unit)，其中的訊息若不是全部成功，就是全部失敗。</span><span class="sxs-lookup"><span data-stu-id="b41d0-145">Communication with the service takes place within the scope of the transaction, causing it to be treated as an atomic unit where all messages succeed or fail.</span></span> <span data-ttu-id="b41d0-146">呼叫異動範圍上的 `Complete`，即可認可異動。</span><span class="sxs-lookup"><span data-stu-id="b41d0-146">The transaction is committed by calling `Complete` on the transaction scope.</span></span>

```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderStatusService)))
{
    // Open the ServiceHostBase to create listeners and start listening
    // for order status messages.
    serviceHost.Open();

    // Create a proxy with given client endpoint configuration
    OrderProcessorClient client = new OrderProcessorClient();

    // Create the purchase order
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

    //Create a transaction scope.
    using (TransactionScope scope = new
        TransactionScope(TransactionScopeOption.Required))
    {
        // Make a queued call to submit the purchase order
        client.SubmitPurchaseOrder(po,
       "net.msmq://localhost/private/ServiceModelSamplesOrder/OrderStatus");
        // Complete the transaction.
        scope.Complete();
    }

    //Closing the client gracefully closes the connection and cleans up
    //resources
    client.Close();

    Console.WriteLine();
    Console.WriteLine("Press <ENTER> to terminate client.");
    Console.ReadLine();

    // Close the ServiceHostBase to shutdown the service.
    serviceHost.Close();
    }
```

<span data-ttu-id="b41d0-147">用戶端程式碼會實作 `IOrderStatus` 合約以接收服務的訂單狀態。</span><span class="sxs-lookup"><span data-stu-id="b41d0-147">The client code implements the `IOrderStatus` contract to receive order status from the service.</span></span> <span data-ttu-id="b41d0-148">在此範例中，它會印出訂單狀態。</span><span class="sxs-lookup"><span data-stu-id="b41d0-148">In this case, it prints out the order status.</span></span>

```csharp
[ServiceBehavior]
public class OrderStatusService : IOrderStatus
{
    [OperationBehavior(TransactionAutoComplete = true,
                        TransactionScopeRequired = true)]
    public void OrderStatus(string poNumber, string status)
    {
        Console.WriteLine("Status of order {0}:{1} ",
                                         poNumber , status);
    }
}
```

<span data-ttu-id="b41d0-149">訂單狀態佇列會建立在 `Main` 方法中。</span><span class="sxs-lookup"><span data-stu-id="b41d0-149">The order status queue is created in the `Main` method.</span></span> <span data-ttu-id="b41d0-150">用戶端組態會包含訂單狀態服務組態來裝載訂單狀態服務，如下列範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="b41d0-150">The client configuration includes the order status service configuration to host the order status service, as shown in the following sample configuration.</span></span>

```xml
<appSettings>
    <!-- use appSetting to configure MSMQ queue name -->
    <add key="targetQueueName" value=".\private$\ServiceModelSamples/service.svc" />
    <add key="responseQueueName" value=".\private$\ServiceModelSamples/OrderStatus" />
  </appSettings>

<system.serviceModel>

    <services>
      <service
         name="Microsoft.ServiceModel.Samples.OrderStatusService">
        <!-- Define NetMsmqEndpoint -->
        <endpoint address="net.msmq://localhost/private/ServiceModelSamples/OrderStatus"
                  binding="netMsmqBinding"
                  contract="Microsoft.ServiceModel.Samples.IOrderStatus" />
      </service>
    </services>

    <client>
      <!-- Define NetMsmqEndpoint -->
      <endpoint name="OrderProcessorEndpoint"
                address="net.msmq://localhost/private/ServiceModelSamples/service.svc"
                binding="netMsmqBinding"
                contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />
    </client>

  </system.serviceModel>
```

<span data-ttu-id="b41d0-151">當您執行範例時，用戶端與服務活動都會顯示在伺服器與用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="b41d0-151">When you run the sample, the client and service activities are displayed in both the server and client console windows.</span></span> <span data-ttu-id="b41d0-152">您可以看到伺服器從用戶端接收訊息。</span><span class="sxs-lookup"><span data-stu-id="b41d0-152">You can see the server receive messages from the client.</span></span> <span data-ttu-id="b41d0-153">在每一個主控台視窗中按 ENTER 鍵，即可關閉伺服器與用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-153">Press ENTER in each console window to shut down the server and client.</span></span>

<span data-ttu-id="b41d0-154">用戶端會顯示伺服器傳送的訂單狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="b41d0-154">The client displays the order status information sent by the server:</span></span>

```console
Press <ENTER> to terminate client.
Status of order 70cf9d63-3dfa-4e69-81c2-23aa4478ebed :Pending
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="b41d0-155">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="b41d0-155">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="b41d0-156">請確定已安裝 IIS 7.0，因為 WAS 啟用時需要它。</span><span class="sxs-lookup"><span data-stu-id="b41d0-156">Ensure that IIS 7.0 is installed, as it is required for WAS activation.</span></span>

2. <span data-ttu-id="b41d0-157">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b41d0-157">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span> <span data-ttu-id="b41d0-158">此外，您必須安裝 WCF 非 HTTP 啟用元件：</span><span class="sxs-lookup"><span data-stu-id="b41d0-158">In addition, you must install the WCF non-HTTP activation components:</span></span>

    1. <span data-ttu-id="b41d0-159">在 [開始]\*\*\*\* 功能表內選擇 [控制台]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b41d0-159">From the **Start** menu, choose **Control Panel**.</span></span>

    2. <span data-ttu-id="b41d0-160">選取 [**程式和功能**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-160">Select **Programs and Features**.</span></span>

    3. <span data-ttu-id="b41d0-161">按一下 [**開啟或關閉 Windows 功能**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-161">Click **Turn Windows Features on or off**.</span></span>

    4. <span data-ttu-id="b41d0-162">在 [**功能摘要**] 下，按一下 [**新增功能**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-162">Under **Features Summary**, click **Add Features**.</span></span>

    5. <span data-ttu-id="b41d0-163">展開 [ **Microsoft .NET Framework 3.0** ] 節點，並檢查 [ **Windows Communication Foundation 非 HTTP 啟用**] 功能。</span><span class="sxs-lookup"><span data-stu-id="b41d0-163">Expand the **Microsoft .NET Framework 3.0** node and check the **Windows Communication Foundation Non-HTTP Activation** feature.</span></span>

3. <span data-ttu-id="b41d0-164">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="b41d0-164">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

4. <span data-ttu-id="b41d0-165">從命令視窗執行 client.exe，以執行用戶端。</span><span class="sxs-lookup"><span data-stu-id="b41d0-165">Run the client by executing client.exe from a command window.</span></span> <span data-ttu-id="b41d0-166">這會建立佇列，並將訊息傳送給它。</span><span class="sxs-lookup"><span data-stu-id="b41d0-166">This creates the queue and sends a message to it.</span></span> <span data-ttu-id="b41d0-167">讓用戶端繼續執行，以便查看服務讀取訊息的結果。</span><span class="sxs-lookup"><span data-stu-id="b41d0-167">Leave the client running to see the result of the service reading the message</span></span>

5. <span data-ttu-id="b41d0-168">根據預設，MSMQ 啟動服務會以網路服務的身分執行。</span><span class="sxs-lookup"><span data-stu-id="b41d0-168">The MSMQ activation service runs as Network Service by default.</span></span> <span data-ttu-id="b41d0-169">因此，用來啟動應用程式的佇列必須讓「網路服務」擁有接收和查看其中訊息的權限。</span><span class="sxs-lookup"><span data-stu-id="b41d0-169">Therefore, the queue that is used to activate the application must have receive and peek permissions for Network Service.</span></span> <span data-ttu-id="b41d0-170">您可以使用訊息佇列 MMC 來新增此權限：</span><span class="sxs-lookup"><span data-stu-id="b41d0-170">This can be added by using the Message Queuing MMC:</span></span>

    1. <span data-ttu-id="b41d0-171">在 [**開始**] 功能表中，按一下 [**執行**]，然後輸入 `Compmgmt.msc` ，再按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="b41d0-171">From the **Start** menu, click **Run**, then type `Compmgmt.msc` and press ENTER.</span></span>

    2. <span data-ttu-id="b41d0-172">在 [**服務和應用程式**] 底下，展開 [**訊息佇列**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-172">Under **Services and Applications**, expand **Message Queuing**.</span></span>

    3. <span data-ttu-id="b41d0-173">按一下 [**私用佇列**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-173">Click **Private Queues**.</span></span>

    4. <span data-ttu-id="b41d0-174">以滑鼠右鍵按一下佇列（servicemodelsamples/Service .svc），然後選擇 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-174">Right-click the queue (servicemodelsamples/Service.svc) and choose **Properties**.</span></span>

    5. <span data-ttu-id="b41d0-175">在 [**安全性**] 索引標籤上，按一下 [**新增**]，並提供網路服務的查看和接收許可權。</span><span class="sxs-lookup"><span data-stu-id="b41d0-175">On the **Security** tab, click **Add** and give peek and receive permissions to Network Service.</span></span>

6. <span data-ttu-id="b41d0-176">設定 Windows Process Activation Service (WAS) 以支援 MSMQ 啟動。</span><span class="sxs-lookup"><span data-stu-id="b41d0-176">Configure the Windows Process Activation Service (WAS) to support MSMQ activation.</span></span>

    <span data-ttu-id="b41d0-177">為了方便起見，下列步驟會以範例目錄中名為 AddMsmqSiteBinding.cmd 的批次檔實作。</span><span class="sxs-lookup"><span data-stu-id="b41d0-177">As a convenience, the following steps are implemented in a batch file called AddMsmqSiteBinding.cmd located in the sample directory.</span></span>

    1. <span data-ttu-id="b41d0-178">若要支援 net.msmq 啟動，預設的網站必須先繫結至 net.msmq 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b41d0-178">To support net.msmq activation, the default Web site must first be bound to the net.msmq protocol.</span></span> <span data-ttu-id="b41d0-179">使用以 IIS 7.0 管理工具集安裝的 appcmd.exe 完成此操作。</span><span class="sxs-lookup"><span data-stu-id="b41d0-179">This can be done using appcmd.exe, which is installed with the IIS 7.0 management toolset.</span></span> <span data-ttu-id="b41d0-180">從提高權限的 (系統管理員) 命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b41d0-180">From an elevated (administrator) command prompt, run the following command.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        -+bindings.[protocol='net.msmq',bindingInformation='localhost']
        ```

        > [!NOTE]
        > <span data-ttu-id="b41d0-181">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b41d0-181">This command is a single line of text.</span></span>

        <span data-ttu-id="b41d0-182">此命令會將 net.msmq 網站繫結加入至預設網站。</span><span class="sxs-lookup"><span data-stu-id="b41d0-182">This command adds a net.msmq site binding to the default Web site.</span></span>

    2. <span data-ttu-id="b41d0-183">雖然網站中的所有應用程式會共用一般 net.msmq 繫結，但是每個應用程式都可以個別啟用 net.msmq 支援。</span><span class="sxs-lookup"><span data-stu-id="b41d0-183">Although all applications within a site share a common net.msmq binding, each application can enable net.msmq support individually.</span></span> <span data-ttu-id="b41d0-184">若要啟用 /servicemodelsamples 應用程式的 net.msmq，請從提高權限的命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b41d0-184">To enable net.msmq for the /servicemodelsamples application, run the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.msmq
        ```

        > [!NOTE]
        > <span data-ttu-id="b41d0-185">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b41d0-185">This command is a single line of text.</span></span>

        <span data-ttu-id="b41d0-186">此命令可讓您使用和來存取/servicemodelsamples 應用程式 `http://localhost/servicemodelsamples` `net.msmq://localhost/servicemodelsamples` 。</span><span class="sxs-lookup"><span data-stu-id="b41d0-186">This command enables the /servicemodelsamples application to be accessed using `http://localhost/servicemodelsamples` and `net.msmq://localhost/servicemodelsamples`.</span></span>

7. <span data-ttu-id="b41d0-187">如果您之前未曾這麼做，請確定 MSMQ 啟動服務已啟用。</span><span class="sxs-lookup"><span data-stu-id="b41d0-187">If you have not done so previously, ensure that the MSMQ activation service is enabled.</span></span> <span data-ttu-id="b41d0-188">在 [**開始**] 功能表中，按一下 [**執行**]，然後輸入 `Services.msc` 。</span><span class="sxs-lookup"><span data-stu-id="b41d0-188">From the **Start** menu, click **Run**, and type `Services.msc`.</span></span> <span data-ttu-id="b41d0-189">搜尋 [Net.tcp 接聽程式**介面卡]** 的服務清單。</span><span class="sxs-lookup"><span data-stu-id="b41d0-189">Search the list of services for the **Net.Msmq Listener Adapter**.</span></span> <span data-ttu-id="b41d0-190">按一下滑鼠右鍵並選取 [內容]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b41d0-190">Right-click and select **Properties**.</span></span> <span data-ttu-id="b41d0-191">將 [**啟動類型**] 設定為 [**自動**]，按一下 [套用] **，然後按一下**[**開始**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b41d0-191">Set the **Startup Type** to **Automatic**, click **Apply** and click the **Start** button.</span></span> <span data-ttu-id="b41d0-192">這個步驟只需要在第一次使用 Net.Msmq 接聽程式配接器服務之前執行一次。</span><span class="sxs-lookup"><span data-stu-id="b41d0-192">This step must only be done once prior to the first usage of the Net.Msmq Listener Adapter service.</span></span>

8. <span data-ttu-id="b41d0-193">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="b41d0-193">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span> <span data-ttu-id="b41d0-194">此外，還要在發送採購單的用戶端上變更程式碼，以便在送出採購單時將電腦名稱反映於佇列的 URI。</span><span class="sxs-lookup"><span data-stu-id="b41d0-194">Additionally, change the code on the client that submits the purchase order to reflect the computer name in the URI of the queue when submitting the purchase order.</span></span> <span data-ttu-id="b41d0-195">使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b41d0-195">Use the following code:</span></span>

    ```csharp
    client.SubmitPurchaseOrder(po, "net.msmq://localhost/private/ServiceModelSamples/OrderStatus");
    ```

9. <span data-ttu-id="b41d0-196">移除您為此範例加入的 net.msmq 網站繫結。</span><span class="sxs-lookup"><span data-stu-id="b41d0-196">Remove the net.msmq site binding you added for this sample.</span></span>

    <span data-ttu-id="b41d0-197">為了方便起見，下列步驟會以範例目錄中名為 RemoveMsmqSiteBinding.cmd 的批次檔實作：</span><span class="sxs-lookup"><span data-stu-id="b41d0-197">As a convenience, the following steps are implemented in a batch file called RemoveMsmqSiteBinding.cmd located in the sample directory:</span></span>

    1. <span data-ttu-id="b41d0-198">從提高權限的命令提示字元中執行下列命令，以從啟用的通訊協定清單中移除 net.msmq。</span><span class="sxs-lookup"><span data-stu-id="b41d0-198">Remove net.msmq from the list of enabled protocols by running the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > <span data-ttu-id="b41d0-199">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b41d0-199">This command is a single line of text.</span></span>

    2. <span data-ttu-id="b41d0-200">從提高權限的命令提示字元中執行下列命令以移除 net.msmq 網站繫結。</span><span class="sxs-lookup"><span data-stu-id="b41d0-200">Remove the net.msmq site binding by running the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" --bindings.[protocol='net.msmq',bindingInformation='localhost']
        ```

        > [!NOTE]
        > <span data-ttu-id="b41d0-201">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b41d0-201">This command is a single line of text.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b41d0-202">執行批次檔會將 DefaultAppPool 重設為使用 .NET Framework 2.0 版執行。</span><span class="sxs-lookup"><span data-stu-id="b41d0-202">Running the batch file will reset the DefaultAppPool to run using .NET Framework version 2.0.</span></span>

<span data-ttu-id="b41d0-203">根據預設，安全性會透過 `netMsmqBinding` 繫結傳輸啟用。</span><span class="sxs-lookup"><span data-stu-id="b41d0-203">By default with the `netMsmqBinding` binding transport, security is enabled.</span></span> <span data-ttu-id="b41d0-204">`MsmqAuthenticationMode` 和 `MsmqProtectionLevel` 這兩個屬性會共同決定傳輸安全性的類型。</span><span class="sxs-lookup"><span data-stu-id="b41d0-204">Two properties, `MsmqAuthenticationMode` and `MsmqProtectionLevel`, together determine the type of transport security.</span></span> <span data-ttu-id="b41d0-205">根據預設，驗證模式會設定為 `Windows`，保護層級則會設定為 `Sign`。</span><span class="sxs-lookup"><span data-stu-id="b41d0-205">By default the authentication mode is set to `Windows` and the protection level is set to `Sign`.</span></span> <span data-ttu-id="b41d0-206">若要 MSMQ 提供驗證和簽署功能，則 MSMQ 必須是網域的一部分。</span><span class="sxs-lookup"><span data-stu-id="b41d0-206">For MSMQ to provide the authentication and signing feature, it must be part of a domain.</span></span> <span data-ttu-id="b41d0-207">如果您在不屬於網域的電腦上執行這個範例，就會收到下列錯誤：「使用者的內部訊息佇列憑證不存在」。</span><span class="sxs-lookup"><span data-stu-id="b41d0-207">If you run this sample on a computer that is not part of a domain, the following error is received: "User's internal message queuing certificate does not exist".</span></span>

### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup"></a><span data-ttu-id="b41d0-208">若要在加入至工作群組的電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="b41d0-208">To run the sample on a computer joined to a workgroup</span></span>

1. <span data-ttu-id="b41d0-209">如果您的電腦不是網域的一部分，請將驗證模式和保護層級設定為 None，以關閉傳輸安全性，如下面的範例組態所示：</span><span class="sxs-lookup"><span data-stu-id="b41d0-209">If your computer is not part of a domain, turn off transport security by setting the authentication mode and protection level to none as shown in the following sample configuration.</span></span>

    ```xml
    <bindings>
        <netMsmqBinding>
            <binding configurationName="TransactedBinding">
                <security mode="None"/>
            </binding>
        </netMsmqBinding>
    </bindings>
    ```

2. <span data-ttu-id="b41d0-210">請先變更伺服器與用戶端上的組態，再執行範例。</span><span class="sxs-lookup"><span data-stu-id="b41d0-210">Change the configuration on both the server and the client before you run the sample.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b41d0-211">將 `security mode` 設定為 `None`，相當於將 `MsmqAuthenticationMode`、`MsmqProtectionLevel` 和 `Message` 安全性設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="b41d0-211">Setting `security mode` to `None` is equivalent to setting `MsmqAuthenticationMode`, `MsmqProtectionLevel` and `Message` security to `None`.</span></span>

3. <span data-ttu-id="b41d0-212">若要在已加入工作群組的電腦中啟用啟動作業，則啟動服務和背景工作處理序都必須透過特定使用者帳戶 (這兩者的帳戶必須相同) 來執行，而且佇列必須具有特定使用者帳戶的 ACL。</span><span class="sxs-lookup"><span data-stu-id="b41d0-212">To enable activation in a computer joined to a workgroup, both the activation service and the worker process must be run with a specific user account (must be same for both) and the queue must have ACLs for the specific user account.</span></span>

     <span data-ttu-id="b41d0-213">若要變更背景工作處理序用以執行的身分識別：</span><span class="sxs-lookup"><span data-stu-id="b41d0-213">To change the identity that the worker process runs under:</span></span>

    1. <span data-ttu-id="b41d0-214">執行 Inetmgr.exe。</span><span class="sxs-lookup"><span data-stu-id="b41d0-214">Run Inetmgr.exe.</span></span>

    2. <span data-ttu-id="b41d0-215">在 [**應用程式**集區] 下，以滑鼠右鍵按一下**AppPool** （通常是**DefaultAppPool**），然後選擇 [**設定應用程式集區預設值**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-215">Under **Application Pools**, right-click the **AppPool** (typically **DefaultAppPool**) and choose **Set Application Pool Defaults…**.</span></span>

    3. <span data-ttu-id="b41d0-216">變更 Identity 屬性以使用特定的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b41d0-216">Change the Identity properties to use the specific user account.</span></span>

     <span data-ttu-id="b41d0-217">若要變更啟動服務用以執行的身分識別：</span><span class="sxs-lookup"><span data-stu-id="b41d0-217">To change the identity that the Activation Service runs under:</span></span>

    1. <span data-ttu-id="b41d0-218">執行 Services.msc。</span><span class="sxs-lookup"><span data-stu-id="b41d0-218">Run Services.msc.</span></span>

    2. <span data-ttu-id="b41d0-219">在**MsmqListener 介面卡**上按一下滑鼠右鍵，然後選擇 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="b41d0-219">Right-click the **Net.MsmqListener Adapter**, and choose **Properties**.</span></span>

4. <span data-ttu-id="b41d0-220">在 [**登**入] 索引標籤中變更帳戶。</span><span class="sxs-lookup"><span data-stu-id="b41d0-220">Change the account in the **LogOn** tab.</span></span>

5. <span data-ttu-id="b41d0-221">在工作群組中，服務還必須使用不受限制的權杖來執行。</span><span class="sxs-lookup"><span data-stu-id="b41d0-221">In workgroup, the service must also run using an unrestricted token.</span></span> <span data-ttu-id="b41d0-222">若要這麼做，請在命令視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b41d0-222">To do this, run the following in a command window:</span></span>

    ```console
    sc sidtype netmsmqactivator unrestricted
    ```

## <a name="see-also"></a><span data-ttu-id="b41d0-223">請參閱</span><span class="sxs-lookup"><span data-stu-id="b41d0-223">See also</span></span>

- <span data-ttu-id="b41d0-224">[AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="b41d0-224">[AppFabric Hosting and Persistence Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span></span>

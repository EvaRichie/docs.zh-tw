---
title: 雙向通訊
ms.date: 03/30/2017
ms.assetid: fb64192d-b3ea-4e02-9fb3-46a508d26c60
ms.openlocfilehash: 291380d656b0e22c7fdf1cb291c45d05359a95c8
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591263"
---
# <a name="two-way-communication"></a><span data-ttu-id="c2bce-102">雙向通訊</span><span class="sxs-lookup"><span data-stu-id="c2bce-102">Two-Way Communication</span></span>
<span data-ttu-id="c2bce-103">這個範例會示範如何透過 MSMQ 來執行交易雙向佇列通訊。</span><span class="sxs-lookup"><span data-stu-id="c2bce-103">This sample demonstrates how to perform transacted two-way queued communication over MSMQ.</span></span> <span data-ttu-id="c2bce-104">這個範例會使用 `netMsmqBinding` 繫結。</span><span class="sxs-lookup"><span data-stu-id="c2bce-104">This sample uses the `netMsmqBinding` binding.</span></span> <span data-ttu-id="c2bce-105">在此範例中，服務是自我裝載的主控台應用程式，可讓您觀察接收佇列訊息的服務。</span><span class="sxs-lookup"><span data-stu-id="c2bce-105">In this case, the service is a self-hosted console application that allows you to observe the service receiving queued messages.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c2bce-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="c2bce-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="c2bce-107">這個範例是以交易式[MSMQ](transacted-msmq-binding.md)系結為基礎。</span><span class="sxs-lookup"><span data-stu-id="c2bce-107">This sample is based on the [Transacted MSMQ Binding](transacted-msmq-binding.md).</span></span>  
  
 <span data-ttu-id="c2bce-108">在佇列通訊中，用戶端會使用佇列與服務通訊。</span><span class="sxs-lookup"><span data-stu-id="c2bce-108">In queued communication, the client communicates to the service using a queue.</span></span> <span data-ttu-id="c2bce-109">用戶端會將訊息傳送至佇列，而服務會從佇列接收訊息。</span><span class="sxs-lookup"><span data-stu-id="c2bce-109">The client sends messages to a queue, and the service receives messages from the queue.</span></span> <span data-ttu-id="c2bce-110">因此，服務與用戶端不需同時執行，就能使用佇列通訊。</span><span class="sxs-lookup"><span data-stu-id="c2bce-110">The service and client therefore, do not have to be running at the same time to communicate using a queue.</span></span>  
  
 <span data-ttu-id="c2bce-111">這個範例會示範使用佇列的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="c2bce-111">This sample demonstrates 2-way communication using queues.</span></span> <span data-ttu-id="c2bce-112">用戶端會將採購單從交易範圍內傳送至佇列。</span><span class="sxs-lookup"><span data-stu-id="c2bce-112">The client sends purchase orders to the queue from within the scope of a transaction.</span></span> <span data-ttu-id="c2bce-113">服務會接收訂單，處理訂單，然後從在交易範圍內的佇列，根據訂單狀態回呼 (Call Back) 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c2bce-113">The service receives the orders, processes the order and then calls back the client with the status of the order from the queue within the scope of a transaction.</span></span> <span data-ttu-id="c2bce-114">為了促進雙向通訊，用戶端與服務都會使用佇列將採購單和訂單狀態加入佇列。</span><span class="sxs-lookup"><span data-stu-id="c2bce-114">To facilitate two-way communication the client and service both use queues to enqueue purchase orders and order status.</span></span>  
  
 <span data-ttu-id="c2bce-115">服務合約 `IOrderProcessor` 會定義適合與佇列一起使用的單向服務作業。</span><span class="sxs-lookup"><span data-stu-id="c2bce-115">The service contract `IOrderProcessor` defines one-way service operations that suit the use of queuing.</span></span> <span data-ttu-id="c2bce-116">服務作業包含可用來傳送訂單狀態的回覆端點。</span><span class="sxs-lookup"><span data-stu-id="c2bce-116">The service operation includes the reply endpoint to use to send the order statuses to.</span></span> <span data-ttu-id="c2bce-117">回覆端點是將訂單狀態傳回用戶端的佇列 URI。</span><span class="sxs-lookup"><span data-stu-id="c2bce-117">The reply endpoint is the URI of the queue to send the order status back to the client.</span></span> <span data-ttu-id="c2bce-118">訂單處理應用程式會實作這個合約。</span><span class="sxs-lookup"><span data-stu-id="c2bce-118">The order processing application implements this contract.</span></span>  

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true)]  
    void SubmitPurchaseOrder(PurchaseOrder po, string
                                  reportOrderStatusTo);  
}
```
  
 <span data-ttu-id="c2bce-119">用來傳送訂單狀態的回覆合約是由用戶端指定。</span><span class="sxs-lookup"><span data-stu-id="c2bce-119">The reply contract to send order status is specified by the client.</span></span> <span data-ttu-id="c2bce-120">用戶端會實作訂單狀態合約。</span><span class="sxs-lookup"><span data-stu-id="c2bce-120">The client implements the order status contract.</span></span> <span data-ttu-id="c2bce-121">服務會使用這個合約產生的 Proxy 將訂單狀態傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c2bce-121">The service uses the generated proxy of this contract to send order status back to the client.</span></span>  

```csharp
[ServiceContract]  
public interface IOrderStatus  
{  
    [OperationContract(IsOneWay = true)]  
    void OrderStatus(string poNumber, string status);  
}  
```

 <span data-ttu-id="c2bce-122">服務作業會處理已送出的採購單。</span><span class="sxs-lookup"><span data-stu-id="c2bce-122">The service operation processes the submitted purchase order.</span></span> <span data-ttu-id="c2bce-123"><xref:System.ServiceModel.OperationBehaviorAttribute> 會套用至服務作業，以便指定自動登記在用來從佇列接收訊息的交易中，以及指定在服務作業完成時自動完成交易。</span><span class="sxs-lookup"><span data-stu-id="c2bce-123">The <xref:System.ServiceModel.OperationBehaviorAttribute> is applied to the service operation to specify automatic enlistment in a transaction that is used to receive the message from the queue and automatic completion of transactions on completion of the service operation.</span></span> <span data-ttu-id="c2bce-124">`Orders` 類別會封裝訂單處理功能。</span><span class="sxs-lookup"><span data-stu-id="c2bce-124">The `Orders` class encapsulates order processing functionality.</span></span> <span data-ttu-id="c2bce-125">在本例中，這個類別會將採購單新增至字典。</span><span class="sxs-lookup"><span data-stu-id="c2bce-125">In this case, it adds the purchase order to a dictionary.</span></span> <span data-ttu-id="c2bce-126">`Orders` 類別中的作業可以使用服務作業所登記的交易。</span><span class="sxs-lookup"><span data-stu-id="c2bce-126">The transaction that the service operation enlisted in is available to the operations in the `Orders` class.</span></span>  
  
 <span data-ttu-id="c2bce-127">除了處理已送出的採購單，服務作業也會將訂單狀態回覆至用戶端。</span><span class="sxs-lookup"><span data-stu-id="c2bce-127">The service operation, in addition to processing the submitted purchase order, replies back to the client on the status of the order.</span></span>  

```csharp
[OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
public void SubmitPurchaseOrder(PurchaseOrder po, string reportOrderStatusTo)  
{  
    Orders.Add(po);  
    Console.WriteLine("Processing {0} ", po);  
    Console.WriteLine("Sending back order status information");  
    NetMsmqBinding msmqCallbackBinding = new NetMsmqBinding("ClientCallbackBinding");  
    OrderStatusClient client = new OrderStatusClient(msmqCallbackBinding, new EndpointAddress(reportOrderStatusTo));  
  
    // Please note that the same transaction that is used to dequeue the purchase order is used  
    // to send back order status.  
    using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
    {  
        client.OrderStatus(po.PONumber, po.Status);  
        scope.Complete();  
    }  
    //Close the client.  
    client.Close();  
}  
```

 <span data-ttu-id="c2bce-128">MSMQ 佇列名稱是指定在組態檔的 appSettings 區段中。</span><span class="sxs-lookup"><span data-stu-id="c2bce-128">The MSMQ queue name is specified in an appSettings section of the configuration file.</span></span> <span data-ttu-id="c2bce-129">服務端點會定義在組態檔的 System.ServiceModel 區段中。</span><span class="sxs-lookup"><span data-stu-id="c2bce-129">The endpoint for the service is defined in the System.ServiceModel section of the configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c2bce-130">MSMQ 佇列名稱與端點位址會使用稍微不同的定址慣例。</span><span class="sxs-lookup"><span data-stu-id="c2bce-130">The MSMQ queue name and endpoint address use slightly different addressing conventions.</span></span> <span data-ttu-id="c2bce-131">MSMQ 佇列名稱會使用點 (.) 來代表本機電腦，並在其路徑中使用反斜線分隔符號。</span><span class="sxs-lookup"><span data-stu-id="c2bce-131">The MSMQ queue name uses a dot (.) for the local machine and backslash separators in its path.</span></span> <span data-ttu-id="c2bce-132">Windows Communication Foundation （WCF）端點位址會指定一個 net.tcp：配置、使用 "localhost" 代表本機電腦，並在其路徑中使用正斜線。</span><span class="sxs-lookup"><span data-stu-id="c2bce-132">The Windows Communication Foundation (WCF) endpoint address specifies a net.msmq: scheme, uses "localhost" for the local machine, and uses forward slashes in its path.</span></span> <span data-ttu-id="c2bce-133">若要讀取裝載於遠端電腦的佇列，請將 "." 和 "localhost" 取代成遠端電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="c2bce-133">To read from a queue that is hosted on the remote machine, replace the "." and "localhost" to the remote machine name.</span></span>  
  
 <span data-ttu-id="c2bce-134">服務會自我裝載。</span><span class="sxs-lookup"><span data-stu-id="c2bce-134">The service is self hosted.</span></span> <span data-ttu-id="c2bce-135">使用 MSMQ 傳輸時，必須事先建立使用的佇列。</span><span class="sxs-lookup"><span data-stu-id="c2bce-135">When using the MSMQ transport, the queue used must be created in advance.</span></span> <span data-ttu-id="c2bce-136">這個動作可手動或透過程式碼完成。</span><span class="sxs-lookup"><span data-stu-id="c2bce-136">This can be done manually or through code.</span></span> <span data-ttu-id="c2bce-137">在這個範例中，服務會檢查佇列是否存在，並在需要時建立佇列。</span><span class="sxs-lookup"><span data-stu-id="c2bce-137">In this sample, the service checks for the existence of the queue and creates it, if necessary.</span></span> <span data-ttu-id="c2bce-138">佇列名稱會從組態檔中讀取。</span><span class="sxs-lookup"><span data-stu-id="c2bce-138">The queue name is read from the configuration file.</span></span> <span data-ttu-id="c2bce-139">[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)會使用基底位址來產生服務的 proxy。</span><span class="sxs-lookup"><span data-stu-id="c2bce-139">The base address is used by the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to generate the proxy to the service.</span></span>  

```csharp
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Get MSMQ queue name from appSettings in configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
  
    // Create a ServiceHost for the OrderProcessorService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
    {  
        // Open the ServiceHost to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
    }  
}  
```

 <span data-ttu-id="c2bce-140">用戶端會建立交易。</span><span class="sxs-lookup"><span data-stu-id="c2bce-140">The client creates a transaction.</span></span> <span data-ttu-id="c2bce-141">與佇列的通訊會發生在異動範圍內，這點會導致其被視為不可部分完成的原子單位 (Atomic Unit)，其中的訊息若不是全部成功，就是全部失敗。</span><span class="sxs-lookup"><span data-stu-id="c2bce-141">Communication with the queue takes place within the scope of the transaction, causing it to be treated as an atomic unit where all messages succeed or fail.</span></span>  

```csharp
// Create a ServiceHost for the OrderStatus service type.  
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderStatusService)))  
{  
  
    // Open the ServiceHostBase to create listeners and start listening for order status messages.  
    serviceHost.Open();  
  
    // Create the purchase order.  
    ...  
  
    // Create a client with given client endpoint configuration.  
    OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");  
  
    //Create a transaction scope.  
    using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
    {  
        string hostName = Dns.GetHostName();  
  
        // Make a queued call to submit the purchase order.  
        client.SubmitPurchaseOrder(po, "net.msmq://" + hostName + "/private/ServiceModelSamplesTwo-way/OrderStatus");  
  
        // Complete the transaction.  
        scope.Complete();  
    }  
  
    //Close down the client.  
    client.Close();  
  
    Console.WriteLine();  
    Console.WriteLine("Press <ENTER> to terminate client.");  
    Console.ReadLine();  
  
    // Close the ServiceHost to shutdown the service.  
    serviceHost.Close();  
}  
```

 <span data-ttu-id="c2bce-142">用戶端程式碼會實作 `IOrderStatus` 合約以接收服務的訂單狀態。</span><span class="sxs-lookup"><span data-stu-id="c2bce-142">The client code implements the `IOrderStatus` contract to receive order status from the service.</span></span> <span data-ttu-id="c2bce-143">在此範例中，它會印出訂單狀態。</span><span class="sxs-lookup"><span data-stu-id="c2bce-143">In this case, it prints out the order status.</span></span>  

```csharp
[ServiceBehavior]  
public class OrderStatusService : IOrderStatus  
{  
    [OperationBehavior(TransactionAutoComplete = true,
                        TransactionScopeRequired = true)]  
    public void OrderStatus(string poNumber, string status)  
    {  
        Console.WriteLine("Status of order {0}:{1} ", poNumber ,
                                                           status);  
    }  
}  
```

 <span data-ttu-id="c2bce-144">訂單狀態佇列會建立在 `Main` 方法中。</span><span class="sxs-lookup"><span data-stu-id="c2bce-144">The order status queue is created in the `Main` method.</span></span> <span data-ttu-id="c2bce-145">用戶端組態會包含訂單狀態服務組態來裝載訂單狀態服務，如下列範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="c2bce-145">The client configuration includes the order status service configuration to host the order status service, as shown in the following sample configuration.</span></span>  
  
```xml  
<appSettings>  
  <!-- Use appSetting to configure MSMQ queue name. -->  
  <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderStatus" />  
</appSettings>  
  
<system.serviceModel>  
  
  <services>  
    <service
       name="Microsoft.ServiceModel.Samples.OrderStatusService">  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderStatus"  
                binding="netMsmqBinding"  
                contract="Microsoft.ServiceModel.Samples.IOrderStatus" />  
    </service>  
  </services>  
  
  <client>  
    <!-- Define NetMsmqEndpoint -->  
    <endpoint name="OrderProcessorEndpoint"  
              address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"
              binding="netMsmqBinding"
              contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
  </client>  
  
</system.serviceModel>  
```  
  
 <span data-ttu-id="c2bce-146">當您執行範例時，用戶端與服務活動都會顯示在服務與用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="c2bce-146">When you run the sample, the client and service activities are displayed in both the service and client console windows.</span></span> <span data-ttu-id="c2bce-147">您可以查看來自用戶端的服務接收訊息。</span><span class="sxs-lookup"><span data-stu-id="c2bce-147">You can see the service receive messages from the client.</span></span> <span data-ttu-id="c2bce-148">在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。</span><span class="sxs-lookup"><span data-stu-id="c2bce-148">Press ENTER in each console window to shut down the service and client.</span></span>  
  
 <span data-ttu-id="c2bce-149">服務會顯示採購單資訊，並表示它正在將訂單狀態傳送回訂單狀態佇列。</span><span class="sxs-lookup"><span data-stu-id="c2bce-149">The service displays the purchase order information and indicates it is sending back the order status to the order status queue.</span></span>  
  
```console  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 124a1f69-3699-4b16-9bcc-43147a8756fc  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
Sending back order status information  
```  
  
 <span data-ttu-id="c2bce-150">用戶端會顯示服務所傳送的訂單狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="c2bce-150">The client displays the order status information sent by the service.</span></span>  
  
```console  
Press <ENTER> to terminate client.  
Status of order 124a1f69-3699-4b16-9bcc-43147a8756fc:Pending  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="c2bce-151">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="c2bce-151">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="c2bce-152">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c2bce-152">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="c2bce-153">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="c2bce-153">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="c2bce-154">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="c2bce-154">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c2bce-155">如果您使用 Svcutil.exe 重新產生這個範例的組態，請務必修改用戶端組態中的端點名稱，以配合用戶端節點。</span><span class="sxs-lookup"><span data-stu-id="c2bce-155">If you use Svcutil.exe to regenerate the configuration for this sample, be sure to modify the endpoint names in the client configuration to match the client code.</span></span>  
  
 <span data-ttu-id="c2bce-156">根據預設，傳輸安全性會透過 <xref:System.ServiceModel.NetMsmqBinding> 啟用。</span><span class="sxs-lookup"><span data-stu-id="c2bce-156">By default with the <xref:System.ServiceModel.NetMsmqBinding>, transport security is enabled.</span></span> <span data-ttu-id="c2bce-157">MSMQ 傳輸安全性有兩個相關的屬性， <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> 而且 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> `.` 根據預設，驗證模式會設定為 `Windows` ，而保護層級會設定為 `Sign` 。</span><span class="sxs-lookup"><span data-stu-id="c2bce-157">There are two relevant properties for MSMQ transport security, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> and <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>`.` By default, the authentication mode is set to `Windows` and the protection level is set to `Sign`.</span></span> <span data-ttu-id="c2bce-158">若要 MSMQ 提供驗證及簽署功能，MSMQ 必須是網域的一部分，而且必須安裝 MSMQ 的 Active Directory 整合選項。</span><span class="sxs-lookup"><span data-stu-id="c2bce-158">For MSMQ to provide the authentication and signing feature, it must be part of a domain and the active directory integration option for MSMQ must be installed.</span></span> <span data-ttu-id="c2bce-159">如果您在不符合這些條件的電腦上執行這個範例，就會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2bce-159">If you run this sample on a computer that does not satisfy these criteria you receive an error.</span></span>  
  
### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup-or-without-active-directory-integration"></a><span data-ttu-id="c2bce-160">若要在加入工作群組，或是沒有 Active Directory 整合的電腦上執行這個範例</span><span class="sxs-lookup"><span data-stu-id="c2bce-160">To run the sample on a computer joined to a workgroup or without active directory integration</span></span>  
  
1. <span data-ttu-id="c2bce-161">如果您的電腦不是網域的一部分，或是沒有安裝 Active Directory 整合，請將驗證模式和保護層級設定為 `None`，以關閉傳輸安全性，如下列範例組態所示：</span><span class="sxs-lookup"><span data-stu-id="c2bce-161">If your computer is not part of a domain or does not have active directory integration installed, turn off transport security by setting the authentication mode and protection level to `None` as shown in the following sample configuration:</span></span>  
  
    ```xml  
    <configuration>  
  
      <appSettings>  
        <!-- Use appSetting to configure MSMQ queue name. -->  
        <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderProcessor" />  
      </appSettings>  
  
      <system.serviceModel>  
        <services>  
          <service
              name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
            <!-- Define NetMsmqEndpoint -->  
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"  
                      binding="netMsmqBinding"  
                      bindingConfiguration="TransactedBinding"
                      contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
          </service>  
        </services>  
  
        <bindings>  
          <netMsmqBinding>  
            <binding name="TransactedBinding" >  
             <security mode="None" />  
            </binding>  
          </netMsmqBinding>  
        </bindings>  
  
      </system.serviceModel>  
  
    </configuration>  
    ```  
  
2. <span data-ttu-id="c2bce-162">關閉用戶端組態的安全性會產生下列訊息：</span><span class="sxs-lookup"><span data-stu-id="c2bce-162">Turning off security for a client configuration generates the following:</span></span>  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <appSettings>  
        <!-- Use appSetting to configure MSMQ queue name. -->  
        <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderStatus" />  
      </appSettings>  
  
      <system.serviceModel>  
  
        <services>  
          <service
             name="Microsoft.ServiceModel.Samples.OrderStatusService">  
            <!-- Define NetMsmqEndpoint -->  
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderStatus"  
                      binding="netMsmqBinding"  
                      bindingConfiguration="TransactedBinding" contract="Microsoft.ServiceModel.Samples.IOrderStatus" />  
          </service>  
        </services>  
  
        <client>  
          <!-- Define NetMsmqEndpoint -->  
          <endpoint name="OrderProcessorEndpoint"  
                    address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"
                    binding="netMsmqBinding"
                    bindingConfiguration="TransactedBinding"  
                    contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
        </client>  
  
        <bindings>  
          <netMsmqBinding>  
            <binding name="TransactedBinding" >  
             <security mode="None" />  
            </binding>  
          </netMsmqBinding>  
        </bindings>  
  
      </system.serviceModel>  
  
    </configuration>  
    ```  
  
3. <span data-ttu-id="c2bce-163">這個範例的服務會在 `OrderProcessorService` 中建立繫結。</span><span class="sxs-lookup"><span data-stu-id="c2bce-163">The service for this sample creates a binding in the `OrderProcessorService`.</span></span> <span data-ttu-id="c2bce-164">在繫結具現化後新增程式碼行，以便將安全性模式設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="c2bce-164">Add a line of code after the binding is instantiated to set the security mode to `None`.</span></span>  
  
    ```csharp
    NetMsmqBinding msmqCallbackBinding = new NetMsmqBinding();  
    msmqCallbackBinding.Security.Mode = NetMsmqSecurityMode.None;  
    ```  
  
4. <span data-ttu-id="c2bce-165">請務必先變更伺服器與用戶端上的組態，再執行範例。</span><span class="sxs-lookup"><span data-stu-id="c2bce-165">Ensure that you change the configuration on both the server and the client before you run the sample.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c2bce-166">將 `security mode` 設定為 `None`，相當於將 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>、<xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> 或 `Message` 安全性設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="c2bce-166">Setting `security mode` to `None` is equivalent to setting <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> or `Message` security to `None`.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c2bce-167">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c2bce-167">The samples may already be installed on your machine.</span></span> <span data-ttu-id="c2bce-168">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="c2bce-168">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c2bce-169">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="c2bce-169">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c2bce-170">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="c2bce-170">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Binding\Net\MSMQ\Two-Way`  

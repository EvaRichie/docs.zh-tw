---
title: 作法：與 WCF 端點交換佇列訊息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 938e7825-f63a-4c3d-b603-63772fabfdb3
ms.openlocfilehash: 3f69286a2b4d4ec55f18931f9156c20a38da9c34
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265423"
---
# <a name="how-to-exchange-queued-messages-with-wcf-endpoints"></a><span data-ttu-id="83ca7-102">作法：與 WCF 端點交換佇列訊息</span><span class="sxs-lookup"><span data-stu-id="83ca7-102">How to: Exchange Queued Messages with WCF Endpoints</span></span>

<span data-ttu-id="83ca7-103">佇列可確保用戶端和 Windows Communication Foundation (WCF) 服務之間可進行可靠的訊息處理，即使服務在通訊時無法使用也是一樣。</span><span class="sxs-lookup"><span data-stu-id="83ca7-103">Queues ensure that reliable messaging can occur between a client and a Windows Communication Foundation (WCF) service, even if the service is not available at the time of communication.</span></span> <span data-ttu-id="83ca7-104">下列程式示範如何在執行 WCF 服務時，使用標準佇列系結來確保用戶端與服務之間的持久通訊。</span><span class="sxs-lookup"><span data-stu-id="83ca7-104">The following procedures show how to ensure durable communication between a client and a service by using the standard queued binding when implementing the WCF service.</span></span>  
  
 <span data-ttu-id="83ca7-105">本節說明如何用於 <xref:System.ServiceModel.NetMsmqBinding> wcf 用戶端與 wcf 服務之間的佇列通訊。</span><span class="sxs-lookup"><span data-stu-id="83ca7-105">This section explains how to use <xref:System.ServiceModel.NetMsmqBinding> for queued communication between a WCF client and a WCF service.</span></span>  
  
### <a name="to-use-queuing-in-a-wcf-service"></a><span data-ttu-id="83ca7-106">若要在 WCF 服務中使用佇列</span><span class="sxs-lookup"><span data-stu-id="83ca7-106">To use queuing in a WCF service</span></span>  
  
1. <span data-ttu-id="83ca7-107">使用以 <xref:System.ServiceModel.ServiceContractAttribute>標記的介面定義服務合約。</span><span class="sxs-lookup"><span data-stu-id="83ca7-107">Define a service contract using an interface marked with the <xref:System.ServiceModel.ServiceContractAttribute>.</span></span> <span data-ttu-id="83ca7-108">在屬於服務合約部分的介面中標示作業為 <xref:System.ServiceModel.OperationContractAttribute> 並指定它們為單向，因為此方法不用傳回任何回應。</span><span class="sxs-lookup"><span data-stu-id="83ca7-108">Mark the operations in the interface that are part of the service contract with the <xref:System.ServiceModel.OperationContractAttribute> and specify them as one-way because no response to the method is returned.</span></span> <span data-ttu-id="83ca7-109">下列程式碼提供範例服務合約以及其作業定義。</span><span class="sxs-lookup"><span data-stu-id="83ca7-109">The following code provides an example service contract and its operation definition.</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#1)]
     [!code-vb[S_Msmq_Transacted#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#1)]  
  
2. <span data-ttu-id="83ca7-110">當服務合約通過使用者定義型別，您必須為這些型別定義資料合約。</span><span class="sxs-lookup"><span data-stu-id="83ca7-110">When the service contract passes user-defined types, you must define data contracts for those types.</span></span> <span data-ttu-id="83ca7-111">下列程式碼示範兩份資料合約：`PurchaseOrder` 和 `PurchaseOrderLineItem`。</span><span class="sxs-lookup"><span data-stu-id="83ca7-111">The following code shows two data contracts, `PurchaseOrder` and `PurchaseOrderLineItem`.</span></span> <span data-ttu-id="83ca7-112">這兩個型別定義了傳送至服務的資料 </span><span class="sxs-lookup"><span data-stu-id="83ca7-112">These two types define data that is sent to the service.</span></span> <span data-ttu-id="83ca7-113">(請注意，定義這類資料合約的類別也定義許多方法。</span><span class="sxs-lookup"><span data-stu-id="83ca7-113">(Note that the classes that define this data contract also define a number of methods.</span></span> <span data-ttu-id="83ca7-114">這些方法不被視為資料合約的部分。</span><span class="sxs-lookup"><span data-stu-id="83ca7-114">These methods are not considered part of the data contract.</span></span> <span data-ttu-id="83ca7-115">只有以 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性宣告的成員才屬於資料合約的部分)。</span><span class="sxs-lookup"><span data-stu-id="83ca7-115">Only those members that are declared with the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute are part of the data contract.)</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#2)]
     [!code-vb[S_Msmq_Transacted#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#2)]  
  
3. <span data-ttu-id="83ca7-116">實作在類別中之介面所定義的服務合約方法。</span><span class="sxs-lookup"><span data-stu-id="83ca7-116">Implement the methods of the service contract defined in the interface in a class.</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#3)]
     [!code-vb[S_Msmq_Transacted#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#3)]  
  
     <span data-ttu-id="83ca7-117">請注意，<xref:System.ServiceModel.OperationBehaviorAttribute> 放置在 `SubmitPurchaseOrder` 方法上。</span><span class="sxs-lookup"><span data-stu-id="83ca7-117">Notice the <xref:System.ServiceModel.OperationBehaviorAttribute> placed on the `SubmitPurchaseOrder` method.</span></span> <span data-ttu-id="83ca7-118">其用意是指定必須在異動內呼叫此作業，而且異動會隨著方法完成而自動完成。</span><span class="sxs-lookup"><span data-stu-id="83ca7-118">This specifies that this operation must be called within a transaction and that the transaction automatically completes when the method completes.</span></span>  
  
4. <span data-ttu-id="83ca7-119">使用 <xref:System.Messaging> 來建立交易式佇列。</span><span class="sxs-lookup"><span data-stu-id="83ca7-119">Create a transactional queue using <xref:System.Messaging>.</span></span> <span data-ttu-id="83ca7-120">您可以選擇使用 Microsoft Message Queuing (MSMQ) Microsoft Management Console (MMC) 建立佇列。</span><span class="sxs-lookup"><span data-stu-id="83ca7-120">You can choose to create the queue using Microsoft Message Queuing (MSMQ) Microsoft Management Console (MMC) instead.</span></span> <span data-ttu-id="83ca7-121">若是這樣，請確定您建立異動式佇列。</span><span class="sxs-lookup"><span data-stu-id="83ca7-121">If so, make sure you create a transactional queue.</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#4)]
     [!code-vb[S_Msmq_Transacted#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#4)]  
  
5. <span data-ttu-id="83ca7-122">在組態中定義 <xref:System.ServiceModel.Description.ServiceEndpoint>，以指定服務位址，並使用標準 <xref:System.ServiceModel.NetMsmqBinding> 繫結。</span><span class="sxs-lookup"><span data-stu-id="83ca7-122">Define a <xref:System.ServiceModel.Description.ServiceEndpoint> in configuration that specifies the service address and uses the standard <xref:System.ServiceModel.NetMsmqBinding> binding.</span></span> <span data-ttu-id="83ca7-123">如需使用 WCF 設定的詳細資訊，請參閱設定 [wcf 服務](../configuring-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83ca7-123">For more information about using WCF configuration, see [Configuring WCF services](../configuring-services.md).</span></span>  

6. <span data-ttu-id="83ca7-124">使用從佇列讀取訊息並加以處理的 `OrderProcessing` 建立 <xref:System.ServiceModel.ServiceHost> 服務的主機。</span><span class="sxs-lookup"><span data-stu-id="83ca7-124">Create a host for the `OrderProcessing` service using <xref:System.ServiceModel.ServiceHost> that reads messages from the queue and processes them.</span></span> <span data-ttu-id="83ca7-125">開啟服務主機來提供服務。</span><span class="sxs-lookup"><span data-stu-id="83ca7-125">Open the service host to make the service available.</span></span> <span data-ttu-id="83ca7-126">顯示一則訊息，指示使用者按任意鍵終止服務。</span><span class="sxs-lookup"><span data-stu-id="83ca7-126">Display a message that tells the user to press any key to terminate the service.</span></span> <span data-ttu-id="83ca7-127">呼叫 `ReadLine` 以等待按鍵動作，隨後關閉服務。</span><span class="sxs-lookup"><span data-stu-id="83ca7-127">Call `ReadLine` to wait for the key to be pressed and then close the service.</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#6)]
     [!code-vb[S_Msmq_Transacted#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#6)]  
  
### <a name="to-create-a-client-for-the-queued-service"></a><span data-ttu-id="83ca7-128">若要建立佇列服務的用戶端</span><span class="sxs-lookup"><span data-stu-id="83ca7-128">To create a client for the queued service</span></span>  
  
1. <span data-ttu-id="83ca7-129">下列範例示範如何執行裝載應用程式，並使用 Svcutil.exe 工具來建立 WCF 用戶端。</span><span class="sxs-lookup"><span data-stu-id="83ca7-129">The following example shows how to run the hosting application and use the Svcutil.exe tool to create the WCF client.</span></span>  
  
    ```console
    svcutil http://localhost:8000/ServiceModelSamples/service  
    ```  
  
2. <span data-ttu-id="83ca7-130">在組態中定義 <xref:System.ServiceModel.Description.ServiceEndpoint>，藉以指定位址並使用標準 <xref:System.ServiceModel.NetMsmqBinding> 繫結，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="83ca7-130">Define a <xref:System.ServiceModel.Description.ServiceEndpoint> in configuration that specifies the address and uses the standard <xref:System.ServiceModel.NetMsmqBinding> binding, as shown in the following example.</span></span>  

3. <span data-ttu-id="83ca7-131">建立要寫入至交易式佇列的交易範圍、呼叫作業 `SubmitPurchaseOrder` 並關閉 WCF 用戶端，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="83ca7-131">Create a transaction scope to write to the transactional queue, call the `SubmitPurchaseOrder` operation and close the WCF client, as shown in the following example.</span></span>  
  
     [!code-csharp[S_Msmq_Transacted#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#8)]
     [!code-vb[S_Msmq_Transacted#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="83ca7-132">範例</span><span class="sxs-lookup"><span data-stu-id="83ca7-132">Example</span></span>  

 <span data-ttu-id="83ca7-133">以下內容顯示本範例所囊括的服務程式碼、裝載應用程式、App.config 檔案和用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="83ca7-133">The following examples show the service code, hosting application, App.config file, and client code included for this example.</span></span>  
  
 [!code-csharp[S_Msmq_Transacted#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#9)]
 [!code-vb[S_Msmq_Transacted#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#9)]  
  
 [!code-csharp[S_Msmq_Transacted#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#10)]
 [!code-vb[S_Msmq_Transacted#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#10)]  

 [!code-csharp[S_Msmq_Transacted#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#12)]
 [!code-vb[S_Msmq_Transacted#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#12)]  

## <a name="see-also"></a><span data-ttu-id="83ca7-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="83ca7-134">See also</span></span>

- <xref:System.ServiceModel.NetMsmqBinding>
- [<span data-ttu-id="83ca7-135">交易 MSMQ 繫結</span><span class="sxs-lookup"><span data-stu-id="83ca7-135">Transacted MSMQ Binding</span></span>](../samples/transacted-msmq-binding.md)
- [<span data-ttu-id="83ca7-136">WCF 中的佇列</span><span class="sxs-lookup"><span data-stu-id="83ca7-136">Queuing in WCF</span></span>](queuing-in-wcf.md)
- [<span data-ttu-id="83ca7-137">作法：與 WCF 端點和訊息佇列應用程式交換訊息</span><span class="sxs-lookup"><span data-stu-id="83ca7-137">How to: Exchange Messages with WCF Endpoints and Message Queuing Applications</span></span>](how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [<span data-ttu-id="83ca7-138">Windows Communication Foundation 至訊息佇列</span><span class="sxs-lookup"><span data-stu-id="83ca7-138">Windows Communication Foundation to Message Queuing</span></span>](../samples/wcf-to-message-queuing.md)
- [<span data-ttu-id="83ca7-139">安裝訊息佇列 (MSMQ)</span><span class="sxs-lookup"><span data-stu-id="83ca7-139">Installing Message Queuing (MSMQ)</span></span>](../samples/installing-message-queuing-msmq.md)
- [<span data-ttu-id="83ca7-140">訊息佇列至 Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="83ca7-140">Message Queuing to Windows Communication Foundation</span></span>](../samples/message-queuing-to-wcf.md)
- [<span data-ttu-id="83ca7-141">訊息佇列上的訊息安全性</span><span class="sxs-lookup"><span data-stu-id="83ca7-141">Message Security over Message Queuing</span></span>](../samples/message-security-over-message-queuing.md)

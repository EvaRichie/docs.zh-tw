---
title: 自訂訊息篩選條件
ms.date: 03/30/2017
ms.assetid: 98dd0af8-fce6-4255-ac32-42eb547eea67
ms.openlocfilehash: 24dab723a06c128337c1d956a98a1aa85a258e33
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96240923"
---
# <a name="custom-message-filter"></a><span data-ttu-id="d4424-102">自訂訊息篩選條件</span><span class="sxs-lookup"><span data-stu-id="d4424-102">Custom Message Filter</span></span>

<span data-ttu-id="d4424-103">這個範例示範如何取代 Windows Communication Foundation (WCF) 用來將訊息分派至端點的訊息篩選器。</span><span class="sxs-lookup"><span data-stu-id="d4424-103">This sample demonstrates how to replace the message filters that Windows Communication Foundation (WCF) uses to dispatch messages to endpoints.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d4424-104">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="d4424-104">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="d4424-105">當通道上的第一個訊息抵達伺服器時，伺服器必須判定哪一個與該 URI 關聯的端點 (如果有的話) 應該要接收訊息。</span><span class="sxs-lookup"><span data-stu-id="d4424-105">When the first message on a channel arrives at the server, the server must determine which (if any) of the endpoints associated with that URI should receive the message.</span></span> <span data-ttu-id="d4424-106">這個程序會由附加至 <xref:System.ServiceModel.Dispatcher.MessageFilter> 的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 物件控制。</span><span class="sxs-lookup"><span data-stu-id="d4424-106">This process is controlled by the <xref:System.ServiceModel.Dispatcher.MessageFilter> objects attached to the <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.</span></span>  
  
 <span data-ttu-id="d4424-107">服務的每個端點都有單一 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>。</span><span class="sxs-lookup"><span data-stu-id="d4424-107">Each endpoint of a service has a single <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.</span></span> <span data-ttu-id="d4424-108"><xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 同時擁有 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 和 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>。</span><span class="sxs-lookup"><span data-stu-id="d4424-108">The <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> has both an <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> and a <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>.</span></span> <span data-ttu-id="d4424-109">這兩個篩選條件的聯集便是該端點使用的訊息篩選條件。</span><span class="sxs-lookup"><span data-stu-id="d4424-109">The union of these two filters is the message filter used for that endpoint.</span></span>  
  
 <span data-ttu-id="d4424-110">根據預設，端點的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 會比對定址位址為符合服務端點之 <xref:System.ServiceModel.EndpointAddress> 的任何訊息。</span><span class="sxs-lookup"><span data-stu-id="d4424-110">By default, the <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> for an endpoint matches any message that is addressed to an address that matches the service endpoint's <xref:System.ServiceModel.EndpointAddress>.</span></span> <span data-ttu-id="d4424-111">根據預設，端點的會 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> 檢查內送訊息的動作，並將任何訊息與服務端點合約作業的其中一個動作對應的動作相符 (只 `IsInitiating` = `true` 會將動作視為) 。</span><span class="sxs-lookup"><span data-stu-id="d4424-111">By default, the <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> for an endpoint inspects the action of the incoming message and matches any message with an action that corresponds to one of the actions of the service endpoint contract's operations (only `IsInitiating`=`true` actions are considered).</span></span> <span data-ttu-id="d4424-112">因此，根據預設，只有在訊息的 To 標頭為端點的 <xref:System.ServiceModel.EndpointAddress>，而且訊息的動作符合其中一個端點作業動作時，端點的篩選條件才會相符。</span><span class="sxs-lookup"><span data-stu-id="d4424-112">As a result, by default, the filter for an endpoint only matches if both the message's To header is the <xref:System.ServiceModel.EndpointAddress> of the endpoint and the message's action matches one of the endpoint operation's actions.</span></span>  
  
 <span data-ttu-id="d4424-113">這些篩選條件可以使用行為加以變更。</span><span class="sxs-lookup"><span data-stu-id="d4424-113">These filters can be changed using a behavior.</span></span> <span data-ttu-id="d4424-114">在此範例中，服務會建立可取代 <xref:System.ServiceModel.Description.IEndpointBehavior> 上之 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 和 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> 的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>：</span><span class="sxs-lookup"><span data-stu-id="d4424-114">In the sample, the service creates an <xref:System.ServiceModel.Description.IEndpointBehavior> that replaces the <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> and <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> on the <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>:</span></span>  
  
```csharp
class FilteringEndpointBehavior : IEndpointBehavior
{
    //...
}
```  
  
 <span data-ttu-id="d4424-115">定義兩組位址篩選條件：</span><span class="sxs-lookup"><span data-stu-id="d4424-115">Two address filters are defined:</span></span>  
  
```csharp
// Matches any message whose To address contains the letter 'e'  
class MatchEAddressFilter : MessageFilter { }
// Matches any message whose To address does not contain the letter 'e'  
class MatchNoEAddressFilter : MessageFilter { }  
```  
  
 <span data-ttu-id="d4424-116">`FilteringEndpointBehavior` 已設定可設定狀態，並且允許兩種不同的變化。</span><span class="sxs-lookup"><span data-stu-id="d4424-116">The `FilteringEndpointBehavior` is made configurable and allows for two different variations.</span></span>  
  
```csharp
public class FilteringEndpointBehaviorExtension : BehaviorExtensionElement { }
```  
  
 <span data-ttu-id="d4424-117">變化 1 只會比對包含 'e' 的位址 (但可以是任何動作)，而變化 2 只比對缺少 'e' 的位址：</span><span class="sxs-lookup"><span data-stu-id="d4424-117">Variation 1 matches only addresses that contain an 'e' (but that have any Action) whereas Variation 2 matches only addresses that lack an 'e':</span></span>  
  
```csharp
if (Variation == 1)  
    return new FilteringEndpointBehavior(  
        new MatchEAddressFilter(), new MatchAllMessageFilter());  
else  
    return new FilteringEndpointBehavior(  
        new MatchNoEAddressFilter(), new MatchAllMessageFilter());  
```  
  
 <span data-ttu-id="d4424-118">在此組態檔中，服務會註冊新的行為：</span><span class="sxs-lookup"><span data-stu-id="d4424-118">In the configuration file, the service registers the new behavior:</span></span>  
  
```xml  
<extensions>  
    <behaviorExtensions>  
        <add name="filteringEndpointBehavior" type="Microsoft.ServiceModel.Samples.FilteringEndpointBehaviorExtension, service" />  
    </behaviorExtensions>  
</extensions>
```  
  
 <span data-ttu-id="d4424-119">接著，服務會建立每個變化的 `endpointBehavior` 組態：</span><span class="sxs-lookup"><span data-stu-id="d4424-119">Then the service creates `endpointBehavior` configurations for each variation:</span></span>  
  
```xml  
<endpointBehaviors>  
    <behavior name="endpoint1">  
        <filteringEndpointBehavior variation="1" />  
    </behavior>  
    <behavior name="endpoint2">  
        <filteringEndpointBehavior variation="2" />  
    </behavior>  
</endpointBehaviors>  
```  
  
 <span data-ttu-id="d4424-120">最後，服務的端點會參考其中一個 `behaviorConfigurations`：</span><span class="sxs-lookup"><span data-stu-id="d4424-120">Finally, the service's endpoint references one of the `behaviorConfigurations`:</span></span>  
  
```xml  
<endpoint address=""  
        bindingConfiguration="ws"  
        listenUri=""
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IHello"
        behaviorConfiguration="endpoint2" />  
```  
  
 <span data-ttu-id="d4424-121">用戶端應用程式的實作是很直接的工作；它會建立服務 URI 的兩個通道 (藉由將該值當作第二個 (`via`) 參數傳遞至 <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29>)，然後在每個通道傳送單一訊息，但是每個通道使用不同的端點位址。</span><span class="sxs-lookup"><span data-stu-id="d4424-121">The implementation of the client application is straightforward; it creates two channels to the service's URI (by passing in that value as the second (`via`) parameter to <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29> and sends a single message on each channel, but it uses different endpoint addresses for each.</span></span> <span data-ttu-id="d4424-122">因此，來自用戶端的傳出訊息會具有不同的 To 目的地，而伺服器會個別回應，如用戶端輸出所示：</span><span class="sxs-lookup"><span data-stu-id="d4424-122">As a result, the outbound messages from the client have different To designations, and the server responds accordingly, as demonstrated by the client's output:</span></span>  
  
```console  
Sending message to urn:e...  
Exception: The message with To 'urn:e' cannot be processed at the receiver, due to an AddressFilter mismatch at the EndpointDispatcher.  Check that the sender and receiver's EndpointAddresses agree.  
  
Sending message to urn:a...  
Hello  
```  
  
 <span data-ttu-id="d4424-123">切換伺服器組態檔中的變化會導致篩選條件加以切換，並使得用戶端觀察到相反的行為 (即傳送至 `urn:e` 的訊息成功，而傳送至 `urn:a` 的訊息失敗)。</span><span class="sxs-lookup"><span data-stu-id="d4424-123">Switching the variation in the server's configuration file causes the filter to be swapped and the client sees the opposite behavior (the message to `urn:e` succeeds, whereas the message to `urn:a` fails).</span></span>  
  
```xml  
<endpoint address=""  
          bindingConfiguration="ws"  
          listenUri=""
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.IHello"
          behaviorConfiguration="endpoint1" />  
```  
  
> [!IMPORTANT]
> <span data-ttu-id="d4424-124">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d4424-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="d4424-125">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="d4424-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="d4424-126">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="d4424-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d4424-127">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="d4424-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageFilter`  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="d4424-128">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="d4424-128">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="d4424-129">若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="d4424-129">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
2. <span data-ttu-id="d4424-130">若要在單一電腦設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d4424-130">To run the sample in a single-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
3. <span data-ttu-id="d4424-131">若要在跨電腦設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md) 中的指示，並在 Client.cs 中變更下行。</span><span class="sxs-lookup"><span data-stu-id="d4424-131">To run the sample in a cross-machine configuration, follow the instructions at [Running the Windows Communication Foundation Samples](running-the-samples.md) and change the following line in Client.cs.</span></span>  
  
    ```csharp
    Uri serviceVia = new Uri("http://localhost/ServiceModelSamples/service.svc");  
    ```  
  
     <span data-ttu-id="d4424-132">以伺服器名稱取代 localhost。</span><span class="sxs-lookup"><span data-stu-id="d4424-132">Replace localhost with the name of server.</span></span>  
  
    ```csharp
    Uri serviceVia = new Uri("http://servermachinename/ServiceModelSamples/service.svc");  
    ```  

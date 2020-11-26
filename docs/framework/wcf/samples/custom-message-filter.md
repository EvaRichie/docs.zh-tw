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
# <a name="custom-message-filter"></a>自訂訊息篩選條件

這個範例示範如何取代 Windows Communication Foundation (WCF) 用來將訊息分派至端點的訊息篩選器。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 當通道上的第一個訊息抵達伺服器時，伺服器必須判定哪一個與該 URI 關聯的端點 (如果有的話) 應該要接收訊息。 這個程序會由附加至 <xref:System.ServiceModel.Dispatcher.MessageFilter> 的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 物件控制。  
  
 服務的每個端點都有單一 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>。 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 同時擁有 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 和 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>。 這兩個篩選條件的聯集便是該端點使用的訊息篩選條件。  
  
 根據預設，端點的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 會比對定址位址為符合服務端點之 <xref:System.ServiceModel.EndpointAddress> 的任何訊息。 根據預設，端點的會 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> 檢查內送訊息的動作，並將任何訊息與服務端點合約作業的其中一個動作對應的動作相符 (只 `IsInitiating` = `true` 會將動作視為) 。 因此，根據預設，只有在訊息的 To 標頭為端點的 <xref:System.ServiceModel.EndpointAddress>，而且訊息的動作符合其中一個端點作業動作時，端點的篩選條件才會相符。  
  
 這些篩選條件可以使用行為加以變更。 在此範例中，服務會建立可取代 <xref:System.ServiceModel.Description.IEndpointBehavior> 上之 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> 和 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> 的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>：  
  
```csharp
class FilteringEndpointBehavior : IEndpointBehavior
{
    //...
}
```  
  
 定義兩組位址篩選條件：  
  
```csharp
// Matches any message whose To address contains the letter 'e'  
class MatchEAddressFilter : MessageFilter { }
// Matches any message whose To address does not contain the letter 'e'  
class MatchNoEAddressFilter : MessageFilter { }  
```  
  
 `FilteringEndpointBehavior` 已設定可設定狀態，並且允許兩種不同的變化。  
  
```csharp
public class FilteringEndpointBehaviorExtension : BehaviorExtensionElement { }
```  
  
 變化 1 只會比對包含 'e' 的位址 (但可以是任何動作)，而變化 2 只比對缺少 'e' 的位址：  
  
```csharp
if (Variation == 1)  
    return new FilteringEndpointBehavior(  
        new MatchEAddressFilter(), new MatchAllMessageFilter());  
else  
    return new FilteringEndpointBehavior(  
        new MatchNoEAddressFilter(), new MatchAllMessageFilter());  
```  
  
 在此組態檔中，服務會註冊新的行為：  
  
```xml  
<extensions>  
    <behaviorExtensions>  
        <add name="filteringEndpointBehavior" type="Microsoft.ServiceModel.Samples.FilteringEndpointBehaviorExtension, service" />  
    </behaviorExtensions>  
</extensions>
```  
  
 接著，服務會建立每個變化的 `endpointBehavior` 組態：  
  
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
  
 最後，服務的端點會參考其中一個 `behaviorConfigurations`：  
  
```xml  
<endpoint address=""  
        bindingConfiguration="ws"  
        listenUri=""
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IHello"
        behaviorConfiguration="endpoint2" />  
```  
  
 用戶端應用程式的實作是很直接的工作；它會建立服務 URI 的兩個通道 (藉由將該值當作第二個 (`via`) 參數傳遞至 <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29>)，然後在每個通道傳送單一訊息，但是每個通道使用不同的端點位址。 因此，來自用戶端的傳出訊息會具有不同的 To 目的地，而伺服器會個別回應，如用戶端輸出所示：  
  
```console  
Sending message to urn:e...  
Exception: The message with To 'urn:e' cannot be processed at the receiver, due to an AddressFilter mismatch at the EndpointDispatcher.  Check that the sender and receiver's EndpointAddresses agree.  
  
Sending message to urn:a...  
Hello  
```  
  
 切換伺服器組態檔中的變化會導致篩選條件加以切換，並使得用戶端觀察到相反的行為 (即傳送至 `urn:e` 的訊息成功，而傳送至 `urn:a` 的訊息失敗)。  
  
```xml  
<endpoint address=""  
          bindingConfiguration="ws"  
          listenUri=""
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.IHello"
          behaviorConfiguration="endpoint1" />  
```  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageFilter`  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。  
  
2. 若要在單一電腦設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
3. 若要在跨電腦設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md) 中的指示，並在 Client.cs 中變更下行。  
  
    ```csharp
    Uri serviceVia = new Uri("http://localhost/ServiceModelSamples/service.svc");  
    ```  
  
     以伺服器名稱取代 localhost。  
  
    ```csharp
    Uri serviceVia = new Uri("http://servermachinename/ServiceModelSamples/service.svc");  
    ```  

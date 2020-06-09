---
title: 使用 NetHttpBinding
ms.date: 03/30/2017
ms.assetid: fe134acf-ceca-49de-84a9-05a37e3841f1
ms.openlocfilehash: ac6fc658731d032051f2dfd4058397f9b9a55828
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585632"
---
# <a name="using-the-nethttpbinding"></a>使用 NetHttpBinding
<xref:System.ServiceModel.NetHttpBinding> 是為了使用 HTTP 或 WebSocket 服務而設計的繫結，其預設會使用二進位編碼。 <xref:System.ServiceModel.NetHttpBinding> 將會偵測其所搭配使用的是要求-回覆合約還是雙工合約，並改變行為來配合，也就是針對要求-回覆合約使用 HTTP，並針對雙工合約使用 WebSockets。 使用 <xref:System.ServiceModel.Channels.WebSocketTransportUsage> 設定即可覆寫這個行為：  
  
1. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.Always>-這會強制使用 Websocket，即使是要求-回復合約也一樣。  
  
2. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.Never>-這可防止使用 Websocket。 嘗試將這個設定用於雙工合約會導致例外狀況。  
  
3. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.WhenDuplex>-這是預設值，並如上面所述運作。  
  
 <xref:System.ServiceModel.NetHttpBinding> 在 HTTP 模式和 WebSocket 模式下都會支援可靠工作階段。 在 WebSocket 模式中，工作階段是由傳輸提供。  
  
> [!WARNING]
> 當使用 <xref:System.ServiceModel.NetHttpBinding> 且繫結的 TransferMode 設為 TransferMode.Streamed 時，大量資料流可能會造成死結與呼叫逾時。 為了解決此問題，請傳送較小的訊息或使用 TransferMode.Buffered。  
  
## <a name="configuring-a-service-to-use-nethttpbinding"></a>設定服務以使用 NetHttpBinding  
 可以將 <xref:System.ServiceModel.NetHttpBinding> 設定成和任何其他繫結程序一樣。 下列組態檔片段說明如何使用 <xref:System.ServiceModel.NetHttpBinding> 來設定 WCF 服務。  
  
```xml  
<system.serviceModel>  
    <services>  
      <service name="WcfService1.Service1">  
        <endpoint address=""  
                  binding="netHttpBinding"  
                  contract="WcfService1.IService1"/>  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
    <bindings>  
      <netHttpBinding>  
        <binding name="My_NetHttpBindingConfig">  
          <webSocketSettings transportUsage="WhenDuplex"/>  
        </binding>  
      </netHttpBinding>  
    </bindings>  
    ...
  </system.serviceModel>  
```  
  
 下列程式碼片段示範如何在程式碼中加入 <xref:System.ServiceModel.NetHttpBinding>。  
  
```csharp  
ServiceHost svchost = new ServiceHost(typeof(Service1), baseAddress);  
            NetHttpBinding binding = new NetHttpBinding();  
            svchost.AddServiceEndpoint(typeof(IService1), binding, address);
        }  
```  
  
## <a name="see-also"></a>請參閱

- [設定服務的繫結](../configuring-bindings-for-wcf-services.md)
- [繫結](bindings.md)
- [系統提供的繫結](../system-provided-bindings.md)
- [雙工服務](duplex-services.md)

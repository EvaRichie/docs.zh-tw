---
title: 負載平衡
ms.date: 03/30/2017
helpviewer_keywords:
- load balancing [WCF]
ms.assetid: 148e0168-c08d-4886-8769-776d0953b80f
ms.openlocfilehash: ccafce51cadba588dc6c4e8fc8b476f3cd8ee699
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262706"
---
# <a name="load-balancing"></a>負載平衡

提高 WCF) 應用程式 (Windows Communication Foundation 容量的其中一種方式，是將它們部署到負載平衡的伺服器陣列中，以將它們擴充。 WCF 應用程式可使用標準的負載平衡技術來達到負載平衡，包括像是 Windows 網路負載平衡的軟體負載平衡器，以及硬體負載平衡設備。  
  
 下列各節將討論使用各種系統提供的系結來建立 WCF 應用程式負載平衡的考慮。  
  
## <a name="load-balancing-with-the-basic-http-binding"></a>使用基本 HTTP 繫結的負載平衡  

 從負載平衡的觀點來看，使用進行通訊的 WCF 應用程式與 <xref:System.ServiceModel.BasicHttpBinding> 其他常見的 HTTP 網路流量類型（ (靜態 HTML 內容、ASP.NET 網頁或 .Asmx Web 服務) ）並無不同。 使用這個系結的 WCF 通道本質上是無狀態的，而且會在通道關閉時終止其連接。 因此，<xref:System.ServiceModel.BasicHttpBinding> 可搭配現有的 HTTP 負載平衡技術正常運作。  
  
 根據預設，<xref:System.ServiceModel.BasicHttpBinding> 會在訊息中傳送包含 `Keep-Alive` 值的連線 HTTP 標頭，該值可以讓使用者建立服務 (指支援使用者的服務) 的持續連線。 這項組態會改進處理能力，因為先前建立的連線可以重複使用，並將後續訊息傳送到相同的伺服器。 不過，重複使用連線可能會使用戶端與負載平衡陣列內的特定伺服器產生強烈的關聯性，這樣就會降低循環配置資源的有效性。 如果不希望發生這種行為，請針對 `Keep-Alive` 或使用者定義的 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> 使用 <xref:System.ServiceModel.Channels.CustomBinding> 屬性，停用伺服器上的 HTTP <xref:System.ServiceModel.Channels.Binding>。 下列範例會示範如何使用組態來做到這點。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
 <system.serviceModel>  
  <services>  
   <service
     name="Microsoft.ServiceModel.Samples.CalculatorService"  
     behaviorConfiguration="CalculatorServiceBehavior">  
     <host>  
      <baseAddresses>  
       <add baseAddress="http://localhost:8000/servicemodelsamples/service"/>  
      </baseAddresses>  
     </host>  
    <!-- configure http endpoint, use base address provided by host  
         And the customBinding -->  
     <endpoint address=""  
           binding="customBinding"  
           bindingConfiguration="HttpBinding"
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   </service>  
  </services>  
  
  <bindings>  
    <customBinding>  
  
    <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
      <binding name="HttpBinding" keepAliveEnabled="False"/>  
  
    </customBinding>  
  </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 使用 .NET Framework 4 引進的簡化設定，可使用下列簡化的設定來完成相同的行為。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
 <system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="customBinding" />  
    </protocolMapping>  
    <bindings>  
      <customBinding>  
  
      <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
        <binding keepAliveEnabled="False"/>  
  
      </customBinding>  
    </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](simplified-configuration.md)和 [WCF 服務的簡化組態](./samples/simplified-configuration-for-wcf-services.md)。  
  
## <a name="load-balancing-with-the-wshttp-binding-and-the-wsdualhttp-binding"></a>使用 WSHttp 繫結和 WSDualHttp 繫結的負載平衡  

 只要對預設的繫結組態進行一些修改，即可透過 HTTP 負載平衡技術來使 <xref:System.ServiceModel.WSHttpBinding> 與 <xref:System.ServiceModel.WSDualHttpBinding> 兩者達成負載平衡。  
  
- 關閉安全性內容建立：將 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 上的 <xref:System.ServiceModel.WSHttpBinding> 屬性設定為 `false`，即可做到這點。 或者，如果需要安全性會話，則可以使用可設定狀態的安全性會話，如「 [安全會話](./feature-details/secure-sessions.md) 」主題所述。 具狀態的安全性工作階段讓服務能夠保持無狀態，因為安全性工作階段的所有狀態都會隨著每項要求傳輸為保護安全性權杖的一部分。 請注意，為了啟用可設定狀態的安全性工作階段，這時必須使用 <xref:System.ServiceModel.Channels.CustomBinding> 或是使用者定義的 <xref:System.ServiceModel.Channels.Binding>，因為系統提供的 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.WSDualHttpBinding> 上面並未公開 (Expose) 這些必要的組態設定。  
  
- 請勿使用可靠工作階段。 這項功能預設為關閉。  
  
## <a name="load-balancing-the-nettcp-binding"></a>負載平衡 Net.TCP 繫結  

 <xref:System.ServiceModel.NetTcpBinding> 可以使用 IP 層負載平衡技術來達成負載平衡。 不過，根據預設，<xref:System.ServiceModel.NetTcpBinding> 會建立 TCP 連線集區來縮短連線延遲時間。 這種最佳化方式會干擾到負載平衡的基本機制。 進行 <xref:System.ServiceModel.NetTcpBinding> 最佳化的主要組態值是租用逾時，這個值是「連線集區設定」的一部分。 連線集區會導致用戶端連線與陣列內的特定伺服器產生關聯。 隨著這些連線的存留期 (Lifetime) 延長 (由租用逾時設定所控制的因素)，在陣列內各個伺服器中的負載散佈會出現不平衡的情形。 結果一來，就會提高平均的呼叫時間。 所以，當您在負載平衡案例中使用 <xref:System.ServiceModel.NetTcpBinding> 時，請考慮降低繫結所使用的預設租用逾時。 對負載平衡案例來說，30 秒的租用逾時是合理的起始值，不過最佳值會視應用程式而定。 如需通道租用超時和其他傳輸配額的詳細資訊，請參閱 [傳輸配額](./feature-details/transport-quotas.md)。  
  
 為了在負載平衡案例中創造最佳效能，請考慮使用 <xref:System.ServiceModel.NetTcpSecurity> (<xref:System.ServiceModel.SecurityMode.Transport> 或 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>)。  
  
## <a name="see-also"></a>另請參閱

- [網際網路資訊服務裝載最佳做法](./feature-details/internet-information-services-hosting-best-practices.md)

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
# <a name="load-balancing"></a><span data-ttu-id="3e1c0-102">負載平衡</span><span class="sxs-lookup"><span data-stu-id="3e1c0-102">Load Balancing</span></span>

<span data-ttu-id="3e1c0-103">提高 WCF) 應用程式 (Windows Communication Foundation 容量的其中一種方式，是將它們部署到負載平衡的伺服器陣列中，以將它們擴充。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-103">One way to increase the capacity of Windows Communication Foundation (WCF) applications is to scale them out by deploying them into a load-balanced server farm.</span></span> <span data-ttu-id="3e1c0-104">WCF 應用程式可使用標準的負載平衡技術來達到負載平衡，包括像是 Windows 網路負載平衡的軟體負載平衡器，以及硬體負載平衡設備。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-104">WCF applications can be load balanced using standard load balancing techniques, including software load balancers such as Windows Network Load Balancing as well as hardware-based load balancing appliances.</span></span>  
  
 <span data-ttu-id="3e1c0-105">下列各節將討論使用各種系統提供的系結來建立 WCF 應用程式負載平衡的考慮。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-105">The following sections discuss considerations for load balancing WCF applications built using various system-provided bindings.</span></span>  
  
## <a name="load-balancing-with-the-basic-http-binding"></a><span data-ttu-id="3e1c0-106">使用基本 HTTP 繫結的負載平衡</span><span class="sxs-lookup"><span data-stu-id="3e1c0-106">Load Balancing with the Basic HTTP Binding</span></span>  

 <span data-ttu-id="3e1c0-107">從負載平衡的觀點來看，使用進行通訊的 WCF 應用程式與 <xref:System.ServiceModel.BasicHttpBinding> 其他常見的 HTTP 網路流量類型（ (靜態 HTML 內容、ASP.NET 網頁或 .Asmx Web 服務) ）並無不同。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-107">From the perspective of load balancing, WCF applications that communicate using the <xref:System.ServiceModel.BasicHttpBinding> are no different than other common types of HTTP network traffic (static HTML content, ASP.NET pages, or ASMX Web Services).</span></span> <span data-ttu-id="3e1c0-108">使用這個系結的 WCF 通道本質上是無狀態的，而且會在通道關閉時終止其連接。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-108">WCF channels that use this binding are inherently stateless, and terminate their connections when the channel closes.</span></span> <span data-ttu-id="3e1c0-109">因此，<xref:System.ServiceModel.BasicHttpBinding> 可搭配現有的 HTTP 負載平衡技術正常運作。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-109">As such, the <xref:System.ServiceModel.BasicHttpBinding> works well with existing HTTP load balancing techniques.</span></span>  
  
 <span data-ttu-id="3e1c0-110">根據預設，<xref:System.ServiceModel.BasicHttpBinding> 會在訊息中傳送包含 `Keep-Alive` 值的連線 HTTP 標頭，該值可以讓使用者建立服務 (指支援使用者的服務) 的持續連線。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-110">By default, the <xref:System.ServiceModel.BasicHttpBinding> sends a connection HTTP header in messages with a `Keep-Alive` value, which enables clients to establish persistent connections to the services that support them.</span></span> <span data-ttu-id="3e1c0-111">這項組態會改進處理能力，因為先前建立的連線可以重複使用，並將後續訊息傳送到相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-111">This configuration offers enhanced throughput because previously established connections can be reused to send subsequent messages to the same server.</span></span> <span data-ttu-id="3e1c0-112">不過，重複使用連線可能會使用戶端與負載平衡陣列內的特定伺服器產生強烈的關聯性，這樣就會降低循環配置資源的有效性。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-112">However, connection reuse may cause clients to become strongly associated to a specific server within the load-balanced farm, which reduces the effectiveness of round-robin load balancing.</span></span> <span data-ttu-id="3e1c0-113">如果不希望發生這種行為，請針對 `Keep-Alive` 或使用者定義的 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> 使用 <xref:System.ServiceModel.Channels.CustomBinding> 屬性，停用伺服器上的 HTTP <xref:System.ServiceModel.Channels.Binding>。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-113">If this behavior is undesirable, HTTP `Keep-Alive` can be disabled on the server using the <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> property with a <xref:System.ServiceModel.Channels.CustomBinding> or user-defined <xref:System.ServiceModel.Channels.Binding>.</span></span> <span data-ttu-id="3e1c0-114">下列範例會示範如何使用組態來做到這點。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-114">The following example shows how to do this using configuration.</span></span>  
  
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
  
 <span data-ttu-id="3e1c0-115">使用 .NET Framework 4 引進的簡化設定，可使用下列簡化的設定來完成相同的行為。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-115">Using the simplified configuration introduced in .NET Framework 4, the same behavior can be accomplished using the following simplified configuration.</span></span>  
  
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
  
 <span data-ttu-id="3e1c0-116">如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](simplified-configuration.md)和 [WCF 服務的簡化組態](./samples/simplified-configuration-for-wcf-services.md)。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-116">For more information about default endpoints, bindings, and behaviors, see [Simplified Configuration](simplified-configuration.md) and [Simplified Configuration for WCF Services](./samples/simplified-configuration-for-wcf-services.md).</span></span>  
  
## <a name="load-balancing-with-the-wshttp-binding-and-the-wsdualhttp-binding"></a><span data-ttu-id="3e1c0-117">使用 WSHttp 繫結和 WSDualHttp 繫結的負載平衡</span><span class="sxs-lookup"><span data-stu-id="3e1c0-117">Load Balancing with the WSHttp Binding and the WSDualHttp Binding</span></span>  

 <span data-ttu-id="3e1c0-118">只要對預設的繫結組態進行一些修改，即可透過 HTTP 負載平衡技術來使 <xref:System.ServiceModel.WSHttpBinding> 與 <xref:System.ServiceModel.WSDualHttpBinding> 兩者達成負載平衡。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-118">Both the <xref:System.ServiceModel.WSHttpBinding> and the <xref:System.ServiceModel.WSDualHttpBinding> can be load balanced using HTTP load balancing techniques provided several modifications are made to the default binding configuration.</span></span>  
  
- <span data-ttu-id="3e1c0-119">關閉安全性內容建立：將 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 上的 <xref:System.ServiceModel.WSHttpBinding> 屬性設定為 `false`，即可做到這點。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-119">Turn off Security Context Establishment: this can be accomplished by the setting the <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> property on the <xref:System.ServiceModel.WSHttpBinding> to `false`.</span></span> <span data-ttu-id="3e1c0-120">或者，如果需要安全性會話，則可以使用可設定狀態的安全性會話，如「 [安全會話](./feature-details/secure-sessions.md) 」主題所述。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-120">Alternatively, if security sessions are required, it is possible to use stateful security sessions as described in the [Secure Sessions](./feature-details/secure-sessions.md) topic.</span></span> <span data-ttu-id="3e1c0-121">具狀態的安全性工作階段讓服務能夠保持無狀態，因為安全性工作階段的所有狀態都會隨著每項要求傳輸為保護安全性權杖的一部分。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-121">Stateful security sessions enable the service to remain stateless as all of the state for the security session is transmitted with each request as a part of the protection security token.</span></span> <span data-ttu-id="3e1c0-122">請注意，為了啟用可設定狀態的安全性工作階段，這時必須使用 <xref:System.ServiceModel.Channels.CustomBinding> 或是使用者定義的 <xref:System.ServiceModel.Channels.Binding>，因為系統提供的 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.WSDualHttpBinding> 上面並未公開 (Expose) 這些必要的組態設定。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-122">Note that to enable a stateful security session, it is necessary to use a <xref:System.ServiceModel.Channels.CustomBinding> or user-defined <xref:System.ServiceModel.Channels.Binding> as the necessary configuration settings are not exposed on <xref:System.ServiceModel.WSHttpBinding> and <xref:System.ServiceModel.WSDualHttpBinding> that are provided by the system.</span></span>  
  
- <span data-ttu-id="3e1c0-123">請勿使用可靠工作階段。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-123">Do not use reliable sessions.</span></span> <span data-ttu-id="3e1c0-124">這項功能預設為關閉。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-124">This feature is off by default.</span></span>  
  
## <a name="load-balancing-the-nettcp-binding"></a><span data-ttu-id="3e1c0-125">負載平衡 Net.TCP 繫結</span><span class="sxs-lookup"><span data-stu-id="3e1c0-125">Load Balancing the Net.TCP Binding</span></span>  

 <span data-ttu-id="3e1c0-126"><xref:System.ServiceModel.NetTcpBinding> 可以使用 IP 層負載平衡技術來達成負載平衡。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-126">The <xref:System.ServiceModel.NetTcpBinding> can be load balanced using IP-layer load balancing techniques.</span></span> <span data-ttu-id="3e1c0-127">不過，根據預設，<xref:System.ServiceModel.NetTcpBinding> 會建立 TCP 連線集區來縮短連線延遲時間。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-127">However, the <xref:System.ServiceModel.NetTcpBinding> pools TCP connections by default to reduce connection latency.</span></span> <span data-ttu-id="3e1c0-128">這種最佳化方式會干擾到負載平衡的基本機制。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-128">This is an optimization that interferes with the basic mechanism of load balancing.</span></span> <span data-ttu-id="3e1c0-129">進行 <xref:System.ServiceModel.NetTcpBinding> 最佳化的主要組態值是租用逾時，這個值是「連線集區設定」的一部分。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-129">The primary configuration value for optimizing the <xref:System.ServiceModel.NetTcpBinding> is the lease timeout, which is part of the Connection Pool Settings.</span></span> <span data-ttu-id="3e1c0-130">連線集區會導致用戶端連線與陣列內的特定伺服器產生關聯。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-130">Connection pooling causes client connections to become associated to specific servers within the farm.</span></span> <span data-ttu-id="3e1c0-131">隨著這些連線的存留期 (Lifetime) 延長 (由租用逾時設定所控制的因素)，在陣列內各個伺服器中的負載散佈會出現不平衡的情形。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-131">As the lifetime of those connections increase (a factor controlled by the lease timeout setting), the load distribution across various servers in the farm becomes unbalanced.</span></span> <span data-ttu-id="3e1c0-132">結果一來，就會提高平均的呼叫時間。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-132">As a result the average call time increases.</span></span> <span data-ttu-id="3e1c0-133">所以，當您在負載平衡案例中使用 <xref:System.ServiceModel.NetTcpBinding> 時，請考慮降低繫結所使用的預設租用逾時。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-133">So when using the <xref:System.ServiceModel.NetTcpBinding> in load-balanced scenarios, consider reducing the default lease timeout used by the binding.</span></span> <span data-ttu-id="3e1c0-134">對負載平衡案例來說，30 秒的租用逾時是合理的起始值，不過最佳值會視應用程式而定。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-134">A 30-second lease timeout is a reasonable starting point for load-balanced scenarios, although the optimal value is application-dependent.</span></span> <span data-ttu-id="3e1c0-135">如需通道租用超時和其他傳輸配額的詳細資訊，請參閱 [傳輸配額](./feature-details/transport-quotas.md)。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-135">For more information about the channel lease timeout and other transport quotas, see [Transport Quotas](./feature-details/transport-quotas.md).</span></span>  
  
 <span data-ttu-id="3e1c0-136">為了在負載平衡案例中創造最佳效能，請考慮使用 <xref:System.ServiceModel.NetTcpSecurity> (<xref:System.ServiceModel.SecurityMode.Transport> 或 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>)。</span><span class="sxs-lookup"><span data-stu-id="3e1c0-136">For best performance in load-balanced scenarios, consider using <xref:System.ServiceModel.NetTcpSecurity> (either <xref:System.ServiceModel.SecurityMode.Transport> or <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3e1c0-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3e1c0-137">See also</span></span>

- [<span data-ttu-id="3e1c0-138">網際網路資訊服務裝載最佳做法</span><span class="sxs-lookup"><span data-stu-id="3e1c0-138">Internet Information Services Hosting Best Practices</span></span>](./feature-details/internet-information-services-hosting-best-practices.md)

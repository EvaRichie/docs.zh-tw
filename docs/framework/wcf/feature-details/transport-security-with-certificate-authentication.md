---
title: 憑證驗證的傳輸安全性
description: 瞭解在使用傳輸安全性時，WFC 如何使用憑證進行伺服器和用戶端驗證。
ms.date: 03/30/2017
dev_langs:
- csharp
ms.assetid: 3d726b71-4d8b-4581-a3bb-02b9af51d11b
ms.openlocfilehash: 3da1202a5ad3b953470b50dd5924b2ab45f301eb
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244774"
---
# <a name="transport-security-with-certificate-authentication"></a><span data-ttu-id="eddcd-103">憑證驗證的傳輸安全性</span><span class="sxs-lookup"><span data-stu-id="eddcd-103">Transport Security with Certificate Authentication</span></span>

<span data-ttu-id="eddcd-104">本文討論如何在使用傳輸安全性時，針對伺服器和用戶端驗證使用 x.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="eddcd-104">This article discusses using X.509 certificates for server and client authentication when using transport security.</span></span> <span data-ttu-id="eddcd-105">如需 X.509 憑證的詳細資訊，請參閱 [X.509 公用金鑰憑證](/windows/desktop/SecCertEnroll/about-x-509-public-key-certificates)。</span><span class="sxs-lookup"><span data-stu-id="eddcd-105">For more information about X.509 certificates see [X.509 Public Key Certificates](/windows/desktop/SecCertEnroll/about-x-509-public-key-certificates).</span></span> <span data-ttu-id="eddcd-106">憑證必須由憑證授權單位單位發行，這通常是憑證的協力廠商簽發者。</span><span class="sxs-lookup"><span data-stu-id="eddcd-106">Certificates must be issued by a certification authority, which is often a third-party issuer of certificates.</span></span> <span data-ttu-id="eddcd-107">在 Windows Server 網域中，可以使用 Active Directory 憑證服務對網域中的用戶端電腦發行憑證。</span><span class="sxs-lookup"><span data-stu-id="eddcd-107">On a Windows Server domain, Active Directory Certificate Services can be used to issue certificates to client computers on the domain.</span></span> <span data-ttu-id="eddcd-108">在此案例中，服務是在使用安全通訊端層 (SSL) 設定的 Internet Information Services (IIS) 之下裝載。</span><span class="sxs-lookup"><span data-stu-id="eddcd-108">In this scenario, the service is hosted under Internet Information Services (IIS) which is configured with Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="eddcd-109">此服務使用 SSL (X.509) 憑證設定，以允許使用者驗證伺服器的身分識別。</span><span class="sxs-lookup"><span data-stu-id="eddcd-109">The service is configured with an SSL (X.509) certificate to allow clients to verify the identity of the server.</span></span> <span data-ttu-id="eddcd-110">用戶端也使用 X.509 憑證設定，以允許服務驗證用戶端的身分識別。</span><span class="sxs-lookup"><span data-stu-id="eddcd-110">The client is also configured with an X.509 certificate that allows the service to verify the identity of the client.</span></span> <span data-ttu-id="eddcd-111">伺服器的憑證必須受到用戶端的信任，而用戶端的憑證則必須受到伺服器的信任。</span><span class="sxs-lookup"><span data-stu-id="eddcd-111">The server’s certificate must be trusted by the client and the client’s certificate must be trusted by the server.</span></span> <span data-ttu-id="eddcd-112">服務和用戶端驗證彼此身分識別的實際機制，已超出本文的範圍。</span><span class="sxs-lookup"><span data-stu-id="eddcd-112">The actual mechanics of how the service and client verifies each other’s identity is beyond the scope of this article.</span></span> <span data-ttu-id="eddcd-113">如需詳細資訊，請參閱維琪百科上的[數位簽章](https://en.wikipedia.org/wiki/Digital_signature)。</span><span class="sxs-lookup"><span data-stu-id="eddcd-113">For more information, see [Digital Signature](https://en.wikipedia.org/wiki/Digital_signature) on Wikipedia.</span></span>
  
 <span data-ttu-id="eddcd-114">此案例會實作要求/回覆訊息模式，如下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="eddcd-114">This scenario implements a request/reply message pattern as illustrated by the following diagram.</span></span>  
  
 <span data-ttu-id="eddcd-115">![使用憑證的安全傳輸](media/8f7b8968-899f-4538-a9e8-0eaa872a291c.gif "8f7b8968-899f-4538-a9e8-0eaa872a291c")</span><span class="sxs-lookup"><span data-stu-id="eddcd-115">![Secure transfer using certificates](media/8f7b8968-899f-4538-a9e8-0eaa872a291c.gif "8f7b8968-899f-4538-a9e8-0eaa872a291c")</span></span>  
  
 <span data-ttu-id="eddcd-116">如需搭配服務使用憑證的詳細資訊，請參閱使用[憑證](working-with-certificates.md)和[如何：使用 SSL 憑證設定埠](how-to-configure-a-port-with-an-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="eddcd-116">For more information about using a certificate with a service, see [Working with Certificates](working-with-certificates.md) and [How to: Configure a Port with an SSL Certificate](how-to-configure-a-port-with-an-ssl-certificate.md).</span></span> <span data-ttu-id="eddcd-117">下表描述此案例的各種特性。</span><span class="sxs-lookup"><span data-stu-id="eddcd-117">The following table describes the various characteristics of the scenario.</span></span>  
  
|<span data-ttu-id="eddcd-118">特性</span><span class="sxs-lookup"><span data-stu-id="eddcd-118">Characteristic</span></span>|<span data-ttu-id="eddcd-119">描述</span><span class="sxs-lookup"><span data-stu-id="eddcd-119">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="eddcd-120">安全性模式</span><span class="sxs-lookup"><span data-stu-id="eddcd-120">Security Mode</span></span>|<span data-ttu-id="eddcd-121">傳輸</span><span class="sxs-lookup"><span data-stu-id="eddcd-121">Transport</span></span>|  
|<span data-ttu-id="eddcd-122">互通性</span><span class="sxs-lookup"><span data-stu-id="eddcd-122">Interoperability</span></span>|<span data-ttu-id="eddcd-123">使用現有 Web 服務用戶端和服務。</span><span class="sxs-lookup"><span data-stu-id="eddcd-123">With existing Web service clients and services.</span></span>|  
|<span data-ttu-id="eddcd-124">驗證 (伺服器)</span><span class="sxs-lookup"><span data-stu-id="eddcd-124">Authentication (Server)</span></span><br /><br /> <span data-ttu-id="eddcd-125">驗證 (用戶端)</span><span class="sxs-lookup"><span data-stu-id="eddcd-125">Authentication (Client)</span></span>|<span data-ttu-id="eddcd-126">是 (使用 SSL 憑證)</span><span class="sxs-lookup"><span data-stu-id="eddcd-126">Yes (using an SSL certificate)</span></span><br /><br /> <span data-ttu-id="eddcd-127">是 (使用 X.509 憑證)</span><span class="sxs-lookup"><span data-stu-id="eddcd-127">Yes (using an X.509 certificate)</span></span>|  
|<span data-ttu-id="eddcd-128">資料完整性</span><span class="sxs-lookup"><span data-stu-id="eddcd-128">Data Integrity</span></span>|<span data-ttu-id="eddcd-129">Yes</span><span class="sxs-lookup"><span data-stu-id="eddcd-129">Yes</span></span>|  
|<span data-ttu-id="eddcd-130">資料機密性</span><span class="sxs-lookup"><span data-stu-id="eddcd-130">Data Confidentiality</span></span>|<span data-ttu-id="eddcd-131">Yes</span><span class="sxs-lookup"><span data-stu-id="eddcd-131">Yes</span></span>|  
|<span data-ttu-id="eddcd-132">傳輸</span><span class="sxs-lookup"><span data-stu-id="eddcd-132">Transport</span></span>|<span data-ttu-id="eddcd-133">HTTPS</span><span class="sxs-lookup"><span data-stu-id="eddcd-133">HTTPS</span></span>|  
|<span data-ttu-id="eddcd-134">繫結</span><span class="sxs-lookup"><span data-stu-id="eddcd-134">Binding</span></span>|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="configure-the-service"></a><span data-ttu-id="eddcd-135">設定服務</span><span class="sxs-lookup"><span data-stu-id="eddcd-135">Configure the Service</span></span>  
 <span data-ttu-id="eddcd-136">由於此案例中的服務是在 IIS 之下裝載，因此該服務使用 web.config 檔案設定。</span><span class="sxs-lookup"><span data-stu-id="eddcd-136">Since the service in this scenario is hosted under IIS, it is configured with a web.config file.</span></span> <span data-ttu-id="eddcd-137">以下的 web.config 示範如何設定 <xref:System.ServiceModel.WSHttpBinding> 使用傳輸安全性和 X.509 用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="eddcd-137">The following web.config shows how to configure the <xref:System.ServiceModel.WSHttpBinding> to use transport security and X.509 client credentials.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <protocolMapping>  
      <add scheme="https" binding="wsHttpBinding" />  
    </protocolMapping>  
    <bindings>  
      <wsHttpBinding>  
        <!-- configure wsHttp binding with Transport security mode and clientCredentialType as Certificate -->  
        <binding>  
          <security mode="Transport">  
            <transport clientCredentialType="Certificate"/>
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>
           <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="configure-the-client"></a><span data-ttu-id="eddcd-138">設定用戶端</span><span class="sxs-lookup"><span data-stu-id="eddcd-138">Configure the Client</span></span>  
 <span data-ttu-id="eddcd-139">用戶端可以在程式碼或 app.config 檔案中設定。</span><span class="sxs-lookup"><span data-stu-id="eddcd-139">The client can be configured in code or in an app.config file.</span></span> <span data-ttu-id="eddcd-140">下列範例示範如何在程式碼中設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="eddcd-140">The following example shows how to configure the client in code.</span></span>  
  
```csharp
// Create the binding.  
var myBinding = new WSHttpBinding();  
myBinding.Security.Mode = SecurityMode.Transport;  
myBinding.Security.Transport.ClientCredentialType =  
   HttpClientCredentialType.Certificate;  
  
// Create the endpoint address. Note that the machine name
// must match the subject or DNS field of the X.509 certificate  
// used to authenticate the service.
var ea = new  
   EndpointAddress("https://localhost/CalculatorService/service.svc");  
  
// Create the client. The code for the calculator
// client is not shown here. See the sample applications  
// for examples of the calculator code.  
var cc =  
   new CalculatorClient(myBinding, ea);  
  
// The client must specify a certificate trusted by the server.  
cc.ClientCredentials.ClientCertificate.SetCertificate(  
    StoreLocation.CurrentUser,  
    StoreName.My,  
    X509FindType.FindBySubjectName,  
    "contoso.com");  
  
// Begin using the client.  
Console.WriteLine(cc.Add(100, 1111));  
//...  
cc.Close();  
```  
  
 <span data-ttu-id="eddcd-141">或者，您可以在 App.config 檔案中設定用戶端，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="eddcd-141">Alternatively you can configure the client in an App.config file as shown in the following example:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint address=" https://localhost/CalculatorService/service.svc "
                behaviorConfiguration="endpointCredentialBehavior"  
                binding="wsHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.Samples.TransportSecurity.ICalculator"/>  
    </client>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="endpointCredentialBehavior">  
          <clientCredentials>  
            <clientCertificate findValue="contoso.com"  
                               storeLocation="CurrentUser"  
                               storeName="My"  
                               x509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <bindings>  
      <wsHttpBinding>  
        <!-- configure wsHttpbinding with Transport security mode  
                   and clientCredentialType as Certificate -->  
        <binding name="Binding1">  
          <security mode="Transport">  
            <transport clientCredentialType="Certificate"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  </system.serviceModel>  
  
<startup><supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/></startup></configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="eddcd-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eddcd-142">See also</span></span>

- [<span data-ttu-id="eddcd-143">安全性總覽</span><span class="sxs-lookup"><span data-stu-id="eddcd-143">Security Overview</span></span>](security-overview.md)
- <span data-ttu-id="eddcd-144">[Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="eddcd-144">[Security Model for Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span></span>

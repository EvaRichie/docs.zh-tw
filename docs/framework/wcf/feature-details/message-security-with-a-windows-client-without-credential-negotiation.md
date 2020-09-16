---
title: 未使用認證交涉的 Windows 用戶端訊息安全性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fc07a26c-cbee-41c5-8fb0-329085fef749
ms.openlocfilehash: 3e5838c474a4f13136ed29baab440dc1559b95f5
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551089"
---
# <a name="message-security-with-a-windows-client-without-credential-negotiation"></a><span data-ttu-id="02437-102">未使用認證交涉的 Windows 用戶端訊息安全性</span><span class="sxs-lookup"><span data-stu-id="02437-102">Message Security with a Windows Client without Credential Negotiation</span></span>

<span data-ttu-id="02437-103">下列案例顯示 Windows Communication Foundation (由 Kerberos 通訊協定保護的 WCF) 用戶端和服務。</span><span class="sxs-lookup"><span data-stu-id="02437-103">The following scenario shows a Windows Communication Foundation (WCF) client and service secured by the Kerberos protocol.</span></span>

<span data-ttu-id="02437-104">服務和用戶端都是在相同的網域或受信任網域中。</span><span class="sxs-lookup"><span data-stu-id="02437-104">Both the service and the client are in the same domain or trusted domains.</span></span>

> [!NOTE]
> <span data-ttu-id="02437-105">此案例與 [Windows 用戶端的訊息安全性](message-security-with-a-windows-client.md) 之間的差異在於，此案例不會在傳送應用程式訊息之前，將服務認證與服務進行協調。</span><span class="sxs-lookup"><span data-stu-id="02437-105">The difference between this scenario and [Message Security with a Windows Client](message-security-with-a-windows-client.md) is that this scenario does not negotiate the service credential with the service prior to sending the application message.</span></span> <span data-ttu-id="02437-106">此外，因為這必須使用 Kerberos 通訊協定，所以此案例還需要 Windows 網域環境。</span><span class="sxs-lookup"><span data-stu-id="02437-106">Additionally, because this requires the Kerberos protocol, this scenario requires a Windows domain environment.</span></span>

<span data-ttu-id="02437-107">![未使用認證交涉的訊息安全性](media/0c9f9baa-2439-4ef9-92f4-43c242d85d0d.gif "0c9f9baa-2439-4ef9-92f4-43c242d85d0d")</span><span class="sxs-lookup"><span data-stu-id="02437-107">![Message security without credential negotiation](media/0c9f9baa-2439-4ef9-92f4-43c242d85d0d.gif "0c9f9baa-2439-4ef9-92f4-43c242d85d0d")</span></span>

|<span data-ttu-id="02437-108">特性</span><span class="sxs-lookup"><span data-stu-id="02437-108">Characteristic</span></span>|<span data-ttu-id="02437-109">描述</span><span class="sxs-lookup"><span data-stu-id="02437-109">Description</span></span>|
|--------------------|-----------------|
|<span data-ttu-id="02437-110">安全性模式</span><span class="sxs-lookup"><span data-stu-id="02437-110">Security Mode</span></span>|<span data-ttu-id="02437-111">訊息</span><span class="sxs-lookup"><span data-stu-id="02437-111">Message</span></span>|
|<span data-ttu-id="02437-112">互通性</span><span class="sxs-lookup"><span data-stu-id="02437-112">Interoperability</span></span>|<span data-ttu-id="02437-113">具備此特性，有 WS-Security 搭配 Kerberos 權杖設定檔相容的用戶端</span><span class="sxs-lookup"><span data-stu-id="02437-113">Yes, WS-Security with Kerberos token-profile compatible clients</span></span>|
|<span data-ttu-id="02437-114">驗證 (伺服器)</span><span class="sxs-lookup"><span data-stu-id="02437-114">Authentication (Server)</span></span>|<span data-ttu-id="02437-115">交互驗證伺服器和用戶端</span><span class="sxs-lookup"><span data-stu-id="02437-115">Mutual authentication of the server and client</span></span>|
|<span data-ttu-id="02437-116">驗證 (用戶端)</span><span class="sxs-lookup"><span data-stu-id="02437-116">Authentication (Client)</span></span>|<span data-ttu-id="02437-117">交互驗證伺服器和用戶端</span><span class="sxs-lookup"><span data-stu-id="02437-117">Mutual authentication of the server and client</span></span>|
|<span data-ttu-id="02437-118">完整性</span><span class="sxs-lookup"><span data-stu-id="02437-118">Integrity</span></span>|<span data-ttu-id="02437-119">是</span><span class="sxs-lookup"><span data-stu-id="02437-119">Yes</span></span>|
|<span data-ttu-id="02437-120">機密性</span><span class="sxs-lookup"><span data-stu-id="02437-120">Confidentiality</span></span>|<span data-ttu-id="02437-121">是</span><span class="sxs-lookup"><span data-stu-id="02437-121">Yes</span></span>|
|<span data-ttu-id="02437-122">傳輸</span><span class="sxs-lookup"><span data-stu-id="02437-122">Transport</span></span>|<span data-ttu-id="02437-123">HTTP</span><span class="sxs-lookup"><span data-stu-id="02437-123">HTTP</span></span>|
|<span data-ttu-id="02437-124">繫結</span><span class="sxs-lookup"><span data-stu-id="02437-124">Binding</span></span>|<xref:System.ServiceModel.WSHttpBinding>|

## <a name="service"></a><span data-ttu-id="02437-125">服務</span><span class="sxs-lookup"><span data-stu-id="02437-125">Service</span></span>

<span data-ttu-id="02437-126">下列程式碼和組態要獨立執行。</span><span class="sxs-lookup"><span data-stu-id="02437-126">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="02437-127">執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="02437-127">Do one of the following:</span></span>

- <span data-ttu-id="02437-128">使用不含組態的程式碼建立獨立服務。</span><span class="sxs-lookup"><span data-stu-id="02437-128">Create a stand-alone service using the code with no configuration.</span></span>

- <span data-ttu-id="02437-129">使用提供的組態建立服務，但不要定義任何端點。</span><span class="sxs-lookup"><span data-stu-id="02437-129">Create a service using the supplied configuration, but do not define any endpoints.</span></span>

### <a name="code"></a><span data-ttu-id="02437-130">程式碼</span><span class="sxs-lookup"><span data-stu-id="02437-130">Code</span></span>

<span data-ttu-id="02437-131">下列程式碼會建立使用訊息安全性的服務端點。</span><span class="sxs-lookup"><span data-stu-id="02437-131">The following code creates a service endpoint that uses message security.</span></span> <span data-ttu-id="02437-132">程式碼會停用服務認證交涉以及安全性內容權杖 (SCT) 的建立。</span><span class="sxs-lookup"><span data-stu-id="02437-132">The code disables service credential negotiation, and the establishment of a security context token (SCT).</span></span>

> [!NOTE]
> <span data-ttu-id="02437-133">若要在沒有交涉的情況下使用 Windows 認證類型，服務的使用者帳戶必須可以存取已在 Active Directory 網域中註冊的服務主要名稱 (SPN)。</span><span class="sxs-lookup"><span data-stu-id="02437-133">To use the Windows credential type without negotiation, the service's user account must have access to service principal name (SPN) that is registered with the Active Directory domain.</span></span> <span data-ttu-id="02437-134">您可以使用兩種方式執行此動作：</span><span class="sxs-lookup"><span data-stu-id="02437-134">You can do this in two ways:</span></span>

1. <span data-ttu-id="02437-135">使用 `NetworkService` 或 `LocalSystem` 帳戶來執行服務。</span><span class="sxs-lookup"><span data-stu-id="02437-135">Use the `NetworkService` or `LocalSystem` account to run your service.</span></span> <span data-ttu-id="02437-136">因為這些帳戶可以存取電腦加入 Active Directory 網域時所建立的電腦 SPN，所以 WCF 會在服務的中繼資料中自動產生適當的 SPN 元素 (Web 服務描述語言或 WSDL) 。</span><span class="sxs-lookup"><span data-stu-id="02437-136">Because those accounts have access to the machine SPN that is established when the machine joins the Active Directory domain, WCF automatically generates the proper SPN element inside the service's endpoint in the service's metadata (Web Services Description Language, or WSDL).</span></span>

2. <span data-ttu-id="02437-137">使用任意的 Active Directory 網域帳戶來執行服務。</span><span class="sxs-lookup"><span data-stu-id="02437-137">Use an arbitrary Active Directory domain account to run your service.</span></span> <span data-ttu-id="02437-138">在這種情況下，您必須建立該網域帳戶的 SPN。</span><span class="sxs-lookup"><span data-stu-id="02437-138">In this case, you need to establish an SPN for that domain account.</span></span> <span data-ttu-id="02437-139">使用 Setspn.exe 公用程式工具來建立，是其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="02437-139">One way of doing this is to use the Setspn.exe utility tool.</span></span> <span data-ttu-id="02437-140">一旦建立服務帳戶的 SPN，請設定 WCF 以透過 (WSDL) 的中繼資料，將該 SPN 發行至服務的用戶端。</span><span class="sxs-lookup"><span data-stu-id="02437-140">Once the SPN is created for the service's account, configure WCF to publish that SPN to the service's clients through its metadata (WSDL).</span></span> <span data-ttu-id="02437-141">不論是透過應用程式組態檔或程式碼，都可以設定公開端點的端點身分識別來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="02437-141">This is done by setting the endpoint identity for the exposed endpoint, either though an application configuration file or code.</span></span> <span data-ttu-id="02437-142">下列範例會以程式設計方式發行身分識別。</span><span class="sxs-lookup"><span data-stu-id="02437-142">The following example publishes the identity programmatically.</span></span>

<span data-ttu-id="02437-143">如需 Spn、Kerberos 通訊協定和 Active Directory 的詳細資訊，請參閱 [Windows 的 Kerberos 技術補充](/previous-versions/msp-n-p/ff649429(v=pandp.10))。</span><span class="sxs-lookup"><span data-stu-id="02437-143">For more information about SPNs, the Kerberos protocol, and Active Directory, see [Kerberos Technical Supplement for Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10)).</span></span> <span data-ttu-id="02437-144">如需端點身分識別的詳細資訊，請參閱 [SecurityBindingElement 驗證模式](securitybindingelement-authentication-modes.md)。</span><span class="sxs-lookup"><span data-stu-id="02437-144">For more information about endpoint identities, see [SecurityBindingElement Authentication Modes](securitybindingelement-authentication-modes.md).</span></span>

[!code-csharp[C_SecurityScenarios#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#12)]
[!code-vb[C_SecurityScenarios#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#12)]

### <a name="configuration"></a><span data-ttu-id="02437-145">組態</span><span class="sxs-lookup"><span data-stu-id="02437-145">Configuration</span></span>

<span data-ttu-id="02437-146">可以使用以下組態來取代程式碼。</span><span class="sxs-lookup"><span data-stu-id="02437-146">The following configuration can be used instead of the code.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <behaviors />
    <services>
      <service behaviorConfiguration="" name="ServiceModel.Calculator">
        <endpoint address="http://localhost/Calculator"
                  binding="wsHttpBinding"
                  bindingConfiguration="KerberosBinding"
                  name="WSHttpBinding_ICalculator"
                  contract="ServiceModel.ICalculator"
                  listenUri="net.tcp://localhost/metadata" >
         <identity>
            <servicePrincipalName value="service_spn_name" />
         </identity>
        </endpoint>
      </service>
    </services>
    <bindings>
      <wsHttpBinding>
        <binding name="KerberosBinding">
          <security>
            <message negotiateServiceCredential="false"
                     establishSecurityContext="false" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client />
  </system.serviceModel>
</configuration>
```

## <a name="client"></a><span data-ttu-id="02437-147">用戶端</span><span class="sxs-lookup"><span data-stu-id="02437-147">Client</span></span>

<span data-ttu-id="02437-148">下列程式碼和組態要獨立執行。</span><span class="sxs-lookup"><span data-stu-id="02437-148">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="02437-149">執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="02437-149">Do one of the following:</span></span>

- <span data-ttu-id="02437-150">使用此程式碼 (和用戶端程式碼) 建立獨立用戶端。</span><span class="sxs-lookup"><span data-stu-id="02437-150">Create a stand-alone client using the code (and client code).</span></span>

- <span data-ttu-id="02437-151">建立未定義任何端點位址的用戶端，</span><span class="sxs-lookup"><span data-stu-id="02437-151">Create a client that does not define any endpoint addresses.</span></span> <span data-ttu-id="02437-152">然後改用可接受組態名稱當做引數的用戶端建構函式。</span><span class="sxs-lookup"><span data-stu-id="02437-152">Instead, use the client constructor that takes the configuration name as an argument.</span></span> <span data-ttu-id="02437-153">例如：</span><span class="sxs-lookup"><span data-stu-id="02437-153">For example:</span></span>

  [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
  [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]

### <a name="code"></a><span data-ttu-id="02437-154">程式碼</span><span class="sxs-lookup"><span data-stu-id="02437-154">Code</span></span>

<span data-ttu-id="02437-155">下列程式碼會設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="02437-155">The following code configures the client.</span></span> <span data-ttu-id="02437-156">安全性模式設定為 Message，而用戶端認證類型設定為 Windows。</span><span class="sxs-lookup"><span data-stu-id="02437-156">The security mode is set to Message, and the client credential type is set to Windows.</span></span> <span data-ttu-id="02437-157">請注意，<xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> 和 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 屬性會設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="02437-157">Note that the <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> and <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> properties are set to `false`.</span></span>

> [!NOTE]
> <span data-ttu-id="02437-158">若要在沒有交涉的情況下使用 Windows 認證類型，就必須先使用服務的帳戶 SPN 設定用戶端，再開始與服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="02437-158">To use Windows credential type without negotiation, the client must be configured with the service's account SPN prior to commencing the communication with the service.</span></span> <span data-ttu-id="02437-159">用戶端會使用 SPN 取得 Kerberos 權杖，以驗證並保護與服務進行的通訊。</span><span class="sxs-lookup"><span data-stu-id="02437-159">The client uses the SPN to get the Kerberos token to authenticate and secure the communication with the service.</span></span> <span data-ttu-id="02437-160">下列範例示範如何使用服務的 SPN 來設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="02437-160">The following sample shows how to configure the client with the service's SPN.</span></span> <span data-ttu-id="02437-161">如果您使用「使用的 [中繼資料公用程式工具」 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md) 來產生用戶端，如果服務的中繼資料包含該資訊，服務的 SPN 將會自動從服務的中繼資料傳送至用戶端 (WSDL) 。</span><span class="sxs-lookup"><span data-stu-id="02437-161">If you are using the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to generate the client, the service's SPN will be automatically propagated to the client from the service's metadata (WSDL), if the service's metadata contains that information.</span></span> <span data-ttu-id="02437-162">如需如何設定服務以在服務的中繼資料中包含其 SPN 的詳細資訊，請參閱本主題稍後的「服務」一節。</span><span class="sxs-lookup"><span data-stu-id="02437-162">For more information about how to configure the service to include its SPN in the service's metadata, see the "Service" section later in this topic .</span></span>
>
> <span data-ttu-id="02437-163">如需 Spn、Kerberos 和 Active Directory 的詳細資訊，請參閱 [Windows 的 Kerberos 技術補充（適用于 Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10))）。</span><span class="sxs-lookup"><span data-stu-id="02437-163">For more information about SPNs, Kerberos, and Active Directory, see [Kerberos Technical Supplement for Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10)).</span></span> <span data-ttu-id="02437-164">如需端點身分識別的詳細資訊，請參閱 [SecurityBindingElement Authentication 模式](securitybindingelement-authentication-modes.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="02437-164">For more information about endpoint identities, see [SecurityBindingElement Authentication Modes](securitybindingelement-authentication-modes.md) topic.</span></span>

[!code-csharp[C_SecurityScenarios#19](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#19)]
[!code-vb[C_SecurityScenarios#19](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#19)]

### <a name="configuration"></a><span data-ttu-id="02437-165">組態</span><span class="sxs-lookup"><span data-stu-id="02437-165">Configuration</span></span>

<span data-ttu-id="02437-166">下列程式碼會設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="02437-166">The following code configures the client.</span></span> <span data-ttu-id="02437-167">請注意，專案 [\<servicePrincipalName>](../../configure-apps/file-schema/wcf/serviceprincipalname.md) 必須設定為符合服務的 SPN （在 Active Directory 網域中註冊服務的帳戶）。</span><span class="sxs-lookup"><span data-stu-id="02437-167">Note that the [\<servicePrincipalName>](../../configure-apps/file-schema/wcf/serviceprincipalname.md) element must be set to match the service's SPN as registered for the service's account in the Active Directory domain.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" >
          <security mode="Message">
            <message clientCredentialType="Windows"
                     negotiateServiceCredential="false"
                     establishSecurityContext="false" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client>
      <endpoint address="http://localhost/Calculator"
                binding="wsHttpBinding"
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"
                name="WSHttpBinding_ICalculator">
        <identity>
          <servicePrincipalName value="service_spn_name" />
        </identity>
      </endpoint>
    </client>
  </system.serviceModel>
</configuration>
```

## <a name="see-also"></a><span data-ttu-id="02437-168">另請參閱</span><span class="sxs-lookup"><span data-stu-id="02437-168">See also</span></span>

- [<span data-ttu-id="02437-169">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="02437-169">Security Overview</span></span>](security-overview.md)
- [<span data-ttu-id="02437-170">服務身分識別和驗證</span><span class="sxs-lookup"><span data-stu-id="02437-170">Service Identity and Authentication</span></span>](service-identity-and-authentication.md)
- <span data-ttu-id="02437-171">[Windows Server AppFabric 的資訊安全模型](/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="02437-171">[Security Model for Windows Server App Fabric](/previous-versions/appfabric/ee677202(v=azure.10))</span></span>

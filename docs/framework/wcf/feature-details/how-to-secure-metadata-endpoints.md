---
title: HOW TO：安全中繼資料端點
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9f71b6ae-737c-4382-8d89-0a7b1c7e182b
ms.openlocfilehash: 2746c608fb47b94446c5d7e10748ba185d555e7f
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202334"
---
# <a name="how-to-secure-metadata-endpoints"></a><span data-ttu-id="fff7d-102">HOW TO：安全中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="fff7d-102">How to: Secure Metadata Endpoints</span></span>

<span data-ttu-id="fff7d-103">服務的中繼資料可能包含有關應用程式而可能會遭到惡意使用者利用的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="fff7d-103">Metadata for a service can contain sensitive information about your application that a malicious user can leverage.</span></span> <span data-ttu-id="fff7d-104">服務的取用者也可能會要求安全機制來取得關於服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fff7d-104">Consumers of your service may also require a secure mechanism for obtaining metadata about your service.</span></span> <span data-ttu-id="fff7d-105">因此，有時候會需要使用安全端點來發行中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fff7d-105">Therefore, it is sometimes necessary to publish your metadata using a secure endpoint.</span></span>

<span data-ttu-id="fff7d-106">中繼資料端點通常是使用 Windows Communication Foundation （WCF）中定義的標準安全性機制來保護應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="fff7d-106">Metadata endpoints are generally secured using the standard security mechanisms defined in Windows Communication Foundation (WCF) for securing application endpoints.</span></span> <span data-ttu-id="fff7d-107">如需詳細資訊，請參閱[安全性概觀](security-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fff7d-107">For more information, see [Security Overview](security-overview.md).</span></span>

<span data-ttu-id="fff7d-108">本主題會逐步解說建立受 Secure Sockets Layer (SSL) 憑證保護之端點 (也就是 HTTPS 端點) 的步驟。</span><span class="sxs-lookup"><span data-stu-id="fff7d-108">This topic walks through the steps to create an endpoint secured by a Secure Sockets Layer (SSL) certificate or, in other words, an HTTPS endpoint.</span></span>

### <a name="to-create-a-secure-https-get-metadata-endpoint-in-code"></a><span data-ttu-id="fff7d-109">在程式碼中建立安全的 HTTPS GET 中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="fff7d-109">To create a secure HTTPS GET metadata endpoint in code</span></span>

1. <span data-ttu-id="fff7d-110">使用適當的 X.509 憑證設定連接埠。</span><span class="sxs-lookup"><span data-stu-id="fff7d-110">Configure a port with an appropriate X.509 certificate.</span></span> <span data-ttu-id="fff7d-111">憑證必須來自受信任的授權單位 (CA)，而且必須可以用於「服務授權」。</span><span class="sxs-lookup"><span data-stu-id="fff7d-111">The certificate must come from a trusted authority, and it must have an intended use of "Service Authorization."</span></span> <span data-ttu-id="fff7d-112">您必須使用 HttpCfg.exe 工具將憑證附加到該連接埠。</span><span class="sxs-lookup"><span data-stu-id="fff7d-112">You must use the HttpCfg.exe tool to attach the certificate to the port.</span></span> <span data-ttu-id="fff7d-113">請參閱[如何：使用 SSL 憑證設定埠](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="fff7d-113">See [How to: Configure a Port with an SSL Certificate](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fff7d-114">憑證的主體或是其網域名稱系統 (DNS) 必須符合電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="fff7d-114">The subject of the certificate or its Domain Name System (DNS) must match the name of the computer.</span></span> <span data-ttu-id="fff7d-115">這點是必要條件，因為 HTTPS 機制一開始執行的一個步驟，就是檢查該憑證是否為發行給與其被叫用位址相同的統一資源識別元 (URI)。</span><span class="sxs-lookup"><span data-stu-id="fff7d-115">This is essential because one of the first steps the HTTPS mechanism performs is to check that the certificate is issued to the same Uniform Resource Identifier (URI) as the address upon which it is invoked.</span></span>

2. <span data-ttu-id="fff7d-116">建立 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 類別的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="fff7d-116">Create a new instance of the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> class.</span></span>

3. <span data-ttu-id="fff7d-117">將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 類別的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="fff7d-117">Set the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> property of the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> class to `true`.</span></span>

4. <span data-ttu-id="fff7d-118">將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> 屬性設定為適當的 URL。</span><span class="sxs-lookup"><span data-stu-id="fff7d-118">Set the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> property to an appropriate URL.</span></span> <span data-ttu-id="fff7d-119">請注意，如果您指定絕對位址，則 URL 的開頭必須是配置 `https://` 。</span><span class="sxs-lookup"><span data-stu-id="fff7d-119">Note that if you specify an absolute address, the URL must begin with the scheme `https://`.</span></span> <span data-ttu-id="fff7d-120">如果是指定相對位址，您就必須提供服務主機的 HTTPS 起始位址。</span><span class="sxs-lookup"><span data-stu-id="fff7d-120">If you specify a relative address, you must supply an HTTPS base address for your service host.</span></span> <span data-ttu-id="fff7d-121">如果沒有設定這個屬性，預設的位址就會是 ""，或是直接使用服務的 HTTPS 起始位址。</span><span class="sxs-lookup"><span data-stu-id="fff7d-121">If this property is not set, the default address is "", or directly at the HTTPS base address for the service.</span></span>

5. <span data-ttu-id="fff7d-122">在 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 類別之 <xref:System.ServiceModel.Description.ServiceDescription> 屬性所傳回的行為集合中新增執行個體，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="fff7d-122">Add the instance to the behaviors collection that the <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> property of the <xref:System.ServiceModel.Description.ServiceDescription> class returns, as shown in the following code.</span></span>

    [!code-csharp[c_HowToSecureEndpoint#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosecureendpoint/cs/source.cs#1)]
    [!code-vb[c_HowToSecureEndpoint#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosecureendpoint/vb/source.vb#1)]

### <a name="to-create-a-secure-https-get-metadata-endpoint-in-configuration"></a><span data-ttu-id="fff7d-123">在組態中建立安全的 HTTPS GET 中繼資料端點</span><span class="sxs-lookup"><span data-stu-id="fff7d-123">To create a secure HTTPS GET metadata endpoint in configuration</span></span>

1. <span data-ttu-id="fff7d-124">將 [\<behaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素新增至 [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 服務設定檔的專案。</span><span class="sxs-lookup"><span data-stu-id="fff7d-124">Add a [\<behaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) element to the [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) element of the configuration file for your service.</span></span>

2. <span data-ttu-id="fff7d-125">將 [\<serviceBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) 元素新增至專案 [\<behaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 。</span><span class="sxs-lookup"><span data-stu-id="fff7d-125">Add a [\<serviceBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) element to the [\<behaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) element.</span></span>

3. <span data-ttu-id="fff7d-126">將 [\<behavior>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素新增至專案 `<serviceBehaviors>` 。</span><span class="sxs-lookup"><span data-stu-id="fff7d-126">Add a [\<behavior>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) element to the `<serviceBehaviors>` element.</span></span>

4. <span data-ttu-id="fff7d-127">將 `name` 項目的 `<behavior>` 屬性設定為適當的值。</span><span class="sxs-lookup"><span data-stu-id="fff7d-127">Set the `name` attribute of the `<behavior>` element to an appropriate value.</span></span> <span data-ttu-id="fff7d-128">`name` 屬性 (Attribute) 是必要項。</span><span class="sxs-lookup"><span data-stu-id="fff7d-128">The `name` attribute is required.</span></span> <span data-ttu-id="fff7d-129">下面這個範例會使用值 `mySvcBehavior`。</span><span class="sxs-lookup"><span data-stu-id="fff7d-129">The example below uses the value `mySvcBehavior`.</span></span>

5. <span data-ttu-id="fff7d-130">將加入 [\<serviceMetadata>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) 至 `<behavior>` 元素。</span><span class="sxs-lookup"><span data-stu-id="fff7d-130">Add a [\<serviceMetadata>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) to the `<behavior>` element.</span></span>

6. <span data-ttu-id="fff7d-131">將 `httpsGetEnabled` 項目的 `<serviceMetadata>` 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="fff7d-131">Set the `httpsGetEnabled` attribute of the `<serviceMetadata>` element to `true`.</span></span>

7. <span data-ttu-id="fff7d-132">將 `httpsGetUrl` 項目的 `<serviceMetadata>` 屬性設定為適當的值。</span><span class="sxs-lookup"><span data-stu-id="fff7d-132">Set the `httpsGetUrl` attribute of the `<serviceMetadata>` element to an appropriate value.</span></span> <span data-ttu-id="fff7d-133">請注意，如果您指定絕對位址，則 URL 的開頭必須是配置 `https://` 。</span><span class="sxs-lookup"><span data-stu-id="fff7d-133">Note that if you specify an absolute address, the URL must begin with the scheme `https://`.</span></span> <span data-ttu-id="fff7d-134">如果是指定相對位址，您就必須提供服務主機的 HTTPS 起始位址。</span><span class="sxs-lookup"><span data-stu-id="fff7d-134">If you specify a relative address, you must supply an HTTPS base address for your service host.</span></span> <span data-ttu-id="fff7d-135">如果沒有設定這個屬性，預設的位址就會是 ""，或是直接使用服務的 HTTPS 起始位址。</span><span class="sxs-lookup"><span data-stu-id="fff7d-135">If this property is not set, the default address is "", or directly at the HTTPS base address for the service.</span></span>

8. <span data-ttu-id="fff7d-136">若要使用服務的行為，請將 `behaviorConfiguration` 元素的屬性設定 [\<service>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) 為行為元素的 name 屬性值。</span><span class="sxs-lookup"><span data-stu-id="fff7d-136">To use the behavior with a service, set the `behaviorConfiguration` attribute of the [\<service>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) element to the value of the name attribute of the behavior element.</span></span> <span data-ttu-id="fff7d-137">下列組態程式碼會示範完整的範例。</span><span class="sxs-lookup"><span data-stu-id="fff7d-137">The following configuration code shows a complete example.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
     <system.serviceModel>
      <behaviors>
       <serviceBehaviors>
        <behavior name="mySvcBehavior">
         <serviceMetadata httpsGetEnabled="true"
              httpsGetUrl="https://localhost:8036/calcMetadata" />
        </behavior>
       </serviceBehaviors>
      </behaviors>
     <services>
      <service behaviorConfiguration="mySvcBehavior"
            name="Microsoft.Security.Samples.Calculator">
       <endpoint address="http://localhost:8037/ServiceModelSamples/calculator"
       binding="wsHttpBinding" bindingConfiguration=""
       contract="Microsoft.Security.Samples.ICalculator" />
      </service>
     </services>
    </system.serviceModel>
    </configuration>
    ```

## <a name="example"></a><span data-ttu-id="fff7d-138">範例</span><span class="sxs-lookup"><span data-stu-id="fff7d-138">Example</span></span>

<span data-ttu-id="fff7d-139">下列範例會建立 <xref:System.ServiceModel.ServiceHost> 類別的執行個體，並新增端點。</span><span class="sxs-lookup"><span data-stu-id="fff7d-139">The following example creates an instance of a <xref:System.ServiceModel.ServiceHost> class and adds an endpoint.</span></span> <span data-ttu-id="fff7d-140">接下來，這段程式碼會建立 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 類別的執行個體，並設定其中屬性來建立安全的中繼資料交換點。</span><span class="sxs-lookup"><span data-stu-id="fff7d-140">The code then creates an instance of the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> class and sets the properties to create a secure metadata exchange point.</span></span>

[!code-csharp[c_HowToSecureEndpoint#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosecureendpoint/cs/source.cs#0)]
[!code-vb[c_HowToSecureEndpoint#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosecureendpoint/vb/source.vb#0)]

## <a name="compiling-the-code"></a><span data-ttu-id="fff7d-141">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="fff7d-141">Compiling the Code</span></span>

<span data-ttu-id="fff7d-142">此程式碼範例會使用下列命名空間 (Namespace)：</span><span class="sxs-lookup"><span data-stu-id="fff7d-142">The code example uses the following namespaces:</span></span>

- <xref:System.ServiceModel?displayProperty=nameWithType>

- <xref:System.ServiceModel.Description?displayProperty=nameWithType>

## <a name="see-also"></a><span data-ttu-id="fff7d-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fff7d-143">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>
- [<span data-ttu-id="fff7d-144">如何：使用 SSL 憑證設定連接埠</span><span class="sxs-lookup"><span data-stu-id="fff7d-144">How to: Configure a Port with an SSL Certificate</span></span>](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [<span data-ttu-id="fff7d-145">Working with Certificates</span><span class="sxs-lookup"><span data-stu-id="fff7d-145">Working with Certificates</span></span>](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [<span data-ttu-id="fff7d-146">中繼資料的安全性考量</span><span class="sxs-lookup"><span data-stu-id="fff7d-146">Security Considerations with Metadata</span></span>](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)
- [<span data-ttu-id="fff7d-147">Securing Services and Clients</span><span class="sxs-lookup"><span data-stu-id="fff7d-147">Securing Services and Clients</span></span>](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)

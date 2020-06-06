---
title: <authentication> 項目的 <serviceCertificate>
ms.date: 03/30/2017
ms.assetid: 733b67b4-08a1-4d25-9741-10046f9357ef
ms.openlocfilehash: 29170f032469b4d55b50f57ca06ce403a5aeaf2c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398232"
---
# <a name="authentication-of-servicecertificate-element"></a><span data-ttu-id="74711-102">\<authentication> 項目的 \<serviceCertificate></span><span class="sxs-lookup"><span data-stu-id="74711-102">\<authentication> of \<serviceCertificate> Element</span></span>
<span data-ttu-id="74711-103">指定用戶端 Proxy 用來驗證服務憑證的設定，而這份憑證是使用 SSL/TLS 交涉所取得。</span><span class="sxs-lookup"><span data-stu-id="74711-103">Specifies the settings used by the client proxy to authenticate service certificates that are obtained using SSL/TLS negotiation.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCertificate>**](servicecertificate-of-clientcredentials-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<authentication>**  
  
## <a name="syntax"></a><span data-ttu-id="74711-104">語法</span><span class="sxs-lookup"><span data-stu-id="74711-104">Syntax</span></span>  
  
```xml  
<authentication customCertificateValidatorType="String"
                certificateValidationMode="None/PeerTrust/ChainTrust/PeerOrChainTrust/Custom"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="LocalMachine/CurrentUser" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="74711-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="74711-105">Attributes and Elements</span></span>  
 <span data-ttu-id="74711-106">下列各節說明屬性、子元素和父元素</span><span class="sxs-lookup"><span data-stu-id="74711-106">The following sections describe attributes, child elements, and parent elements</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="74711-107">屬性</span><span class="sxs-lookup"><span data-stu-id="74711-107">Attributes</span></span>  
  
|<span data-ttu-id="74711-108">屬性</span><span class="sxs-lookup"><span data-stu-id="74711-108">Attribute</span></span>|<span data-ttu-id="74711-109">描述</span><span class="sxs-lookup"><span data-stu-id="74711-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="74711-110">customCertificateValidatorType</span><span class="sxs-lookup"><span data-stu-id="74711-110">customCertificateValidatorType</span></span>|<span data-ttu-id="74711-111">字串。</span><span class="sxs-lookup"><span data-stu-id="74711-111">String.</span></span> <span data-ttu-id="74711-112">用來驗證自訂型別的型別和組件。</span><span class="sxs-lookup"><span data-stu-id="74711-112">A type and assembly used to validate a custom type.</span></span>|  
|<span data-ttu-id="74711-113">certificateValidationMode</span><span class="sxs-lookup"><span data-stu-id="74711-113">certificateValidationMode</span></span>|<span data-ttu-id="74711-114">指定用來驗證認證之三個模式的其中一個。</span><span class="sxs-lookup"><span data-stu-id="74711-114">Specifies one of three modes used to validate credentials.</span></span> <span data-ttu-id="74711-115">如果設定為 `Custom`，也必須提供 customCertificateValidator。</span><span class="sxs-lookup"><span data-stu-id="74711-115">If set to `Custom`, then a customCertificateValidator must also be supplied.</span></span> <span data-ttu-id="74711-116">預設值為 `ChainTrust`。</span><span class="sxs-lookup"><span data-stu-id="74711-116">The default is `ChainTrust`.</span></span>|  
|<span data-ttu-id="74711-117">revocationMode</span><span class="sxs-lookup"><span data-stu-id="74711-117">revocationMode</span></span>|<span data-ttu-id="74711-118">用於檢查撤銷憑證清單 (CRL) 的模式之一。</span><span class="sxs-lookup"><span data-stu-id="74711-118">One of the modes used to check for a revoked certificate lists (CRL).</span></span> <span data-ttu-id="74711-119">預設值為 `Online`。</span><span class="sxs-lookup"><span data-stu-id="74711-119">The default is `Online`.</span></span>|  
|<span data-ttu-id="74711-120">trustedStoreLocation</span><span class="sxs-lookup"><span data-stu-id="74711-120">trustedStoreLocation</span></span>|<span data-ttu-id="74711-121">兩個系統存放位置的其中一個：`LocalMachine` 或 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="74711-121">One of the two system store locations: `LocalMachine` or `CurrentUser`.</span></span> <span data-ttu-id="74711-122">當與用戶端交涉服務憑證時，會使用這個值。</span><span class="sxs-lookup"><span data-stu-id="74711-122">This value is used when a service certificate is negotiated to the client.</span></span> <span data-ttu-id="74711-123">會針對指定存放區位置中的「**受信任的人**」存放區執行驗證。</span><span class="sxs-lookup"><span data-stu-id="74711-123">Validation is performed against the **Trusted People** store in the specified store location.</span></span> <span data-ttu-id="74711-124">預設值為 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="74711-124">The default is `CurrentUser`.</span></span>|  
  
## <a name="customcertificatevalidator-attribute"></a><span data-ttu-id="74711-125">customCertificateValidator 屬性</span><span class="sxs-lookup"><span data-stu-id="74711-125">customCertificateValidator Attribute</span></span>  
  
|<span data-ttu-id="74711-126">值</span><span class="sxs-lookup"><span data-stu-id="74711-126">Value</span></span>|<span data-ttu-id="74711-127">描述</span><span class="sxs-lookup"><span data-stu-id="74711-127">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="74711-128">String</span><span class="sxs-lookup"><span data-stu-id="74711-128">String</span></span>|<span data-ttu-id="74711-129">指定型別名稱和組件以及用來尋找此型別的其他資料。</span><span class="sxs-lookup"><span data-stu-id="74711-129">Specifies the type name and assembly and other data used to find the type.</span></span>|  
  
## <a name="certificatevalidationmode-attribute"></a><span data-ttu-id="74711-130">certificateValidationMode 屬性</span><span class="sxs-lookup"><span data-stu-id="74711-130">certificateValidationMode Attribute</span></span>  
  
|<span data-ttu-id="74711-131">值</span><span class="sxs-lookup"><span data-stu-id="74711-131">Value</span></span>|<span data-ttu-id="74711-132">描述</span><span class="sxs-lookup"><span data-stu-id="74711-132">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="74711-133">列舉型別</span><span class="sxs-lookup"><span data-stu-id="74711-133">Enumeration</span></span>|<span data-ttu-id="74711-134">下列其中一個值：None、PeerTrust、ChainTrust、PeerOrChainTrust、Custom。</span><span class="sxs-lookup"><span data-stu-id="74711-134">One of the following values: None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom.</span></span><br /><br /> <span data-ttu-id="74711-135">如需詳細資訊，請參閱[使用憑證](../../../wcf/feature-details/working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="74711-135">For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).</span></span>|  
  
## <a name="revocationmode-attribute"></a><span data-ttu-id="74711-136">revocationMode 屬性</span><span class="sxs-lookup"><span data-stu-id="74711-136">revocationMode Attribute</span></span>  
  
|<span data-ttu-id="74711-137">值</span><span class="sxs-lookup"><span data-stu-id="74711-137">Value</span></span>|<span data-ttu-id="74711-138">描述</span><span class="sxs-lookup"><span data-stu-id="74711-138">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="74711-139">列舉型別</span><span class="sxs-lookup"><span data-stu-id="74711-139">Enumeration</span></span>|<span data-ttu-id="74711-140">下列其中一個值：NoCheck、Online、Offline。</span><span class="sxs-lookup"><span data-stu-id="74711-140">One of the following values: NoCheck, Online, Offline.</span></span><br /><br /> <span data-ttu-id="74711-141">如需詳細資訊，請參閱[使用憑證](../../../wcf/feature-details/working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="74711-141">For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).</span></span>|  
  
## <a name="trustedstorelocation-attribute"></a><span data-ttu-id="74711-142">trustedStoreLocation 屬性</span><span class="sxs-lookup"><span data-stu-id="74711-142">trustedStoreLocation Attribute</span></span>  
  
|<span data-ttu-id="74711-143">值</span><span class="sxs-lookup"><span data-stu-id="74711-143">Value</span></span>|<span data-ttu-id="74711-144">描述</span><span class="sxs-lookup"><span data-stu-id="74711-144">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="74711-145">列舉型別</span><span class="sxs-lookup"><span data-stu-id="74711-145">Enumeration</span></span>|<span data-ttu-id="74711-146">下列其中一個值：LocalMachine 或 CurrentUser。</span><span class="sxs-lookup"><span data-stu-id="74711-146">One of the following values: LocalMachine or CurrentUser.</span></span> <span data-ttu-id="74711-147">預設值為 CurrentUser。</span><span class="sxs-lookup"><span data-stu-id="74711-147">The default is CurrentUser.</span></span> <span data-ttu-id="74711-148">如果用戶端應用程式是在系統帳戶下執行，則憑證通常位於 LocalMachine 之下。</span><span class="sxs-lookup"><span data-stu-id="74711-148">If the client application is running under a system account, then the certificate is typically under LocalMachine.</span></span> <span data-ttu-id="74711-149">如果用戶端應用程式是在使用者帳戶下執行，則憑證通常位於 CurrentUser 中。</span><span class="sxs-lookup"><span data-stu-id="74711-149">If the client application is running under a user account, then the certificate is typically in CurrentUser.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="74711-150">子元素</span><span class="sxs-lookup"><span data-stu-id="74711-150">Child Elements</span></span>  
 <span data-ttu-id="74711-151">無。</span><span class="sxs-lookup"><span data-stu-id="74711-151">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="74711-152">父項目</span><span class="sxs-lookup"><span data-stu-id="74711-152">Parent Elements</span></span>  
  
|<span data-ttu-id="74711-153">元素</span><span class="sxs-lookup"><span data-stu-id="74711-153">Element</span></span>|<span data-ttu-id="74711-154">描述</span><span class="sxs-lookup"><span data-stu-id="74711-154">Description</span></span>|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)|<span data-ttu-id="74711-155">指定對用戶端驗證服務時所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="74711-155">Specifies a certificate to use when authenticating a service to the client.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="74711-156">備註</span><span class="sxs-lookup"><span data-stu-id="74711-156">Remarks</span></span>  
 <span data-ttu-id="74711-157">這個組態項目的 `certificateValidationMode` 屬性會指定用來驗證憑證的信任層級。</span><span class="sxs-lookup"><span data-stu-id="74711-157">The `certificateValidationMode` attribute of this configuration element specifies the level of trust used to authenticate certificates.</span></span> <span data-ttu-id="74711-158">根據預設，層級會設為 `ChainTrust`，指定每一個憑證必須出現在鏈結頂端以受信任的憑證授權單位為結尾的憑證階層中。</span><span class="sxs-lookup"><span data-stu-id="74711-158">By default, the level is set to `ChainTrust`, which specifies that each certificate must be found in a hierarchy of certificates ending in a trusted certification authority at the top of the chain.</span></span> <span data-ttu-id="74711-159">這是最安全的模式。</span><span class="sxs-lookup"><span data-stu-id="74711-159">This is the most secure mode.</span></span> <span data-ttu-id="74711-160">您也可以將值設定為 `PeerOrChainTrust`，指定可接受自行發出的憑證 (對等信任)，以及信任鏈結內的憑證。</span><span class="sxs-lookup"><span data-stu-id="74711-160">You can also set the value to `PeerOrChainTrust`, which specifies that self-issued certificates (peer trust) are accepted as well as certificates that are in a trusted chain.</span></span> <span data-ttu-id="74711-161">這個值會在開發及偵錯用戶端和服務時使用，因為自行發出的憑證不需要從受信任的授權單位購買。</span><span class="sxs-lookup"><span data-stu-id="74711-161">This value is used when developing and debugging clients and services because self-issued certificates need not be purchased from a trusted authority.</span></span> <span data-ttu-id="74711-162">部署用戶端時，請改用 `ChainTrust` 值。</span><span class="sxs-lookup"><span data-stu-id="74711-162">When deploying a client, use the `ChainTrust` value instead.</span></span> <span data-ttu-id="74711-163">您也可以將值設為 `Custom` 或 `None`。</span><span class="sxs-lookup"><span data-stu-id="74711-163">You can also set the value to `Custom` or `None`.</span></span> <span data-ttu-id="74711-164">若要使用 `Custom` 值，您必須同時將 `customCertificateValidator` 屬性 (Attribute) 設為可用來驗證憑證的組件與型別。</span><span class="sxs-lookup"><span data-stu-id="74711-164">To use the `Custom` value, you must also set the `customCertificateValidator` attribute to an assembly and type used to validate the certificate.</span></span> <span data-ttu-id="74711-165">若要建立自己的自訂驗證程式，您必須繼承自抽象 X509CertificateValidator 類別。</span><span class="sxs-lookup"><span data-stu-id="74711-165">To create your own custom validator, you must inherit from the abstract X509CertificateValidator class.</span></span> <span data-ttu-id="74711-166">如需詳細資訊，請參閱[如何：建立採用自訂憑證驗證程式的服務](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)。</span><span class="sxs-lookup"><span data-stu-id="74711-166">For more information, see [How to: Create a Service that Employs a Custom Certificate Validator](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).</span></span>  
  
 <span data-ttu-id="74711-167">`revocationMode` 屬性會指定檢查憑證是否已被撤銷的方法。</span><span class="sxs-lookup"><span data-stu-id="74711-167">The `revocationMode` attribute specifies how certificates are checked for revocation.</span></span> <span data-ttu-id="74711-168">預設為 `online`，表示會自動檢查該憑證是否已被撤銷。</span><span class="sxs-lookup"><span data-stu-id="74711-168">The default is `online` which indicates that certificates will be checked automatically for revocation.</span></span> <span data-ttu-id="74711-169">如需詳細資訊，請參閱[使用憑證](../../../wcf/feature-details/working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="74711-169">For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="74711-170">範例</span><span class="sxs-lookup"><span data-stu-id="74711-170">Example</span></span>  
 <span data-ttu-id="74711-171">下列範例會執行兩個工作。</span><span class="sxs-lookup"><span data-stu-id="74711-171">The following example does two tasks.</span></span> <span data-ttu-id="74711-172">它會先指定服務憑證，讓用戶端在與其功能變數名稱是透過 HTTP 通訊協定的端點進行通訊時使用 `www.contoso.com` 。</span><span class="sxs-lookup"><span data-stu-id="74711-172">It first specifies a service certificate for the client to use when communicating with endpoints whose domain name is `www.contoso.com` over the HTTP protocol.</span></span> <span data-ttu-id="74711-173">第二，指定驗證時使用的撤銷模式和存放區位置。</span><span class="sxs-lookup"><span data-stu-id="74711-173">Second, it specifies the revocation mode and store location used during authentication.</span></span>  
  
```xml  
<serviceCertificate>
  <defaultCertificate findValue="www.contoso.com"
                      storeLocation="LocalMachine"
                      storeName="TrustedPeople"
                      x509FindType="FindByIssuerDistinguishedName" />
  <scopedCertificates>
     <add targetUri="http://www.contoso.com"
          findValue="www.contoso.com"
          storeLocation="LocalMachine"
          storeName="Root"
          x509FindType="FindByIssuerName" />
  </scopedCertificates>
  <authentication revocationMode="Online"
                  trustedStoreLocation="LocalMachine" />
</serviceCertificate>
```  
  
## <a name="see-also"></a><span data-ttu-id="74711-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="74711-174">See also</span></span>

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.Authentication%2A>
- <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>
- [<span data-ttu-id="74711-175">安全性行為</span><span class="sxs-lookup"><span data-stu-id="74711-175">Security Behaviors</span></span>](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [<span data-ttu-id="74711-176">Working with Certificates</span><span class="sxs-lookup"><span data-stu-id="74711-176">Working with Certificates</span></span>](../../../wcf/feature-details/working-with-certificates.md)
- [<span data-ttu-id="74711-177">HOW TO：建立使用自訂憑證驗證程式的服務</span><span class="sxs-lookup"><span data-stu-id="74711-177">How to: Create a Service that Employs a Custom Certificate Validator</span></span>](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [\<authentication>](authentication-of-clientcertificate-element.md)
- [<span data-ttu-id="74711-178">保護用戶端安全</span><span class="sxs-lookup"><span data-stu-id="74711-178">Securing Clients</span></span>](../../../wcf/securing-clients.md)
- [<span data-ttu-id="74711-179">Securing Services and Clients</span><span class="sxs-lookup"><span data-stu-id="74711-179">Securing Services and Clients</span></span>](../../../wcf/feature-details/securing-services-and-clients.md)

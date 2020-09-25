---
title: <authentication> 項目的 <clientCertificate>
ms.date: 03/30/2017
ms.assetid: 4a55eea2-1826-4026-b911-b7cc9e9c8bfe
ms.openlocfilehash: 13296dbc2b3bc8836770197a1549586c841b4635
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201599"
---
# <a name="authentication-of-clientcertificate-element"></a><span data-ttu-id="c78e2-102">\<authentication> 項目的 \<clientCertificate></span><span class="sxs-lookup"><span data-stu-id="c78e2-102">\<authentication> of \<clientCertificate> Element</span></span>

<span data-ttu-id="c78e2-103">指定服務所使用之用戶端憑證的驗證行為。</span><span class="sxs-lookup"><span data-stu-id="c78e2-103">Specifies authentication behaviors for client certificates used by a service.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCertificate>**](clientcertificate-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<authentication>**  
  
## <a name="syntax"></a><span data-ttu-id="c78e2-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="c78e2-104">Syntax</span></span>  
  
```xml  
<authentication customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                includeWindowsGroups="Boolean"
                mapClientCertificateToWindowsAccount="Boolean"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="c78e2-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="c78e2-105">Attributes and Elements</span></span>  

 <span data-ttu-id="c78e2-106">下列各節說明屬性、子元素和父元素</span><span class="sxs-lookup"><span data-stu-id="c78e2-106">The following sections describe attributes, child elements, and parent elements</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="c78e2-107">屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-107">Attributes</span></span>  
  
|<span data-ttu-id="c78e2-108">屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-108">Attribute</span></span>|<span data-ttu-id="c78e2-109">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="c78e2-110">customCertificateValidatorType</span><span class="sxs-lookup"><span data-stu-id="c78e2-110">customCertificateValidatorType</span></span>|<span data-ttu-id="c78e2-111">選擇性字串。</span><span class="sxs-lookup"><span data-stu-id="c78e2-111">Optional string.</span></span> <span data-ttu-id="c78e2-112">用來驗證自訂型別的型別和組件。</span><span class="sxs-lookup"><span data-stu-id="c78e2-112">A type and assembly used to validate a custom type.</span></span> <span data-ttu-id="c78e2-113">當 `certificateValidationMode` 設定為 `Custom` 時，必須設定這個屬性。</span><span class="sxs-lookup"><span data-stu-id="c78e2-113">This attribute must be set when `certificateValidationMode` is set to `Custom`.</span></span>|  
|<span data-ttu-id="c78e2-114">certificateValidationMode</span><span class="sxs-lookup"><span data-stu-id="c78e2-114">certificateValidationMode</span></span>|<span data-ttu-id="c78e2-115">選擇性列舉。</span><span class="sxs-lookup"><span data-stu-id="c78e2-115">Optional enumeration.</span></span> <span data-ttu-id="c78e2-116">指定用來驗證認證的其中一個模式。</span><span class="sxs-lookup"><span data-stu-id="c78e2-116">Specifies one of the modes used to validate credentials.</span></span> <span data-ttu-id="c78e2-117">此屬性的型別為 <xref:System.ServiceModel.Security.X509CertificateValidationMode>。</span><span class="sxs-lookup"><span data-stu-id="c78e2-117">This attribute is of the <xref:System.ServiceModel.Security.X509CertificateValidationMode> type.</span></span> <span data-ttu-id="c78e2-118">如果設定為 <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom?displayProperty=nameWithType>，也必須提供 `customCertificateValidator`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-118">If set to <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom?displayProperty=nameWithType>, then a `customCertificateValidator` must also be supplied.</span></span> <span data-ttu-id="c78e2-119">預設為 <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="c78e2-119">The default is <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust?displayProperty=nameWithType>.</span></span>|  
|<span data-ttu-id="c78e2-120">includeWindowsGroups</span><span class="sxs-lookup"><span data-stu-id="c78e2-120">includeWindowsGroups</span></span>|<span data-ttu-id="c78e2-121">選擇性布林值。</span><span class="sxs-lookup"><span data-stu-id="c78e2-121">Optional Boolean.</span></span> <span data-ttu-id="c78e2-122">指定 Windows 群組是否包含在安全性內容中。</span><span class="sxs-lookup"><span data-stu-id="c78e2-122">Specifies if Windows groups are included in the security context.</span></span> <span data-ttu-id="c78e2-123">將這個屬性設定為 `true` 會有效能方面的影響，因為它會造成完整的群組擴充。</span><span class="sxs-lookup"><span data-stu-id="c78e2-123">Setting this attribute to `true` has a performance impact, as it results in a full group expansion.</span></span> <span data-ttu-id="c78e2-124">如果您不需要建立使用者所屬之群組的清單，請將此屬性設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-124">Set this attribute to `false` if you do not need to establish the list of groups a user belongs to.</span></span>|  
|<span data-ttu-id="c78e2-125">mapClientCertificateToWindowsAccount</span><span class="sxs-lookup"><span data-stu-id="c78e2-125">mapClientCertificateToWindowsAccount</span></span>|<span data-ttu-id="c78e2-126">布林值。</span><span class="sxs-lookup"><span data-stu-id="c78e2-126">Boolean.</span></span> <span data-ttu-id="c78e2-127">指定是否能夠使用憑證將用戶端對應至 Windows 身分識別。</span><span class="sxs-lookup"><span data-stu-id="c78e2-127">Specifies whether the client can be mapped to a Windows identity using the certificate.</span></span> <span data-ttu-id="c78e2-128">必須啟用 Active Directory 才能這麼做。</span><span class="sxs-lookup"><span data-stu-id="c78e2-128">Active Directory must be enabled to do this.</span></span>|  
|<span data-ttu-id="c78e2-129">revocationMode</span><span class="sxs-lookup"><span data-stu-id="c78e2-129">revocationMode</span></span>|<span data-ttu-id="c78e2-130">選擇性列舉。</span><span class="sxs-lookup"><span data-stu-id="c78e2-130">Optional enumeration.</span></span> <span data-ttu-id="c78e2-131">用於檢查撤銷憑證清單 (RCL) 的模式之一。</span><span class="sxs-lookup"><span data-stu-id="c78e2-131">One of the modes used to check for a revoked certificate lists (RCL).</span></span> <span data-ttu-id="c78e2-132">預設值為 `Online`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-132">The default is `Online`.</span></span> <span data-ttu-id="c78e2-133">使用 HTTP 傳輸安全性時，將忽略此值。</span><span class="sxs-lookup"><span data-stu-id="c78e2-133">This value is ignored when using HTTP transport security.</span></span>|  
|<span data-ttu-id="c78e2-134">trustedStoreLocation</span><span class="sxs-lookup"><span data-stu-id="c78e2-134">trustedStoreLocation</span></span>|<span data-ttu-id="c78e2-135">選擇性列舉。</span><span class="sxs-lookup"><span data-stu-id="c78e2-135">Optional enumeration.</span></span> <span data-ttu-id="c78e2-136">兩個系統存放位置的其中一個：`LocalMachine` 或 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-136">One of the two system store locations: `LocalMachine` or `CurrentUser`.</span></span> <span data-ttu-id="c78e2-137">當與用戶端交涉服務憑證時，會使用這個值。</span><span class="sxs-lookup"><span data-stu-id="c78e2-137">This value is used when a service certificate is negotiated to the client.</span></span> <span data-ttu-id="c78e2-138">針對指定存放區位置中 **受信任的人** 存放區執行驗證。</span><span class="sxs-lookup"><span data-stu-id="c78e2-138">Validation is performed against the **Trusted People** store in the specified store location.</span></span> <span data-ttu-id="c78e2-139">預設值為 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-139">The default is `CurrentUser`.</span></span>|  
  
## <a name="customcertificatevalidatortype-attribute"></a><span data-ttu-id="c78e2-140">customCertificateValidatorType 屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-140">customCertificateValidatorType Attribute</span></span>  
  
|<span data-ttu-id="c78e2-141">值</span><span class="sxs-lookup"><span data-stu-id="c78e2-141">Value</span></span>|<span data-ttu-id="c78e2-142">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-142">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="c78e2-143">String</span><span class="sxs-lookup"><span data-stu-id="c78e2-143">String</span></span>|<span data-ttu-id="c78e2-144">指定型別名稱和組件以及用來尋找此型別的其他資料。</span><span class="sxs-lookup"><span data-stu-id="c78e2-144">Specifies the type name and assembly and other data used to find the type.</span></span>|  
  
## <a name="certificatevalidationmode-attribute"></a><span data-ttu-id="c78e2-145">certificateValidationMode 屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-145">certificateValidationMode Attribute</span></span>  
  
|<span data-ttu-id="c78e2-146">值</span><span class="sxs-lookup"><span data-stu-id="c78e2-146">Value</span></span>|<span data-ttu-id="c78e2-147">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-147">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="c78e2-148">列舉型別</span><span class="sxs-lookup"><span data-stu-id="c78e2-148">Enumeration</span></span>|<span data-ttu-id="c78e2-149">下列其中一個值：None、PeerTrust、ChainTrust、PeerOrChainTrust、Custom。</span><span class="sxs-lookup"><span data-stu-id="c78e2-149">One of the following values: None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom.</span></span><br /><br /> <span data-ttu-id="c78e2-150">如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e2-150">For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).</span></span>|  
  
## <a name="revocationmode-attribute"></a><span data-ttu-id="c78e2-151">revocationMode 屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-151">revocationMode Attribute</span></span>  
  
|<span data-ttu-id="c78e2-152">值</span><span class="sxs-lookup"><span data-stu-id="c78e2-152">Value</span></span>|<span data-ttu-id="c78e2-153">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-153">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="c78e2-154">列舉型別</span><span class="sxs-lookup"><span data-stu-id="c78e2-154">Enumeration</span></span>|<span data-ttu-id="c78e2-155">下列其中一個值：NoCheck、Online、Offline。</span><span class="sxs-lookup"><span data-stu-id="c78e2-155">One of the following values: NoCheck, Online, Offline.</span></span> <span data-ttu-id="c78e2-156">如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e2-156">For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).</span></span>|  
  
## <a name="trustedstorelocation-attribute"></a><span data-ttu-id="c78e2-157">trustedStoreLocation 屬性</span><span class="sxs-lookup"><span data-stu-id="c78e2-157">trustedStoreLocation Attribute</span></span>  
  
|<span data-ttu-id="c78e2-158">值</span><span class="sxs-lookup"><span data-stu-id="c78e2-158">Value</span></span>|<span data-ttu-id="c78e2-159">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-159">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="c78e2-160">列舉型別</span><span class="sxs-lookup"><span data-stu-id="c78e2-160">Enumeration</span></span>|<span data-ttu-id="c78e2-161">下列其中一個值：`LocalMachine` 或 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-161">One of the following values: `LocalMachine` or `CurrentUser`.</span></span> <span data-ttu-id="c78e2-162">預設值為 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-162">The default is `CurrentUser`.</span></span> <span data-ttu-id="c78e2-163">如果用戶端應用程式是在系統帳戶下執行，則憑證通常位於 `LocalMachine` 之下。</span><span class="sxs-lookup"><span data-stu-id="c78e2-163">If the client application is running under a system account then the certificate is typically under `LocalMachine`.</span></span> <span data-ttu-id="c78e2-164">如果用戶端應用程式是在使用者帳戶下執行，則憑證通常位於 `CurrentUser`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-164">If the client application is running under a user account then the certificate is typically in `CurrentUser`.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="c78e2-165">子元素</span><span class="sxs-lookup"><span data-stu-id="c78e2-165">Child Elements</span></span>  

 <span data-ttu-id="c78e2-166">無。</span><span class="sxs-lookup"><span data-stu-id="c78e2-166">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="c78e2-167">父項目</span><span class="sxs-lookup"><span data-stu-id="c78e2-167">Parent Elements</span></span>  
  
|<span data-ttu-id="c78e2-168">項目</span><span class="sxs-lookup"><span data-stu-id="c78e2-168">Element</span></span>|<span data-ttu-id="c78e2-169">描述</span><span class="sxs-lookup"><span data-stu-id="c78e2-169">Description</span></span>|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-servicecredentials.md)|<span data-ttu-id="c78e2-170">定義用於向服務驗證的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="c78e2-170">Defines an X.509 certificate used to authenticate a client to a service.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c78e2-171">備註</span><span class="sxs-lookup"><span data-stu-id="c78e2-171">Remarks</span></span>  

 <span data-ttu-id="c78e2-172">`<authentication>` 項目對應至 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 類別。</span><span class="sxs-lookup"><span data-stu-id="c78e2-172">The `<authentication>` element corresponds to the <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> class.</span></span> <span data-ttu-id="c78e2-173">它可讓您自訂驗證用戶端的方法。</span><span class="sxs-lookup"><span data-stu-id="c78e2-173">It enables you to customize how clients are authenticated.</span></span> <span data-ttu-id="c78e2-174">您可以將 `certificateValidationMode` 屬性 (Attribute) 設定為 `None`、`ChainTrust`、`PeerOrChainTrust`、`PeerTrust` 或 `Custom`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-174">You can set the `certificateValidationMode` attribute to `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust`, or `Custom`.</span></span> <span data-ttu-id="c78e2-175">根據預設，層級會設為 `ChainTrust` ，指定每個憑證都必須在鏈頂端以 *根授權* 單位結尾的憑證階層中找到。</span><span class="sxs-lookup"><span data-stu-id="c78e2-175">By default, the level is set to `ChainTrust`, which specifies that each certificate must be found in a hierarchy of certificates ending in a *root authority* at the top of the chain.</span></span> <span data-ttu-id="c78e2-176">這是最安全的模式。</span><span class="sxs-lookup"><span data-stu-id="c78e2-176">This is the most secure mode.</span></span> <span data-ttu-id="c78e2-177">您也可以將值設定為 `PeerOrChainTrust`，指定可接受自行發出的憑證 (對等信任)，以及信任鏈結內的憑證。</span><span class="sxs-lookup"><span data-stu-id="c78e2-177">You can also set the value to `PeerOrChainTrust`, which specifies that self-issued certificates (peer trust) are accepted as well as certificates that are in a trusted chain.</span></span> <span data-ttu-id="c78e2-178">這個值會在開發及偵錯用戶端和服務時使用，因為自行發出的憑證不需要從受信任的授權單位購買。</span><span class="sxs-lookup"><span data-stu-id="c78e2-178">This value is used when developing and debugging clients and services because self-issued certificates need not be purchased from a trusted authority.</span></span> <span data-ttu-id="c78e2-179">部署用戶端時，請改用 `ChainTrust` 值。</span><span class="sxs-lookup"><span data-stu-id="c78e2-179">When deploying a client, use the `ChainTrust` value instead.</span></span>  
  
 <span data-ttu-id="c78e2-180">您也可以將值設定為 `Custom`。</span><span class="sxs-lookup"><span data-stu-id="c78e2-180">You can also set the value to `Custom`.</span></span> <span data-ttu-id="c78e2-181">設定為 `Custom` 值時，您還必須將 `customCertificateValidatorType` 屬性設定為可用來驗證憑證的組件與型別。</span><span class="sxs-lookup"><span data-stu-id="c78e2-181">When set to the `Custom` value, you must also set the `customCertificateValidatorType` attribute to an assembly and type used to validate the certificate.</span></span> <span data-ttu-id="c78e2-182">若要建立自己的自訂驗證程式，您必須繼承自抽象 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 類別。</span><span class="sxs-lookup"><span data-stu-id="c78e2-182">To create your own custom validator, you must inherit from the abstract <xref:System.IdentityModel.Selectors.X509CertificateValidator> class.</span></span> <span data-ttu-id="c78e2-183">如需詳細資訊，請參閱 [如何：建立採用自訂憑證驗證程式的服務](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e2-183">For more information, see [How to: Create a Service that Employs a Custom Certificate Validator](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="c78e2-184">範例</span><span class="sxs-lookup"><span data-stu-id="c78e2-184">Example</span></span>  

 <span data-ttu-id="c78e2-185">下列程式碼會在 `<authentication>` 項目中指定 X.509 憑證和自訂驗證類型。</span><span class="sxs-lookup"><span data-stu-id="c78e2-185">The following code specifies an X.509 certificate and a custom validation type in the `<authentication>` element.</span></span>  
  
```xml  
<serviceBehaviors>
  <behavior name="myServiceBehavior">
    <clientCertificate>
      <certificate findValue="www.cohowinery.com"
                   storeLocation="CurrentUser"
                   storeName="TrustedPeople"
                   x509FindType="FindByIssuerName" />
      <authentication customCertificateValidatorType="MyTypes.Coho"
                      certificateValidationMode="Custom"
                      revocationMode="Offline"
                      includeWindowsGroups="false"
                      mapClientCertificateToWindowsAccount="true" />
    </clientCertificate>
  </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a><span data-ttu-id="c78e2-186">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c78e2-186">See also</span></span>

- <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>
- <xref:System.ServiceModel.Security.X509CertificateValidationMode>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509ClientCertificateAuthenticationElement>
- [<span data-ttu-id="c78e2-187">安全性行為</span><span class="sxs-lookup"><span data-stu-id="c78e2-187">Security Behaviors</span></span>](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [<span data-ttu-id="c78e2-188">作法：建立使用自訂憑證驗證程式的服務</span><span class="sxs-lookup"><span data-stu-id="c78e2-188">How to: Create a Service that Employs a Custom Certificate Validator</span></span>](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [<span data-ttu-id="c78e2-189">使用憑證</span><span class="sxs-lookup"><span data-stu-id="c78e2-189">Working with Certificates</span></span>](../../../wcf/feature-details/working-with-certificates.md)

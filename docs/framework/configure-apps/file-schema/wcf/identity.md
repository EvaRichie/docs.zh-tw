---
title: <identity>
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: 15c9e38a141fc294c47863b1a932711444ac079a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855148"
---
# \<identity>
<span data-ttu-id="9d290-101">身分識別項目允許用戶端開發人員在設計階段指定服務的預期身分識別。</span><span class="sxs-lookup"><span data-stu-id="9d290-101">The identity element allows a client developer to specify at design time the expected identity of the service.</span></span> <span data-ttu-id="9d290-102">在用戶端和服務之間的交握程式中，Windows Communication Foundation （WCF）基礎結構將確保預期服務的身分識別符合此元素的值，因此可以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9d290-102">In the handshake process between the client and service, the Windows Communication Foundation (WCF) infrastructure will ensure that the identity of the expected service matches the values of this element, and thus can be authenticated.</span></span> <span data-ttu-id="9d290-103">如需詳細資訊，請參閱[服務身分識別和驗證](../../../wcf/feature-details/service-identity-and-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="9d290-103">For more information, see [Service Identity and Authentication](../../../wcf/feature-details/service-identity-and-authentication.md).</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<identity>**  
  
## <a name="syntax"></a><span data-ttu-id="9d290-104">語法</span><span class="sxs-lookup"><span data-stu-id="9d290-104">Syntax</span></span>  
  
```xml  
<identity>
  <certificate encodedValue="String" />
  <certificateReference findValue="String"
                        isChainIncluded="Boolean"
                        storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                        storeLocation="LocalMachine/CurrentUser"
                        X509FindType="Enumeration" />
  <dns value="String" />
  <rsa value="String" />
  <servicePrincipalName value="String" />
  <userPrincipalName value="String" />
</identity>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="9d290-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="9d290-105">Attributes and Elements</span></span>  
 <span data-ttu-id="9d290-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="9d290-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="9d290-107">屬性</span><span class="sxs-lookup"><span data-stu-id="9d290-107">Attributes</span></span>  
 <span data-ttu-id="9d290-108">無。</span><span class="sxs-lookup"><span data-stu-id="9d290-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="9d290-109">子元素</span><span class="sxs-lookup"><span data-stu-id="9d290-109">Child Elements</span></span>  
  
|<span data-ttu-id="9d290-110">元素</span><span class="sxs-lookup"><span data-stu-id="9d290-110">Element</span></span>|<span data-ttu-id="9d290-111">描述</span><span class="sxs-lookup"><span data-stu-id="9d290-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="9d290-112">憑證 (certificate)</span><span class="sxs-lookup"><span data-stu-id="9d290-112">certificate</span></span>|<span data-ttu-id="9d290-113">指定 X.509 憑證的設定。</span><span class="sxs-lookup"><span data-stu-id="9d290-113">Specifies settings of an X.509 certificate.</span></span> <span data-ttu-id="9d290-114">此項目的型別為 <xref:System.ServiceModel.Configuration.CertificateElement>。</span><span class="sxs-lookup"><span data-stu-id="9d290-114">This element is of type <xref:System.ServiceModel.Configuration.CertificateElement>.</span></span> <span data-ttu-id="9d290-115">它包含是字串的屬性 `encodedValue`，指定由此憑證編碼的值。</span><span class="sxs-lookup"><span data-stu-id="9d290-115">It contains an attribute `encodedValue` that is a string, which specifies the value encoded by this certificate.</span></span>|  
|<span data-ttu-id="9d290-116">certificateReference</span><span class="sxs-lookup"><span data-stu-id="9d290-116">certificateReference</span></span>|<span data-ttu-id="9d290-117">指定 X.509 憑證驗證的設定。</span><span class="sxs-lookup"><span data-stu-id="9d290-117">Specifies settings for X.509 certificate validation.</span></span> <span data-ttu-id="9d290-118">此項目的型別為 <xref:System.ServiceModel.Configuration.CertificateReferenceElement>。</span><span class="sxs-lookup"><span data-stu-id="9d290-118">This element is of type <xref:System.ServiceModel.Configuration.CertificateReferenceElement>.</span></span>|  
|<span data-ttu-id="9d290-119">dns</span><span class="sxs-lookup"><span data-stu-id="9d290-119">dns</span></span>|<span data-ttu-id="9d290-120">指定用來驗證服務之 X.509 憑證的 DNS。</span><span class="sxs-lookup"><span data-stu-id="9d290-120">Specifies the DNS of an X.509 certificate used to authenticate a service.</span></span> <span data-ttu-id="9d290-121">這個項目包含是字串的屬性 `value`，而且包含實際的身分識別。</span><span class="sxs-lookup"><span data-stu-id="9d290-121">This element contains an attribute `value` that is a string, and contains the actual identity.</span></span>|  
|<span data-ttu-id="9d290-122">rsa</span><span class="sxs-lookup"><span data-stu-id="9d290-122">rsa</span></span>|<span data-ttu-id="9d290-123">指定 X.509 憑證的 RSA 欄位值，此憑證可用來驗證用戶端的服務。</span><span class="sxs-lookup"><span data-stu-id="9d290-123">Specifies the value of the RSA field of an X.509 certificate used to authenticate a service to a client.</span></span> <span data-ttu-id="9d290-124">這個項目包含是字串的屬性 `value`，而且包含實際的身分識別。</span><span class="sxs-lookup"><span data-stu-id="9d290-124">This element contains an attribute `value` that is a string, and contains the actual identity</span></span>|  
|<span data-ttu-id="9d290-125">servicePrincipalName</span><span class="sxs-lookup"><span data-stu-id="9d290-125">servicePrincipalName</span></span>|<span data-ttu-id="9d290-126">指定伺服器主要名稱 (SPN) 身分識別，也就是用戶端可唯一識別服務執行個體時所用的主要名稱。</span><span class="sxs-lookup"><span data-stu-id="9d290-126">Specifies a server principal name (SPN) identity, which is the principal name used by a client to uniquely identify an instance of a service.</span></span> <span data-ttu-id="9d290-127">這個項目包含是字串的屬性 `value`，而且包含實際的主要名稱。</span><span class="sxs-lookup"><span data-stu-id="9d290-127">This element contains an attribute `value` that is a string, and contains the actual principal name.</span></span> <span data-ttu-id="9d290-128">此項目的型別為 <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement>。</span><span class="sxs-lookup"><span data-stu-id="9d290-128">This element is of type <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement>.</span></span>|  
|<span data-ttu-id="9d290-129">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="9d290-129">userPrincipalName</span></span>|<span data-ttu-id="9d290-130">指定使用者主要名稱 (UPN) 身分識別，也就是網路上使用者的登入名稱類型。</span><span class="sxs-lookup"><span data-stu-id="9d290-130">Specifies a user principal name (UPN) identity, which is the logon name type of a user on a network.</span></span> <span data-ttu-id="9d290-131">使用者主體名稱包含 Active Directory 中使用的使用者物件名稱，後面接著 at 符號（ \@ ），然後通常是網域名稱系統父系網域。</span><span class="sxs-lookup"><span data-stu-id="9d290-131">The user principal name consists of the user object name used in Active Directory, followed by the at symbol (\@) and then, typically, the Domain Name System parent domain.</span></span> <span data-ttu-id="9d290-132">例如，Fabrikam.com 網域樹狀結構中的 Jeff 可能會有使用者主體名稱 [jeff@fabrikam.com](mailto:jeffsmith@fabrikam.com) 。</span><span class="sxs-lookup"><span data-stu-id="9d290-132">For example, Jeff in the Fabrikam.com domain tree might have the user principal name [jeff@fabrikam.com](mailto:jeffsmith@fabrikam.com).</span></span>  <span data-ttu-id="9d290-133">這個項目包含是字串的屬性 `value`，而且包含實際的主要名稱。</span><span class="sxs-lookup"><span data-stu-id="9d290-133">This element contains an attribute `value` that is a string, and contains the actual principal name.</span></span> <span data-ttu-id="9d290-134">此項目的型別為 <xref:System.ServiceModel.Configuration.UserPrincipalNameElement>。</span><span class="sxs-lookup"><span data-stu-id="9d290-134">This element is of type <xref:System.ServiceModel.Configuration.UserPrincipalNameElement>.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="9d290-135">父項目</span><span class="sxs-lookup"><span data-stu-id="9d290-135">Parent Elements</span></span>  
  
|<span data-ttu-id="9d290-136">元素</span><span class="sxs-lookup"><span data-stu-id="9d290-136">Element</span></span>|<span data-ttu-id="9d290-137">描述</span><span class="sxs-lookup"><span data-stu-id="9d290-137">Description</span></span>|  
|-------------|-----------------|  
|[\<custom>](custom.md)|<span data-ttu-id="9d290-138">指定 netPeerTcpBinding 的自訂對等解析程式。</span><span class="sxs-lookup"><span data-stu-id="9d290-138">Specifies a custom peer resolver for a netPeerTcpBinding.</span></span>|  
|[\<endpoint>](endpoint-element.md)|<span data-ttu-id="9d290-139">設定服務端點。</span><span class="sxs-lookup"><span data-stu-id="9d290-139">Configures service endpoints.</span></span>|  
|[<span data-ttu-id="9d290-140">\<endpoint>的\<client></span><span class="sxs-lookup"><span data-stu-id="9d290-140">\<endpoint> of \<client></span></span>](endpoint-of-client.md)|<span data-ttu-id="9d290-141">設定通道端點。</span><span class="sxs-lookup"><span data-stu-id="9d290-141">Configures channel endpoints.</span></span>|  
|[\<issuer>](issuer.md)|<span data-ttu-id="9d290-142">指定聯合服務的安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="9d290-142">Specifies the Security Token Service (STS) for the federated service.</span></span>|  
|[\<issuerMetadata>](issuermetadata.md)|<span data-ttu-id="9d290-143">為聯合服務的安全性權杖服務 (STS) 指定中繼資料端點。</span><span class="sxs-lookup"><span data-stu-id="9d290-143">Specifies the metadata endpoint for the Security Token Service (STS) of a federated service.</span></span>|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|<span data-ttu-id="9d290-144">定義自訂繫結中已發行權杖的參數。</span><span class="sxs-lookup"><span data-stu-id="9d290-144">Defines parameters for an issued token in a custom binding.</span></span>|  
|[\<localIssuer>](localissuer.md)|<span data-ttu-id="9d290-145">指定本機安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="9d290-145">Specifies a local Security Token Service (STS).</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="9d290-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9d290-146">See also</span></span>

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- [<span data-ttu-id="9d290-147">服務身分識別和驗證</span><span class="sxs-lookup"><span data-stu-id="9d290-147">Service Identity and Authentication</span></span>](../../../wcf/feature-details/service-identity-and-authentication.md)
- [<span data-ttu-id="9d290-148">端點：位址、繫結和合約</span><span class="sxs-lookup"><span data-stu-id="9d290-148">Endpoints: Addresses, Bindings, and Contracts</span></span>](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)

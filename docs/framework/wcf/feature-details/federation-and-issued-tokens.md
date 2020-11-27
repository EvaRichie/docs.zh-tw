---
title: 聯合與發行的權杖
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, federation
- issued tokens [WCF]
- federation [WCF], issued tokens
ms.assetid: 4c31ee7d-a820-4067-8b84-a83049021bb6
ms.openlocfilehash: 0ab3d6bad717e71901b4d94c99f1c48f99d8675e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96255516"
---
# <a name="federation-and-issued-tokens"></a><span data-ttu-id="c1c80-102">聯合與發行的權杖</span><span class="sxs-lookup"><span data-stu-id="c1c80-102">Federation and Issued Tokens</span></span>

<span data-ttu-id="c1c80-103">使用 WCF) 的 Windows Communication Foundation (，您可以建立用戶端，以安全地與執行 WS-Federation 和 WS-Trust 規格的服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c1c80-103">With Windows Communication Foundation (WCF), you can create clients that communicate securely with services that implement the WS-Federation and WS-Trust specifications.</span></span> <span data-ttu-id="c1c80-104">這些規格使用 XML、SOAP 和 Web 服務描述語言 (WSDL)，提供跨不同信任領域的驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="c1c80-104">The specifications use XML, SOAP, and Web Services Description Language (WSDL) to provide mechanisms that enable authentication and authorization across different trust realms.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="c1c80-105">本節內容</span><span class="sxs-lookup"><span data-stu-id="c1c80-105">In This Section</span></span>  

 [<span data-ttu-id="c1c80-106">同盟</span><span class="sxs-lookup"><span data-stu-id="c1c80-106">Federation</span></span>](federation.md)  
 <span data-ttu-id="c1c80-107">提供聯合的概觀。</span><span class="sxs-lookup"><span data-stu-id="c1c80-107">Provides an overview of federation.</span></span>  
  
 [<span data-ttu-id="c1c80-108">聯合與信任</span><span class="sxs-lookup"><span data-stu-id="c1c80-108">Federation and Trust</span></span>](federation-and-trust.md)  
 <span data-ttu-id="c1c80-109">列出建立聯合服務或用戶端時應注意的設計問題。</span><span class="sxs-lookup"><span data-stu-id="c1c80-109">Lists the design issues to be aware of when creating federated services or clients.</span></span>  
  
 [<span data-ttu-id="c1c80-110">作法：建立同盟用戶端</span><span class="sxs-lookup"><span data-stu-id="c1c80-110">How to: Create a Federated Client</span></span>](how-to-create-a-federated-client.md)  
 <span data-ttu-id="c1c80-111">描述使用 WCF 建立同盟用戶端的基本概念。</span><span class="sxs-lookup"><span data-stu-id="c1c80-111">Describes the basics of creating a federated client with WCF.</span></span>  
  
 [<span data-ttu-id="c1c80-112">作法：設定同盟服務的認證</span><span class="sxs-lookup"><span data-stu-id="c1c80-112">How to: Configure Credentials on a Federation Service</span></span>](how-to-configure-credentials-on-a-federation-service.md)  
 <span data-ttu-id="c1c80-113">說明建立聯盟服務的步驟。</span><span class="sxs-lookup"><span data-stu-id="c1c80-113">Describes the steps of creating a federated service.</span></span>  
  
 [<span data-ttu-id="c1c80-114">作法：建立 WSFederationHttpBinding</span><span class="sxs-lookup"><span data-stu-id="c1c80-114">How to: Create a WSFederationHttpBinding</span></span>](how-to-create-a-wsfederationhttpbinding.md)  
 <span data-ttu-id="c1c80-115">說明如何設定使用 `WSFederationHttpBinding` 的用戶端和服務。</span><span class="sxs-lookup"><span data-stu-id="c1c80-115">Describes how to configure clients and services that use the `WSFederationHttpBinding`.</span></span>  
  
 [<span data-ttu-id="c1c80-116">作法：建立安全性權杖服務</span><span class="sxs-lookup"><span data-stu-id="c1c80-116">How to: Create a Security Token Service</span></span>](how-to-create-a-security-token-service.md)  
 <span data-ttu-id="c1c80-117">說明建立安全性權杖服務的步驟。</span><span class="sxs-lookup"><span data-stu-id="c1c80-117">Describes the steps of creating a security token service.</span></span>  
  
 [<span data-ttu-id="c1c80-118">安全性判斷提示標記語言 (SAML) 權杖與宣告</span><span class="sxs-lookup"><span data-stu-id="c1c80-118">Security Assertions Markup Language (SAML) Tokens and Claims</span></span>](saml-tokens-and-claims.md)  
 <span data-ttu-id="c1c80-119">說明 Security Assertions Markup Language (SAML) 權杖，這是一個可擴充，並且可讓您建立豐富之宣告類型的權杖。</span><span class="sxs-lookup"><span data-stu-id="c1c80-119">Describes Security Assertions Markup Language (SAML) tokens, which are extensible and enable you to create rich claim types.</span></span>  
  
 [<span data-ttu-id="c1c80-120">作法：設定本機簽發者</span><span class="sxs-lookup"><span data-stu-id="c1c80-120">How to: Configure a Local Issuer</span></span>](how-to-configure-a-local-issuer.md)  
 <span data-ttu-id="c1c80-121">說明如何建立安全性權杖的本機簽發者。</span><span class="sxs-lookup"><span data-stu-id="c1c80-121">Describes how to create a local issuer of security tokens.</span></span>  
  
 [<span data-ttu-id="c1c80-122">作法：在 WSFederationHttpBinding 上停用安全工作階段</span><span class="sxs-lookup"><span data-stu-id="c1c80-122">How to: Disable Secure Sessions on a WSFederationHttpBinding</span></span>](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 <span data-ttu-id="c1c80-123">說明如何停用 `WSFederationHttpBinding` 上的安全工作階段。</span><span class="sxs-lookup"><span data-stu-id="c1c80-123">Describes how to disable secure sessions on a `WSFederationHttpBinding`.</span></span> <span data-ttu-id="c1c80-124">在建立要求每個用戶端都使用一個工作階段的 Web 伺服陣列時，必須停用安全工作階段。</span><span class="sxs-lookup"><span data-stu-id="c1c80-124">Disabling secure sessions is necessary when creating a Web farm that requires a session for each client.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="c1c80-125">參考</span><span class="sxs-lookup"><span data-stu-id="c1c80-125">Reference</span></span>  

 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>  
  
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenProvider>  
  
 <xref:System.ServiceModel.WSFederationHttpBinding>  
  
## <a name="see-also"></a><span data-ttu-id="c1c80-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c1c80-126">See also</span></span>

- [<span data-ttu-id="c1c80-127">授權</span><span class="sxs-lookup"><span data-stu-id="c1c80-127">Authorization</span></span>](authorization-in-wcf.md)
- [<span data-ttu-id="c1c80-128">自訂權杖</span><span class="sxs-lookup"><span data-stu-id="c1c80-128">Custom Tokens</span></span>](../extending/custom-tokens.md)
- <span data-ttu-id="c1c80-129">[Windows Server AppFabric 的資訊安全模型](/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="c1c80-129">[Security Model for Windows Server App Fabric](/previous-versions/appfabric/ee677202(v=azure.10))</span></span>

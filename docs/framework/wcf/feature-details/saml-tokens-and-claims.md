---
title: SAML 權杖與宣告
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
- issued tokens
- SAML token
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
ms.openlocfilehash: 6220365d5c43299a75d1e0fa8e46a7392b0ccaa2
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590367"
---
# <a name="saml-tokens-and-claims"></a><span data-ttu-id="b4509-102">SAML 權杖與宣告</span><span class="sxs-lookup"><span data-stu-id="b4509-102">SAML Tokens and Claims</span></span>
<span data-ttu-id="b4509-103">安全性判斷提示標記語言（SAML）*權杖*是宣告的 XML 標記法。</span><span class="sxs-lookup"><span data-stu-id="b4509-103">Security Assertions Markup Language (SAML) *tokens* are XML representations of claims.</span></span> <span data-ttu-id="b4509-104">根據預設，在同盟安全性案例中使用的 SAML 權杖 Windows Communication Foundation （WCF）會*發行權杖*。</span><span class="sxs-lookup"><span data-stu-id="b4509-104">By default, SAML tokens Windows Communication Foundation (WCF) uses in federated security scenarios are *issued tokens*.</span></span>  
  
 <span data-ttu-id="b4509-105">SAML 權杖包含一實體對另一實體所做出之宣告集合的陳述式。</span><span class="sxs-lookup"><span data-stu-id="b4509-105">SAML tokens carry statements that are sets of claims made by one entity about another entity.</span></span> <span data-ttu-id="b4509-106">例如，在聯合安全性案例中，陳述式是由系統中關於使用者的安全性權杖服務所表示。</span><span class="sxs-lookup"><span data-stu-id="b4509-106">For example, in federated security scenarios, the statements are made by a security token service about a user in the system.</span></span> <span data-ttu-id="b4509-107">安全性權杖服務會簽署 SAML 權杖，以表示權杖中所含陳述式的真實性。</span><span class="sxs-lookup"><span data-stu-id="b4509-107">The security token service signs the SAML token to indicate the veracity of the statements contained in the token.</span></span> <span data-ttu-id="b4509-108">除此之外，SAML 權杖會與 SAML 權杖使用者證實知悉的密碼編譯金鑰內容產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b4509-108">In addition, the SAML token is associated with cryptographic key material that the user of the SAML token proves knowledge of.</span></span> <span data-ttu-id="b4509-109">這項證明能滿足信賴憑證者，證實該 SAML 權杖確實簽發至該使用者。</span><span class="sxs-lookup"><span data-stu-id="b4509-109">This proof satisfies the relying party that the SAML token was, in fact, issued to that user.</span></span> <span data-ttu-id="b4509-110">例如，在典型的案例中：</span><span class="sxs-lookup"><span data-stu-id="b4509-110">For example, in a typical scenario:</span></span>  
  
1. <span data-ttu-id="b4509-111">用戶端向安全性權杖服務要求 SAML 權杖，藉由使用 Windows 認證，驗證至該安全性權杖服務。</span><span class="sxs-lookup"><span data-stu-id="b4509-111">A client requests a SAML token from a security token service, authenticating to that security token service by using Windows credentials.</span></span>  
  
2. <span data-ttu-id="b4509-112">安全性權杖服務簽發 SAML 權杖至用戶端。</span><span class="sxs-lookup"><span data-stu-id="b4509-112">The security token service issues a SAML token to the client.</span></span> <span data-ttu-id="b4509-113">SAML 權杖是以與安全性權杖服務相關的憑證進行簽署，並且包含針對目標服務加密的證明金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4509-113">The SAML token is signed with a certificate associated with the security token service and contains a proof key encrypted for the target service.</span></span>  
  
3. <span data-ttu-id="b4509-114">用戶端也會收到*證明金鑰*的複本。</span><span class="sxs-lookup"><span data-stu-id="b4509-114">The client also receives a copy of the *proof key*.</span></span> <span data-ttu-id="b4509-115">然後，用戶端會向應用程式服務（*信賴*憑證者）出示 SAML 權杖，並使用該證明金鑰來簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="b4509-115">The client then presents the SAML token to the application service (the *relying party*) and signs the message with that proof key.</span></span>  
  
4. <span data-ttu-id="b4509-116">SAML 權杖上的簽章會告訴信賴憑證者，這是由安全性權杖服務所簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="b4509-116">The signature over the SAML token tells the relying party that the security token service issued the token.</span></span> <span data-ttu-id="b4509-117">使用證明金鑰所建立的訊息簽章會告訴信賴憑證者，該權杖曾簽發至用戶端。</span><span class="sxs-lookup"><span data-stu-id="b4509-117">The message signature created with the proof key tells the relying party that the token was issued to the client.</span></span>  
  
## <a name="from-claims-to-samlattributes"></a><span data-ttu-id="b4509-118">從宣告到 SamlAttributes</span><span class="sxs-lookup"><span data-stu-id="b4509-118">From Claims to SamlAttributes</span></span>  
 <span data-ttu-id="b4509-119">在 WCF 中，SAML 權杖中的語句會模型化為 <xref:System.IdentityModel.Tokens.SamlAttribute> 物件， <xref:System.IdentityModel.Claims.Claim> 如果 <xref:System.IdentityModel.Claims.Claim> 物件具有 <xref:System.IdentityModel.Claims.Claim.Right%2A> 的屬性為 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> ，且 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 屬性的類型為 <xref:System.String> ，則可以直接從物件填入。</span><span class="sxs-lookup"><span data-stu-id="b4509-119">In WCF, statements in SAML tokens are modeled as <xref:System.IdentityModel.Tokens.SamlAttribute> objects, which can be populated directly from <xref:System.IdentityModel.Claims.Claim> objects, provided the <xref:System.IdentityModel.Claims.Claim> object has a <xref:System.IdentityModel.Claims.Claim.Right%2A> property of <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> and the <xref:System.IdentityModel.Claims.Claim.Resource%2A> property is of type <xref:System.String>.</span></span> <span data-ttu-id="b4509-120">例如：</span><span class="sxs-lookup"><span data-stu-id="b4509-120">For example:</span></span>  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
> <span data-ttu-id="b4509-121">當 SAML 權杖在訊息中序列化，不論是當這些權杖是安全性權杖服務所核發，或是當這些權杖由用戶端視為驗證的一部分提供至服務，訊息大小配額上限必須大到足以容納 SAML 權杖及其他訊息部分。</span><span class="sxs-lookup"><span data-stu-id="b4509-121">When SAML tokens are serialized in messages, either when they are issued by a security token service or when they are presented by clients to services as part of authentication, the maximum message size quota must be sufficiently large to accommodate the SAML token and the other message parts.</span></span> <span data-ttu-id="b4509-122">正常情況下，預設訊息大小配額應足夠。</span><span class="sxs-lookup"><span data-stu-id="b4509-122">In normal cases, the default message size quotas are sufficient.</span></span> <span data-ttu-id="b4509-123">然而，若 SAML 權杖因為包含數百個宣告而變很大時，您可能需要增加配額以容納序列化的權杖。</span><span class="sxs-lookup"><span data-stu-id="b4509-123">However, in cases where a SAML token is large because it contains hundreds of claims, you may need to increase the quotas to accommodate the serialized token.</span></span> <span data-ttu-id="b4509-124">如需詳細資訊，請參閱[資料的安全性考慮](security-considerations-for-data.md)。</span><span class="sxs-lookup"><span data-stu-id="b4509-124">For more information, see [Security Considerations for Data](security-considerations-for-data.md).</span></span>  
  
## <a name="from-samlattributes-to-claims"></a><span data-ttu-id="b4509-125">從 SamlAttributes 到宣告</span><span class="sxs-lookup"><span data-stu-id="b4509-125">From SamlAttributes to Claims</span></span>  
 <span data-ttu-id="b4509-126">當 SAML 權杖在訊息內接收時，SAML 權杖內的各種陳述式會轉變成  物件，置於 之內。</span><span class="sxs-lookup"><span data-stu-id="b4509-126">When SAML tokens are received in messages, the various statements in the SAML token are turned into <xref:System.IdentityModel.Policy.IAuthorizationPolicy> objects that are placed into the <xref:System.IdentityModel.Policy.AuthorizationContext>.</span></span> <span data-ttu-id="b4509-127">來自每個 SAML 陳述式的宣告均由 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> 的 <xref:System.IdentityModel.Policy.AuthorizationContext> 屬性傳回，並且可進行檢查以決定是否驗證並授權使用者。</span><span class="sxs-lookup"><span data-stu-id="b4509-127">The claims from each SAML statement are returned by the <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> property of the <xref:System.IdentityModel.Policy.AuthorizationContext> and can be examined to determine whether to authenticate and authorize the user.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b4509-128">請參閱</span><span class="sxs-lookup"><span data-stu-id="b4509-128">See also</span></span>

- <xref:System.IdentityModel.Policy.AuthorizationContext>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [<span data-ttu-id="b4509-129">同盟</span><span class="sxs-lookup"><span data-stu-id="b4509-129">Federation</span></span>](federation.md)
- [<span data-ttu-id="b4509-130">如何：建立同盟用戶端</span><span class="sxs-lookup"><span data-stu-id="b4509-130">How to: Create a Federated Client</span></span>](how-to-create-a-federated-client.md)
- [<span data-ttu-id="b4509-131">HOW TO：設定聯合服務的認證</span><span class="sxs-lookup"><span data-stu-id="b4509-131">How to: Configure Credentials on a Federation Service</span></span>](how-to-configure-credentials-on-a-federation-service.md)
- [<span data-ttu-id="b4509-132">使用身分識別模型來管理宣告與授權</span><span class="sxs-lookup"><span data-stu-id="b4509-132">Managing Claims and Authorization with the Identity Model</span></span>](managing-claims-and-authorization-with-the-identity-model.md)
- [<span data-ttu-id="b4509-133">宣告與權杖</span><span class="sxs-lookup"><span data-stu-id="b4509-133">Claims and Tokens</span></span>](claims-and-tokens.md)
- [<span data-ttu-id="b4509-134">宣告建立與資源值</span><span class="sxs-lookup"><span data-stu-id="b4509-134">Claim Creation and Resource Values</span></span>](claim-creation-and-resource-values.md)
- [<span data-ttu-id="b4509-135">HOW TO：建立自訂宣告</span><span class="sxs-lookup"><span data-stu-id="b4509-135">How to: Create a Custom Claim</span></span>](../extending/how-to-create-a-custom-claim.md)

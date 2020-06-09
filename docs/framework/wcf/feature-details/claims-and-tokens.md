---
title: 宣告與權杖
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], and tokens
ms.assetid: eff167f3-33f8-483d-a950-aa3e9f97a189
ms.openlocfilehash: cbc97f2224bce640757e1cef88fe325db477cfd7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587023"
---
# <a name="claims-and-tokens"></a><span data-ttu-id="d40ff-102">宣告與權杖</span><span class="sxs-lookup"><span data-stu-id="d40ff-102">Claims and Tokens</span></span>

<span data-ttu-id="d40ff-103">本主題描述 Windows Communication Foundation （WCF）從其支援的預設權杖建立的各種宣告類型。</span><span class="sxs-lookup"><span data-stu-id="d40ff-103">This topic describes the various claim types that Windows Communication Foundation (WCF) creates from the default tokens that it supports.</span></span>

<span data-ttu-id="d40ff-104">您可以使用 <xref:System.IdentityModel.Claims.ClaimSet> 和 <xref:System.IdentityModel.Claims.Claim> 類別來檢查用戶端認證的宣告。</span><span class="sxs-lookup"><span data-stu-id="d40ff-104">You can examine the claims of a client credential by using the <xref:System.IdentityModel.Claims.ClaimSet> and <xref:System.IdentityModel.Claims.Claim> classes.</span></span> <span data-ttu-id="d40ff-105">`ClaimSet` 包含 `Claim` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="d40ff-105">The `ClaimSet` contains a collection of `Claim` objects.</span></span> <span data-ttu-id="d40ff-106">每個 `Claim` 都具有下列重要的成員：</span><span class="sxs-lookup"><span data-stu-id="d40ff-106">Each `Claim` has the following important members:</span></span>

- <span data-ttu-id="d40ff-107"><xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 屬性會傳回指定所要建立之宣告類型的統一資源識別元 (URI)。</span><span class="sxs-lookup"><span data-stu-id="d40ff-107">The <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> property returns a Uniform Resource Identifier (URI) that specifies the type of claim being made.</span></span> <span data-ttu-id="d40ff-108">例如，宣告類型可能是憑證的指紋，在此情況下，URI 為 `http://schemas.microsoft.com/ws/20005/05/identity/claims/thumprint` 。</span><span class="sxs-lookup"><span data-stu-id="d40ff-108">For example, a claim type may be a thumbprint of a certificate, in which case the URI is `http://schemas.microsoft.com/ws/20005/05/identity/claims/thumprint`.</span></span>

- <span data-ttu-id="d40ff-109"><xref:System.IdentityModel.Claims.Claim.Right%2A> 屬性會傳回指定宣告權限的 URI。</span><span class="sxs-lookup"><span data-stu-id="d40ff-109">The <xref:System.IdentityModel.Claims.Claim.Right%2A> property returns a URI that specifies the right of the claim.</span></span> <span data-ttu-id="d40ff-110">預先定義的權限可以在 <xref:System.IdentityModel.Claims.Rights> 類別中找到 (<xref:System.IdentityModel.Claims.Rights.Identity%2A>、<xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>)。</span><span class="sxs-lookup"><span data-stu-id="d40ff-110">Predefined rights are found in the <xref:System.IdentityModel.Claims.Rights> class (<xref:System.IdentityModel.Claims.Rights.Identity%2A>,  <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>).</span></span>

- <span data-ttu-id="d40ff-111"><xref:System.IdentityModel.Claims.Claim.Resource%2A> 屬性會傳回與宣告相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="d40ff-111">The <xref:System.IdentityModel.Claims.Claim.Resource%2A> property returns the resource associated with the claim.</span></span>

<span data-ttu-id="d40ff-112">每個 <xref:System.IdentityModel.Claims.ClaimSet> 也都有 <xref:System.IdentityModel.Claims.ClaimSet.Issuer%2A> 屬性，此屬性表示 <xref:System.IdentityModel.Claims.ClaimSet> 的 `Issuer`。</span><span class="sxs-lookup"><span data-stu-id="d40ff-112">Each <xref:System.IdentityModel.Claims.ClaimSet> also has an <xref:System.IdentityModel.Claims.ClaimSet.Issuer%2A> property, which represents the <xref:System.IdentityModel.Claims.ClaimSet> of the `Issuer`.</span></span>

## <a name="windows-accounts"></a><span data-ttu-id="d40ff-113">Windows 帳戶</span><span class="sxs-lookup"><span data-stu-id="d40ff-113">Windows Accounts</span></span>

<span data-ttu-id="d40ff-114">當用戶端認證對應至 Windows 使用者帳戶時，產生的 <xref:System.IdentityModel.Claims.ClaimSet> 具有下列值：</span><span class="sxs-lookup"><span data-stu-id="d40ff-114">Where a client credential maps to a Windows user account, the resulting <xref:System.IdentityModel.Claims.ClaimSet> has the following values:</span></span>

- <span data-ttu-id="d40ff-115">`Issuer` 是 <xref:System.IdentityModel.Claims.ClaimSet> 類別的靜態 Windows 屬性所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="d40ff-115">The `Issuer` is the value returned by the static Windows property of the <xref:System.IdentityModel.Claims.ClaimSet> class.</span></span>

- <span data-ttu-id="d40ff-116">此集合中的宣告為：</span><span class="sxs-lookup"><span data-stu-id="d40ff-116">The claims in the collection are:</span></span>

  - <span data-ttu-id="d40ff-117">具有安全識別項 (SID) 之 <xref:System.IdentityModel.Claims.Claim> 值的 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A>、<xref:System.IdentityModel.Claims.Claim.Right%2A> 的 `Identity` 屬性值，以及傳回實際 SID 值的 <xref:System.IdentityModel.Claims.Claim.Resource%2A>。</span><span class="sxs-lookup"><span data-stu-id="d40ff-117">A <xref:System.IdentityModel.Claims.Claim> with a <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> value of security identifier (SID), a <xref:System.IdentityModel.Claims.Claim.Right%2A> property value of `Identity`, and a <xref:System.IdentityModel.Claims.Claim.Resource%2A> that returns the actual SID value.</span></span> <span data-ttu-id="d40ff-118">SID 是網域控制站發出至每個使用者的唯一值。</span><span class="sxs-lookup"><span data-stu-id="d40ff-118">A SID is a unique value the domain controller issues to every user.</span></span> <span data-ttu-id="d40ff-119">SID 可用來識別與 Windows 安全性互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="d40ff-119">The SID is used to identify the user in interactions with Windows security.</span></span>

  - <span data-ttu-id="d40ff-120">具有 SID 之 <xref:System.IdentityModel.Claims.Claim> 值的 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A>、<xref:System.IdentityModel.Claims.Claim.Right%2A> 的 `PossessProperty`，以及 SID 值的 <xref:System.IdentityModel.Claims.Claim.Resource%2A>。</span><span class="sxs-lookup"><span data-stu-id="d40ff-120">A <xref:System.IdentityModel.Claims.Claim> with a <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> value of SID, a <xref:System.IdentityModel.Claims.Claim.Right%2A> of `PossessProperty`, and a <xref:System.IdentityModel.Claims.Claim.Resource%2A> of the SID value.</span></span>

  - <span data-ttu-id="d40ff-121">具有 <xref:System.IdentityModel.Claims.Claim> 之 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 的 <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A>、<xref:System.IdentityModel.Claims.Claim.Right%2A> 的 `PossessProperty`，以及包含使用者名稱之字串 (例如，"MYMACHINE\Bob") 的 <xref:System.IdentityModel.Claims.Claim.Resource%2A>。</span><span class="sxs-lookup"><span data-stu-id="d40ff-121">A <xref:System.IdentityModel.Claims.Claim> with a <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> of <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A>, a <xref:System.IdentityModel.Claims.Claim.Right%2A> of `PossessProperty` and a <xref:System.IdentityModel.Claims.Claim.Resource%2A> of string containing the user name (for example, "MYMACHINE\Bob").</span></span>

  - <span data-ttu-id="d40ff-122">其他 SID 宣告，這些宣告具有使用者所屬之各種群組的 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>。</span><span class="sxs-lookup"><span data-stu-id="d40ff-122">Additional SID claims with <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> for the various groups the user belongs to.</span></span>

## <a name="certificates"></a><span data-ttu-id="d40ff-123">憑證</span><span class="sxs-lookup"><span data-stu-id="d40ff-123">Certificates</span></span>

<span data-ttu-id="d40ff-124">當用戶端認證是憑證時，產生的 <xref:System.IdentityModel.Claims.ClaimSet> 具有下列值：</span><span class="sxs-lookup"><span data-stu-id="d40ff-124">Where the client credential is a certificate, the resulting <xref:System.IdentityModel.Claims.ClaimSet> has the following values:</span></span>

- <span data-ttu-id="d40ff-125">如果是自動發行的憑證，`Issuer` 就是 <xref:System.IdentityModel.Claims.ClaimSet> 本身。</span><span class="sxs-lookup"><span data-stu-id="d40ff-125">For self-issued certificates, the `Issuer` is the <xref:System.IdentityModel.Claims.ClaimSet> itself.</span></span> <span data-ttu-id="d40ff-126"><xref:System.IdentityModel.Claims.ClaimSet> 會傳回 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 的 <xref:System.IdentityModel.Claims.ClaimTypes.Thumbprint%2A>、<xref:System.IdentityModel.Claims.Claim.Right%2A> 的 `Identity`，以及 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 值，此值表示包含憑證指紋的 <xref:System.Byte> 陣列。</span><span class="sxs-lookup"><span data-stu-id="d40ff-126">The <xref:System.IdentityModel.Claims.ClaimSet> returns a <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> of <xref:System.IdentityModel.Claims.ClaimTypes.Thumbprint%2A>, a <xref:System.IdentityModel.Claims.Claim.Right%2A> of `Identity`, and a <xref:System.IdentityModel.Claims.Claim.Resource%2A> value that is a <xref:System.Byte> array containing the thumbprint of the certificate.</span></span>

- <span data-ttu-id="d40ff-127">如果是由憑證授權單位發出的憑證，簽發者就是 `ClaimSet`，表示憑證授權單位的憑證。</span><span class="sxs-lookup"><span data-stu-id="d40ff-127">For a certificate issued by a certification authority, the issuer is the `ClaimSet` representing the certification authority’s certificate.</span></span>

- <span data-ttu-id="d40ff-128">此集合中的 `Claims` 包括：</span><span class="sxs-lookup"><span data-stu-id="d40ff-128">The `Claims` in the collection include:</span></span>

  - <span data-ttu-id="d40ff-129">具有 Thumbprint 之 `Claim` 的 `ClaimType`、PossessProperty 的 `Right`，以及 `Resource`，表示包含憑證指紋的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="d40ff-129">A `Claim` with a `ClaimType` of Thumbprint, a `Right` of PossessProperty, and a `Resource` that is a byte array containing the thumbprint of the certificate</span></span>

  - <span data-ttu-id="d40ff-130">各種類型的其他 PossessProperty 宣告，包括 X500DistinguishedName、Dns、Name、Upn 和 Rsa，表示憑證的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="d40ff-130">Additional PossessProperty claims of various types, including X500DistinguishedName, Dns, Name, Upn, and Rsa, represent various properties of the certificate.</span></span> <span data-ttu-id="d40ff-131">Rsa 宣告的資源是與憑證相關聯的公開金鑰。**注意**其中，用戶端認證類型是服務對應至 Windows 帳戶的憑證， `ClaimSet` 會產生兩個物件。</span><span class="sxs-lookup"><span data-stu-id="d40ff-131">The resource for the Rsa claim is the public key associated with the certificate.**Note** Where the client credential type is a certificate that the service maps to a Windows account, two `ClaimSet` objects are generated.</span></span> <span data-ttu-id="d40ff-132">第一個包含與 Windows 帳戶相關的所有宣告，第二個則包含與憑證相關的所有宣告。</span><span class="sxs-lookup"><span data-stu-id="d40ff-132">The first contains all the claims related to the Windows account and the second contains all the claims related to the certificate.</span></span>

## <a name="user-namepassword"></a><span data-ttu-id="d40ff-133">使用者名稱/密碼</span><span class="sxs-lookup"><span data-stu-id="d40ff-133">User Name/Password</span></span>

<span data-ttu-id="d40ff-134">當用戶端認證是未對應至 Windows 帳戶的使用者名稱/密碼 (或對等用法) 時，產生的 `ClaimSet` 會由 <xref:System.IdentityModel.Claims.ClaimSet.System%2A> 類別的靜態 `ClaimSet` 屬性發出。</span><span class="sxs-lookup"><span data-stu-id="d40ff-134">Where the client credential is a user name/password (or equivalent) that does not map to a Windows account, the resulting `ClaimSet` is issued by the static <xref:System.IdentityModel.Claims.ClaimSet.System%2A> property of the `ClaimSet` class.</span></span> <span data-ttu-id="d40ff-135">`ClaimSet`包含類型的 `Identity` <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A> 宣告，其資源是用戶端提供的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d40ff-135">The `ClaimSet` contains an `Identity` claim of type <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A> whose resource is the user name the client provides.</span></span> <span data-ttu-id="d40ff-136">對應的宣告具有 `Right` 的`PossessProperty`。</span><span class="sxs-lookup"><span data-stu-id="d40ff-136">A corresponding claim has a `Right` of `PossessProperty`.</span></span>

## <a name="rsa-keys"></a><span data-ttu-id="d40ff-137">RSA 金鑰</span><span class="sxs-lookup"><span data-stu-id="d40ff-137">RSA Keys</span></span>

<span data-ttu-id="d40ff-138">當使用未與憑證相關聯的 RSA 金鑰時，產生的 `ClaimSet` 會自行發出，並包含 `Identity` 類型的宣告， <xref:System.IdentityModel.Claims.ClaimTypes.Rsa%2A> 其資源是 RSA 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d40ff-138">Where an RSA key not associated with a certificate is used, the resulting `ClaimSet` is self-issued and contains an `Identity` claim of type <xref:System.IdentityModel.Claims.ClaimTypes.Rsa%2A> whose resource is the RSA key.</span></span> <span data-ttu-id="d40ff-139">對應的宣告具有 `Right` 的`PossessProperty`。</span><span class="sxs-lookup"><span data-stu-id="d40ff-139">A corresponding claim has a `Right` of `PossessProperty`.</span></span>

## <a name="saml"></a><span data-ttu-id="d40ff-140">SAML</span><span class="sxs-lookup"><span data-stu-id="d40ff-140">SAML</span></span>

<span data-ttu-id="d40ff-141">當用戶端使用安全性判斷提示標記語言 (SAML) 權杖進行驗證時，產生的 `ClaimSet` 會由簽署 SAML 權杖的實體發出，通常是所發出 SAML 權杖之安全性權杖服務 (STS) 的憑證。</span><span class="sxs-lookup"><span data-stu-id="d40ff-141">Where the client authenticates with a Security Assertions Markup Language (SAML) token, the resulting `ClaimSet` is issued by the entity that signed the SAML token, often the certificate of the security token service (STS) that issued the SAML token.</span></span> <span data-ttu-id="d40ff-142">`ClaimSet` 包含 SAML 權杖中的各種宣告。</span><span class="sxs-lookup"><span data-stu-id="d40ff-142">The `ClaimSet` contains various claims as found in the SAML token.</span></span> <span data-ttu-id="d40ff-143">如果 SAML 權杖包含具有非 `SamlSubject` 名稱的 `null`，則會建立具有 `Identity` 型別的 <xref:System.IdentityModel.Claims.ClaimTypes.NameIdentifier%2A> 宣告和 <xref:System.IdentityModel.Tokens.SamlNameIdentifierClaimResource> 的資源型別。</span><span class="sxs-lookup"><span data-stu-id="d40ff-143">If the SAML token contains a `SamlSubject` with a non-`null` name, then an `Identity` claim with a type of <xref:System.IdentityModel.Claims.ClaimTypes.NameIdentifier%2A> and a resource type of <xref:System.IdentityModel.Tokens.SamlNameIdentifierClaimResource> are created.</span></span>

## <a name="identity-claims-and-servicesecuritycontextisanonymous"></a><span data-ttu-id="d40ff-144">身分識別宣告和 ServiceSecurityContext.IsAnonymous</span><span class="sxs-lookup"><span data-stu-id="d40ff-144">Identity Claims and ServiceSecurityContext.IsAnonymous</span></span>

<span data-ttu-id="d40ff-145">如果 `ClaimSet` 用戶端認證產生的物件都不包含具有之的宣告， `Right` `Identity,` 則屬性會傳回 <xref:System.ServiceModel.ServiceSecurityContext.IsAnonymous%2A> `true` 。</span><span class="sxs-lookup"><span data-stu-id="d40ff-145">If none of the `ClaimSet` objects resulting from the client credentials contain a claim with a `Right` of `Identity,` then the <xref:System.ServiceModel.ServiceSecurityContext.IsAnonymous%2A> property returns `true`.</span></span> <span data-ttu-id="d40ff-146">如果出現一或多個這類的宣告，則 `IsAnonymous` 屬性會傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="d40ff-146">If one or more such claims are present, the `IsAnonymous` property returns `false`.</span></span>

## <a name="see-also"></a><span data-ttu-id="d40ff-147">請參閱</span><span class="sxs-lookup"><span data-stu-id="d40ff-147">See also</span></span>

- <xref:System.IdentityModel.Claims.ClaimSet>
- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- [<span data-ttu-id="d40ff-148">使用身分識別模型來管理宣告與授權</span><span class="sxs-lookup"><span data-stu-id="d40ff-148">Managing Claims and Authorization with the Identity Model</span></span>](managing-claims-and-authorization-with-the-identity-model.md)

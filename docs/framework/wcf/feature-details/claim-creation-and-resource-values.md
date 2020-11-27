---
title: 宣告建立與資源值
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], creation and resource values
ms.assetid: 30431f76-cbe7-4bad-bad7-8e43e23a82d4
ms.openlocfilehash: c3f36d607d88b208753066dcbd4e9baa6a2590fa
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295128"
---
# <a name="claim-creation-and-resource-values"></a><span data-ttu-id="b6696-102">宣告建立與資源值</span><span class="sxs-lookup"><span data-stu-id="b6696-102">Claim Creation and Resource Values</span></span>

<span data-ttu-id="b6696-103"><xref:System.IdentityModel.Claims.Claim> 類別提供幾種建立內建宣告類型之執行個體的方法。</span><span class="sxs-lookup"><span data-stu-id="b6696-103">The <xref:System.IdentityModel.Claims.Claim> class provides several methods for creating instances of built-in claims types.</span></span> <span data-ttu-id="b6696-104">這些方法的下列幾項不會對提供的資源執行語意或格式檢查：</span><span class="sxs-lookup"><span data-stu-id="b6696-104">Of these methods, the following perform no semantic or format checking on the supplied resource:</span></span>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDnsClaim%2A>  
  
- <span data-ttu-id="b6696-105"><xref:System.IdentityModel.Claims.Claim.CreateHashClaim%2A> (不會檢查長度或位元組陣列內容)</span><span class="sxs-lookup"><span data-stu-id="b6696-105"><xref:System.IdentityModel.Claims.Claim.CreateHashClaim%2A> (does not check the length or content of the byte array)</span></span>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateNameClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateSpnClaim%2A>  
  
- <span data-ttu-id="b6696-106"><xref:System.IdentityModel.Claims.Claim.CreateThumbprintClaim%2A> (不會檢查長度或位元組陣列內容)</span><span class="sxs-lookup"><span data-stu-id="b6696-106"><xref:System.IdentityModel.Claims.Claim.CreateThumbprintClaim%2A> (does not check the length or content of the byte array)</span></span>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUpnClaim%2A>  
  
 <span data-ttu-id="b6696-107">當呼叫上述方法時應該注意，確定傳入的資源值是使用正確格式，或包含正確的資訊類型 (或兩者皆是)。</span><span class="sxs-lookup"><span data-stu-id="b6696-107">Care should be taken when calling the above methods to ensure that the resource values passed in are of the correct format or contain the correct kind of information (or both).</span></span>  
  
 <span data-ttu-id="b6696-108">下列方法使用特定類型：</span><span class="sxs-lookup"><span data-stu-id="b6696-108">The following methods take specific types:</span></span>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDenyOnlyWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateMailAddressClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateRsaClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUriClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateX500DistinguishedNameClaim%2A>  
  
## <a name="see-also"></a><span data-ttu-id="b6696-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b6696-109">See also</span></span>

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [<span data-ttu-id="b6696-110">使用身分識別模型來管理宣告與授權</span><span class="sxs-lookup"><span data-stu-id="b6696-110">Managing Claims and Authorization with the Identity Model</span></span>](managing-claims-and-authorization-with-the-identity-model.md)

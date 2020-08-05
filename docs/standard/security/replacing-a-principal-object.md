---
title: 取代 Principal 物件
ms.date: 07/15/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- principal objects, replacing
- security [.NET], replacing principal objects
- security [.NET], principals
ms.assetid: c323687e-b196-487b-beba-f38f9b3f961b
ms.openlocfilehash: fced91aef991bc228e65128d5e8d69e6a46588e5
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557095"
---
# <a name="replacing-a-principal-object"></a><span data-ttu-id="482cb-102">取代 Principal 物件</span><span class="sxs-lookup"><span data-stu-id="482cb-102">Replacing a Principal Object</span></span>

<span data-ttu-id="482cb-103">提供驗證服務的應用程式必須能夠針對指定的執行緒取代 **主體** 物件 (<xref:System.Security.Principal.IPrincipal>)。</span><span class="sxs-lookup"><span data-stu-id="482cb-103">Applications that provide authentication services must be able to replace the **Principal** object (<xref:System.Security.Principal.IPrincipal>) for a given thread.</span></span> <span data-ttu-id="482cb-104">此外，因為惡意的附加檔案、不正確的 **主體** 會宣告為不實身分識別或角色，進而危及應用程式的安全性，所以安全性系統必須協助保護取代 **主體** 物件的能力。</span><span class="sxs-lookup"><span data-stu-id="482cb-104">Furthermore, the security system must help protect the ability to replace **Principal** objects because a maliciously attached, incorrect **Principal** compromises the security of your application by claiming an untrue identity or role.</span></span> <span data-ttu-id="482cb-105">因此，需要能夠取代 **主體** 物件的應用程式必須為其授與主體控制的 <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType> 物件。</span><span class="sxs-lookup"><span data-stu-id="482cb-105">Therefore, applications that require the ability to replace **Principal** objects must be granted the <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType> object for principal control.</span></span> <span data-ttu-id="482cb-106">(請注意執行以角色為基礎的安全性檢查或建立 **主體** 物件並不需要此權限。)</span><span class="sxs-lookup"><span data-stu-id="482cb-106">(Note that this permission is not required for performing role-based security checks or for creating **Principal** objects.)</span></span>  
  
<span data-ttu-id="482cb-107">目前可以執行下列工作來取代 **主體** 物件：</span><span class="sxs-lookup"><span data-stu-id="482cb-107">The current **Principal** object can be replaced by performing the following tasks:</span></span>  
  
1. <span data-ttu-id="482cb-108">建立取代 **主體** 物件和相關聯的 **身分識別** 物件。</span><span class="sxs-lookup"><span data-stu-id="482cb-108">Create the replacement **Principal** object and associated **Identity** object.</span></span>  
  
2. <span data-ttu-id="482cb-109">將新的 **主體** 物件附加至呼叫內容。</span><span class="sxs-lookup"><span data-stu-id="482cb-109">Attach the new **Principal** object to the call context.</span></span>  
  
## <a name="example"></a><span data-ttu-id="482cb-110">範例</span><span class="sxs-lookup"><span data-stu-id="482cb-110">Example</span></span>

<span data-ttu-id="482cb-111">下列範例示範如何建立一般的主體物件，並用來設定執行緒主體。</span><span class="sxs-lookup"><span data-stu-id="482cb-111">The following example shows how to create a generic principal object and use it to set the principal of a thread.</span></span>  
  
[!code-csharp[SetCurrentPrincipal#1](../../../samples/snippets/csharp/VS_Snippets_CLR/SetCurrentPrincipal/CS/program.cs#1)]
[!code-vb[SetCurrentPrincipal#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/SetCurrentPrincipal/VB/program.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="482cb-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="482cb-112">See also</span></span>

- <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType>
- [<span data-ttu-id="482cb-113">Principal 和 Identity 物件</span><span class="sxs-lookup"><span data-stu-id="482cb-113">Principal and Identity Objects</span></span>](principal-and-identity-objects.md)
- [<span data-ttu-id="482cb-114">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="482cb-114">ASP.NET Core Security</span></span>](/aspnet/core/security/)

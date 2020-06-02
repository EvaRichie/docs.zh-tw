---
title: 取代 Principal 物件
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- principal objects, replacing
- security [.NET Framework], replacing principal objects
- security [.NET Framework], principals
ms.assetid: c323687e-b196-487b-beba-f38f9b3f961b
ms.openlocfilehash: 056bd0bbafe0e7dc84d8d0c532ff844370c59230
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291210"
---
# <a name="replacing-a-principal-object"></a>取代 Principal 物件
提供驗證服務的應用程式必須能夠針對指定的執行緒取代 **主體** 物件 (<xref:System.Security.Principal.IPrincipal>)。 此外，因為惡意的附加檔案、不正確的 **主體** 會宣告為不實身分識別或角色，進而危及應用程式的安全性，所以安全性系統必須協助保護取代 **主體** 物件的能力。 因此，需要能夠取代 **主體** 物件的應用程式必須為其授與主體控制的 <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType> 物件。 (請注意執行以角色為基礎的安全性檢查或建立 **主體** 物件並不需要此權限。)  
  
 目前可以執行下列工作來取代 **主體** 物件：  
  
1. 建立取代 **主體** 物件和相關聯的 **身分識別** 物件。  
  
2. 將新的 **主體** 物件附加至呼叫內容。  
  
## <a name="example"></a>範例  
 下列範例示範如何建立一般的主體物件，並用來設定執行緒主體。  
  
 [!code-csharp[SetCurrentPrincipal#1](../../../samples/snippets/csharp/VS_Snippets_CLR/SetCurrentPrincipal/CS/program.cs#1)]
 [!code-vb[SetCurrentPrincipal#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/SetCurrentPrincipal/VB/program.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType>
- [Principal 和 Identity 物件](principal-and-identity-objects.md)

---
title: 不支援的功能
ms.date: 03/30/2017
ms.assetid: e480cfb5-697e-42c8-bed5-9264c945c4f9
ms.openlocfilehash: d4fe3d91b80197d962989cd2d3bc9bb2df6e3ffe
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164151"
---
# <a name="unsupported-functionality"></a><span data-ttu-id="70478-102">不支援的功能</span><span class="sxs-lookup"><span data-stu-id="70478-102">Unsupported Functionality</span></span>

<span data-ttu-id="70478-103">在 LINQ to SQL 中，下列 SQL 功能無法透過轉譯現有 Common Language Runtime (CLR) 和 .NET Framework 建構來公開 (Expose)：</span><span class="sxs-lookup"><span data-stu-id="70478-103">In LINQ to SQL, the following SQL functionality cannot be exposed through translation of existing common language runtime (CLR) and .NET Framework constructs:</span></span>  
  
- `STDDEV`  
  
- `LIKE`  
  
     <span data-ttu-id="70478-104">雖然 `LIKE` 並非透過直接轉譯提供支援，但是類似的功能存在 <xref:System.Data.Linq.SqlClient.SqlMethods> 類別 (Class) 中。</span><span class="sxs-lookup"><span data-stu-id="70478-104">Although `LIKE` is not supported through direct translation, similar functionality exists in the <xref:System.Data.Linq.SqlClient.SqlMethods> class.</span></span> <span data-ttu-id="70478-105">如需詳細資訊，請參閱<xref:System.Data.Linq.SqlClient.SqlMethods.Like%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="70478-105">For more information, see <xref:System.Data.Linq.SqlClient.SqlMethods.Like%2A?displayProperty=nameWithType>.</span></span>  
  
- `DATEDIFF`  
  
     <span data-ttu-id="70478-106">LINQ to SQL 對於 `DATEDIFF` 的支援有限。</span><span class="sxs-lookup"><span data-stu-id="70478-106">LINQ to SQL has limited support for `DATEDIFF`.</span></span> <span data-ttu-id="70478-107">類似的功能存在 <xref:System.Data.Linq.SqlClient.SqlMethods> 類別中。</span><span class="sxs-lookup"><span data-stu-id="70478-107">Similar functionality exists in the <xref:System.Data.Linq.SqlClient.SqlMethods> class.</span></span>  
  
- `ROUND`  
  
     <span data-ttu-id="70478-108">LINQ to SQL 對於 `ROUND` 的支援有限。</span><span class="sxs-lookup"><span data-stu-id="70478-108">LINQ to SQL has limited support for `ROUND`.</span></span> <span data-ttu-id="70478-109">如需詳細資訊，請參閱 [系統數學方法](system-math-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="70478-109">For more information, see [System.Math Methods](system-math-methods.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="70478-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70478-110">See also</span></span>

- [<span data-ttu-id="70478-111">資料類型與函式</span><span class="sxs-lookup"><span data-stu-id="70478-111">Data Types and Functions</span></span>](data-types-and-functions.md)

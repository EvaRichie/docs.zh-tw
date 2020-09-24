---
title: 將類型轉換為泛型 IEnumerable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 64774fb5-7447-4296-ad3b-8a94346f99a1
ms.openlocfilehash: c2d34ae708f79d9f920679b3714a100fe8943c38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164411"
---
# <a name="convert-a-type-to-a-generic-ienumerable"></a><span data-ttu-id="766cd-102">將類型轉換為泛型 IEnumerable</span><span class="sxs-lookup"><span data-stu-id="766cd-102">Convert a Type to a Generic IEnumerable</span></span>

<span data-ttu-id="766cd-103">使用 <xref:System.Linq.Enumerable.AsEnumerable%2A> 傳回型別設為泛型 `IEnumerable` 的引數。</span><span class="sxs-lookup"><span data-stu-id="766cd-103">Use <xref:System.Linq.Enumerable.AsEnumerable%2A> to return the argument typed as a generic `IEnumerable`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="766cd-104">範例</span><span class="sxs-lookup"><span data-stu-id="766cd-104">Example</span></span>  

 <span data-ttu-id="766cd-105">在此範例中，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (使用預設泛型 `Query`) 會嘗試將查詢轉換為 SQL，並且在伺服器上執行查詢。</span><span class="sxs-lookup"><span data-stu-id="766cd-105">In this example, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (using the default generic `Query`) would try to convert the query to SQL and execute it on the server.</span></span> <span data-ttu-id="766cd-106">但是，`where` 子句會參考使用者定義的用戶端方法 (`isValidProduct`)，而該方法無法轉換為 SQL。</span><span class="sxs-lookup"><span data-stu-id="766cd-106">But the `where` clause references a user-defined client-side method (`isValidProduct`), which cannot be converted to SQL.</span></span>  
  
 <span data-ttu-id="766cd-107">解決方案為指定 <xref:System.Collections.Generic.IEnumerable%601> 的用戶端泛型 `where` 實作，以取代泛型 <xref:System.Linq.IQueryable%601>。</span><span class="sxs-lookup"><span data-stu-id="766cd-107">The solution is to specify the client-side generic <xref:System.Collections.Generic.IEnumerable%601> implementation of `where` to replace the generic <xref:System.Linq.IQueryable%601>.</span></span> <span data-ttu-id="766cd-108">您可藉由叫用 (Invoke) <xref:System.Linq.Enumerable.AsEnumerable%2A> 運算子來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="766cd-108">You do this by invoking the <xref:System.Linq.Enumerable.AsEnumerable%2A> operator.</span></span>  
  
 [!code-csharp[DLinqQueryExamples#46](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#46)]
 [!code-vb[DLinqQueryExamples#46](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#46)]  
  
## <a name="see-also"></a><span data-ttu-id="766cd-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="766cd-109">See also</span></span>

- [<span data-ttu-id="766cd-110">查詢範例</span><span class="sxs-lookup"><span data-stu-id="766cd-110">Query Examples</span></span>](query-examples.md)

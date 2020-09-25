---
title: 從方法傳回查詢
description: 如何傳回查詢。
ms.date: 11/30/2016
ms.assetid: db220f79-c35b-41f2-886c-cd068672d42d
ms.openlocfilehash: 646e771d637aa242231e3fe216d4a856bb156649
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203328"
---
# <a name="how-to-return-a-query-from-a-method-c-programming-guide"></a><span data-ttu-id="8c69d-103">如何從方法傳回查詢 (c # 程式設計手冊) </span><span class="sxs-lookup"><span data-stu-id="8c69d-103">How to return a query from a method (C# Programming Guide)</span></span>

<span data-ttu-id="8c69d-104">這個範例示範如何以傳回值和 `out` 參數形式從方法中傳回查詢。</span><span class="sxs-lookup"><span data-stu-id="8c69d-104">This example shows how to return a query from a method as the return value and as an `out` parameter.</span></span>  
  
 <span data-ttu-id="8c69d-105">查詢物件是可編寫的，這表示您可以從方法傳回查詢。</span><span class="sxs-lookup"><span data-stu-id="8c69d-105">Query objects are composable, meaning that you can return a query from a method.</span></span> <span data-ttu-id="8c69d-106">代表查詢的物件不會儲存所產生的集合，而是在必要時產生結果的步驟。</span><span class="sxs-lookup"><span data-stu-id="8c69d-106">Objects that represent queries do not store the resulting collection, but rather the steps to produce the results when needed.</span></span> <span data-ttu-id="8c69d-107">從方法傳回查詢物件的優點，在於可以進一步編寫或修改它們。</span><span class="sxs-lookup"><span data-stu-id="8c69d-107">The advantage of returning query objects from methods is that they can be further composed or modified.</span></span> <span data-ttu-id="8c69d-108">因此，傳回查詢的方法的任何傳回值或 `out` 參數也必須具有該類型。</span><span class="sxs-lookup"><span data-stu-id="8c69d-108">Therefore any return value or `out` parameter of a method that returns a query must also have that type.</span></span> <span data-ttu-id="8c69d-109">如果方法將查詢具體化到具體 <xref:System.Collections.Generic.List%601> 或 <xref:System.Array> 類型，則會視為傳回查詢結果，而不是查詢本身。</span><span class="sxs-lookup"><span data-stu-id="8c69d-109">If a method materializes a query into a concrete <xref:System.Collections.Generic.List%601> or <xref:System.Array> type, it is considered to be returning the query results instead of the query itself.</span></span> <span data-ttu-id="8c69d-110">從方法傳回的查詢變數仍然可以進行編寫或修改。</span><span class="sxs-lookup"><span data-stu-id="8c69d-110">A query variable that is returned from a method can still be composed or modified.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8c69d-111">範例</span><span class="sxs-lookup"><span data-stu-id="8c69d-111">Example</span></span>  

 <span data-ttu-id="8c69d-112">在下列範例中，第一個方法會以傳回值形式傳回查詢，第二個方法會以 `out` 參數形式傳回查詢。</span><span class="sxs-lookup"><span data-stu-id="8c69d-112">In the following example, the first method returns a query as a return value, and the second method returns a query as an `out` parameter.</span></span> <span data-ttu-id="8c69d-113">請注意，在這兩種情況下，它是傳回的查詢，而不是查詢結果。</span><span class="sxs-lookup"><span data-stu-id="8c69d-113">Note that in both cases it is a query that is  returned, not query results.</span></span>  
  
 [!code-csharp[csProgGuideLINQ#80](~/samples/snippets/csharp/concepts/linq/how-to-return-a-query-from-a-method_1.cs)]  

## <a name="see-also"></a><span data-ttu-id="8c69d-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8c69d-114">See also</span></span>

- [<span data-ttu-id="8c69d-115">Language Integrated Query (LINQ)</span><span class="sxs-lookup"><span data-stu-id="8c69d-115">Language Integrated Query (LINQ)</span></span>](index.md)

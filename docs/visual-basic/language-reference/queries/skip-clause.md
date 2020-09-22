---
title: Skip 子句
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkip
helpviewer_keywords:
- queries [Visual Basic], Skip
- Skip statement [Visual Basic]
- Skip clause [Visual Basic]
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
ms.openlocfilehash: 40e89160baf663f7d6785e5d3e09ad6cc4eefbde
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866310"
---
# <a name="skip-clause-visual-basic"></a><span data-ttu-id="c05e6-102">Skip 子句 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c05e6-102">Skip Clause (Visual Basic)</span></span>

<span data-ttu-id="c05e6-103">略過集合中指定數目的項目，然後傳回其餘項目。</span><span class="sxs-lookup"><span data-stu-id="c05e6-103">Bypasses a specified number of elements in a collection and then returns the remaining elements.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c05e6-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="c05e6-104">Syntax</span></span>  
  
```vb  
Skip count  
```  
  
## <a name="parts"></a><span data-ttu-id="c05e6-105">組件</span><span class="sxs-lookup"><span data-stu-id="c05e6-105">Parts</span></span>  

 `count`  
 <span data-ttu-id="c05e6-106">必要。</span><span class="sxs-lookup"><span data-stu-id="c05e6-106">Required.</span></span> <span data-ttu-id="c05e6-107">值或運算式，評估為要跳過之序列的專案數。</span><span class="sxs-lookup"><span data-stu-id="c05e6-107">A value or an expression that evaluates to the number of elements of the sequence to skip.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c05e6-108">備註</span><span class="sxs-lookup"><span data-stu-id="c05e6-108">Remarks</span></span>  

 <span data-ttu-id="c05e6-109">`Skip`子句會讓查詢略過結果清單開頭的專案，並傳回其餘的元素。</span><span class="sxs-lookup"><span data-stu-id="c05e6-109">The `Skip` clause causes a query to bypass elements at the beginning of a results list and return the remaining elements.</span></span> <span data-ttu-id="c05e6-110">要跳過的元素數目是由參數所識別 `count` 。</span><span class="sxs-lookup"><span data-stu-id="c05e6-110">The number of elements to skip is identified by the `count` parameter.</span></span>  
  
 <span data-ttu-id="c05e6-111">您可以使用 `Skip` 子句搭配 `Take` 子句，從查詢的任何區段傳回資料範圍。</span><span class="sxs-lookup"><span data-stu-id="c05e6-111">You can use the `Skip` clause with the `Take` clause to return a range of data from any segment of a query.</span></span> <span data-ttu-id="c05e6-112">若要這樣做，請將範圍第一個元素的索引傳遞給子句，並將範圍的大小傳遞給 `Skip` `Take` 子句。</span><span class="sxs-lookup"><span data-stu-id="c05e6-112">To do this, pass the index of the first element of the range to the `Skip` clause and the size of the range to the `Take` clause.</span></span>  
  
 <span data-ttu-id="c05e6-113">當您 `Skip` 在查詢中使用子句時，您可能也需要確保結果會以可讓 `Skip` 子句略過預期結果的順序傳回。</span><span class="sxs-lookup"><span data-stu-id="c05e6-113">When you use the `Skip` clause in a query, you may also need to ensure that the results are returned in an order that will enable the `Skip` clause to bypass the intended results.</span></span> <span data-ttu-id="c05e6-114">如需排序查詢結果的詳細資訊，請參閱 [Order By 子句](order-by-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="c05e6-114">For more information about ordering query results, see [Order By Clause](order-by-clause.md).</span></span>  
  
 <span data-ttu-id="c05e6-115">您可以使用 `SkipWhile` 子句來指定根據提供的條件，只忽略特定的元素。</span><span class="sxs-lookup"><span data-stu-id="c05e6-115">You can use the `SkipWhile` clause to specify that only certain elements are ignored, depending on a supplied condition.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c05e6-116">範例</span><span class="sxs-lookup"><span data-stu-id="c05e6-116">Example</span></span>  

 <span data-ttu-id="c05e6-117">下列程式碼範例會將 `Skip` 子句和子句一起使用， `Take` 以從頁面中的查詢傳回資料。</span><span class="sxs-lookup"><span data-stu-id="c05e6-117">The following code example uses the `Skip` clause together with the `Take` clause to return data from a query in pages.</span></span> <span data-ttu-id="c05e6-118">`GetCustomers`函數會使用 `Skip` 子句來略過清單中的客戶，直到提供的起始索引值為止，並使用 `Take` 子句傳回從該索引值開始之客戶的頁面。</span><span class="sxs-lookup"><span data-stu-id="c05e6-118">The `GetCustomers` function uses the `Skip` clause to bypass the customers in the list until the supplied starting index value, and uses the `Take` clause to return a page of customers starting from that index value.</span></span>  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="c05e6-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c05e6-119">See also</span></span>

- [<span data-ttu-id="c05e6-120">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="c05e6-120">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="c05e6-121">查詢</span><span class="sxs-lookup"><span data-stu-id="c05e6-121">Queries</span></span>](index.md)
- [<span data-ttu-id="c05e6-122">Select 子句</span><span class="sxs-lookup"><span data-stu-id="c05e6-122">Select Clause</span></span>](select-clause.md)
- [<span data-ttu-id="c05e6-123">From 子句</span><span class="sxs-lookup"><span data-stu-id="c05e6-123">From Clause</span></span>](from-clause.md)
- [<span data-ttu-id="c05e6-124">Order By 子句</span><span class="sxs-lookup"><span data-stu-id="c05e6-124">Order By Clause</span></span>](order-by-clause.md)
- [<span data-ttu-id="c05e6-125">Skip While 子句</span><span class="sxs-lookup"><span data-stu-id="c05e6-125">Skip While Clause</span></span>](skip-while-clause.md)
- [<span data-ttu-id="c05e6-126">Take 子句</span><span class="sxs-lookup"><span data-stu-id="c05e6-126">Take Clause</span></span>](take-clause.md)

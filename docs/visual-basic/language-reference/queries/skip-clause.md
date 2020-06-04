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
ms.openlocfilehash: 427d14453260a54bd3f2ab9a8ac75dedacd291f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359654"
---
# <a name="skip-clause-visual-basic"></a><span data-ttu-id="acc8b-102">Skip 子句 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="acc8b-102">Skip Clause (Visual Basic)</span></span>
<span data-ttu-id="acc8b-103">略過集合中指定數目的項目，然後傳回其餘項目。</span><span class="sxs-lookup"><span data-stu-id="acc8b-103">Bypasses a specified number of elements in a collection and then returns the remaining elements.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="acc8b-104">語法</span><span class="sxs-lookup"><span data-stu-id="acc8b-104">Syntax</span></span>  
  
```vb  
Skip count  
```  
  
## <a name="parts"></a><span data-ttu-id="acc8b-105">組件</span><span class="sxs-lookup"><span data-stu-id="acc8b-105">Parts</span></span>  
 `count`  
 <span data-ttu-id="acc8b-106">必要。</span><span class="sxs-lookup"><span data-stu-id="acc8b-106">Required.</span></span> <span data-ttu-id="acc8b-107">值或運算式，評估為要略過的序列元素數目。</span><span class="sxs-lookup"><span data-stu-id="acc8b-107">A value or an expression that evaluates to the number of elements of the sequence to skip.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="acc8b-108">備註</span><span class="sxs-lookup"><span data-stu-id="acc8b-108">Remarks</span></span>  
 <span data-ttu-id="acc8b-109">`Skip`子句會讓查詢略過結果清單開頭的專案，並傳回剩餘的元素。</span><span class="sxs-lookup"><span data-stu-id="acc8b-109">The `Skip` clause causes a query to bypass elements at the beginning of a results list and return the remaining elements.</span></span> <span data-ttu-id="acc8b-110">要略過的元素數目是由參數所識別 `count` 。</span><span class="sxs-lookup"><span data-stu-id="acc8b-110">The number of elements to skip is identified by the `count` parameter.</span></span>  
  
 <span data-ttu-id="acc8b-111">您可以使用 `Skip` 子句搭配子句， `Take` 從查詢的任何區段傳回資料範圍。</span><span class="sxs-lookup"><span data-stu-id="acc8b-111">You can use the `Skip` clause with the `Take` clause to return a range of data from any segment of a query.</span></span> <span data-ttu-id="acc8b-112">若要這麼做，請將範圍的第一個元素的索引傳遞至 `Skip` 子句，並將範圍的大小傳遞給 `Take` 子句。</span><span class="sxs-lookup"><span data-stu-id="acc8b-112">To do this, pass the index of the first element of the range to the `Skip` clause and the size of the range to the `Take` clause.</span></span>  
  
 <span data-ttu-id="acc8b-113">當您 `Skip` 在查詢中使用子句時，您可能也需要確保以可讓 `Skip` 子句略過預期結果的順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="acc8b-113">When you use the `Skip` clause in a query, you may also need to ensure that the results are returned in an order that will enable the `Skip` clause to bypass the intended results.</span></span> <span data-ttu-id="acc8b-114">如需排序查詢結果的詳細資訊，請參閱[Order By 子句](order-by-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="acc8b-114">For more information about ordering query results, see [Order By Clause](order-by-clause.md).</span></span>  
  
 <span data-ttu-id="acc8b-115">視提供的條件而定，您可以使用 `SkipWhile` 子句來指定只忽略特定的元素。</span><span class="sxs-lookup"><span data-stu-id="acc8b-115">You can use the `SkipWhile` clause to specify that only certain elements are ignored, depending on a supplied condition.</span></span>  
  
## <a name="example"></a><span data-ttu-id="acc8b-116">範例</span><span class="sxs-lookup"><span data-stu-id="acc8b-116">Example</span></span>  
 <span data-ttu-id="acc8b-117">下列程式碼範例會 `Skip` 搭配子句使用子句 `Take` ，以從頁面中的查詢傳回資料。</span><span class="sxs-lookup"><span data-stu-id="acc8b-117">The following code example uses the `Skip` clause together with the `Take` clause to return data from a query in pages.</span></span> <span data-ttu-id="acc8b-118">函式會 `GetCustomers` 使用 `Skip` 子句來略過清單中的客戶，直到提供的起始索引值，並使用 `Take` 子句來傳回從該索引值開始的客戶頁面。</span><span class="sxs-lookup"><span data-stu-id="acc8b-118">The `GetCustomers` function uses the `Skip` clause to bypass the customers in the list until the supplied starting index value, and uses the `Take` clause to return a page of customers starting from that index value.</span></span>  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="acc8b-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="acc8b-119">See also</span></span>

- [<span data-ttu-id="acc8b-120">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="acc8b-120">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="acc8b-121">查詢</span><span class="sxs-lookup"><span data-stu-id="acc8b-121">Queries</span></span>](index.md)
- [<span data-ttu-id="acc8b-122">Select 子句</span><span class="sxs-lookup"><span data-stu-id="acc8b-122">Select Clause</span></span>](select-clause.md)
- [<span data-ttu-id="acc8b-123">From 子句</span><span class="sxs-lookup"><span data-stu-id="acc8b-123">From Clause</span></span>](from-clause.md)
- [<span data-ttu-id="acc8b-124">Order By 子句</span><span class="sxs-lookup"><span data-stu-id="acc8b-124">Order By Clause</span></span>](order-by-clause.md)
- [<span data-ttu-id="acc8b-125">Skip While 子句</span><span class="sxs-lookup"><span data-stu-id="acc8b-125">Skip While Clause</span></span>](skip-while-clause.md)
- [<span data-ttu-id="acc8b-126">Take 子句</span><span class="sxs-lookup"><span data-stu-id="acc8b-126">Take Clause</span></span>](take-clause.md)

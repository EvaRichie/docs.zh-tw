---
title: Let 子句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryLet
helpviewer_keywords:
- queries [Visual Basic], Let
- Let clause [Visual Basic]
- Let statement [Visual Basic]
ms.assetid: 981aa516-16eb-4c53-b1f1-5aa3e82f316e
ms.openlocfilehash: 4bf832651d9753c41ee5a02defec4adc55af1ff1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359757"
---
# <a name="let-clause-visual-basic"></a><span data-ttu-id="5debc-102">Let 子句 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="5debc-102">Let Clause (Visual Basic)</span></span>
<span data-ttu-id="5debc-103">計算值，並將它指派給查詢中的新變數。</span><span class="sxs-lookup"><span data-stu-id="5debc-103">Computes a value and assigns it to a new variable within the query.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5debc-104">語法</span><span class="sxs-lookup"><span data-stu-id="5debc-104">Syntax</span></span>  
  
```vb  
Let variable = expression [, ...]  
```  
  
## <a name="parts"></a><span data-ttu-id="5debc-105">組件</span><span class="sxs-lookup"><span data-stu-id="5debc-105">Parts</span></span>  
  
|<span data-ttu-id="5debc-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="5debc-106">Term</span></span>|<span data-ttu-id="5debc-107">定義</span><span class="sxs-lookup"><span data-stu-id="5debc-107">Definition</span></span>|  
|---|---|  
|`variable`|<span data-ttu-id="5debc-108">必要。</span><span class="sxs-lookup"><span data-stu-id="5debc-108">Required.</span></span> <span data-ttu-id="5debc-109">可以用來參考所提供運算式之結果的別名。</span><span class="sxs-lookup"><span data-stu-id="5debc-109">An alias that can be used to reference the results of the supplied expression.</span></span>|  
|`expression`|<span data-ttu-id="5debc-110">必要。</span><span class="sxs-lookup"><span data-stu-id="5debc-110">Required.</span></span> <span data-ttu-id="5debc-111">將評估並指派給指定之變數的運算式。</span><span class="sxs-lookup"><span data-stu-id="5debc-111">An expression that will be evaluated and assigned to the specified variable.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="5debc-112">備註</span><span class="sxs-lookup"><span data-stu-id="5debc-112">Remarks</span></span>  
 <span data-ttu-id="5debc-113">`Let`子句可讓您計算每個查詢結果的值，並使用別名來參考它們。</span><span class="sxs-lookup"><span data-stu-id="5debc-113">The `Let` clause enables you to compute values for each query result and reference them by using an alias.</span></span> <span data-ttu-id="5debc-114">別名可用於其他子句，例如 `Where` 子句。</span><span class="sxs-lookup"><span data-stu-id="5debc-114">The alias can be used in other clauses, such as the `Where` clause.</span></span> <span data-ttu-id="5debc-115">`Let`子句可讓您建立更容易閱讀的查詢語句，因為您可以為查詢中包含的運算式子句指定別名，並在每次使用 expression 子句時替換別名。</span><span class="sxs-lookup"><span data-stu-id="5debc-115">The `Let` clause enables you to create a query statement that is easier to read because you can specify an alias for an expression clause included in the query and substitute the alias each time the expression clause is used.</span></span>  
  
 <span data-ttu-id="5debc-116">您可以在子句中包含任意數目的 `variable` 和 `expression` 指派 `Let` 。</span><span class="sxs-lookup"><span data-stu-id="5debc-116">You can include any number of `variable` and `expression` assignments in the `Let` clause.</span></span> <span data-ttu-id="5debc-117">以逗號（，）分隔每個指派。</span><span class="sxs-lookup"><span data-stu-id="5debc-117">Separate each assignment with a comma (,).</span></span>  
  
## <a name="example"></a><span data-ttu-id="5debc-118">範例</span><span class="sxs-lookup"><span data-stu-id="5debc-118">Example</span></span>  
 <span data-ttu-id="5debc-119">下列程式碼範例使用 `Let` 子句來計算產品的10% 折扣。</span><span class="sxs-lookup"><span data-stu-id="5debc-119">The following code example uses the `Let` clause to compute a 10 percent discount on products.</span></span>  
  
 [!code-vb[VbSimpleQuerySamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#16)]  
  
## <a name="see-also"></a><span data-ttu-id="5debc-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5debc-120">See also</span></span>

- [<span data-ttu-id="5debc-121">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="5debc-121">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="5debc-122">查詢</span><span class="sxs-lookup"><span data-stu-id="5debc-122">Queries</span></span>](index.md)
- [<span data-ttu-id="5debc-123">Select 子句</span><span class="sxs-lookup"><span data-stu-id="5debc-123">Select Clause</span></span>](select-clause.md)
- [<span data-ttu-id="5debc-124">From 子句</span><span class="sxs-lookup"><span data-stu-id="5debc-124">From Clause</span></span>](from-clause.md)
- [<span data-ttu-id="5debc-125">Where 子句</span><span class="sxs-lookup"><span data-stu-id="5debc-125">Where Clause</span></span>](where-clause.md)

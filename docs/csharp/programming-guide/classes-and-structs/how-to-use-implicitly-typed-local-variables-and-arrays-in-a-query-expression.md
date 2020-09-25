---
title: '如何在查詢運算式中使用隱含類型區域變數和陣列-c # 程式設計手冊'
description: '使用 c # 中的隱含類型區域變數，讓編譯器判斷區域變數的型別。 您必須使用它們來儲存匿名型別。'
ms.date: 07/20/2015
helpviewer_keywords:
- implicitly-typed local variables [C#], how to use
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
ms.openlocfilehash: fcfb154f6abd90033ae57bb1543d0c891f6c5999
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91174195"
---
# <a name="how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression-c-programming-guide"></a><span data-ttu-id="44ca2-104">如何在查詢運算式中使用隱含類型區域變數和陣列 (c # 程式設計手冊) </span><span class="sxs-lookup"><span data-stu-id="44ca2-104">How to use implicitly typed local variables and arrays in a query expression (C# Programming Guide)</span></span>

<span data-ttu-id="44ca2-105">每次您希望編譯器判斷區域變數的類型時，可以使用隱含型別區域變數。</span><span class="sxs-lookup"><span data-stu-id="44ca2-105">You can use implicitly typed local variables whenever you want the compiler to determine the type of a local variable.</span></span> <span data-ttu-id="44ca2-106">您必須使用隱含型別區域變數來儲存查詢運算式中常用的匿名型別。</span><span class="sxs-lookup"><span data-stu-id="44ca2-106">You must use implicitly typed local variables to store anonymous types, which are often used in query expressions.</span></span> <span data-ttu-id="44ca2-107">下列範例說明在查詢中選擇性使用和必須使用隱含型別區域變數的情況。</span><span class="sxs-lookup"><span data-stu-id="44ca2-107">The following examples illustrate both optional and required uses of implicitly typed local variables in queries.</span></span>  
  
 <span data-ttu-id="44ca2-108">隱含型別區域變數是透過 [var](../../language-reference/keywords/var.md) 內容關鍵字宣告。</span><span class="sxs-lookup"><span data-stu-id="44ca2-108">Implicitly typed local variables are declared by using the [var](../../language-reference/keywords/var.md) contextual keyword.</span></span> <span data-ttu-id="44ca2-109">如需詳細資訊，請參閱[隱含型別區域變數](./implicitly-typed-local-variables.md)和[隱含型別陣列](../arrays/implicitly-typed-arrays.md)。</span><span class="sxs-lookup"><span data-stu-id="44ca2-109">For more information, see [Implicitly Typed Local Variables](./implicitly-typed-local-variables.md) and [Implicitly Typed Arrays](../arrays/implicitly-typed-arrays.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="44ca2-110">範例</span><span class="sxs-lookup"><span data-stu-id="44ca2-110">Example</span></span>  

 <span data-ttu-id="44ca2-111">下列範例顯示需要 `var` 關鍵字的常見案例：產生一系列匿名型別的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="44ca2-111">The following example shows a common scenario in which the `var` keyword is required: a query expression that produces a sequence of anonymous types.</span></span> <span data-ttu-id="44ca2-112">在此案例中，`foreach` 陳述式中的查詢變數和反覆運算變數都必須使用 `var` 來隱含輸入，因為您無法存取匿名型別的類型名稱。</span><span class="sxs-lookup"><span data-stu-id="44ca2-112">In this scenario, both the query variable and the iteration variable in the `foreach` statement must be implicitly typed by using `var` because you do not have access to a type name for the anonymous type.</span></span> <span data-ttu-id="44ca2-113">如需匿名型別的詳細資訊，請參閱[匿名型別](./anonymous-types.md)。</span><span class="sxs-lookup"><span data-stu-id="44ca2-113">For more information about anonymous types, see [Anonymous Types](./anonymous-types.md).</span></span>  
  
 [!code-csharp[csProgGuideLINQ#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#32)]  
  
## <a name="example"></a><span data-ttu-id="44ca2-114">範例</span><span class="sxs-lookup"><span data-stu-id="44ca2-114">Example</span></span>  

 <span data-ttu-id="44ca2-115">下列範例會在類似情況下使用 `var` 關鍵字，但可選擇是否使用 `var`。</span><span class="sxs-lookup"><span data-stu-id="44ca2-115">The following example uses the `var` keyword in a situation that is similar, but in which the use of `var` is optional.</span></span> <span data-ttu-id="44ca2-116">因為 `student.LastName` 是字串，所以執行查詢會傳回一系列的字串。</span><span class="sxs-lookup"><span data-stu-id="44ca2-116">Because `student.LastName` is a string, execution of the query returns a sequence of strings.</span></span> <span data-ttu-id="44ca2-117">因此，`queryID` 的類型會宣告為 `System.Collections.Generic.IEnumerable<string>`，而不是 `var`。</span><span class="sxs-lookup"><span data-stu-id="44ca2-117">Therefore, the type of `queryID` could be declared as `System.Collections.Generic.IEnumerable<string>` instead of `var`.</span></span> <span data-ttu-id="44ca2-118">關鍵字 `var` 是為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="44ca2-118">Keyword `var` is used for convenience.</span></span> <span data-ttu-id="44ca2-119">在範例中，`foreach` 陳述式中的反覆運算變數明確輸入為字串，但它可以改為使用 `var` 來宣告。</span><span class="sxs-lookup"><span data-stu-id="44ca2-119">In the example, the iteration variable in the `foreach` statement is explicitly typed as a string, but it could instead be declared by using `var`.</span></span> <span data-ttu-id="44ca2-120">因為反覆運算變數的類型不是匿名型別，所以使用 `var` 是選項而非需求。</span><span class="sxs-lookup"><span data-stu-id="44ca2-120">Because the type of the iteration variable is not an anonymous type, the use of `var` is an option, not a requirement.</span></span> <span data-ttu-id="44ca2-121">請記住，`var` 本身不是類型，而是編譯器用來推斷和指派類型的指令。</span><span class="sxs-lookup"><span data-stu-id="44ca2-121">Remember, `var` itself is not a type, but an instruction to the compiler to infer and assign the type.</span></span>  
  
 [!code-csharp[csProgGuideLINQ#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#33)]  
  
## <a name="see-also"></a><span data-ttu-id="44ca2-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="44ca2-122">See also</span></span>

- [<span data-ttu-id="44ca2-123">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="44ca2-123">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="44ca2-124">擴充方法</span><span class="sxs-lookup"><span data-stu-id="44ca2-124">Extension Methods</span></span>](./extension-methods.md)
- [<span data-ttu-id="44ca2-125">LINQ (Language-Integrated Query)</span><span class="sxs-lookup"><span data-stu-id="44ca2-125">LINQ (Language-Integrated Query)</span></span>](../../linq/index.md)
- [<span data-ttu-id="44ca2-126">無 功</span><span class="sxs-lookup"><span data-stu-id="44ca2-126">var</span></span>](../../language-reference/keywords/var.md)
- [<span data-ttu-id="44ca2-127">C# 中的 LINQ</span><span class="sxs-lookup"><span data-stu-id="44ca2-127">LINQ in C#</span></span>](../../linq/index.md)

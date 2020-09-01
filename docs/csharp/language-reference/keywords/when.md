---
description: when 內容關鍵字 - C# 參考
title: when 內容關鍵字 - C# 參考
ms.date: 03/07/2017
f1_keywords:
- when_CSharpKeyword
- when
helpviewer_keywords:
- when keyword [C#]
ms.assetid: dd543335-ae37-48ac-9560-bd5f047b9aea
ms.openlocfilehash: bd3a7beeb7d3c4b62d6b70e2b1c6f38ab4b6804f
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89138211"
---
# <a name="when-c-reference"></a><span data-ttu-id="18461-103">when (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="18461-103">when (C# Reference)</span></span>

<span data-ttu-id="18461-104">您可以使用 `when` 內容關鍵字來指定下列內容中的篩選準則：</span><span class="sxs-lookup"><span data-stu-id="18461-104">You can use the `when` contextual keyword to specify a filter condition in the following contexts:</span></span>

- <span data-ttu-id="18461-105">在 [try/catch](try-catch.md) 或 [try/catch/finally](try-catch-finally.md) 區塊的 `catch` 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="18461-105">In the `catch` statement of a [try/catch](try-catch.md) or [try/catch/finally](try-catch-finally.md) block.</span></span>
- <span data-ttu-id="18461-106">在 [switch](switch.md) 陳述式的 `case` 標籤中。</span><span class="sxs-lookup"><span data-stu-id="18461-106">In the `case` label of a [switch](switch.md) statement.</span></span>
- <span data-ttu-id="18461-107">[ `switch` 運算式](../operators/switch-expression.md)中的。</span><span class="sxs-lookup"><span data-stu-id="18461-107">In the [`switch` expression](../operators/switch-expression.md).</span></span>

## <a name="when-in-a-catch-statement"></a><span data-ttu-id="18461-108">`catch` 陳述式中的 `when`</span><span class="sxs-lookup"><span data-stu-id="18461-108">`when` in a `catch` statement</span></span>

<span data-ttu-id="18461-109">從 C# 6 開始，`when` 可以用於 `catch` 陳述式中，來指定必須符合才能執行特定例外狀況的處理常式的條件。</span><span class="sxs-lookup"><span data-stu-id="18461-109">Starting with C# 6, `when` can be used in a `catch` statement to specify a condition that must be true for the handler for a specific exception to execute.</span></span> <span data-ttu-id="18461-110">其語法如下：</span><span class="sxs-lookup"><span data-stu-id="18461-110">Its syntax is:</span></span>

```csharp
catch (ExceptionType [e]) when (expr)
```

<span data-ttu-id="18461-111">其中，*expr* 是可評估為布林值的運算式。</span><span class="sxs-lookup"><span data-stu-id="18461-111">where *expr* is an expression that evaluates to a Boolean value.</span></span> <span data-ttu-id="18461-112">如果它傳回 `true`，則會執行例外狀況處理常式；如果 `false` 則否。</span><span class="sxs-lookup"><span data-stu-id="18461-112">If it returns `true`, the exception handler executes; if `false`, it does not.</span></span>

<span data-ttu-id="18461-113">下列範例使用 `when` 關鍵字，根據例外狀況訊息的文字，有條件地執行 <xref:System.Net.Http.HttpRequestException> 的處理常式。</span><span class="sxs-lookup"><span data-stu-id="18461-113">The following example uses the `when` keyword to conditionally execute handlers for an <xref:System.Net.Http.HttpRequestException> depending on the text of the exception message.</span></span>

[!code-csharp[when-with-catch](~/samples/snippets/csharp/language-reference/keywords/when/catch.cs)]

## <a name="when-in-a-switch-statement"></a><span data-ttu-id="18461-114">`switch` 陳述式中的 `when`</span><span class="sxs-lookup"><span data-stu-id="18461-114">`when` in a `switch` statement</span></span>

<span data-ttu-id="18461-115">從 C# 7.0 開始，`case` 標籤不再需要互斥，而且 `case` 標籤在 `switch` 陳述式中的出現順序可以判斷要執行的 switch 區塊。</span><span class="sxs-lookup"><span data-stu-id="18461-115">Starting with C# 7.0, `case` labels no longer need be mutually exclusive, and the order in which `case` labels appear in a `switch` statement can determine which switch block executes.</span></span> <span data-ttu-id="18461-116">`when` 關鍵字可以用來指定篩選條件，使其相關聯的 case 標籤只有在篩選條件也是為 true 時才為 true。</span><span class="sxs-lookup"><span data-stu-id="18461-116">The `when` keyword can be used to specify a filter condition that causes its associated case label to be true only if the filter condition is also true.</span></span> <span data-ttu-id="18461-117">其語法如下：</span><span class="sxs-lookup"><span data-stu-id="18461-117">Its syntax is:</span></span>

```csharp
case (expr) when (when-condition):
```

<span data-ttu-id="18461-118">其中，*expr* 是與比對運算式進行比較的常數模式或類型模式，而 *when-condition* 是任何布林運算式。</span><span class="sxs-lookup"><span data-stu-id="18461-118">where *expr* is a constant pattern or type pattern that is compared to the match expression, and *when-condition* is any Boolean expression.</span></span>

<span data-ttu-id="18461-119">下列範例使用 `when` 關鍵字來測試是否有具有零區域的 `Shape` 物件，以及測試是否有具有大於零的區域的各種 `Shape` 物件。</span><span class="sxs-lookup"><span data-stu-id="18461-119">The following example uses the `when` keyword to test for `Shape` objects that have an area of zero, as well as to test for a variety of `Shape` objects that have an area greater than zero.</span></span>

[!code-csharp[when-with-case#1](~/samples/snippets/csharp/language-reference/keywords/when/when.cs#1)]

## <a name="see-also"></a><span data-ttu-id="18461-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="18461-120">See also</span></span>

- [<span data-ttu-id="18461-121">switch 陳述式</span><span class="sxs-lookup"><span data-stu-id="18461-121">switch statement</span></span>](switch.md)
- [<span data-ttu-id="18461-122">try/catch 陳述式</span><span class="sxs-lookup"><span data-stu-id="18461-122">try/catch statement</span></span>](try-catch.md)
- [<span data-ttu-id="18461-123">try/catch/finally 語句</span><span class="sxs-lookup"><span data-stu-id="18461-123">try/catch/finally statement</span></span>](try-catch-finally.md)

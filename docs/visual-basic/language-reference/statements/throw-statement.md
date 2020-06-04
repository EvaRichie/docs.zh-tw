---
title: Throw 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.Throw
helpviewer_keywords:
- structured exception handling, throw statements
- try-catch exception handling, throw statements
- throw statement [Visual Basic], about throw statements
- throwing exceptions, throw statement
- exception handling, throw statement
- On Error statement [Visual Basic], throwing exceptions
- throwing exceptions
- exception handling, unstructured
- throw statement [Visual Basic]
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
ms.openlocfilehash: 95572b1739490e90f53da6b6ec283bfb532c46d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404131"
---
# <a name="throw-statement-visual-basic"></a><span data-ttu-id="3a0d9-102">Throw 陳述式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3a0d9-102">Throw Statement (Visual Basic)</span></span>

<span data-ttu-id="3a0d9-103">在程式中擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-103">Throws an exception within a procedure.</span></span>

## <a name="syntax"></a><span data-ttu-id="3a0d9-104">語法</span><span class="sxs-lookup"><span data-stu-id="3a0d9-104">Syntax</span></span>

```vb
Throw [ expression ]
```

## <a name="part"></a><span data-ttu-id="3a0d9-105">部分</span><span class="sxs-lookup"><span data-stu-id="3a0d9-105">Part</span></span>

`expression`\
<span data-ttu-id="3a0d9-106">提供要擲回之例外狀況的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-106">Provides information about the exception to be thrown.</span></span> <span data-ttu-id="3a0d9-107">如果位於 `Catch` 語句中，則為選擇性，否則為必要項。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-107">Optional when residing in a `Catch` statement, otherwise required.</span></span>

## <a name="remarks"></a><span data-ttu-id="3a0d9-108">備註</span><span class="sxs-lookup"><span data-stu-id="3a0d9-108">Remarks</span></span>

<span data-ttu-id="3a0d9-109">`Throw`語句會擲回例外狀況，您可以處理結構化例外狀況處理常式代碼（ `Try` ... `Catch`...`Finally`)或非結構化例外狀況處理常式代碼（ `On Error GoTo` ）。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-109">The `Throw` statement throws an exception that you can handle with structured exception-handling code (`Try`...`Catch`...`Finally`) or unstructured exception-handling code (`On Error GoTo`).</span></span> <span data-ttu-id="3a0d9-110">您可以使用 `Throw` 語句來攔截程式碼內的錯誤，因為 Visual Basic 會向上移動呼叫堆疊，直到找到適當的例外狀況處理常式代碼為止。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-110">You can use the `Throw` statement to trap errors within your code because Visual Basic moves up the call stack until it finds the appropriate exception-handling code.</span></span>

<span data-ttu-id="3a0d9-111">`Throw`沒有運算式的語句只能在語句中使用 `Catch` ，在此情況下，語句會重新擲回目前正由語句處理的例外狀況 `Catch` 。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-111">A `Throw` statement with no expression can only be used in a `Catch` statement, in which case the statement rethrows the exception currently being handled by the `Catch` statement.</span></span>

<span data-ttu-id="3a0d9-112">`Throw`語句會重設例外狀況的呼叫堆疊 `expression` 。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-112">The `Throw` statement resets the call stack for the `expression` exception.</span></span> <span data-ttu-id="3a0d9-113">如果 `expression` 未提供，則會將呼叫堆疊保持不變。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-113">If `expression` is not provided, the call stack is left unchanged.</span></span> <span data-ttu-id="3a0d9-114">您可以透過屬性存取例外狀況的呼叫堆疊 <xref:System.Exception.StackTrace%2A> 。</span><span class="sxs-lookup"><span data-stu-id="3a0d9-114">You can access the call stack for the exception through the <xref:System.Exception.StackTrace%2A> property.</span></span>

## <a name="example"></a><span data-ttu-id="3a0d9-115">範例</span><span class="sxs-lookup"><span data-stu-id="3a0d9-115">Example</span></span>

<span data-ttu-id="3a0d9-116">下列程式碼會使用 `Throw` 語句來擲回例外狀況：</span><span class="sxs-lookup"><span data-stu-id="3a0d9-116">The following code uses the `Throw` statement to throw an exception:</span></span>

[!code-vb[VbVbalrStatements#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#84)]

## <a name="see-also"></a><span data-ttu-id="3a0d9-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3a0d9-117">See also</span></span>

- [<span data-ttu-id="3a0d9-118">Try...Catch...Finally 陳述式</span><span class="sxs-lookup"><span data-stu-id="3a0d9-118">Try...Catch...Finally Statement</span></span>](try-catch-finally-statement.md)
- [<span data-ttu-id="3a0d9-119">On Error 陳述式</span><span class="sxs-lookup"><span data-stu-id="3a0d9-119">On Error Statement</span></span>](on-error-statement.md)

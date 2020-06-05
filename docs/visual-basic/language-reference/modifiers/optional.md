---
title: 選擇性
ms.date: 07/20/2015
f1_keywords:
- vb.Optional
- vb.optional
helpviewer_keywords:
- Optional keyword [Visual Basic], contexts
- Optional keyword [Visual Basic]
ms.assetid: 4571ce88-a539-4115-b230-54eb277c6aa7
ms.openlocfilehash: c46d06dba61158d7362d736731161be306af3f10
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392141"
---
# <a name="optional-visual-basic"></a><span data-ttu-id="c98ba-102">Optional (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c98ba-102">Optional (Visual Basic)</span></span>

<span data-ttu-id="c98ba-103">指定在呼叫程式時，可以省略程式引數。</span><span class="sxs-lookup"><span data-stu-id="c98ba-103">Specifies that a procedure argument can be omitted when the procedure is called.</span></span>

## <a name="remarks"></a><span data-ttu-id="c98ba-104">備註</span><span class="sxs-lookup"><span data-stu-id="c98ba-104">Remarks</span></span>

<span data-ttu-id="c98ba-105">針對每個選擇性參數，您必須指定常數運算式做為該參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="c98ba-105">For each optional parameter, you must specify a constant expression as the default value of that parameter.</span></span> <span data-ttu-id="c98ba-106">如果運算式評估為 [[無](../nothing.md)]，則會使用 value 資料類型的預設值做為參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="c98ba-106">If the expression evaluates to [Nothing](../nothing.md), the default value of the value data type is used as the default value of the parameter.</span></span>

<span data-ttu-id="c98ba-107">如果參數清單包含選擇性參數，則後面的每個參數也必須是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="c98ba-107">If the parameter list contains an optional parameter, every parameter that follows it must also be optional.</span></span>

<span data-ttu-id="c98ba-108">`Optional` 修飾詞可用於以下內容：</span><span class="sxs-lookup"><span data-stu-id="c98ba-108">The `Optional` modifier can be used in these contexts:</span></span>

- [<span data-ttu-id="c98ba-109">Declare Statement</span><span class="sxs-lookup"><span data-stu-id="c98ba-109">Declare Statement</span></span>](../statements/declare-statement.md)

- [<span data-ttu-id="c98ba-110">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="c98ba-110">Function Statement</span></span>](../statements/function-statement.md)

- [<span data-ttu-id="c98ba-111">Property Statement</span><span class="sxs-lookup"><span data-stu-id="c98ba-111">Property Statement</span></span>](../statements/property-statement.md)

- [<span data-ttu-id="c98ba-112">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="c98ba-112">Sub Statement</span></span>](../statements/sub-statement.md)

> [!NOTE]
> <span data-ttu-id="c98ba-113">呼叫含有或不含選擇性參數的程式時，您可以依位置或名稱傳遞引數。</span><span class="sxs-lookup"><span data-stu-id="c98ba-113">When calling a procedure with or without optional parameters, you can pass arguments by position or by name.</span></span> <span data-ttu-id="c98ba-114">如需詳細資訊，請參閱[依位置和名稱傳遞引數](../../programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)。</span><span class="sxs-lookup"><span data-stu-id="c98ba-114">For more information, see [Passing Arguments by Position and by Name](../../programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c98ba-115">您也可以使用多載來定義具有選擇性參數的程式。</span><span class="sxs-lookup"><span data-stu-id="c98ba-115">You can also define a procedure with optional parameters by using overloading.</span></span> <span data-ttu-id="c98ba-116">如果您有一個選擇性參數，您可以定義程式的兩個多載版本，一個會接受參數，另一個則不會。</span><span class="sxs-lookup"><span data-stu-id="c98ba-116">If you have one optional parameter, you can define two overloaded versions of the procedure, one that accepts the parameter and one that doesn’t.</span></span> <span data-ttu-id="c98ba-117">如需詳細資訊，請參閱 [Procedure Overloading](../../programming-guide/language-features/procedures/procedure-overloading.md)。</span><span class="sxs-lookup"><span data-stu-id="c98ba-117">For more information, see [Procedure Overloading](../../programming-guide/language-features/procedures/procedure-overloading.md).</span></span>

## <a name="example"></a><span data-ttu-id="c98ba-118">範例</span><span class="sxs-lookup"><span data-stu-id="c98ba-118">Example</span></span>

<span data-ttu-id="c98ba-119">下列範例會定義具有選擇性參數的程式。</span><span class="sxs-lookup"><span data-stu-id="c98ba-119">The following example defines a procedure that has an optional parameter.</span></span>

```vb
Public Function FindMatches(ByRef values As List(Of String),
                            ByVal searchString As String,
                            Optional ByVal matchCase As Boolean = False) As List(Of String)

    Dim results As IEnumerable(Of String)

    If matchCase Then
        results = From v In values
                  Where v.Contains(searchString)
    Else
        results = From v In values
                  Where UCase(v).Contains(UCase(searchString))
    End If

    Return results.ToList()
End Function
```

## <a name="example"></a><span data-ttu-id="c98ba-120">範例</span><span class="sxs-lookup"><span data-stu-id="c98ba-120">Example</span></span>

<span data-ttu-id="c98ba-121">下列範例示範如何呼叫具有由位置傳遞的引數，以及以名稱傳遞之引數的程式。</span><span class="sxs-lookup"><span data-stu-id="c98ba-121">The following example demonstrates how to call a procedure with arguments passed by position and with arguments passed by name.</span></span> <span data-ttu-id="c98ba-122">此程式有兩個選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="c98ba-122">The procedure has two optional parameters.</span></span>

[!code-vb[VbVbalrKeywords#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class8.vb#21)]

## <a name="see-also"></a><span data-ttu-id="c98ba-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c98ba-123">See also</span></span>

- [<span data-ttu-id="c98ba-124">參數清單</span><span class="sxs-lookup"><span data-stu-id="c98ba-124">Parameter List</span></span>](../statements/parameter-list.md)
- [<span data-ttu-id="c98ba-125">選擇性參數</span><span class="sxs-lookup"><span data-stu-id="c98ba-125">Optional Parameters</span></span>](../../programming-guide/language-features/procedures/optional-parameters.md)
- [<span data-ttu-id="c98ba-126">關鍵字</span><span class="sxs-lookup"><span data-stu-id="c98ba-126">Keywords</span></span>](../keywords/index.md)

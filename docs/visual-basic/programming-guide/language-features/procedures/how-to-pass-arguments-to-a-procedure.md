---
title: 如何：將引數傳遞至程序
ms.date: 07/20/2015
helpviewer_keywords:
- arguments [Visual Basic], passing to procedures
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], calling
- argument passing [Visual Basic], procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
ms.openlocfilehash: 816d6388a0dbb7ae346074d258ff651c793c5e0e
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071504"
---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a><span data-ttu-id="ae1c3-102">如何：將引數傳遞至程序 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ae1c3-102">How to: Pass Arguments to a Procedure (Visual Basic)</span></span>

<span data-ttu-id="ae1c3-103">當您呼叫程式時，請以括弧括住具有引數清單的程式名稱。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-103">When you call a procedure, you follow the procedure name with an argument list in parentheses.</span></span> <span data-ttu-id="ae1c3-104">您提供的引數會對應至程式所定義的每個必要參數，而且您可以選擇性地提供參數的引數 `Optional` 。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-104">You supply an argument corresponding to every required parameter the procedure defines, and you can optionally supply arguments to the `Optional` parameters.</span></span> <span data-ttu-id="ae1c3-105">如果您未 `Optional` 在呼叫中提供參數，而且您要提供任何後續的引數，則必須包含逗號，以將其位置標示在引數清單中。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-105">If you do not supply an `Optional` parameter in the call, you must include a comma to mark its place in the argument list if you are supplying any subsequent arguments.</span></span>  
  
 <span data-ttu-id="ae1c3-106">如果您想要傳遞資料類型的引數與其對應參數的引數（例如）， `Byte` `String` 您可以將「類型檢查參數」 ([Option Strict 語句](../../../language-reference/statements/option-strict-statement.md)) 設定為 `Off` 。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-106">If you intend to pass an argument of a data type different from that of its corresponding parameter, such as `Byte` to `String`, you can set the type-checking switch ([Option Strict Statement](../../../language-reference/statements/option-strict-statement.md)) to `Off`.</span></span> <span data-ttu-id="ae1c3-107">如果 `Option Strict` 是 `On` ，您必須使用擴輾轉換或明確轉換關鍵字。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-107">If `Option Strict` is `On`, you must use either widening conversions or explicit conversion keywords.</span></span> <span data-ttu-id="ae1c3-108">如需詳細資訊，請參閱 [擴展和縮小轉換](../data-types/widening-and-narrowing-conversions.md) 和 [類型轉換函數](../../../language-reference/functions/type-conversion-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-108">For more information, see [Widening and Narrowing Conversions](../data-types/widening-and-narrowing-conversions.md) and [Type Conversion Functions](../../../language-reference/functions/type-conversion-functions.md).</span></span>  
  
 <span data-ttu-id="ae1c3-109">如需詳細資訊，請參閱程式 [參數和引數](./procedure-parameters-and-arguments.md)。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-109">For more information, see [Procedure Parameters and Arguments](./procedure-parameters-and-arguments.md).</span></span>  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a><span data-ttu-id="ae1c3-110">將一或多個引數傳遞至程式</span><span class="sxs-lookup"><span data-stu-id="ae1c3-110">To pass one or more arguments to a procedure</span></span>  
  
1. <span data-ttu-id="ae1c3-111">在呼叫語句中，在程式名稱後面加上括弧。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-111">In the calling statement, follow the procedure name with parentheses.</span></span>  
  
2. <span data-ttu-id="ae1c3-112">在括弧內放置引數清單。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-112">Inside the parentheses, put an argument list.</span></span> <span data-ttu-id="ae1c3-113">針對程式定義的每個必要參數包含引數，並以逗號分隔引數。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-113">Include an argument for each required parameter the procedure defines, and separate the arguments with commas.</span></span>  
  
3. <span data-ttu-id="ae1c3-114">請確定每個引數都是有效的運算式，其評估結果為可轉換成程式為對應參數定義之類型的資料類型。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-114">Make sure each argument is a valid expression that evaluates to a data type convertible to the type the procedure defines for the corresponding parameter.</span></span>  
  
4. <span data-ttu-id="ae1c3-115">如果參數定義為 [選擇性](../../../language-reference/modifiers/optional.md)，則可以將它包含在引數清單中，或將其省略。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-115">If a parameter is defined as [Optional](../../../language-reference/modifiers/optional.md), you can either include it in the argument list or omit it.</span></span> <span data-ttu-id="ae1c3-116">如果您省略它，程式會使用針對該參數定義的預設值。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-116">If you omit it, the procedure uses the default value defined for that parameter.</span></span>  
  
5. <span data-ttu-id="ae1c3-117">如果您省略參數的引數 `Optional` ，而且在參數清單中有另一個參數，您可以在引數清單中將省略引數的位置標記為額外的逗號。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-117">If you omit an argument for an `Optional` parameter and there is another parameter after it in the parameter list, you can mark the place of the omitted argument by an extra comma in the argument list.</span></span>  
  
     <span data-ttu-id="ae1c3-118">下列範例會呼叫 Visual Basic <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 函數。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-118">The following example calls the Visual Basic <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> function.</span></span>  
  
     [!code-vb[VbVbcnProcedures#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#34)]  
  
     <span data-ttu-id="ae1c3-119">上述範例會提供必要的第一個引數，也就是要顯示的訊息字串。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-119">The preceding example supplies the required first argument, which is the message string to be displayed.</span></span> <span data-ttu-id="ae1c3-120">它會省略選擇性第二個參數的引數，以指定要在訊息方塊上顯示的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-120">It omits an argument for the optional second parameter, which specifies the buttons to be displayed on the message box.</span></span> <span data-ttu-id="ae1c3-121">因為呼叫未提供值，所以會 `MsgBox` 使用預設值，此值 `MsgBoxStyle.OKOnly` 只會顯示 **[確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-121">Because the call does not supply a value, `MsgBox` uses the default value, `MsgBoxStyle.OKOnly`, which displays only an **OK** button.</span></span>  
  
     <span data-ttu-id="ae1c3-122">引數清單中的第二個逗號會標示省略的第二個引數，而最後一個字串會傳遞給的選擇性第三個參數 `MsgBox` ，也就是要顯示在標題列中的文字。</span><span class="sxs-lookup"><span data-stu-id="ae1c3-122">The second comma in the argument list marks the place of the omitted second argument, and the last string is passed to the optional third parameter of `MsgBox`, which is the text to be displayed in the title bar.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ae1c3-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ae1c3-123">See also</span></span>

- [<span data-ttu-id="ae1c3-124">Sub 程序</span><span class="sxs-lookup"><span data-stu-id="ae1c3-124">Sub Procedures</span></span>](./sub-procedures.md)
- [<span data-ttu-id="ae1c3-125">Function 程序</span><span class="sxs-lookup"><span data-stu-id="ae1c3-125">Function Procedures</span></span>](./function-procedures.md)
- [<span data-ttu-id="ae1c3-126">屬性程序</span><span class="sxs-lookup"><span data-stu-id="ae1c3-126">Property Procedures</span></span>](./property-procedures.md)
- [<span data-ttu-id="ae1c3-127">運算子程序</span><span class="sxs-lookup"><span data-stu-id="ae1c3-127">Operator Procedures</span></span>](./operator-procedures.md)
- [<span data-ttu-id="ae1c3-128">如何：定義程序的參數</span><span class="sxs-lookup"><span data-stu-id="ae1c3-128">How to: Define a Parameter for a Procedure</span></span>](./how-to-define-a-parameter-for-a-procedure.md)
- [<span data-ttu-id="ae1c3-129">以傳值和傳址方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="ae1c3-129">Passing Arguments by Value and by Reference</span></span>](./passing-arguments-by-value-and-by-reference.md)
- [<span data-ttu-id="ae1c3-130">遞迴程序</span><span class="sxs-lookup"><span data-stu-id="ae1c3-130">Recursive Procedures</span></span>](./recursive-procedures.md)
- [<span data-ttu-id="ae1c3-131">程序多載化</span><span class="sxs-lookup"><span data-stu-id="ae1c3-131">Procedure Overloading</span></span>](./procedure-overloading.md)
- [<span data-ttu-id="ae1c3-132">物件和類別</span><span class="sxs-lookup"><span data-stu-id="ae1c3-132">Objects and Classes</span></span>](../objects-and-classes/index.md)
- [<span data-ttu-id="ae1c3-133">物件導向程式設計 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ae1c3-133">Object-Oriented Programming (Visual Basic)</span></span>](../../concepts/object-oriented-programming.md)

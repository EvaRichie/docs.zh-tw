---
title: 寬鬆委派轉換
ms.date: 07/20/2015
helpviewer_keywords:
- relaxed delegate conversion [Visual Basic]
- delegates [Visual Basic], relaxed conversion
- conversions [Visual Basic], relaxed delegate
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
ms.openlocfilehash: a581ffae77c496908d2e4e38df53491a54ae2ab8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410666"
---
# <a name="relaxed-delegate-conversion-visual-basic"></a><span data-ttu-id="f9fff-102">寬鬆委派轉換 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f9fff-102">Relaxed Delegate Conversion (Visual Basic)</span></span>
<span data-ttu-id="f9fff-103">寬鬆委派轉換可讓您將子函數和函式指派給委派或處理常式，即使其簽章不相同也是一樣。</span><span class="sxs-lookup"><span data-stu-id="f9fff-103">Relaxed delegate conversion enables you to assign subs and functions to delegates or handlers even when their signatures are not identical.</span></span> <span data-ttu-id="f9fff-104">因此，系結至委派會與已允許方法調用的系結一致。</span><span class="sxs-lookup"><span data-stu-id="f9fff-104">Therefore, binding to delegates becomes consistent with the binding already allowed for method invocations.</span></span>  
  
## <a name="parameters-and-return-type"></a><span data-ttu-id="f9fff-105">參數和傳回型別</span><span class="sxs-lookup"><span data-stu-id="f9fff-105">Parameters and Return Type</span></span>  
 <span data-ttu-id="f9fff-106">為了取代確切的簽章相符，當設定為時，寬鬆轉換需要符合下列條件 `Option Strict` `On` ：</span><span class="sxs-lookup"><span data-stu-id="f9fff-106">In place of exact signature match, relaxed conversion requires that the following conditions be met when `Option Strict` is set to `On`:</span></span>  
  
- <span data-ttu-id="f9fff-107">擴輾轉換必須存在於每個委派參數的資料類型，以及所指派函式之對應參數的資料類型 `Sub` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-107">A widening conversion must exist from the data type of each delegate parameter to the data type of the corresponding parameter of the assigned function or `Sub`.</span></span> <span data-ttu-id="f9fff-108">在下列範例中，委派 `Del1` 有一個參數，也就是 `Integer` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-108">In the following example, the delegate `Del1` has one parameter, an `Integer`.</span></span> <span data-ttu-id="f9fff-109">`m`指派的 lambda 運算式中的參數必須具有從進行擴輾轉換的資料類型 `Integer` ，例如 `Long` 或 `Double` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-109">Parameter `m` in the assigned lambda expressions must have a data type for which there is a widening conversion from `Integer`, such as `Long` or `Double`.</span></span>  
  
     [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
     [!code-vb[VbVbalrRelaxedDelegates#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#2)]  
  
     <span data-ttu-id="f9fff-110">只有當設定為時，才允許縮小轉換 `Option Strict` `Off` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-110">Narrowing conversions are permitted only when `Option Strict` is set to `Off`.</span></span>  
  
     [!code-vb[VbVbalrRelaxedDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#8)]  
  
- <span data-ttu-id="f9fff-111">擴輾轉換必須與指派之函式的傳回型別或委派的傳回型別有相反的方向 `Sub` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-111">A widening conversion must exist in the opposite direction from the return type of the assigned function or `Sub` to the return type of the delegate.</span></span> <span data-ttu-id="f9fff-112">在下列範例中，每個指派的 lambda 運算式的主體都必須評估為擴大為的資料類型， `Integer` 因為的傳回類型 `del1` 是 `Integer` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-112">In the following examples, the body of each assigned lambda expression must evaluate to a data type that widens to `Integer` because the return type of `del1` is `Integer`.</span></span>  
  
     [!code-vb[VbVbalrRelaxedDelegates#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#3)]  
  
 <span data-ttu-id="f9fff-113">如果 `Option Strict` 設定為 `Off` ，則會同時移除這兩個方向的擴展限制。</span><span class="sxs-lookup"><span data-stu-id="f9fff-113">If `Option Strict` is set to `Off`, the widening restriction is removed in both directions.</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#4)]  
  
## <a name="omitting-parameter-specifications"></a><span data-ttu-id="f9fff-114">省略參數規格</span><span class="sxs-lookup"><span data-stu-id="f9fff-114">Omitting Parameter Specifications</span></span>  
 <span data-ttu-id="f9fff-115">寬鬆委派也可以讓您完全省略指派方法中的參數規格：</span><span class="sxs-lookup"><span data-stu-id="f9fff-115">Relaxed delegates also allow you to completely omit parameter specifications in the assigned method:</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#5)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#6)]  
  
 <span data-ttu-id="f9fff-116">請注意，您不能指定某些參數，並省略其他參數。</span><span class="sxs-lookup"><span data-stu-id="f9fff-116">Note that you cannot specify some parameters and omit others.</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#15)]  
  
 <span data-ttu-id="f9fff-117">省略參數的功能在定義事件處理常式（其中牽涉到數個複雜參數）的情況下很有説明。</span><span class="sxs-lookup"><span data-stu-id="f9fff-117">The ability to omit parameters is helpful in a situation such as defining an event handler, where several complex parameters are involved.</span></span> <span data-ttu-id="f9fff-118">不會使用某些事件處理常式的引數。</span><span class="sxs-lookup"><span data-stu-id="f9fff-118">The arguments to some event handlers are not used.</span></span> <span data-ttu-id="f9fff-119">相反地，處理常式會直接存取已註冊事件之控制項的狀態，並忽略引數。</span><span class="sxs-lookup"><span data-stu-id="f9fff-119">Instead, the handler directly accesses the state of the control on which the event is registered, and ignores the arguments.</span></span> <span data-ttu-id="f9fff-120">寬鬆的委派可讓您在沒有不明確的結果時，省略這類宣告中的引數。</span><span class="sxs-lookup"><span data-stu-id="f9fff-120">Relaxed delegates allow you to omit the arguments in such declarations when no ambiguities result.</span></span> <span data-ttu-id="f9fff-121">在下列範例中，可以將完整指定的方法 `OnClick` 改寫為 `RelaxedOnClick` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-121">In the following example, the fully specified method `OnClick` can be rewritten as `RelaxedOnClick`.</span></span>  
  
```vb  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## <a name="addressof-examples"></a><span data-ttu-id="f9fff-122">AddressOf 範例</span><span class="sxs-lookup"><span data-stu-id="f9fff-122">AddressOf Examples</span></span>  
 <span data-ttu-id="f9fff-123">在先前的範例中，會使用 Lambda 運算式，讓型別關聯性變得更容易查看。</span><span class="sxs-lookup"><span data-stu-id="f9fff-123">Lambda expressions are used in the previous examples to make the type relationships easy to see.</span></span> <span data-ttu-id="f9fff-124">不過，使用、或的委派指派也允許相同的 `AddressOf` relaxations `Handles` `AddHandler` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-124">However, the same relaxations are permitted for delegate assignments that use `AddressOf`, `Handles`, or `AddHandler`.</span></span>  
  
 <span data-ttu-id="f9fff-125">在下列範例中，函數 `f1` 、 `f2` 、 `f3` 和都 `f4` 可以指派給 `Del1` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-125">In the following example, functions `f1`, `f2`, `f3`, and `f4` can all be assigned to `Del1`.</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#7)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#9)]  
  
 <span data-ttu-id="f9fff-126">只有當設定為時，下列範例才有效 `Option Strict` `Off` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-126">The following example is valid only when `Option Strict` is set to `Off`.</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#14)]  
  
## <a name="dropping-function-returns"></a><span data-ttu-id="f9fff-127">卸載函式傳回</span><span class="sxs-lookup"><span data-stu-id="f9fff-127">Dropping Function Returns</span></span>  
 <span data-ttu-id="f9fff-128">寬鬆委派轉換可讓您將函式指派給 `Sub` 委派，有效地忽略函數的傳回值。</span><span class="sxs-lookup"><span data-stu-id="f9fff-128">Relaxed delegate conversion enables you to assign a function to a `Sub` delegate, effectively ignoring the return value of the function.</span></span> <span data-ttu-id="f9fff-129">不過，您無法將指派給 `Sub` 函數委派。</span><span class="sxs-lookup"><span data-stu-id="f9fff-129">However, you cannot assign a `Sub` to a function delegate.</span></span> <span data-ttu-id="f9fff-130">在下列範例中，會將函式的位址 `doubler` 指派給 `Sub` 委派 `Del3` 。</span><span class="sxs-lookup"><span data-stu-id="f9fff-130">In the following example, the address of function `doubler` is assigned to `Sub` delegate `Del3`.</span></span>  
  
 [!code-vb[VbVbalrRelaxedDelegates#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#10)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#11)]  
  
## <a name="see-also"></a><span data-ttu-id="f9fff-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f9fff-131">See also</span></span>

- [<span data-ttu-id="f9fff-132">Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="f9fff-132">Lambda Expressions</span></span>](../procedures/lambda-expressions.md)
- [<span data-ttu-id="f9fff-133">Widening and Narrowing Conversions</span><span class="sxs-lookup"><span data-stu-id="f9fff-133">Widening and Narrowing Conversions</span></span>](../data-types/widening-and-narrowing-conversions.md)
- [<span data-ttu-id="f9fff-134">委派</span><span class="sxs-lookup"><span data-stu-id="f9fff-134">Delegates</span></span>](index.md)
- [<span data-ttu-id="f9fff-135">如何：在 Visual Basic 中將程序傳遞至其他程序</span><span class="sxs-lookup"><span data-stu-id="f9fff-135">How to: Pass Procedures to Another Procedure in Visual Basic</span></span>](how-to-pass-procedures-to-another-procedure.md)
- [<span data-ttu-id="f9fff-136">區域型別推斷</span><span class="sxs-lookup"><span data-stu-id="f9fff-136">Local Type Inference</span></span>](../variables/local-type-inference.md)
- [<span data-ttu-id="f9fff-137">Long</span><span class="sxs-lookup"><span data-stu-id="f9fff-137">Option Strict Statement</span></span>](../../../language-reference/statements/option-strict-statement.md)

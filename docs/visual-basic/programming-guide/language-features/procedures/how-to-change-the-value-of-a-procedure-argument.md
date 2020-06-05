---
title: 如何：變更程序引數的值
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- arguments [Visual Basic], passing by reference
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
ms.openlocfilehash: 46cf9062d01e248b6e90882a923a48210780f7f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388500"
---
# <a name="how-to-change-the-value-of-a-procedure-argument-visual-basic"></a><span data-ttu-id="0573d-102">如何：變更程序引數的值 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0573d-102">How to: Change the Value of a Procedure Argument (Visual Basic)</span></span>
<span data-ttu-id="0573d-103">當您呼叫程式時，您所提供的每個引數都會對應至程式中所定義的其中一個參數。</span><span class="sxs-lookup"><span data-stu-id="0573d-103">When you call a procedure, each argument you supply corresponds to one of the parameters defined in the procedure.</span></span> <span data-ttu-id="0573d-104">在某些情況下，程式碼可以變更呼叫程式碼中引數的基礎值。</span><span class="sxs-lookup"><span data-stu-id="0573d-104">In some cases, the procedure code can change the value underlying an argument in the calling code.</span></span> <span data-ttu-id="0573d-105">在其他情況下，程式只會變更其引數的本機複本。</span><span class="sxs-lookup"><span data-stu-id="0573d-105">In other cases, the procedure can change only its local copy of an argument.</span></span>  
  
 <span data-ttu-id="0573d-106">當您呼叫程式時，Visual Basic 會為每個傳遞[ByVal](../../../language-reference/modifiers/byval.md)的引數建立本機複本。</span><span class="sxs-lookup"><span data-stu-id="0573d-106">When you call the procedure, Visual Basic makes a local copy of every argument that is passed [ByVal](../../../language-reference/modifiers/byval.md).</span></span> <span data-ttu-id="0573d-107">對於傳遞了[ByRef](../../../language-reference/modifiers/byref.md)的每個引數，Visual Basic 會提供程式碼直接參考呼叫程式碼中引數的基礎程式設計項目。</span><span class="sxs-lookup"><span data-stu-id="0573d-107">For each argument passed [ByRef](../../../language-reference/modifiers/byref.md), Visual Basic gives the procedure code a direct reference to the programming element underlying the argument in the calling code.</span></span>  
  
 <span data-ttu-id="0573d-108">如果呼叫程式碼中的基礎元素是可修改的元素，且已傳遞引數 `ByRef` ，程式碼就可以使用直接參考來變更呼叫程式碼中的元素值。</span><span class="sxs-lookup"><span data-stu-id="0573d-108">If the underlying element in the calling code is a modifiable element and the argument is passed `ByRef`, the procedure code can use the direct reference to change the element's value in the calling code.</span></span>  
  
## <a name="changing-the-underlying-value"></a><span data-ttu-id="0573d-109">變更基礎值</span><span class="sxs-lookup"><span data-stu-id="0573d-109">Changing the Underlying Value</span></span>  
  
#### <a name="to-change-the-underlying-value-of-a-procedure-argument-in-the-calling-code"></a><span data-ttu-id="0573d-110">若要在呼叫程式碼中變更程式引數的基礎值</span><span class="sxs-lookup"><span data-stu-id="0573d-110">To change the underlying value of a procedure argument in the calling code</span></span>  
  
1. <span data-ttu-id="0573d-111">在程式宣告中，針對對應至引數的參數指定[ByRef](../../../language-reference/modifiers/byref.md) 。</span><span class="sxs-lookup"><span data-stu-id="0573d-111">In the procedure declaration, specify [ByRef](../../../language-reference/modifiers/byref.md) for the parameter corresponding to the argument.</span></span>  
  
2. <span data-ttu-id="0573d-112">在呼叫程式碼中，傳遞可修改的程式設計項目做為引數。</span><span class="sxs-lookup"><span data-stu-id="0573d-112">In the calling code, pass a modifiable programming element as the argument.</span></span>  
  
3. <span data-ttu-id="0573d-113">在呼叫程式碼中，請勿將引數括在引數清單中的括弧內。</span><span class="sxs-lookup"><span data-stu-id="0573d-113">In the calling code, do not enclose the argument in parentheses in the argument list.</span></span>  
  
4. <span data-ttu-id="0573d-114">在程式碼中，請使用參數名稱，將值指派給呼叫程式碼中的基礎元素。</span><span class="sxs-lookup"><span data-stu-id="0573d-114">In the procedure code, use the parameter name to assign a value to the underlying element in the calling code.</span></span>  
  
 <span data-ttu-id="0573d-115">如需示範，請參閱進一步的範例。</span><span class="sxs-lookup"><span data-stu-id="0573d-115">See the example further down for a demonstration.</span></span>  
  
## <a name="changing-local-copies"></a><span data-ttu-id="0573d-116">變更本機複本</span><span class="sxs-lookup"><span data-stu-id="0573d-116">Changing Local Copies</span></span>  
 <span data-ttu-id="0573d-117">如果呼叫程式碼中的基礎元素是無法修改的元素，或者傳遞了引數 `ByVal` ，程式就無法在呼叫程式碼中變更其值。</span><span class="sxs-lookup"><span data-stu-id="0573d-117">If the underlying element in the calling code is a nonmodifiable element, or if the argument is passed `ByVal`, the procedure cannot change its value in the calling code.</span></span> <span data-ttu-id="0573d-118">不過，程式可以變更其這類引數的本機複本。</span><span class="sxs-lookup"><span data-stu-id="0573d-118">However, the procedure can change its local copy of such an argument.</span></span>  
  
#### <a name="to-change-the-copy-of-a-procedure-argument-in-the-procedure-code"></a><span data-ttu-id="0573d-119">若要在程式碼中變更程式引數的複本</span><span class="sxs-lookup"><span data-stu-id="0573d-119">To change the copy of a procedure argument in the procedure code</span></span>  
  
1. <span data-ttu-id="0573d-120">在程式宣告中，針對對應至引數的參數指定[ByVal](../../../language-reference/modifiers/byval.md) 。</span><span class="sxs-lookup"><span data-stu-id="0573d-120">In the procedure declaration, specify [ByVal](../../../language-reference/modifiers/byval.md) for the parameter corresponding to the argument.</span></span>  
  
     <span data-ttu-id="0573d-121">-或-</span><span class="sxs-lookup"><span data-stu-id="0573d-121">-or-</span></span>  
  
     <span data-ttu-id="0573d-122">在呼叫程式碼中，將引數括在引數清單中的括弧內。</span><span class="sxs-lookup"><span data-stu-id="0573d-122">In the calling code, enclose the argument in parentheses in the argument list.</span></span> <span data-ttu-id="0573d-123">這會強制 Visual Basic 以傳值方式傳遞引數，即使對應的參數指定了亦然 `ByRef` 。</span><span class="sxs-lookup"><span data-stu-id="0573d-123">This forces Visual Basic to pass the argument by value, even if the corresponding parameter specifies `ByRef`.</span></span>  
  
2. <span data-ttu-id="0573d-124">在程式碼中，請使用參數名稱，將值指派給引數的本機複本。</span><span class="sxs-lookup"><span data-stu-id="0573d-124">In the procedure code, use the parameter name to assign a value to the local copy of the argument.</span></span> <span data-ttu-id="0573d-125">呼叫程式碼中的基礎值不會變更。</span><span class="sxs-lookup"><span data-stu-id="0573d-125">The underlying value in the calling code is not changed.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0573d-126">範例</span><span class="sxs-lookup"><span data-stu-id="0573d-126">Example</span></span>  
 <span data-ttu-id="0573d-127">下列範例顯示兩個採用陣列變數並在其專案上操作的程式。</span><span class="sxs-lookup"><span data-stu-id="0573d-127">The following example shows two procedures that take an array variable and operate on its elements.</span></span> <span data-ttu-id="0573d-128">此程式 `increase` 只會將一個專案新增至每個元素。</span><span class="sxs-lookup"><span data-stu-id="0573d-128">The `increase` procedure simply adds one to each element.</span></span> <span data-ttu-id="0573d-129">程式會將 `replace` 新的陣列指派給參數 `a()` ，然後將它加入至每個元素。</span><span class="sxs-lookup"><span data-stu-id="0573d-129">The `replace` procedure assigns a new array to the parameter `a()` and then adds one to each element.</span></span>  
  
 [!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]  
  
 [!code-vb[VbVbcnProcedures#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#36)]  
  
 [!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]  
  
 <span data-ttu-id="0573d-130">第一個 `MsgBox` 呼叫會顯示「增加（n）：11，21，31，41」。</span><span class="sxs-lookup"><span data-stu-id="0573d-130">The first `MsgBox` call displays "After increase(n): 11, 21, 31, 41".</span></span> <span data-ttu-id="0573d-131">因為陣列 `n` 是參考型別，所以 `replace` 可以變更其成員，即使傳遞機制是也一樣 `ByVal` 。</span><span class="sxs-lookup"><span data-stu-id="0573d-131">Because the array `n` is a reference type, `replace` can change its members, even though the passing mechanism is `ByVal`.</span></span>  
  
 <span data-ttu-id="0573d-132">第二個 `MsgBox` 呼叫會顯示 "After replace （n）：101，201，301"。</span><span class="sxs-lookup"><span data-stu-id="0573d-132">The second `MsgBox` call displays "After replace(n): 101, 201, 301".</span></span> <span data-ttu-id="0573d-133">因為 `n` 會傳遞 `ByRef` ，所以 `replace` 可以修改 `n` 呼叫程式碼中的變數，並將新的陣列指派給它。</span><span class="sxs-lookup"><span data-stu-id="0573d-133">Because `n` is passed `ByRef`, `replace` can modify the variable `n` in the calling code and assign a new array to it.</span></span> <span data-ttu-id="0573d-134">因為 `n` 是參考型別，所以 `replace` 也可以變更其成員。</span><span class="sxs-lookup"><span data-stu-id="0573d-134">Because `n` is a reference type, `replace` can also change its members.</span></span>  
  
 <span data-ttu-id="0573d-135">您可以防止程式在呼叫程式碼中修改變數本身。</span><span class="sxs-lookup"><span data-stu-id="0573d-135">You can prevent the procedure from modifying the variable itself in the calling code.</span></span> <span data-ttu-id="0573d-136">請參閱[如何：根據值變更保護程式引數](./how-to-protect-a-procedure-argument-against-value-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="0573d-136">See [How to: Protect a Procedure Argument Against Value Changes](./how-to-protect-a-procedure-argument-against-value-changes.md).</span></span>  
  
## <a name="compile-the-code"></a><span data-ttu-id="0573d-137">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="0573d-137">Compile the code</span></span>  
 <span data-ttu-id="0573d-138">當您以傳址方式傳遞變數時，您必須使用 `ByRef` 關鍵字來指定這項機制。</span><span class="sxs-lookup"><span data-stu-id="0573d-138">When you pass a variable by reference, you must use the `ByRef` keyword to specify this mechanism.</span></span>  
  
 <span data-ttu-id="0573d-139">Visual Basic 中的預設值是以傳值方式傳遞引數。</span><span class="sxs-lookup"><span data-stu-id="0573d-139">The default in Visual Basic is to pass arguments by value.</span></span> <span data-ttu-id="0573d-140">不過，在每個宣告的參數中包含[ByVal](../../../language-reference/modifiers/byval.md)或[ByRef](../../../language-reference/modifiers/byref.md)關鍵字是很好的程式設計作法。</span><span class="sxs-lookup"><span data-stu-id="0573d-140">However, it is good programming practice to include either the [ByVal](../../../language-reference/modifiers/byval.md) or [ByRef](../../../language-reference/modifiers/byref.md) keyword with every declared parameter.</span></span> <span data-ttu-id="0573d-141">這可讓您的程式碼更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="0573d-141">This makes your code easier to read.</span></span>  
  
## <a name="net-framework-security"></a><span data-ttu-id="0573d-142">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="0573d-142">.NET Framework Security</span></span>  
 <span data-ttu-id="0573d-143">允許程式變更呼叫程式碼中引數的基礎值，一律會有潛在的風險。</span><span class="sxs-lookup"><span data-stu-id="0573d-143">There is always a potential risk in allowing a procedure to change the value underlying an argument in the calling code.</span></span> <span data-ttu-id="0573d-144">請確定您預期會變更此值，並在使用它之前準備好檢查其有效性。</span><span class="sxs-lookup"><span data-stu-id="0573d-144">Make sure you expect this value to be changed, and be prepared to check it for validity before using it.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0573d-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0573d-145">See also</span></span>

- [<span data-ttu-id="0573d-146">程序</span><span class="sxs-lookup"><span data-stu-id="0573d-146">Procedures</span></span>](./index.md)
- [<span data-ttu-id="0573d-147">程序參數和引數</span><span class="sxs-lookup"><span data-stu-id="0573d-147">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="0573d-148">如何：將引數傳遞至程序</span><span class="sxs-lookup"><span data-stu-id="0573d-148">How to: Pass Arguments to a Procedure</span></span>](./how-to-pass-arguments-to-a-procedure.md)
- [<span data-ttu-id="0573d-149">以傳值和傳址方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="0573d-149">Passing Arguments by Value and by Reference</span></span>](./passing-arguments-by-value-and-by-reference.md)
- [<span data-ttu-id="0573d-150">可修改引數和不可修改引數之間的差異</span><span class="sxs-lookup"><span data-stu-id="0573d-150">Differences Between Modifiable and Nonmodifiable Arguments</span></span>](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [<span data-ttu-id="0573d-151">以傳值或傳址方式傳遞引數的差別</span><span class="sxs-lookup"><span data-stu-id="0573d-151">Differences Between Passing an Argument By Value and By Reference</span></span>](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [<span data-ttu-id="0573d-152">如何：防止程序引數的值變更</span><span class="sxs-lookup"><span data-stu-id="0573d-152">How to: Protect a Procedure Argument Against Value Changes</span></span>](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [<span data-ttu-id="0573d-153">如何：強制以傳值方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="0573d-153">How to: Force an Argument to Be Passed by Value</span></span>](./how-to-force-an-argument-to-be-passed-by-value.md)
- [<span data-ttu-id="0573d-154">依位置和名稱傳遞引數</span><span class="sxs-lookup"><span data-stu-id="0573d-154">Passing Arguments by Position and by Name</span></span>](./passing-arguments-by-position-and-by-name.md)
- [<span data-ttu-id="0573d-155">Value Types and Reference Types</span><span class="sxs-lookup"><span data-stu-id="0573d-155">Value Types and Reference Types</span></span>](../data-types/value-types-and-reference-types.md)

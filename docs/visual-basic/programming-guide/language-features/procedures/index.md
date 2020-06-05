---
title: 程序
ms.date: 04/28/2017
helpviewer_keywords:
- procedures [Visual Basic], structured code
- Visual Basic code, procedures
- procedures [Visual Basic], types of
- structured code [Visual Basic], procedures
- procedures
ms.assetid: 9effbcf0-80a0-4d1a-98f4-2c6920592766
ms.openlocfilehash: c0d9921704570c6984b203817aed8f5546b2f936
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408786"
---
# <a name="procedures-in-visual-basic"></a><span data-ttu-id="1ca42-102">Visual Basic 中的程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-102">Procedures in Visual Basic</span></span>
<span data-ttu-id="1ca42-103">程式*是以*宣告語句（ `Function` 、 `Sub` 、 `Operator` 、 `Get` 、 `Set` ）和相符的 `End` 宣告括住的 Visual Basic 語句區塊。</span><span class="sxs-lookup"><span data-stu-id="1ca42-103">A *procedure* is a block of Visual Basic statements enclosed by a declaration statement (`Function`, `Sub`, `Operator`, `Get`, `Set`) and a matching `End` declaration.</span></span> <span data-ttu-id="1ca42-104">Visual Basic 中的所有可執行語句都必須在某個程式內。</span><span class="sxs-lookup"><span data-stu-id="1ca42-104">All executable statements in Visual Basic must be within some procedure.</span></span>  
  
## <a name="calling-a-procedure"></a><span data-ttu-id="1ca42-105">呼叫程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-105">Calling a Procedure</span></span>  
 <span data-ttu-id="1ca42-106">您可以從程式碼中的其他位置叫用程序。</span><span class="sxs-lookup"><span data-stu-id="1ca42-106">You invoke a procedure from some other place in the code.</span></span> <span data-ttu-id="1ca42-107">這稱為「程序呼叫」\*\*。</span><span class="sxs-lookup"><span data-stu-id="1ca42-107">This is known as a *procedure call*.</span></span> <span data-ttu-id="1ca42-108">當程序完成執行時，會將控制權交還給叫用程序的程式碼，稱為「呼叫程式碼」\*\*。</span><span class="sxs-lookup"><span data-stu-id="1ca42-108">When the procedure is finished running, it returns control to the code that invoked it, which is known as the *calling code*.</span></span> <span data-ttu-id="1ca42-109">呼叫程式碼是陳述式或陳述式內的運算式，可依名稱指定程序，並將控制權轉移給它。</span><span class="sxs-lookup"><span data-stu-id="1ca42-109">The calling code is a statement, or an expression within a statement, that specifies the procedure by name and transfers control to it.</span></span>  
  
## <a name="returning-from-a-procedure"></a><span data-ttu-id="1ca42-110">從程序交還</span><span class="sxs-lookup"><span data-stu-id="1ca42-110">Returning from a Procedure</span></span>  
 <span data-ttu-id="1ca42-111">程序會在完成執行時將控制權交還給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-111">A procedure returns control to the calling code when it has finished running.</span></span> <span data-ttu-id="1ca42-112">若要這樣做，它可以使用[Return 語句](../../../language-reference/statements/return-statement.md)、程式的適當[Exit 語句](../../../language-reference/statements/exit-statement.md)語句，或程式的[End \<keyword> 語句](../../../language-reference/statements/end-keyword-statement.md)語句。</span><span class="sxs-lookup"><span data-stu-id="1ca42-112">To do this, it can use a [Return Statement](../../../language-reference/statements/return-statement.md), the appropriate [Exit Statement](../../../language-reference/statements/exit-statement.md) statement for the procedure, or the procedure's [End \<keyword> Statement](../../../language-reference/statements/end-keyword-statement.md) statement.</span></span> <span data-ttu-id="1ca42-113">控制權會在下列程序呼叫時間點之後接著傳遞給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-113">Control then passes to the calling code following the point of the procedure call.</span></span>  
  
- <span data-ttu-id="1ca42-114">若使用 `Return` 陳述式，控制權會立即交還給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-114">With a `Return` statement, control returns immediately to the calling code.</span></span> <span data-ttu-id="1ca42-115">`Return` 陳述式後面的陳述式不會執行。</span><span class="sxs-lookup"><span data-stu-id="1ca42-115">Statements following the `Return` statement do not run.</span></span> <span data-ttu-id="1ca42-116">同一個程序中可以有多個 `Return` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1ca42-116">You can have more than one `Return` statement in the same procedure.</span></span>  
  
- <span data-ttu-id="1ca42-117">若使用 `Exit Sub` 或 `Exit Function` 陳述式，控制權會立即交還給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-117">With an `Exit Sub` or `Exit Function` statement, control returns immediately to the calling code.</span></span> <span data-ttu-id="1ca42-118">`Exit` 陳述式後面的陳述式不會執行。</span><span class="sxs-lookup"><span data-stu-id="1ca42-118">Statements following the `Exit` statement do not run.</span></span> <span data-ttu-id="1ca42-119">同一個程序中可以有多個 `Exit` 陳述式，也可以混合 `Return` 和 `Exit` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1ca42-119">You can have more than one `Exit` statement in the same procedure, and you can mix `Return` and `Exit` statements in the same procedure.</span></span>  
  
- <span data-ttu-id="1ca42-120">如果程序沒有 `Return` 或 `Exit` 陳述式，則會以程序主體最後一個陳述式後面的 `End Sub`、`End Function`、`End Get` 或 `End Set` 陳述式結束。</span><span class="sxs-lookup"><span data-stu-id="1ca42-120">If a procedure has no `Return` or `Exit` statements, it concludes with an `End Sub` or `End Function`, `End Get`, or `End Set` statement following the last statement of the procedure body.</span></span> <span data-ttu-id="1ca42-121">`End` 陳述式會將控制權立即交還給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-121">The `End` statement returns control immediately to the calling code.</span></span> <span data-ttu-id="1ca42-122">一個程序中只能有一個 `End` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1ca42-122">You can have only one `End` statement in a procedure.</span></span>  
  
## <a name="parameters-and-arguments"></a><span data-ttu-id="1ca42-123">參數和引數</span><span class="sxs-lookup"><span data-stu-id="1ca42-123">Parameters and Arguments</span></span>  
 <span data-ttu-id="1ca42-124">在大部分情況下，程序會在每次呼叫時針對不同的資料執行。</span><span class="sxs-lookup"><span data-stu-id="1ca42-124">In most cases, a procedure needs to operate on different data each time you call it.</span></span> <span data-ttu-id="1ca42-125">您可以將這項資訊當作程序呼叫的一部分傳遞給程序。</span><span class="sxs-lookup"><span data-stu-id="1ca42-125">You can pass this information to the procedure as part of the procedure call.</span></span> <span data-ttu-id="1ca42-126">程序會定義零或多個「參數」\*\*，每個參數代表預期會收到的值。</span><span class="sxs-lookup"><span data-stu-id="1ca42-126">The procedure defines zero or more *parameters*, each of which represents a value it expects you to pass to it.</span></span> <span data-ttu-id="1ca42-127">程序定義中的每個參數會對應至程序呼叫中的「引數」\*\*。</span><span class="sxs-lookup"><span data-stu-id="1ca42-127">Corresponding to each parameter in the procedure definition is an *argument* in the procedure call.</span></span> <span data-ttu-id="1ca42-128">引數代表您傳遞給指定程序呼叫中對應參數的值。</span><span class="sxs-lookup"><span data-stu-id="1ca42-128">An argument represents the value you pass to the corresponding parameter in a given procedure call.</span></span>  
  
## <a name="types-of-procedures"></a><span data-ttu-id="1ca42-129">程序類型</span><span class="sxs-lookup"><span data-stu-id="1ca42-129">Types of Procedures</span></span>  
 <span data-ttu-id="1ca42-130">Visual Basic 使用數種類型的程式：</span><span class="sxs-lookup"><span data-stu-id="1ca42-130">Visual Basic uses several types of procedures:</span></span>  
  
- <span data-ttu-id="1ca42-131">[Sub 程序](./sub-procedures.md)會執行動作，但不會傳回值給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-131">[Sub Procedures](./sub-procedures.md) perform actions but do not return a value to the calling code.</span></span>  
  
- <span data-ttu-id="1ca42-132">事件處理程序是為了回應使用者動作或程式中某個項目所引發之事件所執行的 `Sub` 程序。</span><span class="sxs-lookup"><span data-stu-id="1ca42-132">Event-handling procedures are `Sub` procedures that execute in response to an event raised by user action or by an occurrence in a program.</span></span>  
  
- <span data-ttu-id="1ca42-133">[Function 程序](./function-procedures.md)會傳回值給呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ca42-133">[Function Procedures](./function-procedures.md) return a value to the calling code.</span></span> <span data-ttu-id="1ca42-134">該程序可在傳回前執行其他動作。</span><span class="sxs-lookup"><span data-stu-id="1ca42-134">They can perform other actions before returning.</span></span>

    <span data-ttu-id="1ca42-135">某些以 C# 撰寫的函式會傳回「參考傳回值」\*\*。</span><span class="sxs-lookup"><span data-stu-id="1ca42-135">Some functions written in C# return a *reference return value*.</span></span> <span data-ttu-id="1ca42-136">函式呼叫者可以修改傳回值，而且這項修改會反映在所呼叫物件的狀態中。</span><span class="sxs-lookup"><span data-stu-id="1ca42-136">Function callers can modify the return value, and this modification is reflected in the state of the called object.</span></span> <span data-ttu-id="1ca42-137">從 Visual Basic 2017 開始，Visual Basic 程式碼可以使用參考傳回值，但無法以傳址方式傳回值。</span><span class="sxs-lookup"><span data-stu-id="1ca42-137">Starting with Visual Basic 2017, Visual Basic code can consume reference return values, although it cannot return a value by reference.</span></span> <span data-ttu-id="1ca42-138">如需詳細資訊，請參閱[參考傳回值](ref-return-values.md)。</span><span class="sxs-lookup"><span data-stu-id="1ca42-138">For more information, see [Reference return values](ref-return-values.md).</span></span>
  
- <span data-ttu-id="1ca42-139">[屬性程序](./property-procedures.md)會傳回並指派物件或模組上的屬性值。</span><span class="sxs-lookup"><span data-stu-id="1ca42-139">[Property Procedures](./property-procedures.md) return and assign values of properties on objects or modules.</span></span>  
  
- <span data-ttu-id="1ca42-140">當一或多個運算元是新定義的類別或結構時，[運算子程序](./operator-procedures.md)會定義標準運算式的行為。</span><span class="sxs-lookup"><span data-stu-id="1ca42-140">[Operator Procedures](./operator-procedures.md) define the behavior of a standard operator when one or both of the operands is a newly-defined class or structure.</span></span>  
  
- <span data-ttu-id="1ca42-141">[Visual Basic 中的泛型程序](../data-types/generic-procedures.md)除了其一般參數之外，還會定義一或多個「型別參數」\*\*，讓呼叫程式碼可在每次呼叫時傳遞特定資料類型。</span><span class="sxs-lookup"><span data-stu-id="1ca42-141">[Generic Procedures in Visual Basic](../data-types/generic-procedures.md) define one or more *type parameters* in addition to their normal parameters, so the calling code can pass specific data types each time it makes a call.</span></span>  
  
## <a name="procedures-and-structured-code"></a><span data-ttu-id="1ca42-142">程序和結構化程式碼</span><span class="sxs-lookup"><span data-stu-id="1ca42-142">Procedures and Structured Code</span></span>  
 <span data-ttu-id="1ca42-143">應用程式中所有的可執行程式碼行都必須在某個程序內，例如 `Main`、`calculate` 或 `Button1_Click`。</span><span class="sxs-lookup"><span data-stu-id="1ca42-143">Every line of executable code in your application must be inside some procedure, such as `Main`, `calculate`, or `Button1_Click`.</span></span> <span data-ttu-id="1ca42-144">如果您將大型程序細分成較小的程序，您的應用程式會更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="1ca42-144">If you subdivide large procedures into smaller ones, your application is more readable.</span></span>  
  
 <span data-ttu-id="1ca42-145">程序很適合用來執行重複或共用的工作，例如常用的計算、文字和控制項操作，以及資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="1ca42-145">Procedures are useful for performing repeated or shared tasks, such as frequently used calculations, text and control manipulation, and database operations.</span></span> <span data-ttu-id="1ca42-146">您可以從程式碼的許多不同位置呼叫程序，因此您可以將程序作為應用程式的建置組塊使用。</span><span class="sxs-lookup"><span data-stu-id="1ca42-146">You can call a procedure from many different places in your code, so you can use procedures as building blocks for your application.</span></span>  
  
 <span data-ttu-id="1ca42-147">使用程序建構您的程式碼提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1ca42-147">Structuring your code with procedures gives you the following benefits:</span></span>  
  
- <span data-ttu-id="1ca42-148">程序可讓您將程式分成不連續的邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="1ca42-148">Procedures allow you to break your programs into discrete logical units.</span></span> <span data-ttu-id="1ca42-149">比起不使用程序對整個程式進行偵錯，偵錯個別單元會更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="1ca42-149">You can debug separate units more easily than you can debug an entire program without procedures.</span></span>  
  
- <span data-ttu-id="1ca42-150">開發用於一個平台的程序之後，您可以在其他程式中使用這些程序，通常只需要微幅修改或完全不需要修改。</span><span class="sxs-lookup"><span data-stu-id="1ca42-150">After you develop procedures for use in one program, you can use them in other programs, often with little or no modification.</span></span> <span data-ttu-id="1ca42-151">這可協助您避免程式碼重複。</span><span class="sxs-lookup"><span data-stu-id="1ca42-151">This helps you avoid code duplication.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1ca42-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1ca42-152">See also</span></span>

- [<span data-ttu-id="1ca42-153">如何：建立程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-153">How to: Create a Procedure</span></span>](./how-to-create-a-procedure.md)
- [<span data-ttu-id="1ca42-154">Sub 程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-154">Sub Procedures</span></span>](./sub-procedures.md)
- [<span data-ttu-id="1ca42-155">Function 程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-155">Function Procedures</span></span>](./function-procedures.md)
- [<span data-ttu-id="1ca42-156">屬性程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-156">Property Procedures</span></span>](./property-procedures.md)
- [<span data-ttu-id="1ca42-157">運算子程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-157">Operator Procedures</span></span>](./operator-procedures.md)
- [<span data-ttu-id="1ca42-158">程序參數和引數</span><span class="sxs-lookup"><span data-stu-id="1ca42-158">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="1ca42-159">遞迴程序</span><span class="sxs-lookup"><span data-stu-id="1ca42-159">Recursive Procedures</span></span>](./recursive-procedures.md)
- [<span data-ttu-id="1ca42-160">程序多載化</span><span class="sxs-lookup"><span data-stu-id="1ca42-160">Procedure Overloading</span></span>](./procedure-overloading.md)
- [<span data-ttu-id="1ca42-161">Generic Procedures in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="1ca42-161">Generic Procedures in Visual Basic</span></span>](../data-types/generic-procedures.md)
- [<span data-ttu-id="1ca42-162">物件和類別</span><span class="sxs-lookup"><span data-stu-id="1ca42-162">Objects and Classes</span></span>](../objects-and-classes/index.md)

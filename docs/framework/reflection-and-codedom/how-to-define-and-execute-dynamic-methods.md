---
title: 作法：定義和執行動態方法
description: 請參閱如何在 .NET 中定義和執行動態方法。 查看簡單動態方法的範例，以及系結至類別實例的動態方法。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection emit, dynamic methods
- dynamic methods
ms.assetid: 07d08a99-62c5-4254-bce2-2a75e55a18ab
ms.openlocfilehash: 1ea15149ea72c3c422251abefb5a1008cc496f2c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263447"
---
# <a name="how-to-define-and-execute-dynamic-methods"></a><span data-ttu-id="5fbc6-104">作法：定義和執行動態方法</span><span class="sxs-lookup"><span data-stu-id="5fbc6-104">How to: Define and Execute Dynamic Methods</span></span>

<span data-ttu-id="5fbc6-105">下列程序顯示如何定義及執行簡單的動態方法及繫結至類別執行個體的動態方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-105">The following procedures show how to define and execute a simple dynamic method and a dynamic method bound to an instance of a class.</span></span> <span data-ttu-id="5fbc6-106">如需動態方法的詳細資訊，請參閱 <xref:System.Reflection.Emit.DynamicMethod> 類別和[反映發出動態方法案例](/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-106">For more information on dynamic methods, see the <xref:System.Reflection.Emit.DynamicMethod> class and [Reflection Emit Dynamic Method Scenarios](/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100)).</span></span>  
  
### <a name="to-define-and-execute-a-dynamic-method"></a><span data-ttu-id="5fbc6-107">定義和執行動態方法</span><span class="sxs-lookup"><span data-stu-id="5fbc6-107">To define and execute a dynamic method</span></span>  
  
1. <span data-ttu-id="5fbc6-108">宣告委派類型來執行方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-108">Declare a delegate type to execute the method.</span></span> <span data-ttu-id="5fbc6-109">請考慮使用泛型委派，將您需要宣告的委派類型數目降到最低。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-109">Consider using a generic delegate to minimize the number of delegate types you need to declare.</span></span> <span data-ttu-id="5fbc6-110">下列程式碼會宣告兩個可用於 `SquareIt` 方法的委派類型，其中之一是泛型。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-110">The following code declares two delegate types that could be used for the `SquareIt` method, and one of them is generic.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#2)]
     [!code-csharp[DynamicMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#2)]
     [!code-vb[DynamicMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#2)]  
  
2. <span data-ttu-id="5fbc6-111">建立陣列，指定動態方法的參數類型。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-111">Create an array that specifies the parameter types for the dynamic method.</span></span> <span data-ttu-id="5fbc6-112">在此範例中，唯一的參數是 `int` (Visual Basic 為 `Integer`)，所以陣列只有一個項目。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-112">In this example, the only parameter is an `int` (`Integer` in Visual Basic), so the array has only one element.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#3)]
     [!code-csharp[DynamicMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#3)]
     [!code-vb[DynamicMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#3)]  
  
3. <span data-ttu-id="5fbc6-113">建立 <xref:System.Reflection.Emit.DynamicMethod>。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-113">Create a <xref:System.Reflection.Emit.DynamicMethod>.</span></span> <span data-ttu-id="5fbc6-114">本例中的方法名為 `SquareIt`。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-114">In this example the method is named `SquareIt`.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="5fbc6-115">不需要提供動態方法名稱，它們無法依名稱叫用。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-115">It is not necessary to give dynamic methods names, and they cannot be invoked by name.</span></span> <span data-ttu-id="5fbc6-116">多個動態方法可有相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-116">Multiple dynamic methods can have the same name.</span></span> <span data-ttu-id="5fbc6-117">不過，名稱會出現在呼叫堆疊中，有利於偵錯。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-117">However, the name appears in call stacks and can be useful for debugging.</span></span>  
  
     <span data-ttu-id="5fbc6-118">傳回值的類型指定為 `long`。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-118">The type of the return value is specified as `long`.</span></span> <span data-ttu-id="5fbc6-119">與包含 `Example` 類別的模組建立關聯的方法，包含範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-119">The method is associated with the module that contains the `Example` class, which contains the example code.</span></span> <span data-ttu-id="5fbc6-120">可指定任何已載入的模組。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-120">Any loaded module could be specified.</span></span> <span data-ttu-id="5fbc6-121">動態方法的行為如同模組層級的 `static` 方法 (Visual Basic 為 `Shared`)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-121">The dynamic method acts like a module-level `static` method (`Shared` in Visual Basic).</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#4)]
     [!code-csharp[DynamicMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#4)]
     [!code-vb[DynamicMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#4)]  
  
4. <span data-ttu-id="5fbc6-122">發出方法主體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-122">Emit the method body.</span></span> <span data-ttu-id="5fbc6-123">本例中使用 <xref:System.Reflection.Emit.ILGenerator> 物件發出 Microsoft 中繼語言 (MSIL)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-123">In this example, an <xref:System.Reflection.Emit.ILGenerator> object is used to emit the Microsoft intermediate language (MSIL).</span></span> <span data-ttu-id="5fbc6-124">或者，您可使用 <xref:System.Reflection.Emit.DynamicILInfo> 物件結合 Unmanaged 程式碼產生器，發出 <xref:System.Reflection.Emit.DynamicMethod> 的方法主體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-124">Alternatively, a <xref:System.Reflection.Emit.DynamicILInfo> object can be used in conjunction with unmanaged code generators to emit the method body for a <xref:System.Reflection.Emit.DynamicMethod>.</span></span>  
  
     <span data-ttu-id="5fbc6-125">本例中的 MSIL 是 `int`，會將引數載入到堆疊上，再將它轉換成 `long`，重複 `long` 再將兩個數字相乘。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-125">The MSIL in this example loads the argument, which is an `int`, onto the stack, converts it to a `long`, duplicates the `long`, and multiplies the two numbers.</span></span> <span data-ttu-id="5fbc6-126">這會將平方的結果留在堆疊上，而方法唯一要做的只有傳回。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-126">This leaves the squared result on the stack, and all the method has to do is return.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#5](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#5)]
     [!code-csharp[DynamicMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#5)]
     [!code-vb[DynamicMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#5)]  
  
5. <span data-ttu-id="5fbc6-127">呼叫 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> 方法，以建立表示動態方法之 (在步驟 1 中宣告) 委派的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-127">Create an instance of the delegate (declared in step 1) that represents the dynamic method by calling the <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> method.</span></span> <span data-ttu-id="5fbc6-128">建立委派即會完成方法，而任何進一步變更方法的嘗試，例如新增更多的 MSIL，則予以忽略。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-128">Creating the delegate completes the method, and any further attempts to change the method — for example, adding more MSIL — are ignored.</span></span> <span data-ttu-id="5fbc6-129">下列程式碼會使用泛型委派，建立並叫用委派。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-129">The following code creates the delegate and invokes it, using a generic delegate.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#6)]
     [!code-csharp[DynamicMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#6)]
     [!code-vb[DynamicMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#6)]  
  
### <a name="to-define-and-execute-a-dynamic-method-that-is-bound-to-an-object"></a><span data-ttu-id="5fbc6-130">定義及執行繫結至物件的動態方法</span><span class="sxs-lookup"><span data-stu-id="5fbc6-130">To define and execute a dynamic method that is bound to an object</span></span>  
  
1. <span data-ttu-id="5fbc6-131">宣告委派類型來執行方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-131">Declare a delegate type to execute the method.</span></span> <span data-ttu-id="5fbc6-132">請考慮使用泛型委派，將您需要宣告的委派類型數目降到最低。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-132">Consider using a generic delegate to minimize the number of delegate types you need to declare.</span></span> <span data-ttu-id="5fbc6-133">下列程式碼會宣告泛型委派類型，其可用於執行任何具有一個參數和傳回值的方法，如果委派繫結至物件，則可為具有兩個參數和傳回值的方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-133">The following code declares a generic delegate type that can be used to execute any method with one parameter and a return value, or a method with two parameters and a return value if the delegate is bound to an object.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#12](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#12)]
     [!code-csharp[DynamicMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#12)]
     [!code-vb[DynamicMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#12)]  
  
2. <span data-ttu-id="5fbc6-134">建立陣列，指定動態方法的參數類型。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-134">Create an array that specifies the parameter types for the dynamic method.</span></span> <span data-ttu-id="5fbc6-135">如果表示方法的委派繫結至物件，第一個參數就必須符合委派繫結的類型。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-135">If the delegate representing the method is to be bound to an object, the first parameter must match the type the delegate is bound to.</span></span> <span data-ttu-id="5fbc6-136">本例中有兩個參數，類型 `Example` 和類型 `int` (Visual Basic 為 `Integer`)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-136">In this example, there are two parameters, of type `Example` and type `int` (`Integer` in Visual Basic).</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#13](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#13)]
     [!code-csharp[DynamicMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#13)]
     [!code-vb[DynamicMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#13)]  
  
3. <span data-ttu-id="5fbc6-137">建立 <xref:System.Reflection.Emit.DynamicMethod>。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-137">Create a <xref:System.Reflection.Emit.DynamicMethod>.</span></span> <span data-ttu-id="5fbc6-138">本例中的方法沒有名稱。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-138">In this example the method has no name.</span></span> <span data-ttu-id="5fbc6-139">傳回值的類型指定為 `int` (Visual Basic 為 `Integer`)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-139">The type of the return value is specified as `int` (`Integer` in Visual Basic).</span></span> <span data-ttu-id="5fbc6-140">方法可以存取 `Example` 類別的私用和受保護成員。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-140">The method has access to the private and protected members of the `Example` class.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#14](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#14)]
     [!code-csharp[DynamicMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#14)]
     [!code-vb[DynamicMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#14)]  
  
4. <span data-ttu-id="5fbc6-141">發出方法主體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-141">Emit the method body.</span></span> <span data-ttu-id="5fbc6-142">本例中使用 <xref:System.Reflection.Emit.ILGenerator> 物件發出 Microsoft 中繼語言 (MSIL)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-142">In this example, an <xref:System.Reflection.Emit.ILGenerator> object is used to emit the Microsoft intermediate language (MSIL).</span></span> <span data-ttu-id="5fbc6-143">或者，您可使用 <xref:System.Reflection.Emit.DynamicILInfo> 物件結合 Unmanaged 程式碼產生器，發出 <xref:System.Reflection.Emit.DynamicMethod> 的方法主體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-143">Alternatively, a <xref:System.Reflection.Emit.DynamicILInfo> object can be used in conjunction with unmanaged code generators to emit the method body for a <xref:System.Reflection.Emit.DynamicMethod>.</span></span>  
  
     <span data-ttu-id="5fbc6-144">本例中的 MSIL 是 `Example` 類別的執行個體，它會載入第一個引數，再使用它載入類型 `int` 的私用執行個體欄位值。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-144">The MSIL in this example loads the first argument, which is an instance of the `Example` class, and uses it to load the value of a private instance field of type `int`.</span></span> <span data-ttu-id="5fbc6-145">載入第二個引數，然後兩個數字相乘。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-145">The second argument is loaded, and the two numbers are multiplied.</span></span> <span data-ttu-id="5fbc6-146">如果結果大於 `int`，則截斷值，捨棄最高有效位元。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-146">If the result is larger than `int`, the value is truncated and the most significant bits are discarded.</span></span> <span data-ttu-id="5fbc6-147">方法傳回，附有堆疊上的傳回值。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-147">The method returns, with the return value on the stack.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#15](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#15)]
     [!code-csharp[DynamicMethodHowTo#15](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#15)]
     [!code-vb[DynamicMethodHowTo#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#15)]  
  
5. <span data-ttu-id="5fbc6-148">呼叫 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%28System.Type%2CSystem.Object%29> 方法多載，以建立表示動態方法之 (步驟 1 所宣告的) 委派的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-148">Create an instance of the delegate (declared in step 1) that represents the dynamic method by calling the <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%28System.Type%2CSystem.Object%29> method overload.</span></span> <span data-ttu-id="5fbc6-149">建立委派即會完成方法，而任何進一步變更方法的嘗試，例如新增更多的 MSIL，則予以忽略。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-149">Creating the delegate completes the method, and any further attempts to change the method — for example, adding more MSIL — are ignored.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="5fbc6-150">您可以多次呼叫 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> 方法，建立繫結至其他目標類型執行個體的委派。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-150">You can call the <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> method multiple times to create delegates bound to other instances of the target type.</span></span>  
  
     <span data-ttu-id="5fbc6-151">下列程式碼會將方法繫結至 `Example` 類別的新執行個體，此類別的私用測試欄位設為 42。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-151">The following code binds the method to a new instance of the `Example` class whose private test field is set to 42.</span></span> <span data-ttu-id="5fbc6-152">亦即，每次叫用委派時，`Example` 的執行個體都會傳遞至方法的第一個參數。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-152">That is, each time the delegate is invoked the instance of `Example` is passed to the first parameter of the method.</span></span>  
  
     <span data-ttu-id="5fbc6-153">因為方法的第一個參數一律會收到 `Example` 的執行個體，所以使用委派 `OneParameter`。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-153">The delegate `OneParameter` is used because the first parameter of the method always receives the instance of `Example`.</span></span> <span data-ttu-id="5fbc6-154">叫用委派時，只需要第二個參數。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-154">When the delegate is invoked, only the second parameter is required.</span></span>  
  
     [!code-cpp[DynamicMethodHowTo#16](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#16)]
     [!code-csharp[DynamicMethodHowTo#16](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#16)]
     [!code-vb[DynamicMethodHowTo#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#16)]  
  
## <a name="example"></a><span data-ttu-id="5fbc6-155">範例</span><span class="sxs-lookup"><span data-stu-id="5fbc6-155">Example</span></span>  

 <span data-ttu-id="5fbc6-156">下列程式碼範例會示範簡單的動態方法及繫結至類別執行個體的動態方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-156">The following code example demonstrates a simple dynamic method and a dynamic method bound to an instance of a class.</span></span>  
  
 <span data-ttu-id="5fbc6-157">簡單的動態方法接受一個 32 位元整數的引數，並傳回該整數的 64 位元平方。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-157">The simple dynamic method takes one argument, a 32-bit integer, and returns the 64-bit square of that integer.</span></span> <span data-ttu-id="5fbc6-158">使用泛型委派叫用方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-158">A generic delegate is used to invoke the method.</span></span>  
  
 <span data-ttu-id="5fbc6-159">第二個動態方法有兩個參數，類型 `Example` 和類型 `int` (Visual Basic 為 `Integer`)。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-159">The second dynamic method has two parameters, of type `Example` and type `int` (`Integer` in Visual Basic).</span></span> <span data-ttu-id="5fbc6-160">動態方法建立後，會使用有一個類別 `int` 引數的泛型委派，繫結至 `Example` 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-160">When the dynamic method has been created, it is bound to an instance of `Example`, using a generic delegate that has one argument of type `int`.</span></span> <span data-ttu-id="5fbc6-161">因為方法的第一個參數一律會收到 `Example` 的繫結執行個體，所以委派沒有類型 `Example` 的引數。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-161">The delegate does not have an argument of type `Example` because the first parameter of the method always receives the bound instance of `Example`.</span></span> <span data-ttu-id="5fbc6-162">叫用委派時，只提供 `int` 引數。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-162">When the delegate is invoked, only the `int` argument is supplied.</span></span> <span data-ttu-id="5fbc6-163">此動態方法會存取 `Example` 類別的私用欄位，並傳回私用欄位和 `int` 引數的乘積。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-163">This dynamic method accesses a private field of the `Example` class and returns the product of the private field and the `int` argument.</span></span>  
  
 <span data-ttu-id="5fbc6-164">程式碼範例會定義委派，此委派可用以執行方法。</span><span class="sxs-lookup"><span data-stu-id="5fbc6-164">The code example defines delegates that can be used to execute the methods.</span></span>  
  
 [!code-cpp[DynamicMethodHowTo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#1)]
 [!code-csharp[DynamicMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#1)]
 [!code-vb[DynamicMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="5fbc6-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5fbc6-165">See also</span></span>

- <xref:System.Reflection.Emit.DynamicMethod>
- <span data-ttu-id="5fbc6-166">[使用反映發出](/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="5fbc6-166">[Using Reflection Emit](/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))</span></span>
- <span data-ttu-id="5fbc6-167">[反映發出動態方法案例](/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="5fbc6-167">[Reflection Emit Dynamic Method Scenarios](/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100))</span></span>

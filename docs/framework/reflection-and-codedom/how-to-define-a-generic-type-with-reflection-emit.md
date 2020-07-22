---
title: 作法：使用反映發出定義泛型型別
description: 請參閱如何使用反映發出定義泛型型別。 建立具有兩個型別參數的泛型型別、套用類別條件約束、介面條件約束等。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- generics [.NET Framework], dynamic types
- reflection emit, generic types
ms.assetid: 07d5f01a-7b5b-40ea-9b15-f21561098fe4
ms.openlocfilehash: fe8fb731fd160ab87e5c65debf367a96bc0dea2a
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865121"
---
# <a name="how-to-define-a-generic-type-with-reflection-emit"></a><span data-ttu-id="cb587-104">作法：使用反映發出定義泛型型別</span><span class="sxs-lookup"><span data-stu-id="cb587-104">How to: Define a Generic Type with Reflection Emit</span></span>
<span data-ttu-id="cb587-105">本主題示範如何建立具有兩個型別參數的簡單泛型類型、如何將類別條件約束、介面條件約束及特殊條件約束套用至型別參數，以及如何建立成員，以使用類別的型別參數作為參數類型及傳回類型。</span><span class="sxs-lookup"><span data-stu-id="cb587-105">This topic shows how to create a simple generic type with two type parameters, how to apply class constraints, interface constraints, and special constraints to the type parameters, and how to create members that use the type parameters of the class as parameter types and return types.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="cb587-106">方法不是只因為屬於泛型型別並使用該類型的類型參數，而成為泛型。</span><span class="sxs-lookup"><span data-stu-id="cb587-106">A method is not generic just because it belongs to a generic type and uses the type parameters of that type.</span></span> <span data-ttu-id="cb587-107">方法只有在有自己的類型參數清單時，才會是泛型。</span><span class="sxs-lookup"><span data-stu-id="cb587-107">A method is generic only if it has its own type parameter list.</span></span> <span data-ttu-id="cb587-108">泛型型別上的大部分方法不是泛型，如本例所示。</span><span class="sxs-lookup"><span data-stu-id="cb587-108">Most methods on generic types are not generic, as in this example.</span></span> <span data-ttu-id="cb587-109">如需發出泛型方法的範例，請參閱[如何︰使用反映發出定義泛型方法](how-to-define-a-generic-method-with-reflection-emit.md)。</span><span class="sxs-lookup"><span data-stu-id="cb587-109">For an example of emitting a generic method, see [How to: Define a Generic Method with Reflection Emit](how-to-define-a-generic-method-with-reflection-emit.md).</span></span>  
  
### <a name="to-define-a-generic-type"></a><span data-ttu-id="cb587-110">定義泛型型別</span><span class="sxs-lookup"><span data-stu-id="cb587-110">To define a generic type</span></span>  
  
1. <span data-ttu-id="cb587-111">定義名為 `GenericEmitExample1` 的動態組件。</span><span class="sxs-lookup"><span data-stu-id="cb587-111">Define a dynamic assembly named `GenericEmitExample1`.</span></span> <span data-ttu-id="cb587-112">在本例中，組件在執行後會儲存到磁碟，因此指定 <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="cb587-112">In this example, the assembly is executed and saved to disk, so <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType> is specified.</span></span>  
  
     [!code-cpp[EmitGenericType#2](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#2)]
     [!code-csharp[EmitGenericType#2](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#2)]
     [!code-vb[EmitGenericType#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#2)]  
  
2. <span data-ttu-id="cb587-113">定義動態模組。</span><span class="sxs-lookup"><span data-stu-id="cb587-113">Define a dynamic module.</span></span> <span data-ttu-id="cb587-114">組件是由可執行模組組成。</span><span class="sxs-lookup"><span data-stu-id="cb587-114">An assembly is made up of executable modules.</span></span> <span data-ttu-id="cb587-115">組件如僅有一個模組，則模組名稱和組件名稱相同，且檔案名稱是模組名稱加上副檔名。</span><span class="sxs-lookup"><span data-stu-id="cb587-115">For a single-module assembly, the module name is the same as the assembly name, and the file name is the module name plus an extension.</span></span>  
  
     [!code-cpp[EmitGenericType#3](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#3)]
     [!code-csharp[EmitGenericType#3](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#3)]
     [!code-vb[EmitGenericType#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#3)]  
  
3. <span data-ttu-id="cb587-116">定義類別。</span><span class="sxs-lookup"><span data-stu-id="cb587-116">Define a class.</span></span> <span data-ttu-id="cb587-117">本例中的類別名為 `Sample`。</span><span class="sxs-lookup"><span data-stu-id="cb587-117">In this example, the class is named `Sample`.</span></span>  
  
     [!code-cpp[EmitGenericType#4](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#4)]
     [!code-csharp[EmitGenericType#4](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#4)]
     [!code-vb[EmitGenericType#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#4)]  
  
4. <span data-ttu-id="cb587-118">將包含參數名稱的字串陣列傳遞至 <xref:System.Reflection.Emit.TypeBuilder.DefineGenericParameters%2A?displayProperty=nameWithType> 方法，以定義 `Sample` 的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="cb587-118">Define the generic type parameters of `Sample` by passing an array of strings containing the names of the parameters to the <xref:System.Reflection.Emit.TypeBuilder.DefineGenericParameters%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="cb587-119">這可讓類別成為泛型型別。</span><span class="sxs-lookup"><span data-stu-id="cb587-119">This makes the class a generic type.</span></span> <span data-ttu-id="cb587-120">傳回值是代表型別參數的 <xref:System.Reflection.Emit.GenericTypeParameterBuilder> 物件陣列，可用於發出的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="cb587-120">The return value is an array of <xref:System.Reflection.Emit.GenericTypeParameterBuilder> objects representing the type parameters, which can be used in your emitted code.</span></span>  
  
     <span data-ttu-id="cb587-121">在下列程式碼中，`Sample` 會成為具有型別參數 `TFirst` 和 `TSecond` 的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="cb587-121">In the following code, `Sample` becomes a generic type with type parameters `TFirst` and `TSecond`.</span></span> <span data-ttu-id="cb587-122">若要讓程式碼便於閱讀，每個 <xref:System.Reflection.Emit.GenericTypeParameterBuilder> 都要放在與型別參數同名的變數中。</span><span class="sxs-lookup"><span data-stu-id="cb587-122">To make the code easier to read, each <xref:System.Reflection.Emit.GenericTypeParameterBuilder> is placed in a variable with the same name as the type parameter.</span></span>  
  
     [!code-cpp[EmitGenericType#5](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#5)]
     [!code-csharp[EmitGenericType#5](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#5)]
     [!code-vb[EmitGenericType#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#5)]  
  
5. <span data-ttu-id="cb587-123">將特殊條件約束新增至型別參數。</span><span class="sxs-lookup"><span data-stu-id="cb587-123">Add special constraints to the type parameters.</span></span> <span data-ttu-id="cb587-124">在此範例中，型別參數 `TFirst` 限為具有無參數建構函式的類型及參考型別。</span><span class="sxs-lookup"><span data-stu-id="cb587-124">In this example, type parameter `TFirst` is constrained to types that have parameterless constructors, and to reference types.</span></span>  
  
     [!code-cpp[EmitGenericType#6](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#6)]
     [!code-csharp[EmitGenericType#6](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#6)]
     [!code-vb[EmitGenericType#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#6)]  
  
6. <span data-ttu-id="cb587-125">或者將類別和介面條件約束新增至類型參數。</span><span class="sxs-lookup"><span data-stu-id="cb587-125">Optionally add class and interface constraints to the type parameters.</span></span> <span data-ttu-id="cb587-126">在本例中，型別參數 `TFirst` 限制為衍生自基底類別的類型，而此基底類別是由包含在變數 `baseType` 中的 <xref:System.Type> 物件所表示；以及實作介面的類型，而此介面的類型包含在變數 `interfaceA` 和 `interfaceB` 中。</span><span class="sxs-lookup"><span data-stu-id="cb587-126">In this example, type parameter `TFirst` is constrained to types that derive from the base class represented by the <xref:System.Type> object contained in the variable `baseType`, and that implement the interfaces whose types are contained in the variables `interfaceA` and `interfaceB`.</span></span> <span data-ttu-id="cb587-127">請參閱宣告和指派這些變數的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="cb587-127">See the code example for the declaration and assignment of these variables.</span></span>  
  
     [!code-cpp[EmitGenericType#7](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#7)]
     [!code-csharp[EmitGenericType#7](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#7)]
     [!code-vb[EmitGenericType#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#7)]  
  
7. <span data-ttu-id="cb587-128">定義欄位。</span><span class="sxs-lookup"><span data-stu-id="cb587-128">Define a field.</span></span> <span data-ttu-id="cb587-129">本例中的欄位類型是由型別參數 `TFirst` 所指定。</span><span class="sxs-lookup"><span data-stu-id="cb587-129">In this example, the type of the field is specified by type parameter `TFirst`.</span></span> <span data-ttu-id="cb587-130"><xref:System.Reflection.Emit.GenericTypeParameterBuilder> 衍生自 <xref:System.Type>，所以只要可以使用類型的位置，都可以使用泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="cb587-130"><xref:System.Reflection.Emit.GenericTypeParameterBuilder> derives from <xref:System.Type>, so you can use generic type parameters anywhere a type can be used.</span></span>  
  
     [!code-cpp[EmitGenericType#21](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#21)]
     [!code-csharp[EmitGenericType#21](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#21)]
     [!code-vb[EmitGenericType#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#21)]  
  
8. <span data-ttu-id="cb587-131">定義使用泛型型別之型別參數的方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-131">Define a method that uses the type parameters of the generic type.</span></span> <span data-ttu-id="cb587-132">請注意，這類方法不是泛型，除非它們有自己的型別參數清單。</span><span class="sxs-lookup"><span data-stu-id="cb587-132">Note that such methods are not generic unless they have their own type parameter lists.</span></span> <span data-ttu-id="cb587-133">下列程式碼定義 `static` 方法 (Visual Basic 為 `Shared`)，其接受 `TFirst` 陣列並傳回包含陣列所有項目的 `List<TFirst>` (Visual Basic 為 `List(Of TFirst)`)。</span><span class="sxs-lookup"><span data-stu-id="cb587-133">The following code defines a `static` method (`Shared` in Visual Basic) that takes an array of `TFirst` and returns a `List<TFirst>` (`List(Of TFirst)` in Visual Basic) containing all the elements of the array.</span></span> <span data-ttu-id="cb587-134">若要定義這個方法，即必須在泛型型別定義 `List<T>` 呼叫 <xref:System.Type.MakeGenericType%2A>，以建立類型 `List<TFirst>`。</span><span class="sxs-lookup"><span data-stu-id="cb587-134">To define this method, it is necessary to create the type `List<TFirst>` by calling <xref:System.Type.MakeGenericType%2A> on the generic type definition, `List<T>`.</span></span> <span data-ttu-id="cb587-135">（ `T` 當您使用 `typeof` 運算子（ `GetType` 在 Visual Basic 中）來取得泛型型別定義時，會省略。）參數類型是使用方法所建立 <xref:System.Type.MakeArrayType%2A> 。</span><span class="sxs-lookup"><span data-stu-id="cb587-135">(The `T` is omitted when you use the `typeof` operator (`GetType` in Visual Basic) to get the generic type definition.) The parameter type is created by using the <xref:System.Type.MakeArrayType%2A> method.</span></span>  
  
     [!code-cpp[EmitGenericType#22](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#22)]
     [!code-csharp[EmitGenericType#22](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#22)]
     [!code-vb[EmitGenericType#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#22)]  
  
9. <span data-ttu-id="cb587-136">發出方法主體。</span><span class="sxs-lookup"><span data-stu-id="cb587-136">Emit the method body.</span></span> <span data-ttu-id="cb587-137">方法主體中包含三個作業碼，可將輸入陣列載入至堆疊，呼叫接受 `IEnumerable<TFirst>` (它會執行所有將輸入項目放入清單中的工作) 的 `List<TFirst>` 建構函式 ，並傳回 (將新的 <xref:System.Collections.Generic.List%601> 物件留在堆疊上)。</span><span class="sxs-lookup"><span data-stu-id="cb587-137">The method body consists of three opcodes that load the input array onto the stack, call the `List<TFirst>` constructor that takes `IEnumerable<TFirst>` (which does all the work of putting the input elements into the list), and return (leaving the new <xref:System.Collections.Generic.List%601> object on the stack).</span></span> <span data-ttu-id="cb587-138">發出此程式碼最困難的部分是取得建構函式。</span><span class="sxs-lookup"><span data-stu-id="cb587-138">The difficult part of emitting this code is getting the constructor.</span></span>  
  
     <span data-ttu-id="cb587-139"><xref:System.Reflection.Emit.GenericTypeParameterBuilder> 不支援 <xref:System.Type.GetConstructor%2A> 方法，所以不可能直接取得 `List<TFirst>` 的建構函式。</span><span class="sxs-lookup"><span data-stu-id="cb587-139">The <xref:System.Type.GetConstructor%2A> method is not supported on a <xref:System.Reflection.Emit.GenericTypeParameterBuilder>, so it is not possible to get the constructor of `List<TFirst>` directly.</span></span> <span data-ttu-id="cb587-140">首先，必須取得泛型型別定義 `List<T>` 的建構函式，然後呼叫能將它轉換成對應的 `List<TFirst>` 建構函式的方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-140">First, it is necessary to get the constructor of the generic type definition `List<T>` and then to call a method that converts it to the corresponding constructor of `List<TFirst>`.</span></span>  
  
     <span data-ttu-id="cb587-141">此程式碼範例所使用的建構函式接受 `IEnumerable<T>`。</span><span class="sxs-lookup"><span data-stu-id="cb587-141">The constructor used for this code example takes an `IEnumerable<T>`.</span></span> <span data-ttu-id="cb587-142">但是請注意，這不是 <xref:System.Collections.Generic.IEnumerable%601> 泛型介面的泛型型別定義；相反地，來自 `List<T>` 的型別參數 `T` 必須取代 `IEnumerable<T>` 的型別參數 `T`。</span><span class="sxs-lookup"><span data-stu-id="cb587-142">Note, however, that this is not the generic type definition of the <xref:System.Collections.Generic.IEnumerable%601> generic interface; instead, the type parameter `T` from `List<T>` must be substituted for the type parameter `T` of `IEnumerable<T>`.</span></span> <span data-ttu-id="cb587-143">(這似乎很令人困惑，只因為這兩個類型都有名為 `T` 的型別參數。</span><span class="sxs-lookup"><span data-stu-id="cb587-143">(This seems confusing only because both types have type parameters named `T`.</span></span> <span data-ttu-id="cb587-144">這就是為什麼此程式碼範例會使用名稱和的原因 `TFirst` `TSecond` ）。若要取得函式引數的型別，請從泛型型別定義開始， `IEnumerable<T>` 並 <xref:System.Type.MakeGenericType%2A> 使用的第一個泛型型別參數呼叫 `List<T>` 。</span><span class="sxs-lookup"><span data-stu-id="cb587-144">That is why this code example uses the names `TFirst` and `TSecond`.) To get the type of the constructor argument, start with the generic type definition `IEnumerable<T>` and call <xref:System.Type.MakeGenericType%2A> with the first generic type parameter of `List<T>`.</span></span> <span data-ttu-id="cb587-145">建構函式引數清單必須當成陣列傳遞，本例中只有一個引數。</span><span class="sxs-lookup"><span data-stu-id="cb587-145">The constructor argument list must be passed as an array, with just one argument in this case.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="cb587-146">當您在 C# 中使用 `typeof` 運算子時，泛型型別定義會表示為 `IEnumerable<>`；在 Visual Basic 中使用 `GetType` 運算子時，會表示為 `IEnumerable(Of )`。</span><span class="sxs-lookup"><span data-stu-id="cb587-146">The generic type definition is expressed as `IEnumerable<>` when you use the `typeof` operator in C#, or `IEnumerable(Of )` when you use the `GetType` operator in Visual Basic.</span></span>  
  
     <span data-ttu-id="cb587-147">現在，在泛型型別定義上呼叫 <xref:System.Type.GetConstructor%2A>，即可能取得 `List<T>` 的建構函式。</span><span class="sxs-lookup"><span data-stu-id="cb587-147">Now it is possible to get the constructor of `List<T>` by calling <xref:System.Type.GetConstructor%2A> on the generic type definition.</span></span> <span data-ttu-id="cb587-148">若要將此建構函式轉換成對應的 `List<TFirst>` 的建構函式，請從 `List<T>` 將 `List<TFirst>` 和建構函式傳遞至靜態的 <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-148">To convert this constructor to the corresponding constructor of `List<TFirst>`, pass `List<TFirst>` and the constructor from `List<T>` to the static <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29?displayProperty=nameWithType> method.</span></span>  
  
     [!code-cpp[EmitGenericType#23](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#23)]
     [!code-csharp[EmitGenericType#23](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#23)]
     [!code-vb[EmitGenericType#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#23)]  
  
10. <span data-ttu-id="cb587-149">建立類型並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="cb587-149">Create the type and save the file.</span></span>  
  
     [!code-cpp[EmitGenericType#8](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#8)]
     [!code-csharp[EmitGenericType#8](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#8)]
     [!code-vb[EmitGenericType#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#8)]  
  
11. <span data-ttu-id="cb587-150">叫用方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-150">Invoke the method.</span></span> <span data-ttu-id="cb587-151">`ExampleMethod` 不是泛型，但其所屬類型是泛型，因此為取得可以叫用的 <xref:System.Reflection.MethodInfo>，必須從 `Sample` 的類型定義建立建構的類型。</span><span class="sxs-lookup"><span data-stu-id="cb587-151">`ExampleMethod` is not generic, but the type it belongs to is generic, so in order to get a <xref:System.Reflection.MethodInfo> that can be invoked it is necessary to create a constructed type from the type definition for `Sample`.</span></span> <span data-ttu-id="cb587-152">建構的類型使用符合 `TFirst` 條件約束的 `Example` 類別，因為它是參考型別，且有預設的無參數建構函式；也使用符合 `TSecond` 條件約束的 `ExampleDerived` 類別。</span><span class="sxs-lookup"><span data-stu-id="cb587-152">The constructed type uses the `Example` class, which satisfies the constraints on `TFirst` because it is a reference type and has a default parameterless constructor, and the `ExampleDerived` class which satisfies the constraints on `TSecond`.</span></span> <span data-ttu-id="cb587-153">（的程式碼 `ExampleDerived` 可在範例程式碼一節中找到）。這兩種類型會傳遞至 <xref:System.Type.MakeGenericType%2A> ，以建立結構化類型。</span><span class="sxs-lookup"><span data-stu-id="cb587-153">(The code for `ExampleDerived` can be found in the example code section.) These two types are passed to <xref:System.Type.MakeGenericType%2A> to create the constructed type.</span></span> <span data-ttu-id="cb587-154">然後，使用 <xref:System.Type.GetMethod%2A> 方法取得 <xref:System.Reflection.MethodInfo>。</span><span class="sxs-lookup"><span data-stu-id="cb587-154">The <xref:System.Reflection.MethodInfo> is then obtained using the <xref:System.Type.GetMethod%2A> method.</span></span>  
  
     [!code-cpp[EmitGenericType#9](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#9)]
     [!code-csharp[EmitGenericType#9](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#9)]
     [!code-vb[EmitGenericType#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#9)]  
  
12. <span data-ttu-id="cb587-155">下列程式碼會建立 `Example` 物件的陣列，將該陣列放在代表要叫用之方法引數的類型 <xref:System.Object> 陣列中，並將它們傳遞至 <xref:System.Reflection.MethodBase.Invoke%28System.Object%2CSystem.Object%5B%5D%29> 方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-155">The following code creates an array of `Example` objects, places that array in an array of type <xref:System.Object> representing the arguments of the method to be invoked, and passes them to the <xref:System.Reflection.MethodBase.Invoke%28System.Object%2CSystem.Object%5B%5D%29> method.</span></span> <span data-ttu-id="cb587-156"><xref:System.Reflection.MethodBase.Invoke%2A> 方法的第一個引數為 Null 參考，因為方法是 `static`。</span><span class="sxs-lookup"><span data-stu-id="cb587-156">The first argument of the <xref:System.Reflection.MethodBase.Invoke%2A> method is a null reference because the method is `static`.</span></span>  
  
     [!code-cpp[EmitGenericType#10](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#10)]
     [!code-csharp[EmitGenericType#10](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#10)]
     [!code-vb[EmitGenericType#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#10)]  
  
## <a name="example"></a><span data-ttu-id="cb587-157">範例</span><span class="sxs-lookup"><span data-stu-id="cb587-157">Example</span></span>  
 <span data-ttu-id="cb587-158">下列程式碼範例會定義名為 `Sample` 的類別，以及一個基底類別和兩個介面。</span><span class="sxs-lookup"><span data-stu-id="cb587-158">The following code example defines a class named `Sample`, along with a base class and two interfaces.</span></span> <span data-ttu-id="cb587-159">程式會為 `Sample` 定義兩個泛型型別參數，將它轉換成泛型型別。</span><span class="sxs-lookup"><span data-stu-id="cb587-159">The program defines two generic type parameters for `Sample`, turning it into a generic type.</span></span> <span data-ttu-id="cb587-160">型別參數是唯一可將類型變成泛型的物件。</span><span class="sxs-lookup"><span data-stu-id="cb587-160">Type parameters are the only thing that makes a type generic.</span></span> <span data-ttu-id="cb587-161">程式會顯示定義型別參數之前和之後的測試訊息，以顯示此變化。</span><span class="sxs-lookup"><span data-stu-id="cb587-161">The program shows this by displaying a test message before and after the definition of the type parameters.</span></span>  
  
 <span data-ttu-id="cb587-162">使用基底類別和介面的型別參數 `TSecond` 用於示範類別和介面條件約束，而型別參數 `TFirst` 用於示範特殊條件約束。</span><span class="sxs-lookup"><span data-stu-id="cb587-162">The type parameter `TSecond` is used to demonstrate class and interface constraints, using the base class and interfaces, and the type parameter `TFirst` is used to demonstrate special constraints.</span></span>  
  
 <span data-ttu-id="cb587-163">程式碼範例會定義欄位和方法，針對欄位類別和參數使用類別的型別參數，並傳回方法的類型。</span><span class="sxs-lookup"><span data-stu-id="cb587-163">The code example defines a field and a method using the class's type parameters for the field type and for the parameter and return type of the method.</span></span>  
  
 <span data-ttu-id="cb587-164">建立 `Sample` 類別之後，即叫用方法。</span><span class="sxs-lookup"><span data-stu-id="cb587-164">After the `Sample` class has been created, the method is invoked.</span></span>  
  
 <span data-ttu-id="cb587-165">程式包含兩種方法，一種會列出泛型型別的相關資訊，一種會列出型別參數的特殊條件約束。</span><span class="sxs-lookup"><span data-stu-id="cb587-165">The program includes a method that lists information about a generic type, and a method that lists the special constraints on a type parameter.</span></span> <span data-ttu-id="cb587-166">這些方法用來顯示已完成之 `Sample` 類別的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cb587-166">These methods are used to display information about the finished `Sample` class.</span></span>  
  
 <span data-ttu-id="cb587-167">程式會在磁碟儲存已完成的模組 `GenericEmitExample1.dll`，因此您可以用 [Ildasm.exe (IL 反組譯工具)](../tools/ildasm-exe-il-disassembler.md) 開啟它，並檢查 MSIL 是否有 `Sample` 類別。</span><span class="sxs-lookup"><span data-stu-id="cb587-167">The program saves the finished module to disk as `GenericEmitExample1.dll`, so you can open it with the [Ildasm.exe (IL Disassembler)](../tools/ildasm-exe-il-disassembler.md) and examine the MSIL for the `Sample` class.</span></span>  
  
 [!code-cpp[EmitGenericType#1](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#1)]
 [!code-csharp[EmitGenericType#1](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#1)]
 [!code-vb[EmitGenericType#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="cb587-168">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cb587-168">See also</span></span>

- <xref:System.Reflection.Emit.GenericTypeParameterBuilder>
- <span data-ttu-id="cb587-169">[使用反映發出](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="cb587-169">[Using Reflection Emit](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))</span></span>
- <span data-ttu-id="cb587-170">[反映發出動態組件案例](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tt9483fk(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="cb587-170">[Reflection Emit Dynamic Assembly Scenarios](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tt9483fk(v=vs.100))</span></span>

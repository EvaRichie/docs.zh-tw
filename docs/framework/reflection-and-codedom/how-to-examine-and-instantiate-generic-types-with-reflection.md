---
title: 如何：使用反映檢視和執行個體化泛型類型
description: 瞭解如何使用反映檢查和具現化泛型型別。 使用 IsGenericType、IsGenericParameter 和 GenericParameterPosition 屬性。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection, generic types
- generics [.NET Framework], reflection
ms.assetid: f93b03b0-1778-43fc-bc6d-35983d210e74
ms.openlocfilehash: 34efca4a26b0ab3739d19b793237532ec9f4f15e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263434"
---
# <a name="how-to-examine-and-instantiate-generic-types-with-reflection"></a><span data-ttu-id="66355-104">如何：使用反映檢視和執行個體化泛型類型</span><span class="sxs-lookup"><span data-stu-id="66355-104">How to: Examine and Instantiate Generic Types with Reflection</span></span>

<span data-ttu-id="66355-105">取得泛型型別相關資訊的方式和取得其他類型相關資訊的方式一樣：檢查代表泛型型別的 <xref:System.Type> 物件。</span><span class="sxs-lookup"><span data-stu-id="66355-105">Information about generic types is obtained in the same way as information about other types: by examining a <xref:System.Type> object that represents the generic type.</span></span> <span data-ttu-id="66355-106">主要差異是泛型型別有代表其泛型型別參數的 <xref:System.Type> 物件清單。</span><span class="sxs-lookup"><span data-stu-id="66355-106">The principle difference is that a generic type has a list of <xref:System.Type> objects representing its generic type parameters.</span></span> <span data-ttu-id="66355-107">本節的第一個程序是檢查泛型型別。</span><span class="sxs-lookup"><span data-stu-id="66355-107">The first procedure in this section examines generic types.</span></span>  
  
 <span data-ttu-id="66355-108">您可以將型別引數繫結至泛型型別定義的型別參數，建立代表建構類型的 <xref:System.Type> 物件。</span><span class="sxs-lookup"><span data-stu-id="66355-108">You can create a <xref:System.Type> object that represents a constructed type by binding type arguments to the type parameters of a generic type definition.</span></span> <span data-ttu-id="66355-109">第二個程序即示範此作業。</span><span class="sxs-lookup"><span data-stu-id="66355-109">The second procedure demonstrates this.</span></span>  
  
### <a name="to-examine-a-generic-type-and-its-type-parameters"></a><span data-ttu-id="66355-110">檢查泛型型別及其型別參數</span><span class="sxs-lookup"><span data-stu-id="66355-110">To examine a generic type and its type parameters</span></span>  
  
1. <span data-ttu-id="66355-111">取得表示泛型型別的 <xref:System.Type> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="66355-111">Get an instance of <xref:System.Type> that represents the generic type.</span></span> <span data-ttu-id="66355-112">在下列程式碼中，類型是使用 C# `typeof` 運算子取得 (Visual Basic 為 `GetType`，Visual C++ 為 `typeid`)。</span><span class="sxs-lookup"><span data-stu-id="66355-112">In the following code, the type is obtained using the C# `typeof` operator (`GetType` in Visual Basic, `typeid` in Visual C++).</span></span> <span data-ttu-id="66355-113">請參閱 <xref:System.Type> 類別主題了解取得 <xref:System.Type> 物件的其他方法。</span><span class="sxs-lookup"><span data-stu-id="66355-113">See the <xref:System.Type> class topic for other ways to get a <xref:System.Type> object.</span></span> <span data-ttu-id="66355-114">請注意，在此程序的其餘部分中，類型是包含在名為 `t` 的方法參數中。</span><span class="sxs-lookup"><span data-stu-id="66355-114">Note that in the rest of this procedure, the type is contained in a method parameter named `t`.</span></span>  
  
     [!code-cpp[HowToGeneric#2](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#2)]
     [!code-csharp[HowToGeneric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#2)]
     [!code-vb[HowToGeneric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#2)]  
  
2. <span data-ttu-id="66355-115">使用 <xref:System.Type.IsGenericType%2A> 屬性判斷類型是否為泛型，使用 <xref:System.Type.IsGenericTypeDefinition%2A> 屬性判斷類型是否為泛型型別定義。</span><span class="sxs-lookup"><span data-stu-id="66355-115">Use the <xref:System.Type.IsGenericType%2A> property to determine whether the type is generic, and use the <xref:System.Type.IsGenericTypeDefinition%2A> property to determine whether the type is a generic type definition.</span></span>  
  
     [!code-cpp[HowToGeneric#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#3)]
     [!code-csharp[HowToGeneric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#3)]
     [!code-vb[HowToGeneric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#3)]  
  
3. <span data-ttu-id="66355-116">使用 <xref:System.Type.GetGenericArguments%2A> 方法取得包含泛型型別引數的陣列。</span><span class="sxs-lookup"><span data-stu-id="66355-116">Get an array that contains the generic type arguments, using the <xref:System.Type.GetGenericArguments%2A> method.</span></span>  
  
     [!code-cpp[HowToGeneric#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#4)]
     [!code-csharp[HowToGeneric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#4)]
     [!code-vb[HowToGeneric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#4)]  
  
4. <span data-ttu-id="66355-117">每個型別引數都要使用 <xref:System.Type.IsGenericParameter%2A> 屬性判斷它是型別參數 (例如，在泛型型別定義中)，還是已針對型別參數指定的類型 (例如，在建構的類型中)。</span><span class="sxs-lookup"><span data-stu-id="66355-117">For each type argument, determine whether it is a type parameter (for example, in a generic type definition) or a type that has been specified for a type parameter (for example, in a constructed type), using the <xref:System.Type.IsGenericParameter%2A> property.</span></span>  
  
     [!code-cpp[HowToGeneric#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#5)]
     [!code-csharp[HowToGeneric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#5)]
     [!code-vb[HowToGeneric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#5)]  
  
5. <span data-ttu-id="66355-118">在型別系統中，泛型型別參數是由 <xref:System.Type> 執行個體表示，就像一般的類型一 樣。</span><span class="sxs-lookup"><span data-stu-id="66355-118">In the type system, a generic type parameter is represented by an instance of <xref:System.Type>, just as ordinary types are.</span></span> <span data-ttu-id="66355-119">下列程式碼會顯示表示泛型型別參數之 <xref:System.Type> 物件的名稱和參數位置。</span><span class="sxs-lookup"><span data-stu-id="66355-119">The following code displays the name and parameter position of a <xref:System.Type> object that represents a generic type parameter.</span></span> <span data-ttu-id="66355-120">參數位置在此為一般的資訊，但當您檢查曾用為其他泛型型別之型別引數的型別參數時，它就很有意思了。</span><span class="sxs-lookup"><span data-stu-id="66355-120">The parameter position is trivial information here; it is of more interest when you are examining a type parameter that has been used as a type argument of another generic type.</span></span>  
  
     [!code-cpp[HowToGeneric#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#6)]
     [!code-csharp[HowToGeneric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#6)]
     [!code-vb[HowToGeneric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#6)]  
  
6. <span data-ttu-id="66355-121">使用 <xref:System.Type.GetGenericParameterConstraints%2A> 方法取得單一陣列中的所有條件約束，來判斷泛型型別參數的基底類型條件約束和介面條件約束。</span><span class="sxs-lookup"><span data-stu-id="66355-121">Determine the base type constraint and the interface constraints of a generic type parameter by using the <xref:System.Type.GetGenericParameterConstraints%2A> method to obtain all the constraints in a single array.</span></span> <span data-ttu-id="66355-122">條件約束不保證任何特定順序。</span><span class="sxs-lookup"><span data-stu-id="66355-122">Constraints are not guaranteed to be in any particular order.</span></span>  
  
     [!code-cpp[HowToGeneric#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#7)]
     [!code-csharp[HowToGeneric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#7)]
     [!code-vb[HowToGeneric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#7)]  
  
7. <span data-ttu-id="66355-123">使用 <xref:System.Type.GenericParameterAttributes%2A> 屬性探索型別參數上的特殊條件約束，例如需要它為參考型別。</span><span class="sxs-lookup"><span data-stu-id="66355-123">Use the <xref:System.Type.GenericParameterAttributes%2A> property to discover the special constraints on a type parameter, such as requiring that it be a reference type.</span></span> <span data-ttu-id="66355-124">屬性也包含代表差異的值，您可以關閉遮罩，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="66355-124">The property also includes values that represent variance, which you can mask off as shown in the following code.</span></span>  
  
     [!code-cpp[HowToGeneric#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#8)]
     [!code-csharp[HowToGeneric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#8)]
     [!code-vb[HowToGeneric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#8)]  
  
8. <span data-ttu-id="66355-125">特殊條件約束屬性是旗標，而不代表任何特殊條件約束的相同旗標 (<xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType>)，也不代表任何共變數或反變數。</span><span class="sxs-lookup"><span data-stu-id="66355-125">The special constraint attributes are flags, and the same flag (<xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType>) that represents no special constraints also represents no covariance or contravariance.</span></span> <span data-ttu-id="66355-126">因此，若要測試任一條件，您必須使用適當的遮罩。</span><span class="sxs-lookup"><span data-stu-id="66355-126">Thus, to test for either of these conditions you must use the appropriate mask.</span></span> <span data-ttu-id="66355-127">本例使用 <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType> 隔離特殊條件約束旗標。</span><span class="sxs-lookup"><span data-stu-id="66355-127">In this case, use <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType> to isolate the special constraint flags.</span></span>  
  
     [!code-cpp[HowToGeneric#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#9)]
     [!code-csharp[HowToGeneric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#9)]
     [!code-vb[HowToGeneric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#9)]  
  
## <a name="constructing-an-instance-of-a-generic-type"></a><span data-ttu-id="66355-128">建構泛型型別的執行個體</span><span class="sxs-lookup"><span data-stu-id="66355-128">Constructing an Instance of a Generic Type</span></span>  

 <span data-ttu-id="66355-129">泛型型別就像範本。</span><span class="sxs-lookup"><span data-stu-id="66355-129">A generic type is like a template.</span></span> <span data-ttu-id="66355-130">除非指定其泛型型別參數的真實類型，否則無法建立它的執行個體。</span><span class="sxs-lookup"><span data-stu-id="66355-130">You cannot create instances of it unless you specify real types for its generic type parameters.</span></span> <span data-ttu-id="66355-131">若要在執行階段使用反映執行這項操作，需要 <xref:System.Type.MakeGenericType%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="66355-131">To do this at run time, using reflection, requires the <xref:System.Type.MakeGenericType%2A> method.</span></span>  
  
#### <a name="to-construct-an-instance-of-a-generic-type"></a><span data-ttu-id="66355-132">建構泛型型別的執行個體</span><span class="sxs-lookup"><span data-stu-id="66355-132">To construct an instance of a generic type</span></span>  
  
1. <span data-ttu-id="66355-133">取得表示泛型型別的 <xref:System.Type> 物件。</span><span class="sxs-lookup"><span data-stu-id="66355-133">Get a <xref:System.Type> object that represents the generic type.</span></span> <span data-ttu-id="66355-134">下列程式碼以兩種方式取得泛型型別 <xref:System.Collections.Generic.Dictionary%602>：使用 <xref:System.Type.GetType%28System.String%29?displayProperty=nameWithType> 方法多載及描述類型的字串，以及在建構的類型 `Dictionary\<String, Example>`(Visual Basic 為 `Dictionary(Of String, Example)`) 上呼叫 <xref:System.Type.GetGenericTypeDefinition%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="66355-134">The following code gets the generic type <xref:System.Collections.Generic.Dictionary%602> in two different ways: by using the <xref:System.Type.GetType%28System.String%29?displayProperty=nameWithType> method overload with a string describing the type, and by calling the <xref:System.Type.GetGenericTypeDefinition%2A> method on the constructed type `Dictionary\<String, Example>` (`Dictionary(Of String, Example)` in Visual Basic).</span></span> <span data-ttu-id="66355-135"><xref:System.Type.MakeGenericType%2A> 方法需要泛型型別定義。</span><span class="sxs-lookup"><span data-stu-id="66355-135">The <xref:System.Type.MakeGenericType%2A> method requires a generic type definition.</span></span>  
  
     [!code-cpp[HowToGeneric#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#10)]
     [!code-csharp[HowToGeneric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#10)]
     [!code-vb[HowToGeneric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#10)]  
  
2. <span data-ttu-id="66355-136">建構型別引數陣列來替代型別參數。</span><span class="sxs-lookup"><span data-stu-id="66355-136">Construct an array of type arguments to substitute for the type parameters.</span></span> <span data-ttu-id="66355-137">陣列必須包含正確的 <xref:System.Type> 物件數，依型別參數清單中的出現順序排序。</span><span class="sxs-lookup"><span data-stu-id="66355-137">The array must contain the correct number of <xref:System.Type> objects, in the same order as they appear in the type parameter list.</span></span> <span data-ttu-id="66355-138">本例中的索引鍵 (第一個型別參數) 類型是 <xref:System.String>，字典中的值則是名為 `Example` 的類別執行個體。</span><span class="sxs-lookup"><span data-stu-id="66355-138">In this case, the key (first type parameter) is of type <xref:System.String>, and the values in the dictionary are instances of a class named `Example`.</span></span>  
  
     [!code-cpp[HowToGeneric#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#11)]
     [!code-csharp[HowToGeneric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#11)]
     [!code-vb[HowToGeneric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#11)]  
  
3. <span data-ttu-id="66355-139">呼叫 <xref:System.Type.MakeGenericType%2A> 方法將型別引數繫結至型別參數，並建構類型。</span><span class="sxs-lookup"><span data-stu-id="66355-139">Call the <xref:System.Type.MakeGenericType%2A> method to bind the type arguments to the type parameters and construct the type.</span></span>  
  
     [!code-cpp[HowToGeneric#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#12)]
     [!code-csharp[HowToGeneric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#12)]
     [!code-vb[HowToGeneric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#12)]  
  
4. <span data-ttu-id="66355-140">使用 <xref:System.Activator.CreateInstance%28System.Type%29> 方法多載來建立建構類型的物件。</span><span class="sxs-lookup"><span data-stu-id="66355-140">Use the <xref:System.Activator.CreateInstance%28System.Type%29> method overload to create an object of the constructed type.</span></span> <span data-ttu-id="66355-141">下列程式碼會將 `Example` 類別的兩個執行個體儲存在產生的 `Dictionary<String, Example>` 物件中。</span><span class="sxs-lookup"><span data-stu-id="66355-141">The following code stores two instances of the `Example` class in the resulting `Dictionary<String, Example>` object.</span></span>  
  
     [!code-cpp[HowToGeneric#13](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#13)]
     [!code-csharp[HowToGeneric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#13)]
     [!code-vb[HowToGeneric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#13)]  
  
## <a name="example"></a><span data-ttu-id="66355-142">範例</span><span class="sxs-lookup"><span data-stu-id="66355-142">Example</span></span>  

 <span data-ttu-id="66355-143">下列程式碼範例會定義 `DisplayGenericType` 方法，檢查程式碼中的泛型型別定義和建構的類型，並顯示其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66355-143">The following code example defines a `DisplayGenericType` method to examine the generic type definitions and constructed types used in the code and display their information.</span></span> <span data-ttu-id="66355-144">`DisplayGenericType` 方法示範如何使用 <xref:System.Type.IsGenericType%2A>、<xref:System.Type.IsGenericParameter%2A> 和 <xref:System.Type.GenericParameterPosition%2A> 屬性以及 <xref:System.Type.GetGenericArguments%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="66355-144">The `DisplayGenericType` method shows how to use the <xref:System.Type.IsGenericType%2A>, <xref:System.Type.IsGenericParameter%2A>, and <xref:System.Type.GenericParameterPosition%2A> properties and the <xref:System.Type.GetGenericArguments%2A> method.</span></span>  
  
 <span data-ttu-id="66355-145">此範例也會定義 `DisplayGenericParameter` 方法，檢查泛型型別參數，並顯示其條件約束。</span><span class="sxs-lookup"><span data-stu-id="66355-145">The example also defines a `DisplayGenericParameter` method to examine a generic type parameter and display its constraints.</span></span>  
  
 <span data-ttu-id="66355-146">程式碼範例會定義一組測試類型，包括說明型別參數條件約束的泛型型別，以及示範如何顯示這些類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66355-146">The code example defines a set of test types, including a generic type that illustrates type parameter constraints, and shows how to display information about these types.</span></span>  
  
 <span data-ttu-id="66355-147">此範例會建立型別引數陣列並呼叫 <xref:System.Type.MakeGenericType%2A> 方法，從 <xref:System.Collections.Generic.Dictionary%602> 類別建構類型。</span><span class="sxs-lookup"><span data-stu-id="66355-147">The example constructs a type from the <xref:System.Collections.Generic.Dictionary%602> class by creating an array of type arguments and calling the <xref:System.Type.MakeGenericType%2A> method.</span></span> <span data-ttu-id="66355-148">程式會比較使用 <xref:System.Type.MakeGenericType%2A> 建構的 <xref:System.Type> 物件和使用 `typeof` (Visual Basic 為 `GetType`) 取得的 <xref:System.Type> 物件，示範它們是一樣的。</span><span class="sxs-lookup"><span data-stu-id="66355-148">The program compares the <xref:System.Type> object constructed using <xref:System.Type.MakeGenericType%2A> with a <xref:System.Type> object obtained using `typeof` (`GetType` in Visual Basic), demonstrating that they are the same.</span></span> <span data-ttu-id="66355-149">同樣地，程式會使用 <xref:System.Type.GetGenericTypeDefinition%2A> 方法取得建構類型的泛型型別定義，和代表 <xref:System.Collections.Generic.Dictionary%602> 類別的 <xref:System.Type> 物件相比較。</span><span class="sxs-lookup"><span data-stu-id="66355-149">Similarly, the program uses the <xref:System.Type.GetGenericTypeDefinition%2A> method to obtain the generic type definition of the constructed type, and compares it to the <xref:System.Type> object representing the <xref:System.Collections.Generic.Dictionary%602> class.</span></span>  
  
 [!code-cpp[HowToGeneric#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#1)]
 [!code-csharp[HowToGeneric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#1)]
 [!code-vb[HowToGeneric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="66355-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66355-150">See also</span></span>

- <xref:System.Type>
- <xref:System.Reflection.MethodInfo>
- [<span data-ttu-id="66355-151">反映和泛用類型</span><span class="sxs-lookup"><span data-stu-id="66355-151">Reflection and Generic Types</span></span>](reflection-and-generic-types.md)
- [<span data-ttu-id="66355-152">檢視類型資訊</span><span class="sxs-lookup"><span data-stu-id="66355-152">Viewing Type Information</span></span>](viewing-type-information.md)
- [<span data-ttu-id="66355-153">泛型</span><span class="sxs-lookup"><span data-stu-id="66355-153">Generics</span></span>](../../standard/generics/index.md)

---
title: 撰寫自訂屬性
description: 在 .NET 中設計您自己的自訂屬性。 自訂屬性基本上是直接或間接衍生自 System.object 的類別。
ms.date: 07/17/2018
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- multiple attribute instances
- AttributeTargets enumeration
- attributes [.NET], custom
- AllowMultiple property
- custom attributes
- AttributeUsageAttribute class, custom attributes
- Inherited property
- attribute classes, declaring
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
ms.openlocfilehash: 4c7051fa45dfc23a09b037b78030ff90af182a7d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829007"
---
# <a name="writing-custom-attributes"></a><span data-ttu-id="2e453-104">撰寫自訂屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-104">Writing Custom Attributes</span></span>
<span data-ttu-id="2e453-105">若要設計您自己的自訂屬性，並不需要精通很多新概念。</span><span class="sxs-lookup"><span data-stu-id="2e453-105">To design your own custom attributes, you do not need to master many new concepts.</span></span> <span data-ttu-id="2e453-106">假如您擅長物件導向的程式設計，且瞭解如何設計類別，那麼您就已經擁有大部分所需的知識。</span><span class="sxs-lookup"><span data-stu-id="2e453-106">If you are familiar with object-oriented programming and know how to design classes, you already have most of the knowledge needed.</span></span> <span data-ttu-id="2e453-107">自訂屬性基本上是一種直接或間接衍生自 <xref:System.Attribute?displayProperty=nameWithType>的傳統類別。</span><span class="sxs-lookup"><span data-stu-id="2e453-107">Custom attributes are essentially traditional classes that derive directly or indirectly from <xref:System.Attribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="2e453-108">自訂屬性就像傳統類別一樣，含有儲存和擷取資料的方法。</span><span class="sxs-lookup"><span data-stu-id="2e453-108">Just like traditional classes, custom attributes contain methods that store and retrieve data.</span></span>  
  
 <span data-ttu-id="2e453-109">正確設計自訂屬性的主要步驟如下：</span><span class="sxs-lookup"><span data-stu-id="2e453-109">The primary steps to properly design custom attribute classes are as follows:</span></span>  
  
- [<span data-ttu-id="2e453-110">套用 AttributeUsageAttribute</span><span class="sxs-lookup"><span data-stu-id="2e453-110">Applying the AttributeUsageAttribute</span></span>](#applying-the-attributeusageattribute)  
  
- [<span data-ttu-id="2e453-111">宣告屬性類別</span><span class="sxs-lookup"><span data-stu-id="2e453-111">Declaring the attribute class</span></span>](#declaring-the-attribute-class)  
  
- [<span data-ttu-id="2e453-112">宣告函式</span><span class="sxs-lookup"><span data-stu-id="2e453-112">Declaring constructors</span></span>](#declaring-constructors)  
  
- [<span data-ttu-id="2e453-113">宣告屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-113">Declaring properties</span></span>](#declaring-properties)  
  
 <span data-ttu-id="2e453-114">本節會一一說明每個步驟，並於結尾提供 [自訂屬性範例](#custom-attribute-example)。</span><span class="sxs-lookup"><span data-stu-id="2e453-114">This section describes each of these steps and concludes with a [custom attribute example](#custom-attribute-example).</span></span>  
  
## <a name="applying-the-attributeusageattribute"></a><span data-ttu-id="2e453-115">套用 AttributeUsageAttribute</span><span class="sxs-lookup"><span data-stu-id="2e453-115">Applying the AttributeUsageAttribute</span></span>  
 <span data-ttu-id="2e453-116">自訂屬性宣告的開頭為 <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>，它定義您屬性類別的一些主要特性。</span><span class="sxs-lookup"><span data-stu-id="2e453-116">A custom attribute declaration begins with the <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>, which defines some of the key characteristics of your attribute class.</span></span> <span data-ttu-id="2e453-117">例如，您可以指定屬性是否可由其他類別繼承或指定屬性可以套用至哪一個項目。</span><span class="sxs-lookup"><span data-stu-id="2e453-117">For example, you can specify whether your attribute can be inherited by other classes or specify which elements the attribute can be applied to.</span></span> <span data-ttu-id="2e453-118">下列程式碼片段示範如何使用 <xref:System.AttributeUsageAttribute>。</span><span class="sxs-lookup"><span data-stu-id="2e453-118">The following code fragment demonstrates how to use the <xref:System.AttributeUsageAttribute>.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 <span data-ttu-id="2e453-119"><xref:System.AttributeUsageAttribute> 有三個建立自訂屬性所需的重要成員： [AttributeTargets](#attributetargets-member)、 [Inherited](#inherited-property)和 [AllowMultiple](#allowmultiple-property)。</span><span class="sxs-lookup"><span data-stu-id="2e453-119">The <xref:System.AttributeUsageAttribute> has three members that are important for the creation of custom attributes: [AttributeTargets](#attributetargets-member), [Inherited](#inherited-property), and [AllowMultiple](#allowmultiple-property).</span></span>  
  
### <a name="attributetargets-member"></a><span data-ttu-id="2e453-120">AttributeTargets 成員</span><span class="sxs-lookup"><span data-stu-id="2e453-120">AttributeTargets Member</span></span>  
 <span data-ttu-id="2e453-121">在上述範例中，指定了 <xref:System.AttributeTargets.All?displayProperty=nameWithType> ，指出此屬性可以套用到所有程式元素。</span><span class="sxs-lookup"><span data-stu-id="2e453-121">In the previous example, <xref:System.AttributeTargets.All?displayProperty=nameWithType> is specified, indicating that this attribute can be applied to all program elements.</span></span> <span data-ttu-id="2e453-122">或者，您也可以指定 <xref:System.AttributeTargets.Class?displayProperty=nameWithType>，指出您的屬性可以套用到類別，或指定 <xref:System.AttributeTargets.Method?displayProperty=nameWithType>，指出屬性只能套用至方法。</span><span class="sxs-lookup"><span data-stu-id="2e453-122">Alternatively, you can specify <xref:System.AttributeTargets.Class?displayProperty=nameWithType>, indicating that your attribute can be applied only to a class, or <xref:System.AttributeTargets.Method?displayProperty=nameWithType>, indicating that your attribute can be applied only to a method.</span></span> <span data-ttu-id="2e453-123">所有的程式項目都可以用這種方式透過自訂屬性標示為描述。</span><span class="sxs-lookup"><span data-stu-id="2e453-123">All program elements can be marked for description by a custom attribute in this manner.</span></span>  
  
 <span data-ttu-id="2e453-124">您也可以傳遞多個 <xref:System.AttributeTargets> 值。</span><span class="sxs-lookup"><span data-stu-id="2e453-124">You can also pass multiple <xref:System.AttributeTargets> values.</span></span> <span data-ttu-id="2e453-125">下列程式碼片段指定自訂屬性可以套用至任何類別或方法。</span><span class="sxs-lookup"><span data-stu-id="2e453-125">The following code fragment specifies that a custom attribute can be applied to any class or method.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
### <a name="inherited-property"></a><span data-ttu-id="2e453-126">Inherited 屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-126">Inherited Property</span></span>  
 <span data-ttu-id="2e453-127"><xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> 屬性會指出，衍生自套用您屬性之類別的類別，是否可繼承您的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-127">The <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> property indicates whether your attribute can be inherited by classes that are derived from the classes to which your attribute is applied.</span></span> <span data-ttu-id="2e453-128">此屬性會接受 `true` (預設值) 或 `false` 旗標。</span><span class="sxs-lookup"><span data-stu-id="2e453-128">This property takes either a `true` (the default) or `false` flag.</span></span> <span data-ttu-id="2e453-129">在下列範例中，`MyAttribute` 的預設 <xref:System.AttributeUsageAttribute.Inherited%2A> 值為 `true`，而 `YourAttribute` 的 <xref:System.AttributeUsageAttribute.Inherited%2A> 值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="2e453-129">In the following example, `MyAttribute` has a default <xref:System.AttributeUsageAttribute.Inherited%2A> value of `true`, while `YourAttribute` has an <xref:System.AttributeUsageAttribute.Inherited%2A> value of `false`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 <span data-ttu-id="2e453-130">兩個屬性接著會套用到基底類別 `MyClass` 中的方法。</span><span class="sxs-lookup"><span data-stu-id="2e453-130">The two attributes are then applied to a method in the base class `MyClass`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 <span data-ttu-id="2e453-131">最後，會從基底類別 `YourClass` 繼承類別 `MyClass`。</span><span class="sxs-lookup"><span data-stu-id="2e453-131">Finally, the class `YourClass` is inherited from the base class `MyClass`.</span></span> <span data-ttu-id="2e453-132">此方法 `MyMethod` 顯示 `MyAttribute`，但不是 `YourAttribute`。</span><span class="sxs-lookup"><span data-stu-id="2e453-132">The method `MyMethod` shows `MyAttribute`, but not `YourAttribute`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
### <a name="allowmultiple-property"></a><span data-ttu-id="2e453-133">AllowMultiple 屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-133">AllowMultiple Property</span></span>  
 <span data-ttu-id="2e453-134"><xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> 屬性會指出項目上是否可以有您屬性的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2e453-134">The <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> property indicates whether multiple instances of your attribute can exist on an element.</span></span> <span data-ttu-id="2e453-135">如果設定為 `true`，則允許多個執行個體；如果設定為 `false` (預設值)，則只允許一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2e453-135">If set to `true`, multiple instances are allowed; if set to `false` (the default), only one instance is allowed.</span></span>  
  
 <span data-ttu-id="2e453-136">在下列範例中，`MyAttribute` 有預設的 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 值 `false`，而 `YourAttribute` 有 `true` 的值。</span><span class="sxs-lookup"><span data-stu-id="2e453-136">In the following example, `MyAttribute` has a default <xref:System.AttributeUsageAttribute.AllowMultiple%2A> value of `false`, while `YourAttribute` has a value of `true`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 <span data-ttu-id="2e453-137">當套用這些屬性的多個執行個體時， `MyAttribute` 會產生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="2e453-137">When multiple instances of these attributes are applied, `MyAttribute` produces a compiler error.</span></span> <span data-ttu-id="2e453-138">下列程式碼範例示範有效的 `YourAttribute` 用法和無效的 `MyAttribute` 用法。</span><span class="sxs-lookup"><span data-stu-id="2e453-138">The following code example shows the valid use of `YourAttribute` and the invalid use of `MyAttribute`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 <span data-ttu-id="2e453-139">如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 屬性和 <xref:System.AttributeUsageAttribute.Inherited%2A> 屬性都設定為 `true`，繼承自另一個類別的類別可以繼承屬性，並在同一個子類別中套用同一屬性的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2e453-139">If both the <xref:System.AttributeUsageAttribute.AllowMultiple%2A> property and the <xref:System.AttributeUsageAttribute.Inherited%2A> property are set to `true`, a class that is inherited from another class can inherit an attribute and have another instance of the same attribute applied in the same child class.</span></span> <span data-ttu-id="2e453-140">如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 設定為 `false`，父類別中任何屬性的值，都會被子類別中相同屬性的新執行個體覆寫。</span><span class="sxs-lookup"><span data-stu-id="2e453-140">If <xref:System.AttributeUsageAttribute.AllowMultiple%2A> is set to `false`, the values of any attributes in the parent class will be overwritten by new instances of the same attribute in the child class.</span></span>  
  
## <a name="declaring-the-attribute-class"></a><span data-ttu-id="2e453-141">宣告屬性類別</span><span class="sxs-lookup"><span data-stu-id="2e453-141">Declaring the Attribute Class</span></span>  
 <span data-ttu-id="2e453-142">在套用 <xref:System.AttributeUsageAttribute>之後，您可以開始定義屬性的細節。</span><span class="sxs-lookup"><span data-stu-id="2e453-142">After you apply the <xref:System.AttributeUsageAttribute>, you can begin to define the specifics of your attribute.</span></span> <span data-ttu-id="2e453-143">如下列程式碼所示，屬性類別的宣告看起來類似傳統類別的宣告。</span><span class="sxs-lookup"><span data-stu-id="2e453-143">The declaration of an attribute class looks similar to the declaration of a traditional class, as demonstrated by the following code.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 <span data-ttu-id="2e453-144">這個屬性的定義會顯示下列要點：</span><span class="sxs-lookup"><span data-stu-id="2e453-144">This attribute definition demonstrates the following points:</span></span>  
  
- <span data-ttu-id="2e453-145">屬性類別必須宣告為公用類別。</span><span class="sxs-lookup"><span data-stu-id="2e453-145">Attribute classes must be declared as public classes.</span></span>  
  
- <span data-ttu-id="2e453-146">依慣例，屬性類別的名稱會以這個字 **Attribute** 結尾。</span><span class="sxs-lookup"><span data-stu-id="2e453-146">By convention, the name of the attribute class ends with the word **Attribute**.</span></span> <span data-ttu-id="2e453-147">雖然並非必要，不過建議您遵照這個慣例以提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="2e453-147">While not required, this convention is recommended for readability.</span></span> <span data-ttu-id="2e453-148">當屬性已套用時，要不要包含 Attribute 這個字都可以。</span><span class="sxs-lookup"><span data-stu-id="2e453-148">When the attribute is applied, the inclusion of the word Attribute is optional.</span></span>  
  
- <span data-ttu-id="2e453-149">所有的屬性類別必須直接或間接繼承自 <xref:System.Attribute?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="2e453-149">All attribute classes must inherit directly or indirectly from <xref:System.Attribute?displayProperty=nameWithType>.</span></span>  
  
- <span data-ttu-id="2e453-150">在 Microsoft Visual Basic 中，所有自訂屬性的類別都必須有 <xref:System.AttributeUsageAttribute?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-150">In Microsoft Visual Basic, all custom attribute classes must have the <xref:System.AttributeUsageAttribute?displayProperty=nameWithType> attribute.</span></span>  
  
## <a name="declaring-constructors"></a><span data-ttu-id="2e453-151">宣告建構函式</span><span class="sxs-lookup"><span data-stu-id="2e453-151">Declaring Constructors</span></span>  
 <span data-ttu-id="2e453-152">屬性使用建構函式進行初始化的方式，與傳統的類別相同。</span><span class="sxs-lookup"><span data-stu-id="2e453-152">Attributes are initialized with constructors in the same way as traditional classes.</span></span> <span data-ttu-id="2e453-153">下列程式碼片段說明典型的屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="2e453-153">The following code fragment illustrates a typical attribute constructor.</span></span> <span data-ttu-id="2e453-154">這個公用建構函式會接受一個參數並將其值設定為等於成員變數。</span><span class="sxs-lookup"><span data-stu-id="2e453-154">This public constructor takes a parameter and sets a member variable equal to its value.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 <span data-ttu-id="2e453-155">您可以多載建構函式以容納不同的值組合。</span><span class="sxs-lookup"><span data-stu-id="2e453-155">You can overload the constructor to accommodate different combinations of values.</span></span> <span data-ttu-id="2e453-156">如果您也為自訂的屬性類別定義 [屬性](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) ，您可以在初始化屬性時使用具名和位置參數的組合。</span><span class="sxs-lookup"><span data-stu-id="2e453-156">If you also define a [property](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) for your custom attribute class, you can use a combination of named and positional parameters when initializing the attribute.</span></span> <span data-ttu-id="2e453-157">通常您會將所有必要的參數定義為位置，而所有選擇性參數則定義為名稱。</span><span class="sxs-lookup"><span data-stu-id="2e453-157">Typically, you define all required parameters as positional and all optional parameters as named.</span></span> <span data-ttu-id="2e453-158">在此情況下，屬性沒有必要的參數就無法初始化。</span><span class="sxs-lookup"><span data-stu-id="2e453-158">In this case, the attribute cannot be initialized without the required parameter.</span></span> <span data-ttu-id="2e453-159">所有其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="2e453-159">All other parameters are optional.</span></span> <span data-ttu-id="2e453-160">請注意在 Visual Basic 中，屬性類別的建構函式不應使用 ParamArray 引數。</span><span class="sxs-lookup"><span data-stu-id="2e453-160">Note that in Visual Basic, constructors for an attribute class should not use a ParamArray argument.</span></span>  
  
 <span data-ttu-id="2e453-161">下列程式碼範例示範如何使用選擇性和必要的參數，來套用使用先前建構函示的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-161">The following code example shows how an attribute that uses the previous constructor can be applied using optional and required parameters.</span></span> <span data-ttu-id="2e453-162">這項作業會假設屬性有一個必要的布林值和一個選擇性的字串屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-162">It assumes that the attribute has one required Boolean value and one optional string property.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
## <a name="declaring-properties"></a><span data-ttu-id="2e453-163">宣告屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-163">Declaring Properties</span></span>  
 <span data-ttu-id="2e453-164">如果您想要定義具名的參數或提供簡單的方式，來傳回屬性所儲存的值，請宣告 [屬性](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120))。</span><span class="sxs-lookup"><span data-stu-id="2e453-164">If you want to define a named parameter or provide an easy way to return the values stored by your attribute, declare a [property](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)).</span></span> <span data-ttu-id="2e453-165">屬性的屬性應該宣告為公用實體，並具有將傳回之資料類型的描述。</span><span class="sxs-lookup"><span data-stu-id="2e453-165">Attribute properties should be declared as public entities with a description of the data type that will be returned.</span></span> <span data-ttu-id="2e453-166">定義會保存您屬性值的變數，並將其與 **get** 和 **set** 方法建立關聯。</span><span class="sxs-lookup"><span data-stu-id="2e453-166">Define the variable that will hold the value of your property and associate it with the **get** and **set** methods.</span></span> <span data-ttu-id="2e453-167">下列程式碼範例示範如何在您的屬性中實作簡單的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-167">The following code example demonstrates how to implement a simple property in your attribute.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
## <a name="custom-attribute-example"></a><span data-ttu-id="2e453-168">自訂屬性範例</span><span class="sxs-lookup"><span data-stu-id="2e453-168">Custom Attribute Example</span></span>  
 <span data-ttu-id="2e453-169">本節包含先前的資訊，並說明如何設計簡單的屬性，記錄某一段程式碼的作者相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2e453-169">This section incorporates the previous information and shows how to design a simple attribute that documents information about the author of a section of code.</span></span> <span data-ttu-id="2e453-170">此範例中的屬性儲存程式設計人員的名字和層級，以及此程式碼是否經過審閱。</span><span class="sxs-lookup"><span data-stu-id="2e453-170">The attribute in this example stores the name and level of the programmer, and whether the code has been reviewed.</span></span> <span data-ttu-id="2e453-171">它會使用三個私用變數來儲存要儲存的實際值。</span><span class="sxs-lookup"><span data-stu-id="2e453-171">It uses three private variables to store the actual values to save.</span></span> <span data-ttu-id="2e453-172">每個變數都會以取得和設定值的公用屬性來表示。</span><span class="sxs-lookup"><span data-stu-id="2e453-172">Each variable is represented by a public property that gets and sets the values.</span></span> <span data-ttu-id="2e453-173">最後，建構函式會以兩個必要參數來定義。</span><span class="sxs-lookup"><span data-stu-id="2e453-173">Finally, the constructor is defined with two required parameters.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 <span data-ttu-id="2e453-174">您可以用下列其中一種方式，也就是使用完整名稱 `DeveloperAttribute`，或使用縮寫名稱 `Developer`，來套用此屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-174">You can apply this attribute using the full name, `DeveloperAttribute`, or using the abbreviated name, `Developer`, in one of the following ways.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 <span data-ttu-id="2e453-175">第一個範例示範只套用了必要具名參數的屬性，而第二個範例則示範同時套用了必要和選擇性參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e453-175">The first example shows the attribute applied with only the required named parameters, while the second example shows the attribute applied with both the required and optional parameters.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2e453-176">請參閱</span><span class="sxs-lookup"><span data-stu-id="2e453-176">See also</span></span>

- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>
- [<span data-ttu-id="2e453-177">屬性</span><span class="sxs-lookup"><span data-stu-id="2e453-177">Attributes</span></span>](index.md)

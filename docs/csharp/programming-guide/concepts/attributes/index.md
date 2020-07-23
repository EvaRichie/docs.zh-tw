---
title: 屬性 (C#)
description: '瞭解如何使用屬性，將中繼資料或宣告式資訊與 c # 中的程式碼產生關聯。 您可以在執行時間使用反映來查詢屬性。'
ms.date: 04/26/2018
ms.openlocfilehash: 5c57838b649531d8e8fe89919771adf8830e7f54
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924981"
---
# <a name="attributes-c"></a><span data-ttu-id="8e9bd-104">屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-104">Attributes (C#)</span></span>

<span data-ttu-id="8e9bd-105">屬性提供一種功能強大的方法，可將中繼資料或宣告資訊關聯至程式碼 (組建、型別、方法、屬性等)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-105">Attributes provide a powerful method of associating metadata, or declarative information, with code (assemblies, types, methods, properties, and so forth).</span></span> <span data-ttu-id="8e9bd-106">將屬性關聯至程式實體之後，就能在執行階段使用稱為「反映」\*\* 的技術來查詢該屬性。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-106">After an attribute is associated with a program entity, the attribute can be queried at run time by using a technique called *reflection*.</span></span> <span data-ttu-id="8e9bd-107">如需詳細資訊，請參閱[反映 (C#)](../reflection.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-107">For more information, see [Reflection (C#)](../reflection.md).</span></span>

<span data-ttu-id="8e9bd-108">屬性 (Attribute) 包含下列屬性 (Property)：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-108">Attributes have the following properties:</span></span>

- <span data-ttu-id="8e9bd-109">屬性會將中繼資料新增至您的程式。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-109">Attributes add metadata to your program.</span></span> <span data-ttu-id="8e9bd-110">「中繼資料」\*\* 是在程式中定義的型別相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-110">*Metadata* is information about the types defined in a program.</span></span> <span data-ttu-id="8e9bd-111">所有的 .NET 組件都包含一組指定的中繼資料，來描述組件中所定義的型別和型別成員。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-111">All .NET assemblies contain a specified set of metadata that describes the types and type members defined in the assembly.</span></span> <span data-ttu-id="8e9bd-112">您可以新增自訂屬性來指定所需的任何其他資訊。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-112">You can add custom attributes to specify any additional information that is required.</span></span> <span data-ttu-id="8e9bd-113">如需詳細資訊，請參閱[建立自訂屬性 (C#)](creating-custom-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-113">For more information, see, [Creating Custom Attributes (C#)](creating-custom-attributes.md).</span></span>
- <span data-ttu-id="8e9bd-114">您可以將一或多個屬性 (Attribute) 套用至整個組件、模組或較小的程式元素，例如類別和屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-114">You can apply one or more attributes to entire assemblies, modules, or smaller program elements such as classes and properties.</span></span>
- <span data-ttu-id="8e9bd-115">屬性 (Attribute) 可以利用與方法與屬性 (Property) 相同的方式來接受引數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-115">Attributes can accept arguments in the same way as methods and properties.</span></span>
- <span data-ttu-id="8e9bd-116">您的程式可以使用反映，來檢查自己的中繼資料或其他程式的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-116">Your program can examine its own metadata or the metadata in other programs by using reflection.</span></span> <span data-ttu-id="8e9bd-117">如需詳細資訊，請參閱[使用反映存取屬性 (C#)](accessing-attributes-by-using-reflection.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-117">For more information, see [Accessing Attributes by Using Reflection (C#)](accessing-attributes-by-using-reflection.md).</span></span>

## <a name="using-attributes"></a><span data-ttu-id="8e9bd-118">使用屬性</span><span class="sxs-lookup"><span data-stu-id="8e9bd-118">Using attributes</span></span>

<span data-ttu-id="8e9bd-119">屬性可以放置於大多數的任意宣告中，但特定的屬性可能會限制它適用的宣告型別。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-119">Attributes can be placed on most any declaration, though a specific attribute might restrict the types of declarations on which it is valid.</span></span> <span data-ttu-id="8e9bd-120">在 C# 中，指定屬性的方式是以方括弧 ([]) 括住屬性的名稱，並放置在要套用的實體宣告上方。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-120">In C#, you specify an attribute by placing the name of the attribute enclosed in square brackets ([]) above the declaration of the entity to which it applies.</span></span>

<span data-ttu-id="8e9bd-121">在此範例中，會使用 <xref:System.SerializableAttribute> 屬性來將特定的特性套用至類別：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-121">In this example, the <xref:System.SerializableAttribute> attribute is used to apply a specific characteristic to a class:</span></span>

[!code-csharp[Using the serializable attribute](~/samples/snippets/csharp/attributes/AttributesOverview.cs#1)]

<span data-ttu-id="8e9bd-122">具有 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性的方法會如下範例宣告：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-122">A method with the attribute <xref:System.Runtime.InteropServices.DllImportAttribute> is declared like the following example:</span></span>

[!code-csharp[Declaring a method to import from an external library](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#2)]

<span data-ttu-id="8e9bd-123">多個屬性可以放在宣告，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-123">More than one attribute can be placed on a declaration as the following example shows:</span></span>

[!code-csharp[Including the interop namespace](~/samples/snippets/csharp/attributes/AttributesOverview.cs#3)]
[!code-csharp[Declaring two way marshaling for arguments](~/samples/snippets/csharp/attributes/AttributesOverview.cs#4)]

<span data-ttu-id="8e9bd-124">可以針對特定實體多次指定某些屬性。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-124">Some attributes can be specified more than once for a given entity.</span></span> <span data-ttu-id="8e9bd-125"><xref:System.Diagnostics.ConditionalAttribute> 就是這種多次使用屬性的一個例子：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-125">An example of such a multiuse attribute is <xref:System.Diagnostics.ConditionalAttribute>:</span></span>

[!code-csharp[Using the conditional attribute](~/samples/snippets/csharp/attributes/AttributesOverview.cs#5)]

> [!NOTE]
> <span data-ttu-id="8e9bd-126">依照慣例，所有的屬性名稱都會以 "Attribute" 這個字結尾，以便與 .NET 程式庫中的其他項目有所區別。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-126">By convention, all attribute names end with the word "Attribute" to distinguish them from other items in the .NET libraries.</span></span> <span data-ttu-id="8e9bd-127">不過，您在程式碼中使用屬性時，不需要指定屬性的後置詞。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-127">However, you do not need to specify the attribute suffix when using attributes in code.</span></span> <span data-ttu-id="8e9bd-128">例如， `[DllImport]` 相當於 `[DllImportAttribute]` ，但 `DllImportAttribute` 是屬性在 .net 類別庫中的實際名稱。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-128">For example, `[DllImport]` is equivalent to `[DllImportAttribute]`, but `DllImportAttribute` is the attribute's actual name in the .NET Class Library.</span></span>

### <a name="attribute-parameters"></a><span data-ttu-id="8e9bd-129">屬性參數</span><span class="sxs-lookup"><span data-stu-id="8e9bd-129">Attribute parameters</span></span>

<span data-ttu-id="8e9bd-130">許多屬性的參數可以是位置、未命名或具名的參數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-130">Many attributes have parameters, which can be positional, unnamed, or named.</span></span> <span data-ttu-id="8e9bd-131">任何位置的參數必須以特定順序指定，而且不能省略。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-131">Any positional parameters must be specified in a certain order and cannot be omitted.</span></span> <span data-ttu-id="8e9bd-132">具名的參數是選擇性的，可以依照任何順序指定。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-132">Named parameters are optional and can be specified in any order.</span></span> <span data-ttu-id="8e9bd-133">位置參數會先指定。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-133">Positional parameters are specified first.</span></span> <span data-ttu-id="8e9bd-134">例如，這三個屬性是相等的：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-134">For example, these three attributes are equivalent:</span></span>

```csharp
[DllImport("user32.dll")]
[DllImport("user32.dll", SetLastError=false, ExactSpelling=false)]
[DllImport("user32.dll", ExactSpelling=false, SetLastError=false)]
```

<span data-ttu-id="8e9bd-135">第一個參數 (DLL 名稱) 是位置參數，一律會先出現；其他的則為具名參數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-135">The first parameter, the DLL name, is positional and always comes first; the others are named.</span></span> <span data-ttu-id="8e9bd-136">在此案例中，這兩個具名參數預設為 false，因此可以省略。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-136">In this case, both named parameters default to false, so they can be omitted.</span></span> <span data-ttu-id="8e9bd-137">位置參數對應至屬性建構函式的參數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-137">Positional parameters correspond to the parameters of the attribute constructor.</span></span> <span data-ttu-id="8e9bd-138">對應屬性或欄位屬性的具名或選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-138">Named or optional parameters correspond to either properties or fields of the attribute.</span></span> <span data-ttu-id="8e9bd-139">請參閱個別屬性的文件，以取得預設參數值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-139">Refer to the individual attribute's documentation for information on default parameter values.</span></span>

### <a name="attribute-targets"></a><span data-ttu-id="8e9bd-140">屬性目標</span><span class="sxs-lookup"><span data-stu-id="8e9bd-140">Attribute targets</span></span>

<span data-ttu-id="8e9bd-141">屬性的「目標」\*\* 是要套用屬性的實體。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-141">The *target* of an attribute is the entity which the attribute applies to.</span></span> <span data-ttu-id="8e9bd-142">例如，屬性可套用至類別、特定的方法或整個組件。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-142">For example, an attribute may apply to a class, a particular method, or an entire assembly.</span></span> <span data-ttu-id="8e9bd-143">根據預設，屬性會套用至其後的元素。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-143">By default, an attribute applies to the element that follows it.</span></span> <span data-ttu-id="8e9bd-144">但是，舉例來說，您也可以明確地識別是否要將屬性套用到方法、它的參數或它的傳回值。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-144">But you can also explicitly identify, for example, whether an attribute is applied to a method, or to its parameter, or to its return value.</span></span>

<span data-ttu-id="8e9bd-145">若要明確地識別屬性目標，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-145">To explicitly identify an attribute target, use the following syntax:</span></span>

```csharp
[target : attribute-list]
```

<span data-ttu-id="8e9bd-146">下表顯示可能的 `target` 值清單。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-146">The list of possible `target` values is shown in the following table.</span></span>

|<span data-ttu-id="8e9bd-147">目標值</span><span class="sxs-lookup"><span data-stu-id="8e9bd-147">Target value</span></span>|<span data-ttu-id="8e9bd-148">適用於</span><span class="sxs-lookup"><span data-stu-id="8e9bd-148">Applies to</span></span>|
|------------------|----------------|
|`assembly`|<span data-ttu-id="8e9bd-149">整個組件</span><span class="sxs-lookup"><span data-stu-id="8e9bd-149">Entire assembly</span></span>|
|`module`|<span data-ttu-id="8e9bd-150">目前的組件模組</span><span class="sxs-lookup"><span data-stu-id="8e9bd-150">Current assembly module</span></span>|
|`field`|<span data-ttu-id="8e9bd-151">類別或結構中的欄位</span><span class="sxs-lookup"><span data-stu-id="8e9bd-151">Field in a class or a struct</span></span>|
|`event`|<span data-ttu-id="8e9bd-152">事件</span><span class="sxs-lookup"><span data-stu-id="8e9bd-152">Event</span></span>|
|`method`|<span data-ttu-id="8e9bd-153">方法或 `get` 和 `set` 屬性存取子</span><span class="sxs-lookup"><span data-stu-id="8e9bd-153">Method or `get` and `set` property accessors</span></span>|
|`param`|<span data-ttu-id="8e9bd-154">方法參數或 `set` 屬性存取子參數</span><span class="sxs-lookup"><span data-stu-id="8e9bd-154">Method parameters or `set` property accessor parameters</span></span>|
|`property`|<span data-ttu-id="8e9bd-155">屬性</span><span class="sxs-lookup"><span data-stu-id="8e9bd-155">Property</span></span>|
|`return`|<span data-ttu-id="8e9bd-156">方法的傳回值、屬性索引子或 `get` 屬性存取子</span><span class="sxs-lookup"><span data-stu-id="8e9bd-156">Return value of a method, property indexer, or `get` property accessor</span></span>|
|`type`|<span data-ttu-id="8e9bd-157">結構、類別、介面、列舉或委派</span><span class="sxs-lookup"><span data-stu-id="8e9bd-157">Struct, class, interface, enum, or delegate</span></span>|

<span data-ttu-id="8e9bd-158">您可以指定`field`屬性套用至支援欄位的目標值建立[自動實作屬性](../../../properties.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-158">You would specify the `field` target value to apply an attribute to the backing field created for an [auto-implemented property](../../../properties.md).</span></span>

<span data-ttu-id="8e9bd-159">下列範例示範如何將屬性套用到組件和模組。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-159">The following example shows how to apply attributes to assemblies and modules.</span></span> <span data-ttu-id="8e9bd-160">如需詳細資訊，請參閱[常見屬性 (C#)](../../../language-reference/attributes/global.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-160">For more information, see [Common Attributes (C#)](../../../language-reference/attributes/global.md).</span></span>

```csharp
using System;
using System.Reflection;
[assembly: AssemblyTitleAttribute("Production assembly 4")]
[module: CLSCompliant(true)]
```

<span data-ttu-id="8e9bd-161">下列範例示範如何在 C# 中將屬性套用至方法、方法參數和方法傳回值。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-161">The following example shows how to apply attributes to methods, method parameters, and method return values in C#.</span></span>

[!code-csharp[Applying attributes to different code elements](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#6)]

> [!NOTE]
> <span data-ttu-id="8e9bd-162">不論 `ValidatedContract` 定義為有效的目標為何，都必須指定 `return` 目標，即使 `ValidatedContract` 已定義為只套用至傳回值也一樣。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-162">Regardless of the targets on which `ValidatedContract` is defined to be valid, the `return` target has to be specified, even if `ValidatedContract` were defined to apply only to return values.</span></span> <span data-ttu-id="8e9bd-163">換句話說，編譯器不會使用 `AttributeUsage` 資訊來解析模稜兩可的屬性目標。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-163">In other words, the compiler will not use `AttributeUsage` information to resolve ambiguous attribute targets.</span></span> <span data-ttu-id="8e9bd-164">如需詳細資訊，請參閱 [AttributeUsage (C#)](../../../language-reference/attributes/general.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-164">For more information, see [AttributeUsage (C#)](../../../language-reference/attributes/general.md).</span></span>

## <a name="common-uses-for-attributes"></a><span data-ttu-id="8e9bd-165">屬性的常見用法</span><span class="sxs-lookup"><span data-stu-id="8e9bd-165">Common uses for attributes</span></span>

<span data-ttu-id="8e9bd-166">下列清單包含一些程式碼中常見的屬性用法：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-166">The following list includes a few of the common uses of attributes in code:</span></span>

- <span data-ttu-id="8e9bd-167">在 Web 服務中使用 `WebMethod` 屬性標示方法，以表示此方法應該可以透過 SOAP 通訊協定來呼叫。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-167">Marking methods using the `WebMethod` attribute in Web services to indicate that the method should be callable over the SOAP protocol.</span></span> <span data-ttu-id="8e9bd-168">如需詳細資訊，請參閱 <xref:System.Web.Services.WebMethodAttribute> 。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-168">For more information, see <xref:System.Web.Services.WebMethodAttribute>.</span></span>
- <span data-ttu-id="8e9bd-169">描述在與原生程式碼交互作用時，如何封送處理方法參數。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-169">Describing how to marshal method parameters when interoperating with native code.</span></span> <span data-ttu-id="8e9bd-170">如需詳細資訊，請參閱 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-170">For more information, see <xref:System.Runtime.InteropServices.MarshalAsAttribute>.</span></span>
- <span data-ttu-id="8e9bd-171">描述適用於類別、方法和介面的 COM 屬性。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-171">Describing the COM properties for classes, methods, and interfaces.</span></span>
- <span data-ttu-id="8e9bd-172">使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 類別呼叫 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-172">Calling unmanaged code using the <xref:System.Runtime.InteropServices.DllImportAttribute> class.</span></span>
- <span data-ttu-id="8e9bd-173">針對標題、版本、描述或商標等方面來描述您的組件。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-173">Describing your assembly in terms of title, version, description, or trademark.</span></span>
- <span data-ttu-id="8e9bd-174">描述要將類別的哪些成員序列化以取得持續性。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-174">Describing which members of a class to serialize for persistence.</span></span>
- <span data-ttu-id="8e9bd-175">描述如何基於 XML 序列化目的，在類別成員與 XML 節點之間進行對應。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-175">Describing how to map between class members and XML nodes for XML serialization.</span></span>
- <span data-ttu-id="8e9bd-176">描述方法的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-176">Describing the security requirements for methods.</span></span>
- <span data-ttu-id="8e9bd-177">指定用來強制執行安全性的特性。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-177">Specifying characteristics used to enforce security.</span></span>
- <span data-ttu-id="8e9bd-178">控制由 Just-In-Time (JIT) 編譯器所進行的最佳化，讓程式碼保持易於偵錯。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-178">Controlling optimizations by the just-in-time (JIT) compiler so the code remains easy to debug.</span></span>
- <span data-ttu-id="8e9bd-179">取得有關方法之呼叫端的資訊。</span><span class="sxs-lookup"><span data-stu-id="8e9bd-179">Obtaining information about the caller to a method.</span></span>

## <a name="related-sections"></a><span data-ttu-id="8e9bd-180">相關章節</span><span class="sxs-lookup"><span data-stu-id="8e9bd-180">Related sections</span></span>

<span data-ttu-id="8e9bd-181">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8e9bd-181">For more information, see:</span></span>

- [<span data-ttu-id="8e9bd-182">建立自訂屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-182">Creating Custom Attributes (C#)</span></span>](creating-custom-attributes.md)  
- [<span data-ttu-id="8e9bd-183">使用反映存取屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-183">Accessing Attributes by Using Reflection (C#)</span></span>](accessing-attributes-by-using-reflection.md)  
- [<span data-ttu-id="8e9bd-184">如何使用屬性建立 C/c + + 等位（c #）</span><span class="sxs-lookup"><span data-stu-id="8e9bd-184">How to create a C/C++ union by using attributes (C#)</span></span>](how-to-create-a-c-cpp-union-by-using-attributes.md)  
- [<span data-ttu-id="8e9bd-185">常見屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-185">Common Attributes (C#)</span></span>](../../../language-reference/attributes/global.md)  
- [<span data-ttu-id="8e9bd-186">呼叫端資訊 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-186">Caller Information (C#)</span></span>](../../../language-reference/attributes/caller-information.md)  

## <a name="see-also"></a><span data-ttu-id="8e9bd-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8e9bd-187">See also</span></span>

- [<span data-ttu-id="8e9bd-188">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="8e9bd-188">C# Programming Guide</span></span>](../../index.md)
- [<span data-ttu-id="8e9bd-189">反映 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e9bd-189">Reflection (C#)</span></span>](../reflection.md)
- [<span data-ttu-id="8e9bd-190">屬性</span><span class="sxs-lookup"><span data-stu-id="8e9bd-190">Attributes</span></span>](../../../../standard/attributes/index.md)
- [<span data-ttu-id="8e9bd-191">在 C 中使用屬性#</span><span class="sxs-lookup"><span data-stu-id="8e9bd-191">Using Attributes in C#</span></span>](../../../tutorials/attributes.md)

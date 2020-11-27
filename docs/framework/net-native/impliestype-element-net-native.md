---
title: '<ImpliesType> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: 3abd2071-0f28-40ba-b9a0-d52bd94cd2f6
ms.openlocfilehash: 04c3a9498a5c9c24d67dedd02fb4c9d68d9efbdd
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287952"
---
# <a name="impliestype-element-net-native"></a><span data-ttu-id="b3188-102">\<ImpliesType> 元素 ( .NET Native) </span><span class="sxs-lookup"><span data-stu-id="b3188-102">\<ImpliesType> Element (.NET Native)</span></span>

<span data-ttu-id="b3188-103">如果原則已套用至包含類型或方法，則會將該原則套用至類型。</span><span class="sxs-lookup"><span data-stu-id="b3188-103">Applies policy to a type, if that policy has been applied to the containing type or method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b3188-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="b3188-104">Syntax</span></span>  
  
```xml
<ImpliesType Name="type_name"  
             Activate="policy_type"  
             Browse="policy_type"  
             Dynamic="policy_type"  
             Serialize="policy_type"
             DataContractSerializer="policy_setting"  
             DataContractJsonSerializer="policy_setting"  
             XmlSerializer="policy_setting"  
             MarshalObject="policy_setting"  
             MarshalDelegate="policy_setting"  
             MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="b3188-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="b3188-105">Attributes and Elements</span></span>  

 <span data-ttu-id="b3188-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="b3188-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="b3188-107">屬性</span><span class="sxs-lookup"><span data-stu-id="b3188-107">Attributes</span></span>  
  
|<span data-ttu-id="b3188-108">屬性</span><span class="sxs-lookup"><span data-stu-id="b3188-108">Attribute</span></span>|<span data-ttu-id="b3188-109">屬性類型</span><span class="sxs-lookup"><span data-stu-id="b3188-109">Attribute type</span></span>|<span data-ttu-id="b3188-110">描述</span><span class="sxs-lookup"><span data-stu-id="b3188-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Name`|<span data-ttu-id="b3188-111">一般</span><span class="sxs-lookup"><span data-stu-id="b3188-111">General</span></span>|<span data-ttu-id="b3188-112">必要屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-112">Required attribute.</span></span> <span data-ttu-id="b3188-113">指定類型名稱。</span><span class="sxs-lookup"><span data-stu-id="b3188-113">Specifies the type name.</span></span>|  
|`Activate`|<span data-ttu-id="b3188-114">反射</span><span class="sxs-lookup"><span data-stu-id="b3188-114">Reflection</span></span>|<span data-ttu-id="b3188-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-115">Optional attribute.</span></span> <span data-ttu-id="b3188-116">控制建構函式的執行階段存取，以便啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="b3188-116">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="b3188-117">反射</span><span class="sxs-lookup"><span data-stu-id="b3188-117">Reflection</span></span>|<span data-ttu-id="b3188-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-118">Optional attribute.</span></span> <span data-ttu-id="b3188-119">控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。</span><span class="sxs-lookup"><span data-stu-id="b3188-119">Controls querying for information about program elements, but does not enable any runtime access.</span></span>|  
|`Dynamic`|<span data-ttu-id="b3188-120">反射</span><span class="sxs-lookup"><span data-stu-id="b3188-120">Reflection</span></span>|<span data-ttu-id="b3188-121">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-121">Optional attribute.</span></span> <span data-ttu-id="b3188-122">控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="b3188-122">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="b3188-123">序列化</span><span class="sxs-lookup"><span data-stu-id="b3188-123">Serialization</span></span>|<span data-ttu-id="b3188-124">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-124">Optional attribute.</span></span> <span data-ttu-id="b3188-125">控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="b3188-125">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="b3188-126">序列化</span><span class="sxs-lookup"><span data-stu-id="b3188-126">Serialization</span></span>|<span data-ttu-id="b3188-127">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-127">Optional attribute.</span></span> <span data-ttu-id="b3188-128">控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-128">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="b3188-129">序列化</span><span class="sxs-lookup"><span data-stu-id="b3188-129">Serialization</span></span>|<span data-ttu-id="b3188-130">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-130">Optional attribute.</span></span> <span data-ttu-id="b3188-131">控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-131">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="b3188-132">序列化</span><span class="sxs-lookup"><span data-stu-id="b3188-132">Serialization</span></span>|<span data-ttu-id="b3188-133">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-133">Optional attribute.</span></span> <span data-ttu-id="b3188-134">控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-134">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="b3188-135">Interop</span><span class="sxs-lookup"><span data-stu-id="b3188-135">Interop</span></span>|<span data-ttu-id="b3188-136">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-136">Optional attribute.</span></span> <span data-ttu-id="b3188-137">控制 Windows 執行階段和 COM 之參考類型的封送處理原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-137">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="b3188-138">Interop</span><span class="sxs-lookup"><span data-stu-id="b3188-138">Interop</span></span>|<span data-ttu-id="b3188-139">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-139">Optional attribute.</span></span> <span data-ttu-id="b3188-140">控制將委派類型當作函式指標封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-140">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="b3188-141">Interop</span><span class="sxs-lookup"><span data-stu-id="b3188-141">Interop</span></span>|<span data-ttu-id="b3188-142">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="b3188-142">Optional attribute.</span></span> <span data-ttu-id="b3188-143">控制將值類型封送處理為原生程式碼的原則。</span><span class="sxs-lookup"><span data-stu-id="b3188-143">Controls policy for marshaling value types to native code.</span></span>|  
  
## <a name="name-attribute"></a><span data-ttu-id="b3188-144">Name 屬性</span><span class="sxs-lookup"><span data-stu-id="b3188-144">Name attribute</span></span>  
  
|<span data-ttu-id="b3188-145">值</span><span class="sxs-lookup"><span data-stu-id="b3188-145">Value</span></span>|<span data-ttu-id="b3188-146">描述</span><span class="sxs-lookup"><span data-stu-id="b3188-146">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="b3188-147">*type_name*</span><span class="sxs-lookup"><span data-stu-id="b3188-147">*type_name*</span></span>|<span data-ttu-id="b3188-148">類型名稱。</span><span class="sxs-lookup"><span data-stu-id="b3188-148">The type name.</span></span> <span data-ttu-id="b3188-149">如果這個 `<ImpliesType>` 項目所表示的類型位在與其包含 `<Type>` 項目相同的命名空間中，則 *type_name* 可以包含該類型的名稱，而不包含其命名空間。</span><span class="sxs-lookup"><span data-stu-id="b3188-149">If the type represented by this `<ImpliesType>` element is located in the same namespace as its containing `<Type>` element, *type_name* can include the name of the type without its namespace.</span></span> <span data-ttu-id="b3188-150">否則，*type_name* 必須包含完整的類型名稱。</span><span class="sxs-lookup"><span data-stu-id="b3188-150">Otherwise, *type_name* must include the fully qualified type name.</span></span>|  
  
## <a name="all-other-attributes"></a><span data-ttu-id="b3188-151">所有其他屬性</span><span class="sxs-lookup"><span data-stu-id="b3188-151">All other attributes</span></span>  
  
|<span data-ttu-id="b3188-152">值</span><span class="sxs-lookup"><span data-stu-id="b3188-152">Value</span></span>|<span data-ttu-id="b3188-153">描述</span><span class="sxs-lookup"><span data-stu-id="b3188-153">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="b3188-154">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="b3188-154">*policy_setting*</span></span>|<span data-ttu-id="b3188-155">要套用到此原則類型的設定。</span><span class="sxs-lookup"><span data-stu-id="b3188-155">The setting to apply to this policy type.</span></span> <span data-ttu-id="b3188-156">可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。</span><span class="sxs-lookup"><span data-stu-id="b3188-156">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="b3188-157">如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="b3188-157">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="b3188-158">子元素</span><span class="sxs-lookup"><span data-stu-id="b3188-158">Child Elements</span></span>  

 <span data-ttu-id="b3188-159">無。</span><span class="sxs-lookup"><span data-stu-id="b3188-159">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="b3188-160">父項目</span><span class="sxs-lookup"><span data-stu-id="b3188-160">Parent Elements</span></span>  
  
|<span data-ttu-id="b3188-161">元素</span><span class="sxs-lookup"><span data-stu-id="b3188-161">Element</span></span>|<span data-ttu-id="b3188-162">描述</span><span class="sxs-lookup"><span data-stu-id="b3188-162">Description</span></span>|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="b3188-163">將反映原則套用至類型及其所有成員。</span><span class="sxs-lookup"><span data-stu-id="b3188-163">Applies reflection policy to a type and all its members.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="b3188-164">將反映原則套用至建構泛型類型及其所有成員。</span><span class="sxs-lookup"><span data-stu-id="b3188-164">Applies reflection policy to a constructed generic type and all its members.</span></span>|  
|[\<Method>](method-element-net-native.md)|<span data-ttu-id="b3188-165">將反映原則套用至方法。</span><span class="sxs-lookup"><span data-stu-id="b3188-165">Applies reflection policy to a method.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b3188-166">備註</span><span class="sxs-lookup"><span data-stu-id="b3188-166">Remarks</span></span>  

 <span data-ttu-id="b3188-167">`<ImpliesType>` 元素的主要目的是要供程式庫使用。</span><span class="sxs-lookup"><span data-stu-id="b3188-167">The `<ImpliesType>` element is primarily intended for use by libraries.</span></span> <span data-ttu-id="b3188-168">它可以解決下列情況：</span><span class="sxs-lookup"><span data-stu-id="b3188-168">It addresses the following scenario:</span></span>  
  
- <span data-ttu-id="b3188-169">如果常式需要反映在一個類型上，則一定需要反映在第二個類型上。</span><span class="sxs-lookup"><span data-stu-id="b3188-169">If a routine needs to reflect on one type, it necessarily needs to reflect on a second type.</span></span>  
  
- <span data-ttu-id="b3188-170">否則，無法將中繼資料用於第二個類型的隱含具現化，因為靜態分析並未指出中繼資料是必要的。</span><span class="sxs-lookup"><span data-stu-id="b3188-170">The metadata for the implied instantiation of the second type is otherwise unavailable, because static analysis doesn't indicate that it's necessary.</span></span>  
  
 <span data-ttu-id="b3188-171">大多數情況下，這兩個類型是含有共用型別引數的泛型具現化。</span><span class="sxs-lookup"><span data-stu-id="b3188-171">Most commonly, the two types are generic instantiations with shared type arguments.</span></span>  
  
 <span data-ttu-id="b3188-172">`<ImpliesType>` 元素的定義是假設如果需要反映在其父元素指定的類型上，則表示需要反映在 `<ImpliesType>` 元素所指定的類型上。</span><span class="sxs-lookup"><span data-stu-id="b3188-172">The `<ImpliesType>` element was defined with the assumption that a need for reflection on the type specified by its parent element implies a need for reflection on the type specified by the `<ImpliesType>` element.</span></span> <span data-ttu-id="b3188-173">例如，下列反映指示詞套用至 `Explicit<T>` 和 `Implicit<T>` 這兩種類型。</span><span class="sxs-lookup"><span data-stu-id="b3188-173">For example, the following reflection directives apply to two types, `Explicit<T>` and `Implicit<T>`.</span></span>  
  
```xml  
<Type Name="Explicit{ET}">  
    <ImpliesType Name="Implicit{ET}" Dynamic="Required Public" />  
</Type>  
```  
  
 <span data-ttu-id="b3188-174">除非 `Explicit` 的具現化具有已定義的 `Dynamic` 原則設定，否則這個指示詞沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="b3188-174">This directive has no effect unless an instantiation of `Explicit` has a defined `Dynamic` policy setting.</span></span> <span data-ttu-id="b3188-175">例如，如果 `Explicit<Int32>` 是這種情形，則會以其公用成員為基礎來將 `Implicit<Int32>` 具現化，並使其中繼資料可供存取來進行動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="b3188-175">For example, if that's the case for `Explicit<Int32>`, `Implicit<Int32>` is instantiated with its public members rooted, and their metadata is made accessible for dynamic programming.</span></span>  
  
 <span data-ttu-id="b3188-176">下列是套用到至少一個序列化程式的真實世界範例。</span><span class="sxs-lookup"><span data-stu-id="b3188-176">The following is a real-world example that applies to at least one serializer.</span></span> <span data-ttu-id="b3188-177">指示詞會捕捉在輸入的內容上反映的需求，其中 `IList<` *something* `>` 也牽涉到對應的 `List<` *某個* `>` 類型，而不需要任何每個應用程式的注釋。</span><span class="sxs-lookup"><span data-stu-id="b3188-177">The directives capture the requirement that reflecting on something typed as `IList<`*something*`>` also involves reflecting on the corresponding `List<`*something*`>` type without requiring any per-application annotation.</span></span>  
  
```xml  
<Type Name="System.Collections.Generic.IList{T}">  
   <ImpliesType Name="System.Collections.Generic.List{T}" Serialize="Public" />  
</Type>  
```  
  
 <span data-ttu-id="b3188-178">`<ImpliesType>` 元素也會出現在 `<Method>` 元素中，因為在某些情況下，具現化泛型方法表示要反映在類型具現化上。</span><span class="sxs-lookup"><span data-stu-id="b3188-178">The `<ImpliesType>` element can also appear within a `<Method>` element, because in some cases instantiating a generic method implies reflecting on a type instantiation.</span></span> <span data-ttu-id="b3188-179">例如，想像一個給定程式庫將會隨著相關聯的  和  類型動態存取的泛型方法 `IEnumerable<T> MakeEnumerable<T>(string spelling, T defaultValue)`<xref:System.Collections.Generic.List%601><xref:System.Array>。</span><span class="sxs-lookup"><span data-stu-id="b3188-179">For example, imagine a generic method `IEnumerable<T> MakeEnumerable<T>(string spelling, T defaultValue)` that a given library will access dynamically along with the associated <xref:System.Collections.Generic.List%601> and <xref:System.Array> types.</span></span> <span data-ttu-id="b3188-180">這可以表示成：</span><span class="sxs-lookup"><span data-stu-id="b3188-180">This can be expressed as:</span></span>  
  
```xml  
<Type Name="MyType">  
    <Method Name="MakeEnumerable{T}" Signature="(System.String, T)" Dynamic="Included">  
        <ImpliesType Name="T[]" Dynamic="Public" />  
        <ImpliesType Name="System.Collections.Generic.List{T}" Dynamic="Public" />  
    </Method>  
</Type>  
```  
  
## <a name="see-also"></a><span data-ttu-id="b3188-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b3188-181">See also</span></span>

- [<span data-ttu-id="b3188-182">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="b3188-182">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="b3188-183">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="b3188-183">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="b3188-184">執行階段指示詞原則設定</span><span class="sxs-lookup"><span data-stu-id="b3188-184">Runtime Directive Policy Settings</span></span>](runtime-directive-policy-settings.md)

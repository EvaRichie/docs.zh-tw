---
title: '<Subtypes> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: fb854070-248b-46cf-9dab-c322e2b4d624
ms.openlocfilehash: 7484152c351f59ee84b601584bd84347186628a3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287809"
---
# <a name="subtypes-element-net-native"></a><span data-ttu-id="0a366-102">\<Subtypes> 元素 ( .NET Native) </span><span class="sxs-lookup"><span data-stu-id="0a366-102">\<Subtypes> Element (.NET Native)</span></span>

<span data-ttu-id="0a366-103">將執行階段原則套用至從包含類型繼承的所有類別。</span><span class="sxs-lookup"><span data-stu-id="0a366-103">Applies runtime policy to all classes inherited from the containing type.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0a366-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="0a366-104">Syntax</span></span>  
  
```xml  
<Subtypes Activate="policy_type"  
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
  
## <a name="attributes-and-elements"></a><span data-ttu-id="0a366-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="0a366-105">Attributes and Elements</span></span>  

 <span data-ttu-id="0a366-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="0a366-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="0a366-107">屬性</span><span class="sxs-lookup"><span data-stu-id="0a366-107">Attributes</span></span>  
  
|<span data-ttu-id="0a366-108">屬性</span><span class="sxs-lookup"><span data-stu-id="0a366-108">Attribute</span></span>|<span data-ttu-id="0a366-109">屬性類型</span><span class="sxs-lookup"><span data-stu-id="0a366-109">Attribute type</span></span>|<span data-ttu-id="0a366-110">描述</span><span class="sxs-lookup"><span data-stu-id="0a366-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Activate`|<span data-ttu-id="0a366-111">反射</span><span class="sxs-lookup"><span data-stu-id="0a366-111">Reflection</span></span>|<span data-ttu-id="0a366-112">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-112">Optional attribute.</span></span> <span data-ttu-id="0a366-113">控制建構函式的執行階段存取，以便啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="0a366-113">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="0a366-114">反射</span><span class="sxs-lookup"><span data-stu-id="0a366-114">Reflection</span></span>|<span data-ttu-id="0a366-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-115">Optional attribute.</span></span> <span data-ttu-id="0a366-116">控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。</span><span class="sxs-lookup"><span data-stu-id="0a366-116">Controls querying for information about program elements, but does not enable any runtime access.</span></span>|  
|`Dynamic`|<span data-ttu-id="0a366-117">反射</span><span class="sxs-lookup"><span data-stu-id="0a366-117">Reflection</span></span>|<span data-ttu-id="0a366-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-118">Optional attribute.</span></span> <span data-ttu-id="0a366-119">控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="0a366-119">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="0a366-120">序列化</span><span class="sxs-lookup"><span data-stu-id="0a366-120">Serialization</span></span>|<span data-ttu-id="0a366-121">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-121">Optional attribute.</span></span> <span data-ttu-id="0a366-122">控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="0a366-122">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="0a366-123">序列化</span><span class="sxs-lookup"><span data-stu-id="0a366-123">Serialization</span></span>|<span data-ttu-id="0a366-124">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-124">Optional attribute.</span></span> <span data-ttu-id="0a366-125">控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-125">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="0a366-126">序列化</span><span class="sxs-lookup"><span data-stu-id="0a366-126">Serialization</span></span>|<span data-ttu-id="0a366-127">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-127">Optional attribute.</span></span> <span data-ttu-id="0a366-128">控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-128">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="0a366-129">序列化</span><span class="sxs-lookup"><span data-stu-id="0a366-129">Serialization</span></span>|<span data-ttu-id="0a366-130">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-130">Optional attribute.</span></span> <span data-ttu-id="0a366-131">控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-131">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="0a366-132">Interop</span><span class="sxs-lookup"><span data-stu-id="0a366-132">Interop</span></span>|<span data-ttu-id="0a366-133">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-133">Optional attribute.</span></span> <span data-ttu-id="0a366-134">控制 Windows 執行階段和 COM 之參考類型的封送處理原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-134">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="0a366-135">Interop</span><span class="sxs-lookup"><span data-stu-id="0a366-135">Interop</span></span>|<span data-ttu-id="0a366-136">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-136">Optional attribute.</span></span> <span data-ttu-id="0a366-137">控制將委派類型當作函式指標封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-137">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="0a366-138">Interop</span><span class="sxs-lookup"><span data-stu-id="0a366-138">Interop</span></span>|<span data-ttu-id="0a366-139">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="0a366-139">Optional attribute.</span></span> <span data-ttu-id="0a366-140">控制將值類型封送處理為原生程式碼的原則。</span><span class="sxs-lookup"><span data-stu-id="0a366-140">Controls policy for marshaling value types to native code.</span></span>|  
  
## <a name="all-attributes"></a><span data-ttu-id="0a366-141">所有屬性</span><span class="sxs-lookup"><span data-stu-id="0a366-141">All attributes</span></span>  
  
|<span data-ttu-id="0a366-142">值</span><span class="sxs-lookup"><span data-stu-id="0a366-142">Value</span></span>|<span data-ttu-id="0a366-143">描述</span><span class="sxs-lookup"><span data-stu-id="0a366-143">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="0a366-144">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="0a366-144">*policy_setting*</span></span>|<span data-ttu-id="0a366-145">要套用到此原則類型的設定。</span><span class="sxs-lookup"><span data-stu-id="0a366-145">The setting to apply to this policy type.</span></span> <span data-ttu-id="0a366-146">可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。</span><span class="sxs-lookup"><span data-stu-id="0a366-146">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="0a366-147">如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="0a366-147">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="0a366-148">子元素</span><span class="sxs-lookup"><span data-stu-id="0a366-148">Child Elements</span></span>  

 <span data-ttu-id="0a366-149">無。</span><span class="sxs-lookup"><span data-stu-id="0a366-149">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="0a366-150">父項目</span><span class="sxs-lookup"><span data-stu-id="0a366-150">Parent Elements</span></span>  
  
|<span data-ttu-id="0a366-151">元素</span><span class="sxs-lookup"><span data-stu-id="0a366-151">Element</span></span>|<span data-ttu-id="0a366-152">描述</span><span class="sxs-lookup"><span data-stu-id="0a366-152">Description</span></span>|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="0a366-153">將反映原則套用至類型及其所有成員。</span><span class="sxs-lookup"><span data-stu-id="0a366-153">Applies reflection policy to a type and all its members.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="0a366-154">備註</span><span class="sxs-lookup"><span data-stu-id="0a366-154">Remarks</span></span>  

 <span data-ttu-id="0a366-155">`<Subtypes>` 元素將原則套用至其包含類型的所有子類型。</span><span class="sxs-lookup"><span data-stu-id="0a366-155">The `<Subtypes>` element applies policy to all the subtypes of its containing type.</span></span> <span data-ttu-id="0a366-156">當您想將不同的原則套用至衍生類型及其基底類別時，可使用這個元素。</span><span class="sxs-lookup"><span data-stu-id="0a366-156">You use it when you want to apply different policies to derived types and their base classes.</span></span>  
  
 <span data-ttu-id="0a366-157">反映、序列化和 interop 屬性都是選用性，但至少要有一個屬性存在。</span><span class="sxs-lookup"><span data-stu-id="0a366-157">The reflection, serialization, and interop attributes are all optional, although at least one should be present.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0a366-158">範例</span><span class="sxs-lookup"><span data-stu-id="0a366-158">Example</span></span>  

 <span data-ttu-id="0a366-159">下列範例定義名為 `BaseClass` 的類別和名為 `Derived1` 的子類別。</span><span class="sxs-lookup"><span data-stu-id="0a366-159">The following example defines a class named `BaseClass` and a subclass named `Derived1`.</span></span>  
  
 [!code-csharp[ProjectN_Reflection#4](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/subtypes.cs#4)]  
  
 <span data-ttu-id="0a366-160">如下列程式碼所示，執行階段指示詞檔案將 `Dynamic` 的 `Activate` 和 `BaseClass` 原則明確設定為 `Excluded`。</span><span class="sxs-lookup"><span data-stu-id="0a366-160">As shown in the following code, the runtime directives file explicitly sets the `Dynamic` and `Activate` policies for `BaseClass` to `Excluded`.</span></span> <span data-ttu-id="0a366-161">因此，您無法以動態方式或透過呼叫 `BaseClass` 類別建構函式，來具現化 `BaseClass` 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="0a366-161">Because of this, objects of type `BaseClass` cannot be instantiated dynamically or by calls to the `BaseClass` class constructor.</span></span> <span data-ttu-id="0a366-162">不過，`<Subtypes>` 元素可以動態方式及透過呼叫其類別建構函式，來具現化衍生自 `BaseClass` 的類別。</span><span class="sxs-lookup"><span data-stu-id="0a366-162">However, the `<Subtypes>` element allows classes derived from `BaseClass` to be instantiated dynamically and through calls to their class constructors.</span></span>  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
   <Assembly Name="*Application*" Dynamic="Required All" />  
     <Type Name="Examples.Libraries.BaseClass" Activate ="Excluded" Dynamic="Excluded" >  
        <Subtypes Activate="Public" Dynamic ="Public"/>  
     </Type>  
  </Application>  
</Directives>  
```  
  
 <span data-ttu-id="0a366-163">由於 `<Subtypes>` 指示詞，呼叫 `Derived1` 方法以動態具現化 <xref:System.Activator.CreateInstance%28System.Type%29?displayProperty=nameWithType> 執行個體的下列程式碼會順利執行。</span><span class="sxs-lookup"><span data-stu-id="0a366-163">Because of the `<Subtypes>` directive, the following code that instantiates a `Derived1` instance dynamically by calling the <xref:System.Activator.CreateInstance%28System.Type%29?displayProperty=nameWithType> method executes successfully.</span></span>  <span data-ttu-id="0a366-164">此處的區塊變數是空白 Windows 市集應用程式中的 <xref:System.Windows.Controls.TextBlock> 物件。</span><span class="sxs-lookup"><span data-stu-id="0a366-164">The block variable here is a <xref:System.Windows.Controls.TextBlock> object in a blank Windows Store app.</span></span>  
  
 [!code-csharp[ProjectN_Reflection#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/subtypes.cs#5)]  
  
## <a name="see-also"></a><span data-ttu-id="0a366-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0a366-165">See also</span></span>

- [<span data-ttu-id="0a366-166">\<Type> 元素</span><span class="sxs-lookup"><span data-stu-id="0a366-166">\<Type> Element</span></span>](type-element-net-native.md)
- [<span data-ttu-id="0a366-167">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="0a366-167">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="0a366-168">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="0a366-168">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="0a366-169">執行階段指示詞原則設定</span><span class="sxs-lookup"><span data-stu-id="0a366-169">Runtime Directive Policy Settings</span></span>](runtime-directive-policy-settings.md)

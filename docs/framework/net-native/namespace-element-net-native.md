---
title: '<Namespace> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: 57c614e5-18a9-4e87-bfd5-d0fe3396a192
ms.openlocfilehash: 05de04685f8ba746f55bf040c74fd3831c5b63ca
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287887"
---
# <a name="namespace-element-net-native"></a><span data-ttu-id="fb1cc-102">\<Namespace> 元素 ( .NET Native) </span><span class="sxs-lookup"><span data-stu-id="fb1cc-102">\<Namespace> Element (.NET Native)</span></span>

<span data-ttu-id="fb1cc-103">將執行階段反映原則套用至指定命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-103">Applies runtime reflection policy to all the types in a specified namespace.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fb1cc-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="fb1cc-104">Syntax</span></span>  
  
```xml  
<Namespace Name="namespace_name"
           Activate="policy_type"
           Browse="policy_type"  
           Dynamic="policy_setting"  
           Serialize="policy_setting"  
           DataContractSerializer="policy_setting"  
           DataContractJsonSerializer="policy_setting"  
           XmlSerializer="policy_setting"  
           MarshalObject="policy_setting"  
           MarshalDelegate="policy_setting"  
           MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="fb1cc-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="fb1cc-105">Attributes and Elements</span></span>  

 <span data-ttu-id="fb1cc-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="fb1cc-107">屬性</span><span class="sxs-lookup"><span data-stu-id="fb1cc-107">Attributes</span></span>  
  
|<span data-ttu-id="fb1cc-108">屬性</span><span class="sxs-lookup"><span data-stu-id="fb1cc-108">Attribute</span></span>|<span data-ttu-id="fb1cc-109">屬性類型</span><span class="sxs-lookup"><span data-stu-id="fb1cc-109">Attribute type</span></span>|<span data-ttu-id="fb1cc-110">描述</span><span class="sxs-lookup"><span data-stu-id="fb1cc-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Name`|<span data-ttu-id="fb1cc-111">一般</span><span class="sxs-lookup"><span data-stu-id="fb1cc-111">General</span></span>|<span data-ttu-id="fb1cc-112">必要屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-112">Required attribute.</span></span> <span data-ttu-id="fb1cc-113">指定命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-113">Specifies the name of the namespace.</span></span>|  
|`Activate`|<span data-ttu-id="fb1cc-114">反射</span><span class="sxs-lookup"><span data-stu-id="fb1cc-114">Reflection</span></span>|<span data-ttu-id="fb1cc-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-115">Optional attribute.</span></span> <span data-ttu-id="fb1cc-116">控制建構函式的執行階段存取，以便啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-116">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="fb1cc-117">反射</span><span class="sxs-lookup"><span data-stu-id="fb1cc-117">Reflection</span></span>|<span data-ttu-id="fb1cc-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-118">Optional attribute.</span></span> <span data-ttu-id="fb1cc-119">控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-119">Controls querying for information about program elements, but does not enable any runtime access.</span></span>|  
|`Dynamic`|<span data-ttu-id="fb1cc-120">反射</span><span class="sxs-lookup"><span data-stu-id="fb1cc-120">Reflection</span></span>|<span data-ttu-id="fb1cc-121">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-121">Optional attribute.</span></span> <span data-ttu-id="fb1cc-122">控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-122">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="fb1cc-123">序列化</span><span class="sxs-lookup"><span data-stu-id="fb1cc-123">Serialization</span></span>|<span data-ttu-id="fb1cc-124">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-124">Optional attribute.</span></span> <span data-ttu-id="fb1cc-125">控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-125">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="fb1cc-126">序列化</span><span class="sxs-lookup"><span data-stu-id="fb1cc-126">Serialization</span></span>|<span data-ttu-id="fb1cc-127">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-127">Optional attribute.</span></span> <span data-ttu-id="fb1cc-128">控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-128">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="fb1cc-129">序列化</span><span class="sxs-lookup"><span data-stu-id="fb1cc-129">Serialization</span></span>|<span data-ttu-id="fb1cc-130">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-130">Optional attribute.</span></span> <span data-ttu-id="fb1cc-131">控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-131">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="fb1cc-132">序列化</span><span class="sxs-lookup"><span data-stu-id="fb1cc-132">Serialization</span></span>|<span data-ttu-id="fb1cc-133">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-133">Optional attribute.</span></span> <span data-ttu-id="fb1cc-134">控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-134">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="fb1cc-135">Interop</span><span class="sxs-lookup"><span data-stu-id="fb1cc-135">Interop</span></span>|<span data-ttu-id="fb1cc-136">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-136">Optional attribute.</span></span> <span data-ttu-id="fb1cc-137">控制 Windows 執行階段和 COM 之參考類型的封送處理原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-137">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="fb1cc-138">Interop</span><span class="sxs-lookup"><span data-stu-id="fb1cc-138">Interop</span></span>|<span data-ttu-id="fb1cc-139">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-139">Optional attribute.</span></span> <span data-ttu-id="fb1cc-140">控制將委派類型當作函式指標封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-140">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="fb1cc-141">Interop</span><span class="sxs-lookup"><span data-stu-id="fb1cc-141">Interop</span></span>|<span data-ttu-id="fb1cc-142">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-142">Optional attribute.</span></span> <span data-ttu-id="fb1cc-143">控制將結構封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-143">Controls policy for marshaling structures to native code.</span></span>|  
  
## <a name="name-attribute"></a><span data-ttu-id="fb1cc-144">Name 屬性</span><span class="sxs-lookup"><span data-stu-id="fb1cc-144">Name attribute</span></span>  
  
|<span data-ttu-id="fb1cc-145">值</span><span class="sxs-lookup"><span data-stu-id="fb1cc-145">Value</span></span>|<span data-ttu-id="fb1cc-146">描述</span><span class="sxs-lookup"><span data-stu-id="fb1cc-146">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="fb1cc-147">*namespace_name*</span><span class="sxs-lookup"><span data-stu-id="fb1cc-147">*namespace_name*</span></span>|<span data-ttu-id="fb1cc-148">命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-148">The namespace name.</span></span> <span data-ttu-id="fb1cc-149">如果 \<Namespace> 元素是、或專案的子 [\<Application>](application-element-net-native.md) 系 [\<Library>](library-element-net-native.md) [\<Assembly>](assembly-element-net-native.md) ， *namespace_name* 必須是完整命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-149">If the \<Namespace> element is a child of an [\<Application>](application-element-net-native.md), [\<Library>](library-element-net-native.md), or [\<Assembly>](assembly-element-net-native.md) element, *namespace_name* must be a fully qualified namespace name.</span></span> <span data-ttu-id="fb1cc-150">如果 \<Namespace> 元素是另一個專案的子系 \<Namespace> ， *namespace_name* 必須是相對的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-150">If the \<Namespace> element is a child of another \<Namespace> element, *namespace_name* must be a relative namespace name.</span></span>|  
  
## <a name="all-other-attributes"></a><span data-ttu-id="fb1cc-151">所有其他屬性</span><span class="sxs-lookup"><span data-stu-id="fb1cc-151">All other attributes</span></span>  
  
|<span data-ttu-id="fb1cc-152">值</span><span class="sxs-lookup"><span data-stu-id="fb1cc-152">Value</span></span>|<span data-ttu-id="fb1cc-153">描述</span><span class="sxs-lookup"><span data-stu-id="fb1cc-153">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="fb1cc-154">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="fb1cc-154">*policy_setting*</span></span>|<span data-ttu-id="fb1cc-155">針對命名空間中的所有類型，要套用到此原則類型的設定。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-155">The setting to apply to this policy type for all types in the namespace.</span></span> <span data-ttu-id="fb1cc-156">可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-156">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="fb1cc-157">如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-157">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="fb1cc-158">子元素</span><span class="sxs-lookup"><span data-stu-id="fb1cc-158">Child Elements</span></span>  
  
|<span data-ttu-id="fb1cc-159">元素</span><span class="sxs-lookup"><span data-stu-id="fb1cc-159">Element</span></span>|<span data-ttu-id="fb1cc-160">描述</span><span class="sxs-lookup"><span data-stu-id="fb1cc-160">Description</span></span>|  
|-------------|-----------------|  
|`<Namespace>`|<span data-ttu-id="fb1cc-161">將執行階段反映原則套用至父命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-161">Applies runtime reflection policy to all types in a parent namespace.</span></span>|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="fb1cc-162">將反映原則套用至類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-162">Applies reflection policy to a type.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="fb1cc-163">將反映原則套用至建構的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-163">Applies reflection policy to a constructed generic type.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="fb1cc-164">父項目</span><span class="sxs-lookup"><span data-stu-id="fb1cc-164">Parent Elements</span></span>  
  
|<span data-ttu-id="fb1cc-165">元素</span><span class="sxs-lookup"><span data-stu-id="fb1cc-165">Element</span></span>|<span data-ttu-id="fb1cc-166">描述</span><span class="sxs-lookup"><span data-stu-id="fb1cc-166">Description</span></span>|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|<span data-ttu-id="fb1cc-167">做為容器，以包含整個應用程式的類型，以及中繼資料可在執行階段用於反映的類型成員。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-167">Serves as a container for application-wide types and type members whose metadata is available for reflection at run time.</span></span> <span data-ttu-id="fb1cc-168">[\<Application>](application-element-net-native.md)元素可以有零個、一個或多個 [\<Assembly>](assembly-element-net-native.md) 元素。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-168">The [\<Application>](application-element-net-native.md) element can have zero, one, or more [\<Assembly>](assembly-element-net-native.md) elements.</span></span>|  
|[\<Assembly>](assembly-element-net-native.md)|<span data-ttu-id="fb1cc-169">將執行階段反映原則套用至指定組件中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-169">Applies runtime reflection policy to all the types in a specified assembly.</span></span>|  
|[\<Library>](library-element-net-native.md)|<span data-ttu-id="fb1cc-170">定義包含類型和類型成員的組件，這些類型和類型成員的中繼資料可在執行階段用於反映。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-170">Defines the assembly that contains types and type members whose metadata is available for reflection at run time.</span></span> <span data-ttu-id="fb1cc-171">[\<Library>](library-element-net-native.md)元素可以有零個或一個 [\<Assembly>](assembly-element-net-native.md) 元素。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-171">The [\<Library>](library-element-net-native.md) element can have zero or one [\<Assembly>](assembly-element-net-native.md) element.</span></span>|  
|`<Namespace>`|<span data-ttu-id="fb1cc-172">將反映原則套用至父命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-172">Applies reflection policy to all types in a parent namespace.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fb1cc-173">備註</span><span class="sxs-lookup"><span data-stu-id="fb1cc-173">Remarks</span></span>  

 <span data-ttu-id="fb1cc-174">`Activate`、`Browse`、`Dynamic` 和 `Serialize` 都是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-174">The `Activate`, `Browse`, `Dynamic`, and `Serialize` attributes are all optional.</span></span> <span data-ttu-id="fb1cc-175">如果都不存在，`<Namespace>` 元素只會用來做為子元素的容器。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-175">If none are present, the `<Namespace>` element serves only as a container for child elements.</span></span> <span data-ttu-id="fb1cc-176">如果存在，則 `<Namespace>` 元素會將執行階段反映原則套用至指定命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-176">If they are present, the `<Namespace>` element applies runtime reflection policy to all the types in the specified namespace.</span></span>  
  
 <span data-ttu-id="fb1cc-177">當它是專案的子系時 [\<Assembly>](assembly-element-net-native.md) ， `<Namespace>` 元素會覆寫元素所定義的執行時間反映原則  [\<Assembly>](assembly-element-net-native.md) 。</span><span class="sxs-lookup"><span data-stu-id="fb1cc-177">When it is a child of the [\<Assembly>](assembly-element-net-native.md) element, the `<Namespace>` element overrides the runtime reflection policy defined by the  [\<Assembly>](assembly-element-net-native.md) element.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fb1cc-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fb1cc-178">See also</span></span>

- [<span data-ttu-id="fb1cc-179">執行階段指示詞原則設定</span><span class="sxs-lookup"><span data-stu-id="fb1cc-179">Runtime Directive Policy Settings</span></span>](runtime-directive-policy-settings.md)
- [<span data-ttu-id="fb1cc-180">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="fb1cc-180">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="fb1cc-181">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="fb1cc-181">Runtime Directive Elements</span></span>](runtime-directive-elements.md)

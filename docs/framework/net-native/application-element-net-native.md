---
title: <Application>元素（.NET Native）
ms.date: 03/30/2017
ms.assetid: b4e9b37a-059b-4076-8f56-cb3f9cef0cd9
ms.openlocfilehash: e26826b3d8674b536ab0897182da58bc02cfd00b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128524"
---
# <a name="application-element-net-native"></a><span data-ttu-id="3241f-102">\<Application>元素（.NET Native）</span><span class="sxs-lookup"><span data-stu-id="3241f-102">\<Application> Element (.NET Native)</span></span>
<span data-ttu-id="3241f-103">做為容器，以包含整個應用程式中，可在執行階段將中繼資料用於反映的類型和類型成員，並將執行階段反映原則套用至應用程式中的所有程式元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-103">Serves as a container for application-wide types and type members whose metadata is available for reflection at run time, and applies runtime reflection policy to all the program elements in an app.</span></span>  
  
 <span data-ttu-id="3241f-104">\<Directives> 項目</span><span class="sxs-lookup"><span data-stu-id="3241f-104">\<Directives> Element</span></span>  
<span data-ttu-id="3241f-105">\<Application>元素（rd .xml）</span><span class="sxs-lookup"><span data-stu-id="3241f-105">\<Application> Element (rd.xml)</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3241f-106">語法</span><span class="sxs-lookup"><span data-stu-id="3241f-106">Syntax</span></span>  
  
```xml  
<Application Activate="policy_setting"  
             Browse="policy_setting"  
             Dynamic="policy_setting"  
             Serialize="policy_setting"  
             DataContractSerializer="policy_setting"  
             DataContractJsonSerializer="policy_setting"  
             XmlSerializer="policy_setting"  
             MarshalObject="policy_setting"  
             MarshalDelegate="policy_setting"  
             MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="3241f-107">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="3241f-107">Attributes and Elements</span></span>  
 <span data-ttu-id="3241f-108">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-108">The following sections describe attributes, child elements, and parent elements.</span></span> <span data-ttu-id="3241f-109">在「子元素」表格中，原則會指出可在執行階段供特定程式元素使用的中繼資料種類。</span><span class="sxs-lookup"><span data-stu-id="3241f-109">In the Child Elements table, policy refers to the kind of metadata that is made available for particular program elements at run time.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="3241f-110">屬性</span><span class="sxs-lookup"><span data-stu-id="3241f-110">Attributes</span></span>  
  
|<span data-ttu-id="3241f-111">屬性</span><span class="sxs-lookup"><span data-stu-id="3241f-111">Attribute</span></span>|<span data-ttu-id="3241f-112">屬性類型</span><span class="sxs-lookup"><span data-stu-id="3241f-112">Attribute type</span></span>|<span data-ttu-id="3241f-113">描述</span><span class="sxs-lookup"><span data-stu-id="3241f-113">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Activate`|<span data-ttu-id="3241f-114">反射</span><span class="sxs-lookup"><span data-stu-id="3241f-114">Reflection</span></span>|<span data-ttu-id="3241f-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-115">Optional attribute.</span></span> <span data-ttu-id="3241f-116">控制建構函式的執行階段存取，以便啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="3241f-116">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="3241f-117">反射</span><span class="sxs-lookup"><span data-stu-id="3241f-117">Reflection</span></span>|<span data-ttu-id="3241f-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-118">Optional attribute.</span></span> <span data-ttu-id="3241f-119">控制對類型相關資訊的查詢，或控制類型的列舉，但不會在執行階段啟用任何動態存取。</span><span class="sxs-lookup"><span data-stu-id="3241f-119">Controls querying for information about or enumerating the types, but does not enable any dynamic access at run time.</span></span>|  
|`Dynamic`|<span data-ttu-id="3241f-120">反射</span><span class="sxs-lookup"><span data-stu-id="3241f-120">Reflection</span></span>|<span data-ttu-id="3241f-121">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-121">Optional attribute.</span></span> <span data-ttu-id="3241f-122">控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="3241f-122">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="3241f-123">序列化</span><span class="sxs-lookup"><span data-stu-id="3241f-123">Serialization</span></span>|<span data-ttu-id="3241f-124">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-124">Optional attribute.</span></span> <span data-ttu-id="3241f-125">控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="3241f-125">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="3241f-126">序列化</span><span class="sxs-lookup"><span data-stu-id="3241f-126">Serialization</span></span>|<span data-ttu-id="3241f-127">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-127">Optional Attribute.</span></span> <span data-ttu-id="3241f-128">控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-128">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="3241f-129">序列化</span><span class="sxs-lookup"><span data-stu-id="3241f-129">Serialization</span></span>|<span data-ttu-id="3241f-130">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-130">Optional Attribute.</span></span> <span data-ttu-id="3241f-131">控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-131">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="3241f-132">序列化</span><span class="sxs-lookup"><span data-stu-id="3241f-132">Serialization</span></span>|<span data-ttu-id="3241f-133">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-133">Optional Attribute.</span></span> <span data-ttu-id="3241f-134">控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-134">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="3241f-135">Interop</span><span class="sxs-lookup"><span data-stu-id="3241f-135">Interop</span></span>|<span data-ttu-id="3241f-136">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-136">Optional Attribute.</span></span> <span data-ttu-id="3241f-137">控制 Windows 執行階段和 COM 之參考類型的封送處理原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-137">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="3241f-138">Interop</span><span class="sxs-lookup"><span data-stu-id="3241f-138">Interop</span></span>|<span data-ttu-id="3241f-139">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-139">Optional Attribute.</span></span> <span data-ttu-id="3241f-140">控制將委派類型當作函式指標封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-140">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="3241f-141">Interop</span><span class="sxs-lookup"><span data-stu-id="3241f-141">Interop</span></span>|<span data-ttu-id="3241f-142">選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-142">Optional Attribute.</span></span> <span data-ttu-id="3241f-143">控制將結構封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="3241f-143">Controls policy for marshaling structures to native code.</span></span>|  
  
## <a name="all-attributes"></a><span data-ttu-id="3241f-144">所有屬性</span><span class="sxs-lookup"><span data-stu-id="3241f-144">All attributes</span></span>  
  
|<span data-ttu-id="3241f-145">值</span><span class="sxs-lookup"><span data-stu-id="3241f-145">Value</span></span>|<span data-ttu-id="3241f-146">說明</span><span class="sxs-lookup"><span data-stu-id="3241f-146">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="3241f-147">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="3241f-147">*policy_setting*</span></span>|<span data-ttu-id="3241f-148">要讓這個原則在應用程式中套用至類型的設定。</span><span class="sxs-lookup"><span data-stu-id="3241f-148">The setting for this policy to apply to the types in the app.</span></span> <span data-ttu-id="3241f-149">可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。</span><span class="sxs-lookup"><span data-stu-id="3241f-149">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="3241f-150">如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="3241f-150">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="3241f-151">子元素</span><span class="sxs-lookup"><span data-stu-id="3241f-151">Child Elements</span></span>  
  
|<span data-ttu-id="3241f-152">元素</span><span class="sxs-lookup"><span data-stu-id="3241f-152">Element</span></span>|<span data-ttu-id="3241f-153">描述</span><span class="sxs-lookup"><span data-stu-id="3241f-153">Description</span></span>|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|<span data-ttu-id="3241f-154">將原則套用至特定組件中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="3241f-154">Applies policy to all the types in a particular assembly.</span></span>|  
|[\<Namespace>](namespace-element-net-native.md)|<span data-ttu-id="3241f-155">將原則套用至特定命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="3241f-155">Applies policy to all the types in a particular namespace.</span></span>|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="3241f-156">將原則套用至特定類型，例如類別或結構。</span><span class="sxs-lookup"><span data-stu-id="3241f-156">Applies policy to a particular type, such as a class or structure.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="3241f-157">將原則套用至建構的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="3241f-157">Applies policy to a constructed generic type.</span></span> <span data-ttu-id="3241f-158">例如， [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 元素可用來定義類型的原則 `List<String>` 。</span><span class="sxs-lookup"><span data-stu-id="3241f-158">For example, a [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element could be used to define policy for a `List<String>` type.</span></span>|  
|[\<Method>](method-element-net-native.md)|<span data-ttu-id="3241f-159">將原則套用至特定類型上的方法。</span><span class="sxs-lookup"><span data-stu-id="3241f-159">Applies policy to a method on a particular type.</span></span>|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|<span data-ttu-id="3241f-160">將原則套用至建構的泛型方法。</span><span class="sxs-lookup"><span data-stu-id="3241f-160">Applies policy to a constructed generic method.</span></span>|  
|[\<Property>](property-element-net-native.md)|<span data-ttu-id="3241f-161">將原則套用至特定類型上的屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-161">Applies policy to a property on a particular type.</span></span>|  
|[\<Field>](field-element-net-native.md)|<span data-ttu-id="3241f-162">將原則套用至特定類型上的欄位。</span><span class="sxs-lookup"><span data-stu-id="3241f-162">Applies policy to a field on a particular type.</span></span>|  
|[\<Event>](event-element-net-native.md)|<span data-ttu-id="3241f-163">將原則套用至特定類型上的事件。</span><span class="sxs-lookup"><span data-stu-id="3241f-163">Applies policy to an event on a particular type.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="3241f-164">父項目</span><span class="sxs-lookup"><span data-stu-id="3241f-164">Parent Elements</span></span>  
  
|<span data-ttu-id="3241f-165">元素</span><span class="sxs-lookup"><span data-stu-id="3241f-165">Element</span></span>|<span data-ttu-id="3241f-166">描述</span><span class="sxs-lookup"><span data-stu-id="3241f-166">Description</span></span>|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|<span data-ttu-id="3241f-167">執行階段指示詞檔案的根項目。</span><span class="sxs-lookup"><span data-stu-id="3241f-167">The root element of a runtime directives file.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3241f-168">備註</span><span class="sxs-lookup"><span data-stu-id="3241f-168">Remarks</span></span>  
 <span data-ttu-id="3241f-169">[\<Directives>](directives-element-net-native.md)元素可以包含零個或一個 `<Application>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-169">The [\<Directives>](directives-element-net-native.md) element can contain zero or one `<Application>` element.</span></span> <span data-ttu-id="3241f-170">不支援單一反映指示詞檔案中有多個 `<Application>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-170">Multiple `<Application>` elements in a single reflection directives file are not supported.</span></span>  
  
 <span data-ttu-id="3241f-171">`<Application>` 元素有兩種用法：</span><span class="sxs-lookup"><span data-stu-id="3241f-171">The `<Application>` element can be used in one of two ways:</span></span>  
  
- <span data-ttu-id="3241f-172">做為容器，以定義在執行階段會需要其中繼資料的程式元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-172">As a container to define the program elements whose metadata is needed at run time.</span></span> <span data-ttu-id="3241f-173">在此情況下，`<Application>` 元素不需要任何屬性。</span><span class="sxs-lookup"><span data-stu-id="3241f-173">In this case, the `<Application>` element need not have any attributes.</span></span> <span data-ttu-id="3241f-174">在編譯時期，編譯器工具會在所有程式庫 (包括 .NET Framework 核心程式庫) 中，搜尋 `<Application>` 元素的子元素所識別的程式元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-174">At compile time, compiler tools search all libraries, including .NET Framework core libraries, for program elements identified by child elements of the `<Application>` element.</span></span> <span data-ttu-id="3241f-175">相反地，編譯器工具只會搜尋元素所指定的程式庫， [\<Library>](library-element-net-native.md) 以代表的子項目所識別的程式元素 [\<Library>](library-element-net-native.md) 。</span><span class="sxs-lookup"><span data-stu-id="3241f-175">In contrast, compiler tools search only the library designated by the [\<Library>](library-element-net-native.md) element for program elements identified by the child elements of [\<Library>](library-element-net-native.md).</span></span>  
  
- <span data-ttu-id="3241f-176">做為用來為反映、序列化和 interop 設定整個應用程式原則的元素。</span><span class="sxs-lookup"><span data-stu-id="3241f-176">As an element that sets application-wide policy for reflection, serialization, and interop.</span></span> <span data-ttu-id="3241f-177">元素的屬性 `<Application>` 會定義整個應用程式原則，這可能會由或元素所定義的子項目覆 `<Application>` 寫 [\<Library>](library-element-net-native.md) 。</span><span class="sxs-lookup"><span data-stu-id="3241f-177">The attributes of the `<Application>` element define application-wide policy, which may be overridden by the child elements defined by the `<Application>` or [\<Library>](library-element-net-native.md) element.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3241f-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3241f-178">See also</span></span>

- [<span data-ttu-id="3241f-179">\<Library>元素</span><span class="sxs-lookup"><span data-stu-id="3241f-179">\<Library> Element</span></span>](library-element-net-native.md)
- [<span data-ttu-id="3241f-180">\<Directives>元素</span><span class="sxs-lookup"><span data-stu-id="3241f-180">\<Directives> Element</span></span>](directives-element-net-native.md)
- [<span data-ttu-id="3241f-181">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="3241f-181">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="3241f-182">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="3241f-182">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)

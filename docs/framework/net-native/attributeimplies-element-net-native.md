---
title: <AttributeImplies>元素（.NET Native）
ms.date: 03/30/2017
ms.assetid: 82db7193-a860-418b-84fc-fff2fdf2e025
ms.openlocfilehash: 2ab1fdc71bc43f61f69a0d9b7bea7acb35e14ea5
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79181068"
---
# <a name="attributeimplies-element-net-native"></a><span data-ttu-id="27f98-102">\<AttributeImplies>元素（.NET Native）</span><span class="sxs-lookup"><span data-stu-id="27f98-102">\<AttributeImplies> Element (.NET Native)</span></span>
<span data-ttu-id="27f98-103">定義套用包含屬性之程式碼元素的原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-103">Defines policy for code elements the containing attribute is applied to.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="27f98-104">語法</span><span class="sxs-lookup"><span data-stu-id="27f98-104">Syntax</span></span>  
  
```xml  
<AttributeImplies Activate="policy_type"  
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
  
## <a name="attributes-and-elements"></a><span data-ttu-id="27f98-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="27f98-105">Attributes and Elements</span></span>  
 <span data-ttu-id="27f98-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="27f98-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="27f98-107">屬性</span><span class="sxs-lookup"><span data-stu-id="27f98-107">Attributes</span></span>  
  
|<span data-ttu-id="27f98-108">屬性</span><span class="sxs-lookup"><span data-stu-id="27f98-108">Attribute</span></span>|<span data-ttu-id="27f98-109">屬性類型</span><span class="sxs-lookup"><span data-stu-id="27f98-109">Attribute type</span></span>|<span data-ttu-id="27f98-110">描述</span><span class="sxs-lookup"><span data-stu-id="27f98-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Activate`|<span data-ttu-id="27f98-111">反射</span><span class="sxs-lookup"><span data-stu-id="27f98-111">Reflection</span></span>|<span data-ttu-id="27f98-112">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-112">Optional attribute.</span></span> <span data-ttu-id="27f98-113">控制建構函式的執行階段存取，以便啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="27f98-113">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="27f98-114">反射</span><span class="sxs-lookup"><span data-stu-id="27f98-114">Reflection</span></span>|<span data-ttu-id="27f98-115">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-115">Optional attribute.</span></span> <span data-ttu-id="27f98-116">控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。</span><span class="sxs-lookup"><span data-stu-id="27f98-116">Controls querying for information about program elements, but does not enable any runtime access.</span></span>|  
|`Dynamic`|<span data-ttu-id="27f98-117">反射</span><span class="sxs-lookup"><span data-stu-id="27f98-117">Reflection</span></span>|<span data-ttu-id="27f98-118">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-118">Optional attribute.</span></span> <span data-ttu-id="27f98-119">控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="27f98-119">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="27f98-120">序列化</span><span class="sxs-lookup"><span data-stu-id="27f98-120">Serialization</span></span>|<span data-ttu-id="27f98-121">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-121">Optional attribute.</span></span> <span data-ttu-id="27f98-122">控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="27f98-122">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="27f98-123">序列化</span><span class="sxs-lookup"><span data-stu-id="27f98-123">Serialization</span></span>|<span data-ttu-id="27f98-124">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-124">Optional attribute.</span></span> <span data-ttu-id="27f98-125">控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-125">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="27f98-126">序列化</span><span class="sxs-lookup"><span data-stu-id="27f98-126">Serialization</span></span>|<span data-ttu-id="27f98-127">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-127">Optional attribute.</span></span> <span data-ttu-id="27f98-128">控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-128">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="27f98-129">序列化</span><span class="sxs-lookup"><span data-stu-id="27f98-129">Serialization</span></span>|<span data-ttu-id="27f98-130">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-130">Optional attribute.</span></span> <span data-ttu-id="27f98-131">控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-131">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="27f98-132">Interop</span><span class="sxs-lookup"><span data-stu-id="27f98-132">Interop</span></span>|<span data-ttu-id="27f98-133">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-133">Optional attribute.</span></span> <span data-ttu-id="27f98-134">控制 Windows 執行階段和 COM 之參考類型的封送處理原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-134">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="27f98-135">Interop</span><span class="sxs-lookup"><span data-stu-id="27f98-135">Interop</span></span>|<span data-ttu-id="27f98-136">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-136">Optional attribute.</span></span> <span data-ttu-id="27f98-137">控制將委派類型當作函式指標封送處理至機器碼的原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-137">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="27f98-138">Interop</span><span class="sxs-lookup"><span data-stu-id="27f98-138">Interop</span></span>|<span data-ttu-id="27f98-139">選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="27f98-139">Optional attribute.</span></span> <span data-ttu-id="27f98-140">控制將值類型封送處理為原生程式碼的原則。</span><span class="sxs-lookup"><span data-stu-id="27f98-140">Controls policy for marshaling value types to native code.</span></span>|  
  
## <a name="all-attributes"></a><span data-ttu-id="27f98-141">所有屬性</span><span class="sxs-lookup"><span data-stu-id="27f98-141">All attributes</span></span>  
  
|<span data-ttu-id="27f98-142">值</span><span class="sxs-lookup"><span data-stu-id="27f98-142">Value</span></span>|<span data-ttu-id="27f98-143">說明</span><span class="sxs-lookup"><span data-stu-id="27f98-143">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="27f98-144">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="27f98-144">*policy_setting*</span></span>|<span data-ttu-id="27f98-145">要套用到此原則類型的設定。</span><span class="sxs-lookup"><span data-stu-id="27f98-145">The setting to apply to this policy type.</span></span> <span data-ttu-id="27f98-146">可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。</span><span class="sxs-lookup"><span data-stu-id="27f98-146">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="27f98-147">如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="27f98-147">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="27f98-148">子元素</span><span class="sxs-lookup"><span data-stu-id="27f98-148">Child Elements</span></span>  
 <span data-ttu-id="27f98-149">無。</span><span class="sxs-lookup"><span data-stu-id="27f98-149">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="27f98-150">父項目</span><span class="sxs-lookup"><span data-stu-id="27f98-150">Parent Elements</span></span>  
  
|<span data-ttu-id="27f98-151">元素</span><span class="sxs-lookup"><span data-stu-id="27f98-151">Element</span></span>|<span data-ttu-id="27f98-152">描述</span><span class="sxs-lookup"><span data-stu-id="27f98-152">Description</span></span>|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="27f98-153">將反映原則套用至類型及其所有成員。</span><span class="sxs-lookup"><span data-stu-id="27f98-153">Applies reflection policy to a type and all its members.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="27f98-154">備註</span><span class="sxs-lookup"><span data-stu-id="27f98-154">Remarks</span></span>  
 <span data-ttu-id="27f98-155">如果 `<AttributeImplies>` 元素的包含類型是屬性 (也就是衍生自 <xref:System.Attribute?displayProperty=nameWithType> 的類別)，就會使用此元素。</span><span class="sxs-lookup"><span data-stu-id="27f98-155">The `<AttributeImplies>` element is used if its containing type is an attribute (that is, a class derived from <xref:System.Attribute?displayProperty=nameWithType>).</span></span> <span data-ttu-id="27f98-156">如果屬性套用至特定的程式元素，則 `<AttributeImplies>` 元素所定義的原則會套用至該程式元素。</span><span class="sxs-lookup"><span data-stu-id="27f98-156">If the attribute is applied to a particular program element, the policy defined by the `<AttributeImplies>` element applies to that program element.</span></span>  
  
 <span data-ttu-id="27f98-157">反映、序列化和 interop 屬性都是選用性，但至少要有一個屬性存在。</span><span class="sxs-lookup"><span data-stu-id="27f98-157">The reflection, serialization, and interop attributes are all optional, although at least one should be present.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="27f98-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="27f98-158">See also</span></span>

- [<span data-ttu-id="27f98-159">\<Type>元素</span><span class="sxs-lookup"><span data-stu-id="27f98-159">\<Type> Element</span></span>](type-element-net-native.md)
- [<span data-ttu-id="27f98-160">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="27f98-160">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="27f98-161">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="27f98-161">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="27f98-162">執行階段指示詞原則設定</span><span class="sxs-lookup"><span data-stu-id="27f98-162">Runtime Directive Policy Settings</span></span>](runtime-directive-policy-settings.md)

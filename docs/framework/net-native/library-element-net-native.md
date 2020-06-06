---
title: <Library>元素（.NET Native）
ms.date: 03/30/2017
ms.assetid: f642276b-33fb-4a81-b882-8808c31ba69e
ms.openlocfilehash: f94bfe047fa7a95b6f24264bae0b27112c589dfd
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128360"
---
# <a name="library-element-net-native"></a><span data-ttu-id="52d07-102">\<Library>元素（.NET Native）</span><span class="sxs-lookup"><span data-stu-id="52d07-102">\<Library> Element (.NET Native)</span></span>
<span data-ttu-id="52d07-103">定義包含類型和類型成員的組件，這些類型和類型成員的中繼資料可在執行階段用於反映。</span><span class="sxs-lookup"><span data-stu-id="52d07-103">Defines the assembly that contains types and type members whose metadata is available for reflection at run time.</span></span>  
  
 <span data-ttu-id="52d07-104">\<Directives> 項目</span><span class="sxs-lookup"><span data-stu-id="52d07-104">\<Directives> Element</span></span>  
<span data-ttu-id="52d07-105">\<Library> 項目</span><span class="sxs-lookup"><span data-stu-id="52d07-105">\<Library> Element</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="52d07-106">語法</span><span class="sxs-lookup"><span data-stu-id="52d07-106">Syntax</span></span>  
  
```xml  
<Library Name="assembly_name" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="52d07-107">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="52d07-107">Attributes and Elements</span></span>  
 <span data-ttu-id="52d07-108">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="52d07-108">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="52d07-109">屬性</span><span class="sxs-lookup"><span data-stu-id="52d07-109">Attributes</span></span>  
  
|<span data-ttu-id="52d07-110">屬性</span><span class="sxs-lookup"><span data-stu-id="52d07-110">Attribute</span></span>|<span data-ttu-id="52d07-111">描述</span><span class="sxs-lookup"><span data-stu-id="52d07-111">Description</span></span>|  
|---------------|-----------------|  
|`Name`|<span data-ttu-id="52d07-112">必要屬性。</span><span class="sxs-lookup"><span data-stu-id="52d07-112">Required attribute.</span></span> <span data-ttu-id="52d07-113">指定組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="52d07-113">Specifies the name of an assembly.</span></span> <span data-ttu-id="52d07-114">這個 `<Library>` 項目的子項目可針對這個組件中找到的類型和類型成員，定義其執行階段反映原則。</span><span class="sxs-lookup"><span data-stu-id="52d07-114">Child elements of this `<Library>` element define the runtime reflection policy for types and type members found in this assembly.</span></span>|  
  
## <a name="name-attribute"></a><span data-ttu-id="52d07-115">Name 屬性</span><span class="sxs-lookup"><span data-stu-id="52d07-115">Name attribute</span></span>  
  
|<span data-ttu-id="52d07-116">值</span><span class="sxs-lookup"><span data-stu-id="52d07-116">Value</span></span>|<span data-ttu-id="52d07-117">描述</span><span class="sxs-lookup"><span data-stu-id="52d07-117">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="52d07-118">*assembly_name*</span><span class="sxs-lookup"><span data-stu-id="52d07-118">*assembly_name*</span></span>|<span data-ttu-id="52d07-119">組件的簡單名稱，不包含其副檔名。</span><span class="sxs-lookup"><span data-stu-id="52d07-119">The simple name of the assembly, without its file extension.</span></span> <span data-ttu-id="52d07-120">這個屬性 (Attribute) 會對應至 <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> 屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="52d07-120">This attribute corresponds to the <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="52d07-121">例如，名為 Extensions.dll 之組件的名稱是 "Extensions"。</span><span class="sxs-lookup"><span data-stu-id="52d07-121">For example, the name of an assembly named Extensions.dll is "Extensions".</span></span> <span data-ttu-id="52d07-122">如需支援從組件條件式包含中繼資料之 *assembly_name* 的特殊格式，請參閱＜備註＞一節。</span><span class="sxs-lookup"><span data-stu-id="52d07-122">See the Remarks section for a special form of *assembly_name* that supports conditional inclusion of metadata from the assembly.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="52d07-123">子元素</span><span class="sxs-lookup"><span data-stu-id="52d07-123">Child Elements</span></span>  
  
|<span data-ttu-id="52d07-124">元素</span><span class="sxs-lookup"><span data-stu-id="52d07-124">Element</span></span>|<span data-ttu-id="52d07-125">描述</span><span class="sxs-lookup"><span data-stu-id="52d07-125">Description</span></span>|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|<span data-ttu-id="52d07-126">將原則套用至特定組件中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="52d07-126">Applies policy to all the types in a particular assembly.</span></span>|  
|[\<Namespace>](namespace-element-net-native.md)|<span data-ttu-id="52d07-127">將原則套用至特定命名空間中的所有類型。</span><span class="sxs-lookup"><span data-stu-id="52d07-127">Applies policy to all the types in a particular namespace.</span></span>|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="52d07-128">將原則套用至特定類型，例如類別或結構。</span><span class="sxs-lookup"><span data-stu-id="52d07-128">Applies policy to a particular type, such as a class or structure.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="52d07-129">將原則套用至建構的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="52d07-129">Applies policy to a constructed generic type.</span></span> <span data-ttu-id="52d07-130">例如， [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 元素可用來定義類型的原則 `List<String>` 。</span><span class="sxs-lookup"><span data-stu-id="52d07-130">For example, a [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element could be used to define policy for a `List<String>` type.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="52d07-131">父項目</span><span class="sxs-lookup"><span data-stu-id="52d07-131">Parent Elements</span></span>  
  
|<span data-ttu-id="52d07-132">元素</span><span class="sxs-lookup"><span data-stu-id="52d07-132">Element</span></span>|<span data-ttu-id="52d07-133">描述</span><span class="sxs-lookup"><span data-stu-id="52d07-133">Description</span></span>|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|<span data-ttu-id="52d07-134">執行階段指示詞檔案的根項目。</span><span class="sxs-lookup"><span data-stu-id="52d07-134">The root element of a runtime directives file.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="52d07-135">備註</span><span class="sxs-lookup"><span data-stu-id="52d07-135">Remarks</span></span>  
 <span data-ttu-id="52d07-136">[\<Directives>](directives-element-net-native.md)元素可以包含零個、一個或多個 `<Library>` 元素。</span><span class="sxs-lookup"><span data-stu-id="52d07-136">The [\<Directives>](directives-element-net-native.md) element can contain zero, one, or more `<Library>` elements.</span></span>  
  
 <span data-ttu-id="52d07-137">`<Library>` 項目可當做容器來使用，以定義在執行階段需要中繼資料的程式項目；這個項目不會表示原則。</span><span class="sxs-lookup"><span data-stu-id="52d07-137">The `<Library>` element serves as a container to define the program elements whose metadata is needed at run time; this element doesn't express policy.</span></span> <span data-ttu-id="52d07-138">在編譯時期，編譯器工具只會在 `<Library>` 項目所指定的程式庫中，搜尋其子項目所識別的程式項目。</span><span class="sxs-lookup"><span data-stu-id="52d07-138">At compile time, compiler tools search only the library designated by the `<Library>` element for program elements identified by its child elements.</span></span> <span data-ttu-id="52d07-139">相反地，編譯器工具會搜尋所有程式庫（including.NET Framework 核心程式庫），以尋找元素的子項目所識別的程式元素 [\<Application>](application-element-net-native.md) 。</span><span class="sxs-lookup"><span data-stu-id="52d07-139">In contrast, compiler tools search all libraries, including.NET Framework core libraries, for program elements identified by child elements of the [\<Application>](application-element-net-native.md) element.</span></span>  
  
 <span data-ttu-id="52d07-140">您可以有條件地利用 `<Library>` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="52d07-140">`<Library>` directives may be conditionally utilized.</span></span> <span data-ttu-id="52d07-141">如果專案名稱的 `<Library>` 開頭和結尾都是星號（ \* ），則只有在 `<Library>` 應用程式參考星號之間指定的元件時，指示詞才會生效。</span><span class="sxs-lookup"><span data-stu-id="52d07-141">If the name of the `<Library>` element starts and ends with an asterisk (\*), the `<Library>` directive has an effect only if the assembly specified between the asterisks is referenced by the app.</span></span> <span data-ttu-id="52d07-142">例如，下列執行時間指示詞僅適用于應用程式參考的公用程式 .dll 元件。</span><span class="sxs-lookup"><span data-stu-id="52d07-142">For example, the following runtime directive applies only if the Utilities.dll assembly is referenced by the app.</span></span>  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Library Name="*Utilities*">  
   ...  
  </Library>  
</Directives>  
```  
  
## <a name="see-also"></a><span data-ttu-id="52d07-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="52d07-143">See also</span></span>

- [<span data-ttu-id="52d07-144">\<Application>元素</span><span class="sxs-lookup"><span data-stu-id="52d07-144">\<Application> Element</span></span>](application-element-net-native.md)
- [<span data-ttu-id="52d07-145">\<Directives>元素</span><span class="sxs-lookup"><span data-stu-id="52d07-145">\<Directives> Element</span></span>](directives-element-net-native.md)
- [<span data-ttu-id="52d07-146">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="52d07-146">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="52d07-147">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="52d07-147">Runtime Directive Elements</span></span>](runtime-directive-elements.md)

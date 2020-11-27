---
title: '<Application> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: b4e9b37a-059b-4076-8f56-cb3f9cef0cd9
ms.openlocfilehash: a7f2eca5a5bb5cfb7b9827f2463454a17fc128cb
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288134"
---
# <a name="application-element-net-native"></a>\<Application> 元素 ( .NET Native) 

做為容器，以包含整個應用程式中，可在執行階段將中繼資料用於反映的類型和類型成員，並將執行階段反映原則套用至應用程式中的所有程式元素。  
  
 \<Directives> 項目  
\<Application> 元素 ( # A0)   
  
## <a name="syntax"></a>Syntax  
  
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
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。 在「子元素」表格中，原則會指出可在執行階段供特定程式元素使用的中繼資料種類。  
  
### <a name="attributes"></a>屬性  
  
|屬性|屬性類型|描述|  
|---------------|--------------------|-----------------|  
|`Activate`|反射|選擇性屬性。 控制建構函式的執行階段存取，以便啟動執行個體。|  
|`Browse`|反射|選擇性屬性。 控制對類型相關資訊的查詢，或控制類型的列舉，但不會在執行階段啟用任何動態存取。|  
|`Dynamic`|反射|選擇性屬性。 控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。|  
|`Serialize`|序列化|選擇性屬性。 控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。|  
|`DataContractSerializer`|序列化|選用的屬性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。|  
|`DataContractJsonSerializer`|序列化|選用的屬性。 控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。|  
|`XmlSerializer`|序列化|選用的屬性。 控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。|  
|`MarshalObject`|Interop|選用的屬性。 控制 Windows 執行階段和 COM 之參考類型的封送處理原則。|  
|`MarshalDelegate`|Interop|選用的屬性。 控制將委派類型當作函式指標封送處理至機器碼的原則。|  
|`MarshalStructure`|Interop|選用的屬性。 控制將結構封送處理至機器碼的原則。|  
  
## <a name="all-attributes"></a>所有屬性  
  
|值|描述|  
|-----------|-----------------|  
|*policy_setting*|要讓這個原則在應用程式中套用至類型的設定。 可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。 如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|將原則套用至特定組件中的所有類型。|  
|[\<Namespace>](namespace-element-net-native.md)|將原則套用至特定命名空間中的所有類型。|  
|[\<Type>](type-element-net-native.md)|將原則套用至特定類型，例如類別或結構。|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|將原則套用至建構的泛型類型。 例如， [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 元素可用來定義類型的原則 `List<String>` 。|  
|[\<Method>](method-element-net-native.md)|將原則套用至特定類型上的方法。|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|將原則套用至建構的泛型方法。|  
|[\<Property>](property-element-net-native.md)|將原則套用至特定類型上的屬性。|  
|[\<Field>](field-element-net-native.md)|將原則套用至特定類型上的欄位。|  
|[\<Event>](event-element-net-native.md)|將原則套用至特定類型上的事件。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|執行階段指示詞檔案的根項目。|  
  
## <a name="remarks"></a>備註  

 [\<Directives>](directives-element-net-native.md)元素可以包含零個或一個 `<Application>` 元素。 不支援單一反映指示詞檔案中有多個 `<Application>` 元素。  
  
 `<Application>` 元素有兩種用法：  
  
- 做為容器，以定義在執行階段會需要其中繼資料的程式元素。 在此情況下，`<Application>` 元素不需要任何屬性。 在編譯時期，編譯器工具會在所有程式庫 (包括 .NET Framework 核心程式庫) 中，搜尋 `<Application>` 元素的子元素所識別的程式元素。 相反地，編譯器工具只會在專案所指定的程式庫中，搜尋的 [\<Library>](library-element-net-native.md) 子專案所識別的程式元素 [\<Library>](library-element-net-native.md) 。  
  
- 做為用來為反映、序列化和 interop 設定整個應用程式原則的元素。 專案的屬性 `<Application>` 會定義整個應用程式的原則，該原則可能會由或專案所定義的子項目覆寫 `<Application>` [\<Library>](library-element-net-native.md) 。  
  
## <a name="see-also"></a>另請參閱

- [\<Library> 元素](library-element-net-native.md)
- [\<Directives> 元素](directives-element-net-native.md)
- [執行階段指示詞項目](runtime-directive-elements.md)
- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)

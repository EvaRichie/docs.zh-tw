---
title: '<Parameter> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: 22aaa1f3-596f-4733-93db-f4bcabcb5240
ms.openlocfilehash: 7e812ab60eb0a89eb868346733a8ea74e2f76d3e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287861"
---
# <a name="parameter-element-net-native"></a>\<Parameter> 元素 ( .NET Native) 

將反映原則套用至傳遞給方法的引數類型。  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<Parameter Name="parameter_name"  
           Activate="policy_type"  
           Browse="policy_type"  
           Dynamic="policy_type"  
           Serialize="policy_type"  
           DataContractSerializer="policy_type"  
           DataContractJsonSerializer="policy_type"  
           XmlSerializer="policy_type"  
           MarshalObject="policy_type"  
           MarshalDelegate="policy_type"  
           MarshalStructure="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|屬性類型|描述|  
|---------------|--------------------|-----------------|  
|`Name`|一般|必要屬性。 參數名稱。 例如，對於方法簽章 `String.CompareTo(Object value)`而言，`Name` 屬性的值是 "value"。|  
|`Activate`|反射|選擇性屬性。 控制建構函式的執行階段存取，以便啟動執行個體。|  
|`Browse`|反射|選擇性屬性。 控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。|  
|`Dynamic`|反射|選擇性屬性。 控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。|  
|`Serialize`|序列化|選擇性屬性。 控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。|  
|`DataContractSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。|  
|`DataContractJsonSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。|  
|`XmlSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。|  
|`MarshalObject`|Interop|選擇性屬性。 控制將參考類型封送處理至 WinRT 及 COM 的原則。|  
|`MarshalDelegate`|Interop|選擇性屬性。 控制將委派類型當作函式指標封送處理至機器碼的原則。|  
|`MarshalStructure`|Interop|選擇性屬性。 控制將值類型封送處理為原生程式碼的原則。|  
  
## <a name="name-attribute"></a>Name 屬性  
  
|值|描述|  
|-----------|-----------------|  
|*parameter_name*|套用原則的方法參數名稱。 例如，對於方法簽章 `String.CompareTo(Object value)`而言，`Name` 屬性的值是 "value"。|  
  
## <a name="all-other-attributes"></a>所有其他屬性  
  
|值|描述|  
|-----------|-----------------|  
|*policy_setting*|要套用到此原則類型的設定。 可能的值為 `All`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。 如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Method>](method-element-net-native.md)|將執行階段反映原則套用到建構函式或方法。|  
  
## <a name="remarks"></a>備註  

 專案 `<Parameter>` 是專案的子系 [\<Method>](method-element-net-native.md) ，用來將原則套用至特定的方法參數。 特定的方法參數是依名稱指定，而不是依類型。 必須存在至少一個表示原則類型的屬性，例如 `Activate` 或 `Dynamic`。  
  
## <a name="see-also"></a>另請參閱

- [\<Method> 元素](method-element-net-native.md)
- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)
- [執行階段指示詞原則設定](runtime-directive-policy-settings.md)
- [執行階段指示詞項目](runtime-directive-elements.md)

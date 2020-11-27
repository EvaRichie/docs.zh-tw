---
title: '<TypeInstantiation> 元素 ( .NET Native) '
ms.date: 03/30/2017
ms.assetid: a5eada64-075b-4162-9655-ded84e4681f2
ms.openlocfilehash: a1db497762b3dc8c135154086d72fb3ac92ff5a4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250745"
---
# <a name="typeinstantiation-element-net-native"></a>\<TypeInstantiation> 元素 ( .NET Native) 

將執行階段反映原則套用至建構的泛型類型。  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<TypeInstantiation Name="type_name"  
                   Arguments="type_arguments"  
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
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|屬性類型|描述|  
|---------------|--------------------|-----------------|  
|`Name`|一般|必要屬性。 指定類型名稱。|  
|`Arguments`|一般|必要屬性。 指定泛型型別引數。 如果有多個引數存在，會以逗號分隔。|  
|`Activate`|反射|選擇性屬性。 控制建構函式的執行階段存取，以便啟動執行個體。|  
|`Browse`|反射|選擇性屬性。 控制程式項目相關資訊的查詢，但不會啟用任何執行階段存取。|  
|`Dynamic`|反射|選擇性屬性。 控制對所有類型成員 (包括建構函式、方法、欄位、屬性和事件) 的執行階段存取，以啟用動態程式設計。|  
|`Serialize`|序列化|選擇性屬性。 控制建構函式、欄位和屬性的執行階段存取，以便 Newtonsoft JSON 序列化程式等程式庫可對類型執行個體進行序列化和還原序列化。|  
|`DataContractSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 類別的序列化原則。|  
|`DataContractJsonSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 類別的 JSON 序列化原則。|  
|`XmlSerializer`|序列化|選擇性屬性。 控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 類別的 XML 序列化原則。|  
|`MarshalObject`|Interop|選擇性屬性。 控制 Windows 執行階段和 COM 之參考類型的封送處理原則。|  
|`MarshalDelegate`|Interop|選擇性屬性。 控制將委派類型當作函式指標封送處理至機器碼的原則。|  
|`MarshalStructure`|Interop|選擇性屬性。 控制將結構封送處理至機器碼的原則。|  
  
## <a name="name-attribute"></a>Name 屬性  
  
|值|描述|  
|-----------|-----------------|  
|*type_name*|類型名稱。 如果這個 `<TypeInstantiation>` 元素是 [\<Namespace>](namespace-element-net-native.md) 元素、 [\<Type>](type-element-net-native.md) 元素或另一個元素的子系 `<TypeInstantiation>` ， *type_name* 可以指定類型的名稱，而不包含其命名空間。 否則，*type_name* 必須包含完整的類型名稱。 不裝飾類型名稱。 例如，針對 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 物件，`<TypeInstantiation>` 元素可能會像下面這樣：<br /><br /> `\<TypeInstantiation Name=System.Collections.Generic.List Dynamic="Required Public" />`|  
  
## <a name="arguments-attribute"></a>引數屬性  
  
|值|描述|  
|-----------|-----------------|  
|*type_argument*|指定泛型型別引數。 如果有多個引數存在，會以逗號分隔。 每個引數都必須包含完整的類型名稱。|  
  
## <a name="all-other-attributes"></a>所有其他屬性  
  
|值|描述|  
|-----------|-----------------|  
|*policy_setting*|要為建構的泛型類型套用至此原則類型的設定。 可能的值為 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 和 `Required All`。 如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Event>](event-element-net-native.md)|將反映原則套用至屬於此類型的事件。|  
|[\<Field>](field-element-net-native.md)|將反映原則套用至屬於此類型的欄位。|  
|[\<ImpliesType>](impliestype-element-net-native.md)|如果原則已套用至包含 `<TypeInstantiation>` 元素所表示的類型，則會將該原則套用至類型。|  
|[\<Method>](method-element-net-native.md)|將反映原則套用至屬於此類型的方法。|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|將反映原則套用至屬於此類型的建構泛型方法。|  
|[\<Property>](property-element-net-native.md)|將反映原則套用至屬於此類型的屬性。|  
|[\<Type>](type-element-net-native.md)|將反映原則套用至巢狀類型。|  
|`<TypeInstantiation>`|將反映原則套用至巢狀建構的泛型類型。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|做為容器，以包含整個應用程式的類型，以及中繼資料可在執行階段用於反映的類型成員。|  
|[\<Assembly>](assembly-element-net-native.md)|將反映原則套用至指定組件中的所有類型。|  
|[\<Library>](library-element-net-native.md)|定義包含類型和類型成員的組件，這些類型和類型成員的中繼資料可在執行階段用於反映。|  
|[\<Namespace>](namespace-element-net-native.md)|將反映原則套用至命名空間中的所有類型。|  
|[\<Type>](type-element-net-native.md)|將反映原則套用至類型及其所有成員。|  
|`<TypeInstantiation>`|將反映原則套用至建構泛型類型及其所有成員。|  
  
## <a name="remarks"></a>備註  

 反映、序列化和 interop 屬性都是選用性。 不過，必須至少有一個屬性存在。  
  
 如果 `<TypeInstantiation>` 元素是、或專案的子 [\<Assembly>](assembly-element-net-native.md) 系 [\<Namespace>](namespace-element-net-native.md) [\<Type>](type-element-net-native.md) ，它會覆寫父元素所定義的原則設定。 如果專案 [\<Type>](type-element-net-native.md) 定義對應的泛型型別定義，則 `<TypeInstantiation>` 元素只會針對指定之結構化泛型型別的具現化覆寫執行時間反映原則。  
  
## <a name="example"></a>範例  

 下列範例會使用反映，從建構的 <xref:System.Collections.Generic.Dictionary%602> 物件擷取泛型類型定義。 它也會使用反映來顯示代表建構泛型類型和泛型類型定義的 <xref:System.Type> 物件。 `b`範例中的變數為 <xref:Windows.UI.Xaml.Controls.TextBlock> 控制項。  
  
 [!code-csharp[ProjectN_Reflection#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/makegenerictype1.cs#2)]  
  
 使用 .NET Native 工具鏈編譯之後，此範例會在呼叫<xref:System.Type.GetGenericTypeDefinition%2A?displayProperty=nameWithType>方法的程式列上擲回 [MissingMetadataException](missingmetadataexception-class-net-native.md) 例外狀況。 若要消除此例外狀況，並提供必要的中繼資料，您可以將下列 `<TypeInstantiation>` 元素加入至執行階段指示詞檔案：  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
     <TypeInstantiation Name="System.Collections.Generic.Dictionary"  
                        Arguments="System.String,GenericType.Example"  
                        Dynamic="Required Public" />  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)
- [執行階段指示詞項目](runtime-directive-elements.md)
- [執行階段指示詞原則設定](runtime-directive-policy-settings.md)

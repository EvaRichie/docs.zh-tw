---
title: <Method>元素（.NET Native）
ms.date: 03/30/2017
ms.assetid: 348b49e5-589d-4eb2-a597-d6ff60ab52d1
ms.openlocfilehash: 8db32c660846b4f4071fff2a40c760a3d1ef2489
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79180980"
---
# <a name="method-element-net-native"></a>\<Method>元素（.NET Native）
將執行階段反映原則套用到建構函式或方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
<Method Name="method_name"  
        Signature="method_signature"  
        Browse="policy_type"  
        Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|屬性類型|描述|  
|---------------|--------------------|-----------------|  
|`Name`|一般|必要屬性。 指定方法名稱。|  
|`Signature`|一般|選擇性屬性。 指定方法簽章。 如果有多個參數存在，會以逗號分隔。 例如，下列 `<Method>` 元素會定義 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29> 方法的原則。<br /><br /> `<Type Name="System.DateTime">    <Method Name="ToString" Signature="System.String,System.IFormatProvider"            Dynamic="Required" /> </Type>`<br /><br /> 如果屬性不存在，執行階段指示詞會套用到方法的所有多載。|  
|`Browse`|反射|選擇性屬性。 控制對方法相關資訊的查詢，或控制方法的列舉，但不會在執行階段啟用任何動態引動過程。|  
|`Dynamic`|反射|選擇性屬性。 控制對建構函式或方法的執行階段存取權，以啟用動態程式設計。 此原則確保能夠在執行階段動態叫用成員。|  
  
## <a name="name-attribute"></a>Name 屬性  
  
|值|說明|  
|-----------|-----------------|  
|*method_name*|方法名稱。 方法的類型是由父系或元素所定義 [\<Type>](type-element-net-native.md) [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。|  
  
## <a name="signature-attribute"></a>簽章屬性  
  
|值|說明|  
|-----------|-----------------|  
|*method_signature*|構成方法簽章的參數類型。 若有多個參數，會以逗號分隔，例如，`"System.String,System.Int32,System.Int32)"`。 參數類型名稱應該是完整名稱。|  
  
## <a name="all-other-attributes"></a>所有其他屬性  
  
|值|說明|  
|-----------|-----------------|  
|*policy_setting*|要套用到此原則類型的設定。 可能的值為 `Auto`、`Excluded`、`Included` 和 `Required`。 如需詳細資訊，請參閱[執行階段指示詞原則設定](runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Parameter>](parameter-element-net-native.md)|將原則套用到傳遞至方法的引數類型。|  
|[\<GenericParameter>](genericparameter-element-net-native.md)|將原則套用到泛型類型或方法的參數類型。|  
|[\<ImpliesType>](impliestype-element-net-native.md)|如果原則已套用至包含 `<Method>` 元素所表示的方法，則會將該原則套用至類型。|  
|[\<TypeParameter>](typeparameter-element-net-native.md)|將原則套用至傳遞給方法之 <xref:System.Type> 引數所表示的類型。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|將反映原則套用至類型及其所有成員。|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|將反映原則套用至建構泛型類型及其所有成員。|  
  
## <a name="remarks"></a>備註  
 泛型方法的 `<Method>` 的元素會將其原則套用至沒有自己原則的所有具現化。  
  
 您可以使用 `Signature` 屬性來指定適用於特定方法多載的原則。 否則，如果 `Signature` 屬性不存在，執行階段指示詞就會套用到方法的所有多載。  
  
 您不能使用 `<Method>` 元素來為建構函式定義執行階段反映原則， 請改用 `Activate` [\<Assembly>](assembly-element-net-native.md) 、 [\<Namespace>](namespace-element-net-native.md) 、 [\<Type>](type-element-net-native.md) 或元素的屬性 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
## <a name="example"></a>範例  
 下列範例中的 `Stringify` 方法是一般用途的格式化方法，它會使用反映將物件轉換成其字串表示法。 除了呼叫物件的預設 `ToString` 方法，此方法還可以將格式字串及/或 `ToString` 實作傳遞給物件的 <xref:System.IFormatProvider> 方法，以產生格式化的結果字串。 它也可以呼叫其中一個 <xref:System.Convert.ToString%2A?displayProperty=nameWithType> 多載，將數字轉換成二進位、十六進位或八進位表示法。  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 您可以用類似下列程式碼來呼叫 `Stringify` 方法：  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 不過，以 .NET Native 來編譯時，此範例可能會在執行階段擲回一些例外狀況，包括 <xref:System.NullReferenceException> 和 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外狀況。這是因為 `Stringify` 方法主要的目的是支援將 .NET Framework Class Library 中的基本類型動態格式化。 不過，預設指示詞檔案並沒有提供其中繼資料。 但是，即使其中繼資料可供使用，範例還是會擲回 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外狀況，因為適當的 `ToString` 實作尚未包含在機器碼中。  
  
 這些例外狀況全都可以透過使用專案 [\<Type>](type-element-net-native.md) 來定義中繼資料必須存在的類型，以及藉由加入 `<Method>` 元素以確保可動態呼叫的方法多載也存在，藉此消除。 以下是可消除這些例外狀況，並可讓範例執行而不會發生錯誤的 default.rd.xml 檔案。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
     <Assembly Name="*Application*" Dynamic="Required All" />  
  
     <Type Name = "System.Convert" Browse="Required Public" Dynamic="Required Public" >  
        <Method Name="ToString"    Dynamic ="Required" />  
     </Type>  
     <Type Name="System.Double" Browse="Required Public">  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int32" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int64" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Namespace Name="System" >  
        <Type Name="Byte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="DateTime" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Decimal" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Guid" Browse ="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Int16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="SByte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Single" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />
        </Type>  
        <Type Name="TimeSpan" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />
        </Type>  
        <Type Name="UInt16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt32" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt64" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
     </Namespace>  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)
- [執行階段指示詞項目](runtime-directive-elements.md)
- [執行階段指示詞原則設定](runtime-directive-policy-settings.md)
- [\<MethodInstantiation>元素](methodinstantiation-element-net-native.md)

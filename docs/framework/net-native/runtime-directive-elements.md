---
title: 執行階段指示詞項目
ms.date: 03/30/2017
ms.assetid: 3fe5848c-ecd7-4136-970b-8e48d250bde6
ms.openlocfilehash: c900516382c8e526a6b0021bb2b681486283f3ab
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128176"
---
# <a name="runtime-directive-elements"></a>執行階段指示詞項目
執行階段指示詞 (rd.xml) 檔案格式支援下列執行階段指示詞元素。 如需階層表示法，請參閱[執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)。  
  
 [\<Application>](application-element-net-native.md)  
 將執行階段反映原則套用至應用程式使用的所有類型，並做為整個應用程式的類型和類型成員的容器，這些類型和類型成員的中繼資料可在執行階段用於反映。 這是元素的子系 [\<Directives>](directives-element-net-native.md) 。  
  
 [\<Assembly>](assembly-element-net-native.md)  
 將執行階段原則套用至組件中的所有類型。 這是和元素的子 [\<Application>](application-element-net-native.md) 系 [\<Library>](library-element-net-native.md) 。  
  
 [\<AttributeImplies>](attributeimplies-element-net-native.md)  
 如果其包含 [\<Type>](type-element-net-native.md) 的指示詞是屬性，則會將執行時間原則套用至套用該屬性的程式碼元素。  
  
 [\<Directives>](directives-element-net-native.md)  
 .NET Native 的每個執行時間指示詞檔案中的根項目。 其子項目為 [\<Application>](application-element-net-native.md) 和 [\<Library>](library-element-net-native.md) 。  
  
 [\<Event>](event-element-net-native.md)  
 將執行階段原則套用至事件。 這是和元素的子 [\<Type>](type-element-net-native.md) 系 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
 [\<Field>](field-element-net-native.md)  
 將執行階段原則套用至欄位。 這是和元素的子 [\<Type>](type-element-net-native.md) 系 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
 [\<GenericParameter>](genericparameter-element-net-native.md)  
 將執行階段原則套用至泛型類型或方法的參數類型。  
  
 [\<ImpliesType>](impliestype-element-net-native.md)  
 如果執行階段原則已套用至包含類型或方法，則會將該原則套用至類型。  
  
 [\<Library>](library-element-net-native.md)  
 將執行階段原則套用至組件中的所有類型。 這是和元素的子 [\<Application>](application-element-net-native.md) 系 [\<Library>](library-element-net-native.md) 。  
  
 [\<Method>](method-element-net-native.md)  
 將執行階段原則套用至方法。 這是和元素的子 [\<Type>](type-element-net-native.md) 系 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
 [\<MethodInstantiation>](methodinstantiation-element-net-native.md)  
 將執行階段原則套用至建構的泛型方法。 這是和元素的子 [\<Type>](type-element-net-native.md) 系 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
 [\<Namespace>](namespace-element-net-native.md)  
 將執行階段原則套用至命名空間中的所有類型。  
  
 [\<Parameter>](parameter-element-net-native.md)  
 將執行階段原則套用至傳遞給方法的引數類型。  
  
 [\<Property>](property-element-net-native.md)  
 將執行階段原則套用至屬性。 這是和元素的子 [\<Type>](type-element-net-native.md) 系 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 。  
  
 [\<Subtypes>](subtypes-element-net-native.md)  
 將執行階段原則套用至從包含類型繼承的所有類別。  
  
 [\<Type>](type-element-net-native.md)  
 將執行階段原則套用至類型。  
  
 [\<TypeInstantiation>](typeinstantiation-element-net-native.md)  
 將執行階段原則套用至建構的泛型類型。  
  
 [\<TypeParameter>](typeparameter-element-net-native.md)  
 將執行階段原則套用至傳遞給方法之 <xref:System.Type> 引數所表示的類型。  
  
## <a name="see-also"></a>另請參閱

- [rd.xml 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)

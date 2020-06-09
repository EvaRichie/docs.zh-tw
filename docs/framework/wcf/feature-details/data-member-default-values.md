---
title: 資料成員預設值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data members [WCF], default values
- data members [WCF]
ms.assetid: 53a3b505-4b27-444b-b079-0eb84a97cfd8
ms.openlocfilehash: e4eaaec880ecfcff24d9d5b4e8347a84738e070b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593473"
---
# <a name="data-member-default-values"></a>資料成員預設值
在 .NET Framework 中，類型具有*預設值*的概念。 例如，任何參考型別的預設值為 `null`，整數型別則為零。 有時候資料成員設為預設值時，會需要從序列化資料中省略該成員。 因為此成員為預設值，而實際值不需要序列化，因此這樣做可促進效能。  
  
 若要省略序列化資料中的成員，請將 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 屬性 (Attribute) 的 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Property) 設為 `false` (預設值為 `true`)。  
  
> [!NOTE]
> 您應該在有特殊需要時，將 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 屬性設定為 `false`，例如為了互通性或縮減資料大小。  
  
## <a name="example"></a>範例  
 以下程式碼中有數個成員的 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 都設為 `false`。  
  
 [!code-csharp[DataMemberAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datamemberattribute/cs/overview.cs#4)]
 [!code-vb[DataMemberAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datamemberattribute/vb/overview.vb#4)]  
  
 如果這個類別的執行個體已序列化，則結果可能如下：`employeeName` 和 `employeeID` 將會序列化。 `employeeName` 的 null 值和 `employeeID` 的零值將明確成為序列化資料的一部分。 不過，`position`、`salary` 和 `bonus` 成員都不會序列化。 最後，即使 `targetSalary` 屬性設為 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>，`false` 通常仍會序列化，因為 57800 不符合 .NET 預設的整數值，也就是零。  
  
### <a name="xml-representation"></a>XML 表示  
 如果之前的範例已序列化為 XML，則表示方式將類似以下內容：  
  
```xml  
<Employee>  
   <employeeName xsi:nil="true" />  
   <employeeID>0</employeeID>  
<targetSalary>57800</targetSalary>  
</Employee>  
```  
  
 `xsi:nil` 屬性 (Attribute) 是全球資訊網協會 (W3C) XML 結構描述執行個體命名空間中的特殊屬性，會提供可互通的方式明確表示 null 值。 請注意，XML 中沒有任何關於職位、薪資及獎金資料成員的資訊。 接收端可以分別將這些成員解譯為 `null`、零和 `null`。 不過不保證協力廠商的還原序列化程式能夠正確解譯，這也是不建議使用此模式的原因。 <xref:System.Runtime.Serialization.DataContractSerializer> 類別永遠會為遺漏的值選取正確解譯。  
  
### <a name="interaction-with-isrequired"></a>與 IsRequired 互動  
 如[資料合約版本控制](data-contract-versioning.md)中所討論， <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性具有 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 屬性（預設為 `false` ）。 這個屬性會表示還原序列化指定的資料成員時，是否必須以序列化的資料表示該成員。 如果 `IsRequired` 設為 `true` (表示一定要使用一個值)，且 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 設為 `false` (表示如果使用預設值，則不需要使用該值)，因為結果會互相矛盾，所以無法序列化此資料成員的預設值。 如果這類資料成員設為其預設值 (通常為 `null` 或零)，並且嘗試進行序列化，則會擲回 <xref:System.Runtime.Serialization.SerializationException>。  
  
### <a name="schema-representation"></a>結構描述表示  
 當屬性設定為時，資料成員之 XML 架構定義語言（XSD）架構表示的詳細資訊 `EmitDefaultValue` `false` 會在[資料合約架構參考](data-contract-schema-reference.md)中討論。 不過，以下提供簡要的概觀。  
  
- 當 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 設定為時 `false` ，它會在架構中表示為 WINDOWS COMMUNICATION FOUNDATION （WCF）特定的批註。 目前沒有可互通的方式能表示這項資訊。 特別是結構描述中的 "default" 屬性 (Attribute) 不是用於此目的時，`minOccurs` 屬性只會受到 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 設定的影響，而 `nillable` 屬性只會受到資料成員的型別影響。  
  
- 實際使用的預設值不會在結構描述中表示。 端看接收端點如何適當地解譯遺失的項目而定。  
  
 在架構匯入時， <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> `false` 每次偵測到先前所述的 WCF 特定注釋時，屬性都會自動設定為。 針對將屬性設定為的參考型別，它也會設定為 `false` `nillable` `false` ，以支援在使用 ASP.NET Web 服務時通常會發生的特定互通性案例。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute>

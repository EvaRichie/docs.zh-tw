---
title: 變更命名空間前置詞屬性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d5c87cbe-4d69-429f-aad5-3103c2ca2770
ms.openlocfilehash: a4ba378620d0c5ec01aaa5d87020c33fdbffcf01
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725348"
---
# <a name="changing-namespace-prefix-properties"></a>變更命名空間前置詞屬性

**XmlNode** 類別可以讓您變更與指定之節點關聯的命名空間前置詞。 例如，下列程式碼顯示要變更之項目的前置詞。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "b"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "b";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **輸出**  
  
```xml  
<b:test xmlns:a="123" xmlns:b="456" />  
```  
  
 變更節點的前置詞並不會變更其命名空間。 只有在節點建立時才能設定命名空間。 當您保留樹狀時，新命名空間屬性會保留以滿足您所設定的前置詞。 如果無法建立新的命名空間，則前置詞會變更，如此節點會保留它的區域名稱和命名空間。 下列範例顯示要加入的命名空間屬性。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<test xmlns='123'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "a"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<test xmlns='123'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "a";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **輸出**  
  
```xml  
<a:test xmlns="123" xmlns:a="123" />  
```  
  
 樹狀結構保留於字串做為 **doc.InnerXml** 的呼叫結果時，會加入 `xmlns:a='123'` 屬性以保留 `test` 項目的命名空間。 它原本是 `'123'`，且仍保留為 `'123'`。  
  
## <a name="see-also"></a>另請參閱

- [XML 文件物件模型 (DOM)](xml-document-object-model-dom.md)

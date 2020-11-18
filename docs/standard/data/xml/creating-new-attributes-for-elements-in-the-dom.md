---
title: 為 DOM 中的項目建立新屬性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
ms.openlocfilehash: 1cb37e47bedf955ea2c6f9faad628df2175fb703
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826023"
---
# <a name="creating-new-attributes-for-elements-in-the-dom"></a>為 DOM 中的項目建立新屬性

建立新屬性不同於建立其他的節點型別，因為屬性不是節點，而是項目節點的屬性且包含於與項目相關的 **XmlAttributeCollection** 中。 有許多方法可以建立屬性並且將它附加於項目：

- 取得項目節點並且使用 **SetAttribute** 將屬性加入此項目的屬性集合。

- 使用 **CreateAttribute** 方法建立 **XmlAttribute** 節點，取得項目節點，然後使用 **SetAttributeNode** 將節點加入此項目的屬性集合。

下列範例示範如何使用 **SetAttribute** 方法，將屬性新增至元素：

```vb
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()

        Dim doc As New XmlDocument()
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _
                    "<title>Pride And Prejudice</title>" & _
                    "</book>")
        Dim root As XmlElement = doc.DocumentElement

        ' Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel")

        Console.WriteLine("Display the modified XML...")
        Console.WriteLine(doc.InnerXml)
    End Sub
End Class
```  
  
```csharp
using System;
using System.IO;
using System.Xml;

public class Sample
{
    public static void Main()
    {
        var doc = new XmlDocument();
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +
                    "<title>Pride And Prejudice</title>" +
                    "</book>");
        XmlElement root = doc.DocumentElement;

        // Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel");

        Console.WriteLine("Display the modified XML...");
        Console.WriteLine(doc.InnerXml);
    }
}
```

下列範例顯示使用 **CreateAttribute** 方法建立的新屬性。 接著它使用 **SetAttributeNode** 方法，顯示加入 **book** 項目之屬性集合的屬性。

假設有下列的 XML：
  
```xml
<book genre='novel' ISBN='1-861001-57-5'>
<title>Pride And Prejudice</title>
</book>
```

建立新屬性並指定其值：

```vb
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")
attr.Value = "WorldWide Publishing"
```

```csharp
XmlAttribute attr = doc.CreateAttribute("publisher");
attr.Value = "WorldWide Publishing";
```

將它附加於項目：

```vb
doc.DocumentElement.SetAttributeNode(attr)
```

```csharp
doc.DocumentElement.SetAttributeNode(attr);
```

**輸出**

```xml
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">
<title>Pride And Prejudice</title>
</book>
```

如需完整的程式碼範例，請參閱 <xref:System.Xml.XmlDocument.CreateAttribute%2A>。

您也可以建立 **XmlAttribute** 節點並且使用 **InsertBefore** 或 **InsertAfter** 方法將它置於集合的適當位置中。 如果屬性集合中已經有相同名稱的屬性存在，那麼現有的 **XmlAttribute** 節點會從集合中移除，而且新 **XmlAttribute** 節點會插入。 執行方法與 **SetAttribute** 方法相同。 如同參數，這些方法會以現有節點作為參考點來執行 **InsertBefore** 與 **InsertAfter**。 若未提供可指出要在何處插入新節點的參考節點，根據預設，**InsertAfter** 方法會將新節點插入集合的開頭。 若未提供參考節點，根據預設，**InsertBefore** 的位置將是在集合的結尾。

如果您已建立屬性的 **XmlNamedNodeMap** ，您可以使用方法，依名稱加入屬性 <xref:System.Xml.XmlNamedNodeMap.SetNamedItem%2A> 。 如需詳細資訊，請參閱 [NamedNodeMap 和 NodeList 中的節點集合](node-collections-in-namednodemaps-and-nodelists.md)。

## <a name="default-attributes"></a>預設屬性

如果您建立了宣告要有預設屬性的項目，那麼具有預設值的新預設屬性會由 XML 文件物件模型 (DOM) 建立並且附加於項目。 預設屬性的子節點也會在此時建立。

## <a name="attribute-child-nodes"></a>屬性子節點

屬性節點的值會成為它的子節點。 有效的子節點只有兩種類型： **XmlText** 節點和 **XmlEntityReference** 節點。 這些子節點讓像 **FirstChild** 和 **LastChild** 的方法能夠將它們當成子節點處理。 這種擁有子節點的屬性的區別在嘗試移除屬性或屬性子節點時很重要。 如需詳細資訊，請參閱[移除 DOM 中項目節點的屬性](removing-attributes-from-an-element-node-in-the-dom.md)。

## <a name="see-also"></a>請參閱

- [XML 文件物件模型 (DOM)](xml-document-object-model-dom.md)

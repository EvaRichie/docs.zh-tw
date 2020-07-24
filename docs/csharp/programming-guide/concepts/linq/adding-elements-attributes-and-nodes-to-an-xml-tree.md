---
title: 將項目、屬性和節點新增至 XML 樹狀結構 (C#)
description: 瞭解將元素、屬性、批註、處理指示和文字等內容新增至現有 XML 樹狀結構的方法。
ms.date: 07/20/2015
ms.assetid: db911e4f-40aa-499a-9500-a9763bb6df56
ms.openlocfilehash: 78a84401494e2d4280799632fa42dc95574e3e10
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105556"
---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-c"></a>將項目、屬性和節點新增至 XML 樹狀結構 (C#)
您可以將內容 (項目、屬性、註解、處理指示、文字和 CDATA) 加入到現有的 XML 樹狀結構中。  
  
## <a name="methods-for-adding-content"></a>加入內容的方法  
 下列方法會將子內容加入到 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument>：  
  
|方法|說明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|將內容加入到 <xref:System.Xml.Linq.XContainer> 之子內容的結尾。|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|將內容加入到 <xref:System.Xml.Linq.XContainer> 之子內容的開頭。|  
  
 下列方法會加入內容，做為 <xref:System.Xml.Linq.XNode> 的同層級節點。 雖然您可以將有效的同層級內容加入到節點的其他型別 (例如，<xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XText>)，但是您加入同層級內容的最常見目標節點為 <xref:System.Xml.Linq.XComment>。  
  
|方法|說明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|將內容加入到 <xref:System.Xml.Linq.XNode> 之後。|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|將內容加入到 <xref:System.Xml.Linq.XNode> 之前。|  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會建立兩個 XML 樹狀結構，然後修改其中一個樹狀結構。  
  
### <a name="code"></a>程式碼  
  
```csharp  
XElement srcTree = new XElement("Root",
    new XElement("Element1", 1),  
    new XElement("Element2", 2),  
    new XElement("Element3", 3),  
    new XElement("Element4", 4),  
    new XElement("Element5", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child1", 1),  
    new XElement("Child2", 2),  
    new XElement("Child3", 3),  
    new XElement("Child4", 4),  
    new XElement("Child5", 5)  
);  
xmlTree.Add(new XElement("NewChild", "new content"));  
xmlTree.Add(  
    from el in srcTree.Elements()  
    where (int)el > 3  
    select el  
);  
// Even though Child9 does not exist in srcTree, the following statement will not  
// throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"));  
Console.WriteLine(xmlTree);  
```  
  
### <a name="comments"></a>註解  
 此程式碼會產生下列輸出：  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
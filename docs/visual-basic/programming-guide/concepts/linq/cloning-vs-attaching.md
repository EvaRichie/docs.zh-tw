---
title: 複製與正在附加
ms.date: 07/20/2015
ms.assetid: 3c3bd105-c9d3-49bd-875b-27ab4e8bc7a3
ms.openlocfilehash: aaf3344c0439d96a01006ee000d0a827884a5af9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410873"
---
# <a name="cloning-vs-attaching-visual-basic"></a>複製與附加（Visual Basic）
將 <xref:System.Xml.Linq.XNode> (包括 <xref:System.Xml.Linq.XElement>) 或 <xref:System.Xml.Linq.XAttribute> 物件加入到新的樹狀結構時，如果新內容沒有父代，這些物件只會附加到 XML 樹狀結構。 如果新內容已經成為父代，而且屬於其他 XML 樹狀結構的一部分，則會複製新內容。 然後，新複製的內容會附加到新的 XML 樹狀結構。  
  
## <a name="example"></a>範例  
 下列程式碼示範將成為父代的項目加入到樹狀結構時，以及將沒有父代的項目加入樹狀結構時的行為。  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 這個範例會產生下列輸出：  
  
```console  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>另請參閱

- [建立 XML 樹狀結構（Visual Basic）](creating-xml-trees.md)

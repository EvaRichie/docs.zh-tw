---
title: '如何尋找緊接在的先前的兄弟（XPath-LINQ to XML）（c #）'
description: '這個 c # 範例會比較 XPath 與 LINQ to XML，以瞭解如何尋找緊接在節點前面的兄弟。'
ms.date: 07/20/2015
ms.assetid: 74c06201-0b1b-4b5e-b3ac-0092980614e6
ms.openlocfilehash: eaee7f1205ce0d0b2a9c2c41d96ba532573a1384
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105204"
---
# <a name="how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml-c"></a>如何尋找緊接在的先前的兄弟（XPath-LINQ to XML）（c #）
有時候您會想要尋找節點正前面的同層級。 由於前面同層級座標軸的位置性述詞語意 (Semantics) 在 XPath 中與 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 相反的這個差異，這是其中一個更有趣的比較。  
  
## <a name="example"></a>範例  
 在這個範例中，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢會使用 <xref:System.Linq.Enumerable.Last%2A> 運算子，尋找集合中由 <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A> 傳回的最後一個節點。 相較之下，XPath 運算式會使用述詞搭配 1 這個值來尋找正前面的項目。  
  
```csharp  
XElement root = XElement.Parse(  
    @"<Root>  
    <Child1/>  
    <Child2/>  
    <Child3/>  
    <Child4/>  
</Root>");  
XElement child4 = root.Element("Child4");  
  
// LINQ to XML query  
XElement el1 =  
    child4  
    .ElementsBeforeSelf()  
    .Last();  
  
// XPath expression  
XElement el2 =  
    ((IEnumerable)child4  
                 .XPathEvaluate("preceding-sibling::*[1]"))  
                 .Cast<XElement>()  
                 .First();  
  
if (el1 == el2)  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
Console.WriteLine(el1);  
```  
  
 這個範例會產生下列輸出：  
  
```output  
Results are identical  
<Child3 />  
```  

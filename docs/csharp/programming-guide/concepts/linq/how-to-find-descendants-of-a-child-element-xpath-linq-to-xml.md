---
title: '如何尋找子專案的子代（XPath-LINQ to XML）（c #）'
description: 瞭解如何使用 XPath 運算式，尋找具有特定名稱之子專案的子代元素。
ms.date: 07/20/2015
ms.assetid: 505b7512-bb8b-4f85-abbf-491f039c961e
ms.openlocfilehash: b8e110abc2e0df99c3fdf6d2846c7cbbc4736c1a
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303253"
---
# <a name="how-to-find-descendants-of-a-child-element-xpath-linq-to-xml-c"></a>如何尋找子專案的子代（XPath-LINQ to XML）（c #）
本主題顯示如何利用特定名稱取得子項目的子代項目。  
  
 XPath 運算式為：  
  
 `./Paragraph//Text/text()`  
  
## <a name="example"></a>範例  
 此範例模擬從字組處理文件的 XML 表示擷取文字的問題。 它會先選取所有 `Paragraph` 項目，然後它會選取每個 `Text` 項目的所有 `Paragraph` 子代項目。 這不會選取 `Text` 項目的子代 `Comment` 項目。  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root>  
  <Paragraph>  
    <Text>This is the start of</Text>  
  </Paragraph>  
  <Comment>  
    <Text>This comment is not part of the paragraph text.</Text>  
  </Comment>  
  <Paragraph>  
    <Annotation Emphasis='true'>  
      <Text> a sentence.</Text>  
    </Annotation>  
  </Paragraph>  
  <Paragraph>  
    <Text>  This is a second sentence.</Text>  
  </Paragraph>  
</Root>");  
  
// LINQ to XML query  
string str1 =  
    root  
    .Elements("Paragraph")  
    .Descendants("Text")  
    .Select(s => s.Value)  
    .Aggregate(  
        new StringBuilder(),  
        (s, i) => s.Append(i),  
        s => s.ToString()  
    );  
  
// XPath expression  
string str2 =  
    ((IEnumerable)root.XPathEvaluate("./Paragraph//Text/text()"))  
    .Cast<XText>()  
    .Select(s => s.Value)  
    .Aggregate(  
        new StringBuilder(),  
        (s, i) => s.Append(i),  
        s => s.ToString()  
    );  
  
if (str1 == str2)  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
Console.WriteLine(str2);  
```  
  
 這個範例會產生下列輸出：  
  
```output  
Results are identical  
This is the start of a sentence.  This is a second sentence.  
```  
  
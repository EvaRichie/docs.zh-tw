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
# <a name="how-to-find-descendants-of-a-child-element-xpath-linq-to-xml-c"></a><span data-ttu-id="dade3-103">如何尋找子專案的子代（XPath-LINQ to XML）（c #）</span><span class="sxs-lookup"><span data-stu-id="dade3-103">How to find descendants of a child element (XPath-LINQ to XML) (C#)</span></span>
<span data-ttu-id="dade3-104">本主題顯示如何利用特定名稱取得子項目的子代項目。</span><span class="sxs-lookup"><span data-stu-id="dade3-104">This topic shows how to get the descendant elements of a child element with a particular name.</span></span>  
  
 <span data-ttu-id="dade3-105">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="dade3-105">The XPath expression is:</span></span>  
  
 `./Paragraph//Text/text()`  
  
## <a name="example"></a><span data-ttu-id="dade3-106">範例</span><span class="sxs-lookup"><span data-stu-id="dade3-106">Example</span></span>  
 <span data-ttu-id="dade3-107">此範例模擬從字組處理文件的 XML 表示擷取文字的問題。</span><span class="sxs-lookup"><span data-stu-id="dade3-107">This example simulates the problems of extracting text from an XML representation of a word processing document.</span></span> <span data-ttu-id="dade3-108">它會先選取所有 `Paragraph` 項目，然後它會選取每個 `Text` 項目的所有 `Paragraph` 子代項目。</span><span class="sxs-lookup"><span data-stu-id="dade3-108">It first selects all `Paragraph` elements, and then it selects all `Text` descendant elements of each `Paragraph` element.</span></span> <span data-ttu-id="dade3-109">這不會選取 `Text` 項目的子代 `Comment` 項目。</span><span class="sxs-lookup"><span data-stu-id="dade3-109">This doesn't select the descendant `Text` elements of the `Comment` element.</span></span>  
  
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
  
 <span data-ttu-id="dade3-110">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="dade3-110">This example produces the following output:</span></span>  
  
```output  
Results are identical  
This is the start of a sentence.  This is a second sentence.  
```  
  
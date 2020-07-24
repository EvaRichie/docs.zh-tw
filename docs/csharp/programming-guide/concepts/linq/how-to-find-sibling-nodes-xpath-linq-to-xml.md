---
title: '如何尋找同輩節點（XPath-LINQ to XML）（c #）'
description: '這個 c # 範例會比較 XPath 與 LINQ to XML，以瞭解如何尋找具有特定名稱之節點的所有同輩。'
ms.date: 07/20/2015
ms.assetid: e2c73d10-a8ca-4e11-b5aa-d055de285874
ms.openlocfilehash: 2936fc4ad088580a9644f79f1797e679fe877e00
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105219"
---
# <a name="how-to-find-sibling-nodes-xpath-linq-to-xml-c"></a><span data-ttu-id="0a707-103">如何尋找同輩節點（XPath-LINQ to XML）（c #）</span><span class="sxs-lookup"><span data-stu-id="0a707-103">How to find sibling nodes (XPath-LINQ to XML) (C#)</span></span>
<span data-ttu-id="0a707-104">您可能想要尋找具有特定名稱之節點的所有同層級。</span><span class="sxs-lookup"><span data-stu-id="0a707-104">You might want to find all siblings of a node that have a specific name.</span></span> <span data-ttu-id="0a707-105">如果內容節點也有特定的名稱，所產生的集合可能包含內容節點。</span><span class="sxs-lookup"><span data-stu-id="0a707-105">The resulting collection might include the context node if the context node also has the specific name.</span></span>  
  
 <span data-ttu-id="0a707-106">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="0a707-106">The XPath expression is:</span></span>  
  
 `../Book`  
  
## <a name="example"></a><span data-ttu-id="0a707-107">範例</span><span class="sxs-lookup"><span data-stu-id="0a707-107">Example</span></span>  
 <span data-ttu-id="0a707-108">此範例會先尋找 `Book` 項目，然後尋找名稱為 `Book` 的所有同層級項目。</span><span class="sxs-lookup"><span data-stu-id="0a707-108">This example first finds a `Book` element, and then finds all sibling elements named `Book`.</span></span> <span data-ttu-id="0a707-109">所產生的集合包含內容節點。</span><span class="sxs-lookup"><span data-stu-id="0a707-109">The resulting collection includes the context node.</span></span>  
  
 <span data-ttu-id="0a707-110">此範例使用下列 XML 文件︰[範例 XML 檔：書籍 (LINQ to XML)](./sample-xml-file-books-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="0a707-110">This example uses the following XML document: [Sample XML File: Books (LINQ to XML)](./sample-xml-file-books-linq-to-xml.md).</span></span>  
  
```csharp  
XDocument books = XDocument.Load("Books.xml");  
  
XElement book =
    books  
    .Root  
    .Elements("Book")  
    .Skip(1)  
    .First();  
  
// LINQ to XML query  
IEnumerable<XElement> list1 =  
    book  
    .Parent  
    .Elements("Book");  
  
// XPath expression  
IEnumerable<XElement> list2 = book.XPathSelectElements("../Book");  
  
if (list1.Count() == list2.Count() &&  
        list1.Intersect(list2).Count() == list1.Count())  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 <span data-ttu-id="0a707-111">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="0a707-111">This example produces the following output:</span></span>  
  
```output  
Results are identical  
<Book id="bk101">  
  <Author>Garghentini, Davide</Author>  
  <Title>XML Developer's Guide</Title>  
  <Genre>Computer</Genre>  
  <Price>44.95</Price>  
  <PublishDate>2000-10-01</PublishDate>  
  <Description>An in-depth look at creating applications
      with XML.</Description>  
</Book>  
<Book id="bk102">  
  <Author>Garcia, Debra</Author>  
  <Title>Midnight Rain</Title>  
  <Genre>Fantasy</Genre>  
  <Price>5.95</Price>  
  <PublishDate>2000-12-16</PublishDate>  
  <Description>A former architect battles corporate zombies,
      an evil sorceress, and her own childhood to become queen
      of the world.</Description>  
</Book>  
```  

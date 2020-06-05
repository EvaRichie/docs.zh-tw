---
title: 作法：尋找同層級節點 (XPath-LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 73082738-2113-4438-8545-98d5df0927cb
ms.openlocfilehash: add51249dbc7cc4d33c79fcf6f82126f6bdb5612
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364535"
---
# <a name="how-to-find-sibling-nodes-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="510f4-102">如何：尋找同輩節點（XPath-LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="510f4-102">How to: Find Sibling Nodes (XPath-LINQ to XML) (Visual Basic)</span></span>

<span data-ttu-id="510f4-103">您可能想要尋找具有特定名稱之節點的所有同層級。</span><span class="sxs-lookup"><span data-stu-id="510f4-103">You might want to find all siblings of a node that have a specific name.</span></span> <span data-ttu-id="510f4-104">如果內容節點也有特定的名稱，所產生的集合可能包含內容節點。</span><span class="sxs-lookup"><span data-stu-id="510f4-104">The resulting collection might include the context node if the context node also has the specific name.</span></span>

<span data-ttu-id="510f4-105">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="510f4-105">The XPath expression is:</span></span>

`../Book`

## <a name="example"></a><span data-ttu-id="510f4-106">範例</span><span class="sxs-lookup"><span data-stu-id="510f4-106">Example</span></span>

<span data-ttu-id="510f4-107">此範例會先尋找 `Book` 項目，然後尋找名稱為 `Book` 的所有同層級項目。</span><span class="sxs-lookup"><span data-stu-id="510f4-107">This example first finds a `Book` element, and then finds all sibling elements named `Book`.</span></span> <span data-ttu-id="510f4-108">所產生的集合包含內容節點。</span><span class="sxs-lookup"><span data-stu-id="510f4-108">The resulting collection includes the context node.</span></span>

<span data-ttu-id="510f4-109">此範例使用下列 XML 文件︰[範例 XML 檔：書籍 (LINQ to XML)](sample-xml-file-books-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="510f4-109">This example uses the following XML document: [Sample XML File: Books (LINQ to XML)](sample-xml-file-books-linq-to-xml.md).</span></span>

```vb
Dim books As XDocument = XDocument.Load("Books.xml")
Dim book As XElement = books.Root.<Book>.Skip(1).First()

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = book.Parent.<Book>

' XPath expression
Dim list2 As IEnumerable(Of XElement) = book.XPathSelectElements("../Book")

If list1.Count() = list2.Count() And _
        list1.Intersect(list2).Count() = list1.Count() Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
For Each el As XElement In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="510f4-110">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="510f4-110">This example produces the following output:</span></span>

```console
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

## <a name="see-also"></a><span data-ttu-id="510f4-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="510f4-111">See also</span></span>

- [<span data-ttu-id="510f4-112">XPath 使用者的 LINQ to XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="510f4-112">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

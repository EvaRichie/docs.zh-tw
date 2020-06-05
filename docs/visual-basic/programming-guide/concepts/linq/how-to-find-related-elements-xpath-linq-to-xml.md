---
title: 作法：尋找相關項目 (XPath-LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 6b0ef058-d704-48a5-98cd-33f00d088af9
ms.openlocfilehash: 5819ef216f767367aa16b20f818b2bbc537d54b7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364652"
---
# <a name="how-to-find-related-elements-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="a8960-102">如何：尋找相關元素（XPath-LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="a8960-102">How to: Find Related Elements (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="a8960-103">本主題顯示如何取得在其他項目值所參考的屬性上選取的項目。</span><span class="sxs-lookup"><span data-stu-id="a8960-103">This topic shows how to get an element selecting on an attribute that is referred to by the value of another element.</span></span>  
  
 <span data-ttu-id="a8960-104">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="a8960-104">The XPath expression is:</span></span>  
  
 `.//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]`  
  
## <a name="example"></a><span data-ttu-id="a8960-105">範例</span><span class="sxs-lookup"><span data-stu-id="a8960-105">Example</span></span>  
 <span data-ttu-id="a8960-106">此範例會尋找第 12 個 `Order` 項目，然後尋找該順序的客戶。</span><span class="sxs-lookup"><span data-stu-id="a8960-106">This example finds the 12th `Order` element, and then finds the customer for that order.</span></span>  
  
 <span data-ttu-id="a8960-107">請注意，在 .NET 的清單中進行索引時，是以「零」為基礎。</span><span class="sxs-lookup"><span data-stu-id="a8960-107">Note that indexing into a list in .NET is 'zero' based.</span></span> <span data-ttu-id="a8960-108">在 XPath 述詞的節點集合中進行索引時，是以「一」為基礎。</span><span class="sxs-lookup"><span data-stu-id="a8960-108">Indexing into a collection of nodes in an XPath predicate is 'one' based.</span></span> <span data-ttu-id="a8960-109">此範例會反映這個差異。</span><span class="sxs-lookup"><span data-stu-id="a8960-109">This example reflects this difference.</span></span>  
  
 <span data-ttu-id="a8960-110">此範例使用下列 XML 文件︰[範例 XML 檔：客戶和訂單 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="a8960-110">This example uses the following XML document: [Sample XML File: Customers and Orders (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md).</span></span>  
  
```vb  
Dim co As XDocument = XDocument.Load("CustomersOrders.xml")  
  
' LINQ to XML query  
Dim customer1 As XElement = ( _  
    From el In co...<Customer> _  
    Where el.@CustomerID = co.<Root>.<Orders>.<Order>. _  
        ToList()(11).<CustomerID>(0).Value _  
    Select el).First()  
  
' An alternate way to write the query that avoids creation  
' of a System.Collections.Generic.List:  
Dim customer2 As XElement = ( _  
    From el In co...<Customer> _  
    Where el.@CustomerID = co.<Root>.<Orders>.<Order>. _  
        Skip(11).First().<CustomerID>(0).Value _  
    Select el).First()  
  
' XPath expression  
Dim customer3 As XElement = co.XPathSelectElement _  
    (".//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]")  
  
If customer1 Is customer2 And customer1 Is customer3 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(customer1)  
```  
  
 <span data-ttu-id="a8960-111">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="a8960-111">This example produces the following output:</span></span>  
  
```console
Results are identical  
<Customer CustomerID="HUNGC">  
  <CompanyName>Hungry Coyote Import Store</CompanyName>  
  <ContactName>Yoshi Latimer</ContactName>  
  <ContactTitle>Sales Representative</ContactTitle>  
  <Phone>(503) 555-6874</Phone>  
  <Fax>(503) 555-2376</Fax>  
  <FullAddress>  
    <Address>City Center Plaza 516 Main St.</Address>  
    <City>Elgin</City>  
    <Region>OR</Region>  
    <PostalCode>97827</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
</Customer>  
```  
  
## <a name="see-also"></a><span data-ttu-id="a8960-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8960-112">See also</span></span>

- [<span data-ttu-id="a8960-113">XPath 使用者的 LINQ to XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="a8960-113">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

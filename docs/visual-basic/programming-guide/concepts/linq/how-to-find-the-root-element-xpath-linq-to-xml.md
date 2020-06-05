---
title: 作法：尋找根項目 (XPath-LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 72c3aed5-9522-4454-a876-2070aad13f2e
ms.openlocfilehash: d1a507f97954c62672689bae719f251fed9a298b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364509"
---
# <a name="how-to-find-the-root-element-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="db78b-102">如何：尋找根項目（XPath-LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="db78b-102">How to: Find the Root Element (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="db78b-103">本主題顯示如何利用 XPath 和 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 取得根項目。</span><span class="sxs-lookup"><span data-stu-id="db78b-103">This topic shows how to get the root element with XPath and [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span>  
  
 <span data-ttu-id="db78b-104">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="db78b-104">The XPath expression is:</span></span>  
  
 `/PurchaseOrders`  
  
## <a name="example"></a><span data-ttu-id="db78b-105">範例</span><span class="sxs-lookup"><span data-stu-id="db78b-105">Example</span></span>  
 <span data-ttu-id="db78b-106">這個範例會尋找根項目。</span><span class="sxs-lookup"><span data-stu-id="db78b-106">This example finds the root element.</span></span>  
  
 <span data-ttu-id="db78b-107">此範例使用下列 XML 文件︰[範例 XML 檔：多份採購訂單 (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="db78b-107">This example uses the following XML document: [Sample XML File: Multiple Purchase Orders (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md).</span></span>  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim el1 As XElement = po.Root  
  
' XPath expression  
Dim el2 As XElement = po.XPathSelectElement("/PurchaseOrders")  
  
If el1 Is el2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(el1.Name)  
```  
  
 <span data-ttu-id="db78b-108">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="db78b-108">This example produces the following output:</span></span>  
  
```console  
Results are identical  
PurchaseOrders  
```  
  
## <a name="see-also"></a><span data-ttu-id="db78b-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db78b-109">See also</span></span>

- [<span data-ttu-id="db78b-110">XPath 使用者的 LINQ to XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="db78b-110">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

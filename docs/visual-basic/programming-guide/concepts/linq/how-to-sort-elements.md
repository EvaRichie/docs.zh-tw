---
title: 作法：排序項目
ms.date: 07/20/2015
ms.assetid: c2c09279-6c8a-482e-8e71-b1453a815052
ms.openlocfilehash: 1204fb4dc190d68956d01ffce225ce40e11538a4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397748"
---
# <a name="how-to-sort-elements-visual-basic"></a><span data-ttu-id="04b3f-102">如何：排序元素（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="04b3f-102">How to: Sort Elements (Visual Basic)</span></span>
<span data-ttu-id="04b3f-103">此範例顯示如何撰寫排序其結果的查詢。</span><span class="sxs-lookup"><span data-stu-id="04b3f-103">This example shows how to write a query that sorts its results.</span></span>  
  
## <a name="example"></a><span data-ttu-id="04b3f-104">範例</span><span class="sxs-lookup"><span data-stu-id="04b3f-104">Example</span></span>  
 <span data-ttu-id="04b3f-105">此範例使用下列 XML 文件︰[範例 XML 檔：數值資料 (LINQ to XML)](sample-xml-file-numerical-data-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="04b3f-105">This example uses the following XML document: [Sample XML File: Numerical Data (LINQ to XML)](sample-xml-file-numerical-data-linq-to-xml.md).</span></span>  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
Dim prices As IEnumerable(Of Decimal) = _  
    From el In root.<Data> _  
    Let price = Convert.ToDecimal(el.<Price>.Value) _  
    Order By (price) _  
    Select price  
For Each el As Decimal In prices  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="04b3f-106">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="04b3f-106">This code produces the following output:</span></span>  
  
```console  
0.99  
4.95  
6.99  
24.50  
29.00  
66.00  
89.99  
```  
  
## <a name="example"></a><span data-ttu-id="04b3f-107">範例</span><span class="sxs-lookup"><span data-stu-id="04b3f-107">Example</span></span>  
 <span data-ttu-id="04b3f-108">下列範例顯示命名空間中之 XML 的相同查詢。</span><span class="sxs-lookup"><span data-stu-id="04b3f-108">The following example shows the same query for XML that is in a namespace.</span></span> <span data-ttu-id="04b3f-109">如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="04b3f-109">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="04b3f-110">此範例使用下列 XML 文件︰[範例 XML 檔：命名空間中的數值資料](sample-xml-file-numerical-data-in-a-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="04b3f-110">This example uses the following XML document: [Sample XML File: Numerical Data in a Namespace](sample-xml-file-numerical-data-in-a-namespace.md).</span></span>  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("DataInNamespace.xml")  
        Dim prices As IEnumerable(Of Decimal) = _  
            From el In root.<Data> _  
            Let price = Convert.ToDecimal(el.<Price>.Value) _  
            Order By (price) _  
            Select price  
        For Each el As Decimal In prices  
            Console.WriteLine(el)  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="04b3f-111">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="04b3f-111">This code produces the following output:</span></span>  
  
```console  
0.99  
4.95  
6.99  
24.50  
29.00  
66.00  
89.99  
```  
  
## <a name="see-also"></a><span data-ttu-id="04b3f-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="04b3f-112">See also</span></span>

- [<span data-ttu-id="04b3f-113">排序資料</span><span class="sxs-lookup"><span data-stu-id="04b3f-113">Sorting Data</span></span>](sorting-data.md)
- [<span data-ttu-id="04b3f-114">基本查詢（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="04b3f-114">Basic Queries (LINQ to XML) (Visual Basic)</span></span>](basic-queries-linq-to-xml.md)

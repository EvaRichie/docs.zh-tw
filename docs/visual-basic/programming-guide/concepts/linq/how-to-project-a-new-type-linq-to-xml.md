---
title: 作法：投影新類型 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 8cfb24f5-89b2-4cfb-b85d-e7963f8f1845
ms.openlocfilehash: 48fb82e870a4fc4fa16cfb48a127f364e6d81f13
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396502"
---
# <a name="how-to-project-a-new-type-linq-to-xml-visual-basic"></a><span data-ttu-id="2dc5c-102">如何：投影新類型（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="2dc5c-102">How to: Project a New Type (LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="2dc5c-103">本節中的其他範例顯示的查詢會傳回結果，當做 <xref:System.Collections.Generic.IEnumerable%601> 之 <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601> 的 `string`，以及 <xref:System.Collections.Generic.IEnumerable%601> 的 `int`。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-103">Other examples in this section have shown queries that return results as <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601> of `string`, and <xref:System.Collections.Generic.IEnumerable%601> of `int`.</span></span> <span data-ttu-id="2dc5c-104">這些是常見的結果型別，但這些型別不適用於每個案例。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-104">These are common result types, but they are not appropriate for every scenario.</span></span> <span data-ttu-id="2dc5c-105">在許多情況下，您會希望您的查詢傳回其他型別的 <xref:System.Collections.Generic.IEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-105">In many cases you will want your queries to return an <xref:System.Collections.Generic.IEnumerable%601> of some other type.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2dc5c-106">範例</span><span class="sxs-lookup"><span data-stu-id="2dc5c-106">Example</span></span>  
 <span data-ttu-id="2dc5c-107">此範例顯示如何具現化 `Select` 子句中的物件。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-107">This example shows how to instantiate objects in the `Select` clause.</span></span> <span data-ttu-id="2dc5c-108">此程式碼會先利用建構函式定義新的類別，然後修改 `Select` 陳述式，讓運算式成為新類別的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-108">The code first defines a new class with a constructor, and then modifies the `Select` statement so that the expression is a new instance of the new class.</span></span>  
  
 <span data-ttu-id="2dc5c-109">此範例使用下列 XML 文件︰[範例 XML 檔：典型採購訂單 (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-109">This example uses the following XML document: [Sample XML File: Typical Purchase Order (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md).</span></span>  
  
```vb  
Public Class NameQty  
    Public name As String  
    Public qty As Integer  
    Public Sub New(ByVal n As String, ByVal q As Integer)  
        name = n  
        qty = q  
    End Sub  
End Class  
  
Public Class Program  
    Shared Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
  
        Dim nqList As IEnumerable(Of NameQty) = _  
            From n In po...<Item> _  
            Select New NameQty( _  
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))  
  
        For Each n As NameQty In nqList  
            Console.WriteLine(n.name & ":" & n.qty)  
        Next  
    End Sub  
End Class  
```  
  
 <span data-ttu-id="2dc5c-110">這個範例會使用 how `M:System.Xml.Linq.XElement.Element` [To：取出單一子專案（LINQ to XML）（Visual Basic）](how-to-retrieve-a-single-child-element-linq-to-xml.md)主題中引進的方法。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-110">This example uses the `M:System.Xml.Linq.XElement.Element` method that was introduced in the topic [How to: Retrieve a Single Child Element (LINQ to XML) (Visual Basic)](how-to-retrieve-a-single-child-element-linq-to-xml.md).</span></span> <span data-ttu-id="2dc5c-111">它也會使用轉換以擷取 `M:System.Xml.Linq.XElement.Element` 方法所傳回的元素值。</span><span class="sxs-lookup"><span data-stu-id="2dc5c-111">It also uses casts to retrieve the values of the elements that are returned by the `M:System.Xml.Linq.XElement.Element` method.</span></span>  
  
 <span data-ttu-id="2dc5c-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2dc5c-112">This example produces the following output:</span></span>  
  
```console  
Lawnmower:1  
Baby Monitor:2  
```  
  
## <a name="see-also"></a><span data-ttu-id="2dc5c-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2dc5c-113">See also</span></span>

- [<span data-ttu-id="2dc5c-114">投影和轉換（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="2dc5c-114">Projections and Transformations (LINQ to XML) (Visual Basic)</span></span>](projections-and-transformations-linq-to-xml.md)

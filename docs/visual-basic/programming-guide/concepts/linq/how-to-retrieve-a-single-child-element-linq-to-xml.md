---
title: 作法：擷取單一子項目 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 0033e258-d9c4-4569-86f6-79b7c06d1204
ms.openlocfilehash: ab28ddd960374b22f44ac0c8fc7bddfe0608b8c5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397839"
---
# <a name="how-to-retrieve-a-single-child-element-linq-to-xml-visual-basic"></a><span data-ttu-id="ff0ed-102">如何：取出單一子項目（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="ff0ed-102">How to: Retrieve a Single Child Element (LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="ff0ed-103">這個主題會說明如何擷取單一子項目 (如果有子項目的名稱)。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-103">This topic explains how to retrieve a single child element, given the name of the child element.</span></span> <span data-ttu-id="ff0ed-104">當您知道子項目的名稱，而且只有一個項目擁有這個名稱，只擷取一個項目 (而不是擷取一個集合) 可能很方便。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-104">When you know the name of the child element and that there is only one element that has this name, it can be convenient to retrieve just one element, instead of a collection.</span></span>  
  
 <span data-ttu-id="ff0ed-105"><xref:System.Xml.Linq.XContainer.Element%2A> 方法會使用指定的 <xref:System.Xml.Linq.XElement>，傳回第一個子系 <xref:System.Xml.Linq.XName>。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-105">The <xref:System.Xml.Linq.XContainer.Element%2A> method returns the first child <xref:System.Xml.Linq.XElement> with the specified <xref:System.Xml.Linq.XName>.</span></span>  
  
 <span data-ttu-id="ff0ed-106">如果您要在 Visual Basic 中擷取單一子項目，常用的方法是使用 XML 屬性，然後使用陣列索引子標記法擷取第一個項目。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-106">If you want to retrieve a single child element in Visual Basic, a common approach is to use the XML property, and then retrieve the first element using array indexer notation.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ff0ed-107">範例</span><span class="sxs-lookup"><span data-stu-id="ff0ed-107">Example</span></span>  
 <span data-ttu-id="ff0ed-108">下列範例示範 <xref:System.Xml.Linq.XContainer.Element%2A> 方法的用法。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-108">The following example demonstrates the use of the <xref:System.Xml.Linq.XContainer.Element%2A> method.</span></span> <span data-ttu-id="ff0ed-109">此範例會採用名稱為 `po` 的 XML 樹狀結構，並尋找名稱為 `Comment` 的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-109">This example takes the XML tree named `po` and finds the first element named `Comment`.</span></span>  
  
 <span data-ttu-id="ff0ed-110">Visual Basic 範例會顯示使用陣列索引子標記法來擷取單一項目。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-110">The Visual Basic example shows using array indexer notation to retrieve a single element.</span></span>  
  
 <span data-ttu-id="ff0ed-111">此範例使用下列 XML 文件︰[範例 XML 檔：典型採購訂單 (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-111">This example uses the following XML document: [Sample XML File: Typical Purchase Order (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md).</span></span>  
  
```vb  
Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
Dim e As XElement = po.<DeliveryNotes>(0)  
Console.WriteLine(e)  
```  
  
 <span data-ttu-id="ff0ed-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ff0ed-112">This example produces the following output:</span></span>  
  
```xml  
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>  
```  
  
## <a name="example"></a><span data-ttu-id="ff0ed-113">範例</span><span class="sxs-lookup"><span data-stu-id="ff0ed-113">Example</span></span>  
 <span data-ttu-id="ff0ed-114">下列範例顯示命名空間中之 XML 的相同程式碼。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-114">The following example shows the same code for XML that is in a namespace.</span></span> <span data-ttu-id="ff0ed-115">如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-115">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="ff0ed-116">此範例使用下列 XML 文件︰[範例 XML 檔：命名空間中的典型採購訂單](sample-xml-file-typical-purchase-order-in-a-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0ed-116">This example uses the following XML document: [Sample XML File: Typical Purchase Order in a Namespace](sample-xml-file-typical-purchase-order-in-a-namespace.md).</span></span>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrderInNamespace.xml")  
        Dim e As XElement = po.<aw:DeliveryNotes>(0)  
        Console.WriteLine(e)  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="ff0ed-117">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ff0ed-117">This example produces the following output:</span></span>  
  
```xml  
<aw:DeliveryNotes xmlns:aw="http://www.adventure-works.com">Please leave packages in shed by driveway.</aw:DeliveryNotes>  
```  
  
## <a name="see-also"></a><span data-ttu-id="ff0ed-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ff0ed-118">See also</span></span>

- [<span data-ttu-id="ff0ed-119">LINQ to XML 軸 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ff0ed-119">LINQ to XML Axes (Visual Basic)</span></span>](linq-to-xml-axes.md)

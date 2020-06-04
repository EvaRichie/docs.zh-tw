---
title: 作法：撰寫具有複雜篩選的查詢
ms.date: 07/20/2015
ms.assetid: bf286ffc-7990-4b00-a4eb-ee3d70129950
ms.openlocfilehash: 18ed4379b7ec9c8007cc3c189fc45571b5161911
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397618"
---
# <a name="how-to-write-queries-with-complex-filtering-visual-basic"></a><span data-ttu-id="d9ece-102">如何：撰寫具有複雜篩選的查詢（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d9ece-102">How to: Write Queries with Complex Filtering (Visual Basic)</span></span>
<span data-ttu-id="d9ece-103">有時候您會想要利用複雜篩選撰寫 LINQ to XML 查詢。</span><span class="sxs-lookup"><span data-stu-id="d9ece-103">Sometimes you want to write LINQ to XML queries with complex filters.</span></span> <span data-ttu-id="d9ece-104">例如，您可能必須尋找其子項目包含特定名稱和值的所有項目。</span><span class="sxs-lookup"><span data-stu-id="d9ece-104">For example, you might have to find all elements that have a child element with a particular name and value.</span></span> <span data-ttu-id="d9ece-105">本主題提供利用複雜篩選撰寫查詢的範例。</span><span class="sxs-lookup"><span data-stu-id="d9ece-105">This topic gives an example of writing a query with complex filtering.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d9ece-106">範例</span><span class="sxs-lookup"><span data-stu-id="d9ece-106">Example</span></span>  
 <span data-ttu-id="d9ece-107">這個範例顯示如何尋找其 `PurchaseOrder` 子項目的 `Address` 屬性等於 "Shipping"，而 `Type` 子項目等於 "NY" 的所有 `State` 項目。</span><span class="sxs-lookup"><span data-stu-id="d9ece-107">This example shows how to find all `PurchaseOrder` elements that have a child `Address` element that has a `Type` attribute equal to "Shipping" and a child `State` element equal to "NY".</span></span> <span data-ttu-id="d9ece-108">它會在 `Where` 子句中使用巢狀查詢，而且如果集合在其中有任何項目，`Any` 運算子會傳回 `True`。</span><span class="sxs-lookup"><span data-stu-id="d9ece-108">It uses a nested query in the `Where` clause, and the `Any` operator returns `True` if the collection has any elements in it.</span></span>  
  
 <span data-ttu-id="d9ece-109">此範例使用下列 XML 文件︰[範例 XML 檔：多份採購訂單 (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="d9ece-109">This example uses the following XML document: [Sample XML File: Multiple Purchase Orders (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="d9ece-110">如需運算子的詳細資訊 `Any` ，請參閱[數量詞作業（Visual Basic）](quantifier-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="d9ece-110">For more information about the `Any` operator, see [Quantifier Operations (Visual Basic)](quantifier-operations.md).</span></span>  
  
```vb  
Dim root As XElement = XElement.Load("PurchaseOrders.xml")  
Dim purchaseOrders As IEnumerable(Of XElement) = _  
    From el In root.<PurchaseOrder> _  
    Where _  
        (From add In el.<Address> _  
        Where _  
             add.@Type = "Shipping" And _  
             add.<State>.Value = "NY" _  
        Select add) _  
    .Any() _  
    Select el  
For Each el As XElement In purchaseOrders  
    Console.WriteLine(el.@PurchaseOrderNumber)  
Next  
```  
  
 <span data-ttu-id="d9ece-111">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d9ece-111">This code produces the following output:</span></span>  
  
```console  
99505  
```  
  
## <a name="example"></a><span data-ttu-id="d9ece-112">範例</span><span class="sxs-lookup"><span data-stu-id="d9ece-112">Example</span></span>  
 <span data-ttu-id="d9ece-113">下列範例顯示命名空間中之 XML 的相同查詢。</span><span class="sxs-lookup"><span data-stu-id="d9ece-113">The following example shows the same query for XML that is in a namespace.</span></span> <span data-ttu-id="d9ece-114">如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="d9ece-114">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="d9ece-115">此範例使用下列 XML 文件︰[範例 XML 檔：命名空間中的多份採購訂單](sample-xml-file-multiple-purchase-orders-in-a-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="d9ece-115">This example uses the following XML document: [Sample XML File: Multiple Purchase Orders in a Namespace](sample-xml-file-multiple-purchase-orders-in-a-namespace.md).</span></span>  
  
```vb  
Imports <xmlns:aw='http://www.adventure-works.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("PurchaseOrdersInNamespace.xml")  
        Dim purchaseOrders As IEnumerable(Of XElement) = _  
            From el In root.<aw:PurchaseOrder> _  
            Where _  
                (From add In el.<aw:Address> _  
                Where _  
                     add.@aw:Type = "Shipping" And _  
                     add.<aw:State>.Value = "NY" _  
                Select add) _  
            .Any() _  
            Select el  
        For Each el As XElement In purchaseOrders  
            Console.WriteLine(el.@aw:PurchaseOrderNumber)  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="d9ece-116">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d9ece-116">This code produces the following output:</span></span>  
  
```console  
99505  
```  
  
## <a name="see-also"></a><span data-ttu-id="d9ece-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d9ece-117">See also</span></span>

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [<span data-ttu-id="d9ece-118">基本查詢（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d9ece-118">Basic Queries (LINQ to XML) (Visual Basic)</span></span>](basic-queries-linq-to-xml.md)
- [<span data-ttu-id="d9ece-119">XML Child Axis Property</span><span class="sxs-lookup"><span data-stu-id="d9ece-119">XML Child Axis Property</span></span>](../../../language-reference/xml-axis/xml-child-axis-property.md)
- [<span data-ttu-id="d9ece-120">XML Attribute Axis Property</span><span class="sxs-lookup"><span data-stu-id="d9ece-120">XML Attribute Axis Property</span></span>](../../../language-reference/xml-axis/xml-attribute-axis-property.md)
- [<span data-ttu-id="d9ece-121">XML 值屬性</span><span class="sxs-lookup"><span data-stu-id="d9ece-121">XML Value Property</span></span>](../../../language-reference/xml-axis/xml-value-property.md)
- [<span data-ttu-id="d9ece-122">投射作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d9ece-122">Projection Operations (Visual Basic)</span></span>](projection-operations.md)
- [<span data-ttu-id="d9ece-123">數量詞作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d9ece-123">Quantifier Operations (Visual Basic)</span></span>](quantifier-operations.md)

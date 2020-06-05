---
title: 作法：篩選選擇性項目
ms.date: 07/20/2015
ms.assetid: a74b76ad-6889-4185-a189-d6ef2c63841e
ms.openlocfilehash: 9f03eee479e7c47e528a145d370472de6dfddd39
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394359"
---
# <a name="how-to-filter-on-an-optional-element-visual-basic"></a><span data-ttu-id="beab3-102">如何：篩選選擇性元素（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="beab3-102">How to: Filter on an Optional Element (Visual Basic)</span></span>
<span data-ttu-id="beab3-103">有時候即使您不確定項目是否存在於 XML 文件中，您都會想要針對該項目進行篩選。</span><span class="sxs-lookup"><span data-stu-id="beab3-103">Sometimes you want to filter for an element even though you are not sure it exists in your XML document.</span></span> <span data-ttu-id="beab3-104">搜尋應該會執行，因此，如果特定的項目沒有子項目，您就不會篩選該項目來觸發 Null 參考例外狀況。</span><span class="sxs-lookup"><span data-stu-id="beab3-104">The search should be executed so that if the particular element does not have the child element, you do not trigger a null reference exception by filtering for it.</span></span> <span data-ttu-id="beab3-105">在下列範例中，`Child5` 項目沒有 `Type` 子項目，但查詢仍會正確執行。</span><span class="sxs-lookup"><span data-stu-id="beab3-105">In the following example, the `Child5` element does not have a `Type` child element, but the query still executes correctly.</span></span>  
  
## <a name="example"></a><span data-ttu-id="beab3-106">範例</span><span class="sxs-lookup"><span data-stu-id="beab3-106">Example</span></span>  
 <span data-ttu-id="beab3-107">此範例使用 <xref:System.Xml.Linq.Extensions.Elements%2A> 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="beab3-107">This example uses the <xref:System.Xml.Linq.Extensions.Elements%2A> extension method.</span></span>  
  
```vb  
Dim root As XElement = _
    <Root>  
        <Child1>  
            <Text>Child One Text</Text>  
            <Type Value="Yes"/>  
        </Child1>  
        <Child2>  
            <Text>Child Two Text</Text>  
            <Type Value="Yes"/>  
        </Child2>  
        <Child3>  
            <Text>Child Three Text</Text>  
            <Type Value="No"/>  
        </Child3>  
        <Child4>  
            <Text>Child Four Text</Text>  
            <Type Value="Yes"/>  
        </Child4>  
        <Child5>  
            <Text>Child Five Text</Text>  
        </Child5>  
    </Root>  
Dim cList As IEnumerable(Of String) = _  
    From typeElement In root.Elements().<Type> _  
    Where typeElement.@Value = "Yes" _  
    Select typeElement.Parent.<Text>.Value  
Dim str As String  
For Each str In cList  
    Console.WriteLine(str)  
Next  
```  
  
 <span data-ttu-id="beab3-108">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="beab3-108">This code produces the following output:</span></span>  
  
```console  
Child One Text  
Child Two Text  
Child Four Text  
```  
  
## <a name="example"></a><span data-ttu-id="beab3-109">範例</span><span class="sxs-lookup"><span data-stu-id="beab3-109">Example</span></span>  
 <span data-ttu-id="beab3-110">下列範例顯示命名空間中之 XML 的相同查詢。</span><span class="sxs-lookup"><span data-stu-id="beab3-110">The following example shows the same query for XML that is in a namespace.</span></span> <span data-ttu-id="beab3-111">如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="beab3-111">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child1>  
                    <Text>Child One Text</Text>  
                    <Type Value="Yes"/>  
                </Child1>  
                <Child2>  
                    <Text>Child Two Text</Text>  
                    <Type Value="Yes"/>  
                </Child2>  
                <Child3>  
                    <Text>Child Three Text</Text>  
                    <Type Value="No"/>  
                </Child3>  
                <Child4>  
                    <Text>Child Four Text</Text>  
                    <Type Value="Yes"/>  
                </Child4>  
                <Child5>  
                    <Text>Child Five Text</Text>  
                </Child5>  
            </Root>  
        Dim cList As IEnumerable(Of String) = _  
            From typeElement In root.Elements().<Type> _  
            Where typeElement.@Value = "Yes" _  
            Select typeElement.Parent.<Text>.Value  
        Dim str As String  
        For Each str In cList  
            Console.WriteLine(str)  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="beab3-112">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="beab3-112">This code produces the following output:</span></span>  
  
```console  
Child One Text  
Child Two Text  
Child Four Text  
```  
  
## <a name="see-also"></a><span data-ttu-id="beab3-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="beab3-113">See also</span></span>

- <xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType>
- [<span data-ttu-id="beab3-114">基本查詢（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="beab3-114">Basic Queries (LINQ to XML) (Visual Basic)</span></span>](basic-queries-linq-to-xml.md)
- [<span data-ttu-id="beab3-115">XML Child Axis Property</span><span class="sxs-lookup"><span data-stu-id="beab3-115">XML Child Axis Property</span></span>](../../../language-reference/xml-axis/xml-child-axis-property.md)
- [<span data-ttu-id="beab3-116">XML Attribute Axis Property</span><span class="sxs-lookup"><span data-stu-id="beab3-116">XML Attribute Axis Property</span></span>](../../../language-reference/xml-axis/xml-attribute-axis-property.md)
- [<span data-ttu-id="beab3-117">XML 值屬性</span><span class="sxs-lookup"><span data-stu-id="beab3-117">XML Value Property</span></span>](../../../language-reference/xml-axis/xml-value-property.md)
- [<span data-ttu-id="beab3-118">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="beab3-118">Standard Query Operators Overview (Visual Basic)</span></span>](standard-query-operators-overview.md)
- [<span data-ttu-id="beab3-119">投射作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="beab3-119">Projection Operations (Visual Basic)</span></span>](projection-operations.md)

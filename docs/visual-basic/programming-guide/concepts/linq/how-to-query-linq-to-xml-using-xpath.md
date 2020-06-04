---
title: 作法：使用 XPath 查詢 LINQ to XML
ms.date: 07/20/2015
ms.assetid: e1f69a20-1efa-452d-9089-c472fa84b3d5
ms.openlocfilehash: d95e5a82d146c357f52d03375119474b042d49f6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397917"
---
# <a name="how-to-query-linq-to-xml-using-xpath-visual-basic"></a><span data-ttu-id="fcac3-102">如何：使用 XPath 查詢 LINQ to XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="fcac3-102">How to: Query LINQ to XML Using XPath (Visual Basic)</span></span>
<span data-ttu-id="fcac3-103">本主題說明可讓您使用 XPath 查詢 XML 樹狀結構的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="fcac3-103">This topic introduces the extension methods that enable you to query an XML tree by using XPath.</span></span> <span data-ttu-id="fcac3-104">如需有關使用這些擴充方法的詳細資訊，請參閱 <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="fcac3-104">For detailed information about using these extension methods, see <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="fcac3-105">除非您已經有非常特定的理由要使用 XPath 查詢 (例如，廣泛使用舊版程式碼)，否則，不建議搭配 LINQ to XML 使用 XPath。</span><span class="sxs-lookup"><span data-stu-id="fcac3-105">Unless you have a very specific reason for querying using XPath, such as extensive use of legacy code, using XPath with LINQ to XML is not recommended.</span></span> <span data-ttu-id="fcac3-106">XPath 查詢將不會與 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢一起執行。</span><span class="sxs-lookup"><span data-stu-id="fcac3-106">XPath queries will not perform as well as [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] queries.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fcac3-107">範例</span><span class="sxs-lookup"><span data-stu-id="fcac3-107">Example</span></span>  
 <span data-ttu-id="fcac3-108">下列範例會建立小型 XML 樹狀結構，並使用 <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> 來選取一組項目。</span><span class="sxs-lookup"><span data-stu-id="fcac3-108">The following example creates a small XML tree and uses <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> to select a set of elements.</span></span>  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child1>2</Child1>  
        <Child1>3</Child1>  
        <Child2>4</Child2>  
        <Child2>5</Child2>  
        <Child2>6</Child2>  
    </Root>  
  
Dim list As IEnumerable(Of XElement) = root.XPathSelectElements("./Child2")  
For Each el As XElement In list  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="fcac3-109">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="fcac3-109">This example produces the following output:</span></span>  
  
```xml  
<Child2>4</Child2>  
<Child2>5</Child2>  
<Child2>6</Child2>  
```  
  
## <a name="see-also"></a><span data-ttu-id="fcac3-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fcac3-110">See also</span></span>

- [<span data-ttu-id="fcac3-111">先進的查詢技術（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="fcac3-111">Advanced Query Techniques (LINQ to XML) (Visual Basic)</span></span>](advanced-query-techniques-linq-to-xml.md)

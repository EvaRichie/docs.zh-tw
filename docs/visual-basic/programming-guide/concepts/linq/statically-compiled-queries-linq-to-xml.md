---
title: 靜態編譯的查詢 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 3f4825c7-c3b0-48da-ba4e-8e97fb2a2f34
ms.openlocfilehash: f020c1ed8627df8c8386a059f0cea372e8df363e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406764"
---
# <a name="statically-compiled-queries-linq-to-xml-visual-basic"></a><span data-ttu-id="003a2-102">靜態編譯的查詢（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="003a2-102">Statically Compiled Queries (LINQ to XML) (Visual Basic)</span></span>

<span data-ttu-id="003a2-103">相對於 <xref:System.Xml.XmlDocument> 而言，LINQ to XML 其中一個最重要的效能優勢在於，LINQ to XML 中的查詢是靜態編譯的查詢，而 XPath 查詢則必須在執行階段解譯。</span><span class="sxs-lookup"><span data-stu-id="003a2-103">One of the most important performance benefits LINQ to XML, as opposed to <xref:System.Xml.XmlDocument>, is that queries in LINQ to XML are statically compiled, whereas XPath queries must be interpreted at run time.</span></span> <span data-ttu-id="003a2-104">由於這項功能是 LINQ to XML 內建的，所以您不需要進行額外步驟，即可運用此功能，但是在選擇這兩項技術時了解其差異會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="003a2-104">This feature is built in to LINQ to XML, so you do not have to perform extra steps to take advantage of it, but it is helpful to understand the distinction when choosing between the two technologies.</span></span> <span data-ttu-id="003a2-105">本主題將說明兩者的差異。</span><span class="sxs-lookup"><span data-stu-id="003a2-105">This topic explains the difference.</span></span>

## <a name="statically-compiled-queries-vs-xpath"></a><span data-ttu-id="003a2-106">靜態編譯查詢與 XPath 的比較</span><span class="sxs-lookup"><span data-stu-id="003a2-106">Statically Compiled Queries vs. XPath</span></span>

<span data-ttu-id="003a2-107">下列範例將顯示如何取得具有指定之名稱以及具有指定值之屬性的子代項目。</span><span class="sxs-lookup"><span data-stu-id="003a2-107">The following example shows how to get the descendant elements with a specified name, and with an attribute with a specified value.</span></span>

<span data-ttu-id="003a2-108">下面是對等的 XPath 運算式：</span><span class="sxs-lookup"><span data-stu-id="003a2-108">The following is the equivalent XPath expression:</span></span>

```vb
//Address[@Type='Shipping']
```

```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 = From el In po.Descendants("Address")
            Where el.@Type = "Shipping"

For Each el In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="003a2-109">這則範例中的查詢運算式由編譯器重新撰寫成以方法為基礎的查詢語法。</span><span class="sxs-lookup"><span data-stu-id="003a2-109">The query expression in this example is re-written by the compiler to method-based query syntax.</span></span> <span data-ttu-id="003a2-110">下列範例 (使用以方法為基礎的查詢語法所撰寫) 會與先前的範例產生相同的結果：</span><span class="sxs-lookup"><span data-stu-id="003a2-110">The following example, which is written in method-based query syntax, produces the same results as the previous one:</span></span>

```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 As IEnumerable(Of XElement) = po.Descendants("Address").Where(Function(el) el.@Type = "Shipping")

For Each el In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="003a2-111"><xref:System.Linq.Enumerable.Where%2A> 方法是擴充方法。</span><span class="sxs-lookup"><span data-stu-id="003a2-111">The <xref:System.Linq.Enumerable.Where%2A> method is an extension method.</span></span> <span data-ttu-id="003a2-112">如需詳細資訊，請參閱[擴充方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="003a2-112">For more information, see [Extension Methods](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md).</span></span> <span data-ttu-id="003a2-113">由於 <xref:System.Linq.Enumerable.Where%2A> 是擴充方法，所以上述查詢會按照下列方式編譯：</span><span class="sxs-lookup"><span data-stu-id="003a2-113">Because <xref:System.Linq.Enumerable.Where%2A> is an extension method, the query above is compiled as though it were written as follows:</span></span>

```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 = Enumerable.Where(po.Descendants("Address"), Function(el) el.@Type = "Shipping")

For Each el In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="003a2-114">這則範例會與先前兩則範例產生完全相同的結果。</span><span class="sxs-lookup"><span data-stu-id="003a2-114">This example produces exactly the same results as the previous two examples.</span></span> <span data-ttu-id="003a2-115">這表示查詢實際上會編譯成靜態連結方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="003a2-115">This illustrates the fact that queries are effectively compiled into statically linked method calls.</span></span> <span data-ttu-id="003a2-116">與 Iterator 的延後執行語意 (Semantics) 結合之後，便可改善效能。</span><span class="sxs-lookup"><span data-stu-id="003a2-116">This, combined with the deferred execution semantics of iterators, improves performance.</span></span> <span data-ttu-id="003a2-117">如需反覆運算器延後執行語義的詳細資訊，請參閱[LINQ to XML （Visual Basic）中的延後執行和延遲評估](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="003a2-117">For more information about the deferred execution semantics of iterators, see [Deferred Execution and Lazy Evaluation in LINQ to XML (Visual Basic)](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).</span></span>

> [!NOTE]
> <span data-ttu-id="003a2-118">這些範例是代表編譯器可能會撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="003a2-118">These examples are representative of the code that the compiler might write.</span></span> <span data-ttu-id="003a2-119">雖然實際的實作 (Implementation) 可能會與這些範例稍微不同，不過其效能與這些範例相同或相似。</span><span class="sxs-lookup"><span data-stu-id="003a2-119">The actual implementation might differ slightly from these examples, but the performance will be the same or similar to these examples.</span></span>

## <a name="executing-xpath-expressions-with-xmldocument"></a><span data-ttu-id="003a2-120">使用 XmlDocument 來執行 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="003a2-120">Executing XPath Expressions with XmlDocument</span></span>

<span data-ttu-id="003a2-121">下列範例會使用 <xref:System.Xml.XmlDocument> 來達成與先前範例相同的結果：</span><span class="sxs-lookup"><span data-stu-id="003a2-121">The following example uses <xref:System.Xml.XmlDocument> to accomplish the same results as the previous examples:</span></span>

```vb
Dim reader = Xml.XmlReader.Create("PurchaseOrders.xml")
Dim doc As New Xml.XmlDocument()
doc.Load(reader)
Dim nl As Xml.XmlNodeList = doc.SelectNodes(".//Address[@Type='Shipping']")
For Each n As Xml.XmlNode In nl
    Console.WriteLine(n.OuterXml)
Next
reader.Close()
```

<span data-ttu-id="003a2-122">這個查詢與使用 LINQ to XML 的範例會傳回相同的輸出。唯一的差異是 LINQ to XML 會讓列印的 XML 縮排，而 <xref:System.Xml.XmlDocument> 則不會。</span><span class="sxs-lookup"><span data-stu-id="003a2-122">This query returns the same output as the examples that use LINQ to XML; the only difference is that LINQ to XML indents the printed XML, whereas <xref:System.Xml.XmlDocument> does not.</span></span>

<span data-ttu-id="003a2-123">不過，<xref:System.Xml.XmlDocument> 方法的執行效能通常不如 LINQ to XML，因為每次呼叫 <xref:System.Xml.XmlNode.SelectNodes%2A> 方法時，它就必須在內部執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="003a2-123">However, the <xref:System.Xml.XmlDocument> approach generally does not perform as well as LINQ to XML, because the <xref:System.Xml.XmlNode.SelectNodes%2A> method must do the following internally every time it is called:</span></span>

- <span data-ttu-id="003a2-124">它會剖析包含 XPath 運算式的字串，並將此字串分割成語彙基元 (Token)。</span><span class="sxs-lookup"><span data-stu-id="003a2-124">It parses the string that contains the XPath expression, breaking the string into tokens.</span></span>

- <span data-ttu-id="003a2-125">它會驗證這些語彙基元來確定 XPath 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="003a2-125">It validates the tokens to make sure that the XPath expression is valid.</span></span>

- <span data-ttu-id="003a2-126">它會將此運算式轉譯成內部運算式樹狀架構。</span><span class="sxs-lookup"><span data-stu-id="003a2-126">It translates the expression into an internal expression tree.</span></span>

- <span data-ttu-id="003a2-127">它會逐一查看這些節點，並且根據運算式的評估，適當地選取結果集的節點。</span><span class="sxs-lookup"><span data-stu-id="003a2-127">It iterates through the nodes, appropriately selecting the nodes for the result set based on the evaluation of the expression.</span></span>

<span data-ttu-id="003a2-128">這點明顯比對應 LINQ to XML 查詢所完成的工作還多。</span><span class="sxs-lookup"><span data-stu-id="003a2-128">This is significantly more than the work done by the corresponding LINQ to XML query.</span></span> <span data-ttu-id="003a2-129">雖然特定效能差異會因不同類型的查詢而異，不過一般而言，相較於使用 <xref:System.Xml.XmlDocument> 來評估 XPath 運算式，LINQ to XML 查詢會進行較少工作，因此具有較佳的執行效能。</span><span class="sxs-lookup"><span data-stu-id="003a2-129">The specific performance difference varies for different types of queries, but in general LINQ to XML queries do less work, and therefore perform better, than evaluating XPath expressions using <xref:System.Xml.XmlDocument>.</span></span>

## <a name="see-also"></a><span data-ttu-id="003a2-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="003a2-130">See also</span></span>

- [<span data-ttu-id="003a2-131">效能（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="003a2-131">Performance (LINQ to XML) (Visual Basic)</span></span>](performance-linq-to-xml.md)

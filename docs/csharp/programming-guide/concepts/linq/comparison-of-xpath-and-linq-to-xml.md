---
title: XPath 和 LINQ to XML 的比較
description: '瞭解 c # 中 XPath 與 LINQ to XML 之間功能的相似性和差異。 您可以使用這兩者來查詢 XML 樹狀結構。'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 87d361b1-daa9-4fd4-a53a-cbfa40111ad3
ms.openlocfilehash: e2f34903b20a53dea6e5ff4858d4fadaebd9c37a
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104000"
---
# <a name="comparison-of-xpath-and-linq-to-xml"></a><span data-ttu-id="f0edc-104">XPath 和 LINQ to XML 的比較</span><span class="sxs-lookup"><span data-stu-id="f0edc-104">Comparison of XPath and LINQ to XML</span></span>
<span data-ttu-id="f0edc-105">XPath 和 LINQ to XML 提供一些類似的功能。</span><span class="sxs-lookup"><span data-stu-id="f0edc-105">XPath and LINQ to XML offer some similar functionality.</span></span> <span data-ttu-id="f0edc-106">兩者都可用於查詢 XML 樹狀結構，將此類結果當做項目的集合、屬性的集合、節點的集合，以及項目或屬性的值傳回。</span><span class="sxs-lookup"><span data-stu-id="f0edc-106">Both can be used to query an XML tree, returning such results as a collection of elements, a collection of attributes, a collection of nodes, or the value of an element or attribute.</span></span> <span data-ttu-id="f0edc-107">不過，也有一些差異。</span><span class="sxs-lookup"><span data-stu-id="f0edc-107">However, there are also some differences.</span></span>  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a><span data-ttu-id="f0edc-108">XPath 與 LINQ to XML 之間的差異</span><span class="sxs-lookup"><span data-stu-id="f0edc-108">Differences Between XPath and LINQ to XML</span></span>  
 <span data-ttu-id="f0edc-109">XPath 不允許評估新的型別。</span><span class="sxs-lookup"><span data-stu-id="f0edc-109">XPath does not allow projection of new types.</span></span> <span data-ttu-id="f0edc-110">它只能從樹狀結構傳回節點的集合，而 LINQ to XML 可以執行查詢並評估新圖案中的物件圖形或 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f0edc-110">It can only return collections of nodes from the tree, whereas LINQ to XML can execute a query and project an object graph or an XML tree in a new shape.</span></span> <span data-ttu-id="f0edc-111">LINQ to XML 查詢包含的功能更多，而且比 XPath 運算式的功能更強大。</span><span class="sxs-lookup"><span data-stu-id="f0edc-111">LINQ to XML queries encompass much more functionality and are much more powerful than XPath expressions.</span></span>  
  
 <span data-ttu-id="f0edc-112">XPath 運算式存在於字串內的隔離中。</span><span class="sxs-lookup"><span data-stu-id="f0edc-112">XPath expressions exist in isolation within a string.</span></span> <span data-ttu-id="f0edc-113">C# 編譯器在編譯時期無法協助剖析 XPath 運算式。</span><span class="sxs-lookup"><span data-stu-id="f0edc-113">The C# compiler cannot help parse the XPath expression at compile time.</span></span> <span data-ttu-id="f0edc-114">相較之下，C# 編譯器會剖析與編譯 LINQ to XML 查詢。</span><span class="sxs-lookup"><span data-stu-id="f0edc-114">By contrast, LINQ to XML queries are parsed and compiled by the C# compiler.</span></span> <span data-ttu-id="f0edc-115">該編譯器可以擷取許多查詢錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0edc-115">The compiler is able to catch many query errors.</span></span>  
  
 <span data-ttu-id="f0edc-116">XPath 結果不是強型別 (Strongly Typed)。</span><span class="sxs-lookup"><span data-stu-id="f0edc-116">XPath results are not strongly typed.</span></span> <span data-ttu-id="f0edc-117">在許多情況下，評估 XPath 運算式的結果不是物件，而且開發人員可以決定適當的型別，並在必要時轉換結果。</span><span class="sxs-lookup"><span data-stu-id="f0edc-117">In a number of circumstances, the result of evaluating an XPath expression is an object, and it is up to the developer to determine the proper type and cast the result as necessary.</span></span> <span data-ttu-id="f0edc-118">相較之下，LINQ to XML 查詢的評估為強型別。</span><span class="sxs-lookup"><span data-stu-id="f0edc-118">By contrast, the projections from a LINQ to XML query are strongly typed.</span></span>  
  
## <a name="result-ordering"></a><span data-ttu-id="f0edc-119">結果順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-119">Result Ordering</span></span>  
 <span data-ttu-id="f0edc-120">XPath 1.0 建議事項說明評估 XPath 運算式之結果的集合沒有排序。</span><span class="sxs-lookup"><span data-stu-id="f0edc-120">The XPath 1.0 Recommendation states that a collection that is the result of evaluating an XPath expression is unordered.</span></span>  
  
 <span data-ttu-id="f0edc-121">不過，逐一查看由 LINQ to XML XPath 軸方法傳回的集合時，會以文件順序傳回集合中的節點。</span><span class="sxs-lookup"><span data-stu-id="f0edc-121">However, when iterating through a collection returned by a LINQ to XML XPath axis method, the nodes in the collection are returned in document order.</span></span> <span data-ttu-id="f0edc-122">即使在存取 XPath 軸 (其中的述詞會根據反向的文件順序表示，例如，`preceding` 和 `preceding-sibling`) 時，也是如此。</span><span class="sxs-lookup"><span data-stu-id="f0edc-122">This is the case even when accessing the XPath axes where predicates are expressed in terms of reverse document order, such as `preceding` and `preceding-sibling`.</span></span>  
  
 <span data-ttu-id="f0edc-123">相較之下，大部分的 LINQ to XML 軸會以文件順序傳回集合，但其中兩個 (<xref:System.Xml.Linq.XNode.Ancestors%2A> 和 <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>) 會以反向的文件順序傳回集合。</span><span class="sxs-lookup"><span data-stu-id="f0edc-123">By contrast, most of the LINQ to XML axes return collections in document order, but two of them, <xref:System.Xml.Linq.XNode.Ancestors%2A> and <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>, return collections in reverse document order.</span></span> <span data-ttu-id="f0edc-124">下表列舉座標軸，並指出每個座標軸的集合順序：</span><span class="sxs-lookup"><span data-stu-id="f0edc-124">The following table enumerates the axes, and indicates collection order for each:</span></span>  
  
|<span data-ttu-id="f0edc-125">LINQ to XML 軸</span><span class="sxs-lookup"><span data-stu-id="f0edc-125">LINQ to XML axis</span></span>|<span data-ttu-id="f0edc-126">排序</span><span class="sxs-lookup"><span data-stu-id="f0edc-126">Ordering</span></span>|  
|----------------------|--------------|  
|<span data-ttu-id="f0edc-127">XContainer.DescendantNodes</span><span class="sxs-lookup"><span data-stu-id="f0edc-127">XContainer.DescendantNodes</span></span>|<span data-ttu-id="f0edc-128">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-128">Document order</span></span>|  
|<span data-ttu-id="f0edc-129">XContainer.Descendants</span><span class="sxs-lookup"><span data-stu-id="f0edc-129">XContainer.Descendants</span></span>|<span data-ttu-id="f0edc-130">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-130">Document order</span></span>|  
|<span data-ttu-id="f0edc-131">XContainer.Elements</span><span class="sxs-lookup"><span data-stu-id="f0edc-131">XContainer.Elements</span></span>|<span data-ttu-id="f0edc-132">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-132">Document order</span></span>|  
|<span data-ttu-id="f0edc-133">XContainer.Nodes</span><span class="sxs-lookup"><span data-stu-id="f0edc-133">XContainer.Nodes</span></span>|<span data-ttu-id="f0edc-134">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-134">Document order</span></span>|  
|<span data-ttu-id="f0edc-135">XContainer.NodesAfterSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-135">XContainer.NodesAfterSelf</span></span>|<span data-ttu-id="f0edc-136">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-136">Document order</span></span>|  
|<span data-ttu-id="f0edc-137">XContainer.NodesBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-137">XContainer.NodesBeforeSelf</span></span>|<span data-ttu-id="f0edc-138">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-138">Document order</span></span>|  
|<span data-ttu-id="f0edc-139">XElement.AncestorsAndSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-139">XElement.AncestorsAndSelf</span></span>|<span data-ttu-id="f0edc-140">反向的文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-140">Reverse document order</span></span>|  
|<span data-ttu-id="f0edc-141">XElement.Attributes</span><span class="sxs-lookup"><span data-stu-id="f0edc-141">XElement.Attributes</span></span>|<span data-ttu-id="f0edc-142">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-142">Document order</span></span>|  
|<span data-ttu-id="f0edc-143">XElement.DescendantNodesAndSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-143">XElement.DescendantNodesAndSelf</span></span>|<span data-ttu-id="f0edc-144">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-144">Document order</span></span>|  
|<span data-ttu-id="f0edc-145">XElement.DescendantsAndSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-145">XElement.DescendantsAndSelf</span></span>|<span data-ttu-id="f0edc-146">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-146">Document order</span></span>|  
|<span data-ttu-id="f0edc-147">XNode.Ancestors</span><span class="sxs-lookup"><span data-stu-id="f0edc-147">XNode.Ancestors</span></span>|<span data-ttu-id="f0edc-148">反向的文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-148">Reverse document order</span></span>|  
|<span data-ttu-id="f0edc-149">XNode.ElementsAfterSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-149">XNode.ElementsAfterSelf</span></span>|<span data-ttu-id="f0edc-150">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-150">Document order</span></span>|  
|<span data-ttu-id="f0edc-151">XNode.ElementsBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-151">XNode.ElementsBeforeSelf</span></span>|<span data-ttu-id="f0edc-152">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-152">Document order</span></span>|  
|<span data-ttu-id="f0edc-153">XNode.NodesAfterSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-153">XNode.NodesAfterSelf</span></span>|<span data-ttu-id="f0edc-154">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-154">Document order</span></span>|  
|<span data-ttu-id="f0edc-155">XNode.NodesBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="f0edc-155">XNode.NodesBeforeSelf</span></span>|<span data-ttu-id="f0edc-156">文件順序</span><span class="sxs-lookup"><span data-stu-id="f0edc-156">Document order</span></span>|  
  
## <a name="positional-predicates"></a><span data-ttu-id="f0edc-157">位置性述詞</span><span class="sxs-lookup"><span data-stu-id="f0edc-157">Positional Predicates</span></span>  
 <span data-ttu-id="f0edc-158">在 XPath 運算式內，許多座標軸的位置性述詞都是以文件順序表示，但是反向座標軸則以反向的文件順序表示，這些反向座標軸包括 `preceding`、`preceding-sibling`、`ancestor` 和 `ancestor-or-self`。</span><span class="sxs-lookup"><span data-stu-id="f0edc-158">Within an XPath expression, positional predicates are expressed in terms of document order for many axes, but are expressed in reverse document order for reverse axes, which are `preceding`, `preceding-sibling`, `ancestor`, and `ancestor-or-self`.</span></span> <span data-ttu-id="f0edc-159">例如，XPath 運算式 `preceding-sibling::*[1]` 會傳回正前面的同層級。</span><span class="sxs-lookup"><span data-stu-id="f0edc-159">For example, the XPath expression `preceding-sibling::*[1]` returns the immediately preceding sibling.</span></span> <span data-ttu-id="f0edc-160">即使最後的結果集會以文件順序呈現，也是如此。</span><span class="sxs-lookup"><span data-stu-id="f0edc-160">This is the case even though the final result set is presented in document order.</span></span>  
  
 <span data-ttu-id="f0edc-161">相較之下，LINQ to XML 中的所有位置性述詞都一律會以座標軸的順序表示。</span><span class="sxs-lookup"><span data-stu-id="f0edc-161">By contrast, all positional predicates in LINQ to XML are always expressed in terms of the order of the axis.</span></span> <span data-ttu-id="f0edc-162">例如，`anElement.ElementsBeforeSelf().ElementAt(0)` 會傳回所查詢項目之父代的第一個子項目，而非正前面的同層級。</span><span class="sxs-lookup"><span data-stu-id="f0edc-162">For example, `anElement.ElementsBeforeSelf().ElementAt(0)` returns the first child element of the parent of the queried element, not the immediate preceding sibling.</span></span> <span data-ttu-id="f0edc-163">另一個範例：`anElement.Ancestors().ElementAt(0)` 會傳回父項目。</span><span class="sxs-lookup"><span data-stu-id="f0edc-163">Another example: `anElement.Ancestors().ElementAt(0)` returns the parent element.</span></span>  
  
 <span data-ttu-id="f0edc-164">如果您要在 LINQ to XML 中尋找正前面的項目，您可以撰寫下列運算式：</span><span class="sxs-lookup"><span data-stu-id="f0edc-164">If you wanted to find the immediately preceding element in LINQ to XML, you would write the following expression:</span></span>  
  
```csharp
ElementsBeforeSelf().Last()
```
  
```vb
ElementsBeforeSelf().Last()
```
  
## <a name="performance-differences"></a><span data-ttu-id="f0edc-165">效能差異</span><span class="sxs-lookup"><span data-stu-id="f0edc-165">Performance Differences</span></span>  
 <span data-ttu-id="f0edc-166">在 LINQ to XML 中使用 XPath 功能的 XPath 查詢，其執行效能不及 LINQ to XML 查詢。</span><span class="sxs-lookup"><span data-stu-id="f0edc-166">XPath queries that use the XPath functionality in LINQ to XML will not perform as well as LINQ to XML queries.</span></span>  
  
## <a name="comparison-of-composition"></a><span data-ttu-id="f0edc-167">撰寫比較</span><span class="sxs-lookup"><span data-stu-id="f0edc-167">Comparison of Composition</span></span>  
 <span data-ttu-id="f0edc-168">撰寫 LINQ to XML 查詢與撰寫 XPath 運算式類似，但是在語法上非常不同。</span><span class="sxs-lookup"><span data-stu-id="f0edc-168">Composition of a LINQ to XML query is somewhat parallel to composition of an XPath expression, although very different in syntax.</span></span>  
  
 <span data-ttu-id="f0edc-169">例如，如果您在變數中有一個名稱為 `customers` 的項目，而且您想要在名稱為 `CompanyName` 的所有子項目下，尋找名稱為 `Customer` 的後代子項目，您可以撰寫 XPath 運算式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f0edc-169">For example, if you have an element in a variable named `customers`, and you want to find a grandchild element named `CompanyName` under all child elements named `Customer`, you would write an XPath expression as follows:</span></span>  
  
```csharp  
customers.XPathSelectElements("./Customer/CompanyName")
```  
  
```vb
customers.XPathSelectElements("./Customer/CompanyName")
```

 <span data-ttu-id="f0edc-170">對等的 LINQ to XML 查詢為：</span><span class="sxs-lookup"><span data-stu-id="f0edc-170">The equivalent LINQ to XML query is:</span></span>  
  
```csharp  
customers.Elements("Customer").Elements("CompanyName")
```  
  
```vb
customers.Elements("Customer").Elements("CompanyName")
```  

 <span data-ttu-id="f0edc-171">每個 XPath 座標軸都有類似的項目。</span><span class="sxs-lookup"><span data-stu-id="f0edc-171">There are similar parallels for each of the XPath axes.</span></span>  
  
|<span data-ttu-id="f0edc-172">XPath 座標軸</span><span class="sxs-lookup"><span data-stu-id="f0edc-172">XPath axis</span></span>|<span data-ttu-id="f0edc-173">LINQ to XML 軸</span><span class="sxs-lookup"><span data-stu-id="f0edc-173">LINQ to XML axis</span></span>|  
|----------------|----------------------|  
|<span data-ttu-id="f0edc-174">child (預設軸)</span><span class="sxs-lookup"><span data-stu-id="f0edc-174">child (the default axis)</span></span>|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-175">Parent (..)</span><span class="sxs-lookup"><span data-stu-id="f0edc-175">Parent (..)</span></span>|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-176">attribute 軸 (@)</span><span class="sxs-lookup"><span data-stu-id="f0edc-176">attribute axis (@)</span></span>|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType><br /><br /> <span data-ttu-id="f0edc-177">或</span><span class="sxs-lookup"><span data-stu-id="f0edc-177">or</span></span><br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-178">ancestor 軸</span><span class="sxs-lookup"><span data-stu-id="f0edc-178">ancestor axis</span></span>|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-179">ancestor-or-self 軸</span><span class="sxs-lookup"><span data-stu-id="f0edc-179">ancestor-or-self axis</span></span>|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-180">descendant 軸 (//)</span><span class="sxs-lookup"><span data-stu-id="f0edc-180">descendant axis (//)</span></span>|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType><br /><br /> <span data-ttu-id="f0edc-181">或</span><span class="sxs-lookup"><span data-stu-id="f0edc-181">or</span></span><br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-182">descendant-or-self</span><span class="sxs-lookup"><span data-stu-id="f0edc-182">descendant-or-self</span></span>|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType><br /><br /> <span data-ttu-id="f0edc-183">或</span><span class="sxs-lookup"><span data-stu-id="f0edc-183">or</span></span><br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-184">following-sibling</span><span class="sxs-lookup"><span data-stu-id="f0edc-184">following-sibling</span></span>|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType><br /><br /> <span data-ttu-id="f0edc-185">或</span><span class="sxs-lookup"><span data-stu-id="f0edc-185">or</span></span><br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-186">preceding-sibling</span><span class="sxs-lookup"><span data-stu-id="f0edc-186">preceding-sibling</span></span>|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType><br /><br /> <span data-ttu-id="f0edc-187">或</span><span class="sxs-lookup"><span data-stu-id="f0edc-187">or</span></span><br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="f0edc-188">following</span><span class="sxs-lookup"><span data-stu-id="f0edc-188">following</span></span>|<span data-ttu-id="f0edc-189">沒有直接的對等。</span><span class="sxs-lookup"><span data-stu-id="f0edc-189">No direct equivalent.</span></span>|  
|<span data-ttu-id="f0edc-190">preceding</span><span class="sxs-lookup"><span data-stu-id="f0edc-190">preceding</span></span>|<span data-ttu-id="f0edc-191">沒有直接的對等。</span><span class="sxs-lookup"><span data-stu-id="f0edc-191">No direct equivalent.</span></span>|  
  
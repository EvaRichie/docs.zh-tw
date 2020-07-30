---
title: 從 XML 樹狀結構移除項目、屬性和節點 (C#)
description: 瞭解如何從 XML 樹狀結構移除專案、屬性和節點。 查看移除方法和程式碼範例的清單。
ms.date: 07/20/2015
ms.assetid: 07dd06d6-1117-4077-bf98-9120cf51176e
ms.openlocfilehash: 4e753c3d96c4cbc050b08076ca8bff8c17b2e252
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87300042"
---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-c"></a><span data-ttu-id="d9c19-104">從 XML 樹狀結構移除項目、屬性和節點 (C#)</span><span class="sxs-lookup"><span data-stu-id="d9c19-104">Removing Elements, Attributes, and Nodes from an XML Tree (C#)</span></span>

<span data-ttu-id="d9c19-105">您可以修改 XML 樹狀以移除項目、屬性以及其他類型的節點。</span><span class="sxs-lookup"><span data-stu-id="d9c19-105">You can modify an XML tree, removing elements, attributes, and other types of nodes.</span></span>

<span data-ttu-id="d9c19-106">從 XML 文件移除單一項目或單一屬性很直接。</span><span class="sxs-lookup"><span data-stu-id="d9c19-106">Removing a single element or a single attribute from an XML document is straightforward.</span></span> <span data-ttu-id="d9c19-107">不過，移除項目或屬性的集合時，您應該先將集合具體化到清單中，然後從清單中刪除項目或屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c19-107">However, when removing collections of elements or attributes, you should first materialize a collection into a list, and then delete the elements or attributes from the list.</span></span> <span data-ttu-id="d9c19-108">最好的方法是，使用 <xref:System.Xml.Linq.Extensions.Remove%2A> 擴充方法替您執行。</span><span class="sxs-lookup"><span data-stu-id="d9c19-108">The best approach is to use the <xref:System.Xml.Linq.Extensions.Remove%2A> extension method, which will do this for you.</span></span>

<span data-ttu-id="d9c19-109">這麼做的主要原因是因為您從 XML 樹狀結構中擷取的大部分集合都是使用延後執行產生的。</span><span class="sxs-lookup"><span data-stu-id="d9c19-109">The main reason for doing this is that most of the collections you retrieve from an XML tree are yielded using deferred execution.</span></span> <span data-ttu-id="d9c19-110">如果您沒有先將這些集合具體化到清單中，或沒有使用擴充方法，則可能發生特定類別的 Bug。</span><span class="sxs-lookup"><span data-stu-id="d9c19-110">If you do not first materialize them into a list, or if you do not use the extension methods, it is possible to encounter a certain class of bugs.</span></span> <span data-ttu-id="d9c19-111">如需詳細資訊，請參閱[混合的宣告式程式碼/命令式程式碼 Bug (LINQ to XML) (C#)](./mixed-declarative-code-imperative-code-bugs-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="d9c19-111">For more information, see [Mixed Declarative Code/Imperative Code Bugs (LINQ to XML) (C#)](./mixed-declarative-code-imperative-code-bugs-linq-to-xml.md).</span></span>

<span data-ttu-id="d9c19-112">下列方法會從 XML 樹狀移除節點和屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c19-112">The following methods remove nodes and attributes from an XML tree.</span></span>

|<span data-ttu-id="d9c19-113">方法</span><span class="sxs-lookup"><span data-stu-id="d9c19-113">Method</span></span>|<span data-ttu-id="d9c19-114">說明</span><span class="sxs-lookup"><span data-stu-id="d9c19-114">Description</span></span>|
|------------|-----------------|
|<xref:System.Xml.Linq.XAttribute.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-115">從其父代移除 <xref:System.Xml.Linq.XAttribute>。</span><span class="sxs-lookup"><span data-stu-id="d9c19-115">Removes an <xref:System.Xml.Linq.XAttribute> from its parent.</span></span>|
|<xref:System.Xml.Linq.XContainer.RemoveNodes%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-116">從 <xref:System.Xml.Linq.XContainer> 移除子節點。</span><span class="sxs-lookup"><span data-stu-id="d9c19-116">Removes the child nodes from an <xref:System.Xml.Linq.XContainer>.</span></span>|
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-117">從 <xref:System.Xml.Linq.XElement> 移除內容和屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c19-117">Removes content and attributes from an <xref:System.Xml.Linq.XElement>.</span></span>|
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-118">移除 <xref:System.Xml.Linq.XElement> 的屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c19-118">Removes the attributes of an <xref:System.Xml.Linq.XElement>.</span></span>|
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-119">如果您針對值傳遞 `null`，則會移除屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c19-119">If you pass `null` for value, then removes the attribute.</span></span>|
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-120">如果您針對值傳遞 `null`，則會移除子項目。</span><span class="sxs-lookup"><span data-stu-id="d9c19-120">If you pass `null` for value, then removes the child element.</span></span>|
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-121">從其父代移除 <xref:System.Xml.Linq.XNode>。</span><span class="sxs-lookup"><span data-stu-id="d9c19-121">Removes an <xref:System.Xml.Linq.XNode> from its parent.</span></span>|
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="d9c19-122">從其父項目移除來源集合中的每個屬性或項目。</span><span class="sxs-lookup"><span data-stu-id="d9c19-122">Removes every attribute or element in the source collection from its parent element.</span></span>|

## <a name="example"></a><span data-ttu-id="d9c19-123">範例</span><span class="sxs-lookup"><span data-stu-id="d9c19-123">Example</span></span>

### <a name="description"></a><span data-ttu-id="d9c19-124">描述</span><span class="sxs-lookup"><span data-stu-id="d9c19-124">Description</span></span>

<span data-ttu-id="d9c19-125">這個範例會示範三種移除項目的方法。</span><span class="sxs-lookup"><span data-stu-id="d9c19-125">This example demonstrates three approaches to removing elements.</span></span> <span data-ttu-id="d9c19-126">首先，它會移除單一項目。</span><span class="sxs-lookup"><span data-stu-id="d9c19-126">First, it removes a single element.</span></span> <span data-ttu-id="d9c19-127">接著，它會反覆運算項目的集合，使用 <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> 運算子具體化它們，然後移除集合。</span><span class="sxs-lookup"><span data-stu-id="d9c19-127">Second, it retrieves a collection of elements, materializes them using the <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> operator, and removes the collection.</span></span> <span data-ttu-id="d9c19-128">最後，它會擷取項目的集合，並使用 <xref:System.Xml.Linq.Extensions.Remove%2A> 擴充方法加以移除。</span><span class="sxs-lookup"><span data-stu-id="d9c19-128">Finally, it retrieves a collection of elements and removes them using the <xref:System.Xml.Linq.Extensions.Remove%2A> extension method.</span></span>

<span data-ttu-id="d9c19-129">如需 <xref:System.Linq.Enumerable.ToList%2A> 運算子的詳細資訊，請參閱[轉換資料類型 (C#)](./converting-data-types.md)。</span><span class="sxs-lookup"><span data-stu-id="d9c19-129">For more information on the <xref:System.Linq.Enumerable.ToList%2A> operator, see [Converting Data Types (C#)](./converting-data-types.md).</span></span>

### <a name="code"></a><span data-ttu-id="d9c19-130">程式碼</span><span class="sxs-lookup"><span data-stu-id="d9c19-130">Code</span></span>

```csharp
XElement root = XElement.Parse(@"<Root>
    <Child1>
        <GrandChild1/>
        <GrandChild2/>
        <GrandChild3/>
    </Child1>
    <Child2>
        <GrandChild4/>
        <GrandChild5/>
        <GrandChild6/>
    </Child2>
    <Child3>
        <GrandChild7/>
        <GrandChild8/>
        <GrandChild9/>
    </Child3>
</Root>");
root.Element("Child1").Element("GrandChild1").Remove();
root.Element("Child2").Elements().ToList().Remove();
root.Element("Child3").Elements().Remove();
Console.WriteLine(root);
```

### <a name="comments"></a><span data-ttu-id="d9c19-131">註解</span><span class="sxs-lookup"><span data-stu-id="d9c19-131">Comments</span></span>

<span data-ttu-id="d9c19-132">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d9c19-132">This code produces the following output:</span></span>

```xml
<Root>
  <Child1>
    <GrandChild2 />
    <GrandChild3 />
  </Child1>
  <Child2 />
  <Child3 />
</Root>
```

<span data-ttu-id="d9c19-133">請注意，第一個後代子項目已從 `Child1` 移除。</span><span class="sxs-lookup"><span data-stu-id="d9c19-133">Notice that the first grandchild element has been removed from `Child1`.</span></span> <span data-ttu-id="d9c19-134">所有後代子項目都已經從 `Child2` 和 `Child3` 移除。</span><span class="sxs-lookup"><span data-stu-id="d9c19-134">All grandchildren elements have been removed from `Child2` and from `Child3`.</span></span>

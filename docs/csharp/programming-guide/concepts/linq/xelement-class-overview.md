---
title: XElement 類別概觀 (C#)
description: 'System.xml.linq.xelement> 類別代表 c # 中的 XML 元素。 這是 LINQ to XML 中的其中一個基礎類別。 瞭解 System.xml.linq.xelement> 所提供的功能。'
ms.date: 07/20/2015
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
ms.openlocfilehash: f76f51703de054443f47531294777b43a9c0b004
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302174"
---
# <a name="xelement-class-overview-c"></a><span data-ttu-id="b1e2e-105">XElement 類別概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1e2e-105">XElement Class Overview (C#)</span></span>
<span data-ttu-id="b1e2e-106"><xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的其中一個基本類別。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-106">The <xref:System.Xml.Linq.XElement> class is one of the fundamental classes in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span> <span data-ttu-id="b1e2e-107">它代表 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-107">It represents an XML element.</span></span> <span data-ttu-id="b1e2e-108">您可以使用這個類別來建立項目；變更項目的內容；加入、變更或刪除子項目；將屬性加入到項目中；或以文字格式序列化項目的內容。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-108">You can use this class to create elements; change the content of the element; add, change, or delete child elements; add attributes to an element; or serialize the contents of an element in text form.</span></span> <span data-ttu-id="b1e2e-109">您也可以與 <xref:System.Xml?displayProperty=nameWithType> 中的其他類別相互溝通，例如，<xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.Xsl.XslCompiledTransform>。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-109">You can also interoperate with other classes in <xref:System.Xml?displayProperty=nameWithType>, such as <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>, and <xref:System.Xml.Xsl.XslCompiledTransform>.</span></span>  
  
<span data-ttu-id="b1e2e-110">本主題描述 <xref:System.Xml.Linq.XElement> 類別提供的功能。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-110">This topic describes the functionality provided by the <xref:System.Xml.Linq.XElement> class.</span></span>  
  
## <a name="constructing-xml-trees"></a><span data-ttu-id="b1e2e-111">建構 XML 樹狀結構</span><span class="sxs-lookup"><span data-stu-id="b1e2e-111">Constructing XML Trees</span></span>  
 <span data-ttu-id="b1e2e-112">您可以用各種方式建構 XML 樹狀結構，包括：</span><span class="sxs-lookup"><span data-stu-id="b1e2e-112">You can construct XML trees in a variety of ways, including the following:</span></span>  
  
- <span data-ttu-id="b1e2e-113">您可以在程式碼中建構 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-113">You can construct an XML tree in code.</span></span> <span data-ttu-id="b1e2e-114">如需詳細資訊，請參閱[建立 XML 樹狀結構 (C#)](./linq-to-xml-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-114">For more information, see [Creating XML Trees (C#)](./linq-to-xml-overview.md).</span></span>  
  
- <span data-ttu-id="b1e2e-115">您可以剖析來自各種來源的 XML，包括 <xref:System.IO.TextReader>、文字檔或網路位址 (URL)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-115">You can parse XML from various sources, including a <xref:System.IO.TextReader>, text files, or a Web address (URL).</span></span> <span data-ttu-id="b1e2e-116">如需詳細資訊，請參閱[剖析 XML (C#)](./how-to-parse-a-string.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-116">For more information, see [Parsing XML (C#)](./how-to-parse-a-string.md).</span></span>  
  
- <span data-ttu-id="b1e2e-117">您可以使用 <xref:System.Xml.XmlReader> 來填入樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-117">You can use an <xref:System.Xml.XmlReader> to populate the tree.</span></span> <span data-ttu-id="b1e2e-118">如需詳細資訊，請參閱 <xref:System.Xml.Linq.XNode.ReadFrom%2A>。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-118">For more information, see <xref:System.Xml.Linq.XNode.ReadFrom%2A>.</span></span>  
  
- <span data-ttu-id="b1e2e-119">如果您擁有的模組可以將內容寫入到 <xref:System.Xml.XmlWriter>，您可以使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 方法來建立寫入器、將寫入器傳遞到模組，然後使用寫入到 <xref:System.Xml.XmlWriter> 的內容填入 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-119">If you have a module that can write content to an <xref:System.Xml.XmlWriter>, you can use the <xref:System.Xml.Linq.XContainer.CreateWriter%2A> method to create a writer, pass the writer to the module, and then use the content that is written to the <xref:System.Xml.XmlWriter> to populate the XML tree.</span></span>  
  
 <span data-ttu-id="b1e2e-120">不過，建立 XML 樹狀結構最常見的方式為下：</span><span class="sxs-lookup"><span data-stu-id="b1e2e-120">However, the most common way to create an XML tree is as follows:</span></span>  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 <span data-ttu-id="b1e2e-121">建立 XML 樹狀結構的另一個非常常見的技術，包括使用 LINQ 查詢的結果來填入 XML 樹狀結構，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b1e2e-121">Another very common technique for creating an XML tree involves using the results of a LINQ query to populate an XML tree, as shown in the following example:</span></span>  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
```  
  
 <span data-ttu-id="b1e2e-122">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="b1e2e-122">This example produces the following output:</span></span>  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="serializing-xml-trees"></a><span data-ttu-id="b1e2e-123">序列化 XML 樹狀結構</span><span class="sxs-lookup"><span data-stu-id="b1e2e-123">Serializing XML Trees</span></span>  
 <span data-ttu-id="b1e2e-124">您可以將 XML 樹狀結構序列化至 <xref:System.IO.File>、<xref:System.IO.TextWriter> 或 <xref:System.Xml.XmlWriter>。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-124">You can serialize the XML tree to a <xref:System.IO.File>, a <xref:System.IO.TextWriter>, or an <xref:System.Xml.XmlWriter>.</span></span>  
  
 <span data-ttu-id="b1e2e-125">如需詳細資訊，請參閱[序列化 XML 樹狀結構 (C#)](./preserving-white-space-while-serializing.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-125">For more information, see [Serializing XML Trees (C#)](./preserving-white-space-while-serializing.md).</span></span>  
  
## <a name="retrieving-xml-data-via-axis-methods"></a><span data-ttu-id="b1e2e-126">透過座標軸方法擷取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="b1e2e-126">Retrieving XML Data via Axis Methods</span></span>  
 <span data-ttu-id="b1e2e-127">您可以使用座標軸方法來擷取屬性、子項目、子系項目以及祖系項目。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-127">You can use axis methods to retrieve attributes, child elements, descendant elements, and ancestor elements.</span></span> <span data-ttu-id="b1e2e-128">LINQ 查詢會在座標軸方法上運作，並提供數個彈性且功能強大的方式來流覽和處理 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-128">LINQ queries operate on axis methods, and provide several flexible and powerful ways to navigate through and process an XML tree.</span></span>  
  
 <span data-ttu-id="b1e2e-129">如需詳細資訊，請參閱 [LINQ to XML 座標軸 (C#)](./linq-to-xml-axes-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-129">For more information, see [LINQ to XML Axes (C#)](./linq-to-xml-axes-overview.md).</span></span>  
  
## <a name="querying-xml-trees"></a><span data-ttu-id="b1e2e-130">查詢 XML 樹狀</span><span class="sxs-lookup"><span data-stu-id="b1e2e-130">Querying XML Trees</span></span>  
 <span data-ttu-id="b1e2e-131">您可以撰寫從 XML 樹狀結構中解壓縮資料的 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-131">You can write LINQ queries that extract data from an XML tree.</span></span>  
  
 <span data-ttu-id="b1e2e-132">如需詳細資訊，請參閱[查詢 XML 樹狀結構 (C#)](./how-to-find-an-element-with-a-specific-attribute.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-132">For more information, see [Querying XML Trees (C#)](./how-to-find-an-element-with-a-specific-attribute.md).</span></span>  
  
## <a name="modifying-xml-trees"></a><span data-ttu-id="b1e2e-133">修改 XML 樹狀</span><span class="sxs-lookup"><span data-stu-id="b1e2e-133">Modifying XML Trees</span></span>  
 <span data-ttu-id="b1e2e-134">您可以用各種方式修改項目，包括變更其內容或屬性。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-134">You can modify an element in a variety of ways, including changing its content or attributes.</span></span> <span data-ttu-id="b1e2e-135">您也可以從其父代移除項目。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-135">You can also remove an element from its parent.</span></span>  
  
 <span data-ttu-id="b1e2e-136">如需詳細資訊，請參閱[修改 XML 樹狀結構 (LINQ to XML) (C#)](./in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e2e-136">For more information, see [Modifying XML Trees (LINQ to XML) (C#)](./in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b1e2e-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b1e2e-137">See also</span></span>

- [<span data-ttu-id="b1e2e-138">LINQ to XML 程式設計概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1e2e-138">LINQ to XML Programming Overview (C#)</span></span>](serializing-to-files-textwriters-and-xmlwriters.md)

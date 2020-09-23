---
title: XML 常值概觀
ms.date: 07/20/2015
helpviewer_keywords:
- XML literals [Visual Basic], about XML literals
- declaring XML literals [Visual Basic]
- LINQ to XML [Visual Basic], XML literals
- literals [Visual Basic], XML
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
ms.openlocfilehash: c65cac4f6e8f5f314587f20d5c373c92ea0c51e5
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91085382"
---
# <a name="xml-literals-overview-visual-basic"></a><span data-ttu-id="27bcb-102">XML 常值概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="27bcb-102">XML Literals Overview (Visual Basic)</span></span>

<span data-ttu-id="27bcb-103">*Xml 常*值可讓您將 xml 直接併入 Visual Basic 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="27bcb-103">An *XML literal* allows you to incorporate XML directly into your Visual Basic code.</span></span> <span data-ttu-id="27bcb-104">XML 常值語法代表 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 物件，它類似于 XML 1.0 語法。</span><span class="sxs-lookup"><span data-stu-id="27bcb-104">The XML literal syntax represents [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] objects, and it is the similar to the XML 1.0 syntax.</span></span> <span data-ttu-id="27bcb-105">這可讓您更輕鬆地以程式設計方式建立 XML 元素和檔，因為您的程式碼與最後一個 XML 具有相同的結構。</span><span class="sxs-lookup"><span data-stu-id="27bcb-105">This makes it easier to create XML elements and documents programmatically because your code has the same structure as the final XML.</span></span>  
  
 <span data-ttu-id="27bcb-106">Visual Basic 將 XML 常值編譯為 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 物件。</span><span class="sxs-lookup"><span data-stu-id="27bcb-106">Visual Basic compiles XML literals into [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] objects.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="27bcb-107">提供簡單的物件模型，可用於建立和操作 XML，此模型會與 (LINQ) 的語言整合式查詢妥善整合。</span><span class="sxs-lookup"><span data-stu-id="27bcb-107">provides a simple object model for creating and manipulating XML, and this model integrates well with Language-Integrated Query (LINQ).</span></span> <span data-ttu-id="27bcb-108">如需詳細資訊，請參閱<xref:System.Xml.Linq.XElement>。</span><span class="sxs-lookup"><span data-stu-id="27bcb-108">For more information, see <xref:System.Xml.Linq.XElement>.</span></span>  
  
 <span data-ttu-id="27bcb-109">您可以在 XML 常值中內嵌 Visual Basic 運算式。</span><span class="sxs-lookup"><span data-stu-id="27bcb-109">You can embed a Visual Basic expression in an XML literal.</span></span> <span data-ttu-id="27bcb-110">在執行時間，您的應用程式會 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 為每個常值建立一個物件，其中包含內嵌運算式的值。</span><span class="sxs-lookup"><span data-stu-id="27bcb-110">At run time, your application creates a [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object for each literal, incorporating the values of the embedded expressions.</span></span> <span data-ttu-id="27bcb-111">這可讓您在 XML 常值內指定動態內容。</span><span class="sxs-lookup"><span data-stu-id="27bcb-111">This lets you specify dynamic content inside an XML literal.</span></span> <span data-ttu-id="27bcb-112">如需詳細資訊，請參閱 [XML 中的內嵌運算式](embedded-expressions-in-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="27bcb-112">For more information, see [Embedded Expressions in XML](embedded-expressions-in-xml.md).</span></span>  
  
 <span data-ttu-id="27bcb-113">如需 XML 常值語法和 XML 1.0 語法之間差異的詳細資訊，請參閱 [Xml 常值和 xml 1.0 規格](xml-literals-and-the-xml-1-0-specification.md)。</span><span class="sxs-lookup"><span data-stu-id="27bcb-113">For more information about the differences between the XML literal syntax and the XML 1.0 syntax, see [XML Literals and the XML 1.0 Specification](xml-literals-and-the-xml-1-0-specification.md).</span></span>  
  
## <a name="simple-literals"></a><span data-ttu-id="27bcb-114">簡單常值</span><span class="sxs-lookup"><span data-stu-id="27bcb-114">Simple Literals</span></span>  

 <span data-ttu-id="27bcb-115">您可以在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] Visual Basic 程式碼中，藉由輸入或貼上有效的 XML 來建立物件。</span><span class="sxs-lookup"><span data-stu-id="27bcb-115">You can create a [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object in your Visual Basic code by typing or pasting in valid XML.</span></span> <span data-ttu-id="27bcb-116">XML 元素常值會傳回 <xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="27bcb-116">An XML element literal returns an <xref:System.Xml.Linq.XElement> object.</span></span> <span data-ttu-id="27bcb-117">如需詳細資訊，請參閱 [Xml 元素常](../../../language-reference/xml-literals/xml-element-literal.md) 值和 [xml 常值和 xml 1.0 規格](xml-literals-and-the-xml-1-0-specification.md)。</span><span class="sxs-lookup"><span data-stu-id="27bcb-117">For more information, see [XML Element Literal](../../../language-reference/xml-literals/xml-element-literal.md) and [XML Literals and the XML 1.0 Specification](xml-literals-and-the-xml-1-0-specification.md).</span></span> <span data-ttu-id="27bcb-118">下列範例會建立具有多個子項目的 XML 專案。</span><span class="sxs-lookup"><span data-stu-id="27bcb-118">The following example creates an XML element that has several child elements.</span></span>  
  
 [!code-vb[VbXMLSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 <span data-ttu-id="27bcb-119">您可以使用啟動 XML 常值來建立 XML 檔 `<?xml version="1.0"?>` ，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="27bcb-119">You can create an XML document by starting an XML literal with `<?xml version="1.0"?>`, as shown in the following example.</span></span> <span data-ttu-id="27bcb-120">XML 檔常值會傳回 <xref:System.Xml.Linq.XDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="27bcb-120">An XML document literal returns an <xref:System.Xml.Linq.XDocument> object.</span></span> <span data-ttu-id="27bcb-121">如需詳細資訊，請參閱 [XML 檔常](../../../language-reference/xml-literals/xml-document-literal.md)值。</span><span class="sxs-lookup"><span data-stu-id="27bcb-121">For more information, see [XML Document Literal](../../../language-reference/xml-literals/xml-document-literal.md).</span></span>  
  
 [!code-vb[VbXMLSamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#6)]  
  
> [!NOTE]
> <span data-ttu-id="27bcb-122">Visual Basic 中的 XML 常值語法與 XML 1.0 規格中的語法不相同。</span><span class="sxs-lookup"><span data-stu-id="27bcb-122">The XML literal syntax in Visual Basic is not identical to the syntax in the XML 1.0 specification.</span></span> <span data-ttu-id="27bcb-123">如需詳細資訊，請參閱 [Xml 常值和 xml 1.0 規格](xml-literals-and-the-xml-1-0-specification.md)。</span><span class="sxs-lookup"><span data-stu-id="27bcb-123">For more information, see [XML Literals and the XML 1.0 Specification](xml-literals-and-the-xml-1-0-specification.md).</span></span>  
  
## <a name="line-continuation"></a><span data-ttu-id="27bcb-124">行接續</span><span class="sxs-lookup"><span data-stu-id="27bcb-124">Line Continuation</span></span>  

 <span data-ttu-id="27bcb-125">XML 常值可以跨多行，而不使用行接續字元 (空格-底線輸入順序) 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-125">An XML literal can span multiple lines without using line continuation characters (the space-underscore-enter sequence).</span></span> <span data-ttu-id="27bcb-126">這可讓您更輕鬆地將程式碼中的 XML 常值與 XML 檔比較。</span><span class="sxs-lookup"><span data-stu-id="27bcb-126">This makes it easier to compare XML literals in code with XML documents.</span></span>  
  
 <span data-ttu-id="27bcb-127">編譯器會將行接續字元視為 XML 常值的一部分。</span><span class="sxs-lookup"><span data-stu-id="27bcb-127">The compiler treats line continuation characters as part of an XML literal.</span></span> <span data-ttu-id="27bcb-128">因此，只有當它屬於物件時，才應該使用空格-底線輸入順序 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-128">Therefore, you should use the space-underscore-enter sequence only when it belongs in the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object.</span></span>  
  
 <span data-ttu-id="27bcb-129">但是，如果內嵌運算式中有多行運算式，則需要行接續字元。</span><span class="sxs-lookup"><span data-stu-id="27bcb-129">However, you do need line continuation characters if you have a multiline expression in an embedded expression.</span></span> <span data-ttu-id="27bcb-130">如需詳細資訊，請參閱 [XML 中的內嵌運算式](embedded-expressions-in-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="27bcb-130">For more information, see [Embedded Expressions in XML](embedded-expressions-in-xml.md).</span></span>  
  
## <a name="embedding-queries-in-xml-literals"></a><span data-ttu-id="27bcb-131">在 XML 常值中嵌入查詢</span><span class="sxs-lookup"><span data-stu-id="27bcb-131">Embedding Queries in XML Literals</span></span>  

 <span data-ttu-id="27bcb-132">您可以在內嵌運算式中使用查詢。</span><span class="sxs-lookup"><span data-stu-id="27bcb-132">You can use a query in an embedded expression.</span></span> <span data-ttu-id="27bcb-133">當您這樣做時，查詢所傳回的專案就會加入至 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="27bcb-133">When you do this, the elements returned by the query are added to the XML element.</span></span> <span data-ttu-id="27bcb-134">這可讓您將動態內容（例如使用者查詢的結果）新增至 XML 常值。</span><span class="sxs-lookup"><span data-stu-id="27bcb-134">This lets you add dynamic content, such as the result of a user's query, to an XML literal.</span></span>  
  
 <span data-ttu-id="27bcb-135">例如，下列程式碼會使用內嵌查詢從陣列的成員建立 XML 元素 `phoneNumbers2` ，然後將這些專案加入為的子系 `contact2` 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-135">For example, the following code uses an embedded query to create XML elements from the members of the `phoneNumbers2` array and then add those elements as children of `contact2`.</span></span>  
  
 [!code-vb[VbXMLSamples#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#7)]  
  
## <a name="how-the-compiler-creates-objects-from-xml-literals"></a><span data-ttu-id="27bcb-136">編譯器如何從 XML 常值建立物件</span><span class="sxs-lookup"><span data-stu-id="27bcb-136">How the Compiler Creates Objects from XML Literals</span></span>  

 <span data-ttu-id="27bcb-137">Visual Basic 編譯器會將 XML 常值轉譯為對等的函式的呼叫 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] ，以建立 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 物件。</span><span class="sxs-lookup"><span data-stu-id="27bcb-137">The Visual Basic compiler translates XML literals into calls to the equivalent [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] constructors to build up the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object.</span></span> <span data-ttu-id="27bcb-138">例如，Visual Basic 編譯器會將下列程式碼範例轉譯為 XML 版本指令的函式呼叫 <xref:System.Xml.Linq.XProcessingInstruction> 、呼叫、和專案的函式， <xref:System.Xml.Linq.XElement> 以及對 `<contact>` `<name>` `<phone>` <xref:System.Xml.Linq.XAttribute> `type` 屬性的函式的呼叫。</span><span class="sxs-lookup"><span data-stu-id="27bcb-138">For example, the Visual Basic compiler will translate the following code example into a call to the <xref:System.Xml.Linq.XProcessingInstruction> constructor for the XML version instruction, calls to the <xref:System.Xml.Linq.XElement> constructor for the `<contact>`, `<name>`, and `<phone>` elements, and calls to the <xref:System.Xml.Linq.XAttribute> constructor for the `type` attribute.</span></span> <span data-ttu-id="27bcb-139">明確地說，在下列範例中，Visual Basic 編譯器會呼叫兩次的函式 <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-139">Specifically, given the attributes in the following sample, the Visual Basic compiler will call the <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> constructor twice.</span></span> <span data-ttu-id="27bcb-140">第一個會傳遞參數的值 `type` `name` 和參數的值 `home` `value` 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-140">The first will pass the value `type` for the `name` parameter and the value `home` for the `value` parameter.</span></span> <span data-ttu-id="27bcb-141">第二個也會傳遞 `type` 參數的值 `name` ，但參數的值 `work` `value` 。</span><span class="sxs-lookup"><span data-stu-id="27bcb-141">The second will also pass the value `type` for the `name` parameter, but the value `work` for the `value` parameter.</span></span>  
  
 [!code-vb[VbXMLSamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#6)]  
  
## <a name="see-also"></a><span data-ttu-id="27bcb-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="27bcb-142">See also</span></span>

- <xref:System.Xml.Linq.XElement>
- [<span data-ttu-id="27bcb-143">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="27bcb-143">Creating XML in Visual Basic</span></span>](creating-xml.md)
- [<span data-ttu-id="27bcb-144">XML 中內嵌的運算式</span><span class="sxs-lookup"><span data-stu-id="27bcb-144">Embedded Expressions in XML</span></span>](embedded-expressions-in-xml.md)
- [<span data-ttu-id="27bcb-145">XML 文件常值</span><span class="sxs-lookup"><span data-stu-id="27bcb-145">XML Document Literal</span></span>](../../../language-reference/xml-literals/xml-document-literal.md)
- [<span data-ttu-id="27bcb-146">XML 元素常值</span><span class="sxs-lookup"><span data-stu-id="27bcb-146">XML Element Literal</span></span>](../../../language-reference/xml-literals/xml-element-literal.md)
- [<span data-ttu-id="27bcb-147">XML 常值</span><span class="sxs-lookup"><span data-stu-id="27bcb-147">XML Literals</span></span>](../../../language-reference/xml-literals/index.md)

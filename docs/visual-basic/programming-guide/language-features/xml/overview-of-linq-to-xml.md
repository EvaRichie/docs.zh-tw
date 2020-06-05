---
title: LINQ to XML 概觀
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
ms.openlocfilehash: 044aca634f5a0aa6e557a7dd9c0e1de64e35dc15
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374651"
---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a><span data-ttu-id="1ce8c-102">Visual Basic 中的 LINQ to XML 概觀</span><span class="sxs-lookup"><span data-stu-id="1ce8c-102">Overview of LINQ to XML in Visual Basic</span></span>
<span data-ttu-id="1ce8c-103">Visual Basic [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 透過 xml 常值和 xml 軸屬性來提供的支援。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-103">Visual Basic provides support for [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] through XML literals and XML axis properties.</span></span> <span data-ttu-id="1ce8c-104">這可讓您使用熟悉、方便的語法，在您的 Visual Basic 程式碼中使用 XML。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-104">This enables you to use a familiar, convenient syntax for working with XML in your Visual Basic code.</span></span> <span data-ttu-id="1ce8c-105">*Xml 常*值可讓您直接在程式碼中包含 xml。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-105">*XML literals* enable you to include XML directly in your code.</span></span> <span data-ttu-id="1ce8c-106">*Xml 軸屬性*可讓您存取子節點、子代節點，以及 xml 常值的屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-106">*XML axis properties* enable you to access child nodes, descendant nodes, and attributes of an XML literal.</span></span> <span data-ttu-id="1ce8c-107">如需詳細資訊，請參閱[Xml 常值總覽](xml-literals-overview.md)和[存取 VISUAL BASIC 中的 xml](accessing-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-107">For more information, see [XML Literals Overview](xml-literals-overview.md) and [Accessing XML in Visual Basic](accessing-xml.md).</span></span>  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<span data-ttu-id="1ce8c-108">是記憶體中的 XML 程式設計 API，專門設計來利用語言整合式查詢（LINQ）。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-108">is an in-memory XML programming API designed specifically to take advantage of Language-Integrated Query (LINQ).</span></span> <span data-ttu-id="1ce8c-109">雖然您可以直接呼叫 LINQ Api，但只有 Visual Basic 可讓您宣告 XML 常值，並直接存取 XML 軸屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-109">Although you can call the LINQ APIs directly, only Visual Basic enables you to declare XML literals and directly access XML axis properties.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1ce8c-110">ASP.NET 網頁中的宣告式程式碼不支援 XML 常值和 XML 軸屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-110">XML literals and XML axis properties are not supported in declarative code in an ASP.NET page.</span></span> <span data-ttu-id="1ce8c-111">若要使用 Visual Basic XML 功能，請將您的程式碼放在 ASP.NET 應用程式的程式碼後置頁面中。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-111">To use Visual Basic XML features, put your code in a code-behind page in your ASP.NET application.</span></span>  
  
 <span data-ttu-id="1ce8c-112">[播放按鈕](./media/overview-of-linq-to-xml/play-video-icon-example.gif)如需相關的影片示範，請參閱[如何開始使用 LINQ to XML？](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml)和[如何使用 LINQ to XML 建立 Excel 試算表？](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml)。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-112">[Play button](./media/overview-of-linq-to-xml/play-video-icon-example.gif) For related video demonstrations, see [How Do I Get Started with LINQ to XML?](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml) and [How Do I Create Excel Spreadsheets using LINQ to XML?](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml).</span></span>
  
## <a name="creating-xml"></a><span data-ttu-id="1ce8c-113">建立 XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-113">Creating XML</span></span>  
 <span data-ttu-id="1ce8c-114">有兩種方式可在 Visual Basic 中建立 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-114">There are two ways to create XML trees in Visual Basic.</span></span> <span data-ttu-id="1ce8c-115">您可以直接在程式碼中宣告 XML 常值，也可以使用 LINQ Api 來建立樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-115">You can declare an XML literal directly in code, or you can use the LINQ APIs to create the tree.</span></span> <span data-ttu-id="1ce8c-116">這兩個處理常式都可讓程式碼反映 XML 樹狀結構的最終結構。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-116">Both processes enable the code to reflect the final structure of the XML tree.</span></span> <span data-ttu-id="1ce8c-117">例如，下列程式碼範例會建立 XML 元素：</span><span class="sxs-lookup"><span data-stu-id="1ce8c-117">For example, the following code example creates an XML element:</span></span>  
  
 [!code-vb[VbXmlSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 <span data-ttu-id="1ce8c-118">如需詳細資訊，請參閱[在 Visual Basic 中建立 XML](creating-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-118">For more information, see [Creating XML in Visual Basic](creating-xml.md).</span></span>  
  
## <a name="accessing-and-navigating-xml"></a><span data-ttu-id="1ce8c-119">存取和流覽 XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-119">Accessing and Navigating XML</span></span>  
 <span data-ttu-id="1ce8c-120">Visual Basic 提供 XML 軸屬性來存取和流覽 XML 結構。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-120">Visual Basic provides XML axis properties for accessing and navigating XML structures.</span></span> <span data-ttu-id="1ce8c-121">這些屬性可讓您藉由指定 XML 子專案名稱來存取 XML 元素和屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-121">These properties enable you to access XML elements and attributes by specifying the XML child element names.</span></span> <span data-ttu-id="1ce8c-122">或者，您也可以明確地呼叫 LINQ 方法，以流覽和尋找專案和屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-122">Alternatively, you can explicitly call the LINQ methods for navigating and locating elements and attributes.</span></span> <span data-ttu-id="1ce8c-123">例如，下列程式碼範例會使用 XML 軸屬性來參考 XML 專案的屬性和子項目。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-123">For example, the following code example uses XML axis properties to refer to the attributes and child elements of an XML element.</span></span> <span data-ttu-id="1ce8c-124">此程式碼範例會使用 LINQ 查詢來抓取子專案，並將其輸出為 XML 元素，並有效地執行轉換。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-124">The code example uses a LINQ query to retrieve child elements and output them as XML elements, effectively performing a transform.</span></span>  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 <span data-ttu-id="1ce8c-125">如需詳細資訊，請參閱[在 Visual Basic 中存取 XML](accessing-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-125">For more information, see [Accessing XML in Visual Basic](accessing-xml.md).</span></span>  
  
## <a name="xml-namespaces"></a><span data-ttu-id="1ce8c-126">XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="1ce8c-126">XML Namespaces</span></span>  
 <span data-ttu-id="1ce8c-127">Visual Basic 可讓您使用語句，指定全域 XML 命名空間的別名 `Imports` 。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-127">Visual Basic enables you to specify an alias to a global XML namespace by using the `Imports` statement.</span></span> <span data-ttu-id="1ce8c-128">下列範例顯示如何使用 `Imports` 語句來匯入 XML 命名空間：</span><span class="sxs-lookup"><span data-stu-id="1ce8c-128">The following example shows how to use the `Imports` statement to import an XML namespace:</span></span>  
  
 [!code-vb[VbXMLSamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#1)]  
  
 <span data-ttu-id="1ce8c-129">當您存取 XML 軸屬性，並宣告 XML 檔和專案的 XML 常值時，可以使用 XML 命名空間別名。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-129">You can use an XML namespace alias when you access XML axis properties and declare XML literals for XML documents and elements.</span></span>  
  
 <span data-ttu-id="1ce8c-130">您可以 <xref:System.Xml.Linq.XNamespace> 使用[GetXmlNamespace 運算子](../../../language-reference/operators/getxmlnamespace-operator.md)來抓取特定命名空間前置詞的物件。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-130">You can retrieve an <xref:System.Xml.Linq.XNamespace> object for a particular namespace prefix by using the [GetXmlNamespace Operator](../../../language-reference/operators/getxmlnamespace-operator.md).</span></span>  
  
 <span data-ttu-id="1ce8c-131">如需詳細資訊，請參閱[Imports 語句（XML 命名空間）](../../../language-reference/statements/imports-statement-xml-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-131">For more information, see [Imports Statement (XML Namespace)](../../../language-reference/statements/imports-statement-xml-namespace.md).</span></span>  
  
### <a name="using-xml-namespaces-in-xml-literals"></a><span data-ttu-id="1ce8c-132">在 XML 常值中使用 XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="1ce8c-132">Using XML Namespaces in XML Literals</span></span>  
 <span data-ttu-id="1ce8c-133">下列範例顯示如何建立 <xref:System.Xml.Linq.XElement> 使用全域命名空間的物件 `ns` ：</span><span class="sxs-lookup"><span data-stu-id="1ce8c-133">The following example shows how to create an <xref:System.Xml.Linq.XElement> object that uses the global namespace `ns`:</span></span>  
  
 [!code-vb[VbXMLSamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#2)]  
  
 <span data-ttu-id="1ce8c-134">Visual Basic 編譯器會將包含 XML 命名空間別名的 XML 常值轉譯為對等的程式碼，並使用 xml 標記法搭配屬性來使用 xml 命名空間 `xmlns` 。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-134">The Visual Basic compiler translates XML literals that contain XML namespace aliases into equivalent code that uses the XML notation for using XML namespaces, with the `xmlns` attribute.</span></span> <span data-ttu-id="1ce8c-135">在編譯時，上一節範例中的程式碼會產生基本上與下列範例相同的可執行程式碼：</span><span class="sxs-lookup"><span data-stu-id="1ce8c-135">When compiled, the code in the previous section's example produces essentially the same executable code as the following example:</span></span>  
  
 [!code-vb[VbXMLSamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#3)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a><span data-ttu-id="1ce8c-136">在 XML 軸屬性中使用 XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="1ce8c-136">Using XML Namespaces in XML Axis Properties</span></span>  
 <span data-ttu-id="1ce8c-137">Xml 常值中宣告的 XML 命名空間不能用於 XML 軸屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-137">XML namespaces declared in XML literals are not available for use in XML axis properties.</span></span> <span data-ttu-id="1ce8c-138">不過，全域命名空間可以與 XML 軸屬性搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-138">However, global namespaces can be used with the XML axis properties.</span></span> <span data-ttu-id="1ce8c-139">使用冒號來分隔 XML 命名空間前置詞與本機專案名稱。</span><span class="sxs-lookup"><span data-stu-id="1ce8c-139">Use a colon to separate the XML namespace prefix from the local element name.</span></span> <span data-ttu-id="1ce8c-140">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="1ce8c-140">Following is an example:</span></span>  
  
 [!code-vb[VbXMLSamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="1ce8c-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1ce8c-141">See also</span></span>

- [<span data-ttu-id="1ce8c-142">XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-142">XML</span></span>](index.md)
- [<span data-ttu-id="1ce8c-143">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-143">Creating XML in Visual Basic</span></span>](creating-xml.md)
- [<span data-ttu-id="1ce8c-144">在 Visual Basic 中存取 XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-144">Accessing XML in Visual Basic</span></span>](accessing-xml.md)
- [<span data-ttu-id="1ce8c-145">在 Visual Basic 中管理 XML</span><span class="sxs-lookup"><span data-stu-id="1ce8c-145">Manipulating XML in Visual Basic</span></span>](manipulating-xml.md)

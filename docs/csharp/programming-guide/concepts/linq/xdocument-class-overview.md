---
title: XDocument 類別概觀 (C#)
description: 'C # 中的 XDocument 類別包含有效 XML 檔所需的資訊，包括 XML 宣告、處理指示和批註。'
ms.date: 07/20/2015
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
ms.openlocfilehash: 6d522cef25e99e4a5ea54e644855c8dfa7a05f4a
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302187"
---
# <a name="xdocument-class-overview-c"></a><span data-ttu-id="94829-103">XDocument 類別概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="94829-103">XDocument Class Overview (C#)</span></span>
<span data-ttu-id="94829-104">本主題說明 <xref:System.Xml.Linq.XDocument> 類別。</span><span class="sxs-lookup"><span data-stu-id="94829-104">This topic introduces the <xref:System.Xml.Linq.XDocument> class.</span></span>  
  
## <a name="overview-of-the-xdocument-class"></a><span data-ttu-id="94829-105">XDocument 類別的概觀</span><span class="sxs-lookup"><span data-stu-id="94829-105">Overview of the XDocument class</span></span>  
 <span data-ttu-id="94829-106"><xref:System.Xml.Linq.XDocument> 類別包含有效 XML 文件所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="94829-106">The <xref:System.Xml.Linq.XDocument> class contains the information necessary for a valid XML document.</span></span> <span data-ttu-id="94829-107">這包括 XML 宣告、處理指示與註解。</span><span class="sxs-lookup"><span data-stu-id="94829-107">This includes an XML declaration, processing instructions, and comments.</span></span>  
  
 <span data-ttu-id="94829-108">請注意，如果您需要 <xref:System.Xml.Linq.XDocument> 類別所提供的特定功能，您僅需要建立 <xref:System.Xml.Linq.XDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="94829-108">Note that you only have to create <xref:System.Xml.Linq.XDocument> objects if you require the specific functionality provided by the <xref:System.Xml.Linq.XDocument> class.</span></span> <span data-ttu-id="94829-109">在許多情況下，您可以直接使用 <xref:System.Xml.Linq.XElement>。</span><span class="sxs-lookup"><span data-stu-id="94829-109">In many circumstances, you can work directly with <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="94829-110">直接使用 <xref:System.Xml.Linq.XElement> 是較簡單的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="94829-110">Working directly with <xref:System.Xml.Linq.XElement> is a simpler programming model.</span></span>  
  
 <span data-ttu-id="94829-111"><xref:System.Xml.Linq.XDocument> 衍生自 <xref:System.Xml.Linq.XContainer>。</span><span class="sxs-lookup"><span data-stu-id="94829-111"><xref:System.Xml.Linq.XDocument> derives from <xref:System.Xml.Linq.XContainer>.</span></span> <span data-ttu-id="94829-112">因此，它可以包含子節點。</span><span class="sxs-lookup"><span data-stu-id="94829-112">Therefore, it can contain child nodes.</span></span> <span data-ttu-id="94829-113">不過，<xref:System.Xml.Linq.XDocument> 物件可以有只有一個 <xref:System.Xml.Linq.XElement> 子節點。</span><span class="sxs-lookup"><span data-stu-id="94829-113">However, <xref:System.Xml.Linq.XDocument> objects can have only one child <xref:System.Xml.Linq.XElement> node.</span></span> <span data-ttu-id="94829-114">這會反映 XML 標準，也就是說 XML 文件中只能有一個根項目 (Root Element)。</span><span class="sxs-lookup"><span data-stu-id="94829-114">This reflects the XML standard that there can be only one root element in an XML document.</span></span>  
  
## <a name="components-of-xdocument"></a><span data-ttu-id="94829-115">XDocument 的元件</span><span class="sxs-lookup"><span data-stu-id="94829-115">Components of XDocument</span></span>  
 <span data-ttu-id="94829-116"><xref:System.Xml.Linq.XDocument> 可以包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="94829-116">An <xref:System.Xml.Linq.XDocument> can contain the following elements:</span></span>  
  
- <span data-ttu-id="94829-117">一個 <xref:System.Xml.Linq.XDeclaration> 物件。</span><span class="sxs-lookup"><span data-stu-id="94829-117">One <xref:System.Xml.Linq.XDeclaration> object.</span></span> <span data-ttu-id="94829-118"><xref:System.Xml.Linq.XDeclaration> 可讓您指定 XML 宣告的關聯部分：XML 版本、文件的編碼，以及 XML 文件是否是獨立的。</span><span class="sxs-lookup"><span data-stu-id="94829-118"><xref:System.Xml.Linq.XDeclaration> enables you to specify the pertinent parts of an XML declaration: the XML version, the encoding of the document, and whether the XML document is stand-alone.</span></span>  
  
- <span data-ttu-id="94829-119">一個 <xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="94829-119">One <xref:System.Xml.Linq.XElement> object.</span></span> <span data-ttu-id="94829-120">這是 XML 文件的根節點。</span><span class="sxs-lookup"><span data-stu-id="94829-120">This is the root node of the XML document.</span></span>  
  
- <span data-ttu-id="94829-121">任何數目的 <xref:System.Xml.Linq.XProcessingInstruction> 物件。</span><span class="sxs-lookup"><span data-stu-id="94829-121">Any number of <xref:System.Xml.Linq.XProcessingInstruction> objects.</span></span> <span data-ttu-id="94829-122">處理指示會將資訊傳達到處理 XML 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="94829-122">A processing instruction communicates information to an application that processes the XML.</span></span>  
  
- <span data-ttu-id="94829-123">任何數目的 <xref:System.Xml.Linq.XComment> 物件。</span><span class="sxs-lookup"><span data-stu-id="94829-123">Any number of <xref:System.Xml.Linq.XComment> objects.</span></span> <span data-ttu-id="94829-124">這些註解將是根項目的同層級。</span><span class="sxs-lookup"><span data-stu-id="94829-124">The comments will be siblings to the root element.</span></span> <span data-ttu-id="94829-125"><xref:System.Xml.Linq.XComment> 物件不得為清單中的第一個引數，因為對於 XML 文件而言，它不適用於開始註解。</span><span class="sxs-lookup"><span data-stu-id="94829-125">The <xref:System.Xml.Linq.XComment> object cannot be the first argument in the list, because it is not valid for an XML document to start with a comment.</span></span>  
  
- <span data-ttu-id="94829-126">一個適用於 DTD 的 <xref:System.Xml.Linq.XDocumentType>。</span><span class="sxs-lookup"><span data-stu-id="94829-126">One <xref:System.Xml.Linq.XDocumentType> for the DTD.</span></span>  
  
 <span data-ttu-id="94829-127">當您序列化 <xref:System.Xml.Linq.XDocument> 時，即使 `XDocument.Declaration` 為 `null`，如果寫入器已將 `Writer.Settings.OmitXmlDeclaration` 設定為 `false` (預設值)，則輸出將會有 XML 宣告。</span><span class="sxs-lookup"><span data-stu-id="94829-127">When you serialize an <xref:System.Xml.Linq.XDocument>, even if `XDocument.Declaration` is `null`, the output will have an XML declaration if the writer has `Writer.Settings.OmitXmlDeclaration` set to `false` (the default).</span></span>  
  
 <span data-ttu-id="94829-128">根據預設，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會將版本設定為 "1.0"，並將編碼設定為 "utf-8"。</span><span class="sxs-lookup"><span data-stu-id="94829-128">By default, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] sets the version to "1.0", and sets the encoding to "utf-8".</span></span>  
  
## <a name="using-xelement-without-xdocument"></a><span data-ttu-id="94829-129">在沒有 XDocument 的情況下使用 XElement</span><span class="sxs-lookup"><span data-stu-id="94829-129">Using XElement without XDocument</span></span>  
 <span data-ttu-id="94829-130">如先前所述，<xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 程式發展介面中的主要類別。</span><span class="sxs-lookup"><span data-stu-id="94829-130">As previously mentioned, the <xref:System.Xml.Linq.XElement> class is the main class in the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] programming interface.</span></span> <span data-ttu-id="94829-131">在許多情況下，您的應用程式將不需要您建立文件。</span><span class="sxs-lookup"><span data-stu-id="94829-131">In many cases, your application will not require that you create a document.</span></span> <span data-ttu-id="94829-132">您可以使用 <xref:System.Xml.Linq.XElement> 類別來建立 XML 樹狀結構、在其中加入其他 XML 樹狀結構、修改 XML 樹狀結構，然後加以儲存。</span><span class="sxs-lookup"><span data-stu-id="94829-132">By using the <xref:System.Xml.Linq.XElement> class, you can create an XML tree, add other XML trees to it, modify the XML tree, and save it.</span></span>  
  
## <a name="using-xdocument"></a><span data-ttu-id="94829-133">使用 XDocument</span><span class="sxs-lookup"><span data-stu-id="94829-133">Using XDocument</span></span>  
 <span data-ttu-id="94829-134">若要建構 <xref:System.Xml.Linq.XDocument>，請使用功能結構，如同您建構 <xref:System.Xml.Linq.XElement> 物件時所執行的操作。</span><span class="sxs-lookup"><span data-stu-id="94829-134">To construct an <xref:System.Xml.Linq.XDocument>, use functional construction, just like you do to construct <xref:System.Xml.Linq.XElement> objects.</span></span>  
  
 <span data-ttu-id="94829-135">下列程式碼會建立 <xref:System.Xml.Linq.XDocument> 物件及其所包含的相關聯物件。</span><span class="sxs-lookup"><span data-stu-id="94829-135">The following code creates an <xref:System.Xml.Linq.XDocument> object and its associated contained objects.</span></span>  
  
```csharp  
XDocument d = new XDocument(  
    new XComment("This is a comment."),  
    new XProcessingInstruction("xml-stylesheet",  
        "href='mystyle.css' title='Compact' type='text/css'"),  
    new XElement("Pubs",  
        new XElement("Book",  
            new XElement("Title", "Artifacts of Roman Civilization"),  
            new XElement("Author", "Moreno, Jordao")  
        ),  
        new XElement("Book",  
            new XElement("Title", "Midieval Tools and Implements"),  
            new XElement("Author", "Gazit, Inbar")  
        )  
    ),  
    new XComment("This is another comment.")  
);  
d.Declaration = new XDeclaration("1.0", "utf-8", "true");  
Console.WriteLine(d);  
  
d.Save("test.xml");  
```  
  
 <span data-ttu-id="94829-136">當您檢查 test.xml 檔案時，您會得到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="94829-136">When you examine the file test.xml, you get the following output:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a><span data-ttu-id="94829-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="94829-137">See also</span></span>

- [<span data-ttu-id="94829-138">LINQ to XML 程式設計概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="94829-138">LINQ to XML Programming Overview (C#)</span></span>](./linq-to-xml-overview.md)

---
title: 使用 XPathNavigator 擷取 XML 資料
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 095b0987-ee4b-4595-a160-da1c956ad576
ms.openlocfilehash: 0d327738f818c40d8baa9e0fb8bd0092b94c6e07
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721500"
---
# <a name="extract-xml-data-using-xpathnavigator"></a><span data-ttu-id="193b6-102">使用 XPathNavigator 擷取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="193b6-102">Extract XML Data Using XPathNavigator</span></span>

<span data-ttu-id="193b6-103">可採用幾種不同方式表示 Microsoft .NET Framework 中的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="193b6-103">There are several different ways to represent an XML document in the Microsoft .NET Framework.</span></span> <span data-ttu-id="193b6-104">包括使用 <xref:System.String>，或使用 <xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter>、<xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument> 類別。</span><span class="sxs-lookup"><span data-stu-id="193b6-104">This includes using a <xref:System.String>, or by using the <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>, <xref:System.Xml.XmlDocument>, or <xref:System.Xml.XPath.XPathDocument> classes.</span></span> <span data-ttu-id="193b6-105">為便於在 XML 文件的不同表示之間進行切換，<xref:System.Xml.XPath.XPathNavigator> 類別提供了一些方法及屬性，可將 XML 當做 <xref:System.String>、<xref:System.Xml.XmlReader> 物件或 <xref:System.Xml.XmlWriter> 物件擷取。</span><span class="sxs-lookup"><span data-stu-id="193b6-105">To facilitate moving between these different representations of an XML document, the <xref:System.Xml.XPath.XPathNavigator> class provides a number of methods and properties for extracting the XML as a <xref:System.String>, <xref:System.Xml.XmlReader> object or <xref:System.Xml.XmlWriter> object.</span></span>  
  
## <a name="convert-an-xpathnavigator-to-a-string"></a><span data-ttu-id="193b6-106">將 XPathNavigator 轉換為字串</span><span class="sxs-lookup"><span data-stu-id="193b6-106">Convert an XPathNavigator to a String</span></span>  

 <span data-ttu-id="193b6-107">可使用 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 類別的 <xref:System.Xml.XPath.XPathNavigator> 屬性，取得整個 XML 文件的標記，或僅取得單一節點及其子節點的標記。</span><span class="sxs-lookup"><span data-stu-id="193b6-107">The <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> property of the <xref:System.Xml.XPath.XPathNavigator> class is used to get the markup of the entire XML document or just the markup of a single node and its child nodes.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="193b6-108"><xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 屬性僅取得節點之子節點的標記。</span><span class="sxs-lookup"><span data-stu-id="193b6-108">The <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> property gets the markup of just the child nodes of a node.</span></span>  
  
 <span data-ttu-id="193b6-109">下列程式碼範例顯示如何將 <xref:System.Xml.XPath.XPathNavigator> 物件中包含的整個 XML 文件與單一節點及其子節點，儲存為 <xref:System.String>。</span><span class="sxs-lookup"><span data-stu-id="193b6-109">The following code example shows how to save an entire XML document contained in an <xref:System.Xml.XPath.XPathNavigator> object as a <xref:System.String>, as well as a single node and its child nodes.</span></span>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("input.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Save the entire input.xml document to a string.  
Dim xml As String = navigator.OuterXml  
  
' Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element)  
Dim root As String = navigator.OuterXml  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Save the entire input.xml document to a string.  
string xml = navigator.OuterXml;  
  
// Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element);  
string root = navigator.OuterXml;  
```  
  
## <a name="convert-an-xpathnavigator-to-an-xmlreader"></a><span data-ttu-id="193b6-110">將 XPathNavigator 轉換為 XmlReader</span><span class="sxs-lookup"><span data-stu-id="193b6-110">Convert an XPathNavigator to an XmlReader</span></span>  

 <span data-ttu-id="193b6-111">使用 <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 方法，將 XML 文件或僅單一節點及其子節點的全部內容，以資料流方式傳送至 <xref:System.Xml.XmlReader> 物件。</span><span class="sxs-lookup"><span data-stu-id="193b6-111">The <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> method is used to stream the entire contents of an XML document or just a single node and its child nodes to an <xref:System.Xml.XmlReader> object.</span></span>  
  
 <span data-ttu-id="193b6-112">以目前節點及其子節點建立 <xref:System.Xml.XmlReader> 物件時，會將 <xref:System.Xml.XmlReader> 物件的 <xref:System.Xml.XmlReader.ReadState%2A> 屬性設為 <xref:System.Xml.ReadState.Initial>。</span><span class="sxs-lookup"><span data-stu-id="193b6-112">When the <xref:System.Xml.XmlReader> object is created with the current node and its child nodes, the <xref:System.Xml.XmlReader> object's <xref:System.Xml.XmlReader.ReadState%2A> property is set to <xref:System.Xml.ReadState.Initial>.</span></span> <span data-ttu-id="193b6-113">當初次呼叫 <xref:System.Xml.XmlReader> 物件的 <xref:System.Xml.XmlReader.Read%2A> 方法時，<xref:System.Xml.XmlReader> 會移至 <xref:System.Xml.XPath.XPathNavigator> 的目前節點。</span><span class="sxs-lookup"><span data-stu-id="193b6-113">When the <xref:System.Xml.XmlReader> object's <xref:System.Xml.XmlReader.Read%2A> method is called for the first time, the <xref:System.Xml.XmlReader> is moved to the current node of the <xref:System.Xml.XPath.XPathNavigator>.</span></span> <span data-ttu-id="193b6-114">新的 <xref:System.Xml.XmlReader> 物件在到達 XML 樹狀目錄的尾端之前，會持續讀取。</span><span class="sxs-lookup"><span data-stu-id="193b6-114">The new <xref:System.Xml.XmlReader> object continues to read until the end of the XML tree is reached.</span></span> <span data-ttu-id="193b6-115">此時，<xref:System.Xml.XmlReader.Read%2A> 方法會傳回 `false`，且 <xref:System.Xml.XmlReader> 物件的 <xref:System.Xml.XmlReader.ReadState%2A> 屬性會設為 <xref:System.Xml.ReadState.EndOfFile>。</span><span class="sxs-lookup"><span data-stu-id="193b6-115">At this point, the <xref:System.Xml.XmlReader.Read%2A> method returns `false` and the <xref:System.Xml.XmlReader> object's <xref:System.Xml.XmlReader.ReadState%2A> property is set to <xref:System.Xml.ReadState.EndOfFile>.</span></span>  
  
 <span data-ttu-id="193b6-116">建立或移動 <xref:System.Xml.XPath.XPathNavigator> 物件，並不會變更 <xref:System.Xml.XmlReader> 物件的位置。</span><span class="sxs-lookup"><span data-stu-id="193b6-116">The <xref:System.Xml.XPath.XPathNavigator> object's position is unchanged by the creation or movement of the <xref:System.Xml.XmlReader> object.</span></span> <span data-ttu-id="193b6-117">僅當定位在項目或根節點上時，<xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 方法才有效。</span><span class="sxs-lookup"><span data-stu-id="193b6-117">The <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> method is only valid when positioned on an element or root node.</span></span>  
  
 <span data-ttu-id="193b6-118">下列範例顯示如何取得包含 <xref:System.Xml.XmlReader> 物件中整個 XML 文件與單一節點及其子節點的 <xref:System.Xml.XPath.XPathDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="193b6-118">The following example shows how to get an <xref:System.Xml.XmlReader> object containing the entire XML document in an <xref:System.Xml.XPath.XPathDocument> object as well as a single node and its child nodes.</span></span>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlReader.  
Dim xml As XmlReader = navigator.ReadSubtree()  
  
While xml.Read()  
    Console.WriteLine(xml.ReadInnerXml())  
End While  
  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlReader = navigator.ReadSubtree()  
  
While book.Read()  
    Console.WriteLine(book.ReadInnerXml())  
End While  
  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlReader.  
XmlReader xml = navigator.ReadSubtree();  
  
while (xml.Read())  
{  
    Console.WriteLine(xml.ReadInnerXml());  
}  
  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlReader book = navigator.ReadSubtree();  
  
while (book.Read())  
{  
    Console.WriteLine(book.ReadInnerXml());  
}  
  
book.Close();  
```  
  
 <span data-ttu-id="193b6-119">該範例採用 `books.xml` 檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="193b6-119">The example takes the `books.xml` file as input.</span></span>  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
## <a name="converting-an-xpathnavigator-to-an-xmlwriter"></a><span data-ttu-id="193b6-120">將 XPathNavigator 轉換為 XmlWriter</span><span class="sxs-lookup"><span data-stu-id="193b6-120">Converting an XPathNavigator to an XmlWriter</span></span>  

 <span data-ttu-id="193b6-121">使用 <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> 方法，將 XML 文件或僅單一節點及其子節點的全部內容，以資料流方式傳送至 <xref:System.Xml.XmlWriter> 物件。</span><span class="sxs-lookup"><span data-stu-id="193b6-121">The <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> method is used to stream the entire contents of an XML document or just a single node and its child nodes to an <xref:System.Xml.XmlWriter> object.</span></span>  
  
 <span data-ttu-id="193b6-122">建立 <xref:System.Xml.XPath.XPathNavigator> 物件，並不會變更 <xref:System.Xml.XmlWriter> 物件的位置。</span><span class="sxs-lookup"><span data-stu-id="193b6-122">The <xref:System.Xml.XPath.XPathNavigator> object's position is unchanged by the creation of the <xref:System.Xml.XmlWriter> object.</span></span>  
  
 <span data-ttu-id="193b6-123">下列範例顯示如何取得包含 <xref:System.Xml.XmlWriter> 物件中整個 XML 文件與單一節點及其子節點的 <xref:System.Xml.XPath.XPathDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="193b6-123">The following example shows how to get an <xref:System.Xml.XmlWriter> object containing the entire XML document in an <xref:System.Xml.XPath.XPathDocument> object as well as a single node and its child nodes.</span></span>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlWriter.  
Dim xml As XmlWriter = XmlWriter.Create("newbooks.xml")  
navigator.WriteSubtree(xml)  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlWriter = XmlWriter.Create("book.xml")  
navigator.WriteSubtree(book)  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlWriter.  
XmlWriter xml = XmlWriter.Create("newbooks.xml");  
navigator.WriteSubtree(xml);  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlWriter book = XmlWriter.Create("book.xml");  
navigator.WriteSubtree(book);  
book.Close();  
```  
  
 <span data-ttu-id="193b6-124">範例將在本主題的前面部分所找到的 `books.xml` 檔案當做輸入。</span><span class="sxs-lookup"><span data-stu-id="193b6-124">The example takes the `books.xml` file found earlier in this topic as input.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="193b6-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="193b6-125">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="193b6-126">使用 XPath 資料模型處理 XML 資料</span><span class="sxs-lookup"><span data-stu-id="193b6-126">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="193b6-127">使用 XPathNavigator 巡覽節點集</span><span class="sxs-lookup"><span data-stu-id="193b6-127">Node Set Navigation Using XPathNavigator</span></span>](node-set-navigation-using-xpathnavigator.md)
- [<span data-ttu-id="193b6-128">使用 XPathNavigator 巡覽屬性及命名空間節點</span><span class="sxs-lookup"><span data-stu-id="193b6-128">Attribute and Namespace Node Navigation Using XPathNavigator</span></span>](attribute-and-namespace-node-navigation-using-xpathnavigator.md)
- [<span data-ttu-id="193b6-129">使用 XPathNavigator 存取強型別 XML 資料</span><span class="sxs-lookup"><span data-stu-id="193b6-129">Accessing Strongly Typed XML Data Using XPathNavigator</span></span>](accessing-strongly-typed-xml-data-using-xpathnavigator.md)

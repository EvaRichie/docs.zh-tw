---
title: XslTransform 的 XmlDocument 輸入
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 97115892-410a-4657-ab47-1e14dfba73f8
ms.openlocfilehash: 0afee2d706b95117971c02b57a5570427e0fbd3d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94827551"
---
# <a name="xmldocument-input-to-xsltransform"></a><span data-ttu-id="14eed-102">XslTransform 的 XmlDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="14eed-102">XmlDocument Input to XslTransform</span></span>
<span data-ttu-id="14eed-103"><xref:System.Xml.XmlDocument> 類別會提供 XML 文件的編輯功能。</span><span class="sxs-lookup"><span data-stu-id="14eed-103">The <xref:System.Xml.XmlDocument> class provides editing capabilities for an XML document.</span></span> <span data-ttu-id="14eed-104">如果在傳送到 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法前必須先編輯或修改 XML，請將 XML 載入 <xref:System.Xml.XmlDocument> 並加以編輯，然後再將它傳送到 <xref:System.Xml.Xsl.XslTransform>。</span><span class="sxs-lookup"><span data-stu-id="14eed-104">If the XML needs to be edited or modified before being sent to the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method, load the XML into an <xref:System.Xml.XmlDocument>, edit it, and send it in to the <xref:System.Xml.Xsl.XslTransform>.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="14eed-105">在 .NET Framework 2.0 中，<xref:System.Xml.Xsl.XslTransform> 類別已過時。</span><span class="sxs-lookup"><span data-stu-id="14eed-105">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="14eed-106">您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行可延伸樣式表語言轉換 (XSLT)。</span><span class="sxs-lookup"><span data-stu-id="14eed-106">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="14eed-107">如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。</span><span class="sxs-lookup"><span data-stu-id="14eed-107">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>  
  
 <span data-ttu-id="14eed-108"><xref:System.Xml.XmlDocument> 可實作 <xref:System.Xml.XPath.IXPathNavigable> 介面，以便文件在編輯後可傳遞至 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="14eed-108">The <xref:System.Xml.XmlDocument> implements the <xref:System.Xml.XPath.IXPathNavigable> interface, so the document can be passed to the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method after editing.</span></span>  
  
 <span data-ttu-id="14eed-109">由於 <xref:System.Xml.XmlDocument> 的編輯功能之故，使用 <xref:System.Xml.XmlDocument> 類別做為轉換的輸入，會比使用可延伸樣式表語言轉換 (XSLT) 轉換的 <xref:System.Xml.XPath.XPathDocument> 來得慢，因為 <xref:System.Xml.XPath.XPathDocument> 已因內部儲存而針對 XML 路徑語言 (XPath) 查詢進行過最佳化。</span><span class="sxs-lookup"><span data-stu-id="14eed-109">Due to the editing capability of the <xref:System.Xml.XmlDocument>, using the <xref:System.Xml.XmlDocument> class as input to a transformation is slower than using an <xref:System.Xml.XPath.XPathDocument> for the Extensible Stylesheet Language for Transformations (XSLT) transformations, as the <xref:System.Xml.XPath.XPathDocument> is optimized for XML Path Language (XPath) queries due to the internal storage.</span></span>  
  
## <a name="example"></a><span data-ttu-id="14eed-110">範例</span><span class="sxs-lookup"><span data-stu-id="14eed-110">Example</span></span>  
 <span data-ttu-id="14eed-111">下列程式碼範例顯示如何將 <xref:System.Xml.XmlDocument> 提供給 <xref:System.Xml.Xsl.XslTransform>，並將輸出傳送至 <xref:System.Xml.XmlReader>。</span><span class="sxs-lookup"><span data-stu-id="14eed-111">The following code example shows how an <xref:System.Xml.XmlDocument> can be supplied to the <xref:System.Xml.Xsl.XslTransform>, with the output sent to an <xref:System.Xml.XmlReader>.</span></span>  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.Load("books.xml")  
Dim trans As XslTransform = new XslTransform()  
trans.Load("book.xsl")  
Dim rdr As XmlReader = trans.Transform(doc, Nothing, Nothing)  
while (rdr.Read())  
end while  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
XslTransform trans = new XslTransform();  
trans.Load("book.xsl");  
XmlReader rdr = trans.Transform(doc, null, null);  
while (rdr.Read()) {}  
```  
  
## <a name="see-also"></a><span data-ttu-id="14eed-112">請參閱</span><span class="sxs-lookup"><span data-stu-id="14eed-112">See also</span></span>

- <xref:System.Xml.XmlDocument>
- [<span data-ttu-id="14eed-113">使用 XslTransform 類別進行 XSLT 轉換</span><span class="sxs-lookup"><span data-stu-id="14eed-113">XSLT Transformations with the XslTransform Class</span></span>](xslt-transformations-with-the-xsltransform-class.md)
- [<span data-ttu-id="14eed-114">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="14eed-114">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)
- [<span data-ttu-id="14eed-115">轉換中的 XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="14eed-115">XPathNavigator in Transformations</span></span>](xpathnavigator-in-transformations.md)
- [<span data-ttu-id="14eed-116">轉換中的 XPathNodeIterator</span><span class="sxs-lookup"><span data-stu-id="14eed-116">XPathNodeIterator in Transformations</span></span>](xpathnodeiterator-in-transformations.md)
- [<span data-ttu-id="14eed-117">XslTransform 的 XPathDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="14eed-117">XPathDocument Input to XslTransform</span></span>](xpathdocument-input-to-xsltransform.md)
- [<span data-ttu-id="14eed-118">XslTransform 的 XmlDataDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="14eed-118">XmlDataDocument Input to XslTransform</span></span>](xmldatadocument-input-to-xsltransform.md)

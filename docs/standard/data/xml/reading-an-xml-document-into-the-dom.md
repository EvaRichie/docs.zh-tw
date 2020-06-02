---
title: 將 XML 文件讀取到 DOM
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: a4fb291f-5630-49ba-a49a-5b66c3b71e49
ms.openlocfilehash: 02338d72f51d3a7507c0dfa030383399b9e213f6
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84282398"
---
# <a name="reading-an-xml-document-into-the-dom"></a><span data-ttu-id="49499-102">將 XML 文件讀取到 DOM</span><span class="sxs-lookup"><span data-stu-id="49499-102">Reading an XML Document into the DOM</span></span>
<span data-ttu-id="49499-103">從不同的格式將 XML 資訊讀取到記憶體。</span><span class="sxs-lookup"><span data-stu-id="49499-103">XML information is read into memory from different formats.</span></span> <span data-ttu-id="49499-104">可從字串、資料流、URL、文字讀取器或衍生自 <xref:System.Xml.XmlReader> 的類別讀取它。</span><span class="sxs-lookup"><span data-stu-id="49499-104">It can be read from a string, stream, URL, text reader, or a class derived from the <xref:System.Xml.XmlReader>.</span></span>  
  
 <span data-ttu-id="49499-105"><xref:System.Xml.XmlDocument.Load%2A> 方法將文件引入記憶體，並擁有可從各個不同格式取得資料的多載方法。</span><span class="sxs-lookup"><span data-stu-id="49499-105">The <xref:System.Xml.XmlDocument.Load%2A> method brings the document into memory and has overloaded methods available to take data from each of the different formats.</span></span> <span data-ttu-id="49499-106">另外還有一個 <xref:System.Xml.XmlDocument.LoadXml%2A> 方法，可從字串讀取 XML。</span><span class="sxs-lookup"><span data-stu-id="49499-106">There is also a <xref:System.Xml.XmlDocument.LoadXml%2A> method that reads XML from a string.</span></span>  
  
 <span data-ttu-id="49499-107">不同的 <xref:System.Xml.XmlDocument.Load%2A> 方法會影響載入 XML 文件物件模型 (DOM) 時建立的節點。</span><span class="sxs-lookup"><span data-stu-id="49499-107">Different <xref:System.Xml.XmlDocument.Load%2A> methods affect which nodes are created when the XML Document Object Model (DOM) is loaded.</span></span> <span data-ttu-id="49499-108">下表列出某些 <xref:System.Xml.XmlDocument.Load%2A> 方法及說明這些方法之主題間的差異。</span><span class="sxs-lookup"><span data-stu-id="49499-108">The following table lists the differences between some of the <xref:System.Xml.XmlDocument.Load%2A> methods and topics that address them.</span></span>  
  
|<span data-ttu-id="49499-109">主體</span><span class="sxs-lookup"><span data-stu-id="49499-109">Subject</span></span>|<span data-ttu-id="49499-110">主題</span><span class="sxs-lookup"><span data-stu-id="49499-110">Topic</span></span>|  
|-------------|-----------|  
|<span data-ttu-id="49499-111">建立泛空白字元節點</span><span class="sxs-lookup"><span data-stu-id="49499-111">Creation of white space nodes</span></span>|<span data-ttu-id="49499-112">用來載入 DOM 的物件會影響在 DOM 中產生的泛空白字元及顯著泛空白字元節點。</span><span class="sxs-lookup"><span data-stu-id="49499-112">The object used to load the DOM has an affect on the white space and significant white space nodes generated in the DOM.</span></span> <span data-ttu-id="49499-113">如需詳細資訊，請參閱[載入 DOM 時處理泛空白字元和顯著泛空白字元](white-space-and-significant-white-space-handling-when-loading-the-dom.md)。</span><span class="sxs-lookup"><span data-stu-id="49499-113">For more information, see [White Space and Significant White Space Handling when Loading the DOM](white-space-and-significant-white-space-handling-when-loading-the-dom.md).</span></span>|  
|<span data-ttu-id="49499-114">從特定節點開始載入 XML 或載入整個 XML 文件</span><span class="sxs-lookup"><span data-stu-id="49499-114">Loading XML starting from a specific node or loading the entire XML document</span></span>|<span data-ttu-id="49499-115">使用 <xref:System.Xml.XmlDocument.Load%2A?displayProperty=nameWithType> 方法可將資料從特定節點載入至 DOM。</span><span class="sxs-lookup"><span data-stu-id="49499-115">Using the <xref:System.Xml.XmlDocument.Load%2A?displayProperty=nameWithType> method data can be loaded from a specific node into the DOM.</span></span> <span data-ttu-id="49499-116">如需詳細資訊，請參閱[從讀取器載入資料](load-data-from-a-reader.md)。</span><span class="sxs-lookup"><span data-stu-id="49499-116">For more information, see [Load Data from a Reader](load-data-from-a-reader.md).</span></span>|  
|<span data-ttu-id="49499-117">載入 XML 時進行驗證</span><span class="sxs-lookup"><span data-stu-id="49499-117">Validating the XML as it is loaded</span></span>|<span data-ttu-id="49499-118">可在將 XML 資料載入至 DOM 時對其進行驗證。</span><span class="sxs-lookup"><span data-stu-id="49499-118">The XML data loaded into the DOM can be validated as it is loaded.</span></span> <span data-ttu-id="49499-119">使用驗證 <xref:System.Xml.XmlReader> 來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="49499-119">This is accomplished using a validating <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="49499-120">如需在載入 XML 時進行驗證的詳細資訊，請參閱[驗證 DOM 中的 XML 文件](validating-an-xml-document-in-the-dom.md)。</span><span class="sxs-lookup"><span data-stu-id="49499-120">For more information about validating XML as it is loaded, see [Validating an XML Document in the DOM](validating-an-xml-document-in-the-dom.md).</span></span>|  
  
 <span data-ttu-id="49499-121">下列範例顯示以 <xref:System.Xml.XmlDocument.LoadXml%2A> 方法載入的 XML，以及隨後儲存至稱為 `data.xml` 之文字檔的資料。</span><span class="sxs-lookup"><span data-stu-id="49499-121">The following example shows XML being loaded with the <xref:System.Xml.XmlDocument.LoadXml%2A> method and the data subsequently saved to a text file called `data.xml`.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
        ' Create the XmlDocument.  
        Dim doc As New XmlDocument()  
        doc.LoadXml(("<book genre='novel' ISBN='1-861001-57-5'>" & _  
                    "<title>Pride And Prejudice</title>" & _  
                    "</book>"))  
        ' Save the document to a file.  
        doc.Save("data.xml")  
    End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
    public static void Main()  
    {  
        // Create the XmlDocument.  
        XmlDocument doc = new XmlDocument();  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5'>" +  
                    "<title>Pride And Prejudice</title>" +  
                    "</book>");  
  
        // Save the document to a file.  
        doc.Save("data.xml");  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="49499-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49499-122">See also</span></span>

- [<span data-ttu-id="49499-123">XML 文件物件模型 (DOM)</span><span class="sxs-lookup"><span data-stu-id="49499-123">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)

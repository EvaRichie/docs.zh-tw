---
title: 轉換中的 XPathNavigator
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 118f97d1-7110-4d1b-b0bd-4143252c0bb0
ms.openlocfilehash: b28a2d4991e2e4b14027460c0f3c97145862da2a
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818371"
---
# <a name="xpathnavigator-in-transformations"></a><span data-ttu-id="54a92-102">轉換中的 XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="54a92-102">XPathNavigator in Transformations</span></span>
<span data-ttu-id="54a92-103"><xref:System.Xml.XPath.XPathNavigator> 類別可提供資料的唯讀隨機存取，並可當作可延伸樣式表語言轉換 (XSLT) 的輸入。</span><span class="sxs-lookup"><span data-stu-id="54a92-103">The <xref:System.Xml.XPath.XPathNavigator> class provides read-only random access to data and is designed for use as an input to Extensible Stylesheet Language for Transformations (XSLT).</span></span> <span data-ttu-id="54a92-104">它可實作於 <xref:System.Xml.XPath.XPathDocument>、<xref:System.Xml.XmlDataDocument> 及 <xref:System.Xml.XmlDocument>。</span><span class="sxs-lookup"><span data-stu-id="54a92-104">It is implemented on the <xref:System.Xml.XPath.XPathDocument>, <xref:System.Xml.XmlDataDocument>, and <xref:System.Xml.XmlDocument>.</span></span> <span data-ttu-id="54a92-105"><xref:System.Xml.XPath.XPathNavigator> 以 XML 路徑語言 (XPath) 之建議事項第 5 節中所說明的全球資訊網協會 (W3C) 資料模型為基礎。</span><span class="sxs-lookup"><span data-stu-id="54a92-105">The <xref:System.Xml.XPath.XPathNavigator> is based upon the World Wide Web Consortium (W3C) Data Model as described in section 5 of the XML Path Language (XPath) recommendation.</span></span>  
  
 <span data-ttu-id="54a92-106"><xref:System.Xml.XPath.XPathNavigator> 可定義任何存放區上的資料指標模型，並可針對任何資料存放區提供快速、唯讀的 XPath 查詢。</span><span class="sxs-lookup"><span data-stu-id="54a92-106">The <xref:System.Xml.XPath.XPathNavigator> defines a cursor model over any store and provides fast, read-only XPath queries over any data store.</span></span> <span data-ttu-id="54a92-107"><xref:System.Xml.XPath.XPathNavigator> 也是可用來重複 Result Tree Fragment 的類別。</span><span class="sxs-lookup"><span data-stu-id="54a92-107">The <xref:System.Xml.XPath.XPathNavigator> is also the class to use for iterating over result tree fragments.</span></span>  
  
 <span data-ttu-id="54a92-108">此 API 讓您能夠從存放區目前的節點中取得資訊，並移至連接的節點上。</span><span class="sxs-lookup"><span data-stu-id="54a92-108">The API enables you to get information from the current node in the store and move to connected nodes.</span></span> <span data-ttu-id="54a92-109"><xref:System.Xml.XPath.XPathNavigator> 是一種資料指標樣式模型，可使用一組 **Move** 方法執行存放區間的往返作業。</span><span class="sxs-lookup"><span data-stu-id="54a92-109">The <xref:System.Xml.XPath.XPathNavigator> is a cursor style model that performs traversal over a store using a set of **Move** methods.</span></span> <span data-ttu-id="54a92-110"><xref:System.Xml.XPath.XPathNavigator> 一律定位於節點上。</span><span class="sxs-lookup"><span data-stu-id="54a92-110">The <xref:System.Xml.XPath.XPathNavigator> is always positioned on a node.</span></span> <span data-ttu-id="54a92-111">若 **Move** 方法失敗，<xref:System.Xml.XPath.XPathNavigator> 將不會有任何變更。</span><span class="sxs-lookup"><span data-stu-id="54a92-111">Any **Move** method that fails leaves the <xref:System.Xml.XPath.XPathNavigator> unchanged.</span></span>  
  
 <span data-ttu-id="54a92-112"><xref:System.Xml.XPath.XPathNavigator> 是可用來重複 Result Tree Fragment 的類別。</span><span class="sxs-lookup"><span data-stu-id="54a92-112">The <xref:System.Xml.XPath.XPathNavigator> is the class to use for iterating over result tree fragments.</span></span> <span data-ttu-id="54a92-113">下列程式碼範例將藉由呼叫附有 `fragment` 參數的函式，在樣式表中建立 Result Tree Fragment。</span><span class="sxs-lookup"><span data-stu-id="54a92-113">The following code sample creates a result tree fragment within a style sheet by calling the function with the parameter, `fragment`, which contains XML.</span></span>  
  
## <a name="testxsl"></a><span data-ttu-id="54a92-114">test.xsl</span><span class="sxs-lookup"><span data-stu-id="54a92-114">test.xsl</span></span>  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl ="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
  
<xsl:variable name="fragment">  
    <authorlist>  
       <author>Joe</author>  
    </authorlist>  
</xsl:variable>  
  
<msxsl:script language="C#" implements-prefix="user">  
<![CDATA[  
   string NodeFragment(XPathNavigator nav)  
   {  
      if (nav.HasChildren)  
        return nav.Value;  
      else  
        return "";  
   }  
]]>  
</msxsl:script>  
  
<xsl:template match="/">  
     <xsl:value-of select="user:NodeFragment($fragment)"/>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="testxml"></a><span data-ttu-id="54a92-115">test.xml</span><span class="sxs-lookup"><span data-stu-id="54a92-115">test.xml</span></span>  
  
```xml  
<root>Some text</root>  
```  
  
 <span data-ttu-id="54a92-116">下列程式碼使用 **test.xsl** 樣式表和 **test.xml** 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="54a92-116">The following code uses the **test.xsl** style sheet and **test.xml** input data.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
Public Class sample  
  
    Public Shared Sub Main()  
        Dim xslt As New XslTransform()  
        xslt.Load("test.xsl")  
  
        Dim xd As New XPathDocument("test.xml")  
  
        Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
        xslt.Transform(xd, Nothing, strmTemp, Nothing)  
    End Sub 'Main  
End Class 'sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, null, strmTemp, null);  
    }  
}  
```  
  
## <a name="output"></a><span data-ttu-id="54a92-117">輸出</span><span class="sxs-lookup"><span data-stu-id="54a92-117">Output</span></span>  
 <span data-ttu-id="54a92-118">轉換結果儲存在檔案 **out.xml** 內：</span><span class="sxs-lookup"><span data-stu-id="54a92-118">The result of the transformation is found in the file **out.xml**:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>Joe  
```  
  
## <a name="see-also"></a><span data-ttu-id="54a92-119">請參閱</span><span class="sxs-lookup"><span data-stu-id="54a92-119">See also</span></span>

- [<span data-ttu-id="54a92-120">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="54a92-120">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)

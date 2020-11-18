---
title: 樣式表參數和擴充物件的 XsltArgumentList
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: de2f0dce-6b98-4908-bba7-ed150cc50355
ms.openlocfilehash: 6f0be433abcebed7f9da70225563a04170426314
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818202"
---
# <a name="xsltargumentlist-for-style-sheet-parameters-and-extension-objects"></a><span data-ttu-id="98faa-102">樣式表參數和擴充物件的 XsltArgumentList</span><span class="sxs-lookup"><span data-stu-id="98faa-102">XsltArgumentList for Style Sheet Parameters and Extension Objects</span></span>
<span data-ttu-id="98faa-103"><xref:System.Xml.Xsl.XsltArgumentList> 類別包含可擴充樣式表語言轉換 (XSLT) 參數和 XSLT 擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-103">The <xref:System.Xml.Xsl.XsltArgumentList> class contains Extensible Stylesheet Language for Transformations (XSLT) parameters and XSLT extension objects.</span></span> <span data-ttu-id="98faa-104">傳入 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法後，就可從樣式表叫用這些參數和擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-104">When passed into the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method, these parameters and extension objects can be invoked from style sheets.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="98faa-105"><xref:System.Xml.Xsl.XslTransform> 和 <xref:System.Xml.Xsl.XsltArgumentList> 類別在 .NET Framework 2.0 中已過時。</span><span class="sxs-lookup"><span data-stu-id="98faa-105">The <xref:System.Xml.Xsl.XslTransform> and <xref:System.Xml.Xsl.XsltArgumentList> classes are obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="98faa-106">您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行 XSLT 轉換。</span><span class="sxs-lookup"><span data-stu-id="98faa-106">You can perform XSLT transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="98faa-107">如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。</span><span class="sxs-lookup"><span data-stu-id="98faa-107">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>  
  
 <span data-ttu-id="98faa-108"><xref:System.Xml.Xsl.XsltArgumentList> 類別包含 XSLT 參數和 XSLT 擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-108">The <xref:System.Xml.Xsl.XsltArgumentList> class contains XSLT parameters and XSLT extension objects.</span></span> <span data-ttu-id="98faa-109">傳入 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法後，就可從樣式表叫用這些參數和擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-109">When passed into the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method, these parameters and extension objects can be invoked from style sheets.</span></span>  
  
 <span data-ttu-id="98faa-110">下列是傳遞物件，而不是使用內嵌指令碼的優點：</span><span class="sxs-lookup"><span data-stu-id="98faa-110">The following are advantages to passing an object rather than using an embedded script:</span></span>  
  
- <span data-ttu-id="98faa-111">提供較佳的類別封裝和重複使用。</span><span class="sxs-lookup"><span data-stu-id="98faa-111">Provides better encapsulation and reuse of classes.</span></span>  
  
- <span data-ttu-id="98faa-112">允許樣式表更簡潔且更易於維護。</span><span class="sxs-lookup"><span data-stu-id="98faa-112">Allows style sheets to be smaller and more maintainable.</span></span>  
  
- <span data-ttu-id="98faa-113">除了支援的 <xref:System> 命名空間集內所定義的命名空間以外，支援在其他命名空間的類別上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="98faa-113">Supports calling methods on classes belonging to namespaces other than those defined within the set of supported <xref:System> namespaces.</span></span>  
  
- <span data-ttu-id="98faa-114">支援使用 <xref:System.Xml.XPath.XPathNodeIterator> 將結果樹狀結構片段傳遞給樣式表。</span><span class="sxs-lookup"><span data-stu-id="98faa-114">Supports passing result tree fragments to the style sheet with the use of the <xref:System.Xml.XPath.XPathNodeIterator>.</span></span>  
  
## <a name="xslt-style-sheet-parameters"></a><span data-ttu-id="98faa-115">XSLT 樣式表參數</span><span class="sxs-lookup"><span data-stu-id="98faa-115">XSLT Style Sheet Parameters</span></span>  
 <span data-ttu-id="98faa-116">XSLT 參數可使用 <xref:System.Xml.Xsl.XsltArgumentList> 方法加入至 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>。</span><span class="sxs-lookup"><span data-stu-id="98faa-116">XSLT parameters are added to the <xref:System.Xml.Xsl.XsltArgumentList> using the <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> method.</span></span> <span data-ttu-id="98faa-117">限定名稱和命名空間統一資源識別元 (URI) 會在此時與參數物件產生關聯。</span><span class="sxs-lookup"><span data-stu-id="98faa-117">A qualified name and namespace Uniform Resource Identifier (URI) are associated with the parameter object at that time.</span></span>  
  
 <span data-ttu-id="98faa-118">參數物件應對應至全球資訊網協會 (W3C) 型別。</span><span class="sxs-lookup"><span data-stu-id="98faa-118">The parameter object should correspond to a World Wide Web Consortium (W3C) type.</span></span> <span data-ttu-id="98faa-119">下表說明對應的 W3C 型別、對等的 .NET Framework 類別 (型別)，以及 W3C 型別是 XML 路徑語言 (XPath) 型別還是 XSLT 型別。</span><span class="sxs-lookup"><span data-stu-id="98faa-119">The following table shows the corresponding W3C types, the equivalent .NET Framework classes (type), and whether the W3C type is an XML Path Language (XPath) type or XSLT type.</span></span>  
  
|<span data-ttu-id="98faa-120">W3C 型別</span><span class="sxs-lookup"><span data-stu-id="98faa-120">W3C Type</span></span>|<span data-ttu-id="98faa-121">對等的 .NET Framework 類別 (型別)</span><span class="sxs-lookup"><span data-stu-id="98faa-121">Equivalent .NET Framework class (type)</span></span>|<span data-ttu-id="98faa-122">XPath 型別或 XSLT 型別</span><span class="sxs-lookup"><span data-stu-id="98faa-122">XPath type or XSLT type</span></span>|  
|--------------|----------------------------------------------|-----------------------------|  
|<span data-ttu-id="98faa-123">字串</span><span class="sxs-lookup"><span data-stu-id="98faa-123">String</span></span>|<span data-ttu-id="98faa-124">System.String</span><span class="sxs-lookup"><span data-stu-id="98faa-124">System.String</span></span>|<span data-ttu-id="98faa-125">XPath</span><span class="sxs-lookup"><span data-stu-id="98faa-125">XPath</span></span>|  
|<span data-ttu-id="98faa-126">布林值</span><span class="sxs-lookup"><span data-stu-id="98faa-126">Boolean</span></span>|<span data-ttu-id="98faa-127">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="98faa-127">System.Boolean</span></span>|<span data-ttu-id="98faa-128">XPath</span><span class="sxs-lookup"><span data-stu-id="98faa-128">XPath</span></span>|  
|<span data-ttu-id="98faa-129">數字</span><span class="sxs-lookup"><span data-stu-id="98faa-129">Number</span></span>|<span data-ttu-id="98faa-130">System.Double</span><span class="sxs-lookup"><span data-stu-id="98faa-130">System.Double</span></span>|<span data-ttu-id="98faa-131">XPath</span><span class="sxs-lookup"><span data-stu-id="98faa-131">XPath</span></span>|  
|<span data-ttu-id="98faa-132">Result Tree Fragment</span><span class="sxs-lookup"><span data-stu-id="98faa-132">Result Tree Fragment</span></span>|<span data-ttu-id="98faa-133">System.Xml.XPath.XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="98faa-133">System.Xml.XPath.XPathNavigator</span></span>|<span data-ttu-id="98faa-134">XSLT</span><span class="sxs-lookup"><span data-stu-id="98faa-134">XSLT</span></span>|  
|<span data-ttu-id="98faa-135">Node Set</span><span class="sxs-lookup"><span data-stu-id="98faa-135">Node Set</span></span>|<span data-ttu-id="98faa-136">System.Xml.XPath.XPathNodeIterator</span><span class="sxs-lookup"><span data-stu-id="98faa-136">System.Xml.XPath.XPathNodeIterator</span></span>|<span data-ttu-id="98faa-137">XPath</span><span class="sxs-lookup"><span data-stu-id="98faa-137">XPath</span></span>|  
  
 <span data-ttu-id="98faa-138">如果參數物件不是以上類別之一，它會被強制成合適的 Double 或 String。</span><span class="sxs-lookup"><span data-stu-id="98faa-138">If the parameter object is not one of the above classes, it is forced to either a Double or String, as appropriate.</span></span> <span data-ttu-id="98faa-139">Int16、UInt16、Int32、UInt32、Int64、UInt64、Single 和 Decimal 型別被強制成 Double。</span><span class="sxs-lookup"><span data-stu-id="98faa-139">Int16, UInt16, Int32, UInt32, Int64, UInt64, Single and Decimal types are forced to a Double.</span></span> <span data-ttu-id="98faa-140">所有其他型別都會透過 `ToString` 方法而強制轉換為 String。</span><span class="sxs-lookup"><span data-stu-id="98faa-140">All other types are forced to a String using the `ToString` method.</span></span>  
  
#### <a name="to-use-the-xslt-parameter-the-user-needs-to-do-the-following"></a><span data-ttu-id="98faa-141">若要使用 XSLT 參數，使用者必須執行以下作業：</span><span class="sxs-lookup"><span data-stu-id="98faa-141">To use the XSLT parameter, the user needs to do the following:</span></span>  
  
1. <span data-ttu-id="98faa-142">使用 <xref:System.Xml.Xsl.XsltArgumentList> 來建立 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>，並加入物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-142">Create an <xref:System.Xml.Xsl.XsltArgumentList> and add the objects using <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>.</span></span>  
  
2. <span data-ttu-id="98faa-143">從樣式表呼叫參數。</span><span class="sxs-lookup"><span data-stu-id="98faa-143">Call the parameters from the style sheet.</span></span>  
  
3. <span data-ttu-id="98faa-144">將 <xref:System.Xml.Xsl.XsltArgumentList> 傳遞至 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="98faa-144">Pass the <xref:System.Xml.Xsl.XsltArgumentList> to the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method.</span></span>  
  
### <a name="example"></a><span data-ttu-id="98faa-145">範例</span><span class="sxs-lookup"><span data-stu-id="98faa-145">Example</span></span>  
 <span data-ttu-id="98faa-146">下列範例使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法來建立參數，以保留計算的折扣日期。</span><span class="sxs-lookup"><span data-stu-id="98faa-146">The following example uses the <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> method to create a parameter to hold a calculated discount date.</span></span> <span data-ttu-id="98faa-147">折扣日期計算為從訂購日期起的 20 天。</span><span class="sxs-lookup"><span data-stu-id="98faa-147">The discount date is calculated to be 20 days from the order date.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public class Sample  
  
   Private Const filename As String = "order.xml"  
   Private Const stylesheet As String = "discount.xsl"  
  
   Public Shared Sub Main()  
  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Calculate the discount date.  
    Dim today As DateTime = DateTime.Now  
    Dim d As DateTime = today.AddDays(20)  
    xslArg.AddParam("discount", "", d.ToString())  
  
    'Create an XmlTextWriter to handle the output.  
    Dim writer As XmlTextWriter = New XmlTextWriter("orderout.xml", Nothing)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
  
    writer.Close()  
  
  End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample  
{  
   private const String filename = "order.xml";  
   private const String stylesheet = "discount.xsl";  
  
   public static void Main() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Calculate the discount date.  
    DateTime today = DateTime.Now;  
    DateTime d = today.AddDays(20);  
    xslArg.AddParam("discount", "", d.ToString());  
  
    //Create an XmlTextWriter to handle the output.  
    XmlTextWriter writer = new XmlTextWriter("orderout.xml", null);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  }  
}  
```  
  
### <a name="input"></a><span data-ttu-id="98faa-148">輸入</span><span class="sxs-lookup"><span data-stu-id="98faa-148">Input</span></span>  
 <span data-ttu-id="98faa-149">order.xml</span><span class="sxs-lookup"><span data-stu-id="98faa-149">order.xml</span></span>  
  
```xml  
<!--Represents a customer order-->  
<order>  
  <book ISBN='10-861003-324'>  
    <title>The Handmaid's Tale</title>  
    <price>19.95</price>  
  </book>  
  <cd ISBN='2-3631-4'>  
    <title>Americana</title>  
    <price>16.95</price>  
  </cd>  
</order>  
```  
  
 <span data-ttu-id="98faa-150">discount.xsl</span><span class="sxs-lookup"><span data-stu-id="98faa-150">discount.xsl</span></span>  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
  <xsl:param name="discount"/>  
  <xsl:template match="/">  
    <order>  
      <xsl:variable name="sub-total" select="sum(//price)"/>  
      <total><xsl:value-of select="$sub-total"/></total>  
      15% discount if paid by: <xsl:value-of select="$discount"/>  
    </order>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### <a name="output"></a><span data-ttu-id="98faa-151">輸出</span><span class="sxs-lookup"><span data-stu-id="98faa-151">Output</span></span>  
  
```xml  
<order>  
   <total>36.9</total>
   15% discount if paid by: 5/6/2001 5:01:15 PM
</order>  
```  
  
## <a name="xslt-extension-objects"></a><span data-ttu-id="98faa-152">XSLT 擴充物件</span><span class="sxs-lookup"><span data-stu-id="98faa-152">XSLT Extension Objects</span></span>  
 <span data-ttu-id="98faa-153">使用 <xref:System.Xml.Xsl.XsltArgumentList> 方法，將 XSLT 擴充物件加入至 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>。</span><span class="sxs-lookup"><span data-stu-id="98faa-153">XSLT extension objects are added to the <xref:System.Xml.Xsl.XsltArgumentList> using the <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> method.</span></span> <span data-ttu-id="98faa-154">限定名稱和命名空間 URI 於當時與擴充物件產生關聯。</span><span class="sxs-lookup"><span data-stu-id="98faa-154">A qualified name and namespace URI are associated with the extension object at that time.</span></span>  
  
 <span data-ttu-id="98faa-155">加入物件時，<xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 的呼叫端必須在安全性原則中完全受信任。</span><span class="sxs-lookup"><span data-stu-id="98faa-155">When an object is added, the caller of the <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> must be fully trusted in the security policy.</span></span> <span data-ttu-id="98faa-156">如果呼叫端並非完全受信任，則無法加入。</span><span class="sxs-lookup"><span data-stu-id="98faa-156">If the caller is semi-trusted, the addition will fail.</span></span>  
  
 <span data-ttu-id="98faa-157">雖然物件成功加入，但不保證會成功執行。</span><span class="sxs-lookup"><span data-stu-id="98faa-157">Though an object is added successfully, it does not guarantee that the execution will be successful.</span></span> <span data-ttu-id="98faa-158">呼叫 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法時，即會針對 <xref:System.Xml.Xsl.XslTransform.Load%2A> 期間所提供的辨識項計算使用權限，接著將該使用權限集指派給整個轉換程序。</span><span class="sxs-lookup"><span data-stu-id="98faa-158">When the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is called, permissions are calculated against the evidence provided at <xref:System.Xml.Xsl.XslTransform.Load%2A> time, and that permission set is assigned to the entire transformation process.</span></span> <span data-ttu-id="98faa-159">如果擴充物件企圖啟始需要權限集中找不到的使用權限的動作，將擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="98faa-159">If an extension object attempts to initiate an action that requires permissions not found in the set, an exception is thrown.</span></span>  
  
 <span data-ttu-id="98faa-160">從擴充物件中傳回的資料型別，是數字、字串、布林和節點集這四種基本 XPath 資料型別的其中一種。</span><span class="sxs-lookup"><span data-stu-id="98faa-160">The data types returned from extension objects are one of the four basic XPath data types of number, string, Boolean, and node set.</span></span>  
  
#### <a name="to-use-the-xslt-extension-object-the-user-needs-to-do-the-following"></a><span data-ttu-id="98faa-161">若要使用 XSLT 擴充物件，使用者必須執行以下作業：</span><span class="sxs-lookup"><span data-stu-id="98faa-161">To use the XSLT extension object, the user needs to do the following:</span></span>  
  
1. <span data-ttu-id="98faa-162">使用 <xref:System.Xml.Xsl.XsltArgumentList> 來建立 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>，並加入擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-162">Create an <xref:System.Xml.Xsl.XsltArgumentList> and add the extension object using <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>.</span></span>  
  
2. <span data-ttu-id="98faa-163">從樣式表叫用擴充物件。</span><span class="sxs-lookup"><span data-stu-id="98faa-163">Invoke the extension object from the style sheet.</span></span>  
  
3. <span data-ttu-id="98faa-164">將 <xref:System.Xml.Xsl.XsltArgumentList> 傳遞至 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="98faa-164">Pass the <xref:System.Xml.Xsl.XsltArgumentList> to the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method.</span></span>  
  
### <a name="example"></a><span data-ttu-id="98faa-165">範例</span><span class="sxs-lookup"><span data-stu-id="98faa-165">Example</span></span>  
 <span data-ttu-id="98faa-166">以下範例計算圓的圓周 (假設已經知道其半徑)。</span><span class="sxs-lookup"><span data-stu-id="98faa-166">The following example calculates the circumference of a circle given its radius.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
   Private Const filename As String = "number.xml"  
   Private Const stylesheet As String = "circle.xsl"  
  
   Public Shared Sub Main()  
        Dim test As Sample = New Sample  
   End Sub  
  
  Public Sub New()  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Add an object to calculate the circumference of the circle.  
    Dim obj As Calculate = New Calculate  
    xslArg.AddExtensionObject("urn:myObj", obj)  
  
    'Create an XmlTextWriter to output to the console.  
    Dim writer As XmlTextWriter = New XmlTextWriter(Console.Out)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
    writer.Close()  
  
  End Sub  
  
  'Calculates the circumference of a circle given the radius.  
  Public Class Calculate  
  
    Private circ As double = 0  
  
    Public Function Circumference(radius As Double) As Double  
       circ = Math.PI*2*radius  
       Return circ  
    End Function  
  End Class  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample  
{  
   private const String filename = "number.xml";  
   private const String stylesheet = "circle.xsl";  
  
   public static void Main() {  
  
        Sample test = new Sample();  
    }  
  
  public Sample() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Add an object to calculate the circumference of the circle.  
    Calculate obj = new Calculate();  
    xslArg.AddExtensionObject("urn:myObj", obj);  
  
    //Create an XmlTextWriter to output to the console.  
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  
  }  
  
  //Calculates the circumference of a circle given the radius.  
  public class Calculate {  
  
    private double circ = 0;  
  
    public double Circumference(double radius){  
       circ = Math.PI*2*radius;  
       return circ;  
    }  
  }  
}  
```  
  
### <a name="input"></a><span data-ttu-id="98faa-167">輸入</span><span class="sxs-lookup"><span data-stu-id="98faa-167">Input</span></span>  
 <span data-ttu-id="98faa-168">number.xml</span><span class="sxs-lookup"><span data-stu-id="98faa-168">number.xml</span></span>  
  
```xml  
<?xml version='1.0'?>  
<data>  
  <circle>  
    <radius>12</radius>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
  </circle>  
</data>
```  
  
 <span data-ttu-id="98faa-169">circle.xsl</span><span class="sxs-lookup"><span data-stu-id="98faa-169">circle.xsl</span></span>  
  
```xml  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
    xmlns:myObj="urn:myObj">  
  
  <xsl:template match="data">  
  <circles>  
  <xsl:for-each select="circle">  
    <circle>  
    <xsl:copy-of select="node()"/>  
       <circumference>  
          <xsl:value-of select="myObj:Circumference(radius)"/>
       </circumference>  
    </circle>  
  </xsl:for-each>  
  </circles>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### <a name="output"></a><span data-ttu-id="98faa-170">輸出</span><span class="sxs-lookup"><span data-stu-id="98faa-170">Output</span></span>  
 `<circles xmlns:myObj="urn:myObj">`  
  
 `<circle>`  
  
 `<radius>12</radius>`  
  
 `<circumference>75.398223686155</circumference>`  
  
 `</circle>`  
  
 `<circle>`  
  
 `<radius>37.5</radius>`  
  
 `<circumference>235.61944901923448</circumference>`  
  
 `</circle>`  
  
 `</circles>`  
  
## <a name="see-also"></a><span data-ttu-id="98faa-171">請參閱</span><span class="sxs-lookup"><span data-stu-id="98faa-171">See also</span></span>

- [<span data-ttu-id="98faa-172">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="98faa-172">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)

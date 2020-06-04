---
title: XML 的函式轉換
ms.date: 07/20/2015
ms.assetid: fdbe5b91-f457-4b4e-a11b-def4bdd77bab
ms.openlocfilehash: b82030f5763f24feca5b50a5dd84283943ba9bcf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398444"
---
# <a name="functional-transformation-of-xml-visual-basic"></a><span data-ttu-id="831f7-102">XML 函數式轉換 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="831f7-102">Functional Transformation of XML (Visual Basic)</span></span>
<span data-ttu-id="831f7-103">本主題討論修改 XML 文件的純功能性轉換方法，並與程序性方法對照。</span><span class="sxs-lookup"><span data-stu-id="831f7-103">This topic discusses the pure functional transformation approach to modifying XML documents, and contrasts it with a procedural approach.</span></span>  
  
## <a name="modifying-an-xml-document"></a><span data-ttu-id="831f7-104">修改 XML 文件</span><span class="sxs-lookup"><span data-stu-id="831f7-104">Modifying an XML Document</span></span>  
 <span data-ttu-id="831f7-105">XML 程式設計人員其中一個最常見的工做為，將 XML 從一個組織結構轉換為另一個組織結構。</span><span class="sxs-lookup"><span data-stu-id="831f7-105">One of the most common tasks for an XML programmer is transforming XML from one shape to another.</span></span> <span data-ttu-id="831f7-106">XML 文件的組織結構就是文件的結構，其中包括：</span><span class="sxs-lookup"><span data-stu-id="831f7-106">The shape of an XML document is the structure of the document, which includes the following:</span></span>  
  
- <span data-ttu-id="831f7-107">以文件表示的階層。</span><span class="sxs-lookup"><span data-stu-id="831f7-107">The hierarchy expressed by the document.</span></span>  
  
- <span data-ttu-id="831f7-108">項目和屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="831f7-108">The element and attribute names.</span></span>  
  
- <span data-ttu-id="831f7-109">項目和屬性的資料型別。</span><span class="sxs-lookup"><span data-stu-id="831f7-109">The data types of the elements and attributes.</span></span>  
  
 <span data-ttu-id="831f7-110">一般而言，將 XML 從一個組織結構轉換為另一個組織結構最有效的方法是，純功能性轉換的方法。</span><span class="sxs-lookup"><span data-stu-id="831f7-110">In general, the most effective approach to transforming XML from one shape to another is that of pure functional transformation.</span></span> <span data-ttu-id="831f7-111">以此種方法，程式設計人員的主要工做為建立適用於整個 XML 文件 (或者一或多個嚴格定義的程式碼) 的轉換。</span><span class="sxs-lookup"><span data-stu-id="831f7-111">In this approach, the primary programmer task is to create a transformation which is applied to the entire XML document (or to one or more strictly defined nodes).</span></span> <span data-ttu-id="831f7-112">在論證上，功能性轉換對程式碼而言是最簡單的 (在程式設計人員熟悉方法之後)，它會產生最容易維護的程式碼，而且通常比替代方法更精簡。</span><span class="sxs-lookup"><span data-stu-id="831f7-112">Functional transformation is arguably the easiest to code (after a programmer is familiar with the approach), yields the most maintainable code, and is often more compact than alternative approaches.</span></span>  
  
### <a name="xml-functional-transformational-technologies"></a><span data-ttu-id="831f7-113">XML 功能性轉換技術</span><span class="sxs-lookup"><span data-stu-id="831f7-113">XML Functional Transformational Technologies</span></span>  
 <span data-ttu-id="831f7-114">Microsoft 提供兩個可用於 XML 文件的功能性轉換技術：XSLT 和 LINQ to XML。</span><span class="sxs-lookup"><span data-stu-id="831f7-114">Microsoft offers two functional transformation technologies for use on XML documents: XSLT and LINQ to XML.</span></span> <span data-ttu-id="831f7-115">在 <xref:System.Xml.Xsl> Managed 命名空間與 MSXML 的原始 COM 實作中支援 XSLT。</span><span class="sxs-lookup"><span data-stu-id="831f7-115">XSLT is supported in the <xref:System.Xml.Xsl> managed namespace and in the native COM implementation of MSXML.</span></span> <span data-ttu-id="831f7-116">雖然 XSLT 是強大的管理 XML 文件技術，但是它需要特殊領域的專業知識，也就是 XSLT 語言及其支援的 API。</span><span class="sxs-lookup"><span data-stu-id="831f7-116">Although XSLT is a robust technology for manipulating XML documents, it requires expertise in a specialized domain, namely the XSLT language and its supporting APIs.</span></span>  
  
 <span data-ttu-id="831f7-117">LINQ to XML 在 C# 或 Visual Basic 程式碼中，提供以明確而且強大的方式撰寫純功能性轉換之程式碼所需的工具。</span><span class="sxs-lookup"><span data-stu-id="831f7-117">LINQ to XML provides the tools necessary to code pure functional transformations in an expressive and powerful way, within C# or Visual Basic code.</span></span> <span data-ttu-id="831f7-118">例如，LINQ to XML 文件中的許多範例都使用純功能性方法。</span><span class="sxs-lookup"><span data-stu-id="831f7-118">For example, many of the examples in the LINQ to XML documentation use a pure functional approach.</span></span> <span data-ttu-id="831f7-119">此外，在[教學課程：管理 WordprocessingML 檔中的內容（Visual Basic）](tutorial-manipulating-content-in-a-wordprocessingml-document.md)教學課程中，我們使用 LINQ to XML 的功能方法，來操作 Microsoft Word 檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="831f7-119">Also, in the [Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)](tutorial-manipulating-content-in-a-wordprocessingml-document.md) tutorial, we use LINQ to XML in a functional approach to manipulate information in a Microsoft Word document.</span></span>  
  
 <span data-ttu-id="831f7-120">如需更完整的 LINQ to XML 與其他 Microsoft XML 技術的比較，請參閱[LINQ to XML 與其他 Xml 技術](linq-to-xml-vs-other-xml-technologies.md)。</span><span class="sxs-lookup"><span data-stu-id="831f7-120">For a more complete comparison of LINQ to XML with other Microsoft XML technologies, see [LINQ to XML vs. Other XML Technologies](linq-to-xml-vs-other-xml-technologies.md).</span></span>  
  
 <span data-ttu-id="831f7-121">當來源文件具有不規則的結構時，XSLT 是文件中心轉換的建議工具。</span><span class="sxs-lookup"><span data-stu-id="831f7-121">XSLT is the recommended tool for  document-centric transformations when the source document has an irregular structure.</span></span> <span data-ttu-id="831f7-122">不過，LINQ to XML 也可以執行文件中心的轉換。</span><span class="sxs-lookup"><span data-stu-id="831f7-122">However, LINQ to XML can also perform document-centric transforms.</span></span> <span data-ttu-id="831f7-123">如需詳細資訊，請參閱[如何：使用注釋轉換 XSLT 樣式的 LINQ to XML 樹狀結構（Visual Basic）](how-to-use-annotation-trees-to-transform-linq-to-xml-trees-in-an-xslt-style.md)。</span><span class="sxs-lookup"><span data-stu-id="831f7-123">For more information, see [How to: Use Annotations to Transform LINQ to XML Trees in an XSLT Style (Visual Basic)](how-to-use-annotation-trees-to-transform-linq-to-xml-trees-in-an-xslt-style.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="831f7-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="831f7-124">See also</span></span>

- [<span data-ttu-id="831f7-125">純功能性轉換簡介（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="831f7-125">Introduction to Pure Functional Transformations (Visual Basic)</span></span>](introduction-to-pure-functional-transformations.md)
- [<span data-ttu-id="831f7-126">LINQ to XML 比較其他 XML 技術之比較</span><span class="sxs-lookup"><span data-stu-id="831f7-126">LINQ to XML vs. Other XML Technologies</span></span>](linq-to-xml-vs-other-xml-technologies.md)

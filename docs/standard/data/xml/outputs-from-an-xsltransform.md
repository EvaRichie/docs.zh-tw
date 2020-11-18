---
title: XslTransform 的輸出
ms.date: 03/30/2017
ms.assetid: 8e149d32-4b2f-493f-9e4b-d0d93475acde
ms.openlocfilehash: 765f6f9a91cc44a55ab0d66ed71f19f60ef81a56
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830060"
---
# <a name="outputs-from-an-xsltransform"></a><span data-ttu-id="a5ccf-102">XslTransform 的輸出</span><span class="sxs-lookup"><span data-stu-id="a5ccf-102">Outputs from an XslTransform</span></span>
<span data-ttu-id="a5ccf-103">由於樣式表可以使用 `<xsl:output>` 陳述式以及 `method` 屬性決定輸出格式，因此下表將說明在使用 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法寫入輸出，且輸出格式宣告為 <xref:System.IO.Stream> 或 <xref:System.IO.TextWriter> 時，將產生何種輸出格式。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-103">Since style sheets can determine the output format using an `<xsl:output>` statement with the `method` attribute, the following table describes what the output format is when the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is used to write the output, and the output format is declared as a <xref:System.IO.Stream> or <xref:System.IO.TextWriter>.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a5ccf-104">在 .NET Framework 2.0 中，<xref:System.Xml.Xsl.XslTransform> 類別已過時。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-104">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="a5ccf-105">您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行可延伸樣式表語言轉換 (XSLT)。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-105">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="a5ccf-106">如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-106">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>  
  
 <span data-ttu-id="a5ccf-107">由於樣式表可以使用 `<xsl:output>` 陳述式以及 `method` 屬性決定輸出格式，因此下表將說明在使用 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法寫入輸出，且輸出格式宣告為 <xref:System.IO.Stream> 或 <xref:System.IO.TextWriter> 時，將產生何種輸出格式。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-107">Since style sheets can determine the output format using an `<xsl:output>` statement with the `method` attribute, the following table describes what the output format is when the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is used to write the output, and the output format is declared as a <xref:System.IO.Stream> or <xref:System.IO.TextWriter>.</span></span> <span data-ttu-id="a5ccf-108">下表說明在輸出型別由 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法進行宣告，並且搭配使用 `<xsl:output>` 陳述式時，將發生哪些情況：</span><span class="sxs-lookup"><span data-stu-id="a5ccf-108">The following table describes what happens when an output type is declared by the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method in conjunction with the use of an `<xsl:output>` statement:</span></span>  
  
|<span data-ttu-id="a5ccf-109">\<xsl:output method = > 屬性</span><span class="sxs-lookup"><span data-stu-id="a5ccf-109">\<xsl:output method = > attribute</span></span>|<span data-ttu-id="a5ccf-110">結果格式</span><span class="sxs-lookup"><span data-stu-id="a5ccf-110">Result format</span></span>|  
|-----------------------------------------|-------------------|  
|<span data-ttu-id="a5ccf-111">method="xml"</span><span class="sxs-lookup"><span data-stu-id="a5ccf-111">method="xml"</span></span>|<span data-ttu-id="a5ccf-112">XML</span><span class="sxs-lookup"><span data-stu-id="a5ccf-112">XML</span></span>|  
|<span data-ttu-id="a5ccf-113">method="html"</span><span class="sxs-lookup"><span data-stu-id="a5ccf-113">method="html"</span></span>|<span data-ttu-id="a5ccf-114">HTML</span><span class="sxs-lookup"><span data-stu-id="a5ccf-114">HTML</span></span>|  
|<span data-ttu-id="a5ccf-115">method="text"</span><span class="sxs-lookup"><span data-stu-id="a5ccf-115">method="text"</span></span>|<span data-ttu-id="a5ccf-116">Text</span><span class="sxs-lookup"><span data-stu-id="a5ccf-116">Text</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="a5ccf-117">注意：當 `<xsl:output>` 方法的輸出是 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 或 <xref:System.Xml.XmlReader> 時，將會忽略 <xref:System.Xml.XmlWriter> 陳述式。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-117">Note: The `<xsl:output>` statement is ignored when the output of the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is an <xref:System.Xml.XmlReader> or <xref:System.Xml.XmlWriter>.</span></span>  
  
 <span data-ttu-id="a5ccf-118">當 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法輸出為 <xref:System.IO.Stream> 或 <xref:System.IO.TextWriter> 時，可支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a5ccf-118">The following attributes are supported when the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method output is a <xref:System.IO.Stream> or <xref:System.IO.TextWriter>:</span></span>  
  
- <span data-ttu-id="a5ccf-119">encoding\*</span><span class="sxs-lookup"><span data-stu-id="a5ccf-119">encoding\*</span></span>  
  
- <span data-ttu-id="a5ccf-120">omit-xml-declaration</span><span class="sxs-lookup"><span data-stu-id="a5ccf-120">omit-xml-declaration</span></span>  
  
- <span data-ttu-id="a5ccf-121">獨立</span><span class="sxs-lookup"><span data-stu-id="a5ccf-121">standalone</span></span>  
  
- <span data-ttu-id="a5ccf-122">doctype-public</span><span class="sxs-lookup"><span data-stu-id="a5ccf-122">doctype-public</span></span>  
  
- <span data-ttu-id="a5ccf-123">doctype-system</span><span class="sxs-lookup"><span data-stu-id="a5ccf-123">doctype-system</span></span>  
  
- <span data-ttu-id="a5ccf-124">cdata-section-elements</span><span class="sxs-lookup"><span data-stu-id="a5ccf-124">cdata-section-elements</span></span>  
  
- <span data-ttu-id="a5ccf-125">indent</span><span class="sxs-lookup"><span data-stu-id="a5ccf-125">indent</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="a5ccf-126">\*當 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法傳送其輸出給 <xref:System.IO.TextWriter> 時，將會忽略編碼屬性。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-126">\*The encoding attribute is ignored when the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is sending its output to a <xref:System.IO.TextWriter>.</span></span> <span data-ttu-id="a5ccf-127">會改用 <xref:System.IO.TextWriter> 上的編碼屬性。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-127">The encoding property on the <xref:System.IO.TextWriter> is used instead.</span></span>
  
 <span data-ttu-id="a5ccf-128">當 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法輸出是 <xref:System.IO.Stream> 時，將會忽略下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a5ccf-128">The following attribute is ignored when the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method output is a <xref:System.IO.Stream>:</span></span>  
  
- <span data-ttu-id="a5ccf-129">版本：版本一律為 1.0</span><span class="sxs-lookup"><span data-stu-id="a5ccf-129">version: the version is always 1.0</span></span>  
  
- <span data-ttu-id="a5ccf-130">媒體類型：媒體類型</span><span class="sxs-lookup"><span data-stu-id="a5ccf-130">media-type: the media-type</span></span>  
  
## <a name="escaping-special-characters"></a><span data-ttu-id="a5ccf-131">逸出特殊字元</span><span class="sxs-lookup"><span data-stu-id="a5ccf-131">Escaping Special Characters</span></span>  
 <span data-ttu-id="a5ccf-132">`<xsl:text disable-output-escaping>` 標記可用來指示特殊字元是否必須逸出為 XML 格式 (例如，以 `<&lt>` 取代 `"<"` 符號)，或必須保持現有的狀況。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-132">The `<xsl:text disable-output-escaping>` tag is used to indicate whether or not special characters need to be escaped into an XML form (for example, using `<&lt>` in place of the `"<"` symbol) or left in the present condition.</span></span> <span data-ttu-id="a5ccf-133">當轉換為 `disable-output-escaping` 或 <xref:System.Xml.XmlReader> 物件時，會忽略 <xref:System.Xml.XmlWriter> 屬性，這對於特殊字元不會有任何影響。</span><span class="sxs-lookup"><span data-stu-id="a5ccf-133">The `disable-output-escaping` attribute is ignored when transforming to an <xref:System.Xml.XmlReader> or <xref:System.Xml.XmlWriter> object and has no effect on special characters.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a5ccf-134">請參閱</span><span class="sxs-lookup"><span data-stu-id="a5ccf-134">See also</span></span>

- [<span data-ttu-id="a5ccf-135">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="a5ccf-135">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)

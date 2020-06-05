---
title: 如何：從檔案、字串或資料流載入 XML
ms.date: 07/20/2015
helpviewer_keywords:
- XML [Visual Basic], loading
- LINQ to XML [Visual Basic], loading XML from files
ms.assetid: 2b02dcec-4cca-4575-b4ad-89ceb87b984c
ms.openlocfilehash: 7f2a961ebb7ecd4fc0512e141b4a437be87bec0e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392284"
---
# <a name="how-to-load-xml-from-a-file-string-or-stream-visual-basic"></a><span data-ttu-id="5e138-102">如何：從檔案、字串或資料流載入 XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="5e138-102">How to: Load XML from a File, String, or Stream (Visual Basic)</span></span>

<span data-ttu-id="5e138-103">您可以使用數種方法來建立[XML 常](../../../language-reference/xml-literals/index.md)值，並以外部來源（例如檔案、字串或資料流程）的內容填入。</span><span class="sxs-lookup"><span data-stu-id="5e138-103">You can create [XML Literals](../../../language-reference/xml-literals/index.md) and populate them with the contents from an external source such as a file, a string, or a stream by using several methods.</span></span> <span data-ttu-id="5e138-104">下列範例會顯示這些方法。</span><span class="sxs-lookup"><span data-stu-id="5e138-104">These methods are shown in the following examples.</span></span>

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-load-xml-from-a-file"></a><span data-ttu-id="5e138-105">從檔案載入 XML</span><span class="sxs-lookup"><span data-stu-id="5e138-105">To load XML from a file</span></span>

<span data-ttu-id="5e138-106">若要從檔案填入 XML 常值（例如） <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件，請使用 `Load` 方法。</span><span class="sxs-lookup"><span data-stu-id="5e138-106">To populate an XML literal such as an <xref:System.Xml.Linq.XElement> or <xref:System.Xml.Linq.XDocument> object from a file, use the `Load` method.</span></span> <span data-ttu-id="5e138-107">這個方法可以接受檔案路徑、文字資料流程或 XML 資料流程做為輸入。</span><span class="sxs-lookup"><span data-stu-id="5e138-107">This method can take a file path, text stream, or XML stream as input.</span></span>

<span data-ttu-id="5e138-108">下列程式碼範例示範 <xref:System.Xml.Linq.XDocument.Load%28System.String%29> 如何使用方法，將 <xref:System.Xml.Linq.XDocument> 文字檔中的 XML 填入物件。</span><span class="sxs-lookup"><span data-stu-id="5e138-108">The following code example shows the use of the <xref:System.Xml.Linq.XDocument.Load%28System.String%29> method to populate an <xref:System.Xml.Linq.XDocument> object with XML from a text file.</span></span>

[!code-vb[VbXMLSamples#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#43)]

## <a name="to-load-xml-from-a-string"></a><span data-ttu-id="5e138-109">從字串載入 XML</span><span class="sxs-lookup"><span data-stu-id="5e138-109">To load XML from a string</span></span>

<span data-ttu-id="5e138-110">若要從字串填入 XML 常值（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件），您可以使用 `Parse` 方法。</span><span class="sxs-lookup"><span data-stu-id="5e138-110">To populate an XML literal such as an <xref:System.Xml.Linq.XElement> or <xref:System.Xml.Linq.XDocument> object from a string, you can use the `Parse` method.</span></span>

<span data-ttu-id="5e138-111">下列程式碼範例示範 <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=nameWithType> 如何使用方法，將 <xref:System.Xml.Linq.XDocument> 字串中的 XML 填入物件。</span><span class="sxs-lookup"><span data-stu-id="5e138-111">The following code example shows the use of the <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=nameWithType> method to populate an <xref:System.Xml.Linq.XDocument> object with XML from a string.</span></span>

[!code-vb[VbXMLSamples#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#47)]

## <a name="to-load-xml-from-a-stream"></a><span data-ttu-id="5e138-112">從資料流程載入 XML</span><span class="sxs-lookup"><span data-stu-id="5e138-112">To load XML from a stream</span></span>

<span data-ttu-id="5e138-113">若要從資料流程填入 XML 常值（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件），您可以使用 `Load` 方法或 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="5e138-113">To populate an XML literal such as an <xref:System.Xml.Linq.XElement> or <xref:System.Xml.Linq.XDocument> object from a stream, you can use the `Load` method or the <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="5e138-114">下列程式碼範例示範 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 如何使用方法，以 xml 資料流程的 <xref:System.Xml.Linq.XDocument> xml 填入物件。</span><span class="sxs-lookup"><span data-stu-id="5e138-114">The following code example shows the use of the <xref:System.Xml.Linq.XNode.ReadFrom%2A> method to populate an <xref:System.Xml.Linq.XDocument> object with XML from an XML stream.</span></span>

[!code-vb[VbXMLSamples#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#46)]

## <a name="see-also"></a><span data-ttu-id="5e138-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5e138-115">See also</span></span>

- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType>
- [<span data-ttu-id="5e138-116">XML 常值</span><span class="sxs-lookup"><span data-stu-id="5e138-116">XML Literals</span></span>](../../../language-reference/xml-literals/index.md)
- [<span data-ttu-id="5e138-117">XML</span><span class="sxs-lookup"><span data-stu-id="5e138-117">XML</span></span>](index.md)
- [<span data-ttu-id="5e138-118">在 Visual Basic 中管理 XML</span><span class="sxs-lookup"><span data-stu-id="5e138-118">Manipulating XML in Visual Basic</span></span>](manipulating-xml.md)

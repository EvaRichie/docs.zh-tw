---
title: 如何：將運算式內嵌在 XML 常值中
ms.date: 07/20/2015
helpviewer_keywords:
- embedded expressions [Visual Basic]
- XML literals [Visual Basic], embedded expressions
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
ms.openlocfilehash: 59ba03be6e132203523427d3b7af5a163b6f05ac
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392310"
---
# <a name="how-to-embed-expressions-in-xml-literals-visual-basic"></a><span data-ttu-id="59bf4-102">如何：將運算式內嵌在 XML 常值中 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="59bf4-102">How to: Embed Expressions in XML Literals (Visual Basic)</span></span>
<span data-ttu-id="59bf4-103">您可以結合 XML 常值與內嵌運算式，建立 XML 檔、片段或包含在執行時間建立之內容的元素。</span><span class="sxs-lookup"><span data-stu-id="59bf4-103">You can combine XML literals with embedded expressions to create an XML document, fragment, or element that contains content created at run time.</span></span> <span data-ttu-id="59bf4-104">下列範例示範如何在執行時間使用內嵌運算式來填入元素內容、屬性和專案名稱。</span><span class="sxs-lookup"><span data-stu-id="59bf4-104">The following examples demonstrate how to use embedded expressions to populate element content, attributes, and element names at run time.</span></span>  
  
 <span data-ttu-id="59bf4-105">內嵌運算式的語法是 `<%=` `exp` `%>` ，這是 ASP.NET 所使用的相同語法。</span><span class="sxs-lookup"><span data-stu-id="59bf4-105">The syntax for an embedded expression is `<%=` `exp` `%>`, which is the same syntax that ASP.NET uses.</span></span> <span data-ttu-id="59bf4-106">如需詳細資訊，請參閱[XML 中的內嵌運算式](embedded-expressions-in-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="59bf4-106">For more information, see [Embedded Expressions in XML](embedded-expressions-in-xml.md).</span></span>  
  
 <span data-ttu-id="59bf4-107">您也可以使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] api 來建立 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 物件。</span><span class="sxs-lookup"><span data-stu-id="59bf4-107">You can also use the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] APIs to create [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] objects.</span></span> <span data-ttu-id="59bf4-108">如需詳細資訊，請參閱 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="59bf4-108">For more information, see <xref:System.Xml.Linq.XElement>.</span></span>  
  
## <a name="procedures"></a><span data-ttu-id="59bf4-109">程序</span><span class="sxs-lookup"><span data-stu-id="59bf4-109">Procedures</span></span>  
  
#### <a name="to-insert-text-as-element-content"></a><span data-ttu-id="59bf4-110">插入文字做為元素內容</span><span class="sxs-lookup"><span data-stu-id="59bf4-110">To insert text as element content</span></span>  
  
- <span data-ttu-id="59bf4-111">下列範例示範如何在 `contactName` 開頭和結尾名稱元素之間插入變數中包含的文字。</span><span class="sxs-lookup"><span data-stu-id="59bf4-111">The following example shows how to insert the text that is contained in the `contactName` variable between the opening and closing name elements.</span></span>  
  
     [!code-vb[VbXMLSamples#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#39)]  
  
     <span data-ttu-id="59bf4-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="59bf4-112">This example produces the following output:</span></span>  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-as-an-attribute-value"></a><span data-ttu-id="59bf4-113">若要將文字插入為屬性值</span><span class="sxs-lookup"><span data-stu-id="59bf4-113">To insert text as an attribute value</span></span>  
  
- <span data-ttu-id="59bf4-114">下列範例顯示如何將變數中包含的文字插入 `phoneType` 為屬性的值 `type` 。</span><span class="sxs-lookup"><span data-stu-id="59bf4-114">The following example shows how to insert the text that is contained in the `phoneType` variable as the value of the `type` attribute.</span></span>  
  
     [!code-vb[VbXMLSamples#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#40)]  
  
     <span data-ttu-id="59bf4-115">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="59bf4-115">This example produces the following output:</span></span>  
  
    ```xml  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-for-an-element-name"></a><span data-ttu-id="59bf4-116">若要插入元素名稱的文字</span><span class="sxs-lookup"><span data-stu-id="59bf4-116">To insert text for an element name</span></span>  
  
- <span data-ttu-id="59bf4-117">下列範例示範如何將變數中包含的文字插入 `elementName` 為專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="59bf4-117">The following example shows how to insert the text that is contained in the `elementName` variable as the name of an element.</span></span>  
  
     <span data-ttu-id="59bf4-118">使用這項技術來建立專案時，您必須使用標記來關閉它們 \</> 。</span><span class="sxs-lookup"><span data-stu-id="59bf4-118">When creating elements by using this technique, you must close them with the \</> tag.</span></span>  
  
     [!code-vb[VbXMLSamples#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#41)]  
  
     <span data-ttu-id="59bf4-119">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="59bf4-119">This example produces the following output:</span></span>  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="59bf4-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="59bf4-120">See also</span></span>

- [<span data-ttu-id="59bf4-121">如何：建立 XML 常值</span><span class="sxs-lookup"><span data-stu-id="59bf4-121">How to: Create XML Literals</span></span>](how-to-create-xml-literals.md)
- [<span data-ttu-id="59bf4-122">XML 中內嵌的運算式</span><span class="sxs-lookup"><span data-stu-id="59bf4-122">Embedded Expressions in XML</span></span>](embedded-expressions-in-xml.md)
- [<span data-ttu-id="59bf4-123">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="59bf4-123">Creating XML in Visual Basic</span></span>](creating-xml.md)
- [<span data-ttu-id="59bf4-124">XML</span><span class="sxs-lookup"><span data-stu-id="59bf4-124">XML</span></span>](index.md)

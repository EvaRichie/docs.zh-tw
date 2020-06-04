---
title: XML 常值中的空白字元
ms.date: 07/20/2015
helpviewer_keywords:
- white space [XML in Visual Basic]
- XML literals [Visual Basic], white space
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
ms.openlocfilehash: b3caf7ac052f3fed3fe5427da0cc96bbdd955ea6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360471"
---
# <a name="white-space-in-xml-literals-visual-basic"></a><span data-ttu-id="97538-102">XML 常值中的空白字元 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="97538-102">White Space in XML Literals (Visual Basic)</span></span>
<span data-ttu-id="97538-103">Visual Basic 編譯器在建立物件時，只會納入 XML 常值中的重要空白字元 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="97538-103">The Visual Basic compiler incorporates only the significant white space characters from an XML literal when it creates a [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object.</span></span> <span data-ttu-id="97538-104">無意義的空白字元不會合並。</span><span class="sxs-lookup"><span data-stu-id="97538-104">The insignificant white space characters are not incorporated.</span></span>  
  
## <a name="significant-and-insignificant-white-space"></a><span data-ttu-id="97538-105">重要且無意義的空白字元</span><span class="sxs-lookup"><span data-stu-id="97538-105">Significant and Insignificant White Space</span></span>  
 <span data-ttu-id="97538-106">XML 常值中的空白字元只有三個區域才有意義：</span><span class="sxs-lookup"><span data-stu-id="97538-106">White space characters in XML literals are significant in only three areas:</span></span>  
  
- <span data-ttu-id="97538-107">當它們在屬性值中時。</span><span class="sxs-lookup"><span data-stu-id="97538-107">When they are in an attribute value.</span></span>  
  
- <span data-ttu-id="97538-108">當它們是元素文字內容的一部分，而且文字也包含其他字元時。</span><span class="sxs-lookup"><span data-stu-id="97538-108">When they are part of an element's text content and the text also contains other characters.</span></span>  
  
- <span data-ttu-id="97538-109">當它們位於專案文字內容的內嵌運算式中時。</span><span class="sxs-lookup"><span data-stu-id="97538-109">When they are in an embedded expression for an element's text content.</span></span>  
  
 <span data-ttu-id="97538-110">否則，編譯器會將空白字元視為不重要的字元，而且不會在常值的物件中包含 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="97538-110">Otherwise, the compiler treats white space characters as insignificant and does not include then in the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] object for the literal.</span></span>  
  
 <span data-ttu-id="97538-111">若要在 XML 常值中包含無意義的空白字元，請使用包含含有空白字元之字串常值的內嵌運算式。</span><span class="sxs-lookup"><span data-stu-id="97538-111">To include insignificant white space in an XML literal, use an embedded expression that contains a string literal with the white space.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="97538-112">如果 `xml:space` 屬性出現在 XML 專案常值中，Visual Basic 編譯器會在物件中包含屬性 <xref:System.Xml.Linq.XElement> ，但新增這個屬性並不會變更編譯器處理空白字元的方式。</span><span class="sxs-lookup"><span data-stu-id="97538-112">If the `xml:space` attribute appears in an XML element literal, the Visual Basic compiler includes the attribute in the <xref:System.Xml.Linq.XElement> object, but adding this attribute does not change how the compiler treats white space.</span></span>  
  
## <a name="examples"></a><span data-ttu-id="97538-113">範例</span><span class="sxs-lookup"><span data-stu-id="97538-113">Examples</span></span>  
 <span data-ttu-id="97538-114">下列範例包含兩個 XML 元素，外部和內部。</span><span class="sxs-lookup"><span data-stu-id="97538-114">The following example contains two XML elements, outer and inner.</span></span> <span data-ttu-id="97538-115">這兩個元素在其文字內容中都包含空白字元。</span><span class="sxs-lookup"><span data-stu-id="97538-115">Both elements contain white space in their text content.</span></span> <span data-ttu-id="97538-116">專用項目中的空白字元是不重要的，因為它只包含空白字元和 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="97538-116">The white space in the outer element is insignificant because it contains only white space and an XML element.</span></span> <span data-ttu-id="97538-117">內部元素中的空白字元很重要，因為它包含空白字元和文字。</span><span class="sxs-lookup"><span data-stu-id="97538-117">The white space in the inner element is significant because it contains white space and text.</span></span>  
  
 [!code-vb[VbXMLSamples#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#29)]  
  
 <span data-ttu-id="97538-118">執行時，此程式碼會顯示下列文字。</span><span class="sxs-lookup"><span data-stu-id="97538-118">When run, this code displays the following text.</span></span>  
  
```xml  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## <a name="see-also"></a><span data-ttu-id="97538-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="97538-119">See also</span></span>

- [<span data-ttu-id="97538-120">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="97538-120">Creating XML in Visual Basic</span></span>](creating-xml.md)

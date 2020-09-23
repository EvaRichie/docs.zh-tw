---
title: 如何：存取 XML 子項目
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
ms.openlocfilehash: 9c33bec9b9ea865d570bab08f27227129867cce9
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91058296"
---
# <a name="how-to-access-xml-child-elements-visual-basic"></a><span data-ttu-id="3560d-102">如何：存取 XML 子項目 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3560d-102">How to: Access XML Child Elements (Visual Basic)</span></span>

<span data-ttu-id="3560d-103">這個範例示範如何使用子軸屬性來存取 XML 專案中具有指定名稱的所有 XML 子項目。</span><span class="sxs-lookup"><span data-stu-id="3560d-103">This example shows how to use a child axis property to access all XML child elements that have a specified name in an XML element.</span></span> <span data-ttu-id="3560d-104">尤其是，它會使用 <xref:System.Xml.Linq.XElement.Value%2A> 屬性，取得集合中子軸屬性傳回之第一個元素的值 `name` 。</span><span class="sxs-lookup"><span data-stu-id="3560d-104">In particular, it uses the <xref:System.Xml.Linq.XElement.Value%2A> property to get the value of the first element in the collection that the `name` child axis property returns.</span></span> <span data-ttu-id="3560d-105">`name`子軸屬性會取得 `phone` 物件中所命名的所有子項目 `contact` 。</span><span class="sxs-lookup"><span data-stu-id="3560d-105">The `name` child axis property gets all child elements named `phone` in the `contact` object.</span></span> <span data-ttu-id="3560d-106">此範例也會使用 [ `phone` 子軸] 屬性來存取物件中所包含的所有子專案（名稱為 `phone` ） `contact` 。</span><span class="sxs-lookup"><span data-stu-id="3560d-106">This example also uses the `phone` child axis property to access all child elements named `phone` that are contained in the `contact` object.</span></span>  
  
## <a name="example"></a><span data-ttu-id="3560d-107">範例</span><span class="sxs-lookup"><span data-stu-id="3560d-107">Example</span></span>  

 [!code-vb[VbXMLSamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples4.vb#10)]  
  
## <a name="compile-the-code"></a><span data-ttu-id="3560d-108">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="3560d-108">Compile the code</span></span>  

 <span data-ttu-id="3560d-109">這個範例需要：</span><span class="sxs-lookup"><span data-stu-id="3560d-109">This example requires:</span></span>  
  
- <span data-ttu-id="3560d-110"><xref:System.Xml.Linq> 命名空間的參考。</span><span class="sxs-lookup"><span data-stu-id="3560d-110">A reference to the <xref:System.Xml.Linq> namespace.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3560d-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3560d-111">See also</span></span>

- <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>
- [<span data-ttu-id="3560d-112">XML Child Axis Property</span><span class="sxs-lookup"><span data-stu-id="3560d-112">XML Child Axis Property</span></span>](../../../language-reference/xml-axis/xml-child-axis-property.md)
- [<span data-ttu-id="3560d-113">XML 值屬性</span><span class="sxs-lookup"><span data-stu-id="3560d-113">XML Value Property</span></span>](../../../language-reference/xml-axis/xml-value-property.md)
- [<span data-ttu-id="3560d-114">在 Visual Basic 中存取 XML</span><span class="sxs-lookup"><span data-stu-id="3560d-114">Accessing XML in Visual Basic</span></span>](accessing-xml.md)
- [<span data-ttu-id="3560d-115">XML</span><span class="sxs-lookup"><span data-stu-id="3560d-115">XML</span></span>](index.md)

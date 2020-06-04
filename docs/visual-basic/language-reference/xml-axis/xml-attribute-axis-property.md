---
title: XML Attribute Axis Property
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyAttributeAxis
helpviewer_keywords:
- attribute axis property [Visual Basic]
- Visual Basic code, accessing XML
- XML attribute axis property [Visual Basic]
- XML axis [Visual Basic], attribute
- XML [Visual Basic], accessing
ms.assetid: 7a4777e1-0618-4de9-9510-fb9ace2bf4db
ms.openlocfilehash: 3f60190a949856cb2bbc2eba09d097c09089bea7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408428"
---
# <a name="xml-attribute-axis-property-visual-basic"></a><span data-ttu-id="8fdf7-102">XML 屬性軸屬性 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8fdf7-102">XML Attribute Axis Property (Visual Basic)</span></span>
<span data-ttu-id="8fdf7-103">提供物件之屬性值的存取權， <xref:System.Xml.Linq.XElement> 或物件集合中第一個元素的存取權限 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-103">Provides access to the value of an attribute for an <xref:System.Xml.Linq.XElement> object or to the first element in a collection of <xref:System.Xml.Linq.XElement> objects.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8fdf7-104">語法</span><span class="sxs-lookup"><span data-stu-id="8fdf7-104">Syntax</span></span>  
  
```vb  
object.@attribute  
' -or-  
object.@<attribute>  
```  
  
## <a name="parts"></a><span data-ttu-id="8fdf7-105">組件</span><span class="sxs-lookup"><span data-stu-id="8fdf7-105">Parts</span></span>  
 `object`  
 <span data-ttu-id="8fdf7-106">必要。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-106">Required.</span></span> <span data-ttu-id="8fdf7-107"><xref:System.Xml.Linq.XElement>物件或物件的集合 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-107">An <xref:System.Xml.Linq.XElement> object or a collection of <xref:System.Xml.Linq.XElement> objects.</span></span>  
  
 <span data-ttu-id="8fdf7-108">.@</span><span class="sxs-lookup"><span data-stu-id="8fdf7-108">.@</span></span>  
 <span data-ttu-id="8fdf7-109">必要。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-109">Required.</span></span> <span data-ttu-id="8fdf7-110">表示屬性軸屬性的開頭。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-110">Denotes the start of an attribute axis property.</span></span>  
  
 <  
 <span data-ttu-id="8fdf7-111">選擇性。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-111">Optional.</span></span> <span data-ttu-id="8fdf7-112">當不是 Visual Basic 中的有效識別碼時，表示屬性名稱的開頭 `attribute` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-112">Denotes the beginning of the name of the attribute when `attribute` is not a valid identifier in Visual Basic.</span></span>  
  
 `attribute`  
 <span data-ttu-id="8fdf7-113">必要。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-113">Required.</span></span> <span data-ttu-id="8fdf7-114">要存取的屬性名稱，格式為 [ `prefix` ：] `name` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-114">Name of the attribute to access, of the form [`prefix`:]`name`.</span></span>  
  
|<span data-ttu-id="8fdf7-115">部分</span><span class="sxs-lookup"><span data-stu-id="8fdf7-115">Part</span></span>|<span data-ttu-id="8fdf7-116">描述</span><span class="sxs-lookup"><span data-stu-id="8fdf7-116">Description</span></span>|  
|----------|-----------------|  
|`prefix`|<span data-ttu-id="8fdf7-117">選擇性。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-117">Optional.</span></span> <span data-ttu-id="8fdf7-118">屬性的 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-118">XML namespace prefix for the attribute.</span></span> <span data-ttu-id="8fdf7-119">必須是以 `Imports` 陳述式定義的全域 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-119">Must be a global XML namespace defined with an `Imports` statement.</span></span>|  
|`name`|<span data-ttu-id="8fdf7-120">必要。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-120">Required.</span></span> <span data-ttu-id="8fdf7-121">區域屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-121">Local attribute name.</span></span> <span data-ttu-id="8fdf7-122">請參閱宣告[的 XML 元素和屬性的名稱](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-122">See [Names of Declared XML Elements and Attributes](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).</span></span>|  
  
 \>  
 <span data-ttu-id="8fdf7-123">選擇性。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-123">Optional.</span></span> <span data-ttu-id="8fdf7-124">當不是 Visual Basic 中的有效識別碼時，代表屬性名稱的結尾 `attribute` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-124">Denotes the end of the name of the attribute when `attribute` is not a valid identifier in Visual Basic.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8fdf7-125">傳回值</span><span class="sxs-lookup"><span data-stu-id="8fdf7-125">Return Value</span></span>  
 <span data-ttu-id="8fdf7-126">包含值的字串 `attribute` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-126">A string that contains the value of `attribute`.</span></span> <span data-ttu-id="8fdf7-127">如果屬性名稱不存在， `Nothing` 則會傳回。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-127">If the attribute name does not exist, `Nothing` is returned.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8fdf7-128">備註</span><span class="sxs-lookup"><span data-stu-id="8fdf7-128">Remarks</span></span>  
 <span data-ttu-id="8fdf7-129">您可以使用 XML 屬性軸屬性，從物件的名稱， <xref:System.Xml.Linq.XElement> 或從物件集合中的第一個專案，存取屬性的值 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-129">You can use an XML attribute axis property to access the value of an attribute by name from an <xref:System.Xml.Linq.XElement> object or from the first element in a collection of <xref:System.Xml.Linq.XElement> objects.</span></span> <span data-ttu-id="8fdf7-130">您可以依名稱抓取屬性值，或指定新的名稱，並在前面加上 @ identifier，將新的屬性加入至元素。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-130">You can retrieve an attribute value by name, or add a new attribute to an element by specifying a new name preceded by the @ identifier.</span></span>  
  
 <span data-ttu-id="8fdf7-131">當您使用 @ identifier 來參考 XML 屬性時，屬性值會當做字串傳回，而且您不需要明確指定 <xref:System.Xml.Linq.XAttribute.Value%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-131">When you refer to an XML attribute using the @ identifier, the attribute value is returned as a string and you do not need to explicitly specify the <xref:System.Xml.Linq.XAttribute.Value%2A> property.</span></span>  
  
 <span data-ttu-id="8fdf7-132">XML 屬性的命名規則不同于 Visual Basic 識別碼的命名規則。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-132">The naming rules for XML attributes differ from the naming rules for Visual Basic identifiers.</span></span> <span data-ttu-id="8fdf7-133">若要存取名稱不是有效 Visual Basic 識別碼的 XML 屬性，請以角括弧（）括住名稱 \< and > 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-133">To access an XML attribute that has a name that is not a valid Visual Basic identifier, enclose the name in angle brackets (\< and >).</span></span>  
  
## <a name="xml-namespaces"></a><span data-ttu-id="8fdf7-134">XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="8fdf7-134">XML Namespaces</span></span>  
 <span data-ttu-id="8fdf7-135">屬性軸屬性中的名稱只能使用在全域宣告的 XML 命名空間前置詞（使用 `Imports` 語句）。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-135">The name in an attribute axis property can use only XML namespace prefixes declared globally by using the `Imports` statement.</span></span> <span data-ttu-id="8fdf7-136">它不能使用在 XML 項目常值內本機宣告的 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-136">It cannot use XML namespace prefixes declared locally within XML element literals.</span></span> <span data-ttu-id="8fdf7-137">如需詳細資訊，請參閱[Imports 語句（XML 命名空間）](../statements/imports-statement-xml-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-137">For more information, see [Imports Statement (XML Namespace)](../statements/imports-statement-xml-namespace.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="8fdf7-138">範例</span><span class="sxs-lookup"><span data-stu-id="8fdf7-138">Example</span></span>  
 <span data-ttu-id="8fdf7-139">下列範例示範如何從名為的 XML 專案集合中，取得名為之 XML 屬性的值 `type` `phone` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-139">The following example shows how to get the values of the XML attributes named `type` from a collection of XML elements that are named `phone`.</span></span>  
  
 [!code-vb[VbXMLSamples#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#12)]  
  
 <span data-ttu-id="8fdf7-140">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="8fdf7-140">This code displays the following text:</span></span>  
  
 `<phoneTypes>`  
  
 `<type>home</type>`  
  
 `<type>work</type>`  
  
 `</phoneTypes>`  
  
## <a name="example"></a><span data-ttu-id="8fdf7-141">範例</span><span class="sxs-lookup"><span data-stu-id="8fdf7-141">Example</span></span>  
 <span data-ttu-id="8fdf7-142">下列範例示範如何以宣告的方式，將 XML 專案的屬性建立為 XML 的一部分，並藉由將屬性新增至物件的實例來動態地執行 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-142">The following example shows how to create attributes for an XML element both declaratively, as part of the XML, and dynamically by adding an attribute to an instance of an <xref:System.Xml.Linq.XElement> object.</span></span> <span data-ttu-id="8fdf7-143">`type`屬性會以宣告方式建立，並且 `owner` 會動態建立屬性。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-143">The `type` attribute is created declaratively and the `owner` attribute is created dynamically.</span></span>  
  
 [!code-vb[VbXMLSamples#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#44)]  
  
 <span data-ttu-id="8fdf7-144">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="8fdf7-144">This code displays the following text:</span></span>  
  
```xml  
<phone type="home" owner="Harris, Phyllis">206-555-0144</phone>  
```  
  
## <a name="example"></a><span data-ttu-id="8fdf7-145">範例</span><span class="sxs-lookup"><span data-stu-id="8fdf7-145">Example</span></span>  
 <span data-ttu-id="8fdf7-146">下列範例會使用角括弧語法來取得名為之 XML 屬性的值 `number-type` ，這在 Visual Basic 中不是有效的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-146">The following example uses the angle bracket syntax to get the value of the XML attribute named `number-type`, which is not a valid identifier in Visual Basic.</span></span>  
  
 [!code-vb[VbXMLSamples#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#13)]  
  
 <span data-ttu-id="8fdf7-147">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="8fdf7-147">This code displays the following text:</span></span>  
  
 `Phone type: work`  
  
## <a name="example"></a><span data-ttu-id="8fdf7-148">範例</span><span class="sxs-lookup"><span data-stu-id="8fdf7-148">Example</span></span>  
 <span data-ttu-id="8fdf7-149">下列範例會宣告 `ns` 作為 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-149">The following example declares `ns` as an XML namespace prefix.</span></span> <span data-ttu-id="8fdf7-150">然後，它會使用命名空間的前置詞來建立 XML 常值，並存取具有限定名稱 "" 的第一個子節點 `ns:name` 。</span><span class="sxs-lookup"><span data-stu-id="8fdf7-150">It then uses the prefix of the namespace to create an XML literal and access the first child node with the qualified name "`ns:name`".</span></span>  
  
 [!code-vb[VbXMLSamples#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples6.vb#14)]  
  
 <span data-ttu-id="8fdf7-151">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="8fdf7-151">This code displays the following text:</span></span>  
  
 `Phone type: home`  
  
## <a name="see-also"></a><span data-ttu-id="8fdf7-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8fdf7-152">See also</span></span>

- <xref:System.Xml.Linq.XElement>
- [<span data-ttu-id="8fdf7-153">XML 軸屬性</span><span class="sxs-lookup"><span data-stu-id="8fdf7-153">XML Axis Properties</span></span>](index.md)
- [<span data-ttu-id="8fdf7-154">XML 常值</span><span class="sxs-lookup"><span data-stu-id="8fdf7-154">XML Literals</span></span>](../xml-literals/index.md)
- [<span data-ttu-id="8fdf7-155">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="8fdf7-155">Creating XML in Visual Basic</span></span>](../../programming-guide/language-features/xml/creating-xml.md)
- [<span data-ttu-id="8fdf7-156">宣告的 XML 項目和屬性的名稱</span><span class="sxs-lookup"><span data-stu-id="8fdf7-156">Names of Declared XML Elements and Attributes</span></span>](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)

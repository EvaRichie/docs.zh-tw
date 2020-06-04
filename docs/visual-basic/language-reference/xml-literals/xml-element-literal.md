---
title: XML 元素常值
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralElement
helpviewer_keywords:
- XML element literal [Visual Basic]
- element literal [Visual Basic]
- XML literals [Visual Basic], element
ms.assetid: 95039642-7893-48b7-b23f-45a6c55d8f67
ms.openlocfilehash: d6a91de4e279816bafd29f46bb4f5422cbd934ff
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400185"
---
# <a name="xml-element-literal-visual-basic"></a><span data-ttu-id="f2d5b-102">XML 項目常值 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f2d5b-102">XML Element Literal (Visual Basic)</span></span>

<span data-ttu-id="f2d5b-103">代表物件的常值 <xref:System.Xml.Linq.XElement> 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-103">A literal that represents an <xref:System.Xml.Linq.XElement> object.</span></span>

## <a name="syntax"></a><span data-ttu-id="f2d5b-104">語法</span><span class="sxs-lookup"><span data-stu-id="f2d5b-104">Syntax</span></span>

```xml
<name [ attributeList ] />
-or-
<name [ attributeList ] > [ elementContents ] </[ name ]>
```

## <a name="parts"></a><span data-ttu-id="f2d5b-105">組件</span><span class="sxs-lookup"><span data-stu-id="f2d5b-105">Parts</span></span>

- `<`

  <span data-ttu-id="f2d5b-106">必要。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-106">Required.</span></span> <span data-ttu-id="f2d5b-107">開啟起始元素標記。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-107">Opens the starting element tag.</span></span>

- `name`

  <span data-ttu-id="f2d5b-108">必要。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-108">Required.</span></span> <span data-ttu-id="f2d5b-109">元素名稱。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-109">Name of the element.</span></span> <span data-ttu-id="f2d5b-110">格式為下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-110">The format is one of the following:</span></span>

  - <span data-ttu-id="f2d5b-111">元素名稱的常值文字，格式為 `[ePrefix:]eName` ，其中：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-111">Literal text for the element name, of the form `[ePrefix:]eName`, where:</span></span>

    |<span data-ttu-id="f2d5b-112">部分</span><span class="sxs-lookup"><span data-stu-id="f2d5b-112">Part</span></span>|<span data-ttu-id="f2d5b-113">描述</span><span class="sxs-lookup"><span data-stu-id="f2d5b-113">Description</span></span>|
    |---|---|
    |`ePrefix`|<span data-ttu-id="f2d5b-114">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-114">Optional.</span></span> <span data-ttu-id="f2d5b-115">元素的 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-115">XML namespace prefix for the element.</span></span> <span data-ttu-id="f2d5b-116">必須是以檔案中的語句或在專案層級定義的全域 XML 命名空間 `Imports` ，或是在這個元素或父元素中定義的本機 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-116">Must be a global XML namespace that is defined with an `Imports` statement in the file or at the project level, or a local XML namespace that is defined in this element or a parent element.</span></span>|
    |`eName`|<span data-ttu-id="f2d5b-117">必要。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-117">Required.</span></span> <span data-ttu-id="f2d5b-118">元素名稱。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-118">Name of the element.</span></span> <span data-ttu-id="f2d5b-119">格式為下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-119">The format is one of the following:</span></span><br /><br /> <span data-ttu-id="f2d5b-120">-常值文字。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-120">- Literal text.</span></span> <span data-ttu-id="f2d5b-121">請參閱宣告[的 XML 元素和屬性的名稱](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-121">See [Names of Declared XML Elements and Attributes](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).</span></span><br /><span data-ttu-id="f2d5b-122">-表單的內嵌運算式 `<%= eNameExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-122">- Embedded expression of the form `<%= eNameExp %>`.</span></span> <span data-ttu-id="f2d5b-123">的類型 `eNameExp` 必須是 `String` 或可隱含轉換成的類型 <xref:System.Xml.Linq.XName> 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-123">The type of `eNameExp` must be `String` or a type that is implicitly convertible to <xref:System.Xml.Linq.XName>.</span></span>|

  - <span data-ttu-id="f2d5b-124">表單的內嵌運算式 `<%= nameExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-124">Embedded expression of the form `<%= nameExp %>`.</span></span> <span data-ttu-id="f2d5b-125">的類型 `nameExp` 必須是 `String` 或可隱含轉換成的類型 <xref:System.Xml.Linq.XName> 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-125">The type of `nameExp` must be `String` or a type implicitly convertible to <xref:System.Xml.Linq.XName>.</span></span> <span data-ttu-id="f2d5b-126">元素的結束記號中不允許內嵌運算式。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-126">An embedded expression is not allowed in a closing tag of an element.</span></span>

- `attributeList`

  <span data-ttu-id="f2d5b-127">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-127">Optional.</span></span> <span data-ttu-id="f2d5b-128">常值中宣告的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-128">List of attributes declared in the literal.</span></span>

  `attribute [ attribute ... ]`

  <span data-ttu-id="f2d5b-129">每個 `attribute` 都具有下列其中一個語法：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-129">Each `attribute` has one of the following syntaxes:</span></span>

  - <span data-ttu-id="f2d5b-130">屬性指派，格式為 `[aPrefix:]aName=aValue` ，其中：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-130">Attribute assignment, of the form `[aPrefix:]aName=aValue`, where:</span></span>

    |<span data-ttu-id="f2d5b-131">部分</span><span class="sxs-lookup"><span data-stu-id="f2d5b-131">Part</span></span>|<span data-ttu-id="f2d5b-132">描述</span><span class="sxs-lookup"><span data-stu-id="f2d5b-132">Description</span></span>|
    |---|---|
    |`aPrefix`|<span data-ttu-id="f2d5b-133">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-133">Optional.</span></span> <span data-ttu-id="f2d5b-134">屬性的 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-134">XML namespace prefix for the attribute.</span></span> <span data-ttu-id="f2d5b-135">必須是使用語句定義的全域 XML 命名空間 `Imports` ，或是在此元素或父元素中定義的本機 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-135">Must be a global XML namespace that is defined with an `Imports` statement, or a local XML namespace that is defined in this element or a parent element.</span></span>|
    |`aName`|<span data-ttu-id="f2d5b-136">必要。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-136">Required.</span></span> <span data-ttu-id="f2d5b-137">屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-137">Name of the attribute.</span></span> <span data-ttu-id="f2d5b-138">格式為下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-138">The format is one of the following:</span></span><br /><br /> <span data-ttu-id="f2d5b-139">-常值文字。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-139">- Literal text.</span></span> <span data-ttu-id="f2d5b-140">請參閱宣告[的 XML 元素和屬性的名稱](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-140">See [Names of Declared XML Elements and Attributes](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).</span></span><br /><span data-ttu-id="f2d5b-141">-表單的內嵌運算式 `<%= aNameExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-141">- Embedded expression of the form `<%= aNameExp %>`.</span></span> <span data-ttu-id="f2d5b-142">的類型 `aNameExp` 必須是 `String` 或可隱含轉換成的類型 <xref:System.Xml.Linq.XName> 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-142">The type of `aNameExp` must be `String` or a type that is implicitly convertible to <xref:System.Xml.Linq.XName>.</span></span>|
    |`aValue`|<span data-ttu-id="f2d5b-143">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-143">Optional.</span></span> <span data-ttu-id="f2d5b-144">屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-144">Value of the attribute.</span></span> <span data-ttu-id="f2d5b-145">格式為下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-145">The format is one of the following:</span></span><br /><br /> <span data-ttu-id="f2d5b-146">-包含在引號中的常值文字。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-146">- Literal text, enclosed in quotation marks.</span></span><br /><span data-ttu-id="f2d5b-147">-表單的內嵌運算式 `<%= aValueExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-147">- Embedded expression of the form `<%= aValueExp %>`.</span></span> <span data-ttu-id="f2d5b-148">允許任何類型。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-148">Any type is allowed.</span></span>|

  - <span data-ttu-id="f2d5b-149">表單的內嵌運算式 `<%= aExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-149">Embedded expression of the form `<%= aExp %>`.</span></span>

- `/>`

  <span data-ttu-id="f2d5b-150">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-150">Optional.</span></span> <span data-ttu-id="f2d5b-151">指出元素是空的元素，沒有內容。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-151">Indicates that the element is an empty element, without content.</span></span>

- `>`

  <span data-ttu-id="f2d5b-152">必要。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-152">Required.</span></span> <span data-ttu-id="f2d5b-153">結束開頭或空的元素標記。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-153">Ends the beginning or empty element tag.</span></span>

- `elementContents`

  <span data-ttu-id="f2d5b-154">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-154">Optional.</span></span> <span data-ttu-id="f2d5b-155">元素的內容。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-155">Content of the element.</span></span>

  `content [ content ... ]`

  <span data-ttu-id="f2d5b-156">每個都 `content` 可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-156">Each `content` can be one of the following:</span></span>

  - <span data-ttu-id="f2d5b-157">常值文字。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-157">Literal text.</span></span> <span data-ttu-id="f2d5b-158">`elementContents`如果有任何常值文字，中的所有空白字元都會變得很明顯。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-158">All the white space in `elementContents` becomes significant if there is any literal text.</span></span>

  - <span data-ttu-id="f2d5b-159">表單的內嵌運算式 `<%= contentExp %>` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-159">Embedded expression of the form `<%= contentExp %>`.</span></span>

  - <span data-ttu-id="f2d5b-160">XML 元素常值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-160">XML element literal.</span></span>

  - <span data-ttu-id="f2d5b-161">XML 批註常值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-161">XML comment literal.</span></span> <span data-ttu-id="f2d5b-162">請參閱[XML 批註常](xml-comment-literal.md)值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-162">See [XML Comment Literal](xml-comment-literal.md).</span></span>

  - <span data-ttu-id="f2d5b-163">XML 處理指示常值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-163">XML processing instruction literal.</span></span> <span data-ttu-id="f2d5b-164">請參閱[XML 處理指示常](xml-processing-instruction-literal.md)值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-164">See [XML Processing Instruction Literal](xml-processing-instruction-literal.md).</span></span>

  - <span data-ttu-id="f2d5b-165">XML CDATA 常值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-165">XML CDATA literal.</span></span> <span data-ttu-id="f2d5b-166">請參閱[XML CDATA 常](xml-cdata-literal.md)值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-166">See [XML CDATA Literal](xml-cdata-literal.md).</span></span>

- `</[name]>`

  <span data-ttu-id="f2d5b-167">選擇性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-167">Optional.</span></span> <span data-ttu-id="f2d5b-168">表示元素的結束記號。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-168">Represents the closing tag for the element.</span></span> <span data-ttu-id="f2d5b-169">`name`如果是內嵌運算式的結果，則不允許選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-169">The optional `name` parameter is not allowed when it is the result of an embedded expression.</span></span>

## <a name="return-value"></a><span data-ttu-id="f2d5b-170">傳回值</span><span class="sxs-lookup"><span data-stu-id="f2d5b-170">Return Value</span></span>

<span data-ttu-id="f2d5b-171"><xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-171">An <xref:System.Xml.Linq.XElement> object.</span></span>

## <a name="remarks"></a><span data-ttu-id="f2d5b-172">備註</span><span class="sxs-lookup"><span data-stu-id="f2d5b-172">Remarks</span></span>

<span data-ttu-id="f2d5b-173">您可以使用 XML 元素常值語法， <xref:System.Xml.Linq.XElement> 在您的程式碼中建立物件。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-173">You can use the XML element literal syntax to create <xref:System.Xml.Linq.XElement> objects in your code.</span></span>

> [!NOTE]
> <span data-ttu-id="f2d5b-174">XML 常值可以跨越多行，而不需要使用行接續字元。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-174">An XML literal can span multiple lines without using line continuation characters.</span></span> <span data-ttu-id="f2d5b-175">這項功能可讓您從 XML 檔案複製內容，並將它直接貼到 Visual Basic 程式中。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-175">This feature enables you to copy content from an XML document and paste it directly into a Visual Basic program.</span></span>

<span data-ttu-id="f2d5b-176">表單的內嵌運算式可 `<%= exp %>` 讓您將動態資訊新增至 XML 元素常值。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-176">Embedded expressions of the form `<%= exp %>` enable you to add dynamic information to an XML element literal.</span></span> <span data-ttu-id="f2d5b-177">如需詳細資訊，請參閱[XML 中的內嵌運算式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-177">For more information, see [Embedded Expressions in XML](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md).</span></span>

<span data-ttu-id="f2d5b-178">Visual Basic 編譯器會將 XML 專案常值轉換成對此函式的呼叫， <xref:System.Xml.Linq.XElement.%23ctor%2A> 如有需要，則會將它轉換為 <xref:System.Xml.Linq.XAttribute.%23ctor%2A> 函數。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-178">The Visual Basic compiler converts the XML element literal into calls to the <xref:System.Xml.Linq.XElement.%23ctor%2A> constructor and, if it is required, the <xref:System.Xml.Linq.XAttribute.%23ctor%2A> constructor.</span></span>

## <a name="xml-namespaces"></a><span data-ttu-id="f2d5b-179">XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="f2d5b-179">XML Namespaces</span></span>

<span data-ttu-id="f2d5b-180">當您必須在程式碼中多次使用相同命名空間的元素建立 XML 常值時，XML 命名空間前置詞非常有用。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-180">XML namespace prefixes are useful when you have to create XML literals with elements from the same namespace many times in code.</span></span> <span data-ttu-id="f2d5b-181">您可以使用全域 XML 命名空間前置詞，這是使用 `Imports` 語句或使用屬性語法定義的本機前置詞所定義 `xmlns:xmlPrefix="xmlNamespace"` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-181">You can use global XML namespace prefixes, which you define by using the `Imports` statement, or local prefixes, which you define by using the `xmlns:xmlPrefix="xmlNamespace"` attribute syntax.</span></span> <span data-ttu-id="f2d5b-182">如需詳細資訊，請參閱[Imports 語句（XML 命名空間）](../statements/imports-statement-xml-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-182">For more information, see [Imports Statement (XML Namespace)](../statements/imports-statement-xml-namespace.md).</span></span>

<span data-ttu-id="f2d5b-183">根據 XML 命名空間的範圍規則，本機前置詞的優先順序高於全域首碼。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-183">In accordance with the scoping rules for XML namespaces, local prefixes take precedence over global prefixes.</span></span> <span data-ttu-id="f2d5b-184">不過，如果 XML 常值定義 XML 命名空間，則該命名空間無法供內嵌運算式中出現的運算式使用。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-184">However, if an XML literal defines an XML namespace, that namespace is not available to expressions that appear in an embedded expression.</span></span> <span data-ttu-id="f2d5b-185">內嵌運算式只能存取全域 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-185">The embedded expression can access only the global XML namespace.</span></span>

<span data-ttu-id="f2d5b-186">Visual Basic 編譯器會將 XML 常值所使用的每個全域 XML 命名空間，轉換成產生的程式碼中的一個本機命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-186">The Visual Basic compiler converts each global XML namespace that is used by an XML literal into a one local namespace definition in the generated code.</span></span> <span data-ttu-id="f2d5b-187">未使用的全域 XML 命名空間不會出現在產生的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-187">Global XML namespaces that are not used do not appear in the generated code.</span></span>

## <a name="example"></a><span data-ttu-id="f2d5b-188">範例</span><span class="sxs-lookup"><span data-stu-id="f2d5b-188">Example</span></span>

<span data-ttu-id="f2d5b-189">下列範例顯示如何建立具有兩個嵌套空白元素的簡單 XML 專案。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-189">The following example shows how to create a simple XML element that has two nested empty elements.</span></span>

[!code-vb[VbXMLSamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#20)]

<span data-ttu-id="f2d5b-190">此範例會顯示下列文字。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-190">The example displays the following text.</span></span> <span data-ttu-id="f2d5b-191">請注意，常值會保留空白元素的結構。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-191">Notice that the literal preserves the structure of the empty elements.</span></span>

```xml
<outer>
  <inner1></inner1>
  <inner2 />
</outer>
```

## <a name="example"></a><span data-ttu-id="f2d5b-192">範例</span><span class="sxs-lookup"><span data-stu-id="f2d5b-192">Example</span></span>

<span data-ttu-id="f2d5b-193">下列範例顯示如何使用內嵌運算式來命名專案並建立屬性。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-193">The following example shows how to use embedded expressions to name an element and create attributes.</span></span>

[!code-vb[VbXMLSamples#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#21)]

<span data-ttu-id="f2d5b-194">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-194">This code displays the following text:</span></span>

```xml
<book isbn="1234" author="My Author" year="1999" title="My Book" />
```

## <a name="example"></a><span data-ttu-id="f2d5b-195">範例</span><span class="sxs-lookup"><span data-stu-id="f2d5b-195">Example</span></span>

<span data-ttu-id="f2d5b-196">下列範例會宣告 `ns` 作為 XML 命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-196">The following example declares `ns` as an XML namespace prefix.</span></span> <span data-ttu-id="f2d5b-197">然後，它會使用命名空間的前置詞來建立 XML 常值，並顯示專案的最終格式。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-197">It then uses the prefix of the namespace to create an XML literal and displays the element's final form.</span></span>

[!code-vb[VbXMLSamples#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples10.vb#22)]

<span data-ttu-id="f2d5b-198">此程式碼顯示下列文字：</span><span class="sxs-lookup"><span data-stu-id="f2d5b-198">This code displays the following text:</span></span>

```xml
<ns:outer xmlns:ns="http://SomeNamespace">
  <ns:middle xmlns:ns="http://NewNamespace">
    <ns:inner1 />
    <inner2 xmlns="http://SomeNamespace" />
  </ns:middle>
</ns:outer>
```

<span data-ttu-id="f2d5b-199">請注意，編譯器已將全域 XML 命名空間的前置詞，轉換成 XML 命名空間的前置詞定義。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-199">Notice that the compiler converted the prefix of the global XML namespace into a prefix definition for the XML namespace.</span></span> <span data-ttu-id="f2d5b-200">元素會重新 \<ns:middle> 定義元素的 XML 命名空間前置詞 \<ns:inner1> 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-200">The \<ns:middle> element redefines the XML namespace prefix for the \<ns:inner1> element.</span></span> <span data-ttu-id="f2d5b-201">不過， \<ns:inner2> 元素會使用語句所定義的命名空間 `Imports` 。</span><span class="sxs-lookup"><span data-stu-id="f2d5b-201">However, the \<ns:inner2> element uses the namespace defined by the `Imports` statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="f2d5b-202">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f2d5b-202">See also</span></span>

- <xref:System.Xml.Linq.XElement>
- [<span data-ttu-id="f2d5b-203">宣告的 XML 項目和屬性的名稱</span><span class="sxs-lookup"><span data-stu-id="f2d5b-203">Names of Declared XML Elements and Attributes</span></span>](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
- [<span data-ttu-id="f2d5b-204">XML 文件常值</span><span class="sxs-lookup"><span data-stu-id="f2d5b-204">XML Comment Literal</span></span>](xml-comment-literal.md)
- [<span data-ttu-id="f2d5b-205">XML CDATA 常值</span><span class="sxs-lookup"><span data-stu-id="f2d5b-205">XML CDATA Literal</span></span>](xml-cdata-literal.md)
- [<span data-ttu-id="f2d5b-206">XML 常值</span><span class="sxs-lookup"><span data-stu-id="f2d5b-206">XML Literals</span></span>](index.md)
- [<span data-ttu-id="f2d5b-207">在 Visual Basic 中建立 XML</span><span class="sxs-lookup"><span data-stu-id="f2d5b-207">Creating XML in Visual Basic</span></span>](../../programming-guide/language-features/xml/creating-xml.md)
- [<span data-ttu-id="f2d5b-208">XML 中內嵌的運算式</span><span class="sxs-lookup"><span data-stu-id="f2d5b-208">Embedded Expressions in XML</span></span>](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [<span data-ttu-id="f2d5b-209">Imports 陳述式 (XML 命名空間)</span><span class="sxs-lookup"><span data-stu-id="f2d5b-209">Imports Statement (XML Namespace)</span></span>](../statements/imports-statement-xml-namespace.md)

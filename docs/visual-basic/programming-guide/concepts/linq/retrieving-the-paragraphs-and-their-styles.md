---
title: 擷取段落及其樣式
ms.date: 07/20/2015
ms.assetid: d9ed2238-d38e-4ad4-b88b-db7859df9bde
ms.openlocfilehash: ad904abf9bd94e83b981859662c22787652e294f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413400"
---
# <a name="retrieving-the-paragraphs-and-their-styles-visual-basic"></a><span data-ttu-id="fc83c-102">抓取段落和其樣式（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="fc83c-102">Retrieving the Paragraphs and Their Styles (Visual Basic)</span></span>
<span data-ttu-id="fc83c-103">在此範例中，我們會撰寫一個從 WordprocessingML 文件擷取段落節點的查詢。</span><span class="sxs-lookup"><span data-stu-id="fc83c-103">In this example, we write a query that retrieves the paragraph nodes from a WordprocessingML document.</span></span> <span data-ttu-id="fc83c-104">它也可以識別每個段落的樣式。</span><span class="sxs-lookup"><span data-stu-id="fc83c-104">It also identifies the style of each paragraph.</span></span>  
  
 <span data-ttu-id="fc83c-105">此查詢是以上一個範例中的查詢為基礎，[尋找預設段落樣式（Visual Basic）](finding-the-default-paragraph-style.md)，這會從樣式清單中抓取預設樣式。</span><span class="sxs-lookup"><span data-stu-id="fc83c-105">This query builds on the query in the previous example, [Finding the Default Paragraph Style (Visual Basic)](finding-the-default-paragraph-style.md), which retrieves the default style from the list of styles.</span></span> <span data-ttu-id="fc83c-106">系統需要這個資訊，讓查詢可以識別沒有明確設定樣式之段落的樣式。</span><span class="sxs-lookup"><span data-stu-id="fc83c-106">This information is required so that the query can identify the style of paragraphs that do not have a style explicitly set.</span></span> <span data-ttu-id="fc83c-107">段落樣式是透過 `w:pPr` 項目設定的；如果段落不包含這個項目，則會格式化為預設樣式。</span><span class="sxs-lookup"><span data-stu-id="fc83c-107">Paragraph styles are set through the `w:pPr` element; if a paragraph does not contain this element, it is formatted with the default style.</span></span>  
  
 <span data-ttu-id="fc83c-108">本主題說明某些查詢片段的重要性，然後將查詢顯示為完整、實用範例的一部分。</span><span class="sxs-lookup"><span data-stu-id="fc83c-108">This topic explains the significance of some pieces of the query, then shows the query as part of a complete, working example.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fc83c-109">範例</span><span class="sxs-lookup"><span data-stu-id="fc83c-109">Example</span></span>  
 <span data-ttu-id="fc83c-110">在文件及其樣式中擷取所有段落之查詢的來源如下所示：</span><span class="sxs-lookup"><span data-stu-id="fc83c-110">The source of the query to retrieve all the paragraphs in a document and their styles is as follows:</span></span>  
  
```vb  
xDoc.Root.<w:body>...<w:p>  
```  
  
 <span data-ttu-id="fc83c-111">這個運算式類似于上一個範例中查詢的來源，[尋找預設段落樣式（Visual Basic）](finding-the-default-paragraph-style.md)。</span><span class="sxs-lookup"><span data-stu-id="fc83c-111">This expression is similar to the source of the query in the previous example, [Finding the Default Paragraph Style (Visual Basic)](finding-the-default-paragraph-style.md).</span></span> <span data-ttu-id="fc83c-112">主要差異在於，這個運算式使用 <xref:System.Xml.Linq.XContainer.Descendants%2A> 座標軸而非 <xref:System.Xml.Linq.XContainer.Elements%2A> 座標軸。</span><span class="sxs-lookup"><span data-stu-id="fc83c-112">The main difference is that it uses the <xref:System.Xml.Linq.XContainer.Descendants%2A> axis instead of the <xref:System.Xml.Linq.XContainer.Elements%2A> axis.</span></span> <span data-ttu-id="fc83c-113">該查詢使用 <xref:System.Xml.Linq.XContainer.Descendants%2A> 座標軸是因為在具有章節的文件中，段落將不會是本文項目的直接子系，而會在階層中的兩個層級下。</span><span class="sxs-lookup"><span data-stu-id="fc83c-113">The query uses the <xref:System.Xml.Linq.XContainer.Descendants%2A> axis because in documents that have sections, the paragraphs will not be the direct children of the body element; rather, the paragraphs will be two levels down in the hierarchy.</span></span> <span data-ttu-id="fc83c-114">藉由使用 <xref:System.Xml.Linq.XContainer.Descendants%2A> 座標軸，不管文件是否使用章節，程式碼都可以運作。</span><span class="sxs-lookup"><span data-stu-id="fc83c-114">By using the <xref:System.Xml.Linq.XContainer.Descendants%2A> axis, the code will work of whether or not the document uses sections.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fc83c-115">範例</span><span class="sxs-lookup"><span data-stu-id="fc83c-115">Example</span></span>  
 <span data-ttu-id="fc83c-116">此查詢使用 `Let` 子句來判斷包含樣式節點的項目。</span><span class="sxs-lookup"><span data-stu-id="fc83c-116">The query uses a `Let` clause to determine the element that contains the style node.</span></span> <span data-ttu-id="fc83c-117">如果沒有項目，則 `styleNode` 會設定為 `Nothing`：</span><span class="sxs-lookup"><span data-stu-id="fc83c-117">If there is no element, then `styleNode` is set to `Nothing`:</span></span>  
  
```vb  
Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault()  
```  
  
 <span data-ttu-id="fc83c-118">`Let` 子句會先使用 <xref:System.Xml.Linq.XContainer.Elements%2A> 座標軸來尋找名稱為 `pPr` 的所有項目，然後使用 <xref:System.Xml.Linq.Extensions.Elements%2A> 擴充方法來尋找名稱為 `pStyle` 的所有子項目，最後使用 <xref:System.Linq.Enumerable.FirstOrDefault%2A> 標準查詢運算子，將集合轉換為單一子句。</span><span class="sxs-lookup"><span data-stu-id="fc83c-118">The `Let` clause first uses the <xref:System.Xml.Linq.XContainer.Elements%2A> axis to find all elements named `pPr`, then uses the <xref:System.Xml.Linq.Extensions.Elements%2A> extension method to find all child elements named `pStyle`, and finally uses the <xref:System.Linq.Enumerable.FirstOrDefault%2A> standard query operator to convert the collection to a singleton.</span></span> <span data-ttu-id="fc83c-119">如果集合是空的，`styleNode` 會設定為 `Nothing`。</span><span class="sxs-lookup"><span data-stu-id="fc83c-119">If the collection is empty, `styleNode` is set to `Nothing`.</span></span> <span data-ttu-id="fc83c-120">若要尋找 `pStyle` 下階節點，這是相當實用的慣用句。</span><span class="sxs-lookup"><span data-stu-id="fc83c-120">This is a useful idiom to look for the `pStyle` descendant node.</span></span> <span data-ttu-id="fc83c-121">請注意，如果 `pPr` 子節點不存在，擲出例外狀況不會讓程式碼失敗；但是，`styleNode` 會設定為 `Nothing`，這是此 `Let` 子句所需的行為。</span><span class="sxs-lookup"><span data-stu-id="fc83c-121">Note that if the `pPr` child node does not exist, the code does nor fail by throwing an exception; instead, `styleNode` is set to `Nothing`, which is the desired behavior of this `Let` clause.</span></span>  
  
 <span data-ttu-id="fc83c-122">此查詢會使用兩個成員 (`StyleName` 和 `ParagraphNode`) 規劃一組匿名型別。</span><span class="sxs-lookup"><span data-stu-id="fc83c-122">The query projects a collection of an anonymous type with two members, `StyleName` and `ParagraphNode`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fc83c-123">範例</span><span class="sxs-lookup"><span data-stu-id="fc83c-123">Example</span></span>  
 <span data-ttu-id="fc83c-124">此範例會處理 WordprocessingML 文件，並從 WordprocessingML 文件擷取段落節點。</span><span class="sxs-lookup"><span data-stu-id="fc83c-124">This example processes a WordprocessingML document, retrieving the paragraph nodes from a WordprocessingML document.</span></span> <span data-ttu-id="fc83c-125">它也可以識別每個段落的樣式。</span><span class="sxs-lookup"><span data-stu-id="fc83c-125">It also identifies the style of each paragraph.</span></span> <span data-ttu-id="fc83c-126">此範例在這個教學課程中，會在先前的範例上建置。</span><span class="sxs-lookup"><span data-stu-id="fc83c-126">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="fc83c-127">新的查詢會在以下程式碼的註解中叫出。</span><span class="sxs-lookup"><span data-stu-id="fc83c-127">The new query is called out in comments in the code below.</span></span>  
  
 <span data-ttu-id="fc83c-128">您可以在[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中找到建立此範例之來源文件的指示。</span><span class="sxs-lookup"><span data-stu-id="fc83c-128">You can find instructions for creating the source document for this example in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="fc83c-129">這個範例會使用在 WindowsBase 組件中找到的類別。</span><span class="sxs-lookup"><span data-stu-id="fc83c-129">This example uses classes found in the WindowsBase assembly.</span></span> <span data-ttu-id="fc83c-130">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="fc83c-130">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    '  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        Dim defaultStyle As String = _  
            ( _  
                From style In styleDoc.Root.<w:style> _  
                Where style.@w:type = "paragraph" And _  
                      style.@w:default = "1" _  
                Select style _  
            ).First().@w:styleId  
  
        ' Following is the new query that finds all paragraphs in the  
        ' document and their styles.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault() _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        For Each p In paragraphs  
            Console.WriteLine("StyleName:{0}", p.StyleName)  
        Next  
  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="fc83c-131">這個範例會在套用至[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中所述的檔時產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="fc83c-131">This example produces the following output when applied to the document described in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
```console  
StyleName:Heading1  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
```  
  
## <a name="next-steps"></a><span data-ttu-id="fc83c-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc83c-132">Next Steps</span></span>  
 <span data-ttu-id="fc83c-133">在下一個主題中，抓取[段落的文字（Visual Basic）](retrieving-the-text-of-the-paragraphs.md)，您將建立一個查詢來抓取段落的文字。</span><span class="sxs-lookup"><span data-stu-id="fc83c-133">In the next topic, [Retrieving the Text of the Paragraphs (Visual Basic)](retrieving-the-text-of-the-paragraphs.md), you'll create a query to retrieve the text of paragraphs.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc83c-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fc83c-134">See also</span></span>

- [<span data-ttu-id="fc83c-135">教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="fc83c-135">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)

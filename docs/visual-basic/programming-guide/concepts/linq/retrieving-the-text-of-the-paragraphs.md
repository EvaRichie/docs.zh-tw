---
title: 擷取段落的文字
ms.date: 07/20/2015
ms.assetid: 095fa0d9-7b1b-4cbb-9c13-e2c9d8923d31
ms.openlocfilehash: 24167ade2d0326ef9382536f79f9e45eb22c89c5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413384"
---
# <a name="retrieving-the-text-of-the-paragraphs-visual-basic"></a><span data-ttu-id="127ac-102">正在抓取段落的文字（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="127ac-102">Retrieving the Text of the Paragraphs (Visual Basic)</span></span>
<span data-ttu-id="127ac-103">這個範例是以先前的範例為基礎，[並抓取段落和其樣式（Visual Basic）](retrieving-the-paragraphs-and-their-styles.md)。</span><span class="sxs-lookup"><span data-stu-id="127ac-103">This example builds on the previous example, [Retrieving the Paragraphs and Their Styles (Visual Basic)](retrieving-the-paragraphs-and-their-styles.md).</span></span> <span data-ttu-id="127ac-104">這個新的範例會將每個段落的文字當做字串擷取。</span><span class="sxs-lookup"><span data-stu-id="127ac-104">This new example retrieves the text of each paragraph as a string.</span></span>  
  
 <span data-ttu-id="127ac-105">若要擷取文字，此範例可加入逐一查看匿名型別之集合的其他查詢，並規劃加入新成員 `Text` 之匿名型別的新集合。</span><span class="sxs-lookup"><span data-stu-id="127ac-105">To retrieve the text, this example adds an additional query that iterates through the collection of anonymous types and projects a new collection of an anonymous type with the addition of a new member, `Text`.</span></span> <span data-ttu-id="127ac-106">它會使用 <xref:System.Linq.Enumerable.Aggregate%2A> 標準查詢運算子，將多個字串串連到一個字串。</span><span class="sxs-lookup"><span data-stu-id="127ac-106">It uses the <xref:System.Linq.Enumerable.Aggregate%2A> standard query operator to concatenate multiple strings into one string.</span></span>  
  
 <span data-ttu-id="127ac-107">此技術 (也就是，先規劃為匿名型別的集合，然後使用此集合規劃為匿名型別的新集合) 是實用的常見慣用句。</span><span class="sxs-lookup"><span data-stu-id="127ac-107">This technique (that is, first projecting to a collection of an anonymous type, then using this collection to project to a new collection of an anonymous type) is a common and useful idiom.</span></span> <span data-ttu-id="127ac-108">在沒有規劃為第一個匿名型別的情況下，可能已經撰寫這個查詢。</span><span class="sxs-lookup"><span data-stu-id="127ac-108">This query could have been written without projecting to the first anonymous type.</span></span> <span data-ttu-id="127ac-109">不過，因為延遲評估的緣故，這麼做不會使用太多額外的處理電源。</span><span class="sxs-lookup"><span data-stu-id="127ac-109">However, because of lazy evaluation, doing so does not use much additional processing power.</span></span> <span data-ttu-id="127ac-110">此慣用句會在堆積上建立更多短期存在的物件，但實質上，這不會降低效能。</span><span class="sxs-lookup"><span data-stu-id="127ac-110">The idiom creates more short lived objects on the heap, but this does not substantially degrade performance.</span></span>  
  
 <span data-ttu-id="127ac-111">當然，此慣用句可能會撰寫包含功能的單一查詢以擷取段落、每個段落的樣式，以及每個段落的文字。</span><span class="sxs-lookup"><span data-stu-id="127ac-111">Of course, it would be possible to write a single query that contains the functionality to retrieve the paragraphs, the style of each paragraph, and the text of each paragraph.</span></span> <span data-ttu-id="127ac-112">不過，這通常有助於將更複雜的查詢分割為多個查詢，因為所產生的程式碼更為模組化而且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="127ac-112">However, it often is useful to break up a more complicated query into multiple queries because the resulting code is more modular and easier to maintain.</span></span> <span data-ttu-id="127ac-113">此外，如果您需要重複使用某部分查詢，當查詢以此種方式撰寫時，重構比較容易。</span><span class="sxs-lookup"><span data-stu-id="127ac-113">Furthermore, if you need to reuse a portion of the query, it is easier to refactor if the queries are written in this manner.</span></span>  
  
 <span data-ttu-id="127ac-114">這些查詢若連結在一起，請使用在[教學課程：延後執行（Visual Basic）](tutorial-deferred-execution.md)主題中詳細檢查的處理模型。</span><span class="sxs-lookup"><span data-stu-id="127ac-114">These queries, which are chained together, use the processing model that is examined in detail in the topic [Tutorial: Deferred Execution (Visual Basic)](tutorial-deferred-execution.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="127ac-115">範例</span><span class="sxs-lookup"><span data-stu-id="127ac-115">Example</span></span>  
 <span data-ttu-id="127ac-116">此範例會處理 WordprocessingML 文件，以判斷項目節點、樣式名稱，以及每個段落的文字。</span><span class="sxs-lookup"><span data-stu-id="127ac-116">This example processes a WordprocessingML document, determining the element node, the style name, and the text of each paragraph.</span></span> <span data-ttu-id="127ac-117">此範例在這個教學課程中，會在先前的範例上建置。</span><span class="sxs-lookup"><span data-stu-id="127ac-117">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="127ac-118">新的查詢會在以下程式碼的註解中叫出。</span><span class="sxs-lookup"><span data-stu-id="127ac-118">The new query is called out in comments in the code below.</span></span>  
  
 <span data-ttu-id="127ac-119">如需建立此範例之來源文件的指示，請參閱[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)。</span><span class="sxs-lookup"><span data-stu-id="127ac-119">For instructions for creating the source document for this example, see [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="127ac-120">這個範例會使用 WindowsBase 組件的類別。</span><span class="sxs-lookup"><span data-stu-id="127ac-120">This example uses classes from the WindowsBase assembly.</span></span> <span data-ttu-id="127ac-121">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="127ac-121">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    ' Following function is required because Visual Basic does not support short circuit evaluation  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, _  
                                         ByVal defaultStyle As String) As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = _  
          "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = _  
              wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _  
                  docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = _  
                  documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = _  
                      PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
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
  
        ' Find all paragraphs in the document.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        ' Following is the new query that retrieves the text of  
        ' each paragraph.  
        Dim paraWithText = _  
            From para In paragraphs _  
            Select New With { _  
                .ParagraphNode = para.ParagraphNode, _  
                .StyleName = para.StyleName, _  
                .Text = para.ParagraphNode.<w:r>.<w:t> _  
                    .Aggregate(New StringBuilder(), _  
                               Function(s As StringBuilder, i As String) s.Append(CStr(i)), _  
                               Function(s As StringBuilder) s.ToString) _  
            }  
  
        For Each p In paraWithText  
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)  
        Next  
  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="127ac-122">這個範例會在套用至[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中所述的檔時產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="127ac-122">This example produces the following output when applied to the document described in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
```console  
StyleName:Heading1 >Parsing WordprocessingML with LINQ to XML<  
StyleName:Normal ><  
StyleName:Normal >The following example prints to the console.<  
StyleName:Normal ><  
StyleName:Code >Imports System<  
StyleName:Code ><  
StyleName:Code >Class Program<  
StyleName:Code >    Public Shared  Sub Main(ByVal args() As String)<  
StyleName:Code >        Console.WriteLine("Hello World")<  
StyleName:Code >   End Sub<  
StyleName:Code >End Class<  
StyleName:Normal ><  
StyleName:Normal >This example produces the following output:<  
StyleName:Normal ><  
StyleName:Code >Hello World<  
```  
  
## <a name="next-steps"></a><span data-ttu-id="127ac-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="127ac-123">Next Steps</span></span>  
 <span data-ttu-id="127ac-124">下一個範例顯示如何使用擴充方法 (而非 <xref:System.Linq.Enumerable.Aggregate%2A>)，將多個字串串連到一個字串。</span><span class="sxs-lookup"><span data-stu-id="127ac-124">The next example shows how to use an extension method, instead of <xref:System.Linq.Enumerable.Aggregate%2A>, to concatenate multiple strings into a single string.</span></span>  
  
- [<span data-ttu-id="127ac-125">使用擴充方法（Visual Basic）進行重構</span><span class="sxs-lookup"><span data-stu-id="127ac-125">Refactoring Using an Extension Method (Visual Basic)</span></span>](refactoring-using-an-extension-method.md)  
  
## <a name="see-also"></a><span data-ttu-id="127ac-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="127ac-126">See also</span></span>

- [<span data-ttu-id="127ac-127">教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="127ac-127">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
- [<span data-ttu-id="127ac-128">LINQ to XML （Visual Basic）中的延後執行和延遲評估</span><span class="sxs-lookup"><span data-stu-id="127ac-128">Deferred Execution and Lazy Evaluation in LINQ to XML (Visual Basic)</span></span>](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

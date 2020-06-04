---
title: 尋找 Word 文件中的文字
ms.date: 07/20/2015
ms.assetid: eea9819b-a78a-4552-bf13-8837fc0e7a37
ms.openlocfilehash: 546703e3dbead64fd10c04fe52cb1dd98ba53049
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398086"
---
# <a name="finding-text-in-word-documents-visual-basic"></a><span data-ttu-id="38153-102">尋找 Word 檔中的文字（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="38153-102">Finding Text in Word Documents (Visual Basic)</span></span>

<span data-ttu-id="38153-103">本主題會延伸先前的查詢以進行實用的操作：在文件中尋找出現的所有字串。</span><span class="sxs-lookup"><span data-stu-id="38153-103">This topic extends the previous queries to do something useful: find all occurrences of a string in the document.</span></span>

## <a name="example"></a><span data-ttu-id="38153-104">範例</span><span class="sxs-lookup"><span data-stu-id="38153-104">Example</span></span>

<span data-ttu-id="38153-105">此範例會處理 WordprocessingML 文件，以便在文件中尋找所有出現的特定文字片段。</span><span class="sxs-lookup"><span data-stu-id="38153-105">This example processes a WordprocessingML document, to find all the occurrences of a specific piece of text in the document.</span></span> <span data-ttu-id="38153-106">如果要這樣做，我們會使用尋找字串 "Hello" 的查詢。</span><span class="sxs-lookup"><span data-stu-id="38153-106">To do this, we use a query that finds the string "Hello".</span></span> <span data-ttu-id="38153-107">此範例在這個教學課程中，會在先前的範例上建置。</span><span class="sxs-lookup"><span data-stu-id="38153-107">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="38153-108">新的查詢會在以下程式碼的註解中叫出。</span><span class="sxs-lookup"><span data-stu-id="38153-108">The new query is called out in comments in the code below.</span></span>

<span data-ttu-id="38153-109">如需建立此範例之來源文件的指示，請參閱[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)。</span><span class="sxs-lookup"><span data-stu-id="38153-109">For instructions for creating the source document for this example, see [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>

<span data-ttu-id="38153-110">這個範例會使用在 WindowsBase 組件中找到的類別。</span><span class="sxs-lookup"><span data-stu-id="38153-110">This example uses classes found in the WindowsBase assembly.</span></span> <span data-ttu-id="38153-111">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="38153-111">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>

```vb
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">

Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(ByVal source As IEnumerable(Of String)) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each s As String In source
            sb.Append(s)
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal func As Func(Of T, String)) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each item As T In source
            sb.Append(func(item))
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal separator As String) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each s As T In source
            sb.Append(s).Append(separator)
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal func As Func(Of T, String), ByVal separator As String) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each item As T In source
            sb.Append(func(item)).Append(separator)
        Next
        Return sb.ToString()
    End Function

    Public Function ParagraphText(ByVal e As XElement) As String
        Dim w As XNamespace = e.Name.Namespace
        Return (e.<w:r>.<w:t>).StringConcatenate(Function(element) CStr(element))
    End Function

    ' Following function is required because Visual Basic does not support short circuit evaluation
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

        ' Find all paragraphs in the document.
        Dim paragraphs = _
            From para In xDoc.Root.<w:body>...<w:p> _
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault _
        Select New With { _
            .ParagraphNode = para, _
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _
        }

        ' Retrieve the text of each paragraph.
        Dim paraWithText = _
            From para In paragraphs _
            Select New With { _
                .ParagraphNode = para.ParagraphNode, _
                .StyleName = para.StyleName, _
                .Text = ParagraphText(para.ParagraphNode) _
            }

        ' Following is the new query that retrieves all paragraphs
        ' that have specific text in them.
        Dim helloParagraphs = _
            From para In paraWithText _
            Where para.Text.Contains("Hello") _
            Select New With _
            { _
                .ParagraphNode = para.ParagraphNode, _
                .StyleName = para.StyleName, _
                .Text = para.Text _
            }

        For Each p In helloParagraphs
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)
        Next
    End Sub
End Module
```

<span data-ttu-id="38153-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38153-112">This example produces the following output:</span></span>

```console
StyleName:Code >        Console.WriteLine("Hello World")<
StyleName:Code >Hello World<
```

<span data-ttu-id="38153-113">當然您可以修改搜尋條件，讓它搜尋具有特定樣式的行。</span><span class="sxs-lookup"><span data-stu-id="38153-113">You can, of course, modify the search so that it searches for lines with a specific style.</span></span> <span data-ttu-id="38153-114">下列查詢會尋找具有 Code 樣式的所有空行：</span><span class="sxs-lookup"><span data-stu-id="38153-114">The following query finds all blank lines that have the Code style:</span></span>

```vb
Imports System.IO.Packaging
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">

Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(ByVal source As IEnumerable(Of String)) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each s As String In source
            sb.Append(s)
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal func As Func(Of T, String)) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each item As T In source
            sb.Append(func(item))
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal separator As String) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each s As T In source
            sb.Append(s).Append(separator)
        Next
        Return sb.ToString()
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _
    ByVal func As Func(Of T, String), ByVal separator As String) As String
        Dim sb As StringBuilder = New StringBuilder()
        For Each item As T In source
            sb.Append(func(item)).Append(separator)
        Next
        Return sb.ToString()
    End Function

    Public Function ParagraphText(ByVal e As XElement) As String
        Dim w As XNamespace = e.Name.Namespace
        Return (e.<w:r>.<w:t>).StringConcatenate(Function(element) CStr(element))
    End Function

    ' Following function is required because Visual Basic does not support short circuit evaluation
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

        ' Find all paragraphs in the document.
        Dim paragraphs = _
            From para In xDoc.Root.<w:body>...<w:p> _
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault _
        Select New With { _
            .ParagraphNode = para, _
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _
        }

        ' Retrieve the text of each paragraph.
        Dim paraWithText = _
            From para In paragraphs _
            Select New With { _
                .ParagraphNode = para.ParagraphNode, _
                .StyleName = para.StyleName, _
                .Text = ParagraphText(para.ParagraphNode) _
            }

        ' Retrieve all paragraphs that have no text and are styled Code.
        Dim blankCodeParagraphs = _
            From para In paraWithText _
            Where String.IsNullOrEmpty(para.Text) And para.StyleName.Equals("Code") _
            Select New With _
            { _
                .ParagraphNode = para.ParagraphNode, _
                .StyleName = para.StyleName, _
                .Text = para.Text _
            }

        For Each p In blankCodeParagraphs
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)
        Next
    End Sub
End Module
```

<span data-ttu-id="38153-115">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38153-115">This example produces the following output:</span></span>

```console
StyleName:Code ><
```

<span data-ttu-id="38153-116">當然，這個範例可以利用數種方式增強。</span><span class="sxs-lookup"><span data-stu-id="38153-116">Of course, this example could be enhanced in a number of ways.</span></span> <span data-ttu-id="38153-117">例如，我們可以使用規則運算式 (Regular Expression) 來搜尋文字；我們可以在特定的字典中逐一查看所有 Word 檔案等等。</span><span class="sxs-lookup"><span data-stu-id="38153-117">For example, we could use regular expressions to search for text, we could iterate through all the Word files in a particular directory, and so on.</span></span>

<span data-ttu-id="38153-118">請注意，這個範例的執行方式與撰寫為單一查詢的執行方式約略相同。</span><span class="sxs-lookup"><span data-stu-id="38153-118">Note that this example performs approximately as well as if it were written as a single query.</span></span> <span data-ttu-id="38153-119">由於每個查詢都會使用延遲、延後的方式實作，因此每個查詢在反覆運算前不會產生其結果。</span><span class="sxs-lookup"><span data-stu-id="38153-119">Because each query is implemented in a lazy, deferred fashion, each query does not yield its results until the query is iterated.</span></span> <span data-ttu-id="38153-120">如需執行和延遲評估的詳細資訊，請參閱[LINQ to XML （Visual Basic）中的延後執行和延遲評估](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="38153-120">For more information about execution and lazy evaluation, see [Deferred Execution and Lazy Evaluation in LINQ to XML (Visual Basic)](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38153-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38153-121">Next Steps</span></span>

<span data-ttu-id="38153-122">下一節提供有關 WordprocessingML 文件的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="38153-122">The next section provides more information about WordprocessingML documents:</span></span>

- [<span data-ttu-id="38153-123">Office Open XML WordprocessingML 檔的詳細資料（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="38153-123">Details of Office Open XML WordprocessingML Documents (Visual Basic)</span></span>](details-of-office-open-xml-wordprocessingml-documents.md)

## <a name="see-also"></a><span data-ttu-id="38153-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="38153-124">See also</span></span>

- [<span data-ttu-id="38153-125">教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="38153-125">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
- [<span data-ttu-id="38153-126">使用純虛擬函式進行重構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="38153-126">Refactoring Using a Pure Function (Visual Basic)</span></span>](refactoring-using-a-pure-function.md)
- [<span data-ttu-id="38153-127">LINQ to XML （Visual Basic）中的延後執行和延遲評估</span><span class="sxs-lookup"><span data-stu-id="38153-127">Deferred Execution and Lazy Evaluation in LINQ to XML (Visual Basic)</span></span>](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

---
title: 使用擴充方法進行重構
ms.date: 07/20/2015
ms.assetid: d87ae99a-cfa9-4a31-a5e4-9d6437be6810
ms.openlocfilehash: 5bb3ed44c0c3f7616468f820428fe1a384ab6d45
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413426"
---
# <a name="refactoring-using-an-extension-method-visual-basic"></a><span data-ttu-id="8927e-102">使用擴充方法（Visual Basic）進行重構</span><span class="sxs-lookup"><span data-stu-id="8927e-102">Refactoring Using an Extension Method (Visual Basic)</span></span>
<span data-ttu-id="8927e-103">這個範例是以先前的範例為基礎，藉由使用實作為擴充方法的純虛擬函式來重構字串的串連，以抓取[段落的文字（Visual Basic）](retrieving-the-text-of-the-paragraphs.md)。</span><span class="sxs-lookup"><span data-stu-id="8927e-103">This example builds on the previous example, [Retrieving the Text of the Paragraphs (Visual Basic)](retrieving-the-text-of-the-paragraphs.md), by refactoring the concatenation of strings using a pure function that is implemented as an extension method.</span></span>  
  
 <span data-ttu-id="8927e-104">前一個範例使用 <xref:System.Linq.Enumerable.Aggregate%2A> 標準查詢運算子，將多個字串串連到一個字串。</span><span class="sxs-lookup"><span data-stu-id="8927e-104">The previous example used the <xref:System.Linq.Enumerable.Aggregate%2A> standard query operator to concatenate multiple strings into one string.</span></span> <span data-ttu-id="8927e-105">不過，撰寫擴充方法來執行這個動作更為方便，因為所產生的查詢更小而且更簡單。</span><span class="sxs-lookup"><span data-stu-id="8927e-105">However, it is more convenient to write an extension method to do this, because the resulting query smaller and more simple.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8927e-106">範例</span><span class="sxs-lookup"><span data-stu-id="8927e-106">Example</span></span>  
 <span data-ttu-id="8927e-107">這個範例會處理 WordprocessingML 文件，以擷取段落、每個段落的樣式，以及每個段落的文字。</span><span class="sxs-lookup"><span data-stu-id="8927e-107">This example processes a WordprocessingML document, retrieving the paragraphs, the style of each paragraph, and the text of each paragraph.</span></span> <span data-ttu-id="8927e-108">此範例在這個教學課程中，會在先前的範例上建置。</span><span class="sxs-lookup"><span data-stu-id="8927e-108">This example builds on the previous examples in this tutorial.</span></span>  
  
 <span data-ttu-id="8927e-109">此範例包含 `StringConcatenate` 方法的多個多載。</span><span class="sxs-lookup"><span data-stu-id="8927e-109">The example contains multiple overloads of the `StringConcatenate` method.</span></span>  
  
 <span data-ttu-id="8927e-110">您可以在[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中找到建立此範例之來源文件的指示。</span><span class="sxs-lookup"><span data-stu-id="8927e-110">You can find instructions for creating the source document for this example in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="8927e-111">這個範例會使用 WindowsBase 組件的類別。</span><span class="sxs-lookup"><span data-stu-id="8927e-111">This example uses classes from the WindowsBase assembly.</span></span> <span data-ttu-id="8927e-112">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="8927e-112">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```vb  
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
```  
  
## <a name="example"></a><span data-ttu-id="8927e-113">範例</span><span class="sxs-lookup"><span data-stu-id="8927e-113">Example</span></span>  
 <span data-ttu-id="8927e-114">`StringConcatenate` 方法的多載有四個。</span><span class="sxs-lookup"><span data-stu-id="8927e-114">There are four overloads of the `StringConcatenate` method.</span></span> <span data-ttu-id="8927e-115">一個多載只採用一個字串集合並傳回單一字串。</span><span class="sxs-lookup"><span data-stu-id="8927e-115">One overload simply takes a collection of strings and returns a single string.</span></span> <span data-ttu-id="8927e-116">另一個多載可以採用任何型別的集合，然後將該專案從集合的單一子句委派到字串。</span><span class="sxs-lookup"><span data-stu-id="8927e-116">Another overload can take a collection of any type, and a delegate that projects from a singleton of the collection to a string.</span></span> <span data-ttu-id="8927e-117">還有其他兩個多載可讓您指定分隔符號字串。</span><span class="sxs-lookup"><span data-stu-id="8927e-117">There are two more overloads that allow you to specify a separator string.</span></span>  
  
 <span data-ttu-id="8927e-118">下列程式碼會使用全部四個多載。</span><span class="sxs-lookup"><span data-stu-id="8927e-118">The following code uses all four overloads.</span></span>  
  
```vb  
Dim numbers As String() = {"one", "two", "three"}  
  
Console.WriteLine("{0}", numbers.StringConcatenate())  
Console.WriteLine("{0}", numbers.StringConcatenate(":"))  
  
Dim intNumbers As Integer() = {1, 2, 3}  
Console.WriteLine("{0}", intNumbers.StringConcatenate(Function(i) i.ToString()))  
Console.WriteLine("{0}", intNumbers.StringConcatenate(Function(i) i.ToString(), ":"))  
```  
  
 <span data-ttu-id="8927e-119">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="8927e-119">This example produces the following output:</span></span>  
  
```console  
onetwothree  
one:two:three:  
123  
1:2:3:  
```  
  
## <a name="example"></a><span data-ttu-id="8927e-120">範例</span><span class="sxs-lookup"><span data-stu-id="8927e-120">Example</span></span>  
 <span data-ttu-id="8927e-121">現在可以修改範例以利用新的擴充方法：</span><span class="sxs-lookup"><span data-stu-id="8927e-121">Now, the example can be modified to take advantage of the new extension method:</span></span>  
  
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
  
        ' Retrieve the text of each paragraph.  
        Dim paraWithText = _  
            From para In paragraphs _  
            Select New With { _  
                .ParagraphNode = para.ParagraphNode, _  
                .StyleName = para.StyleName, _  
                .Text = para.ParagraphNode.<w:r>.<w:t>.StringConcatenate(Function(e) CStr(e)) _  
            }  
  
        For Each p In paraWithText  
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)  
        Next  
  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="8927e-122">這個範例會在套用至[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中所述的檔時產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="8927e-122">This example produces the following output when applied to the document described in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>
  
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
  
 <span data-ttu-id="8927e-123">請注意，這個重構是重構到純虛擬函式的變數。</span><span class="sxs-lookup"><span data-stu-id="8927e-123">Note that this refactoring is a variant of refactoring into a pure function.</span></span> <span data-ttu-id="8927e-124">下一個主題將更詳細介紹重構到純虛擬函式的概念。</span><span class="sxs-lookup"><span data-stu-id="8927e-124">The next topic will introduce the idea of factoring into pure functions in more detail.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8927e-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8927e-125">Next Steps</span></span>  
 <span data-ttu-id="8927e-126">下一個範例顯示如何使用純虛擬函式，以另一種方式重構此程式碼：</span><span class="sxs-lookup"><span data-stu-id="8927e-126">The next example shows how to refactor this code in another way, by using pure functions:</span></span>  
  
- [<span data-ttu-id="8927e-127">使用純虛擬函式進行重構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8927e-127">Refactoring Using a Pure Function (Visual Basic)</span></span>](refactoring-using-a-pure-function.md)  
  
## <a name="see-also"></a><span data-ttu-id="8927e-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8927e-128">See also</span></span>

- [<span data-ttu-id="8927e-129">教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="8927e-129">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
- [<span data-ttu-id="8927e-130">重構為純虛擬函式（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="8927e-130">Refactoring Into Pure Functions (Visual Basic)</span></span>](refactoring-into-pure-functions.md)

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
# <a name="retrieving-the-text-of-the-paragraphs-visual-basic"></a>正在抓取段落的文字（Visual Basic）
這個範例是以先前的範例為基礎，[並抓取段落和其樣式（Visual Basic）](retrieving-the-paragraphs-and-their-styles.md)。 這個新的範例會將每個段落的文字當做字串擷取。  
  
 若要擷取文字，此範例可加入逐一查看匿名型別之集合的其他查詢，並規劃加入新成員 `Text` 之匿名型別的新集合。 它會使用 <xref:System.Linq.Enumerable.Aggregate%2A> 標準查詢運算子，將多個字串串連到一個字串。  
  
 此技術 (也就是，先規劃為匿名型別的集合，然後使用此集合規劃為匿名型別的新集合) 是實用的常見慣用句。 在沒有規劃為第一個匿名型別的情況下，可能已經撰寫這個查詢。 不過，因為延遲評估的緣故，這麼做不會使用太多額外的處理電源。 此慣用句會在堆積上建立更多短期存在的物件，但實質上，這不會降低效能。  
  
 當然，此慣用句可能會撰寫包含功能的單一查詢以擷取段落、每個段落的樣式，以及每個段落的文字。 不過，這通常有助於將更複雜的查詢分割為多個查詢，因為所產生的程式碼更為模組化而且更容易維護。 此外，如果您需要重複使用某部分查詢，當查詢以此種方式撰寫時，重構比較容易。  
  
 這些查詢若連結在一起，請使用在[教學課程：延後執行（Visual Basic）](tutorial-deferred-execution.md)主題中詳細檢查的處理模型。  
  
## <a name="example"></a>範例  
 此範例會處理 WordprocessingML 文件，以判斷項目節點、樣式名稱，以及每個段落的文字。 此範例在這個教學課程中，會在先前的範例上建置。 新的查詢會在以下程式碼的註解中叫出。  
  
 如需建立此範例之來源文件的指示，請參閱[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)。  
  
 這個範例會使用 WindowsBase 組件的類別。 它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。  
  
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
  
 這個範例會在套用至[建立來源 Office OPEN XML 檔（Visual Basic）](creating-the-source-office-open-xml-document.md)中所述的檔時產生下列輸出。  
  
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
  
## <a name="next-steps"></a>後續步驟  
 下一個範例顯示如何使用擴充方法 (而非 <xref:System.Linq.Enumerable.Aggregate%2A>)，將多個字串串連到一個字串。  
  
- [使用擴充方法（Visual Basic）進行重構](refactoring-using-an-extension-method.md)  
  
## <a name="see-also"></a>另請參閱

- [教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
- [LINQ to XML （Visual Basic）中的延後執行和延遲評估](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

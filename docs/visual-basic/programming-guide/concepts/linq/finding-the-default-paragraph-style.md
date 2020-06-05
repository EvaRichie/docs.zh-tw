---
title: 尋找預設的段落樣式
ms.date: 07/20/2015
ms.assetid: 9d094a4a-ec8c-41b0-b7ab-a3deb2a01d45
ms.openlocfilehash: b70ae72c293d00c4f7b7a2601bfd20b85702b6d5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398073"
---
# <a name="finding-the-default-paragraph-style-visual-basic"></a>尋找預設段落樣式（Visual Basic）
＜管理 WordprocessingML 文件中的資訊＞教學課程中的第一個工作是，尋找文件中的預設段落樣式。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會開啟 Office Open XML WordprocessingML 文件、尋找文件和封裝的樣式部分，然後執行尋找預設樣式名稱的查詢。 如需 Office Open XML 檔套件及其組成之元件的相關資訊，請參閱[Office OPEN Xml WordprocessingML 檔的詳細資料（Visual Basic）](details-of-office-open-xml-wordprocessingml-documents.md)。  
  
 查詢會尋找名稱為 `w:style` 的節點，其中擁有名稱為 `w:type` 且值為 "paragraph" 的屬性，同時也擁有名稱為 `w:default` 且值為 "1" 的屬性。 由於這些屬性只有一個 XML 節點，查詢會使用 <xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType> 運算子，將集合轉換為單一子句。 接著，它會取得名稱為 `w:styleId` 之屬性的值。  
  
 這個範例會使用 WindowsBase 組件的類別。 它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。  
  
### <a name="code"></a>程式碼  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
  
    Sub Main()  
  
        Const fileName As String = "SampleDoc.docx"  
  
        Const documentRelationshipType As String = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Const stylesRelationshipType As String = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = _  
              wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If docPackageRelationship IsNot Nothing Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _  
                  docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                ' Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                ' Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = _  
                  documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If styleRelation IsNot Nothing Then  
                    Dim styleUri As Uri = _  
                      PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    ' Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        ' The following query finds all the paragraphs that have the default style.  
        Dim defParas As IEnumerable(Of XElement) = _  
            From style In styleDoc.Root.<w:style> _  
            Where style.@w:type.Equals("paragraph") And _  
                   style.@w:default.Equals("1") _  
            Select style  
        ' Then find the style of the first.  
        Dim defaultStyle As String = defParas.First().@w:styleId  
  
        Console.WriteLine("The default style is: " & defaultStyle)  
    End Sub  
End Module  
```  
  
### <a name="comments"></a>註解  
 這個範例會產生下列輸出：  
  
```console  
The default style is: Normal  
```  
  
## <a name="next-steps"></a>後續步驟  
 在下一個範例中，您將建立可在文件中尋找所有段落及其樣式的類似查詢：  
  
- [抓取段落和其樣式（Visual Basic）](retrieving-the-paragraphs-and-their-styles.md)  
  
## <a name="see-also"></a>另請參閱

- [教學課程：操作 WordprocessingML 檔中的內容（Visual Basic）](tutorial-manipulating-content-in-a-wordprocessingml-document.md)

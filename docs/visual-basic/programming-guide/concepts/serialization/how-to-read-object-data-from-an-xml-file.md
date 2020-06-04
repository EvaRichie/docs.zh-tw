---
title: 如何：從 XML 檔案讀取物件資料
ms.date: 07/20/2015
ms.assetid: 1e1423bf-74a4-4dde-a3bb-ae1bfc0a68ed
ms.openlocfilehash: 7097ec146987aea7855da40dd30f9cd3c17d8ce4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413163"
---
# <a name="how-to-read-object-data-from-an-xml-file-visual-basic"></a>如何：從 XML 檔案讀取物件資料 (Visual Basic)
此範例會讀取先前使用 <xref:System.Xml.Serialization.XmlSerializer> 類別來寫入 XML 檔案的物件資料。  
  
## <a name="example"></a>範例  
  
```vb  
Public Class Book  
    Public Title As String  
End Class  
  
Public Sub ReadXML()  
    Dim reader As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
    Dim file As New System.IO.StreamReader(  
        "c:\temp\SerializationOverview.xml")  
    Dim overview As Book  
    overview = CType(reader.Deserialize(file), Book)  
    Console.WriteLine(overview.Title)  
End Sub  
```  
  
## <a name="compile-the-code"></a>編譯程式碼  
 以內含序列化資料之檔案的名稱取代檔案名稱 "c:\temp\SerializationOverview.xml"。 如需序列化資料的詳細資訊，請參閱[如何：將物件資料寫入 XML 檔案（Visual Basic）](how-to-write-object-data-to-an-xml-file.md)。  
  
 此類別必須有不具參數的公用建構函式。  
  
 只會還原序列化公用屬性和欄位。  
  
## <a name="robust-programming"></a>穩固程式設計  
 以下條件可能會造成例外狀況：  
  
- 正在序列化的類別沒有公用的無參數建構函式。  
  
- 檔案中的資料不是來自要還原序列化之類別的資料。  
  
- 檔案不存在 (<xref:System.IO.IOException>)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 永遠會驗證輸入，而且絕不會還原序列化來自未受信任來源的資料。 重新建立的物件會以還原序列化該物件之程式碼的權限，在本機電腦上執行。 在應用程式中使用這些資料之前，請先驗證所有輸入值。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO.StreamWriter>
- [如何：將物件資料寫入 XML 檔案 (Visual Basic)](how-to-write-object-data-to-an-xml-file.md)
- [序列化 (Visual Basic)](index.md)
- [Visual Basic 程式設計指南](../../index.md)

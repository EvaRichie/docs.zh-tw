---
title: 如何：將物件資料寫入 XML 檔案
ms.date: 07/20/2015
ms.assetid: f7966480-5ed2-43ac-9894-33427436de2a
ms.openlocfilehash: 9608a48cb8b3fac1c71affa7a0a17e9789f94b18
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413150"
---
# <a name="how-to-write-object-data-to-an-xml-file-visual-basic"></a>如何：將物件資料寫入 XML 檔案 (Visual Basic)
此範例會使用 <xref:System.Xml.Serialization.XmlSerializer> 類別，將來自某個類別的物件寫入 XML 檔案。  
  
## <a name="example"></a>範例  
  
```vb  
Public Module XMLWrite  
  
    Sub Main()  
        WriteXML()  
    End Sub  
  
    Public Class Book  
        Public Title As String  
    End Class  
  
    Public Sub WriteXML()  
        Dim overview As New Book  
        overview.Title = "Serialization Overview"  
        Dim writer As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
        Dim file As New System.IO.StreamWriter(  
            "c:\temp\SerializationOverview.xml")  
        writer.Serialize(file, overview)  
        file.Close()  
    End Sub  
End Module  
```  
  
## <a name="compile-the-code"></a>編譯程式碼  
 此類別必須有不具參數的公用建構函式。  
  
## <a name="robust-programming"></a>穩固程式設計  
 以下條件可能會造成例外狀況：  
  
- 正在序列化的類別沒有公用的無參數建構函式。  
  
- 該檔案存在且為唯讀 (<xref:System.IO.IOException>)。  
  
- 路徑太長 (<xref:System.IO.PathTooLongException>)。  
  
- 磁碟已滿 (<xref:System.IO.IOException>)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果檔案不存在，此範例就會建立新的檔案。 如果應用程式需要建立檔案，該應用程式就需要資料夾的 `Create` 權限。 如果檔案已經存在，則應用程式只需要 `Write` 權限，這是較小的權限。 若有可能，更為安全的做法是在部署期間建立檔案，並且只授與單一檔案的 `Read` 權限，而不授與資料夾的 `Create` 權限。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO.StreamWriter>
- [如何：從 XML 檔案讀取物件資料 (Visual Basic)](how-to-read-object-data-from-an-xml-file.md)
- [序列化 (Visual Basic)](index.md)

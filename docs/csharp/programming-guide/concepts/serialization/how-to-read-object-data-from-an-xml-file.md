---
title: '如何從 XML 檔案讀取物件資料 (c # ) '
description: '這個 c # 範例會讀取先前使用 XmlSerializer 類別寫入至 XML 檔案的物件資料。'
ms.date: 07/20/2015
ms.assetid: 6ad60d96-a4d9-48e6-a8b0-d7f6f803cafa
ms.openlocfilehash: 8d607424201cfad08df1c5ffbfb66a114b31886d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178758"
---
# <a name="how-to-read-object-data-from-an-xml-file-c"></a>如何從 XML 檔案讀取物件資料 (c # ) 

此範例會讀取先前使用 <xref:System.Xml.Serialization.XmlSerializer> 類別來寫入 XML 檔案的物件資料。  
  
## <a name="example"></a>範例  
  
```csharp  
public class Book  
{  
    public String title;  
}
  
public void ReadXML()  
{  
    // First write something so that there is something to read ...  
    var b = new Book { title = "Serialization Overview" };  
    var writer = new System.Xml.Serialization.XmlSerializer(typeof(Book));  
    var wfile = new System.IO.StreamWriter(@"c:\temp\SerializationOverview.xml");  
    writer.Serialize(wfile, b);  
    wfile.Close();  
  
    // Now we can read the serialized book ...  
    System.Xml.Serialization.XmlSerializer reader =
        new System.Xml.Serialization.XmlSerializer(typeof(Book));  
    System.IO.StreamReader file = new System.IO.StreamReader(  
        @"c:\temp\SerializationOverview.xml");  
    Book overview =  (Book)reader.Deserialize(file);  
    file.Close();  
  
    Console.WriteLine(overview.title);  
  
}  
```  
  
## <a name="compiling-the-code"></a>編譯程式碼  

以內含序列化資料之檔案的名稱取代檔案名稱 "c:\temp\SerializationOverview.xml"。 如需序列化資料的詳細資訊，請參閱 [如何將物件資料寫入 XML 檔案 (c # ) ](./how-to-write-object-data-to-an-xml-file.md)。
  
 此類別必須有不具參數的公用建構函式。  
  
 只會還原序列化公用屬性和欄位。  
  
## <a name="robust-programming"></a>穩固程式設計  

 以下條件可能會造成例外狀況：  
  
- 正在序列化的類別沒有公用的無參數建構函式。  
  
- 檔案中的資料不是來自要還原序列化之類別的資料。  
  
- 檔案不存在 (<xref:System.IO.IOException>)。  
  
## <a name="net-security"></a>.NET 安全性  

 永遠會驗證輸入，而且絕不會還原序列化來自未受信任來源的資料。 重新建立的物件會以還原序列化該物件之程式碼的權限，在本機電腦上執行。 在應用程式中使用這些資料之前，請先驗證所有輸入值。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO.StreamWriter>
- [如何將物件資料寫入 XML 檔案 (c # ) ](./how-to-write-object-data-to-an-xml-file.md)
- [序列化 (C#)](./index.md)
- [C # 程式設計指南](../../index.md)

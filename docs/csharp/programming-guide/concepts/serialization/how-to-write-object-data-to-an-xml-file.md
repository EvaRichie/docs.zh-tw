---
title: '如何將物件資料寫入 XML 檔案 (c # ) '
description: '這個 c # 範例會使用 XmlSerializer 類別，將物件從類別寫入至 XML 檔案。 瞭解如何編譯器代碼。'
ms.date: 07/20/2015
ms.assetid: 7681eb98-703d-4005-a369-26a7bca0f894
ms.openlocfilehash: 776ade1752adf15d6acce07d38120de8481a233d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178706"
---
# <a name="how-to-write-object-data-to-an-xml-file-c"></a>如何將物件資料寫入 XML 檔案 (c # ) 

此範例會使用 <xref:System.Xml.Serialization.XmlSerializer> 類別，將來自某個類別的物件寫入 XML 檔案。  
  
## <a name="example"></a>範例  
  
```csharp  
public class XMLWrite  
{  
  
   static void Main(string[] args)  
    {  
        WriteXML();  
    }  
  
    public class Book  
    {  
        public String title;
    }  
  
    public static void WriteXML()  
    {  
        Book overview = new Book();  
        overview.title = "Serialization Overview";  
        System.Xml.Serialization.XmlSerializer writer =
            new System.Xml.Serialization.XmlSerializer(typeof(Book));  
  
        var path = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments) + "//SerializationOverview.xml";  
        System.IO.FileStream file = System.IO.File.Create(path);  
  
        writer.Serialize(file, overview);  
        file.Close();  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>編譯程式碼  

 正在序列化的類別必須有不具參數的公用建構函式。  
  
## <a name="robust-programming"></a>穩固程式設計  

 以下條件可能會造成例外狀況：  
  
- 正在序列化的類別沒有公用的無參數建構函式。  
  
- 該檔案存在且為唯讀 (<xref:System.IO.IOException>)。  
  
- 路徑太長 (<xref:System.IO.PathTooLongException>)。  
  
- 磁碟已滿 (<xref:System.IO.IOException>)。  
  
## <a name="net-security"></a>.NET 安全性  

 如果檔案不存在，此範例就會建立新的檔案。 如果應用程式需要建立檔案，該應用程式就需要資料夾的 `Create` 權限。 如果檔案已經存在，則應用程式只需要 `Write` 權限，這是較小的權限。 若有可能，更為安全的做法是在部署期間建立檔案，並且只授與單一檔案的 `Read` 權限，而不授與資料夾的 `Create` 權限。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO.StreamWriter>
- [如何從 XML 檔案讀取物件資料 (c # ) ](./how-to-read-object-data-from-an-xml-file.md)
- [序列化 (C#)](./index.md)

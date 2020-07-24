---
title: '如何讀取和寫入編碼的檔（c #）'
description: '瞭解如何在 c # 中建立編碼的 XML 檔，方法是將 XDeclaration 加入至 XML 樹狀結構，並將編碼方式設定為所需的字碼頁名稱。'
ms.date: 07/20/2015
ms.assetid: 84f64e71-39a6-42c6-ad68-f052bb158a03
ms.openlocfilehash: ed02b7467f4de71455da516a6c894070337684e7
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104323"
---
# <a name="how-to-read-and-write-an-encoded-document-c"></a>如何讀取和寫入編碼的檔（c #）
若要建立編碼的 XML 文件，您可以將編碼設定為所需的字碼頁名稱，以便將 <xref:System.Xml.Linq.XDeclaration> 加入到 XML 樹狀結構中。  
  
 由 <xref:System.Text.Encoding.WebName%2A> 傳回的任何值都是有效的值。  
  
 如果您要讀取加密的文件，<xref:System.Xml.Linq.XDeclaration.Encoding%2A> 屬性將會設定為字碼頁名稱。  
  
 如果您將 <xref:System.Xml.Linq.XDeclaration.Encoding%2A> 設定為有效的字碼頁名稱，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會使用指定的編碼序列化。  
  
## <a name="example"></a>範例  
 下列範例會建立兩個文件，其中一個編碼為 utf-8，而另一個編碼為 utf-16。 然後，會載入文件並將編碼方式列印至主控台。  
  
```csharp  
Console.WriteLine("Creating a document with utf-8 encoding");  
XDocument encodedDoc8 = new XDocument(  
    new XDeclaration("1.0", "utf-8", "yes"),  
    new XElement("Root", "Content")  
);  
encodedDoc8.Save("EncodedUtf8.xml");  
Console.WriteLine("Encoding is:{0}", encodedDoc8.Declaration.Encoding);  
Console.WriteLine();  
  
Console.WriteLine("Creating a document with utf-16 encoding");  
XDocument encodedDoc16 = new XDocument(  
    new XDeclaration("1.0", "utf-16", "yes"),  
    new XElement("Root", "Content")  
);  
encodedDoc16.Save("EncodedUtf16.xml");  
Console.WriteLine("Encoding is:{0}", encodedDoc16.Declaration.Encoding);  
Console.WriteLine();  
  
XDocument newDoc8 = XDocument.Load("EncodedUtf8.xml");  
Console.WriteLine("Encoded document:");  
Console.WriteLine(File.ReadAllText("EncodedUtf8.xml"));  
Console.WriteLine();  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc8.Declaration.Encoding);  
Console.WriteLine();  
  
XDocument newDoc16 = XDocument.Load("EncodedUtf16.xml");  
Console.WriteLine("Encoded document:");  
Console.WriteLine(File.ReadAllText("EncodedUtf16.xml"));  
Console.WriteLine();  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc16.Declaration.Encoding);  
```  
  
 這個範例會產生下列輸出：  
  
```output  
Creating a document with utf-8 encoding  
Encoding is:utf-8  
  
Creating a document with utf-16 encoding  
Encoding is:utf-16  
  
Encoded document:  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-8  
  
Encoded document:  
<?xml version="1.0" encoding="utf-16" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-16  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Linq.XDeclaration.Encoding%2A?displayProperty=nameWithType>

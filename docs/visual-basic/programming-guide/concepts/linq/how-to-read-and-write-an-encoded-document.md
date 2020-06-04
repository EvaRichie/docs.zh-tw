---
title: 作法：讀取和寫入編碼的文件
ms.date: 07/20/2015
ms.assetid: 159d868f-5ac8-40f2-95ca-07dd925f35c6
ms.openlocfilehash: f66737429950e04f447dfbd58cf47b6434a22976
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397904"
---
# <a name="how-to-read-and-write-an-encoded-document-visual-basic"></a><span data-ttu-id="bdd5e-102">如何：讀取和寫入編碼的檔（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="bdd5e-102">How to: Read and Write an Encoded Document (Visual Basic)</span></span>

<span data-ttu-id="bdd5e-103">若要建立編碼的 XML 文件，您可以將編碼設定為所需的字碼頁名稱，以便將 <xref:System.Xml.Linq.XDeclaration> 加入到 XML 樹狀結構中。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-103">To create an encoded XML document, you add an <xref:System.Xml.Linq.XDeclaration> to the XML tree, setting the encoding to the desired code page name.</span></span>

<span data-ttu-id="bdd5e-104">由 <xref:System.Text.Encoding.WebName%2A> 傳回的任何值都是有效的值。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-104">Any value returned by <xref:System.Text.Encoding.WebName%2A> is a valid value.</span></span>

<span data-ttu-id="bdd5e-105">如果您要讀取加密的文件，<xref:System.Xml.Linq.XDeclaration.Encoding%2A> 屬性將會設定為字碼頁名稱。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-105">If you read an encoded document, the <xref:System.Xml.Linq.XDeclaration.Encoding%2A> property will be set to the code page name.</span></span>

<span data-ttu-id="bdd5e-106">如果您將 <xref:System.Xml.Linq.XDeclaration.Encoding%2A> 設定為有效的字碼頁名稱，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會使用指定的編碼序列化。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-106">If you set <xref:System.Xml.Linq.XDeclaration.Encoding%2A> to a valid code page name, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] will serialize with the specified encoding.</span></span>

## <a name="example"></a><span data-ttu-id="bdd5e-107">範例</span><span class="sxs-lookup"><span data-stu-id="bdd5e-107">Example</span></span>

<span data-ttu-id="bdd5e-108">下列範例會建立兩個文件，其中一個編碼為 utf-8，而另一個編碼為 utf-16。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-108">The following example creates two documents, one with utf-8 encoding, and one with utf-16 encoding.</span></span> <span data-ttu-id="bdd5e-109">然後，會載入文件並將編碼方式列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="bdd5e-109">It then loads the documents and prints the encoding to the console.</span></span>

```vb
Console.WriteLine("Creating a document with utf-8 encoding")
Dim encodedDoc8 As XDocument = _
        <?xml version='1.0' encoding='utf-8' standalone='yes'?>
        <Root>Content</Root>

encodedDoc8.Save("EncodedUtf8.xml")
Console.WriteLine("Encoding is:{0}", encodedDoc8.Declaration.Encoding)
Console.WriteLine()

Console.WriteLine("Creating a document with utf-16 encoding")
Dim encodedDoc16 As XDocument = _
        <?xml version='1.0' encoding='utf-16' standalone='yes'?>
        <Root>Content</Root>

encodedDoc16.Save("EncodedUtf16.xml")
Console.WriteLine("Encoding is:{0}", encodedDoc16.Declaration.Encoding)
Console.WriteLine()

Dim newDoc8 As XDocument = XDocument.Load("EncodedUtf8.xml")
Console.WriteLine("Encoded document:")
Console.WriteLine(File.ReadAllText("EncodedUtf8.xml"))
Console.WriteLine()
Console.WriteLine("Encoding of loaded document is:{0}", newDoc8.Declaration.Encoding)
Console.WriteLine()

Dim newDoc16 As XDocument = XDocument.Load("EncodedUtf16.xml")
Console.WriteLine("Encoded document:")
Console.WriteLine(File.ReadAllText("EncodedUtf16.xml"))
Console.WriteLine()
Console.WriteLine("Encoding of loaded document is:{0}", newDoc16.Declaration.Encoding)
```

<span data-ttu-id="bdd5e-110">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="bdd5e-110">This example produces the following output:</span></span>

```console
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

## <a name="see-also"></a><span data-ttu-id="bdd5e-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bdd5e-111">See also</span></span>

- <xref:System.Xml.Linq.XDeclaration.Encoding%2A?displayProperty=nameWithType>
- [<span data-ttu-id="bdd5e-112">Advanced LINQ to XML 程式設計（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="bdd5e-112">Advanced LINQ to XML Programming (Visual Basic)</span></span>](advanced-linq-to-xml-programming.md)

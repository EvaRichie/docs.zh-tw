---
title: 如何：使用 X.509 憑證解密 XML 項目
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- System.Security.Cryptography.X509Certificate2 class
- decryption
- X.509 certificates
- certificates, X.509 certificates
ms.assetid: bd015722-d88d-408d-8ca8-e4e475c441ed
ms.openlocfilehash: 32a6d95b96bb20571c14c16cc70b944fa3e4032b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84277384"
---
# <a name="how-to-decrypt-xml-elements-with-x509-certificates"></a><span data-ttu-id="634bb-102">如何：使用 X.509 憑證解密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="634bb-102">How to: Decrypt XML Elements with X.509 Certificates</span></span>
<span data-ttu-id="634bb-103">您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別來加密和解密 XML 文件內的項目。</span><span class="sxs-lookup"><span data-stu-id="634bb-103">You can use the classes in the <xref:System.Security.Cryptography.Xml> namespace to encrypt and decrypt an element within an XML document.</span></span>  <span data-ttu-id="634bb-104">XML 加密是交換或儲存加密 XML 資料的標準方法，不必擔心資料被輕易讀取。</span><span class="sxs-lookup"><span data-stu-id="634bb-104">XML Encryption is a standard way to exchange or store encrypted XML data, without worrying about the data being easily read.</span></span>  <span data-ttu-id="634bb-105">如需 XML 加密標準的詳細資訊，請參閱 XML 加密的全球資訊網協會（W3C）規格（位於） <https://www.w3.org/TR/xmldsig-core/> 。</span><span class="sxs-lookup"><span data-stu-id="634bb-105">For more information about the XML Encryption standard, see the World Wide Web Consortium (W3C) specification for XML Encryption located at <https://www.w3.org/TR/xmldsig-core/>.</span></span>  
  
 <span data-ttu-id="634bb-106">這個範例會使用：[如何：使用 X.509 憑證加密 xml](how-to-encrypt-xml-elements-with-x-509-certificates.md)專案中所述的方法，解密已加密的 xml 元素。</span><span class="sxs-lookup"><span data-stu-id="634bb-106">This example decrypts an XML element that was encrypted using the methods described in: [How to: Encrypt XML Elements with X.509 Certificates](how-to-encrypt-xml-elements-with-x-509-certificates.md).</span></span>  <span data-ttu-id="634bb-107">它會尋找 <`EncryptedData`> 專案、將專案解密，然後使用原始純文字 XML 專案來取代元素。</span><span class="sxs-lookup"><span data-stu-id="634bb-107">It finds an <`EncryptedData`> element, decrypts the element, and then replaces the element with the original plaintext XML element.</span></span>  
  
 <span data-ttu-id="634bb-108">此程序的程式碼範例會使用來自目前使用者帳戶本機憑證存放區的 X.509 憑證解密 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="634bb-108">The code example in this procedure decrypts an XML element using an X.509 certificate from the local certificate store of the current user account.</span></span>  <span data-ttu-id="634bb-109">此範例會使用 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法來自動抓取 x.509 憑證，並將儲存在 <> 專案的 <> 元素中的工作階段金鑰解密 `EncryptedKey` `EncryptedData` 。</span><span class="sxs-lookup"><span data-stu-id="634bb-109">The example uses the <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> method to automatically retrieve the X.509 certificate and decrypt a session key stored in the <`EncryptedKey`> element of the <`EncryptedData`> element.</span></span>  <span data-ttu-id="634bb-110"><xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法接著會自動使用工作階段金鑰解密 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="634bb-110">The <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> method then automatically uses the session key to decrypt the XML element.</span></span>  
  
 <span data-ttu-id="634bb-111">這個範例適合多個應用程式需要共用加密資料或應用程式需要在它執行時間之間儲存加密資料的情況。</span><span class="sxs-lookup"><span data-stu-id="634bb-111">This example is appropriate for situations where multiple applications need to share encrypted data or where an application needs to save encrypted data between the times that it runs.</span></span>  
  
### <a name="to-decrypt-an-xml-element-with-an-x509-certificate"></a><span data-ttu-id="634bb-112">使用 X.509 憑證解密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="634bb-112">To decrypt an XML element with an X.509 certificate</span></span>  
  
1. <span data-ttu-id="634bb-113">藉由從磁碟載入 XML 檔案，建立 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="634bb-113">Create an <xref:System.Xml.XmlDocument> object by loading an XML file from disk.</span></span>  <span data-ttu-id="634bb-114"><xref:System.Xml.XmlDocument> 物件會包含要解密的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="634bb-114">The <xref:System.Xml.XmlDocument> object contains the XML element to decrypt.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementX509#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementX509#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#2)]  
  
2. <span data-ttu-id="634bb-115">建立新的 <xref:System.Security.Cryptography.Xml.EncryptedXml> 物件，並傳遞 <xref:System.Xml.XmlDocument> 物件給建構函式。</span><span class="sxs-lookup"><span data-stu-id="634bb-115">Create a new <xref:System.Security.Cryptography.Xml.EncryptedXml> object by passing the <xref:System.Xml.XmlDocument> object to the constructor.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementX509#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementX509#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#3)]  
  
3. <span data-ttu-id="634bb-116">使用 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法解密 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="634bb-116">Decrypt the XML document using the <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> method.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementX509#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#4)]
     [!code-vb[HowToDecryptXMLElementX509#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#4)]  
  
4. <span data-ttu-id="634bb-117">儲存 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="634bb-117">Save the <xref:System.Xml.XmlDocument> object.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementX509#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementX509#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#5)]  
  
## <a name="example"></a><span data-ttu-id="634bb-118">範例</span><span class="sxs-lookup"><span data-stu-id="634bb-118">Example</span></span>  
 <span data-ttu-id="634bb-119">這個範例假設名為 `"test.xml"` 的檔案已存在於和編譯程式相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="634bb-119">This example assumes that a file named `"test.xml"` exists in the same directory as the compiled program.</span></span>  <span data-ttu-id="634bb-120">它同時也假設 `"test.xml"` 包含 `"creditcard"` 元素。</span><span class="sxs-lookup"><span data-stu-id="634bb-120">It also assumes that `"test.xml"` contains a `"creditcard"` element.</span></span>  <span data-ttu-id="634bb-121">您可以將下列 XML 放入稱為 `test.xml` 的檔案，並使用它搭配此範例。</span><span class="sxs-lookup"><span data-stu-id="634bb-121">You can place the following XML into a file called `test.xml` and use it with this example.</span></span>  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToDecryptXMLElementX509#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementX509#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="634bb-122">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="634bb-122">Compiling the Code</span></span>  
  
- <span data-ttu-id="634bb-123">若要編譯此範例，您需要包含 `System.Security.dll` 的參考。</span><span class="sxs-lookup"><span data-stu-id="634bb-123">To compile this example, you need to include a reference to `System.Security.dll`.</span></span>  
  
- <span data-ttu-id="634bb-124">包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。</span><span class="sxs-lookup"><span data-stu-id="634bb-124">Include the following namespaces: <xref:System.Xml>, <xref:System.Security.Cryptography>, and <xref:System.Security.Cryptography.Xml>.</span></span>  
  
## <a name="net-framework-security"></a><span data-ttu-id="634bb-125">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="634bb-125">.NET Framework Security</span></span>  
 <span data-ttu-id="634bb-126">此範例中使用的 X.509 憑證僅供測試使用。</span><span class="sxs-lookup"><span data-stu-id="634bb-126">The X.509 certificate used in this example is for test purposes only.</span></span>  <span data-ttu-id="634bb-127">應用程式應該使用由受信任的憑證授權單位所產生的 X.509 憑證，或使用由 Microsoft Windows 憑證伺服器所產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="634bb-127">Applications should use an X.509 certificate generated by a trusted certificate authority or use a certificate generated by the Microsoft Windows Certificate Server.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="634bb-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="634bb-128">See also</span></span>

- <xref:System.Security.Cryptography.Xml>
- [<span data-ttu-id="634bb-129">如何：使用 X.509 憑證加密 XML 元素</span><span class="sxs-lookup"><span data-stu-id="634bb-129">How to: Encrypt XML Elements with X.509 Certificates</span></span>](how-to-encrypt-xml-elements-with-x-509-certificates.md)

---
title: 作法：使用 X.509 憑證加密 XML 元素
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encryption [.NET], X.509 certificates
- cryptography [.NET], X.509 certificates
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- System.Security.Cryptography.X509Certificate2 class
- X.509 certificates
- certificates, X.509 certificates
ms.assetid: 761f1c66-631c-47af-aa86-ad9c50cfa453
ms.openlocfilehash: 5007404c1e6e872c169ce7ce71425f14d20d3a25
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94820185"
---
# <a name="how-to-encrypt-xml-elements-with-x509-certificates"></a><span data-ttu-id="9aacf-102">作法：使用 X.509 憑證加密 XML 元素</span><span class="sxs-lookup"><span data-stu-id="9aacf-102">How to: Encrypt XML Elements with X.509 Certificates</span></span>

<span data-ttu-id="9aacf-103">您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別來加密 XML 文件內的項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-103">You can use the classes in the <xref:System.Security.Cryptography.Xml> namespace to encrypt an element within an XML document.</span></span>  <span data-ttu-id="9aacf-104">XML 加密是交換或儲存加密 XML 資料的標準方法，不必擔心資料被輕易讀取。</span><span class="sxs-lookup"><span data-stu-id="9aacf-104">XML Encryption is a standard way to exchange or store encrypted XML data, without worrying about the data being easily read.</span></span>  <span data-ttu-id="9aacf-105">如需 XML 加密標準的詳細資訊，請參閱全球資訊網協會 (W3C) 規格中的 XML 加密（位於） <https://www.w3.org/TR/xmldsig-core/> 。</span><span class="sxs-lookup"><span data-stu-id="9aacf-105">For more information about the XML Encryption standard, see the World Wide Web Consortium (W3C) specification for XML Encryption located at <https://www.w3.org/TR/xmldsig-core/>.</span></span>  
  
 <span data-ttu-id="9aacf-106">您可以使用 XML 加密將任何 XML 元素或文件取代為包含加密 XML 資料的 <`EncryptedData`> 元素。</span><span class="sxs-lookup"><span data-stu-id="9aacf-106">You can use XML Encryption to replace any XML element or document with an <`EncryptedData`> element that contains the encrypted XML data.</span></span> <span data-ttu-id="9aacf-107"><`EncryptedData`> 元素可以包含子元素，而子元素會包含有關加密時所使用之金鑰和程序的資訊。</span><span class="sxs-lookup"><span data-stu-id="9aacf-107">The <`EncryptedData`> element can contain sub elements that include information about the keys and processes used during encryption.</span></span>  <span data-ttu-id="9aacf-108">XML 加密可讓文件中包含多個加密的元素，並允許元素加密多次。</span><span class="sxs-lookup"><span data-stu-id="9aacf-108">XML Encryption allows a document to contain multiple encrypted elements and allows an element to be encrypted multiple times.</span></span>  <span data-ttu-id="9aacf-109">這個程序中的程式碼範例將顯示如何建立 <`EncryptedData`> 元素和數個其他子元素，以便稍後在解密時使用。</span><span class="sxs-lookup"><span data-stu-id="9aacf-109">The code example in this procedure shows you how to create an <`EncryptedData`> element along with several other sub elements that you can use later during decryption.</span></span>  
  
<span data-ttu-id="9aacf-110">此範例會使用兩個金鑰來加密 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="9aacf-110">This example encrypts an XML element using two keys.</span></span> <span data-ttu-id="9aacf-111">此範例會以程式設計方式抓取憑證，並使用它來加密使用方法的 XML 元素 <xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> 。</span><span class="sxs-lookup"><span data-stu-id="9aacf-111">The example programmatically retrieves a certificate and uses it to encrypt an XML element using the <xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> method.</span></span> <span data-ttu-id="9aacf-112">就內部而言，<xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> 方法會建立個別的工作階段金鑰，並使用它來加密 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="9aacf-112">Internally, the <xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> method creates a separate session key and uses it to encrypt the XML document.</span></span> <span data-ttu-id="9aacf-113">這個方法會加密工作階段金鑰，並將它與加密的 XML 一併儲存在新的 <`EncryptedData`> 元素中。</span><span class="sxs-lookup"><span data-stu-id="9aacf-113">This method encrypts the session key and saves it along with the encrypted XML within a new <`EncryptedData`> element.</span></span>  

<span data-ttu-id="9aacf-114">若要解密 XML 專案，請呼叫 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法，此方法會自動從存放區抓取 x.509 憑證，並執行必要的解密。</span><span class="sxs-lookup"><span data-stu-id="9aacf-114">To decrypt the XML element, call the <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> method, which automatically retrieves the X.509 certificate from the store and performs the necessary decryption.</span></span>  <span data-ttu-id="9aacf-115">如需如何將使用這個程序加密的 XML 元素解密的詳細資訊，請參閱 [如何：使用 X.509 憑證解密 XML 元素](how-to-decrypt-xml-elements-with-x-509-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="9aacf-115">For more information about how to decrypt an XML element that was encrypted using this procedure, see [How to: Decrypt XML Elements with X.509 Certificates](how-to-decrypt-xml-elements-with-x-509-certificates.md).</span></span>  
  
<span data-ttu-id="9aacf-116">這個範例適合多個應用程式需要共用加密資料或應用程式需要在它執行時間之間儲存加密資料的情況。</span><span class="sxs-lookup"><span data-stu-id="9aacf-116">This example is appropriate for situations where multiple applications need to share encrypted data or where an application needs to save encrypted data between the times that it runs.</span></span>  
  
### <a name="to-encrypt-an-xml-element-with-an-x509-certificate"></a><span data-ttu-id="9aacf-117">使用 X.509 憑證加密 XML元素目</span><span class="sxs-lookup"><span data-stu-id="9aacf-117">To encrypt an XML element with an X.509 certificate</span></span>  

<span data-ttu-id="9aacf-118">若要執行此範例，您必須建立測試憑證，並將它儲存在憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="9aacf-118">To run this example, you need to create a test certificate and save it in a certificate store.</span></span> <span data-ttu-id="9aacf-119">這項工作的指示僅提供給 Windows [憑證建立工具 ( # A0) ](/windows/desktop/SecCrypto/makecert)。</span><span class="sxs-lookup"><span data-stu-id="9aacf-119">Instructions for that task are provided only for the Windows [Certificate Creation Tool (Makecert.exe)](/windows/desktop/SecCrypto/makecert).</span></span>

1. <span data-ttu-id="9aacf-120">使用 [Makecert.exe](/windows/desktop/SecCrypto/makecert) 產生測試 x.509 憑證，並將它放在本機使用者存放區中。</span><span class="sxs-lookup"><span data-stu-id="9aacf-120">Use [Makecert.exe](/windows/desktop/SecCrypto/makecert) to generate a test X.509 certificate and place it in the local user store.</span></span> <span data-ttu-id="9aacf-121">您必須產生交換金鑰，且必須使金鑰可以匯出。</span><span class="sxs-lookup"><span data-stu-id="9aacf-121">You must generate an exchange key and you must make the key exportable.</span></span> <span data-ttu-id="9aacf-122">執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9aacf-122">Run the following command:</span></span>  
  
    ```console  
    makecert -r -pe -n "CN=XML_ENC_TEST_CERT" -b 01/01/2020 -e 01/01/2025 -sky exchange -ss my  
    ```  
  
2. <span data-ttu-id="9aacf-123">建立 <xref:System.Security.Cryptography.X509Certificates.X509Store> 物件，並將它初始化以開啟目前使用者存放區。</span><span class="sxs-lookup"><span data-stu-id="9aacf-123">Create an <xref:System.Security.Cryptography.X509Certificates.X509Store> object and initialize it to open the current user store.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementX509#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#2)]  
  
3. <span data-ttu-id="9aacf-124">在唯讀模式開啟存放區。</span><span class="sxs-lookup"><span data-stu-id="9aacf-124">Open the store in read-only mode.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementX509#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#3)]  
  
4. <span data-ttu-id="9aacf-125">使用存放區中的所有憑證初始化 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2Collection>。</span><span class="sxs-lookup"><span data-stu-id="9aacf-125">Initialize an <xref:System.Security.Cryptography.X509Certificates.X509Certificate2Collection> with all of the certificates in the store.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementX509#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#4)]  
  
5. <span data-ttu-id="9aacf-126">列舉存放區中的憑證，並尋找適當名稱的憑證。</span><span class="sxs-lookup"><span data-stu-id="9aacf-126">Enumerate through the certificates in the store and find the certificate with the appropriate name.</span></span>  <span data-ttu-id="9aacf-127">在此範例中，憑證會命名為 `"CN=XML_ENC_TEST_CERT"`。</span><span class="sxs-lookup"><span data-stu-id="9aacf-127">In this example, the certificate is named `"CN=XML_ENC_TEST_CERT"`.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementX509#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#5)]  
  
6. <span data-ttu-id="9aacf-128">找到憑證之後，關閉存放區。</span><span class="sxs-lookup"><span data-stu-id="9aacf-128">Close the store after the certificate is located.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementX509#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#6)]  
  
7. <span data-ttu-id="9aacf-129">藉由從磁碟載入 XML 檔案，建立 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="9aacf-129">Create an <xref:System.Xml.XmlDocument> object by loading an XML file from disk.</span></span>  <span data-ttu-id="9aacf-130"><xref:System.Xml.XmlDocument> 物件會包含要加密的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-130">The <xref:System.Xml.XmlDocument> object contains the XML element to encrypt.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementX509#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#7)]  
  
8. <span data-ttu-id="9aacf-131">在 <xref:System.Xml.XmlDocument> 物件中尋找指定的項目，並建立新的 <xref:System.Xml.XmlElement> 物件以代表您想要加密的項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-131">Find the specified element in the <xref:System.Xml.XmlDocument> object and create a new <xref:System.Xml.XmlElement> object to represent the element you want to encrypt.</span></span>  <span data-ttu-id="9aacf-132">在此範例中，`"creditcard"` 元素已加密。</span><span class="sxs-lookup"><span data-stu-id="9aacf-132">In this example, the `"creditcard"` element is encrypted.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementX509#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#8)]  
  
9. <span data-ttu-id="9aacf-133">建立 <xref:System.Security.Cryptography.Xml.EncryptedXml> 類別的新執行個體，並使用它使用 X.509 憑證加密指定的項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-133">Create a new instance of the <xref:System.Security.Cryptography.Xml.EncryptedXml> class and use it to encrypt the specified element using the X.509 certificate.</span></span>  <span data-ttu-id="9aacf-134"><xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> 方法會以 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件傳回已加密的項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-134">The <xref:System.Security.Cryptography.Xml.EncryptedXml.Encrypt%2A> method returns the encrypted element as an <xref:System.Security.Cryptography.Xml.EncryptedData> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementX509#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#9)]  
  
10. <span data-ttu-id="9aacf-135">將來自原始 <xref:System.Xml.XmlDocument> 物件的項目取代為 <xref:System.Security.Cryptography.Xml.EncryptedData> 項目。</span><span class="sxs-lookup"><span data-stu-id="9aacf-135">Replace the element from the original <xref:System.Xml.XmlDocument> object with the <xref:System.Security.Cryptography.Xml.EncryptedData> element.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementX509#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#10)]  
  
11. <span data-ttu-id="9aacf-136">儲存 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="9aacf-136">Save the <xref:System.Xml.XmlDocument> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementX509#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementX509#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#11)]  
  
## <a name="example"></a><span data-ttu-id="9aacf-137">範例</span><span class="sxs-lookup"><span data-stu-id="9aacf-137">Example</span></span>  
 <span data-ttu-id="9aacf-138">這個範例假設名為 `"test.xml"` 的檔案已存在於和編譯程式相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="9aacf-138">This example assumes that a file named `"test.xml"` exists in the same directory as the compiled program.</span></span>  <span data-ttu-id="9aacf-139">它同時也假設 `"test.xml"` 包含 `"creditcard"` 元素。</span><span class="sxs-lookup"><span data-stu-id="9aacf-139">It also assumes that `"test.xml"` contains a `"creditcard"` element.</span></span>  <span data-ttu-id="9aacf-140">您可以將下列 XML 放入稱為 `test.xml` 的檔案，並使用它搭配此範例。</span><span class="sxs-lookup"><span data-stu-id="9aacf-140">You can place the following XML into a file called `test.xml` and use it with this example.</span></span>  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToEncryptXMLElementX509#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementX509/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementX509#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementX509/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="9aacf-141">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="9aacf-141">Compiling the Code</span></span>  
  
- <span data-ttu-id="9aacf-142">在以 .NET Framework 為目標的專案中，包含的參考 `System.Security.dll` 。</span><span class="sxs-lookup"><span data-stu-id="9aacf-142">In a project that targets .NET Framework, include a reference to `System.Security.dll`.</span></span>

- <span data-ttu-id="9aacf-143">在以 .NET Core 或 .NET 5 為目標的專案中，安裝 NuGet 套件 [System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml)。</span><span class="sxs-lookup"><span data-stu-id="9aacf-143">In a project that targets .NET Core or .NET 5, install NuGet package [System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml).</span></span>
  
- <span data-ttu-id="9aacf-144">包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。</span><span class="sxs-lookup"><span data-stu-id="9aacf-144">Include the following namespaces: <xref:System.Xml>, <xref:System.Security.Cryptography>, and <xref:System.Security.Cryptography.Xml>.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="9aacf-145">.NET 安全性</span><span class="sxs-lookup"><span data-stu-id="9aacf-145">.NET Security</span></span>
  
<span data-ttu-id="9aacf-146">此範例中使用的 X.509 憑證僅供測試使用。</span><span class="sxs-lookup"><span data-stu-id="9aacf-146">The X.509 certificate used in this example is for test purposes only.</span></span>  <span data-ttu-id="9aacf-147">應用程式應該使用由受信任的憑證授權單位單位所產生的 x.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="9aacf-147">Applications should use an X.509 certificate generated by a trusted certificate authority.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9aacf-148">請參閱</span><span class="sxs-lookup"><span data-stu-id="9aacf-148">See also</span></span>

- [<span data-ttu-id="9aacf-149">密碼編譯模型</span><span class="sxs-lookup"><span data-stu-id="9aacf-149">Cryptography Model</span></span>](cryptography-model.md)
- [<span data-ttu-id="9aacf-150">密碼編譯服務</span><span class="sxs-lookup"><span data-stu-id="9aacf-150">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="9aacf-151">跨平臺密碼編譯</span><span class="sxs-lookup"><span data-stu-id="9aacf-151">Cross-Platform Cryptography</span></span>](cross-platform-cryptography.md)
- <xref:System.Security.Cryptography.Xml>
- [<span data-ttu-id="9aacf-152">作法：使用 X.509 憑證解密 XML 元素</span><span class="sxs-lookup"><span data-stu-id="9aacf-152">How to: Decrypt XML Elements with X.509 Certificates</span></span>](how-to-decrypt-xml-elements-with-x-509-certificates.md)
- [<span data-ttu-id="9aacf-153">ASP.NET Core 資料保護</span><span class="sxs-lookup"><span data-stu-id="9aacf-153">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)

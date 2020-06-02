---
title: 如何：使用非對稱金鑰解密 XML 項目
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.RSACryptoServiceProvider class
- asymmetric keys
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- decryption
ms.assetid: dd5de491-dafe-4b94-966d-99714b2e754a
ms.openlocfilehash: b3d5d91ff8cf268e4e7a1330ff596a97924dfe55
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290846"
---
# <a name="how-to-decrypt-xml-elements-with-asymmetric-keys"></a><span data-ttu-id="034f8-102">如何：使用非對稱金鑰解密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="034f8-102">How to: Decrypt XML Elements with Asymmetric Keys</span></span>
<span data-ttu-id="034f8-103">您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別來加密和解密 XML 文件內的項目。</span><span class="sxs-lookup"><span data-stu-id="034f8-103">You can use the classes in the <xref:System.Security.Cryptography.Xml> namespace to encrypt and decrypt an element within an XML document.</span></span>  <span data-ttu-id="034f8-104">XML 加密是交換或儲存加密 XML 資料的標準方法，不必擔心資料被輕易讀取。</span><span class="sxs-lookup"><span data-stu-id="034f8-104">XML Encryption is a standard way to exchange or store encrypted XML data, without worrying about the data being easily read.</span></span>  <span data-ttu-id="034f8-105">如需 XML 加密標準的詳細資訊，請參閱全球資訊網協會（W3C）建議[xml 簽章語法和處理](https://www.w3.org/TR/xmldsig-core/)。</span><span class="sxs-lookup"><span data-stu-id="034f8-105">For more information about the XML Encryption standard, see the World Wide Web Consortium (W3C) recommendation [XML Signature Syntax and Processing](https://www.w3.org/TR/xmldsig-core/).</span></span>  
  
 <span data-ttu-id="034f8-106">此程式中的範例會使用 how [to：使用非對稱金鑰加密 XML](how-to-encrypt-xml-elements-with-asymmetric-keys.md)專案中所述的方法，解密已加密的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="034f8-106">The example in this procedure decrypts an XML element that was encrypted using the methods described in [How to: Encrypt XML Elements with Asymmetric Keys](how-to-encrypt-xml-elements-with-asymmetric-keys.md).</span></span>  <span data-ttu-id="034f8-107">它會尋找 <`EncryptedData`> 專案、將專案解密，然後使用原始純文字 XML 專案來取代元素。</span><span class="sxs-lookup"><span data-stu-id="034f8-107">It finds an <`EncryptedData`> element, decrypts the element, and then replaces the element with the original plaintext XML element.</span></span>  
  
 <span data-ttu-id="034f8-108">此範例會使用兩個金鑰來解密 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="034f8-108">This example decrypts an XML element using two keys.</span></span>  <span data-ttu-id="034f8-109">它會從金鑰容器中抓取先前產生的 RSA 私密金鑰，然後使用 RSA 金鑰來解密儲存在 <> 元素的 <> 元素中的工作階段金鑰 `EncryptedKey` `EncryptedData` 。</span><span class="sxs-lookup"><span data-stu-id="034f8-109">It retrieves a previously generated RSA private key from a key container, and then uses the RSA key to decrypt a session key stored in the <`EncryptedKey`> element of the <`EncryptedData`> element.</span></span>  <span data-ttu-id="034f8-110">範例接著會使用工作階段金鑰解密 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="034f8-110">The example then uses the session key to decrypt the XML element.</span></span>  
  
 <span data-ttu-id="034f8-111">這個範例適合多個應用程式必須共用加密資料或應用程式必須在它執行時間之間儲存加密資料的情況。</span><span class="sxs-lookup"><span data-stu-id="034f8-111">This example is appropriate for situations where multiple applications have to share encrypted data or where an application has to save encrypted data between the times that it runs.</span></span>  
  
### <a name="to-decrypt-an-xml-element-with-an-asymmetric-key"></a><span data-ttu-id="034f8-112">使用非對稱金鑰解密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="034f8-112">To decrypt an XML element with an asymmetric key</span></span>  
  
1. <span data-ttu-id="034f8-113">建立 <xref:System.Security.Cryptography.CspParameters> 物件，並指定金鑰容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="034f8-113">Create a <xref:System.Security.Cryptography.CspParameters> object and specify the name of the key container.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2. <span data-ttu-id="034f8-114">使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 物件從容器擷取先前產生的非對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="034f8-114">Retrieve a previously generated asymmetric key from the container using the <xref:System.Security.Cryptography.RSACryptoServiceProvider> object.</span></span>  <span data-ttu-id="034f8-115">當您將 <xref:System.Security.Cryptography.CspParameters> 物件傳遞到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 建構函式時，金鑰會自動從金鑰容器擷取。</span><span class="sxs-lookup"><span data-stu-id="034f8-115">The key is automatically retrieved from the key container when you pass the <xref:System.Security.Cryptography.CspParameters> object to the <xref:System.Security.Cryptography.RSACryptoServiceProvider> constructor.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3. <span data-ttu-id="034f8-116">建立新的 <xref:System.Security.Cryptography.Xml.EncryptedXml> 物件以解密文件。</span><span class="sxs-lookup"><span data-stu-id="034f8-116">Create a new <xref:System.Security.Cryptography.Xml.EncryptedXml> object to decrypt the document.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
4. <span data-ttu-id="034f8-117">加入金鑰/名稱對應以將 RSA 金鑰與應該解密之文件中的項目相關聯。</span><span class="sxs-lookup"><span data-stu-id="034f8-117">Add a key/name mapping to associate the RSA key with the element within the document that should be decrypted.</span></span>  <span data-ttu-id="034f8-118">您必須使用與加密文件時所使用金鑰相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="034f8-118">You must use the same name for the key that you used when you encrypted the document.</span></span>  <span data-ttu-id="034f8-119">請注意，這個名稱與用來識別步驟 1 中所指定金鑰容器中的金鑰名稱不同。</span><span class="sxs-lookup"><span data-stu-id="034f8-119">Note that this name is separate from the name used to identify the key in the key container specified in step 1.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
5. <span data-ttu-id="034f8-120">呼叫 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法，將 <`EncryptedData`> 元素解密。</span><span class="sxs-lookup"><span data-stu-id="034f8-120">Call the <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> method to decrypt the <`EncryptedData`> element.</span></span>  <span data-ttu-id="034f8-121">這個方法會使用 RSA 金鑰來解密工作階段金鑰，並會自動使用工作階段金鑰解密 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="034f8-121">This method uses the RSA key to decrypt the session key and automatically uses the session key to decrypt the XML element.</span></span>  <span data-ttu-id="034f8-122">它也會自動 `EncryptedData` 以原始純文字取代 <的> 元素。</span><span class="sxs-lookup"><span data-stu-id="034f8-122">It also automatically replaces the <`EncryptedData`> element with the original plaintext.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
6. <span data-ttu-id="034f8-123">儲存 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="034f8-123">Save the XML document.</span></span>  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="034f8-124">範例</span><span class="sxs-lookup"><span data-stu-id="034f8-124">Example</span></span>  
 <span data-ttu-id="034f8-125">這個範例假設名為 `test.xml` 的檔案已存在於和編譯程式相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="034f8-125">This example assumes that a file named `test.xml` exists in the same directory as the compiled program.</span></span>  <span data-ttu-id="034f8-126">它也假設 `test.xml` 包含使用 how [to：使用非對稱金鑰加密 XML](how-to-encrypt-xml-elements-with-asymmetric-keys.md)專案中所述的技術來加密的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="034f8-126">It also assumes that `test.xml` contains an XML element that was encrypted using the techniques described in [How to: Encrypt XML Elements with Asymmetric Keys](how-to-encrypt-xml-elements-with-asymmetric-keys.md).</span></span>  
  
 [!code-csharp[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="034f8-127">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="034f8-127">Compiling the Code</span></span>  
  
- <span data-ttu-id="034f8-128">若要編譯此範例，您需要包含 `System.Security.dll` 的參考。</span><span class="sxs-lookup"><span data-stu-id="034f8-128">To compile this example, you need to include a reference to `System.Security.dll`.</span></span>  
  
- <span data-ttu-id="034f8-129">包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。</span><span class="sxs-lookup"><span data-stu-id="034f8-129">Include the following namespaces: <xref:System.Xml>, <xref:System.Security.Cryptography>, and <xref:System.Security.Cryptography.Xml>.</span></span>  
  
## <a name="net-framework-security"></a><span data-ttu-id="034f8-130">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="034f8-130">.NET Framework Security</span></span>  
 <span data-ttu-id="034f8-131">絕對不要以純文字儲存對稱密碼編譯金鑰，或以純文字格式在電腦之間傳輸對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="034f8-131">Never store a symmetric cryptographic key in plaintext or transfer a symmetric key between machines in plaintext.</span></span>  <span data-ttu-id="034f8-132">此外，絕對不要以純文字儲存或傳輸非對稱金鑰組的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="034f8-132">Additionally, never store or transfer the private key of an asymmetric key pair in plaintext.</span></span>  <span data-ttu-id="034f8-133">如需對稱和非對稱密碼編譯金鑰的詳細資訊，請參閱[產生加密和解密的金鑰](generating-keys-for-encryption-and-decryption.md)。</span><span class="sxs-lookup"><span data-stu-id="034f8-133">For more information about symmetric and asymmetric cryptographic keys, see [Generating Keys for Encryption and Decryption](generating-keys-for-encryption-and-decryption.md).</span></span>  
  
 <span data-ttu-id="034f8-134">絕對不要直接將金鑰內嵌在您的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="034f8-134">Never embed a key directly into your source code.</span></span>  <span data-ttu-id="034f8-135">您可以使用[Ildasm （IL](../../framework/tools/ildasm-exe-il-disassembler.md)解譯器）或在文字編輯器（例如 [記事本]）中開啟元件，輕鬆地從元件中讀取內嵌的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="034f8-135">Embedded keys can be easily read from an assembly by using [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) or by opening the assembly in a text editor such as Notepad.</span></span>  
  
 <span data-ttu-id="034f8-136">當您使用完密碼編譯金鑰，請從記憶體清除它，方法是將每個位元組設定為零，或呼叫 Managed 密碼編譯類別的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="034f8-136">When you are done using a cryptographic key, clear it from memory by setting each byte to zero or by calling the <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> method of the managed cryptography class.</span></span>  <span data-ttu-id="034f8-137">偵錯工具有時可以從記憶體讀取密碼編譯金鑰，或是在記憶體位置被分頁至磁碟的情況下從硬碟機讀取。</span><span class="sxs-lookup"><span data-stu-id="034f8-137">Cryptographic keys can sometimes be read from memory by a debugger or read from a hard drive if the memory location is paged to disk.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="034f8-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="034f8-138">See also</span></span>

- <xref:System.Security.Cryptography.Xml>
- [<span data-ttu-id="034f8-139">如何：使用非對稱金鑰加密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="034f8-139">How to: Encrypt XML Elements with Asymmetric Keys</span></span>](how-to-encrypt-xml-elements-with-asymmetric-keys.md)

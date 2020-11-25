---
title: 作法：使用非對稱金鑰加密 XML 元素
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [.NET], asymmetric keys
- AES algorithm
- System.Security.Cryptography.RSA class
- asymmetric keys [.NET]
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- key containers
- Advanced Encryption Standard algorithm
- encryption [.NET], asymmetric keys
ms.assetid: a164ba4f-e596-4bbe-a9ca-f214fe89ed48
ms.openlocfilehash: 29fe7c229664b08c9e1563413525818f2e883198
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729339"
---
# <a name="how-to-encrypt-xml-elements-with-asymmetric-keys"></a><span data-ttu-id="66b9e-102">作法：使用非對稱金鑰加密 XML 元素</span><span class="sxs-lookup"><span data-stu-id="66b9e-102">How to: Encrypt XML Elements with Asymmetric Keys</span></span>

<span data-ttu-id="66b9e-103">您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別來加密 XML 文件內的項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-103">You can use the classes in the <xref:System.Security.Cryptography.Xml> namespace to encrypt an element within an XML document.</span></span>  <span data-ttu-id="66b9e-104">XML 加密是交換或儲存加密 XML 資料的標準方法，不必擔心資料被輕易讀取。</span><span class="sxs-lookup"><span data-stu-id="66b9e-104">XML Encryption is a standard way to exchange or store encrypted XML data, without worrying about the data being easily read.</span></span>  <span data-ttu-id="66b9e-105">如需 XML 加密標準的詳細資訊，請參閱全球資訊網協會 (W3C) 規格中的 XML 加密（位於） <https://www.w3.org/TR/xmldsig-core/> 。</span><span class="sxs-lookup"><span data-stu-id="66b9e-105">For more information about the XML Encryption standard, see the World Wide Web Consortium (W3C) specification for XML Encryption located at <https://www.w3.org/TR/xmldsig-core/>.</span></span>  
  
 <span data-ttu-id="66b9e-106">您可以使用 XML 加密將任何 XML 元素或文件取代為包含加密 XML 資料的 <`EncryptedData`> 元素。</span><span class="sxs-lookup"><span data-stu-id="66b9e-106">You can use XML Encryption to replace any XML element or document with an <`EncryptedData`> element that contains the encrypted XML data.</span></span>  <span data-ttu-id="66b9e-107"><的 `EncryptedData`> 專案也可以包含子項目，其中包含加密期間使用之金鑰和進程的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66b9e-107">The <`EncryptedData`> element can also contain sub elements that include information about the keys and processes used during encryption.</span></span>  <span data-ttu-id="66b9e-108">XML 加密可讓文件中包含多個加密的元素，並允許元素加密多次。</span><span class="sxs-lookup"><span data-stu-id="66b9e-108">XML Encryption allows a document to contain multiple encrypted elements and allows an element to be encrypted multiple times.</span></span>  <span data-ttu-id="66b9e-109">此程式中的程式碼範例示範如何建立 <的 `EncryptedData`> 元素，以及您稍後可在解密期間使用的數個其他子項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-109">The code example in this procedure shows how to create an <`EncryptedData`> element along with several other sub elements that you can use later during decryption.</span></span>  
  
 <span data-ttu-id="66b9e-110">此範例會使用兩個金鑰來加密 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="66b9e-110">This example encrypts an XML element using two keys.</span></span>  <span data-ttu-id="66b9e-111">它會產生 RSA 公開/私密金鑰組，並將金鑰組儲存到安全的金鑰容器。</span><span class="sxs-lookup"><span data-stu-id="66b9e-111">It generates an RSA public/private key pair and saves the key pair to a secure key container.</span></span>  <span data-ttu-id="66b9e-112">然後，此範例會使用進階加密標準 (AES) 演算法來建立個別的工作階段金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-112">The example then creates a separate session key using the Advanced Encryption Standard (AES) algorithm.</span></span>  <span data-ttu-id="66b9e-113">範例會使用 AES 工作階段金鑰來加密 XML 文件，然後使用 RSA 公開金鑰來加密 AES 工作階段金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-113">The example uses the AES session key to encrypt the XML document and then uses the RSA public key to encrypt the AES session key.</span></span>  <span data-ttu-id="66b9e-114">最後，此範例會將加密的 AES 工作階段金鑰和加密的 XML 資料儲存到新的 <> 元素內的 XML 檔中 `EncryptedData` 。</span><span class="sxs-lookup"><span data-stu-id="66b9e-114">Finally, the example saves the encrypted AES session key and the encrypted XML data to the XML document within a new <`EncryptedData`> element.</span></span>  
  
 <span data-ttu-id="66b9e-115">若要解密 XML 項目，您可以從金鑰容器中擷取 RSA 私密金鑰、用它來解密工作階段金鑰，然後使用工作階段金鑰來解密文件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-115">To decrypt the XML element, you retrieve the RSA private key from the key container, use it to decrypt the session key, and then use the session key to decrypt the document.</span></span>  <span data-ttu-id="66b9e-116">如需如何將使用這個程式加密的 XML 專案解密的詳細資訊，請參閱 [如何：使用非對稱金鑰解密 Xml 元素](how-to-decrypt-xml-elements-with-asymmetric-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="66b9e-116">For more information about how to decrypt an XML element that was encrypted using this procedure, see [How to: Decrypt XML Elements with Asymmetric Keys](how-to-decrypt-xml-elements-with-asymmetric-keys.md).</span></span>  
  
 <span data-ttu-id="66b9e-117">這個範例適合多個應用程式需要共用加密資料或應用程式需要在它執行時間之間儲存加密資料的情況。</span><span class="sxs-lookup"><span data-stu-id="66b9e-117">This example is appropriate for situations where multiple applications need to share encrypted data or where an application needs to save encrypted data between the times that it runs.</span></span>
  
### <a name="to-encrypt-an-xml-element-with-an-asymmetric-key"></a><span data-ttu-id="66b9e-118">使用非對稱金鑰加密 XML 項目</span><span class="sxs-lookup"><span data-stu-id="66b9e-118">To encrypt an XML element with an asymmetric key</span></span>  
  
1. <span data-ttu-id="66b9e-119">建立 <xref:System.Security.Cryptography.CspParameters> 物件，並指定金鑰容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="66b9e-119">Create a <xref:System.Security.Cryptography.CspParameters> object and specify the name of the key container.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2. <span data-ttu-id="66b9e-120">使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別產生對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-120">Generate a symmetric key using the <xref:System.Security.Cryptography.RSACryptoServiceProvider> class.</span></span>  <span data-ttu-id="66b9e-121">當您將 <xref:System.Security.Cryptography.CspParameters> 物件傳遞到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別的建構函式時，金鑰會自動儲存到金鑰容器。</span><span class="sxs-lookup"><span data-stu-id="66b9e-121">The key is automatically saved to the key container when you pass the <xref:System.Security.Cryptography.CspParameters> object to the constructor of the <xref:System.Security.Cryptography.RSACryptoServiceProvider> class.</span></span>  <span data-ttu-id="66b9e-122">這個金鑰會用來加密 AES 工作階段金鑰，而且可以稍後擷取來進行解密。</span><span class="sxs-lookup"><span data-stu-id="66b9e-122">This key will be used to encrypt the AES session key and can be retrieved later to decrypt it.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3. <span data-ttu-id="66b9e-123">藉由從磁碟載入 XML 檔案，建立 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-123">Create an <xref:System.Xml.XmlDocument> object by loading an XML file from disk.</span></span>  <span data-ttu-id="66b9e-124"><xref:System.Xml.XmlDocument> 物件會包含要加密的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-124">The <xref:System.Xml.XmlDocument> object contains the XML element to encrypt.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#4)]  
  
4. <span data-ttu-id="66b9e-125">在 <xref:System.Xml.XmlDocument> 物件中尋找指定的項目，並建立新的 <xref:System.Xml.XmlElement> 物件以代表您想要加密的項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-125">Find the specified element in the <xref:System.Xml.XmlDocument> object and create a new <xref:System.Xml.XmlElement> object to represent the element you want to encrypt.</span></span> <span data-ttu-id="66b9e-126">在此範例中，`"creditcard"` 元素已加密。</span><span class="sxs-lookup"><span data-stu-id="66b9e-126">In this example, the `"creditcard"` element is encrypted.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
5. <span data-ttu-id="66b9e-127">使用 <xref:System.Security.Cryptography.Aes> 類別建立新的工作階段金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-127">Create a new session key using the <xref:System.Security.Cryptography.Aes> class.</span></span>  <span data-ttu-id="66b9e-128">這個金鑰會加密 XML 項目，並再加密本身並放在 XML 文件中。</span><span class="sxs-lookup"><span data-stu-id="66b9e-128">This key will encrypt the XML element, and then be encrypted itself and placed in the XML document.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
6. <span data-ttu-id="66b9e-129">建立 <xref:System.Security.Cryptography.Xml.EncryptedXml> 類別的新執行個體，並使用它使用工作階段金鑰加密指定的項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-129">Create a new instance of the <xref:System.Security.Cryptography.Xml.EncryptedXml> class and use it to encrypt the specified element using the session key.</span></span>  <span data-ttu-id="66b9e-130"><xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> 方法會以加密位元組陣列傳回已加密的項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-130">The <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> method returns the encrypted element as an array of encrypted bytes.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
7. <span data-ttu-id="66b9e-131">建構 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件並填入加密 XML 項目的 URL 識別項。</span><span class="sxs-lookup"><span data-stu-id="66b9e-131">Construct an <xref:System.Security.Cryptography.Xml.EncryptedData> object and populate it with the URL identifier of the encrypted XML element.</span></span>  <span data-ttu-id="66b9e-132">這個 URL 識別項可讓解密的一方知道 XML 包含加密的項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-132">This URL identifier lets a decrypting party know that the XML contains an encrypted element.</span></span>  <span data-ttu-id="66b9e-133">您可以使用 <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> 欄位來指定 URL 識別項。</span><span class="sxs-lookup"><span data-stu-id="66b9e-133">You can use the <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> field to specify the URL identifier.</span></span>  <span data-ttu-id="66b9e-134">純文字 XML 專案將由 `EncryptedData` 這個物件所封裝的 <> 元素所取代 <xref:System.Security.Cryptography.Xml.EncryptedData> 。</span><span class="sxs-lookup"><span data-stu-id="66b9e-134">The plaintext XML element will be replaced by an <`EncryptedData`> element encapsulated by this <xref:System.Security.Cryptography.Xml.EncryptedData> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
8. <span data-ttu-id="66b9e-135">建立 <xref:System.Security.Cryptography.Xml.EncryptionMethod> 物件，它會初始化為用來產生工作階段金鑰之密碼編譯演算法的 URL 識別項。</span><span class="sxs-lookup"><span data-stu-id="66b9e-135">Create an <xref:System.Security.Cryptography.Xml.EncryptionMethod> object that is initialized to the URL identifier of the cryptographic algorithm used to generate the session key.</span></span>  <span data-ttu-id="66b9e-136">將 <xref:System.Security.Cryptography.Xml.EncryptionMethod> 物件傳遞至 <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="66b9e-136">Pass the <xref:System.Security.Cryptography.Xml.EncryptionMethod> object to the <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A> property.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#9)]  
  
9. <span data-ttu-id="66b9e-137">建立 <xref:System.Security.Cryptography.Xml.EncryptedKey> 物件，以包含加密工作階段金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-137">Create an <xref:System.Security.Cryptography.Xml.EncryptedKey> object to contain the encrypted session key.</span></span>  <span data-ttu-id="66b9e-138">加密工作階段金鑰、將它加入 <xref:System.Security.Cryptography.Xml.EncryptedKey> 物件，然後輸入工作階段金鑰名稱和金鑰識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="66b9e-138">Encrypt the session key, add it to the <xref:System.Security.Cryptography.Xml.EncryptedKey> object, and enter a session key name and key identifier URL.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#10)]  
  
10. <span data-ttu-id="66b9e-139">建立新的 <xref:System.Security.Cryptography.Xml.DataReference> 物件，將加密的資料對應至特定工作階段金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-139">Create a new <xref:System.Security.Cryptography.Xml.DataReference> object that maps the encrypted data to a particular session key.</span></span>  <span data-ttu-id="66b9e-140">此選用步驟可讓您輕鬆地指定 XML 文件的多個部分是由單一金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="66b9e-140">This optional step allows you to easily specify that multiple parts of an XML document were encrypted by a single key.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#11)]  
  
11. <span data-ttu-id="66b9e-141">將加密的金鑰加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-141">Add the encrypted key to the <xref:System.Security.Cryptography.Xml.EncryptedData> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#12)]  
  
12. <span data-ttu-id="66b9e-142">建立新的 <xref:System.Security.Cryptography.Xml.KeyInfo> 物件，指定 RSA 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="66b9e-142">Create a new <xref:System.Security.Cryptography.Xml.KeyInfo> object to specify the name of the RSA key.</span></span>  <span data-ttu-id="66b9e-143">將它加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-143">Add it to the <xref:System.Security.Cryptography.Xml.EncryptedData> object.</span></span> <span data-ttu-id="66b9e-144">這有助於解密方識別要解密工作階段金鑰時所使用的正確非對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-144">This helps the decrypting party identify the correct asymmetric key to use when decrypting the session key.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#13)]  
  
13. <span data-ttu-id="66b9e-145">將加密項目資料加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-145">Add the encrypted element data to the <xref:System.Security.Cryptography.Xml.EncryptedData> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#14)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#14)]  
  
14. <span data-ttu-id="66b9e-146">將來自原始 <xref:System.Xml.XmlDocument> 物件的項目取代為 <xref:System.Security.Cryptography.Xml.EncryptedData> 項目。</span><span class="sxs-lookup"><span data-stu-id="66b9e-146">Replace the element from the original <xref:System.Xml.XmlDocument> object with the <xref:System.Security.Cryptography.Xml.EncryptedData> element.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#15)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#15)]  
  
15. <span data-ttu-id="66b9e-147">儲存 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="66b9e-147">Save the <xref:System.Xml.XmlDocument> object.</span></span>  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#16)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#16)]  
  
## <a name="example"></a><span data-ttu-id="66b9e-148">範例</span><span class="sxs-lookup"><span data-stu-id="66b9e-148">Example</span></span>  

 <span data-ttu-id="66b9e-149">這個範例假設名為 `"test.xml"` 的檔案已存在於和編譯程式相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="66b9e-149">This example assumes that a file named `"test.xml"` exists in the same directory as the compiled program.</span></span>  <span data-ttu-id="66b9e-150">它同時也假設 `"test.xml"` 包含 `"creditcard"` 元素。</span><span class="sxs-lookup"><span data-stu-id="66b9e-150">It also assumes that `"test.xml"` contains a `"creditcard"` element.</span></span>  <span data-ttu-id="66b9e-151">您可以將下列 XML 放入稱為 `test.xml` 的檔案，並使用它搭配此範例。</span><span class="sxs-lookup"><span data-stu-id="66b9e-151">You can place the following XML into a file called `test.xml` and use it with this example.</span></span>  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="66b9e-152">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="66b9e-152">Compiling the Code</span></span>  
  
- <span data-ttu-id="66b9e-153">在以 .NET Framework 為目標的專案中，包含的參考 `System.Security.dll` 。</span><span class="sxs-lookup"><span data-stu-id="66b9e-153">In a project that targets .NET Framework, include a reference to `System.Security.dll`.</span></span>

- <span data-ttu-id="66b9e-154">在以 .NET Core 或 .NET 5 為目標的專案中，安裝 NuGet 套件 [System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml)。</span><span class="sxs-lookup"><span data-stu-id="66b9e-154">In a project that targets .NET Core or .NET 5, install NuGet package [System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml).</span></span>
  
- <span data-ttu-id="66b9e-155">包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。</span><span class="sxs-lookup"><span data-stu-id="66b9e-155">Include the following namespaces: <xref:System.Xml>, <xref:System.Security.Cryptography>, and <xref:System.Security.Cryptography.Xml>.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="66b9e-156">.NET 安全性</span><span class="sxs-lookup"><span data-stu-id="66b9e-156">.NET Security</span></span>

<span data-ttu-id="66b9e-157">絕對不要以純文字儲存對稱密碼編譯金鑰，或以純文字格式在電腦之間傳輸對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-157">Never store a symmetric cryptographic key in plaintext or transfer a symmetric key between machines in plaintext.</span></span>  <span data-ttu-id="66b9e-158">此外，絕對不要以純文字儲存或傳輸非對稱金鑰組的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-158">Additionally, never store or transfer the private key of an asymmetric key pair in plaintext.</span></span>  <span data-ttu-id="66b9e-159">如需對稱和非對稱式密碼編譯金鑰的詳細資訊，請參閱 [產生加密和解密的金鑰](generating-keys-for-encryption-and-decryption.md)。</span><span class="sxs-lookup"><span data-stu-id="66b9e-159">For more information about symmetric and asymmetric cryptographic keys, see [Generating Keys for Encryption and Decryption](generating-keys-for-encryption-and-decryption.md).</span></span>  
  
<span data-ttu-id="66b9e-160">絕對不要直接將金鑰內嵌在您的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="66b9e-160">Never embed a key directly into your source code.</span></span>  <span data-ttu-id="66b9e-161">您可以使用 [Ildasm.exe (IL ](../../framework/tools/ildasm-exe-il-disassembler.md) 解譯器) 或在文字編輯器（例如 [記事本]）中開啟元件，輕鬆地從元件讀取內嵌的金鑰。</span><span class="sxs-lookup"><span data-stu-id="66b9e-161">Embedded keys can be easily read from an assembly using the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) or by opening the assembly in a text editor such as Notepad.</span></span>  
  
<span data-ttu-id="66b9e-162">當您使用完密碼編譯金鑰，請從記憶體清除它，方法是將每個位元組設定為零，或呼叫 Managed 密碼編譯類別的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="66b9e-162">When you are done using a cryptographic key, clear it from memory by setting each byte to zero or by calling the <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> method of the managed cryptography class.</span></span>  <span data-ttu-id="66b9e-163">偵錯工具有時可以從記憶體讀取密碼編譯金鑰，或是在記憶體位置被分頁至磁碟的情況下從硬碟機讀取。</span><span class="sxs-lookup"><span data-stu-id="66b9e-163">Cryptographic keys can sometimes be read from memory by a debugger or read from a hard drive if the memory location is paged to disk.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="66b9e-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66b9e-164">See also</span></span>

- [<span data-ttu-id="66b9e-165">密碼編譯模型</span><span class="sxs-lookup"><span data-stu-id="66b9e-165">Cryptography Model</span></span>](cryptography-model.md)
- [<span data-ttu-id="66b9e-166">密碼編譯服務</span><span class="sxs-lookup"><span data-stu-id="66b9e-166">Cryptographic Services</span></span>](cryptographic-services.md)
- <span data-ttu-id="66b9e-167">[跨平臺密碼編譯](cross-platform-cryptography.md)- <xref:System.Security.Cryptography.Xml></span><span class="sxs-lookup"><span data-stu-id="66b9e-167">[Cross-Platform Cryptography](cross-platform-cryptography.md)- <xref:System.Security.Cryptography.Xml></span></span>
- [<span data-ttu-id="66b9e-168">操作說明：使用非對稱金鑰解密 XML 元素</span><span class="sxs-lookup"><span data-stu-id="66b9e-168">How to: Decrypt XML Elements with Asymmetric Keys</span></span>](how-to-decrypt-xml-elements-with-asymmetric-keys.md)
- [<span data-ttu-id="66b9e-169">ASP.NET Core 資料保護</span><span class="sxs-lookup"><span data-stu-id="66b9e-169">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)

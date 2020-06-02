---
title: 產生加密和解密金鑰
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keys, encryption and decryption
- keys, asymmetric
- keys, symmetric
- encryption [.NET Framework], keys
- symmetric keys
- asymmetric keys [.NET Framework]
- cryptography [.NET Framework], keys
ms.assetid: c197dfc9-a453-4226-898d-37a16638056e
ms.openlocfilehash: 992ac30310d138e04b8408497c5e49166a356ab4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291535"
---
# <a name="generating-keys-for-encryption-and-decryption"></a><span data-ttu-id="18a05-102">產生加密和解密金鑰</span><span class="sxs-lookup"><span data-stu-id="18a05-102">Generating Keys for Encryption and Decryption</span></span>
<span data-ttu-id="18a05-103">建立和管理金鑰是密碼編譯程序中很重要的一部分。</span><span class="sxs-lookup"><span data-stu-id="18a05-103">Creating and managing keys is an important part of the cryptographic process.</span></span> <span data-ttu-id="18a05-104">對稱演算法需要建立金鑰和初始化向量 (IV)。</span><span class="sxs-lookup"><span data-stu-id="18a05-104">Symmetric algorithms require the creation of a key and an initialization vector (IV).</span></span> <span data-ttu-id="18a05-105">務必不要對不該解密您資料的任何人透露金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-105">The key must be kept secret from anyone who should not decrypt your data.</span></span> <span data-ttu-id="18a05-106">IV 不需要加密，但是應該針對每個工作階段變更。</span><span class="sxs-lookup"><span data-stu-id="18a05-106">The IV does not have to be secret, but should be changed for each session.</span></span> <span data-ttu-id="18a05-107">非對稱演算法需要建立公開金鑰和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-107">Asymmetric algorithms require the creation of a public key and a private key.</span></span> <span data-ttu-id="18a05-108">公開金鑰可以公開給任何人，但私密金鑰必須只有將解密以公開金鑰加密之資料的一方知道。</span><span class="sxs-lookup"><span data-stu-id="18a05-108">The public key can be made public to anyone, while the private key must known only by the party who will decrypt the data encrypted with the public key.</span></span> <span data-ttu-id="18a05-109">本節描述如何產生及管理對稱和非對稱演算法的金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-109">This section describes how to generate and manage keys for both symmetric and asymmetric algorithms.</span></span>  
  
## <a name="symmetric-keys"></a><span data-ttu-id="18a05-110">對稱金鑰</span><span class="sxs-lookup"><span data-stu-id="18a05-110">Symmetric Keys</span></span>  
 <span data-ttu-id="18a05-111">.NET Framework 所提供的對稱加密類別需要一個金鑰和新的初始化向量 (IV) 才能加密和解密資料。</span><span class="sxs-lookup"><span data-stu-id="18a05-111">The symmetric encryption classes supplied by the .NET Framework require a key and a new initialization vector (IV) to encrypt and decrypt data.</span></span> <span data-ttu-id="18a05-112">每當您使用無參數的函式來建立其中一個 managed 對稱密碼編譯類別的新實例時，就會自動建立新的金鑰和 IV。</span><span class="sxs-lookup"><span data-stu-id="18a05-112">Whenever you create a new instance of one of the managed symmetric cryptographic classes using the parameterless constructor, a new key and IV are automatically created.</span></span> <span data-ttu-id="18a05-113">您允許解密資料的任何人都必須擁有相同的金鑰和 IV，並使用相同的演算法。</span><span class="sxs-lookup"><span data-stu-id="18a05-113">Anyone that you allow to decrypt your data must possess the same key and IV and use the same algorithm.</span></span> <span data-ttu-id="18a05-114">一般而言，應該為每個工作階段建立新的金鑰和 IV，且金鑰和 IV 都不應該儲存以用於稍後的工作階段。</span><span class="sxs-lookup"><span data-stu-id="18a05-114">Generally, a new key and IV should be created for every session, and neither the key nor IV should be stored for use in a later session.</span></span>  
  
 <span data-ttu-id="18a05-115">若要與遠端的一方溝通對稱金鑰和 IV，通常會使用非對稱加密來加密對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-115">To communicate a symmetric key and IV to a remote party, you would usually encrypt the symmetric key by using asymmetric encryption.</span></span> <span data-ttu-id="18a05-116">在不安全的網路中傳送未加密的金鑰並不安全，因為任何人只要攔截金鑰和 IV，就可以解密您的資料。</span><span class="sxs-lookup"><span data-stu-id="18a05-116">Sending the key across an insecure network without encrypting it is unsafe, because anyone who intercepts the key and IV can then decrypt your data.</span></span> <span data-ttu-id="18a05-117">如需使用加密交換資料的詳細資訊，請參閱 [建立密碼編譯配置](creating-a-cryptographic-scheme.md)。</span><span class="sxs-lookup"><span data-stu-id="18a05-117">For more information about exchanging data by using encryption, see [Creating a Cryptographic Scheme](creating-a-cryptographic-scheme.md).</span></span>  
  
 <span data-ttu-id="18a05-118">下列範例顯示實作 TripleDES 演算法的 <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> 類別的新執行個體建立。</span><span class="sxs-lookup"><span data-stu-id="18a05-118">The following example shows the creation of a new instance of the <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> class that implements the TripleDES algorithm.</span></span>  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
```  
  
 <span data-ttu-id="18a05-119">先前的程式碼執行時，會產生新的金鑰和 IV 並分別放在 **Key** 和 **IV** 屬性。</span><span class="sxs-lookup"><span data-stu-id="18a05-119">When the previous code is executed, a new key and IV are generated and placed in the **Key** and **IV** properties, respectively.</span></span>  
  
 <span data-ttu-id="18a05-120">有時候您可能需要產生多個金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-120">Sometimes you might need to generate multiple keys.</span></span> <span data-ttu-id="18a05-121">在此情況下，您可以建立實作對稱演算法之類別的新執行個體，然後呼叫 **GenerateKey** 和 **GenerateIV** 方法來建立新的金鑰和 IV。</span><span class="sxs-lookup"><span data-stu-id="18a05-121">In this situation, you can create a new instance of a class that implements a symmetric algorithm and then create a new key and IV by calling the **GenerateKey** and **GenerateIV** methods.</span></span> <span data-ttu-id="18a05-122">下列程式碼範例說明如何在建立對稱密碼編譯類別的新實例之後，建立新的金鑰和 Iv。</span><span class="sxs-lookup"><span data-stu-id="18a05-122">The following code example illustrates how to create new keys and IVs after a new instance of the symmetric cryptographic class has been made.</span></span>  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
tdes.GenerateIV()  
tdes.GenerateKey()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
tdes.GenerateIV();  
tdes.GenerateKey();  
```  
  
 <span data-ttu-id="18a05-123">先前的程式碼執行時，當建立 **TripleDESCryptoServiceProvider** 的新執行個體時，會產生金鑰和 IV。</span><span class="sxs-lookup"><span data-stu-id="18a05-123">When the previous code is executed, a key and IV are generated when the new instance of **TripleDESCryptoServiceProvider** is made.</span></span> <span data-ttu-id="18a05-124">呼叫 **GenerateKey** 和 **GenerateIV** 方法時，會建立另一個金鑰和 IV。</span><span class="sxs-lookup"><span data-stu-id="18a05-124">Another key and IV are created when the **GenerateKey** and **GenerateIV** methods are called.</span></span>  
  
## <a name="asymmetric-keys"></a><span data-ttu-id="18a05-125">非對稱金鑰</span><span class="sxs-lookup"><span data-stu-id="18a05-125">Asymmetric Keys</span></span>  
 <span data-ttu-id="18a05-126">.NET Framework 提供 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 和 <xref:System.Security.Cryptography.DSACryptoServiceProvider> 類別以進行非對稱式加密。</span><span class="sxs-lookup"><span data-stu-id="18a05-126">The .NET Framework provides the <xref:System.Security.Cryptography.RSACryptoServiceProvider> and <xref:System.Security.Cryptography.DSACryptoServiceProvider> classes for asymmetric encryption.</span></span> <span data-ttu-id="18a05-127">當您使用無參數的構造函式來建立新的實例時，這些類別會建立公開/私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="18a05-127">These classes create a public/private key pair when you use the parameterless constructor to create a new instance.</span></span> <span data-ttu-id="18a05-128">非對稱金鑰可以儲存以用於多個工作階段，或只針對一個工作階段而產生。</span><span class="sxs-lookup"><span data-stu-id="18a05-128">Asymmetric keys can be either stored for use in multiple sessions or generated for one session only.</span></span> <span data-ttu-id="18a05-129">雖然公開金鑰可以公開提供使用，但應該小心地看護私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a05-129">While the public key can be made generally available, the private key should be closely guarded.</span></span>  
  
 <span data-ttu-id="18a05-130">每當建立非對稱式演算法類別的新執行個體時，就會產生公開/私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="18a05-130">A public/private key pair is generated whenever a new instance of an asymmetric algorithm class is created.</span></span> <span data-ttu-id="18a05-131">建立類別的新執行個體之後，可以使用兩種方法之一擷取金鑰資訊：</span><span class="sxs-lookup"><span data-stu-id="18a05-131">After a new instance of the class is created, the key information can be extracted using one of two methods:</span></span>  
  
- <span data-ttu-id="18a05-132"><xref:System.Security.Cryptography.RSA.ToXmlString%2A> 方法，會傳回金鑰資訊的 XML 表示法。</span><span class="sxs-lookup"><span data-stu-id="18a05-132">The <xref:System.Security.Cryptography.RSA.ToXmlString%2A> method, which returns an XML representation of the key information.</span></span>  
  
- <span data-ttu-id="18a05-133"><xref:System.Security.Cryptography.RSACryptoServiceProvider.ExportParameters%2A> 方法，它會傳回 <xref:System.Security.Cryptography.RSAParameters> 結構，可保存金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="18a05-133">The <xref:System.Security.Cryptography.RSACryptoServiceProvider.ExportParameters%2A> method, which returns an <xref:System.Security.Cryptography.RSAParameters> structure that holds the key information.</span></span>  
  
 <span data-ttu-id="18a05-134">這兩種方法都接受布林值，表示是否只傳回公用金鑰資訊，還是同時傳回公開金鑰和私密金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="18a05-134">Both methods accept a Boolean value that indicates whether to return only the public key information or to return both the public-key and the private-key information.</span></span> <span data-ttu-id="18a05-135">**RSACryptoServiceProvider** 類別可以使用 **方法，初始化為** RSAParameters <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A> 結構的值。</span><span class="sxs-lookup"><span data-stu-id="18a05-135">An **RSACryptoServiceProvider** class can be initialized to the value of an **RSAParameters** structure by using the <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A> method.</span></span>  
  
 <span data-ttu-id="18a05-136">非對稱私密金鑰不應逐字或以純文字儲存到本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="18a05-136">Asymmetric private keys should never be stored verbatim or in plain text on the local computer.</span></span> <span data-ttu-id="18a05-137">如果您需要儲存私密金鑰，您應該使用金鑰容器。</span><span class="sxs-lookup"><span data-stu-id="18a05-137">If you need to store a private key, you should use a key container.</span></span> <span data-ttu-id="18a05-138">如需如何將私密金鑰儲存到金鑰容器的詳細資訊，請參閱 [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md)。</span><span class="sxs-lookup"><span data-stu-id="18a05-138">For more on how to store a private key in a key container, see [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md).</span></span>  
  
 <span data-ttu-id="18a05-139">下列程式碼範例會建立 **RSACryptoServiceProvider** 類別的新執行個體、建立公開/私密金鑰組，並將公開金鑰資訊儲存到 **RSAParameters** 結構。</span><span class="sxs-lookup"><span data-stu-id="18a05-139">The following code example creates a new instance of the **RSACryptoServiceProvider** class, creating a public/private key pair, and saves the public key information to an **RSAParameters** structure.</span></span>  
  
```vb  
'Generate a public/private key pair.  
Dim rsa as RSACryptoServiceProvider = new RSACryptoServiceProvider()  
'Save the public key information to an RSAParameters structure.  
Dim rsaKeyInfo As RSAParameters = rsa.ExportParameters(false)  
```  
  
```csharp  
//Generate a public/private key pair.  
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();  
//Save the public key information to an RSAParameters structure.  
RSAParameters rsaKeyInfo = rsa.ExportParameters(false);  
```  
  
## <a name="see-also"></a><span data-ttu-id="18a05-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="18a05-140">See also</span></span>

- [<span data-ttu-id="18a05-141">加密資料</span><span class="sxs-lookup"><span data-stu-id="18a05-141">Encrypting Data</span></span>](encrypting-data.md)
- [<span data-ttu-id="18a05-142">解密資料</span><span class="sxs-lookup"><span data-stu-id="18a05-142">Decrypting Data</span></span>](decrypting-data.md)
- [<span data-ttu-id="18a05-143">密碼編譯服務</span><span class="sxs-lookup"><span data-stu-id="18a05-143">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="18a05-144">How to: Store Asymmetric Keys in a Key Container</span><span class="sxs-lookup"><span data-stu-id="18a05-144">How to: Store Asymmetric Keys in a Key Container</span></span>](how-to-store-asymmetric-keys-in-a-key-container.md)

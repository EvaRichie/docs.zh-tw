---
title: 在 SQL Server 中加密資料
ms.date: 03/30/2017
ms.assetid: 83b992f7-b351-4678-b4b9-f4ffd58134cc
ms.openlocfilehash: d0bda11f1a2933d096aa91d2be79d3af35172284
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169527"
---
# <a name="data-encryption-in-sql-server"></a><span data-ttu-id="1f95a-102">在 SQL Server 中加密資料</span><span class="sxs-lookup"><span data-stu-id="1f95a-102">Data Encryption in SQL Server</span></span>

<span data-ttu-id="1f95a-103">SQL Server 提供使用憑證、非對稱金鑰或對稱金鑰來加密及解密資料的功能，</span><span class="sxs-lookup"><span data-stu-id="1f95a-103">SQL Server provides functions to encrypt and decrypt data using a certificate, asymmetric key, or symmetric key.</span></span> <span data-ttu-id="1f95a-104">而且可在內部的憑證存放區內管理上述所有項目。</span><span class="sxs-lookup"><span data-stu-id="1f95a-104">It manages all of these in an internal certificate store.</span></span> <span data-ttu-id="1f95a-105">此存放區會使用加密階層，藉由階層中的上層層級來確保下層層級的憑證及金鑰。</span><span class="sxs-lookup"><span data-stu-id="1f95a-105">The store uses an encryption hierarchy that secures certificates and keys at one level with the layer above it in the hierarchy.</span></span> <span data-ttu-id="1f95a-106">SQL Server 的此功能區也稱為「秘密儲存區」(Secret Storage)。</span><span class="sxs-lookup"><span data-stu-id="1f95a-106">This feature area of SQL Server is called Secret Storage.</span></span>  
  
 <span data-ttu-id="1f95a-107">由加密功能所支援的最快加密模式是對稱金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="1f95a-107">The fastest mode of encryption supported by the encryption functions is symmetric key encryption.</span></span> <span data-ttu-id="1f95a-108">此模式適合用來處理大量的資料。</span><span class="sxs-lookup"><span data-stu-id="1f95a-108">This mode is suitable for handling large volumes of data.</span></span> <span data-ttu-id="1f95a-109">對稱金鑰可以藉由憑證、密碼或其他對稱金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="1f95a-109">The symmetric keys can be encrypted by certificates, passwords or other symmetric keys.</span></span>  
  
## <a name="keys-and-algorithms"></a><span data-ttu-id="1f95a-110">金鑰和演算法</span><span class="sxs-lookup"><span data-stu-id="1f95a-110">Keys and Algorithms</span></span>  

 <span data-ttu-id="1f95a-111">SQL Server 支援數種對稱金鑰加密演算法，包括 DES、Triple DES、RC2、RC4、128 位元 RC4、DESX、128 位元 AES、192 位元 AES 和 256 位元 AES 等，</span><span class="sxs-lookup"><span data-stu-id="1f95a-111">SQL Server supports several symmetric key encryption algorithms, including DES, Triple DES, RC2, RC4, 128-bit RC4, DESX, 128-bit AES, 192-bit AES, and 256-bit AES.</span></span> <span data-ttu-id="1f95a-112">這些演算法是使用 Windows Crypto API 來實作。</span><span class="sxs-lookup"><span data-stu-id="1f95a-112">The algorithms are implemented using the Windows Crypto API.</span></span>  
  
 <span data-ttu-id="1f95a-113">SQL Server 可在資料庫連接的範圍內維護多個開放式的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="1f95a-113">Within the scope of a database connection, SQL Server can maintain multiple open symmetric keys.</span></span> <span data-ttu-id="1f95a-114">您可從存放區擷取開放式金鑰，並將其用於解密資料。</span><span class="sxs-lookup"><span data-stu-id="1f95a-114">An open key is retrieved from the store and is available for decrypting data.</span></span> <span data-ttu-id="1f95a-115">在資料解密後，就不需指定要使用的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="1f95a-115">When a piece of data is decrypted, there is no need to specify the symmetric key to use.</span></span> <span data-ttu-id="1f95a-116">每個加密的值都包含加密時所使用金鑰的識別碼 (金鑰 GUID)。</span><span class="sxs-lookup"><span data-stu-id="1f95a-116">Each encrypted value contains the key identifier (key GUID) of the key used to encrypt it.</span></span> <span data-ttu-id="1f95a-117">如果已解密並開啟了正確的金鑰，則引擎會比對加密的位元組資料流與開放式對稱金鑰，</span><span class="sxs-lookup"><span data-stu-id="1f95a-117">The engine matches the encrypted byte stream to an open symmetric key, if the correct key has been decrypted and is open.</span></span> <span data-ttu-id="1f95a-118">然後再使用此金鑰來執行解密作業並傳回資料。</span><span class="sxs-lookup"><span data-stu-id="1f95a-118">This key is then used to perform decryption and return the data.</span></span> <span data-ttu-id="1f95a-119">如果沒有開啟正確的金鑰，則會傳回 NULL。</span><span class="sxs-lookup"><span data-stu-id="1f95a-119">If the correct key is not open, NULL is returned.</span></span>  
  
 <span data-ttu-id="1f95a-120">如需示範如何使用資料庫中加密資料的範例，請參閱 [加密資料行](/sql/relational-databases/security/encryption/encrypt-a-column-of-data)。</span><span class="sxs-lookup"><span data-stu-id="1f95a-120">For an example that shows how to work with encrypted data in a database, see [Encrypt a Column of Data](/sql/relational-databases/security/encryption/encrypt-a-column-of-data).</span></span>
  
## <a name="external-resources"></a><span data-ttu-id="1f95a-121">外部資源</span><span class="sxs-lookup"><span data-stu-id="1f95a-121">External Resources</span></span>  

 <span data-ttu-id="1f95a-122">如需有關資料加密的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="1f95a-122">For more information on data encryption, see the following resources.</span></span>  
  
|<span data-ttu-id="1f95a-123">資源</span><span class="sxs-lookup"><span data-stu-id="1f95a-123">Resource</span></span>|<span data-ttu-id="1f95a-124">描述</span><span class="sxs-lookup"><span data-stu-id="1f95a-124">Description</span></span>|  
|-|-|  
|[<span data-ttu-id="1f95a-125">SQL Server 加密</span><span class="sxs-lookup"><span data-stu-id="1f95a-125">SQL Server Encryption</span></span>](/sql/relational-databases/security/encryption/sql-server-encryption)|<span data-ttu-id="1f95a-126">提供 SQL Server 中的加密概觀。</span><span class="sxs-lookup"><span data-stu-id="1f95a-126">Provides an overview of encryption in SQL Server.</span></span> <span data-ttu-id="1f95a-127">本主題包含其他文章的連結。</span><span class="sxs-lookup"><span data-stu-id="1f95a-127">This topic includes links to additional articles.</span></span>|  
|[<span data-ttu-id="1f95a-128">加密階層</span><span class="sxs-lookup"><span data-stu-id="1f95a-128">Encryption Hierarchy</span></span>](/sql/relational-databases/security/encryption/encryption-hierarchy)|<span data-ttu-id="1f95a-129">提供 SQL Server 中的加密概觀。</span><span class="sxs-lookup"><span data-stu-id="1f95a-129">Provides an overview of encryption in SQL Server.</span></span> <span data-ttu-id="1f95a-130">本主題提供其他文章的連結。</span><span class="sxs-lookup"><span data-stu-id="1f95a-130">This topic provides links to additional articles.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="1f95a-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f95a-131">See also</span></span>

- [<span data-ttu-id="1f95a-132">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="1f95a-132">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- [<span data-ttu-id="1f95a-133">SQL Server 中的應用程式安全性案例</span><span class="sxs-lookup"><span data-stu-id="1f95a-133">Application Security Scenarios in SQL Server</span></span>](application-security-scenarios-in-sql-server.md)
- [<span data-ttu-id="1f95a-134">在 SQL Server 中進行驗證</span><span class="sxs-lookup"><span data-stu-id="1f95a-134">Authentication in SQL Server</span></span>](authentication-in-sql-server.md)
- [<span data-ttu-id="1f95a-135">SQL Server 中的伺服器和資料庫角色</span><span class="sxs-lookup"><span data-stu-id="1f95a-135">Server and Database Roles in SQL Server</span></span>](server-and-database-roles-in-sql-server.md)
- [<span data-ttu-id="1f95a-136">SQL Server 中的擁有權和使用者結構描述分離</span><span class="sxs-lookup"><span data-stu-id="1f95a-136">Ownership and User-Schema Separation in SQL Server</span></span>](ownership-and-user-schema-separation-in-sql-server.md)
- [<span data-ttu-id="1f95a-137">SQL Server 中的授權和權限</span><span class="sxs-lookup"><span data-stu-id="1f95a-137">Authorization and Permissions in SQL Server</span></span>](authorization-and-permissions-in-sql-server.md)
- <span data-ttu-id="1f95a-138">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="1f95a-138">[ADO.NET Overview](../ado-net-overview.md)</span></span>

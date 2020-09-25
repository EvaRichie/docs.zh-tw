---
title: LINQ to SQL 中的安全性
ms.date: 03/30/2017
ms.assetid: d49787f7-414e-4c71-aa33-80a5895536b1
ms.openlocfilehash: 6260f0c565a25764c8fabd2770d4f06a987aa9bb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173389"
---
# <a name="security-in-linq-to-sql"></a><span data-ttu-id="ddbe3-102">LINQ to SQL 中的安全性</span><span class="sxs-lookup"><span data-stu-id="ddbe3-102">Security in LINQ to SQL</span></span>

<span data-ttu-id="ddbe3-103">當您連接至資料庫時，永遠都會存在安全性風險。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-103">Security risks are always present when you connect to a database.</span></span> <span data-ttu-id="ddbe3-104">雖然 LINQ to SQL 可能會包含一些使用 SQL Server 資料的新方式，但是並不會提供任何額外的安全性機制。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-104">Although LINQ to SQL may include some new ways to work with data in SQL Server, it does not provide any additional security mechanisms.</span></span>  
  
## <a name="access-control-and-authentication"></a><span data-ttu-id="ddbe3-105">存取控制和驗證</span><span class="sxs-lookup"><span data-stu-id="ddbe3-105">Access Control and Authentication</span></span>  

 <span data-ttu-id="ddbe3-106">LINQ to SQL 本身並沒有使用者模型或驗證機制。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-106">LINQ to SQL does not have its own user model or authentication mechanisms.</span></span> <span data-ttu-id="ddbe3-107">您可以使用 SQL Server 安全性來控制對應至物件模型 (Object Model) 之資料庫、資料庫資料表、檢視表和預存程序 (Stored Procedure) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-107">Use SQL Server Security to control access to the database, database tables, views, and stored procedures that are mapped to your object model.</span></span> <span data-ttu-id="ddbe3-108">請將最低必要存取權授與使用者，並且要求增強式密碼來進行使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-108">Grant the minimally required access to users and require strong passwords for user authentication.</span></span>  
  
## <a name="mapping-and-schema-information"></a><span data-ttu-id="ddbe3-109">對應和結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="ddbe3-109">Mapping and Schema Information</span></span>  

 <span data-ttu-id="ddbe3-110">物件模型或外部對應檔案中的 SQL-CLR 型別對應和資料庫結構描述資訊可供所有在檔案系統中擁有這些檔案之存取權的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-110">SQL-CLR type mapping and database schema information in your object model or external mapping file is available for all with access to those files in the file system.</span></span> <span data-ttu-id="ddbe3-111">假設可以存取物件模型或外部對應檔案的所有人員都可以使用架構資訊。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-111">Assume that schema information will be available to all who can access the object model or external mapping file.</span></span> <span data-ttu-id="ddbe3-112">若要避免更廣泛地存取架構資訊，請使用檔案安全性機制來保護來源檔案和對應檔。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-112">To prevent more widespread access to schema information, use file security mechanisms to secure source files and mapping files.</span></span>  
  
## <a name="connection-strings"></a><span data-ttu-id="ddbe3-113">連接字串</span><span class="sxs-lookup"><span data-stu-id="ddbe3-113">Connection Strings</span></span>  

 <span data-ttu-id="ddbe3-114">請盡可能避免在連接字串中使用密碼。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-114">Using passwords in connection strings should be avoided whenever possible.</span></span> <span data-ttu-id="ddbe3-115">不但連接字串本身會產生安全性風險，而且使用物件關聯式設計工具或 SQLMetal 命令列工具時，連接字串可能也會以純文字的方式加入至物件模型或外部對應檔案。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-115">Not only is a connection string a security risk in its own right, but the connection string may also be added in clear text to the object model or external mapping file when using the Object Relational Designer or SQLMetal command-line tool.</span></span> <span data-ttu-id="ddbe3-116">可經由檔案系統存取物件模型或外部對應檔案的任何人都可能會看見連接密碼 (如果包含在連接字串中的話)。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-116">Anyone with access to the object model or external mapping file via the file system could see the connection password (if it is included in the connection string).</span></span>  
  
 <span data-ttu-id="ddbe3-117">若要將這類風險降至最低，請使用整合式安全性來建立與 SQL Server 的信任連線。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-117">To minimize such risks, use integrated security to make a trusted connection with SQL Server.</span></span> <span data-ttu-id="ddbe3-118">使用這種方法，就不需要將密碼儲存在連接字串中。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-118">By using this approach, you do not have to store a password in the connection string.</span></span> <span data-ttu-id="ddbe3-119">如需詳細資訊，請參閱 [SQL Server 安全性](../sql-server-security.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-119">For more information, see [SQL Server Security](../sql-server-security.md).</span></span>  
  
 <span data-ttu-id="ddbe3-120">如果沒有整合式安全性，連接字串將會需要純文字密碼。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-120">In the absence of integrated security, a clear-text password will be needed in the connection string.</span></span> <span data-ttu-id="ddbe3-121">協助保護連接字串安全的最佳方法如下所示 (按照風險的遞增順序列出)：</span><span class="sxs-lookup"><span data-stu-id="ddbe3-121">The best way to help secure your connection string, in increasing order of risk, is as follows:</span></span>  
  
- <span data-ttu-id="ddbe3-122">使用整合式安全性。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-122">Use integrated security.</span></span>  
  
- <span data-ttu-id="ddbe3-123">使用密碼來保護連接字串的安全，並且盡可能減少在連接字串前後傳遞密碼。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-123">Secure connection strings with passwords and minimize passing around connection strings.</span></span>  
  
- <span data-ttu-id="ddbe3-124">使用 <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> 類別 (Class) 來取代連接字串，因為它會限制公開的持續期間。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-124">Use a <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> class instead of a connection string since it limits the duration of exposure.</span></span> <span data-ttu-id="ddbe3-125">您可以使用 <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> 來具現化 LINQ to SQL <xref:System.Data.SqlClient.SqlConnection> 類別。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-125">The LINQ to SQL <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> class can be instantiated using a <xref:System.Data.SqlClient.SqlConnection>.</span></span>  
  
- <span data-ttu-id="ddbe3-126">盡可能減少所有連接字串的存留期 (Lifetime) 和接觸點。</span><span class="sxs-lookup"><span data-stu-id="ddbe3-126">Minimize lifetimes and touch points for all connection strings.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ddbe3-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ddbe3-127">See also</span></span>

- [<span data-ttu-id="ddbe3-128">背景資訊</span><span class="sxs-lookup"><span data-stu-id="ddbe3-128">Background Information</span></span>](background-information.md)
- [<span data-ttu-id="ddbe3-129">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ddbe3-129">Frequently Asked Questions</span></span>](frequently-asked-questions.md)

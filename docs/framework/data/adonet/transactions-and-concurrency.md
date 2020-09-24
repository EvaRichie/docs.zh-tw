---
title: 異動和並行存取
ms.date: 03/30/2017
ms.assetid: f46570de-9e50-4fe6-8710-a8c31fa8569b
ms.openlocfilehash: 049e402345e1abbb46739e48c89101207a43bb27
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91191667"
---
# <a name="transactions-and-concurrency"></a><span data-ttu-id="8e127-102">異動和並行存取</span><span class="sxs-lookup"><span data-stu-id="8e127-102">Transactions and Concurrency</span></span>

<span data-ttu-id="8e127-103">異動是由單一命令或當做封裝 (Package) 執行的命令群組所組成。</span><span class="sxs-lookup"><span data-stu-id="8e127-103">A transaction consists of a single command or a group of commands that execute as a package.</span></span> <span data-ttu-id="8e127-104">交易可讓您將多項作業結合成單一工作單位。</span><span class="sxs-lookup"><span data-stu-id="8e127-104">Transactions allow you to combine multiple operations into a single unit of work.</span></span> <span data-ttu-id="8e127-105">如果異動的某一處失敗，則所有更新都會復原到異動之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="8e127-105">If a failure occurs at one point in the transaction, all of the updates can be rolled back to their pre-transaction state.</span></span>  
  
 <span data-ttu-id="8e127-106">異動必須符合 ACID 屬性 (單元性 (Atomicity)、一致性 (Consistency)、隔離性 (Isolation) 和持續性 (Durability)，才能保證資料一致性。</span><span class="sxs-lookup"><span data-stu-id="8e127-106">A transaction must conform to the ACID properties—atomicity, consistency, isolation, and durability—in order to guarantee data consistency.</span></span> <span data-ttu-id="8e127-107">大多數關聯式資料庫系統 (例如 Microsoft SQL Server) 都可以支援異動，其方法是在每次用戶端應用程式執行更新、插入或刪除作業時，提供鎖定、記錄和異動管理功能。</span><span class="sxs-lookup"><span data-stu-id="8e127-107">Most relational database systems, such as Microsoft SQL Server, support transactions by providing locking, logging, and transaction management facilities whenever a client application performs an update, insert, or delete operation.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8e127-108">如果鎖定保留時間太久，包含多個資源的交易可能會降低並行。</span><span class="sxs-lookup"><span data-stu-id="8e127-108">Transactions that involve multiple resources can lower concurrency if locks are held too long.</span></span> <span data-ttu-id="8e127-109">因此，請盡可能縮短異動的時間長度。</span><span class="sxs-lookup"><span data-stu-id="8e127-109">Therefore, keep transactions as short as possible.</span></span>  
  
 <span data-ttu-id="8e127-110">如果某筆異動包含相同資料庫或伺服器中的多個資料表，則預存程序 (Stored Procedure) 中的明確異動通常會有較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="8e127-110">If a transaction involves multiple tables in the same database or server, then explicit transactions in stored procedures often perform better.</span></span> <span data-ttu-id="8e127-111">您可以使用 Transact-SQL `BEGIN TRANSACTION`、`COMMIT TRANSACTION` 和 `ROLLBACK TRANSACTION` 陳述式，在 SQL Server 預存程序中建立交易。</span><span class="sxs-lookup"><span data-stu-id="8e127-111">You can create transactions in SQL Server stored procedures by using the Transact-SQL `BEGIN TRANSACTION`, `COMMIT TRANSACTION`, and `ROLLBACK TRANSACTION` statements.</span></span> <span data-ttu-id="8e127-112">如需詳細資訊，請參閱《SQL Server 線上叢書》。</span><span class="sxs-lookup"><span data-stu-id="8e127-112">For more information, see SQL Server Books Online.</span></span>  
  
 <span data-ttu-id="8e127-113">涉及不同資源管理員的交易（例如 SQL Server 與 Oracle 之間的交易）需要分散式交易。</span><span class="sxs-lookup"><span data-stu-id="8e127-113">Transactions involving different resource managers, such as a transaction between SQL Server and Oracle, require a distributed transaction.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="8e127-114">本節內容</span><span class="sxs-lookup"><span data-stu-id="8e127-114">In This Section</span></span>  

 [<span data-ttu-id="8e127-115">本機交易</span><span class="sxs-lookup"><span data-stu-id="8e127-115">Local Transactions</span></span>](local-transactions.md)  
 <span data-ttu-id="8e127-116">示範如何針對資料庫執行交易。</span><span class="sxs-lookup"><span data-stu-id="8e127-116">Demonstrates how to perform transactions against a database.</span></span>  
  
 [<span data-ttu-id="8e127-117">分散式交易</span><span class="sxs-lookup"><span data-stu-id="8e127-117">Distributed Transactions</span></span>](distributed-transactions.md)  
 <span data-ttu-id="8e127-118">說明如何在 ADO.NET 中執行分散式異動。</span><span class="sxs-lookup"><span data-stu-id="8e127-118">Describes how to perform distributed transactions in ADO.NET.</span></span>  
  
 [<span data-ttu-id="8e127-119">System.Transactions 與 SQL Server 整合</span><span class="sxs-lookup"><span data-stu-id="8e127-119">System.Transactions Integration with SQL Server</span></span>](system-transactions-integration-with-sql-server.md)  
 <span data-ttu-id="8e127-120">描述 <xref:System.Transactions> 與使用分散式交易的 SQL Server 整合。</span><span class="sxs-lookup"><span data-stu-id="8e127-120">Describes <xref:System.Transactions> integration with SQL Server for working with distributed transactions.</span></span>  
  
 [<span data-ttu-id="8e127-121">開放式平行存取</span><span class="sxs-lookup"><span data-stu-id="8e127-121">Optimistic Concurrency</span></span>](optimistic-concurrency.md)  
 <span data-ttu-id="8e127-122">說明開放式與封閉式同步存取，以及如何測試並行違規。</span><span class="sxs-lookup"><span data-stu-id="8e127-122">Describes optimistic and pessimistic concurrency, and how you can test for concurrency violations.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8e127-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8e127-123">See also</span></span>

- [<span data-ttu-id="8e127-124">交易基礎觀念</span><span class="sxs-lookup"><span data-stu-id="8e127-124">Transaction Fundamentals</span></span>](../transactions/transaction-fundamentals.md)
- [<span data-ttu-id="8e127-125">連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="8e127-125">Connecting to a Data Source</span></span>](connecting-to-a-data-source.md)
- [<span data-ttu-id="8e127-126">命令和參數</span><span class="sxs-lookup"><span data-stu-id="8e127-126">Commands and Parameters</span></span>](commands-and-parameters.md)
- [<span data-ttu-id="8e127-127">DataAdapter 和 DataReader</span><span class="sxs-lookup"><span data-stu-id="8e127-127">DataAdapters and DataReaders</span></span>](dataadapters-and-datareaders.md)
- [<span data-ttu-id="8e127-128">DbProviderFactory</span><span class="sxs-lookup"><span data-stu-id="8e127-128">DbProviderFactories</span></span>](dbproviderfactories.md)
- <span data-ttu-id="8e127-129">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="8e127-129">[ADO.NET Overview](ado-net-overview.md)</span></span>

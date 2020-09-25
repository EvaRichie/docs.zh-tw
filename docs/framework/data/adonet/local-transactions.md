---
title: 本機交易
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
ms.openlocfilehash: a0b713ab0b81cb2f0661212dae22db34b7f9f3ae
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91175391"
---
# <a name="local-transactions"></a><span data-ttu-id="29fb8-102">本機交易</span><span class="sxs-lookup"><span data-stu-id="29fb8-102">Local Transactions</span></span>

<span data-ttu-id="29fb8-103">當您想要將多個工作系結在一起，使其以單一工作單位的形式執行時，會使用 ADO.NET 中的交易。</span><span class="sxs-lookup"><span data-stu-id="29fb8-103">Transactions in ADO.NET are used when you want to bind multiple tasks together so that they execute as a single unit of work.</span></span> <span data-ttu-id="29fb8-104">例如，想像應用程式正在執行兩項工作。</span><span class="sxs-lookup"><span data-stu-id="29fb8-104">For example, imagine that an application performs two tasks.</span></span> <span data-ttu-id="29fb8-105">首先，它會更新包含訂單資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="29fb8-105">First, it updates a table with order information.</span></span> <span data-ttu-id="29fb8-106">然後會更新包含存貨資訊的資料表，將訂購項目記入借方。</span><span class="sxs-lookup"><span data-stu-id="29fb8-106">Second, it updates a table that contains inventory information, debiting the items ordered.</span></span> <span data-ttu-id="29fb8-107">如果其中一項工作失敗，則會回復這兩個更新。</span><span class="sxs-lookup"><span data-stu-id="29fb8-107">If either task fails, then both updates are rolled back.</span></span>  
  
## <a name="determining-the-transaction-type"></a><span data-ttu-id="29fb8-108">決定異動類型</span><span class="sxs-lookup"><span data-stu-id="29fb8-108">Determining the Transaction Type</span></span>  

 <span data-ttu-id="29fb8-109">當交易是單一階段交易時，會將交易視為本機交易，並且由資料庫直接處理。</span><span class="sxs-lookup"><span data-stu-id="29fb8-109">A transaction is considered to be a local transaction when it is a single-phase transaction and is handled by the database directly.</span></span> <span data-ttu-id="29fb8-110">當交易由交易監視器協調時，會將交易視為分散式交易，並使用 (的安全機制，例如用於交易解析的兩階段認可) 。</span><span class="sxs-lookup"><span data-stu-id="29fb8-110">A transaction is considered to be a distributed transaction when it is coordinated by a transaction monitor and uses fail-safe mechanisms (such as two-phase commit) for transaction resolution.</span></span>  
  
 <span data-ttu-id="29fb8-111">每個 .NET Framework 資料提供者都有自己 `Transaction` 的物件可執行本機交易。</span><span class="sxs-lookup"><span data-stu-id="29fb8-111">Each of the .NET Framework data providers has its own `Transaction` object for performing local transactions.</span></span> <span data-ttu-id="29fb8-112">如果您需要在 SQL Server 資料庫中執行異動，請選擇 <xref:System.Data.SqlClient> 異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-112">If you require a transaction to be performed in a SQL Server database, select a <xref:System.Data.SqlClient> transaction.</span></span> <span data-ttu-id="29fb8-113">若為 Oracle 異動，請使用 <xref:System.Data.OracleClient> 提供者。</span><span class="sxs-lookup"><span data-stu-id="29fb8-113">For an Oracle transaction, use the <xref:System.Data.OracleClient> provider.</span></span> <span data-ttu-id="29fb8-114">此外，還有一個 <xref:System.Data.Common.DbTransaction> 類別可用來撰寫需要交易的提供者獨立程式碼。</span><span class="sxs-lookup"><span data-stu-id="29fb8-114">In addition, there is a <xref:System.Data.Common.DbTransaction> class that is available for writing provider-independent code that requires transactions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="29fb8-115">在伺服器上執行交易時，交易是最有效率的。</span><span class="sxs-lookup"><span data-stu-id="29fb8-115">Transactions are most efficient when they are performed on the server.</span></span> <span data-ttu-id="29fb8-116">如果您使用的 SQL Server 資料庫大量使用明確的異動，請考慮使用 Transact-SQL BEGIN TRANSACTION 陳述式，將它們寫入為預存程序。</span><span class="sxs-lookup"><span data-stu-id="29fb8-116">If you are working with a SQL Server database that makes extensive use of explicit transactions, consider writing them as stored procedures using the Transact-SQL BEGIN TRANSACTION statement.</span></span>
  
## <a name="performing-a-transaction-using-a-single-connection"></a><span data-ttu-id="29fb8-117">使用單一連接執行異動</span><span class="sxs-lookup"><span data-stu-id="29fb8-117">Performing a Transaction Using a Single Connection</span></span>  

 <span data-ttu-id="29fb8-118">在 ADO.NET 中，您可以使用物件來控制交易 `Connection` 。</span><span class="sxs-lookup"><span data-stu-id="29fb8-118">In ADO.NET, you control transactions with the `Connection` object.</span></span> <span data-ttu-id="29fb8-119">您可使用 `BeginTransaction` 方法來起始本機異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-119">You can initiate a local transaction with the `BeginTransaction` method.</span></span> <span data-ttu-id="29fb8-120">開始異動之後，您可使用 `Transaction` 物件的 `Command` 屬性，在該異動中登記命令。</span><span class="sxs-lookup"><span data-stu-id="29fb8-120">Once you have begun a transaction, you can enlist a command in that transaction with the `Transaction` property of a `Command` object.</span></span> <span data-ttu-id="29fb8-121">然後，您可根據異動元件的成敗，來認可或復原對資料來源所做的修改。</span><span class="sxs-lookup"><span data-stu-id="29fb8-121">You can then commit or roll back modifications made at the data source based on the success or failure of the components of the transaction.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="29fb8-122">`EnlistDistributedTransaction` 方法不可用於本機異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-122">The `EnlistDistributedTransaction` method should not be used for a local transaction.</span></span>  
  
 <span data-ttu-id="29fb8-123">交易的範圍僅限於連接。</span><span class="sxs-lookup"><span data-stu-id="29fb8-123">The scope of the transaction is limited to the connection.</span></span> <span data-ttu-id="29fb8-124">下列範例執行由 `try` 區塊中的兩個單獨命令所組成的明確異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-124">The following example performs an explicit transaction that consists of two separate commands in the `try` block.</span></span> <span data-ttu-id="29fb8-125">這些命令會針對 AdventureWorks SQL Server 範例資料庫中的 Production.scrapreason 資料表執行 INSERT 語句，如果未擲回任何例外狀況，則會認可。</span><span class="sxs-lookup"><span data-stu-id="29fb8-125">The commands execute INSERT statements against the Production.ScrapReason table in the AdventureWorks SQL Server sample database, which are committed if no exceptions are thrown.</span></span> <span data-ttu-id="29fb8-126">如果擲回例外狀況，`catch` 區塊中的程式碼便會復原交易。</span><span class="sxs-lookup"><span data-stu-id="29fb8-126">The code in the `catch` block rolls back the transaction if an exception is thrown.</span></span> <span data-ttu-id="29fb8-127">如果異動在完成之前遭到中止或連接關閉，則會自動復原該異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-127">If the transaction is aborted or the connection is closed before the transaction has completed, it is automatically rolled back.</span></span>  
  
## <a name="example"></a><span data-ttu-id="29fb8-128">範例</span><span class="sxs-lookup"><span data-stu-id="29fb8-128">Example</span></span>  

 <span data-ttu-id="29fb8-129">請遵循下列步驟來執行異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-129">Follow these steps to perform a transaction.</span></span>  
  
1. <span data-ttu-id="29fb8-130">呼叫 <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 物件的 <xref:System.Data.SqlClient.SqlConnection> 方法，來標記交易的開始。</span><span class="sxs-lookup"><span data-stu-id="29fb8-130">Call the <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> method of the <xref:System.Data.SqlClient.SqlConnection> object to mark the start of the transaction.</span></span> <span data-ttu-id="29fb8-131"><xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法會將參考傳回給交易。</span><span class="sxs-lookup"><span data-stu-id="29fb8-131">The <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> method returns a reference to the transaction.</span></span> <span data-ttu-id="29fb8-132">此參考會指派給登記在交易中的 <xref:System.Data.SqlClient.SqlCommand> 物件。</span><span class="sxs-lookup"><span data-stu-id="29fb8-132">This reference is assigned to the <xref:System.Data.SqlClient.SqlCommand> objects that are enlisted in the transaction.</span></span>  
  
2. <span data-ttu-id="29fb8-133">將 `Transaction` 物件指派給要執行之 <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> 的 <xref:System.Data.SqlClient.SqlCommand> 屬性。</span><span class="sxs-lookup"><span data-stu-id="29fb8-133">Assign the `Transaction` object to the <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> property of the <xref:System.Data.SqlClient.SqlCommand> to be executed.</span></span> <span data-ttu-id="29fb8-134">如果在有異動正在作用中的連接上執行命令，且 `Transaction` 物件尚未指派給 `Transaction` 物件的 `Command` 屬性，便會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="29fb8-134">If a command is executed on a connection with an active transaction, and the `Transaction` object has not been assigned to the `Transaction` property of the `Command` object, an exception is thrown.</span></span>  
  
3. <span data-ttu-id="29fb8-135">執行必要的命令。</span><span class="sxs-lookup"><span data-stu-id="29fb8-135">Execute the required commands.</span></span>  
  
4. <span data-ttu-id="29fb8-136">呼叫 <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> 物件的 <xref:System.Data.SqlClient.SqlTransaction> 方法來完成交易，或呼叫 <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> 方法來中止交易。</span><span class="sxs-lookup"><span data-stu-id="29fb8-136">Call the <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> method of the <xref:System.Data.SqlClient.SqlTransaction> object to complete the transaction, or call the <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> method to end the transaction.</span></span> <span data-ttu-id="29fb8-137">如果在執行 <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> 或 <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> 方法之前關閉或處置連接，則會復原異動。</span><span class="sxs-lookup"><span data-stu-id="29fb8-137">If the connection is closed or disposed before either the <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> or <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> methods have been executed, the transaction is rolled back.</span></span>  
  
 <span data-ttu-id="29fb8-138">下列程式碼範例示範使用 ADO.NET 搭配 Microsoft SQL Server 的交易邏輯。</span><span class="sxs-lookup"><span data-stu-id="29fb8-138">The following code example demonstrates transactional logic using ADO.NET with Microsoft SQL Server.</span></span>  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="29fb8-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="29fb8-139">See also</span></span>

- [<span data-ttu-id="29fb8-140">異動和並行存取</span><span class="sxs-lookup"><span data-stu-id="29fb8-140">Transactions and Concurrency</span></span>](transactions-and-concurrency.md)
- [<span data-ttu-id="29fb8-141">分散式交易</span><span class="sxs-lookup"><span data-stu-id="29fb8-141">Distributed Transactions</span></span>](distributed-transactions.md)
- [<span data-ttu-id="29fb8-142">System.Transactions 與 SQL Server 整合</span><span class="sxs-lookup"><span data-stu-id="29fb8-142">System.Transactions Integration with SQL Server</span></span>](system-transactions-integration-with-sql-server.md)
- <span data-ttu-id="29fb8-143">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="29fb8-143">[ADO.NET Overview](ado-net-overview.md)</span></span>

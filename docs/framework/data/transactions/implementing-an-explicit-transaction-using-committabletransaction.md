---
title: 使用 CommittableTransaction 實作明確交易
description: 使用 .NET 中的 CommittableTransaction 類別，來執行明確的交易。 此類別提供明確的方式讓應用程式使用交易。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 29efe5e5-897b-46c2-a35f-e599a273acc8
ms.openlocfilehash: 40001422e665a7dda3fb938c8d57860909525404
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141987"
---
# <a name="implementing-an-explicit-transaction-using-committabletransaction"></a><span data-ttu-id="0777b-104">使用 CommittableTransaction 實作明確交易</span><span class="sxs-lookup"><span data-stu-id="0777b-104">Implementing an Explicit Transaction using CommittableTransaction</span></span>
<span data-ttu-id="0777b-105"><xref:System.Transactions.CommittableTransaction> 類別為應用程式提供使用交易的明確方式，而非隱含地使用 <xref:System.Transactions.TransactionScope> 類別。</span><span class="sxs-lookup"><span data-stu-id="0777b-105">The <xref:System.Transactions.CommittableTransaction> class provides an explicit way for applications to use a transaction, as opposed to using the <xref:System.Transactions.TransactionScope> class implicitly.</span></span> <span data-ttu-id="0777b-106">這個方法對想要跨多個函式呼叫或多個執行緒呼叫來使用相同交易的應用程式也很有用處。</span><span class="sxs-lookup"><span data-stu-id="0777b-106">It is useful for applications that want to use the same transaction across multiple function calls or multiple thread calls.</span></span> <span data-ttu-id="0777b-107">與 <xref:System.Transactions.TransactionScope> 類別不同的是，應用程式寫入器需要特別呼叫 <xref:System.Transactions.CommittableTransaction.Commit%2A> 和 <xref:System.Transactions.Transaction.Rollback%2A> 方法，才能認可或中止交易。</span><span class="sxs-lookup"><span data-stu-id="0777b-107">Unlike the <xref:System.Transactions.TransactionScope> class, the application writer needs to specifically call the <xref:System.Transactions.CommittableTransaction.Commit%2A> and <xref:System.Transactions.Transaction.Rollback%2A> methods in order to commit or abort the transaction.</span></span>  
  
## <a name="overview-of-the-committabletransaction-class"></a><span data-ttu-id="0777b-108">CommittableTransaction 類別的概觀</span><span class="sxs-lookup"><span data-stu-id="0777b-108">Overview of the CommittableTransaction class</span></span>  
 <span data-ttu-id="0777b-109"><xref:System.Transactions.CommittableTransaction> 類別係衍生自 <xref:System.Transactions.Transaction> 類別，因此可提供後者所有功能。</span><span class="sxs-lookup"><span data-stu-id="0777b-109">The <xref:System.Transactions.CommittableTransaction> class derives from the <xref:System.Transactions.Transaction> class, therefore providing all the functionality of the latter.</span></span> <span data-ttu-id="0777b-110"><xref:System.Transactions.Transaction.Rollback%2A> 類別上的 <xref:System.Transactions.Transaction> 方法特別有用，因為它同時能用來復原 <xref:System.Transactions.CommittableTransaction> 物件。</span><span class="sxs-lookup"><span data-stu-id="0777b-110">Specifically useful is the <xref:System.Transactions.Transaction.Rollback%2A> method on the <xref:System.Transactions.Transaction> class that can also be used to rollback a <xref:System.Transactions.CommittableTransaction> object.</span></span>  
  
 <span data-ttu-id="0777b-111"><xref:System.Transactions.Transaction> 類別與 <xref:System.Transactions.CommittableTransaction> 類別類似，但是不會提供 `Commit` 方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-111">The  <xref:System.Transactions.Transaction> class is similar to the <xref:System.Transactions.CommittableTransaction> class but does not offer a `Commit` method.</span></span> <span data-ttu-id="0777b-112">它能讓您在控制交易認可時間的同時，將交易物件 (或其複製品) 傳遞給其他方法 (可能透過其他執行緒)。</span><span class="sxs-lookup"><span data-stu-id="0777b-112">This enables you to pass the transaction object (or clones of it) to other methods (potentially on other threads) while still controlling when the transaction is committed.</span></span> <span data-ttu-id="0777b-113">呼叫的程式碼可以登記並投票給交易，但是只有 <xref:System.Transactions.CommittableTransaction> 物件的建立者有能力認可交易。</span><span class="sxs-lookup"><span data-stu-id="0777b-113">The called code is able to enlist and vote on the transaction, but only the creator of the <xref:System.Transactions.CommittableTransaction> object has the ability to commit the transaction.</span></span>  
  
 <span data-ttu-id="0777b-114">使用 <xref:System.Transactions.CommittableTransaction> 類別時，您應該注意下列事項。</span><span class="sxs-lookup"><span data-stu-id="0777b-114">You should note the followings when working with the <xref:System.Transactions.CommittableTransaction> class,</span></span>  
  
- <span data-ttu-id="0777b-115">建立 <xref:System.Transactions.CommittableTransaction> 交易不會設定環境交易。</span><span class="sxs-lookup"><span data-stu-id="0777b-115">Creating a <xref:System.Transactions.CommittableTransaction> transaction does not set the ambient transaction.</span></span> <span data-ttu-id="0777b-116">您需要特別設定及重設環境交易，以確保資源管理員在適當時機，於正確的交易內容下作業。</span><span class="sxs-lookup"><span data-stu-id="0777b-116">You need to specifically set and reset the ambient transaction, to ensure that resource managers operate under the right transaction context when appropriate.</span></span> <span data-ttu-id="0777b-117">您可以在全域 <xref:System.Transactions.Transaction.Current%2A> 物件上設定靜態 <xref:System.Transactions.Transaction> 屬性，來設定目前的環境交易。</span><span class="sxs-lookup"><span data-stu-id="0777b-117">The way to set the current ambient transaction is by setting the static <xref:System.Transactions.Transaction.Current%2A> property on the global <xref:System.Transactions.Transaction> object.</span></span>  
  
- <span data-ttu-id="0777b-118">您無法重複使用 <xref:System.Transactions.CommittableTransaction> 物件，</span><span class="sxs-lookup"><span data-stu-id="0777b-118">A <xref:System.Transactions.CommittableTransaction> object cannot be reused.</span></span> <span data-ttu-id="0777b-119">一旦 <xref:System.Transactions.CommittableTransaction> 物件已經認可或復原，將無法重複使用在交易中。</span><span class="sxs-lookup"><span data-stu-id="0777b-119">Once a <xref:System.Transactions.CommittableTransaction> object has been committed or rolled back, it cannot be used again in a transaction.</span></span> <span data-ttu-id="0777b-120">亦即，您無法將其設為目前的環境交易內容。</span><span class="sxs-lookup"><span data-stu-id="0777b-120">That is, it cannot be set as the current ambient transaction context.</span></span>  
  
## <a name="creating-a-committabletransaction"></a><span data-ttu-id="0777b-121">建立 CommittableTransaction</span><span class="sxs-lookup"><span data-stu-id="0777b-121">Creating a CommittableTransaction</span></span>  
 <span data-ttu-id="0777b-122">下列範例會建立新的 <xref:System.Transactions.CommittableTransaction> 並加以認可。</span><span class="sxs-lookup"><span data-stu-id="0777b-122">The following sample creates a new <xref:System.Transactions.CommittableTransaction> and commits it.</span></span>  
  
 [!code-csharp[Tx_CommittableTx#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_committabletx/cs/committabletxwithsql.cs#1)]
 [!code-vb[Tx_CommittableTx#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_committabletx/vb/committabletxwithsql.vb#1)]  
  
 <span data-ttu-id="0777b-123">建立 <xref:System.Transactions.CommittableTransaction> 執行個體不會自動設定環境交易內容。</span><span class="sxs-lookup"><span data-stu-id="0777b-123">Creating an instance of <xref:System.Transactions.CommittableTransaction> does not automatically set the ambient transaction context.</span></span> <span data-ttu-id="0777b-124">因此，資源管理員上的任何作業都不是該交易的一部分。</span><span class="sxs-lookup"><span data-stu-id="0777b-124">Therefore, any operation on a resource manager is not part of that transaction.</span></span> <span data-ttu-id="0777b-125">全域 <xref:System.Transactions.Transaction.Current%2A> 物件上的靜態 <xref:System.Transactions.Transaction> 屬性是用來設定或擷取環境交易，應用程式必須手動加以設定以確保資源管理員可以參與交易。</span><span class="sxs-lookup"><span data-stu-id="0777b-125">The static <xref:System.Transactions.Transaction.Current%2A> property on the global <xref:System.Transactions.Transaction> object is used to set or retrieve the ambient transaction and the application must manually set it to ensure that resource managers can participate in the transaction.</span></span> <span data-ttu-id="0777b-126">儲存舊有的環境交易並在 <xref:System.Transactions.CommittableTransaction> 物件使用完畢時將其還原是很好的使用習慣。</span><span class="sxs-lookup"><span data-stu-id="0777b-126">It is also a good practice to save the old ambient transaction and restore it when you finish using the <xref:System.Transactions.CommittableTransaction> object.</span></span>  
  
 <span data-ttu-id="0777b-127">為了認可交易，您需要明確地呼叫 <xref:System.Transactions.CommittableTransaction.Commit%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-127">To commit the transaction, you need to explicitly call the <xref:System.Transactions.CommittableTransaction.Commit%2A> method.</span></span> <span data-ttu-id="0777b-128">若要復原交易，您應該呼叫 <xref:System.Transactions.Transaction.Rollback%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-128">For rolling back a transaction, you should call the <xref:System.Transactions.Transaction.Rollback%2A> method.</span></span> <span data-ttu-id="0777b-129">在已認可或復原 <xref:System.Transactions.CommittableTransaction> 之前，所有與該交易有關的資源都會保持鎖定，這點請您特別注意。</span><span class="sxs-lookup"><span data-stu-id="0777b-129">It is important to note that until a <xref:System.Transactions.CommittableTransaction> has been committed or rolled back, all the resources involved in that transaction are still locked.</span></span>  
  
 <span data-ttu-id="0777b-130"><xref:System.Transactions.CommittableTransaction> 物件可以供多個函式呼叫與執行緒使用。</span><span class="sxs-lookup"><span data-stu-id="0777b-130">A <xref:System.Transactions.CommittableTransaction> object can be used across function calls and threads.</span></span> <span data-ttu-id="0777b-131">然而，應用程式開發人員有權決定是否要在發生失敗時，處理例外狀況並特別呼叫 <xref:System.Transactions.Transaction.Rollback%28System.Exception%29> 方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-131">However, it is up to the application developer to handle exceptions and specifically call the <xref:System.Transactions.Transaction.Rollback%28System.Exception%29> method in case of failures.</span></span>  
  
## <a name="asynchronous-commit"></a><span data-ttu-id="0777b-132">非同步認可</span><span class="sxs-lookup"><span data-stu-id="0777b-132">Asynchronous Commit</span></span>  
 <span data-ttu-id="0777b-133"><xref:System.Transactions.CommittableTransaction> 類別同時提供您以非同步方式認可交易的機制。</span><span class="sxs-lookup"><span data-stu-id="0777b-133">The <xref:System.Transactions.CommittableTransaction> class also provides a mechanism for committing a transaction asynchronously.</span></span> <span data-ttu-id="0777b-134">交易認可作業會花掉很多時間，因為此作業牽涉到多個資料庫存取，而且可能會讓網路產生延遲現象。</span><span class="sxs-lookup"><span data-stu-id="0777b-134">A transaction commit can take substantial time, as it might involve multiple database access and possible network latency.</span></span> <span data-ttu-id="0777b-135">當您想要避免高輸送量應用程式中出現死結 (Deadlock) 的情況時，可以使用非同步認可方式來儘速完成交易作業，並以背景工作方式來執行認可作業。</span><span class="sxs-lookup"><span data-stu-id="0777b-135">When you want to avoid deadlocks in high throughput applications, you can use asynchronous commit to finish the transactional work as soon as possible, and run the commit operation as a background task.</span></span> <span data-ttu-id="0777b-136"><xref:System.Transactions.CommittableTransaction.BeginCommit%2A> 類別的 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 與 <xref:System.Transactions.CommittableTransaction> 方法可讓您這麼做。</span><span class="sxs-lookup"><span data-stu-id="0777b-136">The <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> and <xref:System.Transactions.CommittableTransaction.EndCommit%2A> methods of the <xref:System.Transactions.CommittableTransaction> class allow you to do so.</span></span>  
  
 <span data-ttu-id="0777b-137">您可以呼叫 <xref:System.Transactions.CommittableTransaction.BeginCommit%2A>，將認可停頓分配給來自執行緒集區的執行緒。</span><span class="sxs-lookup"><span data-stu-id="0777b-137">You can call <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> to dispatch the commit holdup to a thread from the thread pool.</span></span> <span data-ttu-id="0777b-138">您也可以呼叫 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 來判斷交易是否已實際認可。</span><span class="sxs-lookup"><span data-stu-id="0777b-138">You can also call <xref:System.Transactions.CommittableTransaction.EndCommit%2A> to determine if the transaction has actually been committed.</span></span> <span data-ttu-id="0777b-139">如果交易因為某種原因而失敗，則 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 會引發交易例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0777b-139">If the transaction failed to commit for whatever reason, <xref:System.Transactions.CommittableTransaction.EndCommit%2A> raises a transaction exception.</span></span> <span data-ttu-id="0777b-140">如果交易在呼叫 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 時尚未認可，則呼叫端會在交易認可或中止之前一直保持封鎖狀態。</span><span class="sxs-lookup"><span data-stu-id="0777b-140">If the transaction is not yet committed by the time <xref:System.Transactions.CommittableTransaction.EndCommit%2A> is called, the caller is blocked until the transaction is committed or aborted.</span></span>  
  
 <span data-ttu-id="0777b-141">進行非同步認可的最簡便方式，就是提供可在完成認可時加以呼叫的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-141">The easiest way to do an asynchronous commit is by providing a callback method, to be called when committing is finished.</span></span> <span data-ttu-id="0777b-142">但是，您必須在用於叫用呼叫的原始 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 物件上呼叫 <xref:System.Transactions.CommittableTransaction> 方法。</span><span class="sxs-lookup"><span data-stu-id="0777b-142">However, you must call the <xref:System.Transactions.CommittableTransaction.EndCommit%2A> method on the original <xref:System.Transactions.CommittableTransaction> object used to invoke the call.</span></span> <span data-ttu-id="0777b-143">若要取得該物件，您可以向下轉換回呼方法的*IAsyncResult*參數，因為類別會實作為 <xref:System.Transactions.CommittableTransaction> <xref:System.IAsyncResult> 類別。</span><span class="sxs-lookup"><span data-stu-id="0777b-143">To obtain that object, you can downcast the *IAsyncResult* parameter of the callback method, since the <xref:System.Transactions.CommittableTransaction> class implements <xref:System.IAsyncResult> class.</span></span>  
  
 <span data-ttu-id="0777b-144">下列範例示範如何完成非同步認可。</span><span class="sxs-lookup"><span data-stu-id="0777b-144">The following example shows how an asynchronous commit can be done.</span></span>  
  
```csharp  
public void DoTransactionalWork()  
{  
     Transaction oldAmbient = Transaction.Current;  
     CommittableTransaction committableTransaction = new CommittableTransaction();  
     Transaction.Current = committableTransaction;  
  
     try  
     {  
          /* Perform transactional work here */  
          // No errors - commit transaction asynchronously  
          committableTransaction.BeginCommit(OnCommitted,null);  
     }  
     finally  
     {  
          //Restore the ambient transaction
          Transaction.Current = oldAmbient;  
     }  
}  
void OnCommitted(IAsyncResult asyncResult)  
{  
     CommittableTransaction committableTransaction;  
     committableTransaction = asyncResult as CommittableTransaction;
     Debug.Assert(committableTransaction != null);  
     try  
     {  
          using(committableTransaction)  
          {  
               committableTransaction.EndCommit(asyncResult);  
          }  
     }  
     catch(TransactionException e)  
     {  
          //Handle the failure to commit  
     }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="0777b-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0777b-145">See also</span></span>

- [<span data-ttu-id="0777b-146">使用異動範圍實作隱含異動</span><span class="sxs-lookup"><span data-stu-id="0777b-146">Implementing an Implicit Transaction using Transaction Scope</span></span>](implementing-an-implicit-transaction-using-transaction-scope.md)
- [<span data-ttu-id="0777b-147">交易處理</span><span class="sxs-lookup"><span data-stu-id="0777b-147">Transaction Processing</span></span>](index.md)

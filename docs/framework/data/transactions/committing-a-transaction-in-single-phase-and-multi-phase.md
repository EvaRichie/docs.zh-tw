---
title: 在單一階段和多重階段中認可交易
description: 閱讀有關在 .NET 中的一或兩個階段認可交易的資訊。 如果交易牽涉到一個以上的資源，就必須執行兩階段認可（2PC）。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 694ea153-e4db-41ae-96ac-9ac66dcb69a9
ms.openlocfilehash: 2f4486998f347bf1db6d22433e6e48b553609c18
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141820"
---
# <a name="committing-a-transaction-in-single-phase-and-multi-phase"></a><span data-ttu-id="96da6-104">在單一階段和多重階段中認可交易</span><span class="sxs-lookup"><span data-stu-id="96da6-104">Committing a Transaction in Single-Phase and Multi-Phase</span></span>
<span data-ttu-id="96da6-105">交易所使用的每項資源都會受到資源管理員 (RM) 的管理，而這些資源管理員在採取行動時必須經過交易管理員 (TM) 的協調。</span><span class="sxs-lookup"><span data-stu-id="96da6-105">Each resource used in a transaction is managed by a resource manager (RM), whose actions are coordinated by a transaction manager (TM).</span></span> <span data-ttu-id="96da6-106">在[交易中將資源登記為參與者](enlisting-resources-as-participants-in-a-transaction.md)主題會討論如何在交易中登記資源（或多個資源）。</span><span class="sxs-lookup"><span data-stu-id="96da6-106">The [Enlisting Resources as Participants in a Transaction](enlisting-resources-as-participants-in-a-transaction.md) topic discusses how a resource (or multiple resources) can be enlisted in a transaction.</span></span> <span data-ttu-id="96da6-107">本主題討論如何在眾多登記的資源中協調要認可的交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-107">This topic discusses how transaction commitment can be coordinated among enlisted resources.</span></span>  
  
 <span data-ttu-id="96da6-108">交易結束時，應用程式便要求認可或回復交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-108">At the end of the transaction, the application requests the transaction to be either committed or rolled back.</span></span> <span data-ttu-id="96da6-109">交易管理員必須消除某些資源管理員投票決定認可，而其他資源管理員卻投票決定復原交易之類的風險。</span><span class="sxs-lookup"><span data-stu-id="96da6-109">The transaction manager must eliminate risks like some resource managers voting to commit while others voting to roll back the transaction.</span></span>  
  
 <span data-ttu-id="96da6-110">如果您的交易涉及一個以上的資源，則您必須執行兩階段交易認可 (2PC)。</span><span class="sxs-lookup"><span data-stu-id="96da6-110">If your transaction involves more than one resource, you must perform a two-phase commit (2PC).</span></span> <span data-ttu-id="96da6-111">兩階段交易認可通訊協定 (準備階段與認可階段) 可確保當交易結束時，對全部資源的所有變更都能全部經過認可，或是全部復原回來。</span><span class="sxs-lookup"><span data-stu-id="96da6-111">The two-phase commit protocol (the prepare phase and the commit phase) ensures that when the transaction ends, all changes to all resources are either totally committed or fully rolled back.</span></span> <span data-ttu-id="96da6-112">接著所有參與者都會收到最後結果的通知。</span><span class="sxs-lookup"><span data-stu-id="96da6-112">All the participants are then informed of the final result.</span></span> <span data-ttu-id="96da6-113">如需兩階段認可通訊協定的詳細討論，請參閱「*交易處理：資料管理系統中的 Morgan Kaufmann 系列） ISBN： 1558601902*」的「Jim 灰色」一書。</span><span class="sxs-lookup"><span data-stu-id="96da6-113">For a detailed discussion of the two-phase commit protocol, please consult the book "*Transaction Processing : Concepts and Techniques (Morgan Kaufmann Series in Data Management Systems) ISBN:1558601902*" by Jim Gray.</span></span>  
  
 <span data-ttu-id="96da6-114">您也可以藉由參與單一階段交易認可通訊協定來最佳化您的交易效能。</span><span class="sxs-lookup"><span data-stu-id="96da6-114">You can also optimize your transaction's performance by taking part in the Single Phase Commit protocol.</span></span> <span data-ttu-id="96da6-115">如需詳細資訊，請參閱[使用單一階段交易認可和可提升單一階段通知的優化](optimization-spc-and-promotable-spn.md)。</span><span class="sxs-lookup"><span data-stu-id="96da6-115">For more information, see [Optimization using Single Phase Commit and Promotable Single Phase Notification](optimization-spc-and-promotable-spn.md).</span></span>  
  
 <span data-ttu-id="96da6-116">如果您只是想要知道交易的結果，但不想參與投票，則應該註冊 <xref:System.Transactions.Transaction.TransactionCompleted> 事件。</span><span class="sxs-lookup"><span data-stu-id="96da6-116">If you just want to be informed of a transaction's outcome, and do not want to participate in voting, you should register for the <xref:System.Transactions.Transaction.TransactionCompleted> event.</span></span>  
  
## <a name="two-phase-commit-2pc"></a><span data-ttu-id="96da6-117">兩階段交易認可 (2PC)</span><span class="sxs-lookup"><span data-stu-id="96da6-117">Two-phase Commit (2PC)</span></span>  
 <span data-ttu-id="96da6-118">在第一個交易階段，交易管理員會查詢每個資源，決定是否應該認可或復原交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-118">In the first transaction phase, the transaction manager queries each resource to determine whether a transaction should be committed or rolled back.</span></span> <span data-ttu-id="96da6-119">在第二個交易階段，交易管理員會將其查詢結果通知每個資源，讓資源執行任何必要的清除作業。</span><span class="sxs-lookup"><span data-stu-id="96da6-119">In the second transaction phase, the transaction manager notifies each resource of the outcome of its queries, allowing it to perform any necessary cleanup.</span></span>  
  
 <span data-ttu-id="96da6-120">為了參與這種交易類型，資源管理員必須實作 <xref:System.Transactions.IEnlistmentNotification> 介面，以便在 2PC 期間提供由 TM 所呼叫的方法做為告知項目。</span><span class="sxs-lookup"><span data-stu-id="96da6-120">To participate in this kind of transaction, a resource manager must implement the <xref:System.Transactions.IEnlistmentNotification> interface, which provides methods that are called by the TM as notifications during a 2PC.</span></span>  <span data-ttu-id="96da6-121">下列範例將說明此類實作。</span><span class="sxs-lookup"><span data-stu-id="96da6-121">The following sample shows an example of such implementation.</span></span>  
  
 [!code-csharp[Tx_Enlist#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_enlist/cs/enlist.cs#2)]
 [!code-vb[Tx_Enlist#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_enlist/vb/enlist.vb#2)]  
  
### <a name="prepare-phase-phase-1"></a><span data-ttu-id="96da6-122">準備階段 (第一階段)</span><span class="sxs-lookup"><span data-stu-id="96da6-122">Prepare phase (Phase 1)</span></span>  
 <span data-ttu-id="96da6-123">在收到來自應用程式的 <xref:System.Transactions.CommittableTransaction.Commit%2A> 要求之後，交易管理員會呼叫每個登記資源上的 <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> 方法來開始所有登記參與者的準備階段，以取得每個資源對交易的投票。</span><span class="sxs-lookup"><span data-stu-id="96da6-123">Upon receiving a <xref:System.Transactions.CommittableTransaction.Commit%2A> request from the application, the transaction manager begins the Prepare phase of all the enlisted participants by calling the <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> method on each enlisted resource, in order to obtain each resource's vote on the transaction.</span></span>  
  
 <span data-ttu-id="96da6-124">負責實作 <xref:System.Transactions.IEnlistmentNotification> 介面的資源管理員應該先實作 <xref:System.Transactions.IEnlistmentNotification.Prepare%28System.Transactions.PreparingEnlistment%29> 方法，如下列簡單範例所示。</span><span class="sxs-lookup"><span data-stu-id="96da6-124">Your resource manager that implements the <xref:System.Transactions.IEnlistmentNotification> interface should first implement the <xref:System.Transactions.IEnlistmentNotification.Prepare%28System.Transactions.PreparingEnlistment%29> method as the following simple example shows.</span></span>  
  
```csharp
public void Prepare(PreparingEnlistment preparingEnlistment)  
{  
     Console.WriteLine("Prepare notification received");  
     //Perform work  
  
     Console.Write("reply with prepared? [Y|N] ");  
     c = Console.ReadKey();  
     Console.WriteLine();  
  
     //If work finished correctly, reply with prepared  
     if ((c.KeyChar == 'Y') || (c.KeyChar == 'y'))  
     {  
          preparingEnlistment.Prepared();  
          break;  
     }  
  
     // otherwise, do a ForceRollback  
     else if ((c.KeyChar == 'N') || (c.KeyChar == 'n'))  
     {  
          preparingEnlistment.ForceRollback();  
          break;  
     }  
}  
```  
  
 <span data-ttu-id="96da6-125">當永久性資源管理員收到此呼叫，它應該將交易的復原資訊 (可藉由擷取 <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> 屬性而得) 以及完成交易認可所需的任何資訊記錄下來。</span><span class="sxs-lookup"><span data-stu-id="96da6-125">When the durable resource manager receives this call, it should log the transaction's recovery information (available by retrieving the <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> property) and whatever information is necessary to complete the transaction on commit.</span></span> <span data-ttu-id="96da6-126">由於 RM 可在工作執行緒上進行這項作業，因此您不需要透過 <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> 方法來做這件事。</span><span class="sxs-lookup"><span data-stu-id="96da6-126">This does not need to be performed within the <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> method because the RM can do this on a worker thread.</span></span>  
  
 <span data-ttu-id="96da6-127">當 RM 完整準備工作時，就會呼叫 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 或 <xref:System.Transactions.PreparingEnlistment.ForceRollback%2A> 方法來投票認可或復原交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-127">When the RM has finished its prepare work, it should vote to commit or roll back by calling the <xref:System.Transactions.PreparingEnlistment.Prepared%2A> or <xref:System.Transactions.PreparingEnlistment.ForceRollback%2A> method.</span></span> <span data-ttu-id="96da6-128">請注意，<xref:System.Transactions.PreparingEnlistment> 類別會繼承來自 <xref:System.Transactions.Enlistment.Done%2A> 類別的 <xref:System.Transactions.Enlistment> 方法。</span><span class="sxs-lookup"><span data-stu-id="96da6-128">Notice that the <xref:System.Transactions.PreparingEnlistment> class inherits a <xref:System.Transactions.Enlistment.Done%2A> method from the <xref:System.Transactions.Enlistment> class.</span></span> <span data-ttu-id="96da6-129">如果您在準備階段於 <xref:System.Transactions.PreparingEnlistment> 回呼上呼叫此方法，則它會通知 TM 已登記為唯讀 (亦即，資源管理員可以讀取但無法更新交易保護的資料) 而且 RM 也將無法繼續收到來自交易管理員有關第二階段交易結果的任何告知。</span><span class="sxs-lookup"><span data-stu-id="96da6-129">If you call this method on the <xref:System.Transactions.PreparingEnlistment> callback during the Prepare phase, it informs the TM that it is a Read-Only enlistment (that is, resource managers that can read but cannot update transaction-protected data) and the RM receives no further notifications from the transaction manager as to the outcome of the transaction in phase 2.</span></span>  
  
 <span data-ttu-id="96da6-130">當所有資源管理員都投票選擇 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 時，應用程式將被告知已經成功認可交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-130">The application is told of the successful commitment of the transaction after all the resource managers vote <xref:System.Transactions.PreparingEnlistment.Prepared%2A>.</span></span>  
  
### <a name="commit-phase-phase-2"></a><span data-ttu-id="96da6-131">交易階段 (第二階段)</span><span class="sxs-lookup"><span data-stu-id="96da6-131">Commit phase (Phase 2)</span></span>  
 <span data-ttu-id="96da6-132">在交易的第二階段，如果交易管理員收到來自所有資源管理員的準備成功消息 (所有資源管理員在第一階段結束時都叫用了 <xref:System.Transactions.PreparingEnlistment.Prepared%2A>)，則它會為每個資源管理員叫用 <xref:System.Transactions.IEnlistmentNotification.Commit%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="96da6-132">In the second phase of the transaction, if the transaction manager receives successful prepares from all the resource managers (all the resource managers have invoked <xref:System.Transactions.PreparingEnlistment.Prepared%2A> at the end of phase 1), it invokes the <xref:System.Transactions.IEnlistmentNotification.Commit%2A> method for each resource manager.</span></span> <span data-ttu-id="96da6-133">資源管理員會接著進行永久性變更並完成交易認可動作。</span><span class="sxs-lookup"><span data-stu-id="96da6-133">The resource managers can then make the changes durable and complete the commit.</span></span>  
  
 <span data-ttu-id="96da6-134">如果有任何資源管理員在第一階段中報告準備失敗，則交易管理員會為每個資源管理員叫用 <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> 方法，並向應用程式指出交易認可失敗之處。</span><span class="sxs-lookup"><span data-stu-id="96da6-134">If any resource manager reported a failure to prepare in phase 1, the transaction manager invokes the <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> method for each resource manager and indicates the failure of the commit to the application.</span></span>  
  
 <span data-ttu-id="96da6-135">因此，您的資源管理員應該實作下列方法。</span><span class="sxs-lookup"><span data-stu-id="96da6-135">Thus, your resource manager should implement the following methods.</span></span>  
  
```csharp
public void Commit (Enlistment enlistment)  
{  
     // Do any work necessary when commit notification is received  
  
     // Declare done on the enlistment  
     enlistment.Done();  
}  
  
public void Rollback (Enlistment enlistment)  
{  
     // Do any work necessary when rollback notification is received  
  
     // Declare done on the enlistment
     enlistment.Done();
}  
```  
  
 <span data-ttu-id="96da6-136">RM 應該依據告知型別執行任何必要的工作以完成交易，並呼叫 <xref:System.Transactions.Enlistment.Done%2A> 參數上的 <xref:System.Transactions.Enlistment> 方法，告知 TM 已完成交易。</span><span class="sxs-lookup"><span data-stu-id="96da6-136">The RM should perform any work necessary to finish the transaction based on the notification type, and inform the TM that it has finished by calling <xref:System.Transactions.Enlistment.Done%2A> method on the <xref:System.Transactions.Enlistment> parameter.</span></span> <span data-ttu-id="96da6-137">這項工作可在工作執行緒上完成。</span><span class="sxs-lookup"><span data-stu-id="96da6-137">This work can be done on a worker thread.</span></span> <span data-ttu-id="96da6-138">請注意，第二階段告知會發生並內嵌在第一階段中呼叫 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 方法的同一個執行緒上。</span><span class="sxs-lookup"><span data-stu-id="96da6-138">Note that the phase 2 notifications can happen inline on the same thread that called the <xref:System.Transactions.PreparingEnlistment.Prepared%2A> method in phase 1.</span></span> <span data-ttu-id="96da6-139">因此，當您預期在收到第二階段告知之前會完成 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 呼叫時，請勿在此呼叫之後執行任何工作 (例如，釋放鎖定)。</span><span class="sxs-lookup"><span data-stu-id="96da6-139">As such, you should not do any work after the <xref:System.Transactions.PreparingEnlistment.Prepared%2A> call (for example, releasing locks) that you would expect to have completed before receiving the phase 2 notifications.</span></span>  
  
### <a name="implementing-indoubt"></a><span data-ttu-id="96da6-140">實作 InDoubt</span><span class="sxs-lookup"><span data-stu-id="96da6-140">Implementing InDoubt</span></span>  
 <span data-ttu-id="96da6-141">最後，您應該為變動性資源管理員實作 <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="96da6-141">Finally, you should implement the <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A> method for the volatile resource manager.</span></span> <span data-ttu-id="96da6-142">如果交易管理員失去與一或多個參與者的聯繫而無法得知其個別狀態時，就會呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="96da6-142">This method is called if the transaction manager loses contact with one or more participants, so their status is unknown.</span></span> <span data-ttu-id="96da6-143">如果發生這種情況，不管是否有任何交易參與者仍舊維持在不一致的狀態，您都應該將此事實記錄下來以便稍後進一步探究原因。</span><span class="sxs-lookup"><span data-stu-id="96da6-143">If this occurs, you should log this fact so that you can investigate later whether any of the transaction participants has been left in an inconsistent state.</span></span>  
  
```csharp
public void InDoubt (Enlistment enlistment)  
{  
     // log this  
     enlistment.Done();  
}  
```  
  
## <a name="single-phase-commit-optimization"></a><span data-ttu-id="96da6-144">單一階段交易認可最佳化</span><span class="sxs-lookup"><span data-stu-id="96da6-144">Single Phase Commit Optimization</span></span>  
 <span data-ttu-id="96da6-145">在執行階段使用單一階段交易認可通訊協定會比較有效率，因為所有的更新不需要任何個別的協調作業就可完成。</span><span class="sxs-lookup"><span data-stu-id="96da6-145">The Single Phase Commit protocol is more efficient at run time because all updates are done without any explicit coordination.</span></span> <span data-ttu-id="96da6-146">如需此通訊協定的詳細資訊，請參閱[使用單一階段認可和可提升單一階段通知的優化](optimization-spc-and-promotable-spn.md)。</span><span class="sxs-lookup"><span data-stu-id="96da6-146">For more information on this protocol, see [Optimization using Single Phase Commit and Promotable Single Phase Notification](optimization-spc-and-promotable-spn.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="96da6-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="96da6-147">See also</span></span>

- [<span data-ttu-id="96da6-148">使用單一階段認可和可提升單一階段通知進行最佳化</span><span class="sxs-lookup"><span data-stu-id="96da6-148">Optimization using Single Phase Commit and Promotable Single Phase Notification</span></span>](optimization-spc-and-promotable-spn.md)
- [<span data-ttu-id="96da6-149">將資源登記成為交易中的參與者</span><span class="sxs-lookup"><span data-stu-id="96da6-149">Enlisting Resources as Participants in a Transaction</span></span>](enlisting-resources-as-participants-in-a-transaction.md)

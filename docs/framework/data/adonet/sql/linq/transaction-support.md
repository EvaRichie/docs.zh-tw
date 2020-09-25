---
title: 異動支援
ms.date: 03/30/2017
ms.assetid: 8cceb26e-8d36-4365-8967-58e2e89e0187
ms.openlocfilehash: 1449f4d10d0feeec47ac17ffda91acb3e0da17ea
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202197"
---
# <a name="transaction-support"></a><span data-ttu-id="45b37-102">異動支援</span><span class="sxs-lookup"><span data-stu-id="45b37-102">Transaction Support</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="45b37-103">支援三種不同的交易模型。</span><span class="sxs-lookup"><span data-stu-id="45b37-103">supports three distinct transaction models.</span></span> <span data-ttu-id="45b37-104">以下按照執行檢查的順序列出這些模型。</span><span class="sxs-lookup"><span data-stu-id="45b37-104">The following lists these models in the order of checks performed.</span></span>  
  
## <a name="explicit-local-transaction"></a><span data-ttu-id="45b37-105">明確本機異動</span><span class="sxs-lookup"><span data-stu-id="45b37-105">Explicit Local Transaction</span></span>  

 <span data-ttu-id="45b37-106">呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 後，如果 <xref:System.Data.Linq.DataContext.Transaction%2A> 屬性已設為 (`IDbTransaction`) 交易，則會在相同交易的情況下執行 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 呼叫。</span><span class="sxs-lookup"><span data-stu-id="45b37-106">When <xref:System.Data.Linq.DataContext.SubmitChanges%2A> is called, if the <xref:System.Data.Linq.DataContext.Transaction%2A> property is set to a (`IDbTransaction`) transaction, the <xref:System.Data.Linq.DataContext.SubmitChanges%2A> call is executed in the context of the same transaction.</span></span>  
  
 <span data-ttu-id="45b37-107">順利執行異動後，您必須負責認可或復原此異動。</span><span class="sxs-lookup"><span data-stu-id="45b37-107">It is your responsibility to commit or rollback the transaction after successful execution of the transaction.</span></span> <span data-ttu-id="45b37-108">對應至此交易的連接必須符合用於建構 <xref:System.Data.Linq.DataContext> 的連接。</span><span class="sxs-lookup"><span data-stu-id="45b37-108">The connection corresponding to the transaction must match the connection used for constructing the <xref:System.Data.Linq.DataContext>.</span></span> <span data-ttu-id="45b37-109">如果使用不同的連接，則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="45b37-109">An exception is thrown if a different connection is used.</span></span>  
  
## <a name="explicit-distributable-transaction"></a><span data-ttu-id="45b37-110">明確可散發異動</span><span class="sxs-lookup"><span data-stu-id="45b37-110">Explicit Distributable Transaction</span></span>  

 <span data-ttu-id="45b37-111">您可以 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (（包括但不限於作用中的) ）來呼叫 api <xref:System.Data.Linq.DataContext.SubmitChanges%2A> <xref:System.Transactions.Transaction> 。</span><span class="sxs-lookup"><span data-stu-id="45b37-111">You can call [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] APIs (including but not limited to <xref:System.Data.Linq.DataContext.SubmitChanges%2A>) in the scope of an active <xref:System.Transactions.Transaction>.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="45b37-112">偵測到呼叫是在交易的範圍內，而且不會建立新的交易。</span><span class="sxs-lookup"><span data-stu-id="45b37-112">detects that the call is in the scope of a transaction and does not create a new transaction.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="45b37-113">也可避免在此情況下關閉連接。</span><span class="sxs-lookup"><span data-stu-id="45b37-113">also avoids closing the connection in this case.</span></span> <span data-ttu-id="45b37-114">您可以在此種異動的情況中執行查詢和 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 執行。</span><span class="sxs-lookup"><span data-stu-id="45b37-114">You can perform query and <xref:System.Data.Linq.DataContext.SubmitChanges%2A> executions in the context of such a transaction.</span></span>  
  
## <a name="implicit-transaction"></a><span data-ttu-id="45b37-115">隱含交易</span><span class="sxs-lookup"><span data-stu-id="45b37-115">Implicit Transaction</span></span>  

 <span data-ttu-id="45b37-116">當您呼叫時 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ，會 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查看此呼叫是否在的範圍內，或者， <xref:System.Transactions.Transaction> 如果 `Transaction` 屬性 (`IDbTransaction`) 設定為使用者啟動的本機交易，則會進行檢查。</span><span class="sxs-lookup"><span data-stu-id="45b37-116">When you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] checks to see whether the call is in the scope of a <xref:System.Transactions.Transaction> or if the `Transaction` property (`IDbTransaction`) is set to a user-started local transaction.</span></span> <span data-ttu-id="45b37-117">如果找不到交易，則會 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 啟動本機交易 (`IDbTransaction`) ，並使用它來執行所產生的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="45b37-117">If it finds neither transaction, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] starts a local transaction (`IDbTransaction`) and uses it to execute the generated SQL commands.</span></span> <span data-ttu-id="45b37-118">當所有 SQL 命令都已順利完成時，會認可 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 本機交易並傳回。</span><span class="sxs-lookup"><span data-stu-id="45b37-118">When all SQL commands have been successfully completed, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] commits the local transaction and returns.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="45b37-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="45b37-119">See also</span></span>

- [<span data-ttu-id="45b37-120">背景資訊</span><span class="sxs-lookup"><span data-stu-id="45b37-120">Background Information</span></span>](background-information.md)
- [<span data-ttu-id="45b37-121">作法：使用異動括住提交的資料</span><span class="sxs-lookup"><span data-stu-id="45b37-121">How to: Bracket Data Submissions by Using Transactions</span></span>](how-to-bracket-data-submissions-by-using-transactions.md)

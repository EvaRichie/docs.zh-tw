---
title: 作法：將變更提交至資料庫
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: 5952cce5469d7a7e13e8b896f91ea1279fd62d8b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197036"
---
# <a name="how-to-submit-changes-to-the-database"></a><span data-ttu-id="44c9f-102">作法：將變更提交至資料庫</span><span class="sxs-lookup"><span data-stu-id="44c9f-102">How to: Submit Changes to the Database</span></span>

<span data-ttu-id="44c9f-103">不論對物件進行多少的變更，都只會變更記憶體中的複本。</span><span class="sxs-lookup"><span data-stu-id="44c9f-103">Regardless of how many changes you make to your objects, changes are made only to in-memory replicas.</span></span> <span data-ttu-id="44c9f-104">並不會變更到資料庫中的實際資料。</span><span class="sxs-lookup"><span data-stu-id="44c9f-104">You have made no changes to the actual data in the database.</span></span> <span data-ttu-id="44c9f-105">在 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 上明確呼叫 <xref:System.Data.Linq.DataContext> 之前，變更都不會傳輸至伺服器。</span><span class="sxs-lookup"><span data-stu-id="44c9f-105">Your changes are not transmitted to the server until you explicitly call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> on the <xref:System.Data.Linq.DataContext>.</span></span>  
  
 <span data-ttu-id="44c9f-106">進行這個呼叫時，<xref:System.Data.Linq.DataContext> 會嘗試將變更轉譯為對等的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="44c9f-106">When you make this call, the <xref:System.Data.Linq.DataContext> tries to translate your changes into equivalent SQL commands.</span></span> <span data-ttu-id="44c9f-107">您可以使用自己的自訂邏輯來覆寫這些動作，但提交的順序是由 <xref:System.Data.Linq.DataContext> 稱為「 *變更處理器*」的服務所協調。</span><span class="sxs-lookup"><span data-stu-id="44c9f-107">You can use your own custom logic to override these actions, but the order of submission is orchestrated by a service of the <xref:System.Data.Linq.DataContext> known as the *change processor*.</span></span> <span data-ttu-id="44c9f-108">事件順序如下：</span><span class="sxs-lookup"><span data-stu-id="44c9f-108">The sequence of events is as follows:</span></span>  
  
1. <span data-ttu-id="44c9f-109">呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會檢查這組已知的物件，判斷新的執行個體 (Instance) 是否已附加至它們。</span><span class="sxs-lookup"><span data-stu-id="44c9f-109">When you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] examines the set of known objects to determine whether new instances have been attached to them.</span></span> <span data-ttu-id="44c9f-110">如果已連接，則這些新的執行個體會加入至這組已追蹤的物件中。</span><span class="sxs-lookup"><span data-stu-id="44c9f-110">If they have, these new instances are added to the set of tracked objects.</span></span>  
  
2. <span data-ttu-id="44c9f-111">所有具有暫止變更的物件，都會根據它們之間的相依性來排序為一串物件。</span><span class="sxs-lookup"><span data-stu-id="44c9f-111">All objects that have pending changes are ordered into a sequence of objects based on the dependencies between them.</span></span> <span data-ttu-id="44c9f-112">而變更是根據其他物件的物件，則會循序放在它們的相依性後面。</span><span class="sxs-lookup"><span data-stu-id="44c9f-112">Objects whose changes depend on other objects are sequenced after their dependencies.</span></span>  
  
3. <span data-ttu-id="44c9f-113">在傳輸任何實際變更之前，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會先啟動交易來封裝一系列個別的命令。</span><span class="sxs-lookup"><span data-stu-id="44c9f-113">Immediately before any actual changes are transmitted, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] starts a transaction to encapsulate the series of individual commands.</span></span>  
  
4. <span data-ttu-id="44c9f-114">物件的變更會一個接著一個地轉換為 SQL 命令，並傳送給伺服器。</span><span class="sxs-lookup"><span data-stu-id="44c9f-114">The changes to the objects are translated one by one to SQL commands and sent to the server.</span></span>  
  
 <span data-ttu-id="44c9f-115">此時，資料庫偵測到的任何錯誤都會停止提交流程，並引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="44c9f-115">At this point, any errors detected by the database cause the submission process to stop, and an exception is raised.</span></span> <span data-ttu-id="44c9f-116">而資料庫的所有變更都會復原為未進行提交之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="44c9f-116">All changes to the database are rolled back as if no submissions ever occurred.</span></span> <span data-ttu-id="44c9f-117"><xref:System.Data.Linq.DataContext> 仍然具有所有變更的完整記錄。</span><span class="sxs-lookup"><span data-stu-id="44c9f-117">The <xref:System.Data.Linq.DataContext> still has a full recording of all changes.</span></span> <span data-ttu-id="44c9f-118">因此，您可以嘗試更正問題，並再次呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="44c9f-118">You can therefore try to correct the problem and call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> again, as in the code example that follows.</span></span>  
  
## <a name="example"></a><span data-ttu-id="44c9f-119">範例</span><span class="sxs-lookup"><span data-stu-id="44c9f-119">Example</span></span>  

 <span data-ttu-id="44c9f-120">當提交異動順利完成時，<xref:System.Data.Linq.DataContext> 會略過變更追蹤資訊，以接受物件的變更。</span><span class="sxs-lookup"><span data-stu-id="44c9f-120">When the transaction around the submission is completed successfully, the <xref:System.Data.Linq.DataContext> accepts the changes to the objects by ignoring the change-tracking information.</span></span>  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="44c9f-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="44c9f-121">See also</span></span>

- [<span data-ttu-id="44c9f-122">作法：偵測和解決發生衝突的提交內容</span><span class="sxs-lookup"><span data-stu-id="44c9f-122">How to: Detect and Resolve Conflicting Submissions</span></span>](how-to-detect-and-resolve-conflicting-submissions.md)
- [<span data-ttu-id="44c9f-123">作法：管理變更衝突</span><span class="sxs-lookup"><span data-stu-id="44c9f-123">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)
- [<span data-ttu-id="44c9f-124">下載範例資料庫</span><span class="sxs-lookup"><span data-stu-id="44c9f-124">Downloading Sample Databases</span></span>](downloading-sample-databases.md)
- [<span data-ttu-id="44c9f-125">變更資料和提交</span><span class="sxs-lookup"><span data-stu-id="44c9f-125">Making and Submitting Data Changes</span></span>](making-and-submitting-data-changes.md)

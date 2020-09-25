---
title: 開放式並行存取：總覽
ms.date: 03/30/2017
ms.assetid: c2e38512-d0c8-4807-b30a-cb7e30338694
ms.openlocfilehash: 7a1bc23d9f012b2f3541c1411a25b7527e696873
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169384"
---
# <a name="optimistic-concurrency-overview"></a><span data-ttu-id="145c5-102">開放式並行存取：總覽</span><span class="sxs-lookup"><span data-stu-id="145c5-102">Optimistic Concurrency: Overview</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="145c5-103">支援開放式並行存取 (Optimistic Concurrency) 控制。</span><span class="sxs-lookup"><span data-stu-id="145c5-103">supports optimistic concurrency control.</span></span> <span data-ttu-id="145c5-104">下表描述適用于檔中開放式平行存取的詞彙 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ：</span><span class="sxs-lookup"><span data-stu-id="145c5-104">The following table describes terms that apply to optimistic concurrency in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] documentation:</span></span>  
  
|<span data-ttu-id="145c5-105">詞彙</span><span class="sxs-lookup"><span data-stu-id="145c5-105">Terms</span></span>|<span data-ttu-id="145c5-106">描述</span><span class="sxs-lookup"><span data-stu-id="145c5-106">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="145c5-107">並行</span><span class="sxs-lookup"><span data-stu-id="145c5-107">concurrency</span></span>|<span data-ttu-id="145c5-108">兩位以上的使用者同時嘗試更新相同資料庫資料列的情況。</span><span class="sxs-lookup"><span data-stu-id="145c5-108">The situation in which two or more users at the same time try to update the same database row.</span></span>|  
|<span data-ttu-id="145c5-109">並行衝突</span><span class="sxs-lookup"><span data-stu-id="145c5-109">concurrency conflict</span></span>|<span data-ttu-id="145c5-110">兩位以上的使用者同時嘗試將衝突值送出給資料列的一個或多個資料行的情況。</span><span class="sxs-lookup"><span data-stu-id="145c5-110">The situation in which two or more users at the same time try to submit conflicting values to one or more columns of a row.</span></span>|  
|<span data-ttu-id="145c5-111">並行控制</span><span class="sxs-lookup"><span data-stu-id="145c5-111">concurrency control</span></span>|<span data-ttu-id="145c5-112">用來解決並行衝突的技術。</span><span class="sxs-lookup"><span data-stu-id="145c5-112">The technique used to resolve concurrency conflicts.</span></span>|  
|<span data-ttu-id="145c5-113">開放式並行存取控制項</span><span class="sxs-lookup"><span data-stu-id="145c5-113">optimistic concurrency control</span></span>|<span data-ttu-id="145c5-114">此種技術會先檢查資料列中的其他異動是否已變更值，才允許送出變更。</span><span class="sxs-lookup"><span data-stu-id="145c5-114">The technique that first investigates whether other transactions have changed values in a row before permitting changes to be submitted.</span></span><br /><br /> <span data-ttu-id="145c5-115">相較于封閉式 *並行存取控制*，這會鎖定記錄以避免並行衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-115">Contrast with *pessimistic concurrency control*, which locks the record to avoid concurrency conflicts.</span></span><br /><br /> <span data-ttu-id="145c5-116">所謂的*開放式*控制項是因為它會考慮一個交易干擾另一個交易的可能性不太可能。</span><span class="sxs-lookup"><span data-stu-id="145c5-116">*Optimistic* control is so termed because it considers the chances of one transaction interfering with another to be unlikely.</span></span>|  
|<span data-ttu-id="145c5-117">衝突的解決方式</span><span class="sxs-lookup"><span data-stu-id="145c5-117">conflict resolution</span></span>|<span data-ttu-id="145c5-118">透過再次查詢資料庫，然後調整差異，以重新整理衝突項目的處理流程。</span><span class="sxs-lookup"><span data-stu-id="145c5-118">The process of refreshing a conflicting item by querying the database again and then reconciling differences.</span></span><br /><br /> <span data-ttu-id="145c5-119">重新整理物件時，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 變更 Tracker 會保留下列資料：</span><span class="sxs-lookup"><span data-stu-id="145c5-119">When an object is refreshed, the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] change tracker holds the following data:</span></span><br /><br /> <span data-ttu-id="145c5-120">-最初取自資料庫並用於更新檢查的值。</span><span class="sxs-lookup"><span data-stu-id="145c5-120">-   The values originally taken from the database and used for the update check.</span></span><br /><span data-ttu-id="145c5-121">-後續查詢中的新資料庫值。</span><span class="sxs-lookup"><span data-stu-id="145c5-121">-   The new database values from the subsequent query.</span></span><br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="145c5-122">接著會判斷物件是否發生衝突 (也就是，它的其中一個或多個成員值是否變更)。</span><span class="sxs-lookup"><span data-stu-id="145c5-122">then determines whether the object is in conflict (that is, whether one or more of its member values has changed).</span></span> <span data-ttu-id="145c5-123">如果物件發生衝突， [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 接下來會判斷其成員有何衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-123">If the object is in conflict, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] next determines which of its members are in conflict.</span></span><br /><br /> <span data-ttu-id="145c5-124">[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 發現的所有成員衝突都會加入至衝突清單中。</span><span class="sxs-lookup"><span data-stu-id="145c5-124">Any member conflict that [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] discovers is added to a conflict list.</span></span>|  
  
 <span data-ttu-id="145c5-125">在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 物件模型中，當下列兩個條件都成立時，就會發生 *開放式平行存取衝突* ：</span><span class="sxs-lookup"><span data-stu-id="145c5-125">In the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] object model, an *optimistic concurrency conflict* occurs when both of the following conditions are true:</span></span>  
  
- <span data-ttu-id="145c5-126">用戶端嘗試將變更送出給資料庫。</span><span class="sxs-lookup"><span data-stu-id="145c5-126">The client tries to submit changes to the database.</span></span>  
  
- <span data-ttu-id="145c5-127">資料庫中的一個或多個更新檢查值，自用戶端最後一次讀取之後已更新過。</span><span class="sxs-lookup"><span data-stu-id="145c5-127">One or more update-check values have been updated in the database since the client last read them.</span></span>  
  
 <span data-ttu-id="145c5-128">解決這項衝突包括探索哪些物件成員發生衝突，然後決定要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="145c5-128">Resolution of this conflict includes discovering which members of the object are in conflict, and then deciding what you want to do about it.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="145c5-129">只有對應成 <xref:System.Data.Linq.Mapping.UpdateCheck.Always> 或 <xref:System.Data.Linq.Mapping.UpdateCheck.WhenChanged> 的成員才會參與開放式並行存取檢查。</span><span class="sxs-lookup"><span data-stu-id="145c5-129">Only members mapped as <xref:System.Data.Linq.Mapping.UpdateCheck.Always> or <xref:System.Data.Linq.Mapping.UpdateCheck.WhenChanged> participate in optimistic concurrency checks.</span></span> <span data-ttu-id="145c5-130">而不會檢查標記為 <xref:System.Data.Linq.Mapping.UpdateCheck.Never> 的成員。</span><span class="sxs-lookup"><span data-stu-id="145c5-130">No check is performed for members marked <xref:System.Data.Linq.Mapping.UpdateCheck.Never>.</span></span> <span data-ttu-id="145c5-131">如需詳細資訊，請參閱<xref:System.Data.Linq.Mapping.UpdateCheck>。</span><span class="sxs-lookup"><span data-stu-id="145c5-131">For more information, see <xref:System.Data.Linq.Mapping.UpdateCheck>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="145c5-132">範例</span><span class="sxs-lookup"><span data-stu-id="145c5-132">Example</span></span>  

 <span data-ttu-id="145c5-133">例如，在下列案例中，User1 查詢資料庫中的資料列，開始準備更新。</span><span class="sxs-lookup"><span data-stu-id="145c5-133">For example, in the following scenario, User1 starts to prepare an update by querying the database for a row.</span></span> <span data-ttu-id="145c5-134">User1 會接收到值為 Alfreds、Maria 和 Sales 的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="145c5-134">User1 receives a row with values of Alfreds, Maria, and Sales.</span></span>  
  
 <span data-ttu-id="145c5-135">User1 想將 Manager 資料行的值變更為 Alfred，並將 Department 資料行的值變更為 Marketing。</span><span class="sxs-lookup"><span data-stu-id="145c5-135">User1 wants to change the value of the Manager column to Alfred and the value of the Department column to Marketing.</span></span> <span data-ttu-id="145c5-136">但是在 User1 送出那些變更之前，User2 就已經先送出變更給資料庫。</span><span class="sxs-lookup"><span data-stu-id="145c5-136">Before User1 can submit those changes, User2 has submitted changes to the database.</span></span> <span data-ttu-id="145c5-137">因此，現在 Assistant 資料行的值已變更為 Mary，而 Department 資料行的值已變更為 Service。</span><span class="sxs-lookup"><span data-stu-id="145c5-137">So now the value of the Assistant column has been changed to Mary and the value of the Department column to Service.</span></span>  
  
 <span data-ttu-id="145c5-138">如果 User1 現在嘗試送出變更，則送出會失敗，而且會擲回 <xref:System.Data.Linq.ChangeConflictException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="145c5-138">When User1 now tries to submit changes, the submission fails and a <xref:System.Data.Linq.ChangeConflictException> exception is thrown.</span></span> <span data-ttu-id="145c5-139">因為 Assistant 資料行和 Department 資料行的資料庫值並不是所預期的值，所以會發生這種結果。</span><span class="sxs-lookup"><span data-stu-id="145c5-139">This result occurs because the database values for the Assistant column and the Department column are not those that were expected.</span></span> <span data-ttu-id="145c5-140">因此表示 Assistant 和 Department 資料行的成員會產生衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-140">Members representing the Assistant and Department columns are in conflict.</span></span> <span data-ttu-id="145c5-141">下表將摘要說明這種情況。</span><span class="sxs-lookup"><span data-stu-id="145c5-141">The following table summarizes the situation.</span></span>  
  
||<span data-ttu-id="145c5-142">Manager</span><span class="sxs-lookup"><span data-stu-id="145c5-142">Manager</span></span>|<span data-ttu-id="145c5-143">Assistant</span><span class="sxs-lookup"><span data-stu-id="145c5-143">Assistant</span></span>|<span data-ttu-id="145c5-144">department</span><span class="sxs-lookup"><span data-stu-id="145c5-144">Department</span></span>|  
|------|-------------|---------------|----------------|  
|<span data-ttu-id="145c5-145">原始狀態</span><span class="sxs-lookup"><span data-stu-id="145c5-145">Original state</span></span>|<span data-ttu-id="145c5-146">Alfreds</span><span class="sxs-lookup"><span data-stu-id="145c5-146">Alfreds</span></span>|<span data-ttu-id="145c5-147">Maria</span><span class="sxs-lookup"><span data-stu-id="145c5-147">Maria</span></span>|<span data-ttu-id="145c5-148">Sales</span><span class="sxs-lookup"><span data-stu-id="145c5-148">Sales</span></span>|  
|<span data-ttu-id="145c5-149">User1</span><span class="sxs-lookup"><span data-stu-id="145c5-149">User1</span></span>|<span data-ttu-id="145c5-150">Alfred</span><span class="sxs-lookup"><span data-stu-id="145c5-150">Alfred</span></span>||<span data-ttu-id="145c5-151">Marketing</span><span class="sxs-lookup"><span data-stu-id="145c5-151">Marketing</span></span>|  
|<span data-ttu-id="145c5-152">User2</span><span class="sxs-lookup"><span data-stu-id="145c5-152">User2</span></span>||<span data-ttu-id="145c5-153">Mary</span><span class="sxs-lookup"><span data-stu-id="145c5-153">Mary</span></span>|<span data-ttu-id="145c5-154">服務</span><span class="sxs-lookup"><span data-stu-id="145c5-154">Service</span></span>|  
  
 <span data-ttu-id="145c5-155">您可以使用不同方式來解決這類衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-155">You can resolve conflicts such as this in different ways.</span></span> <span data-ttu-id="145c5-156">如需詳細資訊，請參閱 [如何：管理變更衝突](how-to-manage-change-conflicts.md)。</span><span class="sxs-lookup"><span data-stu-id="145c5-156">For more information, see [How to: Manage Change Conflicts](how-to-manage-change-conflicts.md).</span></span>  
  
## <a name="conflict-detection-and-resolution-checklist"></a><span data-ttu-id="145c5-157">衝突偵測和解決檢查清單</span><span class="sxs-lookup"><span data-stu-id="145c5-157">Conflict Detection and Resolution Checklist</span></span>  

 <span data-ttu-id="145c5-158">您可以偵測和解決任何精細度等級的衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-158">You can detect and resolve conflicts at any level of detail.</span></span> <span data-ttu-id="145c5-159">其中一種極端的做法是，使用三種方式的其中一種方式來解決所有的衝突 (請參閱 <xref:System.Data.Linq.RefreshMode>)，而不考慮其他事項。</span><span class="sxs-lookup"><span data-stu-id="145c5-159">At one extreme, you can resolve all conflicts in one of three ways (see <xref:System.Data.Linq.RefreshMode>) without additional consideration.</span></span> <span data-ttu-id="145c5-160">另一種極端的做法是，指定每個衝突成員之每種衝突類型的特定動作。</span><span class="sxs-lookup"><span data-stu-id="145c5-160">At the other extreme, you can designate a specific action for each type of conflict on every member in conflict.</span></span>  
  
- <span data-ttu-id="145c5-161">指定或修訂物件模型中的 <xref:System.Data.Linq.Mapping.UpdateCheck> 選項。</span><span class="sxs-lookup"><span data-stu-id="145c5-161">Specify or revise <xref:System.Data.Linq.Mapping.UpdateCheck> options in your object model.</span></span>  
  
     <span data-ttu-id="145c5-162">如需詳細資訊，請參閱 [如何：指定測試並行衝突的成員](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)。</span><span class="sxs-lookup"><span data-stu-id="145c5-162">For more information, see [How to: Specify Which Members are Tested for Concurrency Conflicts](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md).</span></span>  
  
- <span data-ttu-id="145c5-163">在 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 呼叫的 try/catch 區塊中，指定何時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="145c5-163">In the try/catch block of your call to <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, specify at what point you want exceptions to be thrown.</span></span>  
  
     <span data-ttu-id="145c5-164">如需詳細資訊，請參閱 [如何：指定並行例外狀況的](how-to-specify-when-concurrency-exceptions-are-thrown.md)擲回時機。</span><span class="sxs-lookup"><span data-stu-id="145c5-164">For more information, see [How to: Specify When Concurrency Exceptions are Thrown](how-to-specify-when-concurrency-exceptions-are-thrown.md).</span></span>  
  
- <span data-ttu-id="145c5-165">決定想要擷取的衝突詳細資料量，並據此將程式碼併入 try/catch 區域。</span><span class="sxs-lookup"><span data-stu-id="145c5-165">Determine how much conflict detail you want to retrieve, and include code in your try/catch block accordingly.</span></span>  
  
     <span data-ttu-id="145c5-166">如需詳細資訊，請參閱 [如何：取出實體衝突資訊](how-to-retrieve-entity-conflict-information.md) 和 [如何：抓取成員衝突資訊](how-to-retrieve-member-conflict-information.md)。</span><span class="sxs-lookup"><span data-stu-id="145c5-166">For more information, see [How to: Retrieve Entity Conflict Information](how-to-retrieve-entity-conflict-information.md) and [How to: Retrieve Member Conflict Information](how-to-retrieve-member-conflict-information.md).</span></span>  
  
- <span data-ttu-id="145c5-167">在您的程式碼中包含您 `try` / `catch` 要如何解決您發現的各種衝突。</span><span class="sxs-lookup"><span data-stu-id="145c5-167">Include in your `try`/`catch` code how you want to resolve the various conflicts you discover.</span></span>  
  
     <span data-ttu-id="145c5-168">如需詳細資訊，請參閱 [如何：藉由保留資料庫值來解決衝突](how-to-resolve-conflicts-by-retaining-database-values.md)、 [如何：藉由覆寫資料庫值來解決](how-to-resolve-conflicts-by-overwriting-database-values.md)衝突，以及 [如何：藉由與資料庫值合併來解決衝突](how-to-resolve-conflicts-by-merging-with-database-values.md)。</span><span class="sxs-lookup"><span data-stu-id="145c5-168">For more information, see [How to: Resolve Conflicts by Retaining Database Values](how-to-resolve-conflicts-by-retaining-database-values.md), [How to: Resolve Conflicts by Overwriting Database Values](how-to-resolve-conflicts-by-overwriting-database-values.md), and [How to: Resolve Conflicts by Merging with Database Values](how-to-resolve-conflicts-by-merging-with-database-values.md).</span></span>  
  
## <a name="linq-to-sql-types-that-support-conflict-discovery-and-resolution"></a><span data-ttu-id="145c5-169">支援衝突探索和解決的 LINQ to SQL 型別</span><span class="sxs-lookup"><span data-stu-id="145c5-169">LINQ to SQL Types That Support Conflict Discovery and Resolution</span></span>  

 <span data-ttu-id="145c5-170">[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中支援開放式並行存取衝突解決的類別和功能包括：</span><span class="sxs-lookup"><span data-stu-id="145c5-170">Classes and features to support the resolution of conflicts in optimistic concurrency in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] include the following:</span></span>  
  
- <xref:System.Data.Linq.ObjectChangeConflict?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.MemberChangeConflict?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.ChangeConflictCollection?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.ChangeConflictException?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.ChangeConflicts%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.Refresh%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.Mapping.UpdateCheck?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.RefreshMode?displayProperty=nameWithType>  
  
## <a name="see-also"></a><span data-ttu-id="145c5-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="145c5-171">See also</span></span>

- [<span data-ttu-id="145c5-172">作法：管理變更衝突</span><span class="sxs-lookup"><span data-stu-id="145c5-172">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)

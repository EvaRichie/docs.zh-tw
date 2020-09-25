---
title: 作法：藉由覆寫資料庫值來解決衝突
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd6db0b8-c29c-48ff-b768-31d28e7a148c
ms.openlocfilehash: 1dc112350451bde28d27c63961733b96f6fc84be
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91191706"
---
# <a name="how-to-resolve-conflicts-by-overwriting-database-values"></a><span data-ttu-id="0b0a2-102">作法：藉由覆寫資料庫值來解決衝突</span><span class="sxs-lookup"><span data-stu-id="0b0a2-102">How to: Resolve Conflicts by Overwriting Database Values</span></span>

<span data-ttu-id="0b0a2-103">若要先協調預期和實際資料庫值之間的差異再重新送出變更，可以使用 <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> 覆寫資料庫值。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-103">To reconcile differences between expected and actual database values before you try to resubmit your changes, you can use <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> to overwrite database values.</span></span> <span data-ttu-id="0b0a2-104">如需詳細資訊，請參閱 [開放式平行存取：總覽](optimistic-concurrency-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-104">For more information, see [Optimistic Concurrency: Overview](optimistic-concurrency-overview.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0b0a2-105">在所有情況下，擷取資料庫中更新過的資料會先重新整理用戶端上的資料錄。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-105">In all cases, the record on the client is first refreshed by retrieving the updated data from the database.</span></span> <span data-ttu-id="0b0a2-106">這個動作可確保下一次嘗試更新時，不會在相同的並行存取檢查時失敗。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-106">This action makes sure that the next update try will not fail on the same concurrency checks.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0b0a2-107">範例</span><span class="sxs-lookup"><span data-stu-id="0b0a2-107">Example</span></span>  

 <span data-ttu-id="0b0a2-108">在這個案例下，當 User1 嘗試送出變更時，因為 User2 同時變更了 Assistant 和 Department 資料行，所以會擲回 <xref:System.Data.Linq.ChangeConflictException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-108">In this scenario, an <xref:System.Data.Linq.ChangeConflictException> exception is thrown when User1 tries to submit changes, because User2 has in the meantime changed the Assistant and Department columns.</span></span> <span data-ttu-id="0b0a2-109">下表顯示這個情況。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-109">The following table shows the situation.</span></span>  
  
||<span data-ttu-id="0b0a2-110">Manager</span><span class="sxs-lookup"><span data-stu-id="0b0a2-110">Manager</span></span>|<span data-ttu-id="0b0a2-111">Assistant</span><span class="sxs-lookup"><span data-stu-id="0b0a2-111">Assistant</span></span>|<span data-ttu-id="0b0a2-112">department</span><span class="sxs-lookup"><span data-stu-id="0b0a2-112">Department</span></span>|  
|------|-------------|---------------|----------------|  
|<span data-ttu-id="0b0a2-113">User1 和 User2 查詢時的原始資料庫狀態。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-113">Original database state when queried by User1 and User2.</span></span>|<span data-ttu-id="0b0a2-114">Alfreds</span><span class="sxs-lookup"><span data-stu-id="0b0a2-114">Alfreds</span></span>|<span data-ttu-id="0b0a2-115">Maria</span><span class="sxs-lookup"><span data-stu-id="0b0a2-115">Maria</span></span>|<span data-ttu-id="0b0a2-116">Sales</span><span class="sxs-lookup"><span data-stu-id="0b0a2-116">Sales</span></span>|  
|<span data-ttu-id="0b0a2-117">User1 準備送出這些變更。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-117">User1 prepares to submit these changes.</span></span>|<span data-ttu-id="0b0a2-118">Alfred</span><span class="sxs-lookup"><span data-stu-id="0b0a2-118">Alfred</span></span>||<span data-ttu-id="0b0a2-119">Marketing</span><span class="sxs-lookup"><span data-stu-id="0b0a2-119">Marketing</span></span>|  
|<span data-ttu-id="0b0a2-120">User2 已送出這些變更。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-120">User2 has already submitted these changes.</span></span>||<span data-ttu-id="0b0a2-121">Mary</span><span class="sxs-lookup"><span data-stu-id="0b0a2-121">Mary</span></span>|<span data-ttu-id="0b0a2-122">服務</span><span class="sxs-lookup"><span data-stu-id="0b0a2-122">Service</span></span>|  
  
 <span data-ttu-id="0b0a2-123">User1 決定以目前的用戶端成員值覆寫資料庫值，來解決這個衝突。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-123">User1 decides to resolve this conflict by overwriting database values with the current client member values.</span></span>  
  
 <span data-ttu-id="0b0a2-124">User1 使用 <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> 解決衝突時，資料庫中的結果會如同下表：</span><span class="sxs-lookup"><span data-stu-id="0b0a2-124">When User1 resolves the conflict by using <xref:System.Data.Linq.RefreshMode.KeepCurrentValues>, the result in the database is as in following table:</span></span>  
  
||<span data-ttu-id="0b0a2-125">Manager</span><span class="sxs-lookup"><span data-stu-id="0b0a2-125">Manager</span></span>|<span data-ttu-id="0b0a2-126">Assistant</span><span class="sxs-lookup"><span data-stu-id="0b0a2-126">Assistant</span></span>|<span data-ttu-id="0b0a2-127">department</span><span class="sxs-lookup"><span data-stu-id="0b0a2-127">Department</span></span>|  
|------|-------------|---------------|----------------|  
|<span data-ttu-id="0b0a2-128">解決衝突後的新狀態。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-128">New state after conflict resolution.</span></span>|<span data-ttu-id="0b0a2-129">Alfred</span><span class="sxs-lookup"><span data-stu-id="0b0a2-129">Alfred</span></span><br /><br /> <span data-ttu-id="0b0a2-130">(來自 User1)</span><span class="sxs-lookup"><span data-stu-id="0b0a2-130">(from User1)</span></span>|<span data-ttu-id="0b0a2-131">Maria</span><span class="sxs-lookup"><span data-stu-id="0b0a2-131">Maria</span></span><br /><br /> <span data-ttu-id="0b0a2-132">(原始)</span><span class="sxs-lookup"><span data-stu-id="0b0a2-132">(original)</span></span>|<span data-ttu-id="0b0a2-133">Marketing</span><span class="sxs-lookup"><span data-stu-id="0b0a2-133">Marketing</span></span><br /><br /> <span data-ttu-id="0b0a2-134">(來自 User1)</span><span class="sxs-lookup"><span data-stu-id="0b0a2-134">(from User1)</span></span>|  
  
 <span data-ttu-id="0b0a2-135">下列範例程式碼顯示如何以目前的用戶端成員值來覆寫資料庫值 </span><span class="sxs-lookup"><span data-stu-id="0b0a2-135">The following example code shows how to overwrite database values with the current client member values.</span></span> <span data-ttu-id="0b0a2-136">(但不會對個別成員衝突進行任何檢查或自訂處理)。</span><span class="sxs-lookup"><span data-stu-id="0b0a2-136">(No inspection or custom handling of individual member conflicts occurs.)</span></span>  
  
 [!code-csharp[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="0b0a2-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0b0a2-137">See also</span></span>

- [<span data-ttu-id="0b0a2-138">作法：管理變更衝突</span><span class="sxs-lookup"><span data-stu-id="0b0a2-138">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)

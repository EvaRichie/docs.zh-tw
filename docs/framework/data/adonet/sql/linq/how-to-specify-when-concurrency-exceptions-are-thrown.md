---
title: 作法：指定並行例外狀況的擲回時機
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 344ae068-ff63-4a2e-8b00-af22e143675f
ms.openlocfilehash: 9d71ca82c3fe1abd23a82d952d38c3ea23a7f1c0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197101"
---
# <a name="how-to-specify-when-concurrency-exceptions-are-thrown"></a><span data-ttu-id="4b3de-102">作法：指定並行例外狀況的擲回時機</span><span class="sxs-lookup"><span data-stu-id="4b3de-102">How to: Specify When Concurrency Exceptions are Thrown</span></span>

<span data-ttu-id="4b3de-103">在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，因為開放式並行存取 (Optimistic Concurrency) 衝突而未更新物件時，會擲回 <xref:System.Data.Linq.ChangeConflictException> 例外狀況 (Exception)。</span><span class="sxs-lookup"><span data-stu-id="4b3de-103">In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], a <xref:System.Data.Linq.ChangeConflictException> exception is thrown when objects do not update because of optimistic concurrency conflicts.</span></span> <span data-ttu-id="4b3de-104">如需詳細資訊，請參閱 [開放式平行存取：總覽](optimistic-concurrency-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4b3de-104">For more information, see [Optimistic Concurrency: Overview](optimistic-concurrency-overview.md).</span></span>  
  
 <span data-ttu-id="4b3de-105">將變更提交至資料庫之前，您可以指定何時應擲出並行例外狀況：</span><span class="sxs-lookup"><span data-stu-id="4b3de-105">Before you submit your changes to the database, you can specify when concurrency exceptions should be thrown:</span></span>  
  
- <span data-ttu-id="4b3de-106">在第一次失敗時擲出例外狀況 (<xref:System.Data.Linq.ConflictMode.FailOnFirstConflict>)。</span><span class="sxs-lookup"><span data-stu-id="4b3de-106">Throw the exception at the first failure (<xref:System.Data.Linq.ConflictMode.FailOnFirstConflict>).</span></span>  
  
- <span data-ttu-id="4b3de-107">完成所有更新嘗試、累積所有失敗，並且在例外狀況中報告所累積的失敗 (<xref:System.Data.Linq.ConflictMode.ContinueOnConflict>)。</span><span class="sxs-lookup"><span data-stu-id="4b3de-107">Finish all update tries, accumulate all failures, and report the accumulated failures in the exception (<xref:System.Data.Linq.ConflictMode.ContinueOnConflict>).</span></span>  
  
 <span data-ttu-id="4b3de-108">擲出後，<xref:System.Data.Linq.ChangeConflictException> 例外狀況會提供 <xref:System.Data.Linq.ChangeConflictCollection> 集合的存取權。</span><span class="sxs-lookup"><span data-stu-id="4b3de-108">When thrown, the <xref:System.Data.Linq.ChangeConflictException> exception provides access to a <xref:System.Data.Linq.ChangeConflictCollection> collection.</span></span> <span data-ttu-id="4b3de-109">此集合會提供每個衝突的詳細資訊 (對應至失敗的單一更新嘗試)，其中包含 <xref:System.Data.Linq.ObjectChangeConflict.MemberConflicts%2A> 集合的存取權。</span><span class="sxs-lookup"><span data-stu-id="4b3de-109">This collection provides details for each conflict (mapped to a single failed update try), including access to the <xref:System.Data.Linq.ObjectChangeConflict.MemberConflicts%2A> collection.</span></span> <span data-ttu-id="4b3de-110">每個成員衝突都會對應至未通過並行存取檢查之更新中的單一成員。</span><span class="sxs-lookup"><span data-stu-id="4b3de-110">Each member conflict maps to a single member in the update that failed the concurrency check.</span></span>  
  
## <a name="example"></a><span data-ttu-id="4b3de-111">範例</span><span class="sxs-lookup"><span data-stu-id="4b3de-111">Example</span></span>  

 <span data-ttu-id="4b3de-112">下列程式碼會顯示有兩個值的範例。</span><span class="sxs-lookup"><span data-stu-id="4b3de-112">The following code shows examples of both values.</span></span>  
  
 [!code-csharp[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/vb/module1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="4b3de-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4b3de-113">See also</span></span>

- [<span data-ttu-id="4b3de-114">作法：管理變更衝突</span><span class="sxs-lookup"><span data-stu-id="4b3de-114">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)
- [<span data-ttu-id="4b3de-115">變更資料和提交</span><span class="sxs-lookup"><span data-stu-id="4b3de-115">Making and Submitting Data Changes</span></span>](making-and-submitting-data-changes.md)

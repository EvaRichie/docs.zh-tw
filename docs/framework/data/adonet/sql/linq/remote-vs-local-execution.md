---
title: 遠端與本機執行的比較
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ee50e943-9349-4c84-ab1c-c35d3ada1a9c
ms.openlocfilehash: c99e726902192fc8324e77441b80aa4519c55ddc
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91196945"
---
# <a name="remote-vs-local-execution"></a><span data-ttu-id="06746-102">遠端與本機執行的比較</span><span class="sxs-lookup"><span data-stu-id="06746-102">Remote vs. Local Execution</span></span>

<span data-ttu-id="06746-103">您可以決定執行查詢的方式為遠端 (也就是，資料庫引擎對資料庫執行查詢) 或本機 ([!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 對本機快取執行查詢)。</span><span class="sxs-lookup"><span data-stu-id="06746-103">You can decide to execute your queries either remotely (that is, the database engine executes the query against the database) or locally ([!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] executes the query against a local cache).</span></span>  
  
## <a name="remote-execution"></a><span data-ttu-id="06746-104">遠端執行</span><span class="sxs-lookup"><span data-stu-id="06746-104">Remote Execution</span></span>  

 <span data-ttu-id="06746-105">請考慮以下查詢：</span><span class="sxs-lookup"><span data-stu-id="06746-105">Consider the following query:</span></span>  
  
 [!code-csharp[DLinqQueryConcepts#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#7)]
 [!code-vb[DLinqQueryConcepts#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#7)]  
  
 <span data-ttu-id="06746-106">如果資料庫有數千列訂單，當您只要處理一小部分的訂單時，您不會想要擷取出所有訂單。</span><span class="sxs-lookup"><span data-stu-id="06746-106">If your database has thousands of rows of orders, you do not want to retrieve them all to process a small subset.</span></span> <span data-ttu-id="06746-107">在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，<xref:System.Data.Linq.EntitySet%601> 類別 (Class) 會實作 <xref:System.Linq.IQueryable> 介面。</span><span class="sxs-lookup"><span data-stu-id="06746-107">In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], the <xref:System.Data.Linq.EntitySet%601> class implements the <xref:System.Linq.IQueryable> interface.</span></span> <span data-ttu-id="06746-108">這種方法可以確認這類查詢可以遠端執行。</span><span class="sxs-lookup"><span data-stu-id="06746-108">This approach makes sure that such queries can be executed remotely.</span></span> <span data-ttu-id="06746-109">這項技術的兩個主要優點是：</span><span class="sxs-lookup"><span data-stu-id="06746-109">Two major benefits flow from this technique:</span></span>  
  
- <span data-ttu-id="06746-110">不會擷取不必要的資料。</span><span class="sxs-lookup"><span data-stu-id="06746-110">Unnecessary data is not retrieved.</span></span>  
  
- <span data-ttu-id="06746-111">因為利用資料庫索引，所以資料庫引擎執行的查詢通常會較具效率。</span><span class="sxs-lookup"><span data-stu-id="06746-111">A query executed by the database engine is often more efficient because of the database indexes.</span></span>  
  
## <a name="local-execution"></a><span data-ttu-id="06746-112">本機執行</span><span class="sxs-lookup"><span data-stu-id="06746-112">Local Execution</span></span>  

 <span data-ttu-id="06746-113">在其他情況下，您可能會想要擁有本機快取中的完整一組相關實體 (Entity)。</span><span class="sxs-lookup"><span data-stu-id="06746-113">In other situations, you might want to have the complete set of related entities in the local cache.</span></span> <span data-ttu-id="06746-114">因此，<xref:System.Data.Linq.EntitySet%601> 提供 <xref:System.Data.Linq.EntitySet%601.Load%2A> 方法，可以明確載入 <xref:System.Data.Linq.EntitySet%601> 的所有成員。</span><span class="sxs-lookup"><span data-stu-id="06746-114">For this purpose, <xref:System.Data.Linq.EntitySet%601> provides the <xref:System.Data.Linq.EntitySet%601.Load%2A> method to explicitly load all the members of the <xref:System.Data.Linq.EntitySet%601>.</span></span>  
  
 <span data-ttu-id="06746-115">如果已載入 <xref:System.Data.Linq.EntitySet%601>，則會在本機執行後續查詢。</span><span class="sxs-lookup"><span data-stu-id="06746-115">If an <xref:System.Data.Linq.EntitySet%601> is already loaded, subsequent queries are executed locally.</span></span> <span data-ttu-id="06746-116">這種方法有兩項優點：</span><span class="sxs-lookup"><span data-stu-id="06746-116">This approach helps in two ways:</span></span>  
  
- <span data-ttu-id="06746-117">如果必須在本機或多次使用完整集合，則可以避免遠端查詢和相關的延遲時間。</span><span class="sxs-lookup"><span data-stu-id="06746-117">If the complete set must be used locally or multiple times, you can avoid remote queries and associated latencies.</span></span>  
  
- <span data-ttu-id="06746-118">實體可以序列化為完整實體。</span><span class="sxs-lookup"><span data-stu-id="06746-118">The entity can be serialized as a complete entity.</span></span>  
  
 <span data-ttu-id="06746-119">下列程式碼片段說明如何取得本機執行：</span><span class="sxs-lookup"><span data-stu-id="06746-119">The following code fragment illustrates how local execution can be obtained:</span></span>  
  
 [!code-csharp[DLinqQueryConcepts#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#8)]
 [!code-vb[DLinqQueryConcepts#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#8)]  
  
## <a name="comparison"></a><span data-ttu-id="06746-120">比較</span><span class="sxs-lookup"><span data-stu-id="06746-120">Comparison</span></span>  

 <span data-ttu-id="06746-121">這兩個功能可提供強大的選項組合：遠端執行適用於大型集合，而本機執行則適用於小型集合或需要完整集合之處。</span><span class="sxs-lookup"><span data-stu-id="06746-121">These two capabilities provide a powerful combination of options: remote execution for large collections and local execution for small collections or where the complete collection is needed.</span></span> <span data-ttu-id="06746-122">您可以透過 <xref:System.Linq.IQueryable> 實作遠端執行，而本機執行則是根據記憶體中 <xref:System.Collections.Generic.IEnumerable%601> 集合來實作。</span><span class="sxs-lookup"><span data-stu-id="06746-122">You implement remote execution through <xref:System.Linq.IQueryable>, and local execution against an in-memory <xref:System.Collections.Generic.IEnumerable%601> collection.</span></span> <span data-ttu-id="06746-123">若要強制執行本機執行 (也就是 <xref:System.Collections.Generic.IEnumerable%601>) ，請參閱 [將類型轉換為泛型 IEnumerable](convert-a-type-to-a-generic-ienumerable.md)。</span><span class="sxs-lookup"><span data-stu-id="06746-123">To force local execution (that is, <xref:System.Collections.Generic.IEnumerable%601>), see [Convert a Type to a Generic IEnumerable](convert-a-type-to-a-generic-ienumerable.md).</span></span>  
  
### <a name="queries-against-unordered-sets"></a><span data-ttu-id="06746-124">對未排序集合進行查詢</span><span class="sxs-lookup"><span data-stu-id="06746-124">Queries Against Unordered Sets</span></span>  

 <span data-ttu-id="06746-125">請注意執行的本機集合 <xref:System.Collections.Generic.List%601> 與提供遠端查詢的集合，該集合會針對關係資料庫中未 *排序* 的集合執行。</span><span class="sxs-lookup"><span data-stu-id="06746-125">Note the important difference between a local collection that implements <xref:System.Collections.Generic.List%601> and a collection that provides remote queries executed against *unordered sets* in a relational database.</span></span> <span data-ttu-id="06746-126"><xref:System.Collections.Generic.List%601> 方法 (如使用索引值的方法) 需要清單語意 (Semantics)，而這一般無法透過對未排序集合的遠端查詢來取得。</span><span class="sxs-lookup"><span data-stu-id="06746-126"><xref:System.Collections.Generic.List%601> methods such as those that use index values require list semantics, which typically cannot be obtained through a remote query against an unordered set.</span></span> <span data-ttu-id="06746-127">因此，這類方法會隱含地載入 <xref:System.Data.Linq.EntitySet%601>，以允許進行本機執行。</span><span class="sxs-lookup"><span data-stu-id="06746-127">For this reason, such methods implicitly load the <xref:System.Data.Linq.EntitySet%601> to allow local execution.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="06746-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="06746-128">See also</span></span>

- [<span data-ttu-id="06746-129">查詢概念</span><span class="sxs-lookup"><span data-stu-id="06746-129">Query Concepts</span></span>](query-concepts.md)

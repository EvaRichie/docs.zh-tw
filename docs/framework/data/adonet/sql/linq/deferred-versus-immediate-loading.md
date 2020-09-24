---
title: 延後和立即載入的比較
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
ms.openlocfilehash: 4e2cb7c90eb703985cbb1b8673522a9e253564d0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164294"
---
# <a name="deferred-versus-immediate-loading"></a><span data-ttu-id="1d003-102">延後和立即載入的比較</span><span class="sxs-lookup"><span data-stu-id="1d003-102">Deferred versus Immediate Loading</span></span>

<span data-ttu-id="1d003-103">當您查詢物件時，實際上只擷取了所要求的物件。</span><span class="sxs-lookup"><span data-stu-id="1d003-103">When you query for an object, you actually retrieve only the object you requested.</span></span> <span data-ttu-id="1d003-104">*相關*物件不會同時自動提取。</span><span class="sxs-lookup"><span data-stu-id="1d003-104">The *related* objects are not automatically fetched at the same time.</span></span> <span data-ttu-id="1d003-105"> (需詳細資訊，請參閱 [跨關聯性查詢](querying-across-relationships.md)。 ) 您無法看到尚未載入相關物件的事實，因為嘗試存取它們會產生可抓取這些物件的要求。</span><span class="sxs-lookup"><span data-stu-id="1d003-105">(For more information, see [Querying Across Relationships](querying-across-relationships.md).) You cannot see the fact that the related objects are not already loaded, because an attempt to access them produces a request that retrieves them.</span></span>  
  
 <span data-ttu-id="1d003-106">例如，您可能想要查詢一組特定的訂單，然後只偶爾將電子郵件通知傳送給特定客戶。</span><span class="sxs-lookup"><span data-stu-id="1d003-106">For example, you might want to query for a particular set of orders and then only occasionally send an email notification to particular customers.</span></span> <span data-ttu-id="1d003-107">因此並不需要一開始就擷取每筆訂單的所有客戶資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-107">You would not necessarily need initially to retrieve all customer data with every order.</span></span> <span data-ttu-id="1d003-108">您可以使用延後載入，將確切資訊的擷取延後至絕對需要的時候才進行擷取。</span><span class="sxs-lookup"><span data-stu-id="1d003-108">You can use deferred loading to defer retrieval of extra information until you absolutely have to.</span></span> <span data-ttu-id="1d003-109">請考慮下列範例：</span><span class="sxs-lookup"><span data-stu-id="1d003-109">Consider the following example:</span></span>  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 <span data-ttu-id="1d003-110">反之亦然。</span><span class="sxs-lookup"><span data-stu-id="1d003-110">The opposite might also be true.</span></span> <span data-ttu-id="1d003-111">您的應用程式可能需要同時檢視客戶和訂單資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-111">You might have an application that has to view customer and order data at the same time.</span></span> <span data-ttu-id="1d003-112">您知道您需要這兩組資料，</span><span class="sxs-lookup"><span data-stu-id="1d003-112">You know you need both sets of data.</span></span> <span data-ttu-id="1d003-113">另外，一旦您取得結果，應用程式就需要每位客戶的訂單資訊。</span><span class="sxs-lookup"><span data-stu-id="1d003-113">You know your application needs order information for each customer as soon as you get the results.</span></span> <span data-ttu-id="1d003-114">但您不想要針對每位客戶的訂單分別送出個別查詢，</span><span class="sxs-lookup"><span data-stu-id="1d003-114">You would not want to submit individual queries for orders for every customer.</span></span> <span data-ttu-id="1d003-115">您實際想做的是在擷取客戶資料時一起擷取訂單資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-115">What you really want is to retrieve the order data together with the customers.</span></span>  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 <span data-ttu-id="1d003-116">您也可以建立叉積查詢，並將資料的所有相對位元都擷取為一個大型投影 (Projection)，以利用查詢來聯結 (Join) 客戶和訂單。</span><span class="sxs-lookup"><span data-stu-id="1d003-116">You can also join customers and orders in a query by forming the cross-product and retrieving all the relative bits of data as one large projection.</span></span> <span data-ttu-id="1d003-117">但這些結果不是實體 (Entity) </span><span class="sxs-lookup"><span data-stu-id="1d003-117">But these results are not entities.</span></span> <span data-ttu-id="1d003-118"> (需詳細資訊，請參閱 [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)) 。</span><span class="sxs-lookup"><span data-stu-id="1d003-118">(For more information, see [The LINQ to SQL Object Model](the-linq-to-sql-object-model.md)).</span></span> <span data-ttu-id="1d003-119">實體是具有識別 (Identity) 而且可以修改的物件，而上述結果卻是無法變更和持續 (Persist) 的投影。</span><span class="sxs-lookup"><span data-stu-id="1d003-119">Entities are objects that have identity and that you can modify, whereas these results would be projections that cannot be changed and persisted.</span></span> <span data-ttu-id="1d003-120">更糟的是，因為每位客戶會以簡維聯結輸出重複每筆訂單，所以您會擷取到許多多餘的資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-120">Even worse, you would be retrieving lots of redundant data as each customer repeats for each order in the flattened join output.</span></span>  
  
 <span data-ttu-id="1d003-121">您實際需要的是一種可以同時擷取一組相關物件的方式。</span><span class="sxs-lookup"><span data-stu-id="1d003-121">What you really need is a way to retrieve a set of related objects at the same time.</span></span> <span data-ttu-id="1d003-122">而這組物件是圖形的明確部分，因此您擷取到的資料就會是您所需要的資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-122">The set is a delineated section of a graph so that you would never be retrieving more or less than was necessary for your intended use.</span></span> <span data-ttu-id="1d003-123">基於這個目的， [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供 <xref:System.Data.Linq.DataLoadOptions> 立即載入物件模型的區域。</span><span class="sxs-lookup"><span data-stu-id="1d003-123">For this purpose, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] provides <xref:System.Data.Linq.DataLoadOptions> for immediate loading of a region of your object model.</span></span> <span data-ttu-id="1d003-124">方法如下：</span><span class="sxs-lookup"><span data-stu-id="1d003-124">Methods include:</span></span>  
  
- <span data-ttu-id="1d003-125"><xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> 方法，可以立即載入與主要目標相關的資料。</span><span class="sxs-lookup"><span data-stu-id="1d003-125">The  <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> method, to immediately load data related to the main target.</span></span>  
  
- <span data-ttu-id="1d003-126"><xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> 方法，可以篩選針對特定關聯性 (Relationship) 所擷取的物件。</span><span class="sxs-lookup"><span data-stu-id="1d003-126">The <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> method, to filter objects retrieved for a particular relationship.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1d003-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d003-127">See also</span></span>

- [<span data-ttu-id="1d003-128">查詢概念</span><span class="sxs-lookup"><span data-stu-id="1d003-128">Query Concepts</span></span>](query-concepts.md)

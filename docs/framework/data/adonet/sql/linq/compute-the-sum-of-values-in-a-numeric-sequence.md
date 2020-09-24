---
title: 如何：計算數值序列中各值的總和
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
ms.openlocfilehash: 3d160e2cce5f3e0a7eea305657260b6fa4ded7fe
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164437"
---
# <a name="compute-the-sum-of-values-in-a-numeric-sequence"></a><span data-ttu-id="712a9-102">如何：計算數值序列中各值的總和</span><span class="sxs-lookup"><span data-stu-id="712a9-102">Compute the Sum of Values in a Numeric Sequence</span></span>

<span data-ttu-id="712a9-103">使用 <xref:System.Linq.Enumerable.Sum%2A> 運算子，可以計算序列中的數值總和。</span><span class="sxs-lookup"><span data-stu-id="712a9-103">Use the <xref:System.Linq.Enumerable.Sum%2A> operator to compute the sum of numeric values in a sequence.</span></span>  
  
 <span data-ttu-id="712a9-104">請注意，`Sum` 中的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 運算子有下列特性：</span><span class="sxs-lookup"><span data-stu-id="712a9-104">Note the following characteristics of the `Sum` operator in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:</span></span>  
  
- <span data-ttu-id="712a9-105">標準查詢運算子的彙總 (Aggregate) 運算子 `Sum` 會將空序列或只包含 null 的序列評估為零。</span><span class="sxs-lookup"><span data-stu-id="712a9-105">The Standard Query Operator aggregate operator `Sum` evaluates to zero for an empty sequence or a sequence that contains only nulls.</span></span> <span data-ttu-id="712a9-106">在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，SQL 的語意 (Semantics) 則不變。</span><span class="sxs-lookup"><span data-stu-id="712a9-106">In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], the semantics of SQL are left unchanged.</span></span> <span data-ttu-id="712a9-107">因此，`Sum` 會將空序列或只包含 null 的序列評估為 null，而不是零。</span><span class="sxs-lookup"><span data-stu-id="712a9-107">For this reason, `Sum` evaluates to null instead of to zero for an empty sequence or for a sequence that contains only nulls.</span></span>  
  
- <span data-ttu-id="712a9-108">SQL 對中繼結果的限制會套用至 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的彙總。</span><span class="sxs-lookup"><span data-stu-id="712a9-108">SQL limitations on intermediate results apply to aggregates in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].</span></span> <span data-ttu-id="712a9-109">32位整數數量的總和不是使用64位結果來計算，而且可能會發生溢位 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] `Sum` 。</span><span class="sxs-lookup"><span data-stu-id="712a9-109">Sum of 32-bit integer quantities is not computed by using 64-bit results, and overflow can occur for the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] translation of `Sum`.</span></span> <span data-ttu-id="712a9-110">即使標準查詢運算子的實作未使對應的記憶體中序列發生溢位，這個可能性還是存在。</span><span class="sxs-lookup"><span data-stu-id="712a9-110">This possibility exists even if the Standard Query Operator implementation does not cause an overflow for the corresponding in-memory sequence.</span></span>  
  
## <a name="example"></a><span data-ttu-id="712a9-111">範例</span><span class="sxs-lookup"><span data-stu-id="712a9-111">Example</span></span>  

 <span data-ttu-id="712a9-112">下列範例會找出 `Order` 資料表中所有訂單的總運費。</span><span class="sxs-lookup"><span data-stu-id="712a9-112">The following example finds the total freight of all orders in the `Order` table.</span></span>  
  
 <span data-ttu-id="712a9-113">如果您對 Northwind 範例資料庫執行這個查詢，則輸出為：`64942.6900`。</span><span class="sxs-lookup"><span data-stu-id="712a9-113">If you run this query against the Northwind sample database, the output is: `64942.6900`.</span></span>  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## <a name="example"></a><span data-ttu-id="712a9-114">範例</span><span class="sxs-lookup"><span data-stu-id="712a9-114">Example</span></span>  

 <span data-ttu-id="712a9-115">下列範例會找出所有產品的訂購單位總數。</span><span class="sxs-lookup"><span data-stu-id="712a9-115">The following example finds the total number of units on order for all products.</span></span>  
  
 <span data-ttu-id="712a9-116">如果您對 Northwind 範例資料庫執行這個查詢，則輸出為：`780`。</span><span class="sxs-lookup"><span data-stu-id="712a9-116">If you run this query against the Northwind sample database, the output is: `780`.</span></span>  
  
 <span data-ttu-id="712a9-117">請注意，因為 `short` 沒有適用於 short 型別的多載，所以必須轉換 (Cast) `UnitsOnOrder` 型別 (例如，`Sum`)。</span><span class="sxs-lookup"><span data-stu-id="712a9-117">Note that you must cast `short` types (for example, `UnitsOnOrder`) because `Sum` has no overload for short types.</span></span>  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## <a name="see-also"></a><span data-ttu-id="712a9-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="712a9-118">See also</span></span>

- [<span data-ttu-id="712a9-119">彙總查詢</span><span class="sxs-lookup"><span data-stu-id="712a9-119">Aggregate Queries</span></span>](aggregate-queries.md)
- [<span data-ttu-id="712a9-120">下載範例資料庫</span><span class="sxs-lookup"><span data-stu-id="712a9-120">Downloading Sample Databases</span></span>](downloading-sample-databases.md)

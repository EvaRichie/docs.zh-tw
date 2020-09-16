---
title: SKIP (Entity SQL)
ms.date: 03/30/2017
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
ms.openlocfilehash: 68f54dc5118e09d78f98c687e8a44def43b45c7d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540988"
---
# <a name="skip-entity-sql"></a><span data-ttu-id="89580-102">SKIP (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="89580-102">SKIP (Entity SQL)</span></span>

<span data-ttu-id="89580-103">您可以在 ORDER BY 子句中使用 SKIP 子句執行實際分頁。</span><span class="sxs-lookup"><span data-stu-id="89580-103">You can perform physical paging by using the SKIP sub-clause in the ORDER BY clause.</span></span> <span data-ttu-id="89580-104">SKIP 不可單獨使用於 ORDER BY 子句之外。</span><span class="sxs-lookup"><span data-stu-id="89580-104">SKIP cannot be used separately from the ORDER BY clause.</span></span>

## <a name="syntax"></a><span data-ttu-id="89580-105">語法</span><span class="sxs-lookup"><span data-stu-id="89580-105">Syntax</span></span>

```sql
[ SKIP n ]
```

## <a name="arguments"></a><span data-ttu-id="89580-106">引數</span><span class="sxs-lookup"><span data-stu-id="89580-106">Arguments</span></span>

`n` \
<span data-ttu-id="89580-107">要略過的項目數目。</span><span class="sxs-lookup"><span data-stu-id="89580-107">The number of items to skip.</span></span>

## <a name="remarks"></a><span data-ttu-id="89580-108">備註</span><span class="sxs-lookup"><span data-stu-id="89580-108">Remarks</span></span>

<span data-ttu-id="89580-109">如果 ORDER BY 子句中有 SKIP 運算式次子句，結果將會依據排序規格排序，而且結果集將會包括從 SKIP 運算式後面一個資料列開始的資料列。</span><span class="sxs-lookup"><span data-stu-id="89580-109">If a SKIP expression sub-clause is present in an ORDER BY clause, the results will be sorted according the sort specification and the result set will include rows starting from the next row immediately after the SKIP expression.</span></span> <span data-ttu-id="89580-110">例如，SKIP 5 將會略過前五個資料列，並且傳回從第六個資料列以後的資料列。</span><span class="sxs-lookup"><span data-stu-id="89580-110">For example, SKIP 5 will skip the first five rows and return from the sixth row forward.</span></span>

> [!NOTE]
> <span data-ttu-id="89580-111">如果 TOP 修飾詞和 SKIP 之子句兩者出現在同一個查詢運算式中，則 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢會變成無效。</span><span class="sxs-lookup"><span data-stu-id="89580-111">An [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query is invalid if both the TOP modifier and the SKIP sub-clause are present in the same query expression.</span></span> <span data-ttu-id="89580-112">請將 TOP 運算式變更為 LIMIT 運算式來重新撰寫此查詢。</span><span class="sxs-lookup"><span data-stu-id="89580-112">The query should be rewritten by changing the TOP expression to the LIMIT expression.</span></span>

> [!NOTE]
> <span data-ttu-id="89580-113">在 SQL Server 2000 中，在非索引鍵資料行上使用 SKIP with ORDER BY 可能會傳回不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="89580-113">In SQL Server 2000, using SKIP with ORDER BY on non-key columns might return incorrect results.</span></span> <span data-ttu-id="89580-114">如果非索引鍵資料行中有重複的資料，可能會略過超過所指定數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="89580-114">More than the specified number of rows might be skipped if the non-key column has duplicate data in it.</span></span> <span data-ttu-id="89580-115">這是因為略過如何轉譯 SQL Server 2000 的略過。</span><span class="sxs-lookup"><span data-stu-id="89580-115">This is due to how SKIP is translated for SQL Server 2000.</span></span> <span data-ttu-id="89580-116">舉例來講，在以下程式碼中，如果 `E.NonKeyColumn` 中有重複的值，就會略過超過五個資料行：</span><span class="sxs-lookup"><span data-stu-id="89580-116">For example, in the following code more than five rows might be skipped if `E.NonKeyColumn` has duplicate values:</span></span>
>
> ```sql
> SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L
> ```

<span data-ttu-id="89580-117">[!INCLUDE[esql](../../../../../../includes/esql-md.md)][如何：逐頁查看查詢結果](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))中的查詢會使用 ORDER BY 運算子搭配 SKIP 來指定 SELECT 語句中傳回之物件所使用的排序次序。</span><span class="sxs-lookup"><span data-stu-id="89580-117">The [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query in [How to: Page Through Query Results](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100)) uses the ORDER BY operator with SKIP to specify the sort order used on objects returned in a SELECT statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="89580-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="89580-118">See also</span></span>

- [<span data-ttu-id="89580-119">ORDER BY</span><span class="sxs-lookup"><span data-stu-id="89580-119">ORDER BY</span></span>](order-by-entity-sql.md)
- <span data-ttu-id="89580-120">[如何：逐頁檢視查詢結果](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="89580-120">[How to: Page Through Query Results](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))</span></span>
- [<span data-ttu-id="89580-121">分頁</span><span class="sxs-lookup"><span data-stu-id="89580-121">Paging</span></span>](paging-entity-sql.md)
- [<span data-ttu-id="89580-122">返回頁首</span><span class="sxs-lookup"><span data-stu-id="89580-122">TOP</span></span>](top-entity-sql.md)

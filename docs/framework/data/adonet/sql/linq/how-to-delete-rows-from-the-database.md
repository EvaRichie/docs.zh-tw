---
title: 如何：從資料庫刪除資料列
description: 瞭解如何從資料表相關的集合中移除 LINQ to SQL 物件，以刪除資料庫中的資料列。 LINQ to SQL 會將刪除轉換成 SQL DELETE 命令。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2144c99b-8055-4080-a5c6-1ea14335e2a3
ms.openlocfilehash: d08621e834961e1db9312cac36bd2e69133142b5
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286387"
---
# <a name="how-to-delete-rows-from-the-database"></a><span data-ttu-id="7a5c8-104">如何：從資料庫刪除資料列</span><span class="sxs-lookup"><span data-stu-id="7a5c8-104">How to: Delete Rows From the Database</span></span>

<span data-ttu-id="7a5c8-105">您可以從資料表相關的集合中移除對應的物件，藉以刪除資料庫中的資料列 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-105">You can delete rows in a database by removing the corresponding [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] objects from their table-related collection.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]<span data-ttu-id="7a5c8-106">將您的變更轉譯為適當的 SQL `DELETE` 命令。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-106">translates your changes to the appropriate SQL `DELETE` commands.</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="7a5c8-107">不支援或辨識串聯 (Cascade) 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-107">does not support or recognize cascade-delete operations.</span></span> <span data-ttu-id="7a5c8-108">如果您要刪除有條件約束之資料表中的資料列，必須完成下列其中一項工作：</span><span class="sxs-lookup"><span data-stu-id="7a5c8-108">If you want to delete a row in a table that has constraints against it, you must complete either of the following tasks:</span></span>

- <span data-ttu-id="7a5c8-109">在資料庫的外部索引鍵條件約束中設定 `ON DELETE CASCADE` 規則。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-109">Set the `ON DELETE CASCADE` rule in the foreign-key constraint in the database.</span></span>

- <span data-ttu-id="7a5c8-110">使用您自己的程式碼，先刪除使父物件無法刪除的子物件。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-110">Use your own code to first delete the child objects that prevent the parent object from being deleted.</span></span>

 <span data-ttu-id="7a5c8-111">否則，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-111">Otherwise, an exception is thrown.</span></span> <span data-ttu-id="7a5c8-112">請參閱本主題稍後的第二個程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-112">See the second code example later in this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5c8-113">您可以覆寫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 預設方法，以執行 `Insert`、`Update` 和 `Delete` 資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-113">You can override [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] default methods for `Insert`, `Update`, and `Delete` database operations.</span></span> <span data-ttu-id="7a5c8-114">如需詳細資訊，請參閱[自訂插入、更新和刪除作業](customizing-insert-update-and-delete-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-114">For more information, see [Customizing Insert, Update, and Delete Operations](customizing-insert-update-and-delete-operations.md).</span></span>
>
> <span data-ttu-id="7a5c8-115">使用 Visual Studio 的開發人員可以使用物件關聯式設計工具，針對相同的目的來開發預存程式。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-115">Developers using Visual Studio can use the Object Relational Designer to develop stored procedures for the same purpose.</span></span>

<span data-ttu-id="7a5c8-116">下列步驟假設一個有效的 <xref:System.Data.Linq.DataContext> 會將您連接至 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-116">The following steps assume that a valid <xref:System.Data.Linq.DataContext> connects you to the Northwind database.</span></span> <span data-ttu-id="7a5c8-117">如需詳細資訊，請參閱[如何：連接到資料庫](how-to-connect-to-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-117">For more information, see [How to: Connect to a Database](how-to-connect-to-a-database.md).</span></span>

### <a name="to-delete-a-row-in-the-database"></a><span data-ttu-id="7a5c8-118">若要從資料庫刪除資料列</span><span class="sxs-lookup"><span data-stu-id="7a5c8-118">To delete a row in the database</span></span>

1. <span data-ttu-id="7a5c8-119">查詢資料庫，以找出要刪除的資料列。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-119">Query the database for the row to be deleted.</span></span>

2. <span data-ttu-id="7a5c8-120">呼叫 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-120">Call the <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> method.</span></span>

3. <span data-ttu-id="7a5c8-121">將變更提交至資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-121">Submit the change to the database.</span></span>

## <a name="example"></a><span data-ttu-id="7a5c8-122">範例</span><span class="sxs-lookup"><span data-stu-id="7a5c8-122">Example</span></span>

<span data-ttu-id="7a5c8-123">下列第一個程式碼範例會查詢資料庫中屬於訂單 #11000 的訂單明細、將這些訂單明細標示為刪除，然後將這些變更送出至資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-123">This first code example queries the database for order details that belong to Order #11000, marks these order details for deletion, and submits these changes to the database.</span></span>

[!code-csharp[System.Data.Linq.Table#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#3)]
[!code-vb[System.Data.Linq.Table#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#3)]

## <a name="example"></a><span data-ttu-id="7a5c8-124">範例</span><span class="sxs-lookup"><span data-stu-id="7a5c8-124">Example</span></span>

<span data-ttu-id="7a5c8-125">在下列第二個範例中，目標是要移除某張訂單 (#10250)。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-125">In this second example, the objective is to remove an order (#10250).</span></span> <span data-ttu-id="7a5c8-126">這段程式碼會先檢查 `OrderDetails` 資料表，查看要移除的訂單是否在該處有子系。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-126">The code first examines the `OrderDetails` table to see whether the order to be removed has children there.</span></span> <span data-ttu-id="7a5c8-127">如果訂單有子系，則會先將子系標示為移除，再將訂單標示為移除。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-127">If the order has children, first the children and then the order are marked for removal.</span></span> <span data-ttu-id="7a5c8-128"><xref:System.Data.Linq.DataContext> 會將實際的刪除放置在正確的訂單中，使傳送到資料庫的刪除命令得以遵守資料庫條件約束。</span><span class="sxs-lookup"><span data-stu-id="7a5c8-128">The <xref:System.Data.Linq.DataContext> puts the actual deletes in correct order so that delete commands sent to the database abide by the database constraints.</span></span>

[!code-csharp[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCascadeWorkaround/cs/Program.cs#1)]
[!code-vb[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCascadeWorkaround/vb/Module1.vb#1)]

## <a name="see-also"></a><span data-ttu-id="7a5c8-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7a5c8-129">See also</span></span>

- [<span data-ttu-id="7a5c8-130">如何：管理變更衝突</span><span class="sxs-lookup"><span data-stu-id="7a5c8-130">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)
- [<span data-ttu-id="7a5c8-131">如何：指派用來執行更新、插入和刪除的預存程序 (O/R 設計工具)</span><span class="sxs-lookup"><span data-stu-id="7a5c8-131">How to: Assign stored procedures to perform updates, inserts, and deletes (O/R Designer)</span></span>](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [<span data-ttu-id="7a5c8-132">變更資料和提交</span><span class="sxs-lookup"><span data-stu-id="7a5c8-132">Making and Submitting Data Changes</span></span>](making-and-submitting-data-changes.md)

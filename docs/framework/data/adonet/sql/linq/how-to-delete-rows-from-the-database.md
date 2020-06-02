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
# <a name="how-to-delete-rows-from-the-database"></a>如何：從資料庫刪除資料列

您可以從資料表相關的集合中移除對應的物件，藉以刪除資料庫中的資料列 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]將您的變更轉譯為適當的 SQL `DELETE` 命令。

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支援或辨識串聯 (Cascade) 刪除作業。 如果您要刪除有條件約束之資料表中的資料列，必須完成下列其中一項工作：

- 在資料庫的外部索引鍵條件約束中設定 `ON DELETE CASCADE` 規則。

- 使用您自己的程式碼，先刪除使父物件無法刪除的子物件。

 否則，會擲回例外狀況。 請參閱本主題稍後的第二個程式碼範例。

> [!NOTE]
> 您可以覆寫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 預設方法，以執行 `Insert`、`Update` 和 `Delete` 資料庫作業。 如需詳細資訊，請參閱[自訂插入、更新和刪除作業](customizing-insert-update-and-delete-operations.md)。
>
> 使用 Visual Studio 的開發人員可以使用物件關聯式設計工具，針對相同的目的來開發預存程式。

下列步驟假設一個有效的 <xref:System.Data.Linq.DataContext> 會將您連接至 Northwind 資料庫。 如需詳細資訊，請參閱[如何：連接到資料庫](how-to-connect-to-a-database.md)。

### <a name="to-delete-a-row-in-the-database"></a>若要從資料庫刪除資料列

1. 查詢資料庫，以找出要刪除的資料列。

2. 呼叫 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> 方法。

3. 將變更提交至資料庫。

## <a name="example"></a>範例

下列第一個程式碼範例會查詢資料庫中屬於訂單 #11000 的訂單明細、將這些訂單明細標示為刪除，然後將這些變更送出至資料庫。

[!code-csharp[System.Data.Linq.Table#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#3)]
[!code-vb[System.Data.Linq.Table#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#3)]

## <a name="example"></a>範例

在下列第二個範例中，目標是要移除某張訂單 (#10250)。 這段程式碼會先檢查 `OrderDetails` 資料表，查看要移除的訂單是否在該處有子系。 如果訂單有子系，則會先將子系標示為移除，再將訂單標示為移除。 <xref:System.Data.Linq.DataContext> 會將實際的刪除放置在正確的訂單中，使傳送到資料庫的刪除命令得以遵守資料庫條件約束。

[!code-csharp[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCascadeWorkaround/cs/Program.cs#1)]
[!code-vb[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCascadeWorkaround/vb/Module1.vb#1)]

## <a name="see-also"></a>另請參閱

- [如何：管理變更衝突](how-to-manage-change-conflicts.md)
- [如何：指派用來執行更新、插入和刪除的預存程序 (O/R 設計工具)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [變更資料和提交](making-and-submitting-data-changes.md)

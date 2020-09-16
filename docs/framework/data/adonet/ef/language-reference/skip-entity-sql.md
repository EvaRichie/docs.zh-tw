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
# <a name="skip-entity-sql"></a>SKIP (Entity SQL)

您可以在 ORDER BY 子句中使用 SKIP 子句執行實際分頁。 SKIP 不可單獨使用於 ORDER BY 子句之外。

## <a name="syntax"></a>語法

```sql
[ SKIP n ]
```

## <a name="arguments"></a>引數

`n` \
要略過的項目數目。

## <a name="remarks"></a>備註

如果 ORDER BY 子句中有 SKIP 運算式次子句，結果將會依據排序規格排序，而且結果集將會包括從 SKIP 運算式後面一個資料列開始的資料列。 例如，SKIP 5 將會略過前五個資料列，並且傳回從第六個資料列以後的資料列。

> [!NOTE]
> 如果 TOP 修飾詞和 SKIP 之子句兩者出現在同一個查詢運算式中，則 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢會變成無效。 請將 TOP 運算式變更為 LIMIT 運算式來重新撰寫此查詢。

> [!NOTE]
> 在 SQL Server 2000 中，在非索引鍵資料行上使用 SKIP with ORDER BY 可能會傳回不正確的結果。 如果非索引鍵資料行中有重複的資料，可能會略過超過所指定數目的資料行。 這是因為略過如何轉譯 SQL Server 2000 的略過。 舉例來講，在以下程式碼中，如果 `E.NonKeyColumn` 中有重複的值，就會略過超過五個資料行：
>
> ```sql
> SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L
> ```

[!INCLUDE[esql](../../../../../../includes/esql-md.md)][如何：逐頁查看查詢結果](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))中的查詢會使用 ORDER BY 運算子搭配 SKIP 來指定 SELECT 語句中傳回之物件所使用的排序次序。

## <a name="see-also"></a>另請參閱

- [ORDER BY](order-by-entity-sql.md)
- [如何：逐頁檢視查詢結果](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [分頁](paging-entity-sql.md)
- [返回頁首](top-entity-sql.md)

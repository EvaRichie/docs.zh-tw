---
title: 如何：使用 Finally 區塊
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- exceptions, try/catch blocks
- exceptions, finally blocks
- try/catch blocks
- finally blocks
- ArgumentOutOfRangeException class
ms.assetid: 4b9c0137-04af-4468-91d1-b9014df8ddd2
ms.openlocfilehash: 8bc36ce9a755762bb5159a27f9ef5699b2992f0e
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828032"
---
# <a name="how-to-use-finally-blocks"></a>如何使用 finally 區塊

發生例外狀況時，執行會停止，並將控制權交給適當的例外狀況處理常式。 這通常表示會略過您預期要執行的程式碼行。 某些資源清除作業 (例如關閉檔案) 即使擲回例外狀況也必須執行。 若要這樣做，您可以使用 `finally` 區塊。 `finally` 區塊永遠會執行，而不論是否擲回例外狀況。

下列程式碼範例使用 `try`/`catch` 區塊來攔截 <xref:System.ArgumentOutOfRangeException>。 `Main` 方法會建立兩個陣列，並嘗試將其中一個陣列複製到另一個陣列。 此動作會產生 <xref:System.ArgumentOutOfRangeException>，並會將錯誤寫入主控台。 不論複製動作的結果為何，`finally` 區塊都會執行。

[!code-cpp[CodeTryCatchFinallyExample#3](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CPP/source2.cpp#3)]
[!code-csharp[CodeTryCatchFinallyExample#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CS/source2.cs#3)]
[!code-vb[CodeTryCatchFinallyExample#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeTryCatchFinallyExample/VB/source2.vb#3)]  

## <a name="see-also"></a>請參閱

- [例外狀況](index.md)

---
description: volatile - C# 參考
title: volatile - C# 參考
ms.date: 10/24/2018
f1_keywords:
- volatile_CSharpKeyword
- volatile
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
ms.openlocfilehash: bb89e99e8e28ff1e263817f498619dbfae700a50
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89141695"
---
# <a name="volatile-c-reference"></a>volatile (C# 參考)

`volatile` 關鍵字指出某個欄位可能是由同時執行的多個執行緒所修改。 編譯器、執行階段系統，甚至硬體都有可能基於效能因素，而重新排列對記憶體位置的讀取和寫入。 宣告為 `volatile` 的欄位不受限於這些最佳化考量。 加入 `volatile` 修飾詞可確保所有的執行緒都會依執行寫入的順序，觀察任何其他執行緒所執行的暫時性寫入。 不保證 volatile 寫入的單一總排序如所有執行緒的執行中所示。

`volatile` 關鍵字可以套用至下列類型的欄位：

- 參考型別。
- 指標類型 (在不安全的內容中)。 請注意，雖然指標本身可為 volatile，但它所指向的物件不得為 volatile。 換句話說，您無法將指標宣告為 volatile。
- 簡單型別，例如 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`char`、`float` 與 `bool`。
- 使用下列其中一個基底類型的 `enum` 型別：`byte`、`sbyte`、`short`、`ushort`、`int` 或 `uint`。
- 已知為參考型別的泛型型別參數。
- <xref:System.IntPtr> 和 <xref:System.UIntPtr>。

其他型別，包括 `double` 與 `long`，不能標示為 `volatile`，因為對這些型別之欄位的讀取和寫入不保證是不可部分完成。 若要保護對這些欄位類型的多執行緒存取，請使用 <xref:System.Threading.Interlocked> 類別成員或使用語句來保護存取 [`lock`](lock-statement.md) 。

`volatile` 關鍵字只能套用至 `class` 或 `struct` 的欄位。 區域變數不可以宣告為 `volatile`。

## <a name="example"></a>範例

下列範例示範如何將公用欄位變數宣告為 `volatile`。

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Declaration)]

下列範例示範如何建立和使用輔助或背景工作執行緒，以運用主執行緒的輔助或背景工作執行緒來執行平行處理。 如需有關多執行緒的詳細資訊，請參閱 [Managed 執行緒處理](../../../standard/threading/index.md)。

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Volatile)]

將 `volatile` 修飾詞新增到 `_shouldStop` 的宣告之後，您將會一律取得相同的結果 (類似上述程式碼顯示的摘要)。 不過，如果 `_shouldStop` 成員上沒有修飾詞，則行為是無法預測的。 `DoWork` 方法可能會將成員存取最佳化，導致讀取過時的資料。 由於多執行緒程式設計的特性，過時讀取的數目是無法預測的。 程式不同次的執行會產生不同的結果。

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C# 語言規格：volatile 關鍵字](../../../../_csharplang/spec/classes.md#volatile-fields)
- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [修飾詞](index.md)
- [lock 語句](lock-statement.md)
- <xref:System.Threading.Interlocked>

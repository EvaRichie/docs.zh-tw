---
description: unchecked 關鍵字 - C# 參考
title: unchecked 關鍵字 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- unchecked_CSharpKeyword
- unchecked
helpviewer_keywords:
- unchecked keyword [C#]
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
ms.openlocfilehash: bb66639e3657b247b9ebcad1594daf1f57a5c76b
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89141981"
---
# <a name="unchecked-c-reference"></a>unchecked (C# 參考)

`unchecked` 關鍵字是用來抑制整數類型算術運算和轉換的溢位檢查。

在未檢查的內容中，如果運算式產生不在目的類型範圍內的值，則不會標示溢位。 例如，因為是在 `unchecked` 區塊或運算式中執行下列範例中的計算，所以會忽略整數結果太大的事實，而且 `int1` 會獲指派 -2,147,483,639 值。

[!code-csharp[csrefKeywordsChecked#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#5)]

如果移除 `unchecked` 環境，則會發生編譯錯誤。 因為運算式的所有項目都是常數，所以會在編譯時期偵測到溢位。

預設不會在編譯時期和執行階段檢查包含非常數項目的運算式。 如需啟用已檢查環境的資訊，請參閱 [checked](checked.md)。

因為檢查溢位需要一些時間，所以在沒有溢位危險的情況下使用未檢查的程式碼可能會改善效能。 不過，如果可能會發生溢位，則應該使用已檢查過的環境。

## <a name="example"></a>範例

這個範例示範如何使用 `unchecked` 關鍵字。

[!code-csharp[csrefKeywordsChecked#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#2)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [Checked 與 Unchecked](checked-and-unchecked.md)
- [檢查](checked.md)

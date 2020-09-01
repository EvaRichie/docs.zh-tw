---
description: break 陳述式 - C# 參考
title: break 陳述式 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- break
- break_CSharpKeyword
helpviewer_keywords:
- break keyword [C#]
ms.assetid: be2571ed-efb0-4965-b122-81e5b09db0b9
ms.openlocfilehash: 7fd05889f684f7a2282de8222e1195898dead5b9
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89134740"
---
# <a name="break-c-reference"></a>break (C# 參考)

`break` 陳述式會終止其所在的最接近封閉式迴圈或 [switch](./switch.md) 陳述式。 控制權會轉移到已終止陳述式之後的陳述式 (如果有的話)。

## <a name="example"></a>範例

在此範例中，條件式陳述式包含假設從 1 計算到 100 的計數器；不過，`break` 陳述式會在計算 4 次之後終止迴圈。

[!code-csharp[csrefKeywordsJump#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#1)]

## <a name="example"></a>範例

這個範例示範如何在 [switch](./switch.md) 陳述式中使用 `break`。

[!code-csharp[csrefKeywordsJump#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#2)]

如果您已輸入 `4`，則輸出會是︰

```console
Enter your selection (1, 2, or 3): 4
Sorry, invalid selection.
```

## <a name="example"></a>範例

在此範例中，`break` 陳述式是用來破壞內部巢狀迴圈，並將控制權返回外部迴圈。 在嵌套的迴圈中， _只_ 會傳回一個層級給控制項。

[!code-csharp[csrefKeywordsJump#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#7)]

## <a name="example"></a>範例

在此範例中， `break` 語句只會在迴圈的每次反覆運算期間用來中斷目前的分支。 迴圈本身不會受到 `break` 屬於 nested [switch](./switch.md) 語句之實例的影響。

[!code-csharp[csrefKeywordsJump#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#8)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](./index.md)
- [switch](./switch.md)

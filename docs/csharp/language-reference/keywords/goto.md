---
description: goto 陳述式 - C# 參考
title: goto 陳述式 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- goto_CSharpKeyword
- goto
helpviewer_keywords:
- goto keyword [C#]
ms.assetid: 2c03c9c1-8119-44ef-b740-fb3d287a42fe
ms.openlocfilehash: de95e477bd7e76f549130643c8d4b70a0e2f015c
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89128422"
---
# <a name="goto-c-reference"></a>goto (C# 參考)

`goto` 陳述式會將程式控制權直接轉移到標記陳述式。

`goto` 的一個常見用法是將控制權轉移到特定的切換案例標籤，或 `switch` 陳述式中的預設標籤。

`goto` 陳述式也適用於跳出深度巢狀的迴圈。

## <a name="example"></a>範例

下列範例示範如何在 [switch](switch.md) 陳述式中使用 `goto`。

[!code-csharp[csrefKeywordsJump#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#4)]

## <a name="example"></a>範例

下列範例示範如何使用 `goto` 跳出巢狀迴圈。

[!code-csharp[csrefKeywordsJump#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#5)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [goto 陳述式 (C++)](/cpp/cpp/goto-statement-cpp)

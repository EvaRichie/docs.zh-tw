---
description: '@ - C# 參考'
title: '@ - C# 參考'
ms.date: 02/09/2017
f1_keywords:
- '@_CSharpKeyword'
- '@'
helpviewer_keywords:
- '@ special character [C#]'
- '@ language element [C#]'
ms.assetid: 89bc7e53-85f5-478a-866d-1cca003c4e8c
ms.openlocfilehash: 7d78b28479ed6128321207073dc94976710f10b6
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89138900"
---
# <a name="-c-reference"></a>@ (C# 參考)

`@` 特殊字元可用為逐字識別項。 使用方式如下：

1. 讓 C# 關鍵字用為識別項。 `@` 字元將程式碼元素當成前置詞，編譯器要將此元素解譯為識別項，不是 C# 關鍵字。 下例會使用 `@` 字元來定義名為 `for` 的識別項，它會用在 `for` 迴圈中。

   [!code-csharp[verbatim1](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#1)]

1. 表示要逐字解譯字串常值。 這個執行個體中的 `@` 字元會定義「逐字字串常值」**。 簡單逸出序列 (例如 `"\\"` 用於反斜線)、十六進位逸出序列 (例如 `"\x0041"` 用於大寫 A)，以及 Unicode 逸出序列 (例如 `"\u0041"` 用於大寫 A) 都是照字面解譯。 只有引號 escape 序列 (的 `""`) 並不會以字面方式解讀; 它會產生一個雙引號。 此外，如果是逐字[插入字串](interpolated.md)，大括弧逸出序列 (`{{` 和 `}}`) 不會照字面意義解譯，它們會產生一個大括弧字元。 下例會定義兩個相同的檔案路徑，一個使用規則字串常值，另一個使用逐字字串常值。 這是逐字字串常值較常見的用法之一。

   [!code-csharp[verbatim2](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#2)]

   下例示範定義包含相同字元序列的規則字串常值和逐字字串常值的效果。

   [!code-csharp[verbatim3](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#3)]

1. 如果發生命名衝突，讓編譯器區別屬性。 屬性是衍生自 <xref:System.Attribute> 的類別。 其型別名稱通常包含尾碼 **Attribute**，雖然編譯器不會強制執行此慣例。 然後，在程式碼中就可以依其完整型別名稱 (例如 `[InfoAttribute]`) 或簡短名稱 (例如 `[Info]`) 參考屬性。 不過，如果兩個簡短的屬性型別名稱完全相同，但一個型別名稱有 **Attribute** 尾碼，一個沒有，即會發生命名衝突。 例如，下列程式碼無法編譯，因為編譯器無法判斷是否已對 `Example` 類別套用了 `Info` 或 `InfoAttribute` 屬性。 請參閱 [CS1614](../compiler-messages/cs1614.md) 以取得詳細資訊。

   [!code-csharp[verbatim4](../../../../samples/snippets/csharp/language-reference/keywords/verbatim2.cs#1)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 特殊字元](./index.md)

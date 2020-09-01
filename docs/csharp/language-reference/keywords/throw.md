---
description: throw - C# 參考
title: throw - C# 參考
ms.date: 03/02/2015
f1_keywords:
- throw
- throw_CSharpKeyword
helpviewer_keywords:
- throw statement [C#]
- throw expression [C#]
- throw keyword [C#]
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
ms.openlocfilehash: 4cad4810b89f976f92ce576917feb2398acce636
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89142033"
---
# <a name="throw-c-reference"></a>throw (C# 參考)

在程式執行期間發出出現例外狀況的訊號。  
  
## <a name="remarks"></a>備註

`throw` 的語法為：

```csharp
throw [e];
```

而 `e` 是衍生自 <xref:System.Exception?displayProperty=nameWithType> 之類別的執行個體。 如果傳遞給 `GetNumber` 方法的引數未對應至內部陣列的有效索引，則下列範例會使用 `throw` 陳述式來擲回  <xref:System.IndexOutOfRangeException> 。

[!code-csharp[csrefKeyword#1](~/samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#1)]

方法呼叫端接著會使用 `try-catch` 或 `try-catch-finally` 區塊來處理所擲回的例外狀況。 下列範例會處理 `GetNumber` 方法所擲回的例外狀況。

[!code-csharp[csrefKeyword#2](~/samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#2)]

## <a name="re-throwing-an-exception"></a>重新擲回例外狀況

`throw` 也可以用於 `catch` 區塊，以重新擲回 `catch` 區塊中所處理的例外狀況。  在此情況下，`throw` 陳述式不接受例外狀況運算元。 這最適用於當方法將來自呼叫端的引數傳遞給某個其他程式庫方法，且程式庫方法擲回必須傳遞給呼叫端的例外狀況時。 例如，下列範例會重新擲回 <xref:System.NullReferenceException>，而這是在嘗試擷取未初始化字串的第一個字元時擲回。

[!code-csharp[csrefKeyword#3](~/samples/snippets/csharp/language-reference/keywords/throw/throw-3.cs#3)]

> [!IMPORTANT]
> 您也可以使用 `catch` 區塊中的 `throw e` 語法，來具現化傳遞給呼叫端的新例外狀況。 在此情況下，不會保留原始例外狀況的堆疊追蹤 (可從 <xref:System.Exception.StackTrace> 屬性取得)。

## <a name="the-throw-expression"></a>`throw` 運算式

從 C# 7.0 開始，`throw` 可以用作運算式和陳述式。 這可在先前不支援的內容中擲回例外狀況。 其中包含：

- [條件運算子](../operators/conditional-operator.md)。 如果將空字串陣列傳遞給方法，則下列範例會使用 `throw` 運算式來擲回 <xref:System.ArgumentException>。 在 C# 7.0 之前，這個邏輯必須出現在 `if`/`else` 陳述式中。

   [!code-csharp[csrefKeyword#4](~/samples/snippets/csharp/language-reference/keywords/throw/conditional.cs#1)]

- [Null 聯合運算子](../operators/null-coalescing-operator.md)。 在下列範例中，如果指派給 `Name` 屬性的字串是 `null`，則搭配使用 `throw` 運算式與 Null 聯合運算子會擲回例外狀況。

   [!code-csharp[csrefKeyword#5](~/samples/snippets/csharp/language-reference/keywords/throw/coalescing.cs#1)]

- 運算式主體 [ambda](../operators/lambda-expressions.md) 或方法。 下列範例說明因不支援轉換為 <xref:System.DateTime> 值而擲回 <xref:System.InvalidCastException> 的運算式主體方法。

   [!code-csharp[csrefKeyword#6](~/samples/snippets/csharp/language-reference/keywords/throw/exp-bodied.cs#1)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [try-catch](try-catch.md)
- [C # 關鍵字](index.md)
- [如何：明確擲回例外狀況](../../../standard/exceptions/how-to-explicitly-throw-exceptions.md)

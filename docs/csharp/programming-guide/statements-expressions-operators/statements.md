---
title: 陳述式 - C# 程式設計指南
description: '瞭解 c # 程式設計中的語句。 查看語句類型清單，並查看程式碼範例和其他資源。'
ms.date: 07/20/2015
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
ms.openlocfilehash: b941e46f959167f78f1366a3863aca4240810013
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381758"
---
# <a name="statements-c-programming-guide"></a>陳述式 (C# 程式設計手冊)

程式所採取的動作是在陳述式中表示。 根據指定的條件，常見動作包括宣告變數、指派值、呼叫方法、循環執行集合，以及分支到一個或另一個程式碼區塊。 陳述式在程式中的執行順序稱為「控制流程」或「執行流程」。 根據程式如何反應它在執行階段收到的輸入，每次執行程式時，控制流程可能都會不同。

陳述式可以包含一行以分號結束的程式碼或區塊中的一連串單行陳述式。 陳述式區塊會用 {} 括弧括住，而且可以包含巢狀區塊。 下列程式碼示範兩個單行陳述式範例和多行陳述式區塊範例︰

[!code-csharp[csProgGuideStatements#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#1)]

## <a name="types-of-statements"></a>語句的類型

下表列出 C# 中各種類型的陳述式和其相關聯的關鍵字，以及包含更多資訊的主題連結︰

|類別|C# 關鍵字/附註|
|--------------|---------------------------|
|[宣告陳述式](#declaration-statements)|宣告陳述式引進新的變數或常數。 變數宣告可以將值選擇性指派給變數。 在常數宣告中，需要進行指派。|
|[運算式陳述式](expressions.md)|計算值的運算式陳述式必須將值儲存在變數中。 如需詳細資訊，請參閱[運算式陳述式](#expression-statements)。|
|選取範圍陳述式|選取範圍陳述式可讓您根據一或多個指定的條件，分支到不同的程式碼區段。 如需詳細資訊，請參閱下列主題： <ul><li>[if](../../language-reference/keywords/if-else.md)</li><li>[else](../../language-reference/keywords/if-else.md)</li><li>[switch](../../language-reference/keywords/switch.md)</li><li>[例圖](../../language-reference/keywords/switch.md)</li></ul>|
|反覆運算陳述式|反覆運算陳述式可讓您循環執行如陣列這類集合，或重複執行同一組陳述式，直到符合指定的條件為止。 如需詳細資訊，請參閱下列主題： <ul><li>[do](../../language-reference/keywords/do.md)</li><li>[for](../../language-reference/keywords/for.md)</li><li>[foreach](../../language-reference/keywords/foreach-in.md)</li><li>[in](../../language-reference/keywords/foreach-in.md)</li><li>[等待](../../language-reference/keywords/while.md)</li></ul>|
|跳躍陳述式|跳躍陳述式會將控制權轉移給另一個程式碼區段。 如需詳細資訊，請參閱下列主題： <ul><li>[break](../../language-reference/keywords/break.md)</li><li>[持續](../../language-reference/keywords/continue.md)</li><li>[預設值](../../language-reference/keywords/switch.md)</li><li>[goto](../../language-reference/keywords/goto.md)</li><li>[return](../../language-reference/keywords/return.md)</li><li>[yield](../../language-reference/keywords/yield.md)</li></ul>|
|例外狀況處理陳述式|例外狀況處理陳述式可讓您順利復原在執行階段發生的例外狀況。 如需詳細資訊，請參閱下列主題： <ul><li>[throw](../../language-reference/keywords/throw.md)</li><li>[try-catch](../../language-reference/keywords/try-catch.md)</li><li>[try-finally](../../language-reference/keywords/try-finally.md)</li><li>[try-catch-finally](../../language-reference/keywords/try-catch-finally.md)</li></ul>|
|[Checked 和 unchecked](../../language-reference/keywords/checked-and-unchecked.md)|checked 和 unchecked 陳述式可讓您指定，在將結果儲存在太小無法保存所產生值的變數中時，是否允許數值作業導致溢位。 如需詳細資訊，請參閱 [checked](../../language-reference/keywords/checked.md) 和 [unchecked](../../language-reference/keywords/unchecked.md)。|
|`await` 陳述式|如果您使用 [async](../../language-reference/keywords/async.md) 修飾詞來標示方法，可以在方法中使用 [await](../../language-reference/operators/await.md) 運算子。 當控制權到達 async 方法中的 `await` 運算式時，控制權會傳回給呼叫端，並暫止方法中的進度，直到等候的工作完成。 當工作完成時，方法中的執行可以繼續。<br /><br /> 如需簡單範例，請參閱[方法](../classes-and-structs/methods.md)的＜非同步方法＞一節。 如需詳細資訊，請參閱[使用 async 和 await 進行非同步程式設計](../concepts/async/index.md)。|
|`yield return` 陳述式|迭代器會對集合執行自訂的反覆項目，例如清單或陣列。 迭代器會使用 [yield return](../../language-reference/keywords/yield.md) 陳述式來一次傳回一個項目。 當到達 `yield return` 陳述式時，系統會記住程式碼中的目前位置。 下一次呼叫迭代器時，便會從這個位置重新開始執行。<br /><br /> 如需詳細資訊，請參閱[反覆運算](../concepts/iterators.md)器。|
|`fixed` 陳述式|fixed 陳述式可防止記憶體回收行程重新配置可移動的變數。 如需詳細資訊，請參閱 [fixed](../../language-reference/keywords/fixed-statement.md)。|
|`lock` 陳述式|lock 陳述式可讓您限制一次只能存取一個執行緒的程式碼區塊。 如需詳細資訊，請參閱 [lock](../../language-reference/keywords/lock-statement.md)。|
|標記陳述式|您可以提供陳述式標籤，然後使用 [goto](../../language-reference/keywords/goto.md) 關鍵字跳到標記陳述式。 (請參閱下面一列中的範例)。|
|[空的語句](#the-empty-statement)|空陳述式包含一個分號。 它不會執行任何作業，而且可以用於需要陳述式但不需要執行任何動作的位置。|

## <a name="declaration-statements"></a>宣告陳述式

下列程式碼示範具有與沒有初始指派的變數宣告，以及經過必要初始化的常數宣告。

[!code-csharp[csProgGuideStatements#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#23)]

## <a name="expression-statements"></a>運算式陳述式

下列程式碼示範運算式陳述式，包括指派、具有指派的物件建立及方法引動過程。

[!code-csharp[csProgGuideStatements#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#24)]

## <a name="the-empty-statement"></a>空陳述式

下列範例示範空陳述式的兩種用法：

[!code-csharp[csProgGuideStatements#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#25)]

## <a name="embedded-statements"></a>內嵌語句

某些陳述式 (包含 [do](../../language-reference/keywords/do.md)、[while](../../language-reference/keywords/while.md)、[for](../../language-reference/keywords/for.md) 和 [foreach](../../language-reference/keywords/foreach-in.md)) 的後面一律會有內嵌陳述式。 內嵌陳述式可能是單一陳述式或陳述式區塊中用 {} 括弧括住的多個陳述式。 甚至單行內嵌陳述式可以用 {} 括弧括住，如下列範例所示︰

[!code-csharp[csProgGuideStatements#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#26)]

未以 {} 括弧括住的內嵌陳述式不能是宣告陳述式或標記陳述式。 下列範例會顯示這一點：

[!code-csharp[csProgGuideStatements#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#27)]

將內嵌的陳述式放入區塊中來修正錯誤︰

[!code-csharp[csProgGuideStatements#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#28)]

## <a name="nested-statement-blocks"></a>Nested 語句區塊

陳述式區塊可以是巢狀，如下列程式碼所示︰

[!code-csharp[csProgGuideStatements#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#29)]

## <a name="unreachable-statements"></a>無法連線的語句

如果編譯器判斷控制流程在任何情況下都永遠達不到特定陳述式，則會產生警告 CS0162，如下列範例所示︰

[!code-csharp[csProgGuideStatements#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#22)]

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[陳述式](~/_csharplang/spec/statements.md)一節。

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [語句關鍵字](../../language-reference/keywords/statement-keywords.md)  
- [運算式](expressions.md)  

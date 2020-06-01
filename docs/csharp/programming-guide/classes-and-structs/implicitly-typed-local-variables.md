---
title: 隱含類型區域變數 - C# 程式設計手冊
ms.date: 07/20/2015
helpviewer_keywords:
- implicitly-typed local variables [C#]
- var [C#]
ms.assetid: b9218fb2-ef5d-4814-8a8e-2bc29b0bbc9b
ms.openlocfilehash: 842f73b7af9671157495df961f5db22702ae897e
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84240703"
---
# <a name="implicitly-typed-local-variables-c-programming-guide"></a>隱含類型區域變數 (C# 程式設計手冊)

您可以宣告區域變數而不提供明確類型。 `var` 關鍵字會指示編譯器從初始化陳述式右側的運算式推斷變數的類型。 推斷的型別可以是內建型別、匿名型別、使用者定義型別，或是 .NET 類別庫中定義的型別。 如需如何使用 `var` 初始化陣列的詳細資訊，請參閱[隱含型別陣列](../arrays/implicitly-typed-arrays.md)。

下列範例顯示可以使用 `var` 宣告區域變數的各種方法：

[!code-csharp[csProgGuideLINQ#43](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#43)]

請務必了解 `var` 關鍵字不代表 "variant"，也不代表變數是不嚴格規定類型或晚期繫結的。 只代表編譯器會判斷並指派最適當的類型。

`var` 關鍵字可在下列內容中使用：

- 在區域變數 (方法範圍中宣告的變數) 上，如前述範例所示。

- 在 [for](../../language-reference/keywords/for.md) 初始化陳述式中。

    ```csharp
    for (var x = 1; x < 10; x++)
    ```

- 在 [foreach](../../language-reference/keywords/foreach-in.md) 初始化陳述式中。

    ```csharp
    foreach (var item in list) {...}
    ```

- 在 [using](../../language-reference/keywords/using-statement.md) 陳述式中。

    ```csharp
    using (var file = new StreamReader("C:\\myfile.txt")) {...}
    ```

如需詳細資訊，請參閱[如何在查詢運算式中使用隱含類型區域變數和陣列](how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)。

## <a name="var-and-anonymous-types"></a>var 和匿名型別

在許多情況下，使用 `var` 是選擇性的，只是為了在語法上便於使用。 不過，當變數以匿名型別初始化時，如果您稍後需要存取物件的屬性，則必須宣告該變數為 `var`。 這是 LINQ 查詢運算式中的常見案例。 如需詳細資訊，請參閱[匿名](anonymous-types.md)型別。

從原始程式碼的觀點來看，匿名型別沒有名稱。 因此，如果已使用 `var` 初始化查詢變數，則存取傳回的物件序列中屬性的唯一方法，就是使用 `var` 作為 `foreach` 陳述式中反覆運算變數的類型。

[!code-csharp[csProgGuideLINQ#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#44)]

## <a name="remarks"></a>備註

下列限制適用於隱含型別變數宣告：

- `var` 只能在區域變數於相同的陳述式中宣告和初始化時使用；此變數無法初始化為 null、方法群組或匿名函式。

- `var` 無法在類別範圍的欄位中使用。

- 使用 `var` 宣告的變數無法在初始化運算式中使用。 換句話說，這個運算式是合法 `int i = (i = 20);` 的：但這個運算式會產生編譯時期錯誤：`var i = (i = 20);`

- 無法在相同的陳述式中初始化多個隱含型別變數。

- 如果名為 `var` 的類型在範圍之內，則 `var` 關鍵字會解析成該類型名稱，而且不會視為隱含型別區域變數宣告的一部分。

使用 `var` 關鍵字的隱含類型只能套用至本機方法範圍的變數。 隱含類型不適用於類別欄位，因為 C# 編譯器會在處理程式碼時發生邏輯矛盾：編譯器需要了解欄位的類型，但是它無法在分析指派運算式之前判斷類型，而運算式無法在不了解類型的情況下進行評估。 請考慮下列程式碼：

```csharp
private var bookTitles;
```

`bookTitles` 是類型為 `var` 的類別欄位。 因為欄位沒有能評估的運算式，所以編譯器無法推斷 `bookTitles` 的類型為何。 此外，將運算式新增至欄位 (如同你對區域變數進行的操作) 也不足夠：

```csharp
private var bookTitles = new List<string>();
```

當編譯器在編譯程式碼期間遇到欄位時，它會記錄每個欄位的類型，再處理任何與其建立關聯的運算式。 編譯器會在嘗試剖析 `bookTitles` 時發生相同的矛盾：它需要了解欄位的類型，但是編譯器通常會透過分析運算式來判斷 `var` 的類型，而這無法在不事先了解類型的情況下進行。

您會發現在難以判斷查詢運算式中查詢變數的確切建構類型時，`var` 也相當有用。 這會在群組與排序作業時發生。

當您不想要老是在鍵盤上鍵入變數的特定類型，或是此特定類型很明顯或不會增加程式碼的可讀性時，`var` 關鍵字也相當有用。 `var` 有用的其中一個範例是用於巢狀泛型型別時，例如用於群組作業的類型。 在下列查詢中，查詢變數的類型是 `IEnumerable<IGrouping<string, Student>>`。 只要您及維護程式碼的其他使用者了解這點，為求便利和簡潔而使用隱含型別就不會有問題。

[!code-csharp[cscsrefQueryKeywords#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#13)]

使用 `var` 有助於簡化您的程式碼，但其使用方式應該限制為必要的情況，或讓您的程式碼更容易閱讀。 如需何時正確使用的詳細資訊 `var` ，請參閱 c # 程式碼撰寫方針一文的[隱含類型區域變數](../inside-a-program/coding-conventions.md#implicitly-typed-local-variables)一節。

## <a name="see-also"></a>另請參閱

- [C # 參考](../../language-reference/index.md)
- [隱含型別陣列](../arrays/implicitly-typed-arrays.md)
- [如何在查詢運算式中使用隱含類型區域變數和陣列](how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)
- [匿名類型](anonymous-types.md)
- [物件和集合初始設定式](object-and-collection-initializers.md)
- [var](../../language-reference/keywords/var.md)
- [C# 中的 LINQ](../../linq/index.md)
- [LINQ (Language-Integrated Query)](../../linq/index.md)
- [for](../../language-reference/keywords/for.md)
- [foreach、in](../../language-reference/keywords/foreach-in.md)
- [using 陳述式](../../language-reference/keywords/using-statement.md)

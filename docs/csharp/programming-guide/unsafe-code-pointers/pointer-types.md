---
title: 指標類型 - C# 程式設計手冊
ms.date: 04/20/2018
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.openlocfilehash: 492b37460c05ffbc82e020facb354be22706f8d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396255"
---
# <a name="pointer-types-c-programming-guide"></a>指標類型 (C# 程式設計手冊)

在 unsafe 內容中，類型有可能是指標類型、實值類型或參考類型。 指標類型宣告會使用下列其中一種格式：

``` csharp
type* identifier;
void* identifier; //allowed but not recommended
```

在指標型別中的 `*` 之前指定的型別稱為**參考型別**。 只有 [unmanaged 型別](../../language-reference/builtin-types/unmanaged-types.md)才可以是參考型別。

指標型別不會從 [object](../../language-reference/builtin-types/reference-types.md) 繼承，而且指標型別與 `object` 之間無法進行轉換。 此外，boxing 和 unboxing 不支援指標。 不過，不同的指標類型之間以及指標類型與整數類資料類型之間可以進行轉換。

當您在相同的宣告中宣告多個指標時，星號 (*) 只會與基礎類型一起出現，而不會做為每個指標名稱的前置詞使用。 例如：

```csharp
int* p1, p2, p3;   // Ok
int *p1, *p2, *p3;   // Invalid in C#
```

指標無法指向參考或包含參考的 [struct](../../language-reference/builtin-types/struct.md)，因為即使指標指向物件參考，依然可以對物件參考進行記憶體回收。 記憶體回收行程不會持續追蹤是否有任何指標類型指向物件。

`myType*` 類型的指標變數值是 `myType` 類型變數的位址。 以下是指標類型宣告的範例：

|範例|描述|
|-------------|-----------------|
|`int* p`|`p` 為整數的指標。|
|`int** p`|`p` 為整數指標的指標。|
|`int*[] p`|`p` 為整數的一維陣列指標。|
|`char* p`|`p` 為字元的指標。|
|`void* p`|`p` 為未知類型的指標。|

您可以使用指標間接運算子 * 存取指標變數所指向位置的內容。 例如，請參考下列宣告：

```csharp
int* myVariable;
```

這個運算式 `*myVariable` 表示位於 `int` 所包含之位址的 `myVariable` 變數。

[fixed 陳述式](../../language-reference/keywords/fixed-statement.md)和[指標轉換](./pointer-conversions.md)主題中有數個指標範例。 下列範例使用 `unsafe` 關鍵字和 `fixed` 陳述式，並示範如何讓內部指標遞增。  您可以將這個程式碼貼入主控台應用程式的 Main 函式中來執行它  這些範例必須使用 [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) 編譯器選項集合來編譯。

[!code-csharp[Using pointer types](snippets/FixedKeywordExamples.cs#5)]

您無法將間接運算子套用至 `void*` 類型的指標。 不過，您可以使用轉型，將 Void 指標轉換成任何其他指標類型，反之亦然。

指標可以是 `null`。 將間接運算子套用至 null 指標會產生實作定義的行為。

在方法之間傳遞指標時，可能會導致未定義的行為。 請考慮使用透過 `in`、`out` 或 `ref` 參數或是以函式結果的方式，將指標傳至區域變數的方法。 如果已在固定區塊中設定指標，則該指標指向的變數就可能不再是固定的。

下表所列出的運算子和陳述式可以用於 unsafe 內容中的指標：

|運算子/陳述式|使用|
|-------------------------|---------|
|`*`|執行指標間接取值。|
|`->`|透過指標存取結構的成員。|
|`[]`|索引指標。|
|`&`|取得變數位址。|
|`++` 和 `--`|遞增和遞減指標。|
|`+` 和 `-`|執行指標算術。|
|`==`、`!=`、`<`、`>`、`<=` 和 `>=`|比較指標。|
|[`stackalloc`](../../language-reference/operators/stackalloc.md)|在堆疊上配置記憶體。|
|[`fixed`句](../../language-reference/keywords/fixed-statement.md)|暫時固定變數以便找到其位址。|

如需指標相關運算子的詳細資訊，請參閱[指標相關運算子](../../language-reference/operators/pointer-related-operators.md)。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[指標型別](~/_csharplang/spec/unsafe-code.md#pointer-types)。

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [不安全的程式碼和指標](index.md)
- [指標轉換](pointer-conversions.md)
- [參考型別](../../language-reference/keywords/reference-types.md)
- [值類型](../../language-reference/builtin-types/value-types.md)
- [不安全](../../language-reference/keywords/unsafe.md)

---
title: 結構
description: '瞭解 F # 結構，壓縮物件類型通常比具有少量資料和簡單行為之類型的類別更有效率。'
ms.date: 05/16/2016
ms.openlocfilehash: 1e9652cc4776e4d1d52eb20e41b6dd87a6c5ba05
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223820"
---
# <a name="structures"></a>結構

*結構*是一種精簡的物件類型，相較于具有少量資料和簡單行為之類型的類別，其效率可能更高。

## <a name="syntax"></a>語法

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    struct
        type-definition-elements-and-members
    end
// or
[ attributes ]
[<StructAttribute>]
type [accessibility-modifier] type-name =
    type-definition-elements-and-members
```

## <a name="remarks"></a>備註

結構是實 *值*型別，這表示這些型別會直接儲存在堆疊上，或做為欄位或陣列元素（內嵌于父系型別）使用。 有別於類別與記錄，結構具有以值傳遞的語意。 這表示它們主要對於經常存取及複製的小型資料彙總相當實用。

在先前的語法中，顯示了兩個表單。 第一個表單的語法略為複雜，但使用卻很頻繁，因為當您使用 `struct` 和 `end` 關鍵字時，可以省略出現在第二個表單中的 `StructAttribute` 屬性。 您可以將 `StructAttribute` 縮寫為只有 `Struct`。

上述語法中的 *類型定義-元素和成員* 代表成員宣告和定義。 結構可以具有建構函式及可變動和不可變的欄位，同時它們可以宣告成員及介面實作。 如需詳細資訊，請參閱 [成員](./members/index.md)。

結構無法參與繼承、不能包含 `let` 或 `do` 繫結，且不得以遞迴方式包含其本身類型的欄位 (不過它們可以包含參考其本身類型的參考儲存格)。

因為結構不允許 `let` 繫結，因此您必須使用 `val` 關鍵字來宣告結構中的欄位。 `val` 關鍵字會定義欄位及其類型，但不允許進行初始化。 相反地，`val` 宣告會初始化為零或 null。 基於這個理由，具有隱含建構函式 (也就是緊接在宣告中結構名稱後的指定參數) 的結構，需要 `val` 宣告標註 `DefaultValue` 屬性。 具有已定義的建構函式之結構，仍然支援零初始化。 因此，`DefaultValue` 屬性是一種零值對於欄位有效的宣告。 結構的隱含建構函式不會執行任何動作，因為類型上不允許 `let` 和 `do` 繫結，但傳入的隱含建構函式參數值均可用作為私用欄位。

明確建構函式可能會牽涉到欄位值的初始化。 當您的結構有明確的建構函式時，它仍然可以支援零初始化。不過，請勿在 `DefaultValue` 宣告上使用 `val` 屬性，因為它與明確建構函式相衝突。 如需宣告的詳細資訊 `val` ，請參閱 [明確欄位： `val` 關鍵字](./members/explicit-fields-the-val-keyword.md)。

結構上允許屬性和存取範圍修飾詞，並遵循與其他類型相同的規則。 如需詳細資訊，請參閱 [屬性](attributes.md) 和 [存取控制](access-control.md)。

下列程式碼範例說明結構定義。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2501.fs)]

## <a name="byreflike-structs"></a>ByRefLike 結構

您可以定義您自己的結構，以遵循 `byref` 類似的語義：如需詳細資訊，請參閱 [byref](byrefs.md) 。 這是使用屬性來完成的 <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> ：

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike` 不表示 `Struct` 。 兩者都必須存在於類型上。

`byref`F # 中的「-like」結構是堆疊系結的實值型別。 它永遠不會在 managed 堆積上進行配置。 `byref`類似的結構適用于高效能程式設計，因為它會利用存留期和非捕捉的一組強大檢查來強制執行。 這些規則包括：

- 它們可用來作為函式參數、方法參數、區域變數、方法傳回。
- 它們不得為類別或一般結構的靜態或實例成員。
- `async`)  (方法或 lambda 運算式時，無法由任何關閉結構來捕捉它們。
- 它們不能用來做為泛型參數。

雖然這些規則非常嚴格地限制使用方式，但它們會以安全的方式滿足高效能運算的承諾。

## <a name="readonly-structs"></a>ReadOnly 結構

您可以使用屬性來標注結構 <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute> 。 例如：

```fsharp
[<IsReadOnly; Struct>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsReadOnly` 不表示 `Struct` 。 您必須加入兩者以具有 `IsReadOnly` 結構。

使用這個屬性會發出中繼資料，讓 F # 和 c # 知道分別將它視為 `inref<'T>` 和 `in ref` 。

在 readonly 結構內定義可變值會產生錯誤。

## <a name="struct-records-and-discriminated-unions"></a>結構記錄和區分等位

您可以將 [記錄](records.md) 和 [差異](discriminated-unions.md) 聯集表示為具有 `[<Struct>]` 屬性的結構。  請參閱每篇文章以深入瞭解。

## <a name="see-also"></a>另請參閱

- [F # 語言參考](index.md)
- [類別](classes.md)
- [記錄](records.md)
- [成員](./members/index.md)

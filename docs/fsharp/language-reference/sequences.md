---
title: 序列
description: '當您有大量、已排序的資料集合，但不一定要使用所有元素時，瞭解如何使用 F # 序列。'
ms.date: 11/04/2019
ms.openlocfilehash: fa5073f33b9dae52371c249bfb257a2446b4d26a
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855318"
---
# <a name="sequences"></a>序列

「*序列*」是一種專案的邏輯數列，全都屬於一個型別。 當您有大量、已排序的資料集合，但不一定會使用所有的元素時，序列會特別有用。 個別序列元素只會視需要計算，因此在不使用所有元素的情況下，序列可以提供比清單更好的效能。 序列是以型別表示 `seq<'T>` ，這是的別名 <xref:System.Collections.Generic.IEnumerable%601> 。 因此，任何執行介面的 .NET 類型 <xref:System.Collections.Generic.IEnumerable%601> 都可以當做序列使用。 [Seq 模組](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684)可支援涉及序列的操作。

> [!NOTE]
> F # 的 docs.microsoft.com API 參考不完整。 如果您遇到任何中斷的連結，請改為參考[F # 核心程式庫檔](https://fsharp.github.io/fsharp-core-docs/)。

## <a name="sequence-expressions"></a>序列運算式

*序列運算式*是評估為序列的運算式。 順序運算式可以採用數種形式。 最簡單的形式就是指定範圍。 例如， `seq { 1 .. 5 }` 會建立包含五個元素的序列，包括端點1和5。 您也可以指定遞增 (，或在兩個雙句點之間遞減) 。 例如，下列程式碼會建立10的倍數序列。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1502.fs)]

順序運算式是由產生序列值的 F # 運算式所組成。 您也可以透過程式設計方式產生值：

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1503.fs)]

先前的範例使用 `->` 運算子，可讓您指定一個運算式，其值會成為序列的一部分。 只有在後面的 `->` 程式碼的每個部分傳回值時，您才能使用。

或者，您可以指定 `do` 關鍵字，並在後面加上選擇性 `yield` 的：

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1504.fs)]

下列程式碼會在代表方格的陣列中，產生座標配對的清單，以及一個索引。 請注意，第一個 `for` 運算式需要 `do` 指定。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1505.fs)]

`if`序列中使用的運算式是篩選準則。 例如，若只要產生一個質數的序列，假設您有 `isprime` 類型的函式 `int -> bool` ，請依照下列方式來結構化序列。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1506.fs)]

如先前所述，在 `do` 這裡需要，因為沒有任何 `else` 分支使用 `if` 。 如果您嘗試使用 `->` ，您會收到錯誤訊息，指出並非所有分支都傳回值。

## <a name="the-yield-keyword"></a>`yield!` 關鍵字

有時候，您可能會想要將一連串的專案包含在另一個序列中。 若要在另一個序列中包含順序，您必須使用 `yield!` 關鍵字：

```fsharp
// Repeats '1 2 3 4 5' ten times
seq {
    for _ in 1..10 do
        yield! seq { 1; 2; 3; 4; 5}
}
```

另一個思考方式 `yield!` 是，它會壓平合併內部序列，然後將其包含在包含序列中。

`yield!`在運算式中使用時，所有其他單一值都必須使用 `yield` 關鍵字：

```fsharp
// Combine repeated values with their values
seq {
    for x in 1..10 do
        yield x
        yield! seq { for i in 1..x -> i}
}
```

只有 `x` 在上述範例中指定，才會產生序列，而不會產生任何值。

## <a name="examples"></a>範例

第一個範例會使用包含反復專案、篩選和 yield 的序列運算式來產生陣列。 此程式碼會將1到100之間的質數序列列印到主控台。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1507.fs)]

下列範例會建立一個由三個元素的元組組成的乘法資料表，每個專案都包含兩個因素和產品：

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1508.fs)]

下列範例示範 `yield!` 如何使用將個別序列結合成單一最終序列。 在此情況下，二進位樹狀目錄中每個子樹的序列都會在遞迴函式中串連，以產生最終的序列。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1509.fs)]

## <a name="using-sequences"></a>使用順序

序列支援許多與[清單](lists.md)相同的功能。 序列也支援使用索引鍵產生函式的分組和計算之類的作業。 序列也支援更多樣化的函式來解壓縮個子序列。

許多資料類型（例如清單、陣列、集合和對應）都是隱含的序列，因為它們是可列舉的集合。 將序列當做引數使用的函式，除了任何可執行檔 .NET 資料類型之外，也可以搭配任何常見的 F # 資料類型 `System.Collections.Generic.IEnumerable<'T>` 。 相較于接受清單做為引數的函式，它只能接受清單。 類型 `seq<'T>` 是的類型縮寫 `IEnumerable<'T>` 。 這表示任何實作為泛型的型別（ `System.Collections.Generic.IEnumerable<'T>` 包括 F # 中的陣列、清單、集合和對應，以及大多數的 .net 集合類型）都與型別相容， `seq` 而且可以在預期序列的任何位置使用。

## <a name="module-functions"></a>模組函式

[Fsharp.core 命名空間](https://msdn.microsoft.com/library/24f64e5f-5030-47d0-9759-8d3e398ed13f)中的[Seq 模組](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684)包含處理序列的函式。 這些函式也會使用清單、陣列、對應和集合，因為所有這些類型都是可列舉的，因此可以視為序列。

## <a name="creating-sequences"></a>建立序列

如先前所述，或使用特定函數，您可以使用順序運算式來建立序列。

您可以使用 [ [seq](https://msdn.microsoft.com/library/3c7f1c69-6117-4782-b2da-0e04d6854f59)] 建立空的序列，或使用 [ [seq](https://msdn.microsoft.com/library/9b8cc460-a282-4ec5-b29a-630ab17e9de7)] 建立只有一個指定元素的序列。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet9.fs)]

您可以使用[Seq.init](https://msdn.microsoft.com/library/059de69d-812c-4f8e-be86-88aa72101576)來建立使用您所提供的函式來建立元素的序列。 您也可以為序列提供大小。 此函式與[List.init](https://msdn.microsoft.com/library/dd38c096-0ea8-4858-be6b-794b90418b83)相同，唯一不同的是，在您逐一查看序列之前，不會建立元素。 下列程式碼說明的用法 `Seq.init` 。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet10.fs)]

輸出為

```console
0 10 20 30 40
```

藉由使用[list.ofarray](https://msdn.microsoft.com/library/299cd4d9-be72-4511-aac8-089e1ddaac99)和[array.oflist&#60; 不&#62; 函數](https://msdn.microsoft.com/visualfsharpdocs/conceptual/seq.oflist%5b%27t%5d-function-%5bfsharp%5d)，您可以從陣列和清單建立序列。 不過，您也可以使用 cast 運算子，將陣列和清單轉換成序列。 下列程式碼會顯示這兩種技術。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet11.fs)]

藉由使用 Seq，您可以從弱型別集合（例如中定義的型別）建立序列[。](https://msdn.microsoft.com/library/1d087db3-a8b2-41dd-8ddc-227544529334) `System.Collections` 這類弱式類型集合具有元素類型 `System.Object` ，而且是使用非泛型型別來列舉 `System.Collections.Generic.IEnumerable&#96;1` 。 下列程式碼說明如何使用將 `Seq.cast` 轉換 `System.Collections.ArrayList` 成序列。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet12.fs)]

您可以使用[Seq.initInfinite](https://msdn.microsoft.com/library/d1804e53-da92-48ec-8d6e-57eaf4c62bef)函數來定義無限序列。 針對這類順序，您會提供函式，從專案的索引產生每個元素。 無限序列是可能的，因為延遲評估;專案會視需要藉由呼叫您指定的函式來建立。 下列程式碼範例會產生無限的浮點數序列，在此案例中為連續整數的一系列 reciprocals。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet13.fs)]

[[展開](https://msdn.microsoft.com/library/7d9232fc-742e-42bc-bdf7-6f130f0eff21)] 會從接受狀態的計算函式產生序列，並加以轉換，以產生序列中的每個後續元素。 此狀態只是用來計算每個元素的值，而且可以隨著每個元素的計算而變更。 的第二個引數 `Seq.unfold` 是用來啟動序列的起始值。 `Seq.unfold`使用狀態的選項類型，可讓您藉由傳回值來終止序列 `None` 。 下列程式碼顯示兩個 `seq1` 由作業所產生之序列和的範例 `fib` `unfold` 。 第一 `seq1` 種是一個簡單的序列，最高可達20個數字。 第二個會 `fib` 使用 `unfold` 來計算斐波和數列序列。 由於每個數列序列中的元素都是前兩個斐報數位的總和，因此 state 值是由序列中前兩個數字組成的元組。 初始值是 `(1,1)` ，序列中的前兩個數字。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet14.fs)]

輸出如下所示：

```console
The sequence seq1 contains numbers from 0 to 20.

0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20

The sequence fib contains Fibonacci numbers.

2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

下列程式碼範例會使用此處所述的許多順序模組函數來產生和計算無限序列的值。 程式碼可能需要幾分鐘的時間才能執行。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet15.fs)]

## <a name="searching-and-finding-elements"></a>搜尋和尋找元素

序列支援清單所提供的功能： [seq. exists](https://msdn.microsoft.com/library/428c97bf-599d-4c39-a5b9-f8717c198ad1)、 [seq. list.exists2](https://msdn.microsoft.com/library/efdf14a4-27f7-4dc1-9281-52639e66d565)、 [seq. find](https://msdn.microsoft.com/library/02c21ecd-97e5-4e99-a4c1-b4d0b730b7d8)、 [seq. findIndex](https://msdn.microsoft.com/library/96dfe86b-df15-4d92-8316-7cd6055e09f3)、 [seq. pick](https://msdn.microsoft.com/library/a87bc771-55f7-43f9-94f9-33d8f9bf325d)、 [tryFind](https://msdn.microsoft.com/library/ac43c6f5-4dc7-4e9a-a222-00b5736aee47)和[seq. array.tryfindindex](https://msdn.microsoft.com/library/c357b221-edf6-4f68-bf40-82a3156d945a)。 這些可用於序列的函式版本，只會將序列評估為要搜尋的專案。 如需範例，請參閱[清單](https://msdn.microsoft.com/library/83102799-f251-42e1-93ef-64232e8c5b1d)。

## <a name="obtaining-subsequences"></a>取得個子序列

[Seq. filter](https://msdn.microsoft.com/library/7f2e9850-a660-460c-9831-3bbff5613770)和[Seq。選擇](https://msdn.microsoft.com/library/63b83b06-4b24-4239-bf69-a2c12d891395)與可用於清單的對應函式相似，不同之處在于在評估序列元素之前，不會進行篩選和選擇。

[[截斷](https://msdn.microsoft.com/library/1892dfeb-308e-45e2-857a-3c3405d02244)] 會從另一個序列建立順序，但會將序列限制為指定數目的專案。 [Seq. take 會](https://msdn.microsoft.com/library/6e75f701-640b-4c4a-9d63-4313fc090596)建立新的序列，其中只包含序列開頭的指定元素數目。 如果序列中的元素數目比您指定要採用的專案少，會擲回 `Seq.take` `System.InvalidOperationException` 。 和之間的差異在於， `Seq.take` `Seq.truncate` `Seq.truncate` 如果元素數目少於您指定的數目，就不會產生錯誤。

下列程式碼顯示和之間的行為差異 `Seq.truncate` `Seq.take` 。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet16.fs)]

發生錯誤之前的輸出會如下所示。

```console
1 4 9 16 25
1 4 9 16 25 36 49 64 81 100
1 4 9 16 25
1 4 9 16 25 36 49 64 81 100
```

藉由使用[takeWhile](https://msdn.microsoft.com/library/19eea4ce-66e0-4353-b015-72eb03421d92)，您可以將述詞函式指定 (布林函式) 並根據原始序列中的專案所組成的另一個序列來建立順序，但該序列是由該述詞所傳回，但是會在述詞傳回的 `true` 第一個元素之前停止 `false` 。 [Seq. skip](https://msdn.microsoft.com/library/b4eb3f08-8594-4d17-8180-852c6c688bf1)傳回的序列會略過另一個序列中第一個專案的指定數目，並傳回剩餘的元素。 [SkipWhile](https://msdn.microsoft.com/library/fb729021-2a3c-430f-83c3-0b37526f1a16)傳回的序列會略過另一個序列的第一個專案（只要述詞傳回 `true` ），然後傳回其餘的專案，從述詞傳回的第一個元素開始 `false` 。

下列程式碼範例說明、和之間的行為和 `Seq.takeWhile` 差異 `Seq.skip` `Seq.skipWhile` 。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet17.fs)]

輸出如下。

```console
1 4 9
36 49 64 81 100
16 25 36 49 64 81 100
```

## <a name="transforming-sequences"></a>轉換序列

[Seq](https://msdn.microsoft.com/library/210dcf26-4e24-4d83-af6d-a8288b2ae4b1)會建立新的序列，其中輸入序列的後續元素會分組為元組。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet18.fs)]

例如，[視窗](https://msdn.microsoft.com/library/8b565b8f-d645-4dba-be22-099075fe4744)化就像 `Seq.pairwise` ，但不會產生一系列的元組，而是會產生一系列陣列，其中包含從序列 (*視窗*) 的相鄰元素複本。 您可以在每個陣列中指定您想要的相鄰元素數目。

下列程式碼範例示範 `Seq.windowed` 的用法。 在此情況下，視窗中的元素數目是3。 此範例 `printSeq` 會使用，這是在先前的程式碼範例中定義的。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet180.fs)]

輸出如下。

初始順序：

```console
1.0 1.5 2.0 1.5 1.0 1.5

Windows of length 3:
[|1.0; 1.5; 2.0|] [|1.5; 2.0; 1.5|] [|2.0; 1.5; 1.0|] [|1.5; 1.0; 1.5|]

Moving average:
1.5 1.666666667 1.5 1.333333333
```

## <a name="operations-with-multiple-sequences"></a>具有多個序列的作業

[Seq.zip](https://msdn.microsoft.com/library/0a5df8bf-0d48-44ce-bff4-e8ef1df5bca4)和[Seq.zip3](https://msdn.microsoft.com/library/ef13bebb-22ae-4eb9-873b-87dd29154d16)接受兩個或三個序列，並產生一系列的元組。 這些函式就像是適用于[清單](https://msdn.microsoft.com/library/83102799-f251-42e1-93ef-64232e8c5b1d)的對應函數。 沒有對應的功能可將一個序列分隔成兩個或多個序列。 如果您需要序列的這種功能，請將序列轉換為清單，並使用[list. 解壓縮](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21)。

## <a name="sorting-comparing-and-grouping"></a>排序、比較和群組

清單支援的排序函數也適用于順序。 這包括[seq. sort](https://msdn.microsoft.com/library/327ea595-e77c-4529-b61e-8c6cbf5ec92e)和[sortBy](https://msdn.microsoft.com/library/4f8b4fb9-bf20-49d9-b4ee-dcc906c8208f)。 這些函式會逐一查看整個序列。

您可以使用[seq.comparewith](https://msdn.microsoft.com/library/5a740135-0b3a-4545-816f-8f91cc31290f)函數來比較兩個序列。 函式會輪流比較後續的元素，並在遇到第一個不相等的配對時停止。 任何其他元素都不會參與比較。

下列程式碼示範 `Seq.compareWith` 的用法。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet19.fs)]

在先前的程式碼中，只會計算並檢查第一個元素，而結果為-1。

[Seq.countby](https://msdn.microsoft.com/library/721702a5-150e-4fe8-81cd-ffbf8476cc1f)接受一個函式，此函式會針對每個專案產生稱為索引*鍵*的值。 在每個專案上呼叫此函式，即可為每個元素產生索引鍵。 `Seq.countBy`然後傳回包含索引鍵值的序列，以及產生每個索引鍵值的元素計數。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet201.fs)]

輸出如下。

```console
(1, 34) (2, 33) (0, 33)
```

先前的輸出顯示，原始序列中有34個元素產生金鑰1、33值產生金鑰2，以及33產生金鑰0的值。

您可以藉由呼叫[Seq. groupBy](https://msdn.microsoft.com/library/d46a04df-1a42-40cc-a368-058c9c5806fd)來分組序列的元素。 `Seq.groupBy`接受從專案產生索引鍵的序列和函式。 函式會在序列的每個元素上執行。 `Seq.groupBy`傳回一系列的元組，其中每個元組的第一個元素都是索引鍵，而第二個是產生該金鑰的專案序列。

下列程式碼範例示範 `Seq.groupBy` 如何使用將數位序列從1到100分割成三個群組，其中有相異索引鍵值0、1和2。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet202.fs)]

輸出如下。

```console
(1, seq [1; 4; 7; 10; ...]) (2, seq [2; 5; 8; 11; ...]) (0, seq [3; 6; 9; 12; ...])
```

您可以藉由呼叫[Seq. distinct](https://msdn.microsoft.com/library/99d01014-7e0e-4e7b-9d0a-41a61d93f401)來建立刪除重複元素的序列。 或者，您可以使用[seq.distinctby](https://msdn.microsoft.com/library/9293293b-9420-49c8-848f-401a9cd49b75)，它會取得要在每個元素上呼叫的索引鍵產生函式。 產生的序列包含具有唯一索引鍵之原始序列的元素。之後，會捨棄為較早的專案產生重複索引鍵的元素。

下列程式碼範例說明的用法 `Seq.distinct` 。 `Seq.distinct`會藉由產生代表二進位數的序列來示範，然後顯示唯一不同的元素為0和1。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet22.fs)]

下列 `Seq.distinctBy` 程式碼會以包含負數和正數的序列開始示範，並使用絕對值函數做為索引鍵產生函數。 產生的序列遺漏了對應于序列中負數的所有正數，因為負數會出現在序列中的前面，因此會選取，而不是具有相同絕對值或索引鍵的正數。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet23.fs)]

## <a name="readonly-and-cached-sequences"></a>Readonly 和快取的序列

[Seq。 readonly](https://msdn.microsoft.com/library/88059cb4-3bb0-4126-9448-fbcd48fe13a7)會建立序列的唯讀複本。 `Seq.readonly`當您有讀寫集合（例如陣列），而且不想修改原創組合時，會很有用。 此函式可以用來保留資料封裝。 在下列程式碼範例中，會建立包含陣列的類型。 屬性會公開陣列，但不會傳回陣列，它會傳回從陣列使用所建立的序列 `Seq.readonly` 。

[!code-fsharp[Main](~/samples/snippets/fsharp/fssequences/snippet24.fs)]

[Seq. cache](https://msdn.microsoft.com/library/d197f9cc-08bf-4986-9869-246e72ca73f0)會建立序列的預存版本。 使用 `Seq.cache` 來避免重新評估序列，或當您有多個使用序列的執行緒時，您必須確定每個元素只會在一次的情況下進行動作。 當您有多個執行緒正在使用的序列時，您可以有一個執行緒會列舉並計算原始序列的值，而其餘執行緒可以使用快取的序列。

## <a name="performing-computations-on-sequences"></a>在序列上執行計算

簡單的算數運算與清單相似，例如[seq. average](https://msdn.microsoft.com/library/609d793b-c70f-4e36-9ab4-d928056d65b8)、 [seq. sum](https://msdn.microsoft.com/library/01208515-4880-4358-91f5-af34f66dc77a)、 [averageBy](https://msdn.microsoft.com/library/47c855c1-2dbd-415a-885e-b909d9d3e4f8)、 [seq. sumBy](https://msdn.microsoft.com/library/68cca78c-94ed-4a45-9b8d-34d2c5f2b1b1)等等。

[ [Seq](https://msdn.microsoft.com/library/30c4c95a-9563-4c96-bbe1-f7aacfd026e3)]、[ [seq](https://msdn.microsoft.com/library/a2ad4f64-ac69-47d2-92f0-7173d9dfeae9)] 和 [ [seq]。 scan](https://msdn.microsoft.com/library/7e2d23e9-f153-4411-a884-b6d415ff627e)就像是可用於清單的對應函數。 序列支援這些函式的完整變數的子集，這些函式會列出支援。 如需詳細資訊和範例，請參閱[清單](lists.md)。

## <a name="see-also"></a>另請參閱

- [F # 語言參考](index.md)
- [F# 類型](fsharp-types.md)

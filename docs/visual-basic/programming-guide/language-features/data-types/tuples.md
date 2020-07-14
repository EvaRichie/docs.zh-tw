---
title: Tuple
ms.date: 04/23/2017
helpviewer_keywords:
- tuples [Visual Basic]
ms.assetid: 3e66cd1b-3432-4e1d-8c37-5ebacae8f53f
ms.openlocfilehash: 378ee4e7d3a3b106b719e5da819b09f336ff218e
ms.sourcegitcommit: 67cf756b033c6173a1bbd1cbd5aef1fccac99e34
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2020
ms.locfileid: "86226656"
---
# <a name="tuples-visual-basic"></a>元組 (Visual Basic) 

從 Visual Basic 2017 開始，Visual Basic 語言提供元組的內建支援，可讓建立元組並更輕鬆地存取元組的元素。 元組是輕量的資料結構，具有特定的數目和值序列。 當您具現化元組時，您會定義每個值 (或元素) 的數目和資料類型。 例如，2個元組 (或配對) 有兩個元素。 第一個可能是 `Boolean` 值，而第二個是 `String` 。 因為元組可讓您輕鬆地將多個值儲存在單一物件中，所以它們通常是用來從方法傳回多個值的輕量方式。

> [!IMPORTANT]
> 元組支援需要 <xref:System.ValueTuple> 類型。 如果未安裝 .NET Framework 4.7，您必須新增 nuget 套件 `System.ValueTuple` （可在 nuget 資源庫中取得）。 若沒有此套件，您可能會收到類似以下的編譯錯誤：「預先定義的類型 ' System.valuetuple (的,,, ) ' 未定義或匯入。」

## <a name="instantiating-and-using-a-tuple"></a>具現化和使用元組

您可以將元組以括弧括住的逗點分隔值具現化。 然後，每個值都會變成元組的欄位。 例如，下列程式碼會定義三個 (或3個元組) ，其中包含 `Date` 做為其第一個值、 `String` 做為第二個，以及 `Boolean` 做為第三個。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#1)]

根據預設，元組中每個欄位的名稱都包含字串， `Item` 以及該欄位在元組中以一為基礎的位置。 針對這個3元組， `Date` 欄位是 `Item1` ，欄位 `String` 是 `Item2` ， `Boolean` 欄位是 `Item3` 。 下列範例會顯示在上一行程式碼中具現化之元組的欄位值。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#2)]

Visual Basic 元組的欄位是讀寫;在具現化元組之後，您可以修改其值。 下列範例會修改上一個範例中所建立之元組的三個欄位中的兩個，並顯示結果。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#3)]

## <a name="instantiating-and-using-a-named-tuple"></a>具現化及使用命名的元組

您可以藉由將您自己的名稱指派給元組的專案，來具現化*已命名的元組*，而不是使用元組欄位的預設名稱。 然後，元組的欄位可以依其指派的名稱*或*預設名稱來存取。 下列範例會具現化與先前相同的3個元組，但它會明確地命名第一個欄位 `EventDate` 、第二個 `Name` 和第三個 `IsHoliday` 。 然後，它會顯示域值、修改它們，然後再次顯示域值。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#4)]

## <a name="inferred-tuple-element-names"></a>Tuple 型別推導

從 Visual Basic 15.3 開始，Visual Basic 可以推斷元組元素的名稱;您不需要明確地指派它們。 當您從一組變數初始化元組時，如果您想要讓元組元素名稱與變數名稱相同，則推斷的元組名稱很有用。

下列範例會建立一個 `stateInfo` 元組，其中包含三個明確命名的元素：、 `state` `stateName` 和 `capital` 。 請注意，在命名專案時，元組初始化語句只會將同名變數的值指派給已命名的元素。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#1)]

因為元素和變數具有相同的名稱，所以 Visual Basic 編譯器可以推斷欄位的名稱，如下列範例所示。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

若要啟用推斷的元組元素名稱，您必須定義要在 Visual Basic 專案中使用的 Visual Basic 編譯器版本 (\* . vbproj) 檔案：

```xml
<PropertyGroup>
  <LangVersion>15.3</LangVersion>
</PropertyGroup>
```

版本號碼可以是從15.3 開始的任何 Visual Basic 編譯器版本。 除了將特定編譯器版本硬式編碼，您也可以指定「最新」做為的值， `LangVersion` 以在系統上安裝的最新版本 Visual Basic 編譯器進行編譯。

如需詳細資訊，請參閱[設定 Visual Basic 語言版本](../../../language-reference/configure-language-version.md)。

在某些情況下，Visual Basic 編譯器無法從候選名稱推斷元組專案名稱，而且元組欄位只能使用其預設名稱（例如、等等）來參考 `Item1` `Item2` 。其中包括：

- 候選名稱與元組成員的名稱相同，例如 `Item3` 、 `Rest` 或 `ToString` 。

- 候選名稱在元組中是重複的。

當功能變數名稱推斷失敗時，Visual Basic 不會產生編譯器錯誤，也不會在執行時間擲回例外狀況。 相反地，元組欄位必須以預先定義的名稱（例如和）來參考 `Item1` `Item2` 。

## <a name="tuples-versus-structures"></a>元組與結構

Visual Basic 元組是實數值型別，它是**system.valuetuple**泛型型別之一的實例。 例如，在 `holiday` 上一個範例中定義的元組是結構的實例 <xref:System.ValueTuple%603> 。 其設計為數據的輕量容器。 因為元組的目標是要讓您輕鬆地建立具有多個資料項目的物件，所以它缺少自訂結構可能會有的部分功能。 這些包括：

- 自訂成員。 您不能為元組定義自己的屬性、方法或事件。

- 驗證： 您無法驗證指派給欄位的資料。

- 不變性. Visual Basic 元組是可變的。 相反地，自訂結構可讓您控制實例是否可變動或不可變。

如果自訂成員、屬性和欄位驗證或不可變性很重要，您應該使用 Visual Basic [Structure](../../../language-reference/statements/structure-statement.md)語句來定義自訂實值型別。

Visual Basic 元組會繼承其**system.valuetuple**類型的成員。 除了其欄位以外，這些包括下列方法：

| 成員 | 描述 |
| ---|---|
| CompareTo | 比較目前的元組與另一個具有相同專案數目的元組。 |
| 等於 | 判斷目前的元組是否等於另一個元組或物件。 |
| GetHashCode | 計算目前實例的雜湊碼。 |
| ToString | 傳回這個元組的字串表示，其採用格式 `(Item1, Item2...)` ，其中 `Item1` 和 `Item2` 代表元組欄位的值。 |

此外， **system.valuetuple**類型 <xref:System.Collections.IStructuralComparable> 會執行和 <xref:System.Collections.IStructuralEquatable> 介面，讓您定義客戶比較子。

## <a name="assignment-and-tuples"></a>指派和 Tuple

Visual Basic 支援在具有相同欄位數目的元組類型之間指派。 如果下列其中一項為真，則可以轉換欄位類型：

- [來源] 和 [目標] 欄位的類型相同。

- 已定義從來源類型到目標型別的擴展 (或隱含) 轉換。

- `Option Strict`為 `On` ，且已定義從來源類型到目標型別的縮小 (或明確) 轉換。 如果來源值超出目標型別的範圍，此轉換可能會擲回例外狀況。

不會考慮對指派進行其他轉換。 讓我們看看 Tuple 類型之間允許的指派類型。

請考慮在下列範例中使用的這些參數：

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#1)]

前兩個變數（ `unnamed` 和 `anonymous` ）沒有針對欄位提供的語義名稱。 其功能變數名稱為預設值 `Item1` 和 `Item2` 。 最後兩個變數 `named` 和 `differentName` 具有語義功能變數名稱。 請注意，這兩個 Tuple 有不同的欄位名稱。

這四個元組都有相同數目的欄位 (稱為「arity」 ) ，而這些欄位的類型則相同。 因此，所有這些指派都會運作︰

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#2)]

請注意，不會指派 Tuple 的名稱。 依欄位在 Tuple 中的順序，指派欄位的值。

最後，請注意， `named` `conversion` 即使的第一個欄位 `named` 是 `Integer` ，而且的第一個欄位是，我們 `conversion` 還是可以將元組指派給元組 `Long` 。 此指派成功 `Integer` ，因為將轉換成 `Long` 是擴輾轉換。

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#3)]

具有不同欄位數目的元組無法指派：

```vb
' Does not compile.
' VB30311: Value of type '(Integer, Integer, Integer)' cannot be converted
'          to '(Answer As Integer, Message As String)'
var differentShape = (1, 2, 3)
named = differentShape
```

## <a name="tuples-as-method-return-values"></a>Tuple 作為方法傳回值

方法只能傳回單一值。 不過，通常您會想要方法呼叫來傳回多個值。 有數種方式可解決這項限制：

- 您可以建立自訂類別或結構，其屬性或欄位代表方法所傳回的值。 因此是一種重量級解決方案;您必須定義自訂類型，其唯一的目的是要從方法呼叫中取出值。

- 您可以從方法傳回單一值，然後藉由參考傳遞給方法，以傳回其餘的值。 這牽涉到具現化變數的額外負荷，以及不小心覆寫您以傳址方式傳遞之變數值的風險。

- 您可以使用元組，它會提供輕量解決方案來抓取多個傳回值。

例如，.NET 中的**TryParse**方法會傳回一個 `Boolean` 值，指出剖析作業是否成功。 剖析作業的結果會在以傳址方式傳遞至方法的變數中傳回。 一般來說，呼叫剖析方法（例如）如下所 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 示：

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#1)]

如果我們以自己的方法將呼叫包裝至方法，我們就可以從剖析作業傳回元組 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 。 在下列範例中，會 `NumericLibrary.ParseInteger` 呼叫 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 方法，並傳回具有兩個元素的已命名元組。

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

接著，您可以使用如下的程式碼來呼叫方法：

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

## <a name="visual-basic-tuples-and-tuples-in-the-net-framework"></a>.NET Framework 中的 Visual Basic 元組和元組

Visual Basic 元組是 .NET Framework 4.7 中引進的其中一個**system.valuetuple**泛型型別的實例。 .NET Framework 也包含一組一般的**system.object**類別。 不過，這些類別與 Visual Basic 元組和**system.valuetuple**泛型型別有數種不同之處：

- **元組**類別的元素是名為 `Item1` 、等的屬性 `Item2` 。 在 Visual Basic 元組和**system.valuetuple**類型中，元組元素都是欄位。

- 您不能將有意義的名稱指派給**元組**實例或**system.valuetuple**實例的元素。 Visual Basic 可讓您指派可傳達欄位意義的名稱。

- **元組**實例的屬性是唯讀的;元組是不可變的。 在 Visual Basic 元組和**system.valuetuple**類型中，元組欄位是讀寫;元組是可變的。

- 泛型**元組**類型是參考型別。 使用這些**元組**類型表示要設定物件。 在最忙碌路徑上，這可能會對您應用程式的效能造成可觀的衝擊。 Visual Basic 元組和**system.valuetuple**類型都是實數值型別。

類別中的擴充方法 <xref:System.TupleExtensions> 可讓您輕鬆地在 Visual Basic 元組和 .Net**元組**物件之間進行轉換。 **ToTuple**方法會將 Visual Basic 元組轉換成 .Net**元組**物件，而**ToValueTuple**方法會將 .net**元組**物件轉換成 Visual Basic 元組。

下列範例會建立元組、將它轉換成 .NET**元組**物件，並將其轉換回 Visual Basic 元組。 然後，此範例會比較這個元組與原始的，以確保它們相等。

[!code-vb[Convert](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple2.vb#1)]

## <a name="see-also"></a>請參閱

- [Visual Basic 語言參考](index.md)

---
title: Const 陳述式
ms.date: 05/12/2018
f1_keywords:
- vb.Const
helpviewer_keywords:
- Const statement [Visual Basic]
ms.assetid: 495b318d-b7c5-4198-94f8-0790a541b07a
ms.openlocfilehash: 3b05d4067ef99e03df07d2c316c982051180d961
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84382103"
---
# <a name="const-statement-visual-basic"></a>Const 陳述式 (Visual Basic)

宣告並定義一或多個常數。

## <a name="syntax"></a>語法

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ]
Const constantlist
```

## <a name="parts"></a>組件

`attributelist`  
選擇性。 套用至此語句中宣告之所有常數的屬性清單。 請[Attribute List](attribute-list.md)參閱以角括弧（" `<` " 和 ""）括住的屬性清單 `>` 。

`accessmodifier`  
選擇性。 使用此項來指定哪些程式碼可以存取這些常數。 可以是[公用](../modifiers/public.md)、[受保護](../modifiers/protected.md)、 [Friend](../modifiers/friend.md)、[受保護的 Friend](../modifiers/protected-friend.md)、[私](../modifiers/private.md)用或[私用保護](../modifiers/private-protected.md)。

`Shadows`  
選擇性。 使用此專案來重新宣告和隱藏基類中的程式設計項目。 請參閱[Shadows](../modifiers/shadows.md)。

`constantlist`  
必要。 在此語句中宣告的常數清單。

`constant` `[ ,` `constant` `... ]`

每個 `constant` 都具有下列語法和組件：

`constantname` `[ As` `datatype` `] =` `initializer`

|部分|描述|
|----------|-----------------|
|`constantname`|必要。 常數的名稱。 請參閱 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)。|
|`datatype`|如果 `Option Strict` 為，則為必要 `On` 。 常數的資料類型。|
|`initializer`|必要。 在編譯時期評估並指派給常數的運算式。|

## <a name="remarks"></a>備註

如果您的應用程式中有永不變更的值，您可以定義已命名的常數，並將其取代為常值。 名稱比值更容易記住。 您可以只定義常數一次，並將其用於程式碼中的許多位置。 如果在較新的版本中，您需要重新定義值，則 `Const` 語句是您唯一需要進行變更的位置。

您 `Const` 只能在模組或程式層級使用。 這表示變數的宣告*內容*必須是類別、結構、模組、程式或區塊，而且不能是原始程式檔、命名空間或介面。 如需詳細資訊，請參閱[宣告內容和預設存取層級](declaration-contexts-and-default-access-levels.md)。

本機常數（在程式內）預設為公用存取，而且您不能在其上使用任何存取修飾詞。 類別和模組成員常數（在任何程式之外）預設為私用存取，而結構成員常數則預設為公用存取。 您可以使用存取修飾詞來調整其存取層級。

## <a name="rules"></a>規則

- **宣告內容。** 在任何程式以外的模組層級宣告的常數是*成員常數*;它是宣告它的類別、結構或模組的成員。

  在程式層級宣告的常數是*本機常數*;它是在宣告它的程式或區塊的本機。

- **特性.** 您只能將屬性套用至成員常數，而不能套用至本機常數。 屬性會將資訊提供給元件的中繼資料，這對暫存儲存體（例如本機常數）沒有意義。

- **修改.** 根據預設，所有常數都是 `Shared` 、 `Static` 和 `ReadOnly` 。 宣告常數時，您無法使用任何這些關鍵字。

  在程式層級上，您不能使用 `Shadows` 或任何存取修飾詞來宣告本機常數。

- **多個常數。** 您可以在同一個宣告語句中宣告數個常數， `constantname` 為每個常數指定元件。 以逗號分隔多個常數。

## <a name="data-type-rules"></a>資料類型規則

- **資料類型。** `Const`語句可以宣告變數的資料類型。 您可以指定任何資料類型或列舉的名稱。

- **預設類型。** 如果您未指定 `datatype` ，常數會接受的資料類型 `initializer` 。 如果您同時指定 `datatype` 和 `initializer` ，則的資料類型 `initializer` 必須可轉換為 `datatype` 。 如果 `datatype` 和 `initializer` 都不存在，資料類型會預設為 `Object` 。

- **不同的類型。** 您可以 `As` 針對您所宣告的每個變數使用個別的子句，為不同的常數指定不同的資料類型。 但是，您無法使用通用子句，將數個常數宣告為相同類型 `As` 。

- **初始.** 您必須初始化中每個常數的值 `constantlist` 。 您可以使用 `initializer` 來提供要指派給常數的運算式。 運算式可以是常值的任何組合、已定義的其他常數，以及已定義的列舉成員。 您可以使用算術和邏輯運算子來結合這類元素。

  您不能在中使用變數或函數 `initializer` 。 不過，您可以使用轉換關鍵字（例如 `CByte` 和） `CShort` 。 `AscW`如果您以常數或引數呼叫它，您也可以使用 `String` `Char` ，因為它可以在編譯時期進行評估。

## <a name="behavior"></a>行為

- **範圍.** 本機常數只能從其程式或區塊記憶體取。 成員常數可從其類別、結構或模組內的任何位置存取。

- **加.** 類別、結構或模組之外的程式碼必須使用該類別、結構或模組的名稱來限定成員常數的名稱。 程式或區塊外的程式碼無法參考該程式或區塊中的任何本機常數。

## <a name="example"></a>範例

下列範例會使用 `Const` 語句來宣告用來取代常值的常數。

[!code-vb[VbVbalrStatements#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#13)]

## <a name="example"></a>範例

如果您定義具有資料類型的常數 `Object` ，Visual Basic 編譯器會提供它的類型 `initializer` ，而不是 `Object` 。 在下列範例中，常數 `naturalLogBase` 具有執行時間類型 `Decimal` 。

[!code-vb[VbVbalrStatements#87](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#87)]

上述範例 <xref:System.Type.ToString%2A> <xref:System.Type> 會在[GetType 運算子](../operators/gettype-operator.md)傳回的物件上使用方法，因為 <xref:System.Type> 無法使用轉換成 `String` `CStr` 。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- [End 陳述式](enum-statement.md)
- [#Const 指示詞](../directives/const-directive.md)
- [Dim 陳述式](dim-statement.md)
- [ReDim 陳述式](redim-statement.md)
- [隱含和明確轉換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [常數和列舉](../../programming-guide/language-features/constants-enums/index.md)
- [常數和列舉](../constants-and-enumerations.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)

---
title: 使用者定義資料類型
ms.date: 07/20/2015
f1_keywords:
- UserDefined
- UDT
- vb.UDT
- User-Defined
- vb.UserDefined
- vb.User-Defined
helpviewer_keywords:
- user-defined data types [Visual Basic], Visual Basic
- user-defined types
- structures [Visual Basic], as user-defined data types
- user-defined types [Visual Basic], Visual Basic
- user-defined types [Visual Basic], structure declaration
- user-defined types [Visual Basic], structures in Visual Basic
- user-defined data types [Visual Basic], structure declaration
- data types [Visual Basic], assigning
- Structure statement [Visual Basic]
- data types [Visual Basic], user-defined
- user-defined data types [Visual Basic], structures in Visual Basic
- user-defined data types
- types [Visual Basic], user-defined
ms.assetid: be913dca-a364-4a51-96a1-549a1b390b0a
ms.openlocfilehash: fbd9536a54d7fb471d6cb2e130b14a84e40a4940
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415488"
---
# <a name="user-defined-data-type"></a>使用者定義資料類型

以您定義的格式來保存資料。 `Structure`語句會定義格式。

舊版的 Visual Basic 支援使用者定義型別（UDT）。 目前的版本會將 UDT 擴充至*結構*。 結構是一或多個不同資料類型*成員*的串連。 Visual Basic 會將結構視為單一單位，不過您也可以個別存取其成員。

## <a name="remarks"></a>備註

當您需要將各種資料類型結合成單一單位，或沒有任何基本資料類型滿足您的需求時，請定義和使用結構資料類型。

結構資料類型的預設值是由其每個成員的預設值組合所組成。

## <a name="declaration-format"></a>宣告格式

結構宣告會以[結構語句](../statements/structure-statement.md)開頭，並以語句結尾 `End Structure` 。 `Structure`語句會提供結構的名稱，這也是結構所定義之資料類型的識別碼。 程式碼的其他部分可以使用此識別碼來宣告變數、參數和函式傳回值，使其成為此結構的資料類型。

和語句之間的宣告會 `Structure` `End Structure` 定義結構的成員。

## <a name="member-access-levels"></a>成員存取層級

您必須使用[Dim 語句](../statements/dim-statement.md)或指定存取層級的語句（例如[Public](../modifiers/public.md)、 [Friend](../modifiers/friend.md)或[Private](../modifiers/private.md)）來宣告每個成員。 如果您使用 `Dim` 語句，存取層級預設為 [公用]。

## <a name="programming-tips"></a>程式設計提示

- **記憶體耗用量。** 如同所有複合資料型別，您無法安全地計算結構的總記憶體耗用量，方法是將其成員的名義儲存體配置相加。 此外，您無法安全地假設記憶體中的儲存順序與您的宣告順序相同。 如果您需要控制結構的儲存配置，您可以將 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 屬性套用至 `Structure` 語句。

- **Interop 考量：** 如果您要使用的元件不是針對 .NET Framework 所撰寫（例如 Automation 或 COM 物件），請記住，其他環境中的使用者定義類型與 Visual Basic 結構類型不相容。

- **加寬.** 沒有任何結構資料類型的自動轉換。 您可以使用[運算子語句](../statements/operator-statement.md)定義結構上的轉換運算子，也可以將每個轉換運算子宣告為 `Widening` 或 `Narrowing` 。

- **輸入字元。** 結構資料類型沒有常數值型別字元或識別項型別字元。

- **架構類型：** .NET Framework 中沒有對應的類型。 所有結構都會繼承自 .NET Framework 類別 <xref:System.ValueType?displayProperty=nameWithType> ，但不會對應到任何個別結構 <xref:System.ValueType?displayProperty=nameWithType> 。

## <a name="example"></a>範例

下列範例顯示結構宣告的外框。

```vb
[Public | Protected | Friend | Protected Friend | Private] Structure structname
    {Dim | Public | Friend | Private} member1 As datatype1
    ' ...
    {Dim | Public | Friend | Private} memberN As datatypeN
End Structure
```

## <a name="see-also"></a>另請參閱

- <xref:System.ValueType>
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- [資料類型](index.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)
- [轉換摘要](../keywords/conversion-summary.md)
- [Structure 陳述式](../statements/structure-statement.md)
- [Widening](../modifiers/widening.md)
- [Narrowing](../modifiers/narrowing.md)
- [結構](../../programming-guide/language-features/data-types/structures.md)
- [有效率地使用資料類型](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)

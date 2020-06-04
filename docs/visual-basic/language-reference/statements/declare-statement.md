---
title: Declare Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Declare
- vb.Lib
- vb.Any
helpviewer_keywords:
- Lib keyword [Visual Basic]
- declaring procedures [Visual Basic], Declare statement
- functions [Visual Basic], function procedures
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- procedures [Visual Basic], external
- Alias keyword [Visual Basic]
- external references [Visual Basic], Visual Basic
- DLLs, declaring procedures
- Declare statement [Visual Basic]
- declarations [Visual Basic], external
- Visual Basic code, Function procedures
- As keyword [Visual Basic], in Declare statement
- resources [Visual Basic], declaring
- Public keyword [Visual Basic], Declare statement
- platform invoke, Visual Basic external references
- Sub procedures [Visual Basic], declarations
- APIs, declaring API functions
- Visual Basic code, Sub procedures
- Function procedures [Visual Basic], declaring
ms.assetid: d3f21fb0-b804-4c99-97ed-583b23894cf1
ms.openlocfilehash: 021805508a8a053ccc8fab6f1013109bece4b6f2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404767"
---
# <a name="declare-statement"></a>Declare Statement

宣告在外部檔案中執行之程式的參考。

## <a name="syntax"></a>語法

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Sub ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ]
' -or-
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Function ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ] [ As returntype ]
```

## <a name="parts"></a>組件

|詞彙|定義|
|---|---|
|`attributelist`|選擇性。 請參閱[屬性清單](attribute-list.md)。|
|`accessmodifier`|選擇性。 可以是下列其中一項：<br /><br /> -   [公立](../modifiers/public.md)<br />-   [免受](../modifiers/protected.md)<br />-   [給](../modifiers/friend.md)<br />-   [私人](../modifiers/private.md)<br />- [受保護的 Friend](../modifiers/protected-friend.md)<br />- [私用保護](../modifiers/private-protected.md)<br /><br /> 請參閱[Visual Basic 中的存取層級](../../programming-guide/language-features/declared-elements/access-levels.md)。|
|`Shadows`|選擇性。 請參閱[Shadows](../modifiers/shadows.md)。|
|`charsetmodifier`|選擇性。 指定字元集和檔案搜尋資訊。 可以是下列其中一項：<br /><br /> -   [Ansi](../modifiers/ansi.md) （預設值）<br />-   [消除](../modifiers/unicode.md)<br />-   [自動](../modifiers/auto.md)|
|`Sub`|選擇性，但 `Sub` 或 `Function` 必須出現。 表示外部程式不會傳回值。|
|`Function`|選擇性，但 `Sub` 或 `Function` 必須出現。 表示外部程式會傳回值。|
|`name`|必要。 此外部參考的名稱。 如需詳細資訊，請參閱宣告的[元素名稱](../../programming-guide/language-features/declared-elements/declared-element-names.md)。|
|`Lib`|必要。 引進 `Lib` 子句，其可識別包含外部程式的外部檔案（DLL 或程式碼資源）。|
|`libname`|必要。 包含宣告之程式的檔案名。|
|`Alias`|選擇性。 表示所宣告的程式無法在其檔案中以指定的名稱識別 `name` 。 您在中指定其識別 `aliasname` 。|
|`aliasname`|如果您使用關鍵字，則為必要 `Alias` 。 以兩種方式之一來識別程式的字串：<br /><br /> 程式在其檔案中的進入點名稱，以引號括住（ `""` ）<br /><br /> -或-<br /><br /> 數位記號（ `#` ），後面接著一個整數，指定程式在其檔案中的進入點序號|
|`parameterlist`|如果程式採用參數，則為必要。 請參閱[參數清單](parameter-list.md)。|
|`returntype`|如果 `Function` 已指定，且 `Option Strict` 為，則為必要 `On` 。 程式所傳回值的資料類型。|

## <a name="remarks"></a>備註

有時候您需要呼叫專案外部檔案中定義的程式（例如 DLL 或程式碼資源）。 當您這麼做時，Visual Basic 編譯器無法存取正確呼叫程式所需的資訊，例如程式所在位置、識別方式、其呼叫順序和傳回類型，以及它所使用的字串字元集。 `Declare`語句會建立外部程式的參考，並提供此必要資訊。

您只能在模組層級使用 `Declare`。 這表示外部參考的宣告*內容*必須是類別、結構或模組，而且不能是原始程式檔、命名空間、介面、程式或區塊。 如需詳細資訊，請參閱[宣告內容和預設存取層級](declaration-contexts-and-default-access-levels.md)。

外部參考預設為[公用](../modifiers/public.md)存取。 您可以使用存取修飾詞來調整其存取層級。

## <a name="rules"></a>規則

- **特性.** 您可以將屬性套用至外部參考。 您套用的任何屬性只有在您的專案中才有效，而不是在外部檔案中。

- **修改.** 外部程式會隱含[共用](../modifiers/shared.md)。 您不能在宣告 `Shared` 外部參考時使用關鍵字，也無法改變其共用狀態。

  外部程式無法參與覆寫、執行介面成員或處理事件。 因此，您無法 `Overrides` `Overridable` 在語句中使用、、、、 `NotOverridable` `MustOverride` `Implements` 或 `Handles` 關鍵字 `Declare` 。

- **外部程式名稱。** 您不需要在外部檔案（）中，將此外部參考指定為與程式的進入點名稱相同的名稱（在中 `name` 為） `aliasname` 。 您可以使用 `Alias` 子句來指定進入點名稱。 如果外部程式的名稱與 Visual Basic 保留的修飾詞或變數、程式或相同範圍中的任何其他程式設計項目同名，這就很有用。

  > [!NOTE]
  > 大部分 Dll 中的進入點名稱都區分大小寫。

- **外部程式編號。** 或者，您可以使用 `Alias` 子句來指定外部檔案之匯出資料表內進入點的序號。 若要這麼做，請從 `aliasname` 數位記號（ `#` ）開始。 如果 Visual Basic 中不允許外部程式名稱中的任何字元，或如果外部檔案匯出程式但沒有名稱，這會很有用。

## <a name="data-type-rules"></a>資料類型規則

- **參數資料類型。** 如果 `Option Strict` 是 `On` ，您就必須在中指定每個參數的資料類型 `parameterlist` 。 這可以是任何資料類型，或是列舉、結構、類別或介面的名稱。 在中 `parameterlist` ，您可以使用 `As` 子句來指定要傳遞至每個參數之引數的資料類型。

  > [!NOTE]
  > 如果未針對 .NET Framework 寫入外部程式，您必須注意資料類型對應。 例如，如果您使用參數（Visual Basic 6.0 中的16位）來宣告 Visual Basic 6.0 程式的外部參考 `Integer` ，則必須在語句中識別對應的引數 `Short` `Declare` ，因為這是 Visual Basic 中的16位整數類型。 同樣地， `Long` 在 Visual Basic 6.0 中具有不同的資料寬度，並以 `Date` 不同方式執行。

- **傳回資料類型。** 如果外部程式是 `Function` `Option Strict` ，而是 `On` ，則您必須指定傳回給呼叫程式碼之值的資料類型。 這可以是任何資料類型，或是列舉、結構、類別或介面的名稱。

  > [!NOTE]
  > Visual Basic 編譯器不會驗證您的資料類型是否與外部程式的相容。 如果出現不相符的情況，common language runtime 會 <xref:System.Runtime.InteropServices.MarshalDirectiveException> 在執行時間產生例外狀況。

- **預設資料類型。** 如果 `Option Strict` 為， `Off` 而您未在中指定參數的資料類型 `parameterlist` ，則 Visual Basic 編譯器會將對應的引數轉換為[Object 資料類型](../data-types/object-data-type.md)。 同樣地，如果您未指定 `returntype` ，編譯器會將傳回資料類型設為 `Object` 。

  > [!NOTE]
  > 由於您正在處理的外部程式可能是在不同的平臺上撰寫的，因此，對資料類型或允許其預設值的任何假設都是危險的。 指定每個參數的資料類型和傳回值（如果有的話），會比較安全。 這也可以改善程式碼的可讀性。

## <a name="behavior"></a>行為

- **範圍.** 外部參考在其類別、結構或模組的範圍內。

- **期.** 外部參考具有與宣告所在的類別、結構或模組相同的存留期。

- **呼叫外部程式。** 以呼叫或程式的相同方式呼叫外部程式 `Function` `Sub` （如果它傳回值，則在運算式中使用它），或在[呼叫語句](call-statement.md)中指定它（如果未傳回值）。

  您可以將引數傳遞至與語句中所指定完全相同的外部程式 `parameterlist` `Declare` 。 請勿將參數原本在外部檔案中宣告的方式納入考慮。 同樣地，如果有傳回值，請在語句中使用與所指定完全相同的方法 `returntype` `Declare` 。

- **字元集。** 您可以指定 `charsetmodifier` Visual Basic 在呼叫外部程式時，應該如何封送處理字串。 `Ansi`修飾詞會引導 Visual Basic 將所有字串封送處理為 ANSI 值，而 `Unicode` 修飾詞會指示它將所有字串封送處理成 Unicode 值。 修飾詞會 `Auto` 根據外部參考的 .NET Framework 規則 `name` ，或在指定時，指示 Visual Basic 來封送處理字串 `aliasname` 。 預設值為 `Ansi`。

  `charsetmodifier`同時也會指定 Visual Basic 如何在外部檔案中查詢外部程式。 `Ansi`而且 `Unicode` 直接 Visual Basic 在搜尋期間不修改其名稱來進行查詢。 `Auto`會引導 Visual Basic 判斷執行時間平臺的基底字元集，而且可能會修改外部程式名稱，如下所示：

  - 在 ANSI 平臺上（例如 Windows 95、Windows 98 或 Windows Millennium Edition），請先查閱外部程式而不修改名稱。 如果失敗，請將 "A" 附加至外部程式名稱的結尾，然後重新查詢。

  - 在 Unicode 平臺上（例如 Windows NT、Windows 2000 或 Windows XP），請先查閱外部程式而不修改名稱。 如果失敗，請將 "W" 附加至外部程式名稱的結尾，然後重新查詢。

- **機構.** Visual Basic 使用 .NET Framework*平台叫用*（PInvoke）機制來解析和存取外部程式。 `Declare`語句和 <xref:System.Runtime.InteropServices.DllImportAttribute> 類別都會自動使用這項機制，而且您不需要任何的 PInvoke 知識。 如需詳細資訊，請參閱[逐步解說：呼叫 Windows api](../../programming-guide/com-interop/walkthrough-calling-windows-apis.md)。

> [!IMPORTANT]
> 如果外部程式是在 common language runtime （CLR）外部執行，則為*非受控碼*。 當您呼叫這類程式（例如，Windows API 函式或 COM 方法）時，可能會讓您的應用程式暴露于安全性風險下。 如需詳細資訊，請參閱[安全的非受控碼程式碼撰寫方針](https://docs.microsoft.com/previous-versions/dotnet/framework/security/secure-coding-guidelines-for-unmanaged-code)。

## <a name="example"></a>範例

下列範例 `Function` 會宣告會傳回目前使用者名稱之程式的外部參考。 然後，它會在程式中呼叫外部程式 `GetUserNameA` `getUser` 。

[!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]

## <a name="example"></a>範例

<xref:System.Runtime.InteropServices.DllImportAttribute>提供了在非受控程式碼中使用函式的替代方式。 下列範例會宣告已匯入的函式，而不使用 `Declare` 語句。

[!code-vb[VbVbalrStatements#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#16)]

[!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [Imports 陳述式 (.NET 命名空間和類型)](imports-statement-net-namespace-and-type.md)
- [AddressOf 運算子](../operators/addressof-operator.md)
- [Function 陳述式](function-statement.md)
- [Sub 陳述式](sub-statement.md)
- [參數清單](parameter-list.md)
- [Call 陳述式](call-statement.md)
- [逐步解說：呼叫 Windows API](../../programming-guide/com-interop/walkthrough-calling-windows-apis.md)

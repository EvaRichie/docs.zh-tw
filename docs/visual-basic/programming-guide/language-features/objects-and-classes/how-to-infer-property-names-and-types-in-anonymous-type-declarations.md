---
title: 如何：在匿名類型宣告中推斷屬性名稱和類型
ms.date: 07/20/2015
helpviewer_keywords:
- inferring property names [Visual Basic]
- anonymous types [Visual Basic], inferring property names and types
- inferring property types [Visual Basic]
ms.assetid: 7c748b22-913f-4d9d-b747-6b7bf296a0bc
ms.openlocfilehash: 9ebbbe9d2e6d36f5ab2bc7f7c916d18c9240a06d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404884"
---
# <a name="how-to-infer-property-names-and-types-in-anonymous-type-declarations-visual-basic"></a>如何：在匿名類型宣告中推斷屬性名稱和類型 (Visual Basic)

匿名類型未提供任何機制來直接指定屬性的資料類型。 所有屬性的類型都是推斷而來。 在下列範例中，透過用來初始化 `Name` 和 `Price` 類型的值，直接推斷這些類型。

[!code-vb[VbVbalrAnonymousTypes#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#1)]

匿名類型也可以推斷其他來源的屬性名稱和類型。 以下章節提供可進行推斷的情況清單，以及不可進行推斷的狀況範例。

## <a name="successful-inference"></a>成功推斷

#### <a name="anonymous-types-can-infer-property-names-and-types-from-the-following-sources"></a>匿名類型可以推斷下列來源的屬性名稱和類型：

- 透過變數名稱。 匿名類型 `anonProduct` 會有兩個屬性： `productName` 和 `productPrice`。 其資料類型分別是下列原始變數： `String` 和 `Double`。

  [!code-vb[VbVbalrAnonymousTypes#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#11)]

- 透過其他物件的屬性或欄位名稱。 例如，考慮使用類型為 `car` 且包含 `CarClass` 和 `Name` 屬性的 `ID` 物件。 若要利用使用 `car1`物件值初始化的 `Name` 和 `ID` 屬性來建立新的匿名類型執行個體 ( `car` )，您可以撰寫下列項目：

  [!code-vb[VbVbalrAnonymousTypes#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#34)]

  先前的宣告等同於定義匿名類型 `car2`的較長程式碼行。

  [!code-vb[VbVbalrAnonymousTypes#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#35)]

- 透過 XML 成員名稱。

  [!code-vb[VbVbalrAnonymousTypes#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#12)]

  針對 `anon` 產生的屬性會有一個類型 `Book`(Of XElement) 的屬性 <xref:System.Collections.IEnumerable>。

- 透過沒有參數的函式 (如下列範例中的 `SomeFunction` )。

  ```vb
  Dim sc As New SomeClass
  Dim anon1 = New With {Key sc.SomeFunction()}
  ```

  下列程式碼中的變數 `anon2` 是具有一個屬性 (名稱為 `First`的字元) 的匿名類型。 此程式碼會顯示字母 "E" (即函式 <xref:System.Linq.Enumerable.First%2A>所傳回的字母)。

  [!code-vb[VbVbalrAnonymousTypes#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#13)]

## <a name="inference-failures"></a>推斷失敗

#### <a name="name-inference-will-fail-in-many-circumstances-including-the-following"></a>在許多情況下，名稱推斷都會失敗，包括下列情況：

- 推斷衍生自叫用方法、建構函式或需要引數的參數化屬性。 如果 `anon1` 有一個或多個引數，則 `someFunction` 的先前宣告會失敗。

  ```vb
  ' Not valid.
  ' Dim anon3 = New With {Key sc.someFunction(someArg)}
  ```

  指派給新的屬性名稱可解決問題。

  ```vb
  ' Valid.
  Dim anon4 = New With {Key .FunResult = sc.someFunction(someArg)}
  ```

- 推斷衍生自複雜運算式。

  ```vb
  Dim aString As String = "Act "
  ' Not valid.
  ' Dim label = New With {Key aString & "IV"}
  ```

  將運算式的結果指派給屬性名稱，即可解決錯誤。

  [!code-vb[VbVbalrAnonymousTypes#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#14)]

- 多個屬性的推斷會產生兩個或多個同名的屬性。 推斷回先前範例中的宣告，無法將 `product.Name` 和 `car1.Name` 列為相同匿名類型的屬性。 原因是所有的推斷識別項都是 `Name`。

  ```vb
  ' Not valid.
  ' Dim anon5 = New With {Key product.Name, Key car1.Name}
  ```

  將值指派給不同的屬性名稱，即可解決問題。

  [!code-vb[VbVbalrAnonymousTypes#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#36)]

  請注意，大小寫的變更 (大寫與小寫字母之間的變更) 並不會讓這兩個名稱不同。

  ```vb
  Dim price = 0
  ' Not valid, because Price and price are the same name.
  ' Dim anon7 = New With {Key product.Price, Key price}
  ```

- 一個屬性的初始類型和值取決於尚未建立的另一個屬性。 例如，除非已初始化 `.IDName = .LastName` ，否則 `.LastName` 在匿名類型宣告中無效。

  ```vb
  ' Not valid.
  ' Dim anon8 = New With {Key .IDName = .LastName, Key .LastName = "Jones"}
  ```

  在此範例中，您可以反轉屬性的宣告順序來修正問題。

  [!code-vb[VbVbalrAnonymousTypes#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#15)]

- 匿名類型的屬性名稱與 <xref:System.Object>成員的名稱相同。 例如，因為 `Equals` 是 <xref:System.Object>的方法，所以下列宣告會失敗。

  ```vb
  ' Not valid.
  ' Dim relationsLabels1 = New With {Key .Equals = "equals", Key .Greater = _
  '                       "greater than", Key .Less = "less than"}
  ```

  變更屬性名稱，即可修正問題：

  [!code-vb[VbVbalrAnonymousTypes#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#16)]

## <a name="see-also"></a>另請參閱

- [物件初始設定式：具名和匿名型別](object-initializers-named-and-anonymous-types.md)
- [區域型別推斷](../variables/local-type-inference.md)
- [匿名類型](anonymous-types.md)
- [關鍵](../../../language-reference/modifiers/key.md)

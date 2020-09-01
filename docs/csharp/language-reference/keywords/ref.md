---
description: ref 關鍵字 - C# 參考
title: ref 關鍵字 - C# 參考
ms.date: 04/21/2020
f1_keywords:
- ref_CSharpKeyword
- ref
helpviewer_keywords:
- parameters [C#], ref
- ref keyword [C#]
ms.openlocfilehash: 58a4ce30e11ca023b50e5e53b1f1554a30d44390
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89137080"
---
# <a name="ref-c-reference"></a>ref (C# 參考)

`ref` 關鍵字指出以傳址方式傳遞的值。 它用於三個不同的內容：

- 在方法簽章和方法呼叫中，以傳址方式將引數傳遞給方法。 如需詳細資訊，請參閱[以傳址方式傳遞引數](#passing-an-argument-by-reference)。
- 在方法簽章中，以傳參考方式將值傳回給呼叫者。 如需詳細資訊，請參閱[參考傳回值](#reference-return-values)。
- 在成員主體中，指出參考傳回值儲存在本機作為呼叫者想要修改的參考，或是一般而言，以參考存取另一個值的區域變數。 如需詳細資訊，請參閱 [ref 區域變數](#ref-locals)。
- 在 `struct` 宣告中來宣告 `ref struct` 或 `readonly ref struct`。 如需詳細資訊，請參閱[結構類型](../builtin-types/struct.md)一文的[ `ref` 結構](../builtin-types/struct.md#ref-struct)一節。

## <a name="passing-an-argument-by-reference"></a>以傳址方式傳遞引數

用於方法的參數清單時，`ref` 關鍵字指出以傳參考方式傳遞引數，而不是以傳值方式。 `ref` 關鍵字會使形式參數成為引數的別名，其必須為變數。 換句話說，參數上的任何作業都會在引數上進行。 例如，如果呼叫端傳遞區域變數運算式或陣列元素存取運算式，而且被呼叫的方法取代 ref 參數所參考的物件，則呼叫端的區域變數或陣列元素現在會在方法傳回時參考新的物件。

> [!NOTE]
> 請勿將參考傳遞的概念與參考類型的概念相混淆。 兩個概念並不相同。 方法參數可以由 `ref` 修改，而不論其是否為實值類型或參考類型。 當實值類型由參考傳遞時，沒有 boxing。  

若要使用 `ref` 參數，方法定義和呼叫方法都必須明確使用 `ref` 關鍵字，如下列範例所示。  

[!code-csharp-interactive[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#1)]

傳遞至 `ref` 或 `in` 參數的引數，必須在傳遞之前先初始化。 這與 [out](out-parameter-modifier.md) 參數不同，其引數不需要在傳遞之前先明確初始化。

類別的成員的簽章，不能只有在 `ref`、`in` 或 `out` 部分不同。 如果類型的兩個成員之間，唯一的區別在於其中一個有 `ref` 參數，而另一個有 `out` 或 `in` 參數，則會發生編譯器錯誤。 例如，下列程式碼不會進行編譯。  

```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```

但如果一種方法有 `ref`、`in` 或 `out` 參數，而另一種方法有實值參數，則可以對方法進行多載，如下範例所示。
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#2)]
  
 其他需要簽章比對的情況 (像是隱藏或覆寫)，`in`、`ref` 及 `out` 是簽章的一部分，但彼此不相符。  
  
 屬性不是變數。 它們都是方法，且不能傳遞給 `ref` 參數。  
  
 您不可為下列幾種方法使用 `ref`、`in` 和 `out` 關鍵字：  
  
- 使用 [async](async.md) 修飾詞定義的 async 方法。  
- 迭代器方法，其包括 [yield return](yield.md) 或 `yield break` 陳述式。

此外， [擴充方法](../../programming-guide/classes-and-structs/extension-methods.md) 具有下列限制：

- `out`關鍵字不能用在擴充方法的第一個引數上。
- `ref`當引數不是結構，或是不受限於不是結構的泛型型別時，無法在擴充方法的第一個引數上使用關鍵字。
- `in`除非第一個引數是結構，否則無法使用關鍵字。 `in`關鍵字不能用於任何泛型型別，即使當條件約束為結構時也一樣。

## <a name="passing-an-argument-by-reference-an-example"></a>以傳址方式傳遞引數：範例

先前的範例會以傳參考方式傳遞實值型別。 您也可以使用 `ref` 關鍵字，以傳參考方式傳遞參考型別。 以傳址方式傳遞參考型別，可讓已呼叫方法取代參考參數在呼叫者中所參考的物件。 物件的儲存位置會以參考參數值的方式，傳遞至方法。 如果您變更參數儲存位置中的值 (指向新的物件)，則也會變更呼叫端所參考的儲存位置。 下列範例會以 `ref` 參數，傳遞參考類型的執行個體。
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#3)]

如需如何依傳值和依傳址方式來傳遞參考類型的詳細資訊，請參閱[傳遞參考類型參數](../../programming-guide/classes-and-structs/passing-reference-type-parameters.md)。
  
## <a name="reference-return-values"></a>參考傳回值

參考傳回值 (或 ref 傳回值) 是方法以傳參考方式傳回給呼叫者的值。 也就是說，呼叫者可以修改方法所傳回的值，而且該變更會反映在呼叫方法中物件的狀態。

參考傳回值是使用 `ref` 關鍵字所定義：

- 在方法簽章中。 例如，下列方法簽章指出 `GetCurrentPrice` 方法以傳參考方式傳回 <xref:System.Decimal> 值。

```csharp
public ref decimal GetCurrentPrice()
```

- `return` 權杖與方法之 `return` 陳述式中所傳回變數之間。 例如：

```csharp
return ref DecimalArray[0];
```

為了讓呼叫者修改物件的狀態，參考傳回值必須儲存至明確定義為 [ref 區域變數](#ref-locals)的變數。

以下是更完整的 ref 傳回範例，同時顯示方法簽章和方法主體。

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

所呼叫的方法也可能將傳回值宣告為 `ref readonly`，以透過傳址方式將值傳回，並且強制使呼叫程式碼無法修改傳回值。 呼叫的方法可以將值儲存在區域 [ref readonly](#ref-readonly-locals) 變數，以避免複製傳回值。

如需範例，請參閱 [ref 傳回值和 ref 區域變數範例](#a-ref-returns-and-ref-locals-example)。

## <a name="ref-locals"></a>ref 區域變數

ref 區域變數用來參考使用 `return ref` 所傳回的值。 ref 區域變數無法初始化至非 ref 傳回值。 換句話說，初始化的右手邊必須是參考。 任何對 ref 區域變數值進行的修改，都會反映在其方法以傳址方式傳回值之物件的狀態。

定義 ref 區域變數的方式是在變數宣告前面使用 `ref` 關鍵字，並且緊接在以傳參考方式傳回值的方法呼叫前面。

例如，下列陳述式定義名為 `GetEstimatedValue` 之方法所傳回的 ref 區域變數值：

```csharp
ref decimal estValue = ref Building.GetEstimatedValue();
```

您可透過相同方式以參考存取值。 在某些情況下，以參考存取值會避免潛在過度浪費資源的複製作業，進而增加效能。 例如，下列陳述式示範了如何定義用於參考值的區域變數值。

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

在這兩個範例中 `ref` ，關鍵字都必須用於這兩個位置，否則編譯器會產生錯誤 CS8172 「無法使用值將傳址變數初始化」。

從 C# 7.3 開始，`foreach` 陳述式的反覆運算變數可以是 ref 區域變數或 ref readonly 區域變數。 如需詳細資訊，請參閱 [foreach 陳述式](foreach-in.md)一文。

此外，從 c # 7.3 開始，您可以使用 [ref 指派運算子](../operators/assignment-operator.md#ref-assignment-operator)重新指派 ref 區域變數或 ref readonly 區域變數。

## <a name="ref-readonly-locals"></a>ref readonly 區域變數

ref readonly 區域變數是用來參考傳回值 (由特徵標記中有 `ref readonly` 且使用 `return ref` 的方法或屬性傳回)。 `ref readonly` 區域變數結合了 `ref` 區域變數的屬性和 `readonly` 變數：它是受指派之儲存體的別名，且無法修改。

## <a name="a-ref-returns-and-ref-locals-example"></a>ref 傳回值和 ref 區域變數範例

下面範例會定義具有 `Title` 和 `Author` 這兩個 <xref:System.String> 欄位的 `Book` 類別。 它也會定義 `BookCollection` 類別，以包含 `Book` 物件的私用陣列。 以傳址方式傳回個別書籍物件，方法是呼叫其 `GetBookByTitle` 方法。

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#4)]

呼叫者將 `GetBookByTitle` 方法所傳回的值儲存為 ref 區域變數時，呼叫者對傳回值進行的變更會反映在 `BookCollection` 物件中，如下列範例所示。

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#5)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [撰寫安全有效率的程式碼](../../write-safe-efficient-code.md)
- [ref 傳回值和 ref 區域變數](../../programming-guide/classes-and-structs/ref-returns.md)
- [條件 ref 運算式](../operators/conditional-operator.md#conditional-ref-expression)
- [傳遞參數](../../programming-guide/classes-and-structs/passing-parameters.md)
- [方法參數](method-parameters.md)
- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)

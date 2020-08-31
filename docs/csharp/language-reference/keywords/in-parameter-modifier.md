---
description: in 參數修飾詞 - C# 參考
title: in 參數修飾詞 - C# 參考
ms.date: 03/19/2020
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
ms.openlocfilehash: 613be9248e6ce9b974bcab1b59abd30469e9e180
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89118400"
---
# <a name="in-parameter-modifier-c-reference"></a>in 參數修飾詞 (C# 參考)

`in` 關鍵字會導致引數由參考傳遞。 它會使形式參數成為引數的別名，其必須為變數。 換句話說，參數上的任何作業都會在引數上進行。 它就像 [ref](ref.md) 或 [out](out-parameter-modifier.md) 關鍵字，不同的是 `in` 引數不能被呼叫的方法修改。 雖然 `ref` 引數可以被修改，`out` 引數則必須由呼叫方法修改，且那些修改在呼叫的內容中是可觀察的。

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

上述範例示範了 `in` 修飾詞在呼叫位置通常非必要。 而只有在宣告方法時才會需要該項目。

> [!NOTE]
> `in` 關鍵字也可與泛型型別搭配使用，來指定類型參數是否為 Contravariant、屬於 `foreach` 陳述式的一部分，或是屬於 LINQ 查詢中的 `join` 子句。 如需如何在這些內容中使用 `in` 關鍵字的詳細資訊，請參閱 [in](in.md)，其提供所有這些使用的連結。
  
傳遞為 `in` 引數的變數，必須先經過初始化，才能在方法呼叫中傳遞。 但是，呼叫方法可能不會指派值或修改引數。  

`in` 參數修飾詞在 C# 7.2 與更新版本中可用。 先前的版本會產生編譯器錯誤 `CS8107` (C# 7.0 中無法使用 '唯讀參考' 功能。 請使用語言版本 7.2 或更高的版本。」) 若要設定編譯器語言版本，請參閱[選取 C# 語言版本](../configure-language-version.md)。

針對多載解析的目的，`in`、`ref` 和 `out` 關鍵字不被視為方法簽章的一部分。 因此，如果唯一的差別是一種方法採用 `ref` 或 `in` 引數，而另一種方法採用 `out` 引數，則無法對方法進行多載。 例如，將不會編譯下列程式碼：  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
允許取決於 `in` 是否存在的多載：  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a>多載解析規則

您可以透過了解 `in` 引數的動機，來了解傳值方式與 `in` 引數的方法多載解析規則。 使用 `in` 參數定義方法可能會使效能最佳化。 某些 `struct` 型別引數可能大小很大，在緊密迴圈或關鍵程式碼路徑中呼叫方法時，複製那些結構的成本便很重要。 方法會宣告 `in` 參數，以指定可以用傳址方式安全地傳遞引數，因為被呼叫的方法不會修改該引數的狀態。 以傳址方式傳遞那些引數，可避免 (可能) 相當耗費資源的複製。

針對呼叫位置的引數指定 `in` 通常是選擇性的。 以傳值方式傳遞引數，和使用 `in` 修飾詞以傳址方式傳遞引數，兩者之間沒有語意差異。 呼叫位置的 `in` 修飾詞是選擇性的，因為您不需要指出引數的值可能會變更。 在呼叫位置明確地新增 `in` 修飾詞，可以確保引數是以傳址方式傳遞，而非以傳值方式傳遞。 明確地使用 `in` 有下列兩個效果：

首先，在呼叫位置指定 `in` 會強制編譯器選取定義了符合之 `in` 參數的方法。 否則，當兩個方法的差異只在於 `in` 是否存在時，傳值方式的多載是較佳的相符項目。

第二，指定 `in` 會宣告您以傳址方式傳遞引數的意圖。 搭配 `in` 使用的引數必須代表可以直接參考的位置。 `out` 和 `ref` 引數的相同一般規則同樣適用：您無法使用常數、一般屬性或其他會產生值的運算式。 否則，在呼叫位置省略 `in` 會通知編譯器，您將允許它建立暫存變數，傳遞唯讀參考給方法。 編譯器會建立暫存變數，以克服 `in` 引數的幾項限制：

- 暫存變數允許編譯時期常數作為 `in` 參數。
- 暫存變數允許屬性或其他運算式作為 `in` 參數。
- 暫存變數允許隱含從引數型別轉換成參數型別的引數。

在所有先前的情況下，編譯器會建立暫存變數，儲存常數、屬性或其他運算式的值。

下列程式碼說明這些規則：

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

現在，假設可以使用另一個使用傳值引數的方法。 結果的變更如下列程式碼所示：

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

以傳址方式傳遞引數的唯一方法呼叫，是最終的方法呼叫。

> [!NOTE]
> 為簡單起見，上述程式碼使用 `int` 作為引數型別。 因為 `int` 在大多數新型電腦中，不會比參考大，所以將單一 `int` 以唯讀傳址方式傳遞並沒有好處。

## <a name="limitations-on-in-parameters"></a>`in` 參數的限制

您不可為下列幾種方法使用 `in`、`ref` 和 `out` 關鍵字：  
  
- 使用 [async](async.md) 修飾詞定義的 async 方法。  
- 迭代器方法，其包括 [yield return](yield.md) 或 `yield break` 陳述式。
- 擴充方法的第一個引數不能有 `in` 修飾詞，除非該引數是結構。
- 擴充方法的第一個引數，也就是該引數是泛型型別 (即使該型別限制為結構時也一樣 ) 

## <a name="c-language-specification"></a>C# 語言規格  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [方法參數](method-parameters.md)
- [撰寫安全有效率的程式碼](../../write-safe-efficient-code.md)

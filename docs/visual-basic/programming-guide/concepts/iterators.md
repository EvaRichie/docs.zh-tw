---
title: 迭代器
ms.date: 07/20/2015
ms.assetid: f26b5c1e-fe9d-4004-b287-da7919d717ae
ms.openlocfilehash: e638d35aeb86837d91fb14681d300772e3c2375a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410925"
---
# <a name="iterators-visual-basic"></a>迭代器 (Visual Basic)

「迭代器」** 可用來逐步執行集合，例如清單和陣列。

迭代器方法或 `get` 存取子會對集合執行自訂反覆運算。 Iterator 方法會使用[Yield](../../language-reference/statements/yield-statement.md)語句，一次傳回一個元素。 當到達 `Yield` 陳述式時，系統會記住程式碼中的目前位置。 下次呼叫迭代器函式時，便會從這個位置重新開始執行。

您會從用戶端程式代碼取用反覆運算器，方法是使用[For Each .。。下一個](../../language-reference/statements/for-each-next-statement.md)語句，或使用 LINQ 查詢。

在下列範例中，第一次反覆運算 `For Each` 迴圈會使 `SomeNumbers` 迭代器方法中的執行繼續，直到到達第一個 `Yield` 陳述式為止。 此反覆運算會傳回值 3，並保留迭代器方法中的目前位置。 下次反覆運算迴圈時，迭代器方法中的執行會從上次停止的位置繼續，並且在到達 `Yield` 陳述式時再次停止。 此反覆運算會傳回值 5，並再次保留迭代器方法中的目前位置。 當到達迭代器方法結尾時，迴圈便完成。

```vb
Sub Main()
    For Each number As Integer In SomeNumbers()
        Console.Write(number & " ")
    Next
    ' Output: 3 5 8
    Console.ReadKey()
End Sub

Private Iterator Function SomeNumbers() As System.Collections.IEnumerable
    Yield 3
    Yield 5
    Yield 8
End Function
```

迭代器方法或 `get` 存取子的傳回型別可以是 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601>。

您可以使用 `Exit Function` 或 `Return` 語句來結束反復專案。

Visual Basic 反覆運算器函數或 `get` 存取子宣告包含[iterator](../../language-reference/modifiers/iterator.md)修飾詞。

反覆運算器是在 Visual Studio 2012 的 Visual Basic 中引進。

**本主題中的**

- [簡易迭代器](#BKMK_SimpleIterator)

- [建立集合類別](#BKMK_CollectionClass)

- [Try 區塊](#BKMK_TryBlocks)

- [匿名方法](#BKMK_AnonymousMethods)

- [搭配泛型清單使用反覆運算器](#BKMK_GenericList)

- [語法資訊](#BKMK_SyntaxInformation)

- [技術執行](#BKMK_Technical)

- [反覆運算器的使用](#BKMK_UseOfIterators)

> [!NOTE]
> 針對主題中的所有範例（簡單反覆運算器範例除外） [Imports](../../language-reference/statements/imports-statement-net-namespace-and-type.md) ，包含 `System.Collections` 和命名空間的 Imports 語句 `System.Collections.Generic` 。

## <a name="simple-iterator"></a><a name="BKMK_SimpleIterator"></a>簡單反覆運算器

下列範例的單一 `Yield` 語句位於[For .。。下一個](../../language-reference/statements/for-next-statement.md)迴圈。 在 `Main` 中，每次反覆運算 `For Each` 陳述式主體都會建立迭代器函式的呼叫，以繼續進行下一個 `Yield` 陳述式。

```vb
Sub Main()
    For Each number As Integer In EvenSequence(5, 18)
        Console.Write(number & " ")
    Next
    ' Output: 6 8 10 12 14 16 18
    Console.ReadKey()
End Sub

Private Iterator Function EvenSequence(
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _
As System.Collections.Generic.IEnumerable(Of Integer)

    ' Yield even numbers in the range.
    For number As Integer = firstNumber To lastNumber
        If number Mod 2 = 0 Then
            Yield number
        End If
    Next
End Function
```

## <a name="creating-a-collection-class"></a><a name="BKMK_CollectionClass"></a> 建立集合類別

在以下範例中，`DaysOfTheWeek` 類別會實作 <xref:System.Collections.IEnumerable> 介面，而這個介面需使用 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。 編譯器會隱含呼叫 `GetEnumerator` 方法，以傳回 <xref:System.Collections.IEnumerator>。

`GetEnumerator`方法會使用語句，一次傳回一個字串 `Yield` ，而 `Iterator` 修飾詞則是在函式宣告中。

```vb
Sub Main()
    Dim days As New DaysOfTheWeek()
    For Each day As String In days
        Console.Write(day & " ")
    Next
    ' Output: Sun Mon Tue Wed Thu Fri Sat
    Console.ReadKey()
End Sub

Private Class DaysOfTheWeek
    Implements IEnumerable

    Public days =
        New String() {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"}

    Public Iterator Function GetEnumerator() As IEnumerator _
        Implements IEnumerable.GetEnumerator

        ' Yield each day of the week.
        For i As Integer = 0 To days.Length - 1
            Yield days(i)
        Next
    End Function
End Class
```

下列範例會建立 `Zoo` 類別，其中包含動物的集合。

參考類別執行個體 (`theZoo`) 的 `For Each` 陳述式會隱含呼叫 `GetEnumerator` 方法。 參考 `Birds` 和 `Mammals` 屬性的 `For Each` 陳述式會使用 `AnimalsForType` 具名迭代器方法。

```vb
Sub Main()
    Dim theZoo As New Zoo()

    theZoo.AddMammal("Whale")
    theZoo.AddMammal("Rhinoceros")
    theZoo.AddBird("Penguin")
    theZoo.AddBird("Warbler")

    For Each name As String In theZoo
        Console.Write(name & " ")
    Next
    Console.WriteLine()
    ' Output: Whale Rhinoceros Penguin Warbler

    For Each name As String In theZoo.Birds
        Console.Write(name & " ")
    Next
    Console.WriteLine()
    ' Output: Penguin Warbler

    For Each name As String In theZoo.Mammals
        Console.Write(name & " ")
    Next
    Console.WriteLine()
    ' Output: Whale Rhinoceros

    Console.ReadKey()
End Sub

Public Class Zoo
    Implements IEnumerable

    ' Private members.
    Private animals As New List(Of Animal)

    ' Public methods.
    Public Sub AddMammal(ByVal name As String)
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Mammal})
    End Sub

    Public Sub AddBird(ByVal name As String)
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Bird})
    End Sub

    Public Iterator Function GetEnumerator() As IEnumerator _
        Implements IEnumerable.GetEnumerator

        For Each theAnimal As Animal In animals
            Yield theAnimal.Name
        Next
    End Function

    ' Public members.
    Public ReadOnly Property Mammals As IEnumerable
        Get
            Return AnimalsForType(Animal.TypeEnum.Mammal)
        End Get
    End Property

    Public ReadOnly Property Birds As IEnumerable
        Get
            Return AnimalsForType(Animal.TypeEnum.Bird)
        End Get
    End Property

    ' Private methods.
    Private Iterator Function AnimalsForType( _
    ByVal type As Animal.TypeEnum) As IEnumerable
        For Each theAnimal As Animal In animals
            If (theAnimal.Type = type) Then
                Yield theAnimal.Name
            End If
        Next
    End Function

    ' Private class.
    Private Class Animal
        Public Enum TypeEnum
            Bird
            Mammal
        End Enum

        Public Property Name As String
        Public Property Type As TypeEnum
    End Class
End Class
```

## <a name="try-blocks"></a><a name="BKMK_TryBlocks"></a>Try 區塊

Visual Basic 允許在 `Yield` Try 的區塊中使用語句 ... `Try` [Catch .。。Finally 語句](../../language-reference/statements/try-catch-finally-statement.md)。 `Try`具有語句的區塊 `Yield` 可以有 `Catch` 區塊，而且可以有 `Finally` 區塊。

下列範例會 `Try` `Catch` `Finally` 在 iterator 函式中包含、和區塊。 `Finally`Iterator 函數中的區塊會在反復專案 `For Each` 完成之前執行。

```vb
Sub Main()
    For Each number As Integer In Test()
        Console.WriteLine(number)
    Next
    Console.WriteLine("For Each is done.")

    ' Output:
    '  3
    '  4
    '  Something happened. Yields are done.
    '  Finally is called.
    '  For Each is done.
    Console.ReadKey()
End Sub

Private Iterator Function Test() As IEnumerable(Of Integer)
    Try
        Yield 3
        Yield 4
        Throw New Exception("Something happened. Yields are done.")
        Yield 5
        Yield 6
    Catch ex As Exception
        Console.WriteLine(ex.Message)
    Finally
        Console.WriteLine("Finally is called.")
    End Try
End Function
```

`Yield`語句不能在 `Catch` 區塊或 `Finally` 區塊內。

如果 `For Each` 主體（而不是 iterator 方法）擲回例外狀況，則 `Catch` 不會執行 iterator 函式中的區塊，但 `Finally` 會執行 iterator 函數中的區塊。 `Catch`Iterator 函式內的區塊只會攔截反覆運算器函數內所發生的例外狀況。

## <a name="anonymous-methods"></a><a name="BKMK_AnonymousMethods"></a>匿名方法

在 Visual Basic 中，匿名函式可以是反覆運算器函數。 下列範例將說明這點。

```vb
Dim iterateSequence = Iterator Function() _
                      As IEnumerable(Of Integer)
                          Yield 1
                          Yield 2
                      End Function

For Each number As Integer In iterateSequence()
    Console.Write(number & " ")
Next
' Output: 1 2
Console.ReadKey()
```

下列範例具有可驗證引數的非反覆運算器方法。 方法會傳回匿名反覆運算器的結果，以描述集合元素。

```vb
Sub Main()
    For Each number As Integer In GetSequence(5, 10)
        Console.Write(number & " ")
    Next
    ' Output: 5 6 7 8 9 10
    Console.ReadKey()
End Sub

Public Function GetSequence(ByVal low As Integer, ByVal high As Integer) _
As IEnumerable
    ' Validate the arguments.
    If low < 1 Then
        Throw New ArgumentException("low is too low")
    End If
    If high > 140 Then
        Throw New ArgumentException("high is too high")
    End If

    ' Return an anonymous iterator function.
    Dim iterateSequence = Iterator Function() As IEnumerable
                              For index = low To high
                                  Yield index
                              Next
                          End Function
    Return iterateSequence()
End Function
```

如果驗證是在 iterator 函式內，就無法執行驗證，直到主體的第一個反復專案開始為止 `For Each` 。

## <a name="using-iterators-with-a-generic-list"></a><a name="BKMK_GenericList"></a> 搭配泛型清單使用迭代器

在以下範例中，`Stack(Of T)` 泛型類別會實作 <xref:System.Collections.Generic.IEnumerable%601> 泛型介面。 `Push` 方法會將值指派給 `T` 類型的陣列。 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法會使用 `Yield` 陳述式以傳回陣列值。

除了泛型 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法，您也必須實作非泛型 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。 這是因為 <xref:System.Collections.Generic.IEnumerable%601> 繼承自 <xref:System.Collections.IEnumerable>。 非泛型實作會延後到泛型實作。

此範例使用具名迭代器來支援逐一查看相同資料集合的各種方法。 這些具名迭代器是 `TopToBottom` 和 `BottomToTop` 屬性，以及 `TopN` 方法。

`BottomToTop`屬性宣告包含 `Iterator` 關鍵字。

```vb
Sub Main()
    Dim theStack As New Stack(Of Integer)

    ' Add items to the stack.
    For number As Integer = 0 To 9
        theStack.Push(number)
    Next

    ' Retrieve items from the stack.
    ' For Each is allowed because theStack implements
    ' IEnumerable(Of Integer).
    For Each number As Integer In theStack
        Console.Write("{0} ", number)
    Next
    Console.WriteLine()
    ' Output: 9 8 7 6 5 4 3 2 1 0

    ' For Each is allowed, because theStack.TopToBottom
    ' returns IEnumerable(Of Integer).
    For Each number As Integer In theStack.TopToBottom
        Console.Write("{0} ", number)
    Next
    Console.WriteLine()
    ' Output: 9 8 7 6 5 4 3 2 1 0

    For Each number As Integer In theStack.BottomToTop
        Console.Write("{0} ", number)
    Next
    Console.WriteLine()
    ' Output: 0 1 2 3 4 5 6 7 8 9

    For Each number As Integer In theStack.TopN(7)
        Console.Write("{0} ", number)
    Next
    Console.WriteLine()
    ' Output: 9 8 7 6 5 4 3

    Console.ReadKey()
End Sub

Public Class Stack(Of T)
    Implements IEnumerable(Of T)

    Private values As T() = New T(99) {}
    Private top As Integer = 0

    Public Sub Push(ByVal t As T)
        values(top) = t
        top = top + 1
    End Sub

    Public Function Pop() As T
        top = top - 1
        Return values(top)
    End Function

    ' This function implements the GetEnumerator method. It allows
    ' an instance of the class to be used in a For Each statement.
    Public Iterator Function GetEnumerator() As IEnumerator(Of T) _
        Implements IEnumerable(Of T).GetEnumerator

        For index As Integer = top - 1 To 0 Step -1
            Yield values(index)
        Next
    End Function

    Public Iterator Function GetEnumerator1() As IEnumerator _
        Implements IEnumerable.GetEnumerator

        Yield GetEnumerator()
    End Function

    Public ReadOnly Property TopToBottom() As IEnumerable(Of T)
        Get
            Return Me
        End Get
    End Property

    Public ReadOnly Iterator Property BottomToTop As IEnumerable(Of T)
        Get
            For index As Integer = 0 To top - 1
                Yield values(index)
            Next
        End Get
    End Property

    Public Iterator Function TopN(ByVal itemsFromTop As Integer) _
        As IEnumerable(Of T)

        ' Return less than itemsFromTop if necessary.
        Dim startIndex As Integer =
            If(itemsFromTop >= top, 0, top - itemsFromTop)

        For index As Integer = top - 1 To startIndex Step -1
            Yield values(index)
        Next
    End Function
End Class
```

## <a name="syntax-information"></a><a name="BKMK_SyntaxInformation"></a>語法資訊

出現的迭代器可以是方法或 `get` 存取子。 迭代器不能出現在事件、執行個體建構函式、靜態建構函式或靜態解構函式中。

`Yield` 陳述式中的運算式類型必須隱含轉換成迭代器的傳回型別。

在 Visual Basic 中，iterator 方法不能有任何 `ByRef` 參數。

在 Visual Basic 中，"Yield" 不是保留字，只有在方法或存取子中使用時才具有特殊意義 `Iterator` `get` 。

## <a name="technical-implementation"></a><a name="BKMK_Technical"></a>技術執行

雖然您將迭代器撰寫成方法，但編譯器會將其轉譯成巢狀類別，其實也就是狀態機器。 此類別會在用戶端程式碼中的 `For Each...Next` 迴圈繼續期間追蹤迭代器的位置。

若要查看編譯器的功能，您可以使用 Ildasm.exe 工具來檢視為迭代器方法產生的 Microsoft 中繼語言程式碼。

當您建立[類別](../../language-reference/statements/class-statement.md)或[結構](../../language-reference/statements/structure-statement.md)的反覆運算器時，您不需要執行整個 <xref:System.Collections.IEnumerator> 介面。 當編譯器偵測到迭代器時，它會自動產生 <xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601> 介面的 `Current`、`MoveNext` 和 `Dispose` 方法。

之後每次反覆運算 `For Each…Next` 迴圈 (或直接呼叫 `IEnumerator.MoveNext`)，下一個迭代器程式碼主體都會在上一個 `Yield` 陳述式之後繼續。 接著，它會繼續進行下一個 `Yield` 語句，直到到達反覆運算器主體的結尾，或 `Exit Function` 遇到或 `Return` 語句為止。

反覆運算器不支援 <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> 方法。 若要從頭開始逐一查看，您必須取得新的迭代器。

如需詳細資訊，請參閱[Visual Basic 語言規格](../../reference/language-specification/index.md)。

## <a name="use-of-iterators"></a><a name="BKMK_UseOfIterators"></a> 迭代器的使用

當您需要使用複雜的程式碼來填入清單序列時，迭代器可讓您維持 `For Each` 迴圈的簡潔性。 當您想要執行下列作業時，這會很有用：

- 在第一次反覆運算 `For Each` 迴圈之後修改清單序列。

- 避免在第一次反覆運算 `For Each` 迴圈之前完整載入大型清單。 分頁擷取以分批載入資料表資料列即為一例。 另一個範例是 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 方法，它會在 .NET Framework 中實作迭代器。

- 在迭代器中封裝建立清單。 在迭代器方法中，您可以建立清單，然後在迴圈中產生每個結果。

## <a name="see-also"></a>另請參閱

- <xref:System.Collections.Generic>
- <xref:System.Collections.Generic.IEnumerable%601>
- [For Each...Next 陳述式](../../language-reference/statements/for-each-next-statement.md)
- [Yield 陳述式](../../language-reference/statements/yield-statement.md)
- [Iterator](../../language-reference/modifiers/iterator.md)

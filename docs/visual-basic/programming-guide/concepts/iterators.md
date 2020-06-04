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
# <a name="iterators-visual-basic"></a><span data-ttu-id="70ff5-102">迭代器 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="70ff5-102">Iterators (Visual Basic)</span></span>

<span data-ttu-id="70ff5-103">「迭代器」\*\* 可用來逐步執行集合，例如清單和陣列。</span><span class="sxs-lookup"><span data-stu-id="70ff5-103">An *iterator* can be used to step through collections such as lists and arrays.</span></span>

<span data-ttu-id="70ff5-104">迭代器方法或 `get` 存取子會對集合執行自訂反覆運算。</span><span class="sxs-lookup"><span data-stu-id="70ff5-104">An iterator method or `get` accessor performs a custom iteration over a collection.</span></span> <span data-ttu-id="70ff5-105">Iterator 方法會使用[Yield](../../language-reference/statements/yield-statement.md)語句，一次傳回一個元素。</span><span class="sxs-lookup"><span data-stu-id="70ff5-105">An iterator method uses the [Yield](../../language-reference/statements/yield-statement.md) statement to return each element one at a time.</span></span> <span data-ttu-id="70ff5-106">當到達 `Yield` 陳述式時，系統會記住程式碼中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="70ff5-106">When a `Yield` statement is reached, the current location in code is remembered.</span></span> <span data-ttu-id="70ff5-107">下次呼叫迭代器函式時，便會從這個位置重新開始執行。</span><span class="sxs-lookup"><span data-stu-id="70ff5-107">Execution is restarted from that location the next time the iterator function is called.</span></span>

<span data-ttu-id="70ff5-108">您會從用戶端程式代碼取用反覆運算器，方法是使用[For Each .。。下一個](../../language-reference/statements/for-each-next-statement.md)語句，或使用 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="70ff5-108">You consume an iterator from client code by using a [For Each…Next](../../language-reference/statements/for-each-next-statement.md) statement, or by using a LINQ query.</span></span>

<span data-ttu-id="70ff5-109">在下列範例中，第一次反覆運算 `For Each` 迴圈會使 `SomeNumbers` 迭代器方法中的執行繼續，直到到達第一個 `Yield` 陳述式為止。</span><span class="sxs-lookup"><span data-stu-id="70ff5-109">In the following example, the first iteration of the `For Each` loop causes execution to proceed  in the `SomeNumbers` iterator method until the first `Yield` statement is reached.</span></span> <span data-ttu-id="70ff5-110">此反覆運算會傳回值 3，並保留迭代器方法中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="70ff5-110">This iteration returns a value of 3, and the current location in the iterator method is retained.</span></span> <span data-ttu-id="70ff5-111">下次反覆運算迴圈時，迭代器方法中的執行會從上次停止的位置繼續，並且在到達 `Yield` 陳述式時再次停止。</span><span class="sxs-lookup"><span data-stu-id="70ff5-111">On the next iteration of the loop, execution in the iterator method continues from where it left off, again stopping when it reaches a `Yield` statement.</span></span> <span data-ttu-id="70ff5-112">此反覆運算會傳回值 5，並再次保留迭代器方法中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="70ff5-112">This iteration returns a value of 5, and the current location in the iterator method is again retained.</span></span> <span data-ttu-id="70ff5-113">當到達迭代器方法結尾時，迴圈便完成。</span><span class="sxs-lookup"><span data-stu-id="70ff5-113">The loop completes when the end of the iterator method is reached.</span></span>

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

<span data-ttu-id="70ff5-114">迭代器方法或 `get` 存取子的傳回型別可以是 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601>。</span><span class="sxs-lookup"><span data-stu-id="70ff5-114">The return type of an iterator method or `get` accessor can be <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, or <xref:System.Collections.Generic.IEnumerator%601>.</span></span>

<span data-ttu-id="70ff5-115">您可以使用 `Exit Function` 或 `Return` 語句來結束反復專案。</span><span class="sxs-lookup"><span data-stu-id="70ff5-115">You can use an `Exit Function` or `Return` statement to end the iteration.</span></span>

<span data-ttu-id="70ff5-116">Visual Basic 反覆運算器函數或 `get` 存取子宣告包含[iterator](../../language-reference/modifiers/iterator.md)修飾詞。</span><span class="sxs-lookup"><span data-stu-id="70ff5-116">A Visual Basic iterator function or `get` accessor declaration includes an [Iterator](../../language-reference/modifiers/iterator.md) modifier.</span></span>

<span data-ttu-id="70ff5-117">反覆運算器是在 Visual Studio 2012 的 Visual Basic 中引進。</span><span class="sxs-lookup"><span data-stu-id="70ff5-117">Iterators were introduced in Visual Basic in Visual Studio 2012.</span></span>

<span data-ttu-id="70ff5-118">**本主題中的**</span><span class="sxs-lookup"><span data-stu-id="70ff5-118">**In this topic**</span></span>

- [<span data-ttu-id="70ff5-119">簡易迭代器</span><span class="sxs-lookup"><span data-stu-id="70ff5-119">Simple Iterator</span></span>](#BKMK_SimpleIterator)

- [<span data-ttu-id="70ff5-120">建立集合類別</span><span class="sxs-lookup"><span data-stu-id="70ff5-120">Creating a Collection Class</span></span>](#BKMK_CollectionClass)

- [<span data-ttu-id="70ff5-121">Try 區塊</span><span class="sxs-lookup"><span data-stu-id="70ff5-121">Try Blocks</span></span>](#BKMK_TryBlocks)

- [<span data-ttu-id="70ff5-122">匿名方法</span><span class="sxs-lookup"><span data-stu-id="70ff5-122">Anonymous Methods</span></span>](#BKMK_AnonymousMethods)

- [<span data-ttu-id="70ff5-123">搭配泛型清單使用反覆運算器</span><span class="sxs-lookup"><span data-stu-id="70ff5-123">Using Iterators with a Generic List</span></span>](#BKMK_GenericList)

- [<span data-ttu-id="70ff5-124">語法資訊</span><span class="sxs-lookup"><span data-stu-id="70ff5-124">Syntax Information</span></span>](#BKMK_SyntaxInformation)

- [<span data-ttu-id="70ff5-125">技術執行</span><span class="sxs-lookup"><span data-stu-id="70ff5-125">Technical Implementation</span></span>](#BKMK_Technical)

- [<span data-ttu-id="70ff5-126">反覆運算器的使用</span><span class="sxs-lookup"><span data-stu-id="70ff5-126">Use of Iterators</span></span>](#BKMK_UseOfIterators)

> [!NOTE]
> <span data-ttu-id="70ff5-127">針對主題中的所有範例（簡單反覆運算器範例除外） [Imports](../../language-reference/statements/imports-statement-net-namespace-and-type.md) ，包含 `System.Collections` 和命名空間的 Imports 語句 `System.Collections.Generic` 。</span><span class="sxs-lookup"><span data-stu-id="70ff5-127">For all examples in the topic except the Simple Iterator example, include [Imports](../../language-reference/statements/imports-statement-net-namespace-and-type.md) statements for the `System.Collections` and `System.Collections.Generic` namespaces.</span></span>

## <a name="simple-iterator"></a><a name="BKMK_SimpleIterator"></a><span data-ttu-id="70ff5-128">簡單反覆運算器</span><span class="sxs-lookup"><span data-stu-id="70ff5-128">Simple Iterator</span></span>

<span data-ttu-id="70ff5-129">下列範例的單一 `Yield` 語句位於[For .。。下一個](../../language-reference/statements/for-next-statement.md)迴圈。</span><span class="sxs-lookup"><span data-stu-id="70ff5-129">The following example has a single `Yield` statement that is inside a [For…Next](../../language-reference/statements/for-next-statement.md) loop.</span></span> <span data-ttu-id="70ff5-130">在 `Main` 中，每次反覆運算 `For Each` 陳述式主體都會建立迭代器函式的呼叫，以繼續進行下一個 `Yield` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="70ff5-130">In `Main`, each iteration of the `For Each` statement body creates a call to the iterator function, which proceeds to the next `Yield` statement.</span></span>

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

## <a name="creating-a-collection-class"></a><a name="BKMK_CollectionClass"></a> <span data-ttu-id="70ff5-131">建立集合類別</span><span class="sxs-lookup"><span data-stu-id="70ff5-131">Creating a Collection Class</span></span>

<span data-ttu-id="70ff5-132">在以下範例中，`DaysOfTheWeek` 類別會實作 <xref:System.Collections.IEnumerable> 介面，而這個介面需使用 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-132">In the following example, the `DaysOfTheWeek` class implements the <xref:System.Collections.IEnumerable> interface, which requires a <xref:System.Collections.IEnumerable.GetEnumerator%2A> method.</span></span> <span data-ttu-id="70ff5-133">編譯器會隱含呼叫 `GetEnumerator` 方法，以傳回 <xref:System.Collections.IEnumerator>。</span><span class="sxs-lookup"><span data-stu-id="70ff5-133">The compiler implicitly calls the `GetEnumerator` method, which returns an <xref:System.Collections.IEnumerator>.</span></span>

<span data-ttu-id="70ff5-134">`GetEnumerator`方法會使用語句，一次傳回一個字串 `Yield` ，而 `Iterator` 修飾詞則是在函式宣告中。</span><span class="sxs-lookup"><span data-stu-id="70ff5-134">The `GetEnumerator` method returns each string one at a time by using the `Yield` statement, and  an `Iterator` modifier is in the function declaration.</span></span>

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

<span data-ttu-id="70ff5-135">下列範例會建立 `Zoo` 類別，其中包含動物的集合。</span><span class="sxs-lookup"><span data-stu-id="70ff5-135">The following example creates a `Zoo` class that contains a collection of animals.</span></span>

<span data-ttu-id="70ff5-136">參考類別執行個體 (`theZoo`) 的 `For Each` 陳述式會隱含呼叫 `GetEnumerator` 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-136">The `For Each` statement that refers to the class instance (`theZoo`) implicitly calls the `GetEnumerator` method.</span></span> <span data-ttu-id="70ff5-137">參考 `Birds` 和 `Mammals` 屬性的 `For Each` 陳述式會使用 `AnimalsForType` 具名迭代器方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-137">The `For Each` statements that refer to the `Birds` and `Mammals` properties use the `AnimalsForType` named iterator method.</span></span>

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

## <a name="try-blocks"></a><a name="BKMK_TryBlocks"></a><span data-ttu-id="70ff5-138">Try 區塊</span><span class="sxs-lookup"><span data-stu-id="70ff5-138">Try Blocks</span></span>

<span data-ttu-id="70ff5-139">Visual Basic 允許在 `Yield` Try 的區塊中使用語句 ... `Try` [Catch .。。Finally 語句](../../language-reference/statements/try-catch-finally-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="70ff5-139">Visual Basic allows a `Yield` statement in the `Try` block of a [Try...Catch...Finally Statement](../../language-reference/statements/try-catch-finally-statement.md).</span></span> <span data-ttu-id="70ff5-140">`Try`具有語句的區塊 `Yield` 可以有 `Catch` 區塊，而且可以有 `Finally` 區塊。</span><span class="sxs-lookup"><span data-stu-id="70ff5-140">A `Try` block that has a `Yield` statement can have `Catch` blocks, and can have a `Finally` block.</span></span>

<span data-ttu-id="70ff5-141">下列範例會 `Try` `Catch` `Finally` 在 iterator 函式中包含、和區塊。</span><span class="sxs-lookup"><span data-stu-id="70ff5-141">The following example includes `Try`, `Catch`, and `Finally` blocks in an iterator function.</span></span> <span data-ttu-id="70ff5-142">`Finally`Iterator 函數中的區塊會在反復專案 `For Each` 完成之前執行。</span><span class="sxs-lookup"><span data-stu-id="70ff5-142">The `Finally` block in the iterator function executes before the `For Each` iteration finishes.</span></span>

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

<span data-ttu-id="70ff5-143">`Yield`語句不能在 `Catch` 區塊或 `Finally` 區塊內。</span><span class="sxs-lookup"><span data-stu-id="70ff5-143">A `Yield` statement cannot be inside a `Catch` block or a `Finally` block.</span></span>

<span data-ttu-id="70ff5-144">如果 `For Each` 主體（而不是 iterator 方法）擲回例外狀況，則 `Catch` 不會執行 iterator 函式中的區塊，但 `Finally` 會執行 iterator 函數中的區塊。</span><span class="sxs-lookup"><span data-stu-id="70ff5-144">If the `For Each` body (instead of the iterator method) throws an exception, a `Catch` block in the iterator function is not executed, but a `Finally` block in the iterator function is executed.</span></span> <span data-ttu-id="70ff5-145">`Catch`Iterator 函式內的區塊只會攔截反覆運算器函數內所發生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="70ff5-145">A `Catch` block inside an iterator function catches only exceptions that occur inside the iterator function.</span></span>

## <a name="anonymous-methods"></a><a name="BKMK_AnonymousMethods"></a><span data-ttu-id="70ff5-146">匿名方法</span><span class="sxs-lookup"><span data-stu-id="70ff5-146">Anonymous Methods</span></span>

<span data-ttu-id="70ff5-147">在 Visual Basic 中，匿名函式可以是反覆運算器函數。</span><span class="sxs-lookup"><span data-stu-id="70ff5-147">In Visual Basic, an anonymous function can be an iterator function.</span></span> <span data-ttu-id="70ff5-148">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="70ff5-148">The following example illustrates this.</span></span>

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

<span data-ttu-id="70ff5-149">下列範例具有可驗證引數的非反覆運算器方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-149">The following example has a non-iterator method that validates the arguments.</span></span> <span data-ttu-id="70ff5-150">方法會傳回匿名反覆運算器的結果，以描述集合元素。</span><span class="sxs-lookup"><span data-stu-id="70ff5-150">The method returns the result of an anonymous iterator that describes the collection elements.</span></span>

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

<span data-ttu-id="70ff5-151">如果驗證是在 iterator 函式內，就無法執行驗證，直到主體的第一個反復專案開始為止 `For Each` 。</span><span class="sxs-lookup"><span data-stu-id="70ff5-151">If validation is instead inside the iterator function, the validation cannot be performed until the start of the first iteration of the `For Each` body.</span></span>

## <a name="using-iterators-with-a-generic-list"></a><a name="BKMK_GenericList"></a> <span data-ttu-id="70ff5-152">搭配泛型清單使用迭代器</span><span class="sxs-lookup"><span data-stu-id="70ff5-152">Using Iterators with a Generic List</span></span>

<span data-ttu-id="70ff5-153">在以下範例中，`Stack(Of T)` 泛型類別會實作 <xref:System.Collections.Generic.IEnumerable%601> 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="70ff5-153">In the following example, the `Stack(Of T)` generic class implements the <xref:System.Collections.Generic.IEnumerable%601> generic interface.</span></span> <span data-ttu-id="70ff5-154">`Push` 方法會將值指派給 `T` 類型的陣列。</span><span class="sxs-lookup"><span data-stu-id="70ff5-154">The `Push` method assigns values to an array of type `T`.</span></span> <span data-ttu-id="70ff5-155"><xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法會使用 `Yield` 陳述式以傳回陣列值。</span><span class="sxs-lookup"><span data-stu-id="70ff5-155">The <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> method returns the array values by using the `Yield` statement.</span></span>

<span data-ttu-id="70ff5-156">除了泛型 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法，您也必須實作非泛型 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-156">In addition to the generic <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> method, the non-generic <xref:System.Collections.IEnumerable.GetEnumerator%2A> method must also be implemented.</span></span> <span data-ttu-id="70ff5-157">這是因為 <xref:System.Collections.Generic.IEnumerable%601> 繼承自 <xref:System.Collections.IEnumerable>。</span><span class="sxs-lookup"><span data-stu-id="70ff5-157">This is because <xref:System.Collections.Generic.IEnumerable%601> inherits from <xref:System.Collections.IEnumerable>.</span></span> <span data-ttu-id="70ff5-158">非泛型實作會延後到泛型實作。</span><span class="sxs-lookup"><span data-stu-id="70ff5-158">The non-generic implementation defers to the generic implementation.</span></span>

<span data-ttu-id="70ff5-159">此範例使用具名迭代器來支援逐一查看相同資料集合的各種方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-159">The example uses named iterators to support various ways of iterating through the same collection of data.</span></span> <span data-ttu-id="70ff5-160">這些具名迭代器是 `TopToBottom` 和 `BottomToTop` 屬性，以及 `TopN` 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-160">These named iterators are the `TopToBottom` and `BottomToTop` properties, and the `TopN` method.</span></span>

<span data-ttu-id="70ff5-161">`BottomToTop`屬性宣告包含 `Iterator` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="70ff5-161">The `BottomToTop` property declaration includes the `Iterator` keyword.</span></span>

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

## <a name="syntax-information"></a><a name="BKMK_SyntaxInformation"></a><span data-ttu-id="70ff5-162">語法資訊</span><span class="sxs-lookup"><span data-stu-id="70ff5-162">Syntax Information</span></span>

<span data-ttu-id="70ff5-163">出現的迭代器可以是方法或 `get` 存取子。</span><span class="sxs-lookup"><span data-stu-id="70ff5-163">An iterator can occur as a method or `get` accessor.</span></span> <span data-ttu-id="70ff5-164">迭代器不能出現在事件、執行個體建構函式、靜態建構函式或靜態解構函式中。</span><span class="sxs-lookup"><span data-stu-id="70ff5-164">An iterator cannot occur in an event, instance constructor, static constructor, or static destructor.</span></span>

<span data-ttu-id="70ff5-165">`Yield` 陳述式中的運算式類型必須隱含轉換成迭代器的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="70ff5-165">An implicit conversion must exist from the expression type in the `Yield` statement to the return type of the iterator.</span></span>

<span data-ttu-id="70ff5-166">在 Visual Basic 中，iterator 方法不能有任何 `ByRef` 參數。</span><span class="sxs-lookup"><span data-stu-id="70ff5-166">In Visual Basic, an iterator method cannot have any `ByRef` parameters.</span></span>

<span data-ttu-id="70ff5-167">在 Visual Basic 中，"Yield" 不是保留字，只有在方法或存取子中使用時才具有特殊意義 `Iterator` `get` 。</span><span class="sxs-lookup"><span data-stu-id="70ff5-167">In Visual Basic, "Yield" is not a reserved word and has special meaning only when it is used in an `Iterator` method or `get` accessor.</span></span>

## <a name="technical-implementation"></a><a name="BKMK_Technical"></a><span data-ttu-id="70ff5-168">技術執行</span><span class="sxs-lookup"><span data-stu-id="70ff5-168">Technical Implementation</span></span>

<span data-ttu-id="70ff5-169">雖然您將迭代器撰寫成方法，但編譯器會將其轉譯成巢狀類別，其實也就是狀態機器。</span><span class="sxs-lookup"><span data-stu-id="70ff5-169">Although you write an iterator as a method, the compiler translates it into a nested class that is, in effect, a state machine.</span></span> <span data-ttu-id="70ff5-170">此類別會在用戶端程式碼中的 `For Each...Next` 迴圈繼續期間追蹤迭代器的位置。</span><span class="sxs-lookup"><span data-stu-id="70ff5-170">This class keeps track of the position of the iterator as long the `For Each...Next` loop in the client code continues.</span></span>

<span data-ttu-id="70ff5-171">若要查看編譯器的功能，您可以使用 Ildasm.exe 工具來檢視為迭代器方法產生的 Microsoft 中繼語言程式碼。</span><span class="sxs-lookup"><span data-stu-id="70ff5-171">To see what the compiler does, you can use the Ildasm.exe tool to view the Microsoft intermediate language code that is generated for an iterator method.</span></span>

<span data-ttu-id="70ff5-172">當您建立[類別](../../language-reference/statements/class-statement.md)或[結構](../../language-reference/statements/structure-statement.md)的反覆運算器時，您不需要執行整個 <xref:System.Collections.IEnumerator> 介面。</span><span class="sxs-lookup"><span data-stu-id="70ff5-172">When you create an iterator for a [class](../../language-reference/statements/class-statement.md) or [struct](../../language-reference/statements/structure-statement.md), you do not have to implement the whole <xref:System.Collections.IEnumerator> interface.</span></span> <span data-ttu-id="70ff5-173">當編譯器偵測到迭代器時，它會自動產生 <xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601> 介面的 `Current`、`MoveNext` 和 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-173">When the compiler detects the iterator, it automatically generates the `Current`, `MoveNext`, and `Dispose` methods of the <xref:System.Collections.IEnumerator> or <xref:System.Collections.Generic.IEnumerator%601> interface.</span></span>

<span data-ttu-id="70ff5-174">之後每次反覆運算 `For Each…Next` 迴圈 (或直接呼叫 `IEnumerator.MoveNext`)，下一個迭代器程式碼主體都會在上一個 `Yield` 陳述式之後繼續。</span><span class="sxs-lookup"><span data-stu-id="70ff5-174">On each successive iteration of the `For Each…Next` loop (or the direct call to `IEnumerator.MoveNext`), the next iterator code body resumes after the previous `Yield` statement.</span></span> <span data-ttu-id="70ff5-175">接著，它會繼續進行下一個 `Yield` 語句，直到到達反覆運算器主體的結尾，或 `Exit Function` 遇到或 `Return` 語句為止。</span><span class="sxs-lookup"><span data-stu-id="70ff5-175">It then continues to the next `Yield` statement until the end of the iterator body is reached, or until an `Exit Function` or `Return` statement is encountered.</span></span>

<span data-ttu-id="70ff5-176">反覆運算器不支援 <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="70ff5-176">Iterators do not support the <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="70ff5-177">若要從頭開始逐一查看，您必須取得新的迭代器。</span><span class="sxs-lookup"><span data-stu-id="70ff5-177">To re-iterate from the start, you must obtain a new iterator.</span></span>

<span data-ttu-id="70ff5-178">如需詳細資訊，請參閱[Visual Basic 語言規格](../../reference/language-specification/index.md)。</span><span class="sxs-lookup"><span data-stu-id="70ff5-178">For additional information, see the [Visual Basic Language Specification](../../reference/language-specification/index.md).</span></span>

## <a name="use-of-iterators"></a><a name="BKMK_UseOfIterators"></a> <span data-ttu-id="70ff5-179">迭代器的使用</span><span class="sxs-lookup"><span data-stu-id="70ff5-179">Use of Iterators</span></span>

<span data-ttu-id="70ff5-180">當您需要使用複雜的程式碼來填入清單序列時，迭代器可讓您維持 `For Each` 迴圈的簡潔性。</span><span class="sxs-lookup"><span data-stu-id="70ff5-180">Iterators enable you to maintain the simplicity of a `For Each` loop when you need to use complex code to populate a list sequence.</span></span> <span data-ttu-id="70ff5-181">當您想要執行下列作業時，這會很有用：</span><span class="sxs-lookup"><span data-stu-id="70ff5-181">This can be useful when you want to do the following:</span></span>

- <span data-ttu-id="70ff5-182">在第一次反覆運算 `For Each` 迴圈之後修改清單序列。</span><span class="sxs-lookup"><span data-stu-id="70ff5-182">Modify the list sequence after the first `For Each` loop iteration.</span></span>

- <span data-ttu-id="70ff5-183">避免在第一次反覆運算 `For Each` 迴圈之前完整載入大型清單。</span><span class="sxs-lookup"><span data-stu-id="70ff5-183">Avoid fully loading a large list before the first iteration of a `For Each` loop.</span></span> <span data-ttu-id="70ff5-184">分頁擷取以分批載入資料表資料列即為一例。</span><span class="sxs-lookup"><span data-stu-id="70ff5-184">An example is a paged fetch to load a batch of table rows.</span></span> <span data-ttu-id="70ff5-185">另一個範例是 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 方法，它會在 .NET Framework 中實作迭代器。</span><span class="sxs-lookup"><span data-stu-id="70ff5-185">Another example is the <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> method, which implements iterators within the .NET Framework.</span></span>

- <span data-ttu-id="70ff5-186">在迭代器中封裝建立清單。</span><span class="sxs-lookup"><span data-stu-id="70ff5-186">Encapsulate building the list in the iterator.</span></span> <span data-ttu-id="70ff5-187">在迭代器方法中，您可以建立清單，然後在迴圈中產生每個結果。</span><span class="sxs-lookup"><span data-stu-id="70ff5-187">In the iterator method, you can build the list and then yield each result in a loop.</span></span>

## <a name="see-also"></a><span data-ttu-id="70ff5-188">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70ff5-188">See also</span></span>

- <xref:System.Collections.Generic>
- <xref:System.Collections.Generic.IEnumerable%601>
- [<span data-ttu-id="70ff5-189">For Each...Next 陳述式</span><span class="sxs-lookup"><span data-stu-id="70ff5-189">For Each...Next Statement</span></span>](../../language-reference/statements/for-each-next-statement.md)
- [<span data-ttu-id="70ff5-190">Yield 陳述式</span><span class="sxs-lookup"><span data-stu-id="70ff5-190">Yield Statement</span></span>](../../language-reference/statements/yield-statement.md)
- [<span data-ttu-id="70ff5-191">Iterator</span><span class="sxs-lookup"><span data-stu-id="70ff5-191">Iterator</span></span>](../../language-reference/modifiers/iterator.md)

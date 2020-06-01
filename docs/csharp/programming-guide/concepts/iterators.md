---
title: 在 C# 中逐一查看集合
ms.date: 08/14/2018
ms.assetid: c93f6dd4-e72a-4a06-be1c-a98b3255b734
ms.openlocfilehash: 15b77fd11c0ff606119425ec7aae8e7127315e82
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84240690"
---
# <a name="iterators-c"></a><span data-ttu-id="b7058-102">迭代器 (C#)</span><span class="sxs-lookup"><span data-stu-id="b7058-102">Iterators (C#)</span></span>

<span data-ttu-id="b7058-103">「迭代器」\*\* 可用來逐步執行集合，例如清單和陣列。</span><span class="sxs-lookup"><span data-stu-id="b7058-103">An *iterator* can be used to step through collections such as lists and arrays.</span></span>

<span data-ttu-id="b7058-104">迭代器方法或 `get` 存取子會對集合執行自訂反覆運算。</span><span class="sxs-lookup"><span data-stu-id="b7058-104">An iterator method or `get` accessor performs a custom iteration over a collection.</span></span> <span data-ttu-id="b7058-105">迭代器方法使用 [yield return](../../language-reference/keywords/yield.md) 陳述式，一次傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="b7058-105">An iterator method uses the [yield return](../../language-reference/keywords/yield.md) statement to return each element one at a time.</span></span> <span data-ttu-id="b7058-106">當到達 `yield return` 陳述式時，系統會記住程式碼中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="b7058-106">When a `yield return` statement is reached, the current location in code is remembered.</span></span> <span data-ttu-id="b7058-107">下次呼叫迭代器函式時，便會從這個位置重新開始執行。</span><span class="sxs-lookup"><span data-stu-id="b7058-107">Execution is restarted from that location the next time the iterator function is called.</span></span>

<span data-ttu-id="b7058-108">您會使用 [foreach](../../language-reference/keywords/foreach-in.md) 陳述式或使用 LINQ 查詢，透過用戶端程式碼取用迭代器。</span><span class="sxs-lookup"><span data-stu-id="b7058-108">You consume an iterator from client code by using a [foreach](../../language-reference/keywords/foreach-in.md) statement or by using a LINQ query.</span></span>

<span data-ttu-id="b7058-109">在下列範例中，第一次反覆運算 `foreach` 迴圈會使 `SomeNumbers` 迭代器方法中的執行繼續，直到到達第一個 `yield return` 陳述式為止。</span><span class="sxs-lookup"><span data-stu-id="b7058-109">In the following example, the first iteration of the `foreach` loop causes execution to proceed in the `SomeNumbers` iterator method until the first `yield return` statement is reached.</span></span> <span data-ttu-id="b7058-110">此反覆運算會傳回值 3，並保留迭代器方法中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="b7058-110">This iteration returns a value of 3, and the current location in the iterator method is retained.</span></span> <span data-ttu-id="b7058-111">下次反覆運算迴圈時，迭代器方法中的執行會從上次停止的位置繼續，並且在到達 `yield return` 陳述式時再次停止。</span><span class="sxs-lookup"><span data-stu-id="b7058-111">On the next iteration of the loop, execution in the iterator method continues from where it left off, again stopping when it reaches a `yield return` statement.</span></span> <span data-ttu-id="b7058-112">此反覆運算會傳回值 5，並再次保留迭代器方法中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="b7058-112">This iteration returns a value of 5, and the current location in the iterator method is again retained.</span></span> <span data-ttu-id="b7058-113">當到達迭代器方法結尾時，迴圈便完成。</span><span class="sxs-lookup"><span data-stu-id="b7058-113">The loop completes when the end of the iterator method is reached.</span></span>

```csharp
static void Main()
{
    foreach (int number in SomeNumbers())
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 3 5 8
    Console.ReadKey();
}

public static System.Collections.IEnumerable SomeNumbers()
{
    yield return 3;
    yield return 5;
    yield return 8;
}
```

<span data-ttu-id="b7058-114">迭代器方法或 `get` 存取子的傳回型別可以是 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601>。</span><span class="sxs-lookup"><span data-stu-id="b7058-114">The return type of an iterator method or `get` accessor can be <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, or <xref:System.Collections.Generic.IEnumerator%601>.</span></span>

<span data-ttu-id="b7058-115">您可以使用 `yield break` 陳述式結束反覆項目。</span><span class="sxs-lookup"><span data-stu-id="b7058-115">You can use a `yield break` statement to end the iteration.</span></span>

> [!NOTE]
> <span data-ttu-id="b7058-116">如需本主題中除簡易迭代器範例以外的其他所有範例，請加入 `System.Collections` 和 `System.Collections.Generic` 命名空間的 [using](../../language-reference/keywords/using-directive.md) 指示詞。</span><span class="sxs-lookup"><span data-stu-id="b7058-116">For all examples in this topic except the Simple Iterator example, include [using](../../language-reference/keywords/using-directive.md) directives for the `System.Collections` and `System.Collections.Generic` namespaces.</span></span>

## <a name="simple-iterator"></a><span data-ttu-id="b7058-117">簡單的 Iterator</span><span class="sxs-lookup"><span data-stu-id="b7058-117">Simple Iterator</span></span>

<span data-ttu-id="b7058-118">下列範例在 [for](../../language-reference/keywords/for.md) 迴圈內有一行 `yield return` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b7058-118">The following example has a single `yield return` statement that is inside a [for](../../language-reference/keywords/for.md) loop.</span></span> <span data-ttu-id="b7058-119">在 `Main` 中，每次反覆運算 `foreach` 陳述式主體都會建立迭代器函式的呼叫，以繼續進行下一個 `yield return` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b7058-119">In `Main`, each iteration of the `foreach` statement body creates a call to the iterator function, which proceeds to the next `yield return` statement.</span></span>

```csharp
static void Main()
{
    foreach (int number in EvenSequence(5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 6 8 10 12 14 16 18
    Console.ReadKey();
}

public static System.Collections.Generic.IEnumerable<int>
    EvenSequence(int firstNumber, int lastNumber)
{
    // Yield even numbers in the range.
    for (int number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
```

## <a name="creating-a-collection-class"></a><span data-ttu-id="b7058-120">建立集合類別</span><span class="sxs-lookup"><span data-stu-id="b7058-120">Creating a Collection Class</span></span>

<span data-ttu-id="b7058-121">在以下範例中，`DaysOfTheWeek` 類別會實作 <xref:System.Collections.IEnumerable> 介面，而這個介面需使用 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-121">In the following example, the `DaysOfTheWeek` class implements the <xref:System.Collections.IEnumerable> interface, which requires a <xref:System.Collections.IEnumerable.GetEnumerator%2A> method.</span></span> <span data-ttu-id="b7058-122">編譯器會隱含呼叫 `GetEnumerator` 方法，以傳回 <xref:System.Collections.IEnumerator>。</span><span class="sxs-lookup"><span data-stu-id="b7058-122">The compiler implicitly calls the `GetEnumerator` method, which returns an <xref:System.Collections.IEnumerator>.</span></span>

<span data-ttu-id="b7058-123">`GetEnumerator` 方法使用 `yield return` 陳述式，一次傳回一個字串。</span><span class="sxs-lookup"><span data-stu-id="b7058-123">The `GetEnumerator` method returns each string one at a time by using the `yield return` statement.</span></span>

```csharp
static void Main()
{
    DaysOfTheWeek days = new DaysOfTheWeek();

    foreach (string day in days)
    {
        Console.Write(day + " ");
    }
    // Output: Sun Mon Tue Wed Thu Fri Sat
    Console.ReadKey();
}

public class DaysOfTheWeek : IEnumerable
{
    private string[] days = { "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" };

    public IEnumerator GetEnumerator()
    {
        for (int index = 0; index < days.Length; index++)
        {
            // Yield each day of the week.
            yield return days[index];
        }
    }
}
```

<span data-ttu-id="b7058-124">下列範例會建立 `Zoo` 類別，其中包含動物的集合。</span><span class="sxs-lookup"><span data-stu-id="b7058-124">The following example creates a `Zoo` class that contains a collection of animals.</span></span>

<span data-ttu-id="b7058-125">參考類別執行個體 (`theZoo`) 的 `foreach` 陳述式會隱含呼叫 `GetEnumerator` 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-125">The `foreach` statement that refers to the class instance (`theZoo`) implicitly calls the `GetEnumerator` method.</span></span> <span data-ttu-id="b7058-126">參考 `Birds` 和 `Mammals` 屬性的 `foreach` 陳述式會使用 `AnimalsForType` 具名迭代器方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-126">The `foreach` statements that refer to the `Birds` and `Mammals` properties use the `AnimalsForType` named iterator method.</span></span>

```csharp
static void Main()
{
    Zoo theZoo = new Zoo();

    theZoo.AddMammal("Whale");
    theZoo.AddMammal("Rhinoceros");
    theZoo.AddBird("Penguin");
    theZoo.AddBird("Warbler");

    foreach (string name in theZoo)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros Penguin Warbler

    foreach (string name in theZoo.Birds)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Penguin Warbler

    foreach (string name in theZoo.Mammals)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros

    Console.ReadKey();
}

public class Zoo : IEnumerable
{
    // Private members.
    private List<Animal> animals = new List<Animal>();

    // Public methods.
    public void AddMammal(string name)
    {
        animals.Add(new Animal { Name = name, Type = Animal.TypeEnum.Mammal });
    }

    public void AddBird(string name)
    {
        animals.Add(new Animal { Name = name, Type = Animal.TypeEnum.Bird });
    }

    public IEnumerator GetEnumerator()
    {
        foreach (Animal theAnimal in animals)
        {
            yield return theAnimal.Name;
        }
    }

    // Public members.
    public IEnumerable Mammals
    {
        get { return AnimalsForType(Animal.TypeEnum.Mammal); }
    }

    public IEnumerable Birds
    {
        get { return AnimalsForType(Animal.TypeEnum.Bird); }
    }

    // Private methods.
    private IEnumerable AnimalsForType(Animal.TypeEnum type)
    {
        foreach (Animal theAnimal in animals)
        {
            if (theAnimal.Type == type)
            {
                yield return theAnimal.Name;
            }
        }
    }

    // Private class.
    private class Animal
    {
        public enum TypeEnum { Bird, Mammal }

        public string Name { get; set; }
        public TypeEnum Type { get; set; }
    }
}
```

## <a name="using-iterators-with-a-generic-list"></a><span data-ttu-id="b7058-127">搭配泛型清單使用迭代器</span><span class="sxs-lookup"><span data-stu-id="b7058-127">Using Iterators with a Generic List</span></span>

<span data-ttu-id="b7058-128">在以下範例中，<xref:System.Collections.Generic.Stack%601> 泛型類別會實作 <xref:System.Collections.Generic.IEnumerable%601> 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="b7058-128">In the following example, the <xref:System.Collections.Generic.Stack%601> generic class implements the <xref:System.Collections.Generic.IEnumerable%601> generic interface.</span></span> <span data-ttu-id="b7058-129"><xref:System.Collections.Generic.Stack%601.Push%2A> 方法會將值指派給 `T` 類型的陣列。</span><span class="sxs-lookup"><span data-stu-id="b7058-129">The <xref:System.Collections.Generic.Stack%601.Push%2A> method assigns values to an array of type `T`.</span></span> <span data-ttu-id="b7058-130"><xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法會使用 `yield return` 陳述式以傳回陣列值。</span><span class="sxs-lookup"><span data-stu-id="b7058-130">The <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> method returns the array values by using the `yield return` statement.</span></span>

<span data-ttu-id="b7058-131">除了泛型 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法，您也必須實作非泛型 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-131">In addition to the generic <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> method, the non-generic <xref:System.Collections.IEnumerable.GetEnumerator%2A> method must also be implemented.</span></span> <span data-ttu-id="b7058-132">這是因為 <xref:System.Collections.Generic.IEnumerable%601> 繼承自 <xref:System.Collections.IEnumerable>。</span><span class="sxs-lookup"><span data-stu-id="b7058-132">This is because <xref:System.Collections.Generic.IEnumerable%601> inherits from <xref:System.Collections.IEnumerable>.</span></span> <span data-ttu-id="b7058-133">非泛型實作會延後到泛型實作。</span><span class="sxs-lookup"><span data-stu-id="b7058-133">The non-generic implementation defers to the generic implementation.</span></span>

<span data-ttu-id="b7058-134">此範例使用具名迭代器來支援逐一查看相同資料集合的各種方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-134">The example uses named iterators to support various ways of iterating through the same collection of data.</span></span> <span data-ttu-id="b7058-135">這些具名迭代器是 `TopToBottom` 和 `BottomToTop` 屬性，以及 `TopN` 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-135">These named iterators are the `TopToBottom` and `BottomToTop` properties, and the `TopN` method.</span></span>

<span data-ttu-id="b7058-136">`BottomToTop` 屬性會在 `get` 存取子中使用迭代器。</span><span class="sxs-lookup"><span data-stu-id="b7058-136">The `BottomToTop` property uses an iterator in a `get` accessor.</span></span>

```csharp
static void Main()
{
    Stack<int> theStack = new Stack<int>();

    //  Add items to the stack.
    for (int number = 0; number <= 9; number++)
    {
        theStack.Push(number);
    }

    // Retrieve items from the stack.
    // foreach is allowed because theStack implements IEnumerable<int>.
    foreach (int number in theStack)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0

    // foreach is allowed, because theStack.TopToBottom returns IEnumerable(Of Integer).
    foreach (int number in theStack.TopToBottom)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0

    foreach (int number in theStack.BottomToTop)
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 0 1 2 3 4 5 6 7 8 9

    foreach (int number in theStack.TopN(7))
    {
        Console.Write("{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3

    Console.ReadKey();
}

public class Stack<T> : IEnumerable<T>
{
    private T[] values = new T[100];
    private int top = 0;

    public void Push(T t)
    {
        values[top] = t;
        top++;
    }
    public T Pop()
    {
        top--;
        return values[top];
    }

    // This method implements the GetEnumerator method. It allows
    // an instance of the class to be used in a foreach statement.
    public IEnumerator<T> GetEnumerator()
    {
        for (int index = top - 1; index >= 0; index--)
        {
            yield return values[index];
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }

    public IEnumerable<T> TopToBottom
    {
        get { return this; }
    }

    public IEnumerable<T> BottomToTop
    {
        get
        {
            for (int index = 0; index <= top - 1; index++)
            {
                yield return values[index];
            }
        }
    }

    public IEnumerable<T> TopN(int itemsFromTop)
    {
        // Return less than itemsFromTop if necessary.
        int startIndex = itemsFromTop >= top ? 0 : top - itemsFromTop;

        for (int index = top - 1; index >= startIndex; index--)
        {
            yield return values[index];
        }
    }

}
```

## <a name="syntax-information"></a><span data-ttu-id="b7058-137">語法資訊</span><span class="sxs-lookup"><span data-stu-id="b7058-137">Syntax Information</span></span>

<span data-ttu-id="b7058-138">出現的迭代器可以是方法或 `get` 存取子。</span><span class="sxs-lookup"><span data-stu-id="b7058-138">An iterator can occur as a method or `get` accessor.</span></span> <span data-ttu-id="b7058-139">迭代器不能出現在事件、執行個體建構函式、靜態建構函式或靜態完成項中。</span><span class="sxs-lookup"><span data-stu-id="b7058-139">An iterator cannot occur in an event, instance constructor, static constructor, or static finalizer.</span></span>

<span data-ttu-id="b7058-140">從語句中的運算式類型 `yield return` 到反覆運算器所傳回之的型別引數，都必須有隱含轉換 `IEnumerable<T>` 。</span><span class="sxs-lookup"><span data-stu-id="b7058-140">An implicit conversion must exist from the expression type in the `yield return` statement to the type argument for the `IEnumerable<T>` returned by the iterator.</span></span>

<span data-ttu-id="b7058-141">在 C# 中，迭代器方法不可有任何 `in`、`ref` 或 `out` 參數。</span><span class="sxs-lookup"><span data-stu-id="b7058-141">In C#, an iterator method cannot have any `in`, `ref`, or `out` parameters.</span></span>

<span data-ttu-id="b7058-142">在 c # 中，不是 `yield` 保留字，只有在或關鍵字之前使用時才具有特殊意義 `return` `break` 。</span><span class="sxs-lookup"><span data-stu-id="b7058-142">In C#, `yield` is not a reserved word and has special meaning only when it is used before a `return` or `break` keyword.</span></span>

## <a name="technical-implementation"></a><span data-ttu-id="b7058-143">技術實作</span><span class="sxs-lookup"><span data-stu-id="b7058-143">Technical Implementation</span></span>

<span data-ttu-id="b7058-144">雖然您將迭代器撰寫成方法，但編譯器會將其轉譯成巢狀類別，其實也就是狀態機器。</span><span class="sxs-lookup"><span data-stu-id="b7058-144">Although you write an iterator as a method, the compiler translates it into a nested class that is, in effect, a state machine.</span></span> <span data-ttu-id="b7058-145">此類別會在用戶端程式碼中的 `foreach` 迴圈繼續期間追蹤迭代器的位置。</span><span class="sxs-lookup"><span data-stu-id="b7058-145">This class keeps track of the position of the iterator as long the `foreach` loop in the client code continues.</span></span>

<span data-ttu-id="b7058-146">若要查看編譯器的功能，您可以使用 Ildasm.exe 工具，檢視為迭代器方法產生的 Microsoft 中繼語言程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7058-146">To see what the compiler does, you can use the Ildasm.exe tool to view the Microsoft intermediate language code that's generated for an iterator method.</span></span>

<span data-ttu-id="b7058-147">當您建立 [class](../../language-reference/keywords/class.md) 或 [struct](../../language-reference/builtin-types/struct.md) 的迭代器時，您不需要實作整個 <xref:System.Collections.IEnumerator> 介面。</span><span class="sxs-lookup"><span data-stu-id="b7058-147">When you create an iterator for a [class](../../language-reference/keywords/class.md) or [struct](../../language-reference/builtin-types/struct.md), you don't have to implement the whole <xref:System.Collections.IEnumerator> interface.</span></span> <span data-ttu-id="b7058-148">當編譯器偵測到迭代器時，它會自動產生 <xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601> 介面的 `Current`、`MoveNext` 和 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-148">When the compiler detects the iterator, it automatically generates the `Current`, `MoveNext`, and `Dispose` methods of the <xref:System.Collections.IEnumerator> or <xref:System.Collections.Generic.IEnumerator%601> interface.</span></span>

<span data-ttu-id="b7058-149">之後每次反覆運算 `foreach` 迴圈 (或直接呼叫 `IEnumerator.MoveNext`)，下一個迭代器程式碼主體都會在上一個 `yield return` 陳述式之後繼續。</span><span class="sxs-lookup"><span data-stu-id="b7058-149">On each successive iteration of the `foreach` loop (or the direct call to `IEnumerator.MoveNext`), the next iterator code body resumes after the previous `yield return` statement.</span></span> <span data-ttu-id="b7058-150">然後繼續執行至下一個 `yield return` 陳述式，直到達到迭代器主體結尾，或遇到 `yield break` 陳述式為止。</span><span class="sxs-lookup"><span data-stu-id="b7058-150">It then continues to the next `yield return` statement until the end of the iterator body is reached, or until a `yield break` statement is encountered.</span></span>

<span data-ttu-id="b7058-151">迭代器不支援 <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="b7058-151">Iterators don't support the <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="b7058-152">若要從頭開始逐一查看，您必須取得新的迭代器。</span><span class="sxs-lookup"><span data-stu-id="b7058-152">To reiterate from the start, you must obtain a new iterator.</span></span> <span data-ttu-id="b7058-153">對迭代器方法傳回的迭代器呼叫 <xref:System.Collections.IEnumerator.Reset%2A> 會擲回 <xref:System.NotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="b7058-153">Calling <xref:System.Collections.IEnumerator.Reset%2A> on the iterator returned by an iterator method throws a <xref:System.NotSupportedException>.</span></span>

<span data-ttu-id="b7058-154">如需其他資訊，請參閱 [C# 語言規格](~/_csharplang/spec/classes.md#iterators)。</span><span class="sxs-lookup"><span data-stu-id="b7058-154">For additional information, see the [C# Language Specification](~/_csharplang/spec/classes.md#iterators).</span></span>

## <a name="use-of-iterators"></a><span data-ttu-id="b7058-155">迭代器的使用</span><span class="sxs-lookup"><span data-stu-id="b7058-155">Use of Iterators</span></span>

<span data-ttu-id="b7058-156">當您需要使用複雜的程式碼來填入清單序列時，迭代器可讓您維持 `foreach` 迴圈的簡潔性。</span><span class="sxs-lookup"><span data-stu-id="b7058-156">Iterators enable you to maintain the simplicity of a `foreach` loop when you need to use complex code to populate a list sequence.</span></span> <span data-ttu-id="b7058-157">當您想要執行下列作業時，這會很有用：</span><span class="sxs-lookup"><span data-stu-id="b7058-157">This can be useful when you want to do the following:</span></span>

- <span data-ttu-id="b7058-158">在第一次反覆運算 `foreach` 迴圈之後修改清單序列。</span><span class="sxs-lookup"><span data-stu-id="b7058-158">Modify the list sequence after the first `foreach` loop iteration.</span></span>

- <span data-ttu-id="b7058-159">避免在第一次反覆運算 `foreach` 迴圈之前完整載入大型清單。</span><span class="sxs-lookup"><span data-stu-id="b7058-159">Avoid fully loading a large list before the first iteration of a `foreach` loop.</span></span> <span data-ttu-id="b7058-160">分頁擷取以分批載入資料表資料列即為一例。</span><span class="sxs-lookup"><span data-stu-id="b7058-160">An example is a paged fetch to load a batch of table rows.</span></span> <span data-ttu-id="b7058-161">另一個範例是 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 方法，它會在 .net 中執行反覆運算器。</span><span class="sxs-lookup"><span data-stu-id="b7058-161">Another example is the <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> method, which implements iterators in .NET.</span></span>

- <span data-ttu-id="b7058-162">在迭代器中封裝建立清單。</span><span class="sxs-lookup"><span data-stu-id="b7058-162">Encapsulate building the list in the iterator.</span></span> <span data-ttu-id="b7058-163">在迭代器方法中，您可以建立清單，然後在迴圈中產生每個結果。</span><span class="sxs-lookup"><span data-stu-id="b7058-163">In the iterator method, you can build the list and then yield each result in a loop.</span></span>

## <a name="see-also"></a><span data-ttu-id="b7058-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7058-164">See also</span></span>

- <xref:System.Collections.Generic>
- <xref:System.Collections.Generic.IEnumerable%601>
- [<span data-ttu-id="b7058-165">foreach、in</span><span class="sxs-lookup"><span data-stu-id="b7058-165">foreach, in</span></span>](../../language-reference/keywords/foreach-in.md)
- [<span data-ttu-id="b7058-166">yield</span><span class="sxs-lookup"><span data-stu-id="b7058-166">yield</span></span>](../../language-reference/keywords/yield.md)
- [<span data-ttu-id="b7058-167">搭配陣列使用 foreach</span><span class="sxs-lookup"><span data-stu-id="b7058-167">Using foreach with Arrays</span></span>](../arrays/using-foreach-with-arrays.md)
- [<span data-ttu-id="b7058-168">泛型</span><span class="sxs-lookup"><span data-stu-id="b7058-168">Generics</span></span>](../generics/index.md)

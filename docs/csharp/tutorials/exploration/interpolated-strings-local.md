---
title: 字串插補 - C# 教學課程
description: 此教學課程示範如何使用 C# 字串插補功能，在較大字串中包含格式化運算式結果。
ms.date: 10/23/2018
ms.openlocfilehash: d1b78670361e8b333499d12b68c0364ad9e40a85
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82796050"
---
# <a name="use-string-interpolation-to-construct-formatted-strings"></a><span data-ttu-id="f31b0-103">使用字串插補來建構格式化的字串</span><span class="sxs-lookup"><span data-stu-id="f31b0-103">Use string interpolation to construct formatted strings</span></span>

<span data-ttu-id="f31b0-104">此教學課程將教您如何使用 C# [字串插補](../../language-reference/tokens/interpolated.md)，在單一結果字串中插入值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-104">This tutorial teaches you how to use C# [string interpolation](../../language-reference/tokens/interpolated.md) to insert values into a single result string.</span></span> <span data-ttu-id="f31b0-105">您將會撰寫 C# 程式碼，並查看程式碼編譯和執行的結果。</span><span class="sxs-lookup"><span data-stu-id="f31b0-105">You write C# code and see the results of compiling and running it.</span></span> <span data-ttu-id="f31b0-106">此教學課程包含一系列的課程，示範如何將值插入至字串，並以不同的方式設定那些值的格式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-106">The tutorial contains a series of lessons that show you how to insert values into a string and format those values in different ways.</span></span>

<span data-ttu-id="f31b0-107">此教學課程要求您必須有可用於開發的電腦。</span><span class="sxs-lookup"><span data-stu-id="f31b0-107">This tutorial expects that you have a machine you can use for development.</span></span> <span data-ttu-id="f31b0-108">.NET 教學課程[Hello World 在10分鐘內](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)，有在 Windows、Linux 或 macOS 上設定本機開發環境的指示。</span><span class="sxs-lookup"><span data-stu-id="f31b0-108">The .NET tutorial [Hello World in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) has instructions for setting up your local development environment on Windows, Linux, or macOS.</span></span> <span data-ttu-id="f31b0-109">您也可以在瀏覽器中完成本教學課程的[互動式版本](interpolated-strings.yml)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-109">You can also complete the [interactive version](interpolated-strings.yml) of this tutorial in your browser.</span></span>

## <a name="create-an-interpolated-string"></a><span data-ttu-id="f31b0-110">建立插入字串</span><span class="sxs-lookup"><span data-stu-id="f31b0-110">Create an interpolated string</span></span>

<span data-ttu-id="f31b0-111">建立名為 *interpolated* 的目錄。</span><span class="sxs-lookup"><span data-stu-id="f31b0-111">Create a directory named *interpolated*.</span></span> <span data-ttu-id="f31b0-112">讓它成為目前目錄，並從主控台視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f31b0-112">Make it the current directory and run the following command from a console window:</span></span>

```dotnetcli
dotnet new console
```

<span data-ttu-id="f31b0-113">此命令會在目前的目錄中建立新的 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-113">This command creates a new .NET Core console application in the current directory.</span></span>

<span data-ttu-id="f31b0-114">在您最愛的編輯器中開啟 *Program.cs*，並將 `Console.WriteLine("Hello World!");` 行取代為下列程式碼；其中，您可以將 `<name>` 取代為您的名稱：</span><span class="sxs-lookup"><span data-stu-id="f31b0-114">Open *Program.cs* in your favorite editor, and replace the line `Console.WriteLine("Hello World!");` with the following code, where you replace `<name>` with your name:</span></span>

```csharp
var name = "<name>";
Console.WriteLine($"Hello, {name}. It's a pleasure to meet you!");
```

<span data-ttu-id="f31b0-115">在主控台視窗中鍵入 `dotnet run` 來嘗試此程式碼。</span><span class="sxs-lookup"><span data-stu-id="f31b0-115">Try this code by typing `dotnet run` in your console window.</span></span> <span data-ttu-id="f31b0-116">當您執行程式時，它會顯示問候語中包含您名稱的單一字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-116">When you run the program, it displays a single string that includes your name in the greeting.</span></span> <span data-ttu-id="f31b0-117"><xref:System.Console.WriteLine%2A> 方法呼叫中所含的字串是「插入字串運算式」\*\*。</span><span class="sxs-lookup"><span data-stu-id="f31b0-117">The string included in the <xref:System.Console.WriteLine%2A> method call is an *interpolated string expression*.</span></span> <span data-ttu-id="f31b0-118">它是一種範本，可讓您從包含內嵌程式碼的字串建構單一字串 (稱為「結果字串」\*\*)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-118">It's a kind of template that lets you construct a single string (called the *result string*) from a string that includes embedded code.</span></span> <span data-ttu-id="f31b0-119">插入字串特別適用於將值插入至字串或將字串串連 (聯結在一起)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-119">Interpolated strings are particularly useful for inserting values into a string or concatenating (joining together) strings.</span></span>

<span data-ttu-id="f31b0-120">這個簡單範例包含每個插入字串都必須要有的兩個項目：</span><span class="sxs-lookup"><span data-stu-id="f31b0-120">This simple example contains the two elements that every interpolated string must have:</span></span>

- <span data-ttu-id="f31b0-121">左引號字元之前開頭為 `$` 字元的字串常值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-121">A string literal that begins with the `$` character before its opening quotation mark character.</span></span> <span data-ttu-id="f31b0-122">`$` 符號與引號字元之間不能有任何空格。</span><span class="sxs-lookup"><span data-stu-id="f31b0-122">There can't be any spaces between the `$` symbol and the quotation mark character.</span></span> <span data-ttu-id="f31b0-123">(如果您想要查看包含空格時會發生什麼情況，請在 `$` 字元後面插入空格、儲存檔案，然後在主控台視窗中鍵入 `dotnet run` 以重新執行程式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-123">(If you'd like to see what happens if you include one, insert a space after the `$` character, save the file, and run the program again by typing `dotnet run` in the console window.</span></span> <span data-ttu-id="f31b0-124">C# 編譯器會顯示錯誤訊息「錯誤 CS1056: 未預期的字元 '$'」)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-124">The C# compiler displays an error message, "error CS1056: Unexpected character '$'".)</span></span>

- <span data-ttu-id="f31b0-125">一或多個「插入運算式」\*\*。</span><span class="sxs-lookup"><span data-stu-id="f31b0-125">One or more *interpolation expressions*.</span></span> <span data-ttu-id="f31b0-126">插入運算式是以左右大括弧 (`{` 和 `}`) 指出。</span><span class="sxs-lookup"><span data-stu-id="f31b0-126">An interpolation expression is indicated by an opening and closing brace (`{` and `}`).</span></span> <span data-ttu-id="f31b0-127">您可以放置任何 C# 運算式，以傳回大括號內的值 (包含 `null`)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-127">You can put any C# expression that returns a value (including `null`) inside the braces.</span></span>

<span data-ttu-id="f31b0-128">嘗試更多包含一些其他資料類型的字串插補範例。</span><span class="sxs-lookup"><span data-stu-id="f31b0-128">Let's try a few more string interpolation examples with some other data types.</span></span>

## <a name="include-different-data-types"></a><span data-ttu-id="f31b0-129">包含不同的資料類型</span><span class="sxs-lookup"><span data-stu-id="f31b0-129">Include different data types</span></span>

<span data-ttu-id="f31b0-130">在上節中，您使用字串插補將某個字串插入至另一個字串內部。</span><span class="sxs-lookup"><span data-stu-id="f31b0-130">In the previous section, you used string interpolation to insert one string inside of another.</span></span> <span data-ttu-id="f31b0-131">不過，插入運算式的結果可以是任意資料類型。</span><span class="sxs-lookup"><span data-stu-id="f31b0-131">The result of an interpolation expression can be of any data type, though.</span></span> <span data-ttu-id="f31b0-132">請包含插入字串中各種資料類型的值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-132">Let's include values of various data types in an interpolated string.</span></span>

<span data-ttu-id="f31b0-133">在下列範例中，我們先定義具有 `Name` [屬性](../../properties.md)與 `ToString` [方法](../../methods.md)的[類別](../../programming-guide/classes-and-structs/classes.md)資料類型 `Vegetable`，它會[覆寫](../../language-reference/keywords/override.md)<xref:System.Object.ToString?displayProperty=nameWithType> 方法的行為。</span><span class="sxs-lookup"><span data-stu-id="f31b0-133">In the following example, we first define a [class](../../programming-guide/classes-and-structs/classes.md) data type `Vegetable` that has a `Name` [property](../../properties.md) and a `ToString` [method](../../methods.md), which [overrides](../../language-reference/keywords/override.md) the behavior of the <xref:System.Object.ToString?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="f31b0-134">存取修飾詞會使該方法可供任何用戶端程式代碼取得`Vegetable`實例的字串表示。 [ `public` ](../../language-reference/keywords/public.md)</span><span class="sxs-lookup"><span data-stu-id="f31b0-134">The [`public` access modifier](../../language-reference/keywords/public.md) makes that method available to any client code to get the string representation of a `Vegetable` instance.</span></span> <span data-ttu-id="f31b0-135">在範例中， `Vegetable.ToString`方法會[傳回在此](../../programming-guide/classes-and-structs/constructors.md) `Vegetable`函`Name`式上初始化之屬性的值：</span><span class="sxs-lookup"><span data-stu-id="f31b0-135">In the example the `Vegetable.ToString` method returns the value of the `Name` property that is initialized at the `Vegetable` [constructor](../../programming-guide/classes-and-structs/constructors.md):</span></span>

```csharp
public Vegetable(string name) => Name = name;
```

<span data-ttu-id="f31b0-136">然後，我們會使用[ `new`運算子](../../language-reference/operators/new-operator.md)來`Vegetable`建立名`item`為的類別實例，並提供此函式的`Vegetable`名稱：</span><span class="sxs-lookup"><span data-stu-id="f31b0-136">Then we create an instance of the `Vegetable` class named `item` by using the [`new` operator](../../language-reference/operators/new-operator.md) and providing a name for the constructor `Vegetable`:</span></span>

```csharp
var item = new Vegetable("eggplant");
```

<span data-ttu-id="f31b0-137">最後，我們將 `item` 變數併入插入字串，而此插入字串也包含 <xref:System.DateTime> 值、<xref:System.Decimal> 值和 `Unit` [enumeration](../../language-reference/builtin-types/enum.md) 值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-137">Finally, we include the `item` variable into an interpolated string that also contains a <xref:System.DateTime> value, a <xref:System.Decimal> value, and a `Unit` [enumeration](../../language-reference/builtin-types/enum.md) value.</span></span> <span data-ttu-id="f31b0-138">將編輯器中的所有 C# 程式碼都取代為下列程式碼，然後使用 `dotnet run` 命令來執行此程式碼：</span><span class="sxs-lookup"><span data-stu-id="f31b0-138">Replace all of the C# code in your editor with the following code, and then use the `dotnet run` command to run it:</span></span>

```csharp
using System;

public class Vegetable
{
   public Vegetable(string name) => Name = name;

   public string Name { get; }

   public override string ToString() => Name;
}

public class Program
{
   public enum Unit { item, kilogram, gram, dozen };

   public static void Main()
   {
      var item = new Vegetable("eggplant");
      var date = DateTime.Now;
      var price = 1.99m;
      var unit = Unit.item;
      Console.WriteLine($"On {date}, the price of {item} was {price} per {unit}.");
   }
}
```

<span data-ttu-id="f31b0-139">請注意，插入字串中的插入運算式 `item` 會解析為結果字串中的文字 "eggplant"。</span><span class="sxs-lookup"><span data-stu-id="f31b0-139">Note that the interpolation expression `item` in the interpolated string resolves to the text "eggplant" in the result string.</span></span> <span data-ttu-id="f31b0-140">原因是，運算式結果的型別不是字串時，會使用下列方式將結果解析為字串：</span><span class="sxs-lookup"><span data-stu-id="f31b0-140">That's because, when the type of the expression result is not a string, the result is resolved to a string in the following way:</span></span>

- <span data-ttu-id="f31b0-141">如果插入運算式評估為 `null`，則會使用空字串 (""，或 <xref:System.String.Empty?displayProperty=nameWithType>)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-141">If the interpolation expression evaluates to `null`, an empty string ("", or <xref:System.String.Empty?displayProperty=nameWithType>) is used.</span></span>

- <span data-ttu-id="f31b0-142">如果插入運算式未評估為 `null`，一般會呼叫結果類型的 `ToString` 方法。</span><span class="sxs-lookup"><span data-stu-id="f31b0-142">If the interpolation expression doesn't evaluate to `null`, typically the `ToString` method of the result type is called.</span></span> <span data-ttu-id="f31b0-143">測試這項作業的方式是更新 `Vegetable.ToString` 方法的實作。</span><span class="sxs-lookup"><span data-stu-id="f31b0-143">You can test this by updating the implementation of the `Vegetable.ToString` method.</span></span> <span data-ttu-id="f31b0-144">您甚至可能不需要實作 `ToString` 方法，因為每個類型都有這個方法的某種實作。</span><span class="sxs-lookup"><span data-stu-id="f31b0-144">You might not even need to implement the `ToString` method since every type has some implementation of this method.</span></span> <span data-ttu-id="f31b0-145">若要測試此作業，請將範例中 `Vegetable.ToString` 方法的定義註解化 (作法是在其前面放置註解符號 `//`)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-145">To test this, comment out the definition of the `Vegetable.ToString` method in the example (to do that, put a comment symbol, `//`, in front of it).</span></span> <span data-ttu-id="f31b0-146">在輸出中，字串 "eggplant" 會取代為完整類型名稱 (在此範例中，為 "Vegetable")，這是 <xref:System.Object.ToString?displayProperty=nameWithType> 方法的預設行為。</span><span class="sxs-lookup"><span data-stu-id="f31b0-146">In the output, the string "eggplant" is replaced by the fully qualified type name ("Vegetable" in this example), which is the default behavior of the <xref:System.Object.ToString?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="f31b0-147">列舉值 `ToString` 方法的預設行為是傳回該值的字串表示。</span><span class="sxs-lookup"><span data-stu-id="f31b0-147">The default behavior of the `ToString` method for an enumeration value is to return the string representation of the value.</span></span>

<span data-ttu-id="f31b0-148">在此範例的輸出中，日期太過精確 (eggplant 價格不會因第二個而變更)，而價格值未指出貨幣單位。</span><span class="sxs-lookup"><span data-stu-id="f31b0-148">In the output from this example, the date is too precise (the price of eggplant doesn't change every second), and the price value doesn't indicate a unit of currency.</span></span> <span data-ttu-id="f31b0-149">在下節中，您將學習如何控制運算式結果的字串表示格式來修正這些問題。</span><span class="sxs-lookup"><span data-stu-id="f31b0-149">In the next section, you'll learn how to fix those issues by controlling the format of string representations of the expression results.</span></span>

## <a name="control-the-formatting-of-interpolation-expressions"></a><span data-ttu-id="f31b0-150">控制插入運算式的格式</span><span class="sxs-lookup"><span data-stu-id="f31b0-150">Control the formatting of interpolation expressions</span></span>

<span data-ttu-id="f31b0-151">在上節中，已將兩個格式不佳的字串插入至結果字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-151">In the previous section, two poorly formatted strings were inserted into the result string.</span></span> <span data-ttu-id="f31b0-152">其中一個是只有日期才適合的日期和時間值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-152">One was a date and time value for which only the date was appropriate.</span></span> <span data-ttu-id="f31b0-153">第二個是未指出其貨幣單位的價格。</span><span class="sxs-lookup"><span data-stu-id="f31b0-153">The second was a price that didn't indicate its unit of currency.</span></span> <span data-ttu-id="f31b0-154">這兩個問題都很容易解決。</span><span class="sxs-lookup"><span data-stu-id="f31b0-154">Both issues are easy to address.</span></span> <span data-ttu-id="f31b0-155">字串插補可讓您指定「格式字串」\*\*，以控制特定類型的格式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-155">String interpolation lets you specify *format strings* that control the formatting of particular types.</span></span> <span data-ttu-id="f31b0-156">修改前一個範例中的 `Console.WriteLine` 呼叫，使其包含日期和價格運算式的格式字串，如下行所示：</span><span class="sxs-lookup"><span data-stu-id="f31b0-156">Modify the call to `Console.WriteLine` from the previous example to include the format strings for the date and price expressions as shown in the following line:</span></span>

```csharp
Console.WriteLine($"On {date:d}, the price of {item} was {price:C2} per {unit}.");
```

<span data-ttu-id="f31b0-157">在插入運算式後面接著冒號 (":") 和格式字串，即可指定格式字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-157">You specify a format string by following the interpolation expression with a colon (":") and the format string.</span></span> <span data-ttu-id="f31b0-158">"d" 是[標準日期和時間格式字串](../../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier)，可呈現簡短日期格式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-158">"d" is a [standard date and time format string](../../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier) that represents the short date format.</span></span> <span data-ttu-id="f31b0-159">"C2" 是[標準數值格式字串](../../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier)，表示數位是小數點後有兩位數的貨幣值。</span><span class="sxs-lookup"><span data-stu-id="f31b0-159">"C2" is a  [standard numeric format string](../../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier) that represents a number as a currency value with two digits after the decimal point.</span></span>

<span data-ttu-id="f31b0-160">.NET 程式庫中有多種類型都支援一組預先定義的格式字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-160">A number of types in the .NET libraries support a predefined set of format strings.</span></span> <span data-ttu-id="f31b0-161">其中包含所有數值類型以及日期和時間類型。</span><span class="sxs-lookup"><span data-stu-id="f31b0-161">These include all the numeric types and the date and time types.</span></span> <span data-ttu-id="f31b0-162">如需支援格式字串之類型的完整清單，請參閱[在 .NET 中格式化類型](../../../standard/base-types/formatting-types.md)一文中的[格式字串和 .NET 類別庫類型](../../../standard/base-types/formatting-types.md#format-strings-and-net-types)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-162">For a complete list of types that support format strings, see [Format Strings and .NET Class Library Types](../../../standard/base-types/formatting-types.md#format-strings-and-net-types) in the [Formatting Types in .NET](../../../standard/base-types/formatting-types.md) article.</span></span>

<span data-ttu-id="f31b0-163">嘗試在文字編輯器中修改格式字串，並在每次進行變更時，重新執行程式以查看變更對日期和時間以及數值格式的影響。</span><span class="sxs-lookup"><span data-stu-id="f31b0-163">Try modifying the format strings in your text editor and, each time you make a change, rerun the program to see how the changes affect the formatting of the date and time and the numeric value.</span></span> <span data-ttu-id="f31b0-164">將 `{date:d}` 中的 "d" 變更為 "t" (顯示簡短時間格式)、"y" (顯示年份和月份) 以及 "yyyy" (將年份顯示為四位數)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-164">Change the "d" in `{date:d}` to "t" (to display the short time format), "y" (to display the year and month), and "yyyy" (to display the year as a four-digit number).</span></span> <span data-ttu-id="f31b0-165">將 `{price:C2}` 中的 "C2" 變更為 "e" (適用於指數標記法) 和 "F3" (適用於小數點後面有三位數的數值)。</span><span class="sxs-lookup"><span data-stu-id="f31b0-165">Change the "C2" in `{price:C2}` to "e" (for exponential notation) and "F3" (for a numeric value with three digits after the decimal point).</span></span>

<span data-ttu-id="f31b0-166">除了控制格式之外，您也可以控制結果字串中所含格式化字串的欄位寬度和對齊方式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-166">In addition to controlling formatting, you can also control the field width and alignment of the formatted strings that are included in the result string.</span></span> <span data-ttu-id="f31b0-167">在下節中，您將學習如何執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="f31b0-167">In the next section, you'll learn how to do this.</span></span>

## <a name="control-the-field-width-and-alignment-of-interpolation-expressions"></a><span data-ttu-id="f31b0-168">控制插入運算式的欄位寬度和對齊方式</span><span class="sxs-lookup"><span data-stu-id="f31b0-168">Control the field width and alignment of interpolation expressions</span></span>

<span data-ttu-id="f31b0-169">一般情況下，插入運算式的結果格式化為字串時，結果字串中會包含該字串，而且沒有前置或尾端空格。</span><span class="sxs-lookup"><span data-stu-id="f31b0-169">Ordinarily, when the result of an interpolation expression is formatted to string, that string is included in a result string without leading or trailing spaces.</span></span> <span data-ttu-id="f31b0-170">特別是當您使用一組資料時，可控制欄位寬度和文字對齊方式有助於產生更容易讀取的輸出。</span><span class="sxs-lookup"><span data-stu-id="f31b0-170">Particularly when you work with a set of data, being able to control a field width and text alignment helps to produce a more readable output.</span></span> <span data-ttu-id="f31b0-171">若要確認這一點，請將文字編輯器中的所有程式碼都取代為下列程式碼，然後鍵入 `dotnet run` 以執行程式：</span><span class="sxs-lookup"><span data-stu-id="f31b0-171">To see this, replace all the code in your text editor with the following code, then type `dotnet run` to execute the program:</span></span>

```csharp
using System;
using System.Collections.Generic;

public class Example
{
   public static void Main()
   {
      var titles = new Dictionary<string, string>()
      {
          ["Doyle, Arthur Conan"] = "Hound of the Baskervilles, The",
          ["London, Jack"] = "Call of the Wild, The",
          ["Shakespeare, William"] = "Tempest, The"
      };

      Console.WriteLine("Author and Title List");
      Console.WriteLine();
      Console.WriteLine($"|{"Author",-25}|{"Title",30}|");
      foreach (var title in titles)
         Console.WriteLine($"|{title.Key,-25}|{title.Value,30}|");
   }
}
```

<span data-ttu-id="f31b0-172">作者名稱會靠左對齊，而他們所撰寫的標題會靠右對齊。</span><span class="sxs-lookup"><span data-stu-id="f31b0-172">The names of authors are left-aligned, and the titles they wrote are right-aligned.</span></span> <span data-ttu-id="f31b0-173">在插入運算式後面加上逗號 (",")，並指定「最小」\*\* 欄位寬度，即可指定對齊方式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-173">You specify the alignment by adding a comma (",") after an interpolation expression and designating the *minimum* field width.</span></span> <span data-ttu-id="f31b0-174">如果指定的值是正數，則欄位會靠右對齊。</span><span class="sxs-lookup"><span data-stu-id="f31b0-174">If the specified value is a positive number, the field is right-aligned.</span></span> <span data-ttu-id="f31b0-175">如果它是負數，則欄位會靠左對齊。</span><span class="sxs-lookup"><span data-stu-id="f31b0-175">If it is a negative number, the field is left-aligned.</span></span>

<span data-ttu-id="f31b0-176">嘗試移除 `{"Author",-25}` 和 `{title.Key,-25}` 程式碼中的負號，然後重新執行此範例，如下列程式碼所執行：</span><span class="sxs-lookup"><span data-stu-id="f31b0-176">Try removing the negative signs from the `{"Author",-25}` and `{title.Key,-25}` code and run the example again, as the following code does:</span></span>

```csharp
Console.WriteLine($"|{"Author",25}|{"Title",30}|");
foreach (var title in titles)
   Console.WriteLine($"|{title.Key,25}|{title.Value,30}|");
```

<span data-ttu-id="f31b0-177">目前，作者資訊會靠右對齊。</span><span class="sxs-lookup"><span data-stu-id="f31b0-177">This time, the author information is right-aligned.</span></span>

<span data-ttu-id="f31b0-178">您可以將對齊規範與格式字串結合為單一插入運算式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-178">You can combine an alignment specifier and a format string for a single interpolation expression.</span></span> <span data-ttu-id="f31b0-179">若要這樣做，請先指定對齊方式，而且後面接著冒號和格式字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-179">To do that, specify the alignment first, followed by a colon and the format string.</span></span> <span data-ttu-id="f31b0-180">將 `Main` 方法內的所有程式碼都取代為下列程式碼，以顯示具有所定義欄位寬度的三個格式化字串。</span><span class="sxs-lookup"><span data-stu-id="f31b0-180">Replace all of the code inside the `Main` method with the following code, which displays three formatted strings with defined field widths.</span></span> <span data-ttu-id="f31b0-181">然後輸入 `dotnet run` 命令，以執行程式。</span><span class="sxs-lookup"><span data-stu-id="f31b0-181">Then run the program by entering the `dotnet run` command.</span></span>

```csharp
Console.WriteLine($"[{DateTime.Now,-20:d}] Hour [{DateTime.Now,-10:HH}] [{1063.342,15:N2}] feet");
```

<span data-ttu-id="f31b0-182">輸出會與下列內容類似：</span><span class="sxs-lookup"><span data-stu-id="f31b0-182">The output looks something like the following:</span></span>

```console
[04/14/2018          ] Hour [16        ] [       1,063.34] feet
```

<span data-ttu-id="f31b0-183">您已完成字串插補教學課程。</span><span class="sxs-lookup"><span data-stu-id="f31b0-183">You've completed the string interpolation tutorial.</span></span>

<span data-ttu-id="f31b0-184">如需詳細資訊，請參閱[字串插補](../../language-reference/tokens/interpolated.md)主題和 [C# 中的字串插補](../string-interpolation.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="f31b0-184">For more information, see the [String interpolation](../../language-reference/tokens/interpolated.md) topic and the [String interpolation in C#](../string-interpolation.md) tutorial.</span></span>

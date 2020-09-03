---
title: 使用集合 - C# 教學課程簡介
description: 在此教學課程中探索 List 集合來了解 C#。
ms.date: 10/13/2017
ms.custom: mvc
ms.openlocfilehash: e2282df21420630634911e07f4fb3b94f34a792b
ms.sourcegitcommit: b1f4756120deaecb8b554477bb040620f69a4209
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414679"
---
# <a name="learn-to-manage-data-collections-using-the-generic-list-type"></a><span data-ttu-id="8ee8e-103">了解如何使用一般清單類型管理資料收集</span><span class="sxs-lookup"><span data-stu-id="8ee8e-103">Learn to manage data collections using the generic list type</span></span>

<span data-ttu-id="8ee8e-104">此入門教學課程提供 C# 語言的簡介，以及 <xref:System.Collections.Generic.List%601> 類別的基礎知識。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-104">This introductory tutorial provides an introduction to the C# language and the basics of the <xref:System.Collections.Generic.List%601> class.</span></span>

<span data-ttu-id="8ee8e-105">此教學課程要求您必須有可用於開發的電腦。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-105">This tutorial expects you to have a machine you can use for development.</span></span> <span data-ttu-id="8ee8e-106">.NET 教學課程 [Hello World 10 分鐘內](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) 的指示，說明如何在 Windows、Linux 或 macOS 上設定您的本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-106">The .NET tutorial [Hello World in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) has instructions for setting up your local development environment on Windows, Linux, or macOS.</span></span> <span data-ttu-id="8ee8e-107">您可以在[熟悉開發工具](local-environment.md)中快速檢視將會用到的命令，並取得可提供詳細資料的連結。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-107">A quick overview of the commands you'll use is in [Become familiar with the development tools](local-environment.md), with links to more details.</span></span>

## <a name="a-basic-list-example"></a><span data-ttu-id="8ee8e-108">基本的清單範例</span><span class="sxs-lookup"><span data-stu-id="8ee8e-108">A basic list example</span></span>

<span data-ttu-id="8ee8e-109">建立名為 *list-tutorial* 的目錄。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-109">Create a directory named *list-tutorial*.</span></span> <span data-ttu-id="8ee8e-110">將該目錄設為目前的目錄，並執行 `dotnet new console`。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-110">Make that the current directory and run `dotnet new console`.</span></span>

<span data-ttu-id="8ee8e-111">在您最愛的編輯器中開啟 *Program.cs*，並以下列內容取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-111">Open *Program.cs* in your favorite editor, and replace the existing code with the following:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

<span data-ttu-id="8ee8e-112">以您的名稱取代 `<name>`。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-112">Replace `<name>` with your name.</span></span> <span data-ttu-id="8ee8e-113">儲存 *Program.cs*。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-113">Save *Program.cs*.</span></span> <span data-ttu-id="8ee8e-114">在主控台視窗中輸入 `dotnet run` 來嘗試它。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-114">Type `dotnet run` in your console window to try it.</span></span>

<span data-ttu-id="8ee8e-115">您已建立字串清單，在該清單中新增三個名稱，並以全部大寫的形式列印出那些名稱。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-115">You've created a list of strings, added three names to that list, and printed out the names in all CAPS.</span></span> <span data-ttu-id="8ee8e-116">您會使用從先前教學課程中學習到的概念，在清單中執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-116">You're using concepts that you've learned in earlier tutorials to loop through the list.</span></span>

<span data-ttu-id="8ee8e-117">顯示名稱的程式碼會運用[字串內插補點](../../language-reference/tokens/interpolated.md)功能。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-117">The code to display names makes use of the [string interpolation](../../language-reference/tokens/interpolated.md) feature.</span></span>  <span data-ttu-id="8ee8e-118">當您在 `string` 的前方放置 `$` 時，您可以在字串宣告中內嵌 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-118">When you precede a `string` with the `$` character, you can embed C# code in the string declaration.</span></span> <span data-ttu-id="8ee8e-119">實際的字串會以它所產生的值取代 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-119">The actual string replaces that C# code with the value it generates.</span></span> <span data-ttu-id="8ee8e-120">在此範例中，它會以每個 (轉換成大寫字母的) 名稱取代 `{name.ToUpper()}`，因為您呼叫了 <xref:System.String.ToUpper%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-120">In this example, it replaces the `{name.ToUpper()}` with each name, converted to capital letters, because you called the <xref:System.String.ToUpper%2A> method.</span></span>

<span data-ttu-id="8ee8e-121">讓我們繼續探索。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-121">Let's keep exploring.</span></span>

## <a name="modify-list-contents"></a><span data-ttu-id="8ee8e-122">修改清單內容</span><span class="sxs-lookup"><span data-stu-id="8ee8e-122">Modify list contents</span></span>

<span data-ttu-id="8ee8e-123">您所建立的集合會使用 <xref:System.Collections.Generic.List%601> 類型。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-123">The collection you created uses the <xref:System.Collections.Generic.List%601> type.</span></span> <span data-ttu-id="8ee8e-124">此類型會儲存元素的序列。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-124">This type stores sequences of elements.</span></span> <span data-ttu-id="8ee8e-125">您會在角括弧之間指定元素的類型。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-125">You specify the type of the elements between the angle brackets.</span></span>

<span data-ttu-id="8ee8e-126">此 <xref:System.Collections.Generic.List%601> 類型的其中一個重要層面，在於它可以擴張或縮小，使您可以新增或移除元素。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-126">One important aspect of this <xref:System.Collections.Generic.List%601> type is that it can grow or shrink, enabling you to add or remove elements.</span></span> <span data-ttu-id="8ee8e-127">在 `Main` 方法中關閉 `}` 之前，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-127">Add this code before the closing `}` in the `Main` method:</span></span>

```csharp
Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

<span data-ttu-id="8ee8e-128">您已在清單末端新增兩個額外的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-128">You've added two more names to the end of the list.</span></span> <span data-ttu-id="8ee8e-129">您也移除了一個名稱。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-129">You've also removed one as well.</span></span> <span data-ttu-id="8ee8e-130">儲存檔案，並輸入 `dotnet run` 來嘗試它。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-130">Save the file, and type `dotnet run` to try it.</span></span>

<span data-ttu-id="8ee8e-131"><xref:System.Collections.Generic.List%601> 也可讓您透過**索引**參考個別的項目。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-131">The <xref:System.Collections.Generic.List%601> enables you to reference individual items by **index** as well.</span></span> <span data-ttu-id="8ee8e-132">您需將索引放在 `[` 和 `]` 語彙基元之間，位於清單名稱之後。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-132">You place the index between `[` and `]` tokens following the list name.</span></span> <span data-ttu-id="8ee8e-133">C# 使用 0 作為第一個索引。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-133">C# uses 0 for the first index.</span></span> <span data-ttu-id="8ee8e-134">將下列程式碼新增至您剛才新增的程式碼下方，然後嘗試它：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-134">Add this code directly below the code you just added and try it:</span></span>

```csharp
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

<span data-ttu-id="8ee8e-135">您無法存取清單結尾以外的索引。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-135">You can't access an index beyond the end of the list.</span></span> <span data-ttu-id="8ee8e-136">請記住，索引是從 0 開始，因此最大的有效索引數目為清單項目數目減去 1。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-136">Remember that indices start at 0, so the largest valid index is one less than the number of items in the list.</span></span> <span data-ttu-id="8ee8e-137">您可以使用 <xref:System.Collections.Generic.List%601.Count%2A> 屬性檢查清單的長度。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-137">You can check how long the list is using the <xref:System.Collections.Generic.List%601.Count%2A> property.</span></span> <span data-ttu-id="8ee8e-138">在 Main 方法的結尾，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-138">Add the following code at the end of the Main method:</span></span>

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
 ```

<span data-ttu-id="8ee8e-139">儲存檔案，然後再次輸入 `dotnet run` 以查看結果。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-139">Save the file, and type `dotnet run` again to see the results.</span></span>

## <a name="search-and-sort-lists"></a><span data-ttu-id="8ee8e-140">針對清單進行搜尋和排序</span><span class="sxs-lookup"><span data-stu-id="8ee8e-140">Search and sort lists</span></span>

<span data-ttu-id="8ee8e-141">我們的範例所使用的清單相對較小，但是您的應用程式可能經常會建立具有更多元素的清單，數量甚至會達數千個之多。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-141">Our samples use relatively small lists, but your applications may often create lists with many more elements, sometimes numbering in the thousands.</span></span> <span data-ttu-id="8ee8e-142">若要在這些較大的集合中尋找元素，您需要在清單中搜尋不同的項目。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-142">To find elements in these larger collections, you need to search the list for different items.</span></span> <span data-ttu-id="8ee8e-143"><xref:System.Collections.Generic.List%601.IndexOf%2A> 方法會搜尋項目，並傳回該項目的索引。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-143">The <xref:System.Collections.Generic.List%601.IndexOf%2A> method searches for an item and returns the index of the item.</span></span> <span data-ttu-id="8ee8e-144">如果專案不在清單中，則 `IndexOf` 傳回 `-1` 。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-144">If the item isn't in the list, `IndexOf` returns `-1`.</span></span> <span data-ttu-id="8ee8e-145">將下列程式碼新增到 `Main` 方法的底部：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-145">Add this code to the bottom of your `Main` method:</span></span>

```csharp
var index = names.IndexOf("Felipe");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
}

index = names.IndexOf("Not Found");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");

}
```

<span data-ttu-id="8ee8e-146">也可以對您清單中的項目進行排序。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-146">The items in your list can be sorted as well.</span></span> <span data-ttu-id="8ee8e-147"><xref:System.Collections.Generic.List%601.Sort%2A>方法會依標準順序排序清單中的所有專案， (以字母順序排序字串) 。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-147">The <xref:System.Collections.Generic.List%601.Sort%2A> method sorts all the items in the list in their normal order (alphabetically for strings).</span></span> <span data-ttu-id="8ee8e-148">將下列程式碼新增到 `Main` 方法的底部：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-148">Add this code to the bottom of our `Main` method:</span></span>

```csharp
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

<span data-ttu-id="8ee8e-149">儲存檔案並輸入 `dotnet run` 以嘗試此最新版本。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-149">Save the file and type `dotnet run` to try this latest version.</span></span>

<span data-ttu-id="8ee8e-150">在開始下一節之前，讓我們將目前的程式碼移到另一個個別的方法。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-150">Before you start the next section, let's move the current code into a separate method.</span></span> <span data-ttu-id="8ee8e-151">這可讓您更輕鬆地開始處理新的範例。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-151">That makes it easier to start working with a new example.</span></span> <span data-ttu-id="8ee8e-152">將 `Main` 方法重新命名為 `WorkingWithStrings`，然後撰寫會呼叫 `WorkingWithStrings` 的新 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-152">Rename your `Main` method to `WorkingWithStrings` and write a new `Main` method that calls `WorkingWithStrings`.</span></span> <span data-ttu-id="8ee8e-153">當您完成時，您的程式碼看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-153">When you've finished, your code should look like this:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkingWithStrings();
        }

        static void WorkingWithStrings()
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine();
            names.Add("Maria");
            names.Add("Bill");
            names.Remove("Ana");
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine($"My name is {names[0]}");
            Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");

            Console.WriteLine($"The list has {names.Count} people in it");

            var index = names.IndexOf("Felipe");
            if (index == -1)
            {
                Console.WriteLine($"When an item is not found, IndexOf returns {index}");
            }
            else
            {
                Console.WriteLine($"The name {names[index]} is at index {index}");
            }

            index = names.IndexOf("Not Found");
            if (index == -1)
            {
                Console.WriteLine($"When an item is not found, IndexOf returns {index}");
            }
            else
            {
                Console.WriteLine($"The name {names[index]} is at index {index}");

            }

            names.Sort();
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

## <a name="lists-of-other-types"></a><span data-ttu-id="8ee8e-154">其他類型的清單</span><span class="sxs-lookup"><span data-stu-id="8ee8e-154">Lists of other types</span></span>

<span data-ttu-id="8ee8e-155">到目前為止，您都是使用清單中的 `string` 類型。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-155">You've been using the `string` type in lists so far.</span></span> <span data-ttu-id="8ee8e-156">讓我們使用不同的類型建立 <xref:System.Collections.Generic.List%601>。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-156">Let's make a <xref:System.Collections.Generic.List%601> using a different type.</span></span> <span data-ttu-id="8ee8e-157">讓我們來建置一組數字。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-157">Let's build a set of numbers.</span></span>

<span data-ttu-id="8ee8e-158">將下列內容新增到新 `Main` 方法的底部：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-158">Add the following to the bottom of your new `Main` method:</span></span>

```csharp
var fibonacciNumbers = new List<int> {1, 1};
```

<span data-ttu-id="8ee8e-159">這將會建立整數清單，並將前兩個整數設定為 1 的值。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-159">That creates a list of integers, and sets the first two integers to the value 1.</span></span> <span data-ttu-id="8ee8e-160">這是*費氏數列*的前兩個值。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-160">These are the first two values of a *Fibonacci Sequence*, a sequence of numbers.</span></span> <span data-ttu-id="8ee8e-161">這兩個值之後每個費式數列數字，都會是其前兩個數字的總和。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-161">Each next Fibonacci number is found by taking the sum of the previous two numbers.</span></span> <span data-ttu-id="8ee8e-162">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8ee8e-162">Add this code:</span></span>

```csharp
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach (var item in fibonacciNumbers)
    Console.WriteLine(item);
```

<span data-ttu-id="8ee8e-163">儲存檔案並輸入 `dotnet run` 來查看結果。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-163">Save the file and type `dotnet run` to see the results.</span></span>

> [!TIP]
> <span data-ttu-id="8ee8e-164">若要僅專注於本節的內容，您可以對呼叫 `WorkingWithStrings();` 的程式碼進行註解化。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-164">To concentrate on just this section, you can comment out the code that calls `WorkingWithStrings();`.</span></span> <span data-ttu-id="8ee8e-165">請在該呼叫之前放置兩個 `/` 字元，例如：`// WorkingWithStrings();`。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-165">Just put two `/` characters in front of the call like this:  `// WorkingWithStrings();`.</span></span>

## <a name="challenge"></a><span data-ttu-id="8ee8e-166">挑戰</span><span class="sxs-lookup"><span data-stu-id="8ee8e-166">Challenge</span></span>

<span data-ttu-id="8ee8e-167">看看您是否可以結合運用來自此課程和先前課程的概念。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-167">See if you can put together some of the concepts from this and earlier lessons.</span></span> <span data-ttu-id="8ee8e-168">請依費式數列數字，擴展您到目前為止所建立的內容。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-168">Expand on what you've built so far with Fibonacci Numbers.</span></span> <span data-ttu-id="8ee8e-169">請嘗試將程式碼撰寫成可產生該數列的前 20 個數字。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-169">Try to write the code to generate the first 20 numbers in the sequence.</span></span> <span data-ttu-id="8ee8e-170">(小提示：第 20 個費式數列數字為 6765)。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-170">(As a hint, the 20th Fibonacci number is 6765.)</span></span>

## <a name="complete-challenge"></a><span data-ttu-id="8ee8e-171">完成挑戰</span><span class="sxs-lookup"><span data-stu-id="8ee8e-171">Complete challenge</span></span>

<span data-ttu-id="8ee8e-172">您可以查看 [GitHub 上已完成的範例程式碼](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23)，以查看範例解決方案。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-172">You can see an example solution by [looking at the finished sample code on GitHub](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23).</span></span>

<span data-ttu-id="8ee8e-173">在迴圈每次反覆運算時，您都必須取清單中的最後兩個整數，將它們加總，並將該值新增至清單。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-173">With each iteration of the loop, you're taking the last two integers in the list, summing them, and adding that value to the list.</span></span> <span data-ttu-id="8ee8e-174">迴圈會持續重複，直到將 20 個項目新增至清單為止。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-174">The loop repeats until you've added 20 items to the list.</span></span>

<span data-ttu-id="8ee8e-175">恭喜，您已完成清單的教學課程。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-175">Congratulations, you've completed the list tutorial.</span></span> <span data-ttu-id="8ee8e-176">您可以在自己的開發環境中，繼續完成[類別簡介](introduction-to-classes.md)教學課程中的內容。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-176">You can continue with the [Introduction to classes](introduction-to-classes.md) tutorial in your own development environment.</span></span>

<span data-ttu-id="8ee8e-177">您可以在 .NET 基礎檔的集合中深入瞭解如何使用此 `List` 類型[collections](../../../standard/collections/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-177">You can learn more about working with the `List` type in the .NET fundamentals article on [collections](../../../standard/collections/index.md).</span></span> <span data-ttu-id="8ee8e-178">您也能學習到許多其他的集合類型。</span><span class="sxs-lookup"><span data-stu-id="8ee8e-178">You'll also learn about many other collection types.</span></span>

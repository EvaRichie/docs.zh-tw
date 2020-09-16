---
title: 處理 LINQ
description: 本教學課程會教導您如何使用 LINQ 產生序列、撰寫用於 LINQ 查詢的方法，並區分立即和延遲評估。
ms.date: 10/29/2018
ms.technology: csharp-linq
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.openlocfilehash: 59e86d6412e16728fb03d05f7f4e221a26ec1bb1
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90536232"
---
# <a name="work-with-language-integrated-query-linq"></a><span data-ttu-id="954b2-103">使用 (LINQ) 的語言整合式查詢</span><span class="sxs-lookup"><span data-stu-id="954b2-103">Work with Language-Integrated Query (LINQ)</span></span>

## <a name="introduction"></a><span data-ttu-id="954b2-104">簡介</span><span class="sxs-lookup"><span data-stu-id="954b2-104">Introduction</span></span>

<span data-ttu-id="954b2-105">此教學課程會教導您 .NET Core 和 C# 語言中的功能。</span><span class="sxs-lookup"><span data-stu-id="954b2-105">This tutorial teaches you features in .NET Core and the C# language.</span></span> <span data-ttu-id="954b2-106">您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="954b2-106">You’ll learn how to:</span></span>

- <span data-ttu-id="954b2-107">使用 LINQ 產生序列。</span><span class="sxs-lookup"><span data-stu-id="954b2-107">Generate sequences with LINQ.</span></span>
- <span data-ttu-id="954b2-108">撰寫可以在 LINQ 查詢中輕鬆使用的方法。</span><span class="sxs-lookup"><span data-stu-id="954b2-108">Write methods that can be easily used in LINQ queries.</span></span>
- <span data-ttu-id="954b2-109">區分積極和延遲評估。</span><span class="sxs-lookup"><span data-stu-id="954b2-109">Distinguish between eager and lazy evaluation.</span></span>

<span data-ttu-id="954b2-110">您將建置一個應用程式來學習這些技術，其中將示範任何魔術師都會的基礎技巧：[完美洗牌 (英文)](https://en.wikipedia.org/wiki/Faro_shuffle)。</span><span class="sxs-lookup"><span data-stu-id="954b2-110">You'll learn these techniques by building an application that demonstrates one of the basic skills of any magician: the [faro shuffle](https://en.wikipedia.org/wiki/Faro_shuffle).</span></span> <span data-ttu-id="954b2-111">簡單地說，完美洗牌是將牌組確實分成兩半，然後互相交錯每一張紙牌來重建原始牌堆的技術。</span><span class="sxs-lookup"><span data-stu-id="954b2-111">Briefly, a faro shuffle is a technique where you split a card deck exactly in half, then the shuffle interleaves each one card from each half to rebuild the original deck.</span></span>

<span data-ttu-id="954b2-112">魔術師使用這項技術的原因，是因為在每次洗牌後，每張紙牌都會在已知的位置，其順序會遵循重複性的模式。</span><span class="sxs-lookup"><span data-stu-id="954b2-112">Magicians use this technique because every card is in a known location after each shuffle, and the order is a repeating pattern.</span></span>

<span data-ttu-id="954b2-113">基於您的目的，這是以較輕鬆的方式來了解對資料序列的操作。</span><span class="sxs-lookup"><span data-stu-id="954b2-113">For your purposes, it is a light hearted look at manipulating sequences of data.</span></span> <span data-ttu-id="954b2-114">您將建立的應用程式會結構化卡片，然後執行一連串的洗牌，每次都會寫出序列。</span><span class="sxs-lookup"><span data-stu-id="954b2-114">The application you'll build constructs a card deck and then performs a sequence of shuffles, writing the sequence out each time.</span></span> <span data-ttu-id="954b2-115">您也會比較原始的順序與更新過的順序。</span><span class="sxs-lookup"><span data-stu-id="954b2-115">You'll also compare the updated order to the original order.</span></span>

<span data-ttu-id="954b2-116">本教學課程有多個步驟。</span><span class="sxs-lookup"><span data-stu-id="954b2-116">This tutorial has multiple steps.</span></span> <span data-ttu-id="954b2-117">在每個步驟之後，您可以執行應用程式並查看進度。</span><span class="sxs-lookup"><span data-stu-id="954b2-117">After each step, you can run the application and see the progress.</span></span> <span data-ttu-id="954b2-118">您也可以在 dotnet/samples GitHub 存放機制中查看[完整範例](https://github.com/dotnet/samples/blob/master/csharp/getting-started/console-linq)。</span><span class="sxs-lookup"><span data-stu-id="954b2-118">You can also see the [completed sample](https://github.com/dotnet/samples/blob/master/csharp/getting-started/console-linq) in the dotnet/samples GitHub repository.</span></span> <span data-ttu-id="954b2-119">如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#view-and-download-samples)。</span><span class="sxs-lookup"><span data-stu-id="954b2-119">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#view-and-download-samples).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954b2-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="954b2-120">Prerequisites</span></span>

<span data-ttu-id="954b2-121">您將必須設定電腦以執行 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="954b2-121">You’ll need to set up your machine to run .NET core.</span></span> <span data-ttu-id="954b2-122">您可以在 [.Net Core 下載](https://dotnet.microsoft.com/download) 頁面中找到安裝指示。</span><span class="sxs-lookup"><span data-stu-id="954b2-122">You can find the installation instructions on the [.NET Core Download](https://dotnet.microsoft.com/download) page.</span></span> <span data-ttu-id="954b2-123">您可以在 Windows、Ubuntu Linux 或 OS X 上執行此應用程式，或在 Docker 容器中執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="954b2-123">You can run this application on Windows, Ubuntu Linux, or OS X, or in a Docker container.</span></span> <span data-ttu-id="954b2-124">您將必須安裝慣用的程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="954b2-124">You’ll need to install your favorite code editor.</span></span> <span data-ttu-id="954b2-125">下列說明使用 [Visual Studio Code](https://code.visualstudio.com/) 是開放原始碼的跨平臺編輯器。</span><span class="sxs-lookup"><span data-stu-id="954b2-125">The descriptions below use [Visual Studio Code](https://code.visualstudio.com/) which is an open source, cross-platform editor.</span></span> <span data-ttu-id="954b2-126">不過，您可以使用您熟悉的任何工具。</span><span class="sxs-lookup"><span data-stu-id="954b2-126">However, you can use whatever tools you are comfortable with.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="954b2-127">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="954b2-127">Create the Application</span></span>

<span data-ttu-id="954b2-128">第一個步驟是建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="954b2-128">The first step is to create a new application.</span></span> <span data-ttu-id="954b2-129">請開啟命令提示字元，然後為您的應用程式建立新目錄。</span><span class="sxs-lookup"><span data-stu-id="954b2-129">Open a command prompt and create a new directory for your application.</span></span> <span data-ttu-id="954b2-130">使該目錄成為目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="954b2-130">Make that the current directory.</span></span> <span data-ttu-id="954b2-131">在命令提示字元處輸入命令 `dotnet new console`。</span><span class="sxs-lookup"><span data-stu-id="954b2-131">Type the command `dotnet new console` at the command prompt.</span></span> <span data-ttu-id="954b2-132">這會建立基本 "Hello World" 應用程式的起始檔案。</span><span class="sxs-lookup"><span data-stu-id="954b2-132">This creates the starter files for a basic "Hello World" application.</span></span>

<span data-ttu-id="954b2-133">如果您從未使用過 C#，[此教學課程](console-teleprompter.md)會說明 C# 程式的結構。</span><span class="sxs-lookup"><span data-stu-id="954b2-133">If you've never used C# before, [this tutorial](console-teleprompter.md) explains the structure of a C# program.</span></span> <span data-ttu-id="954b2-134">您可以閱讀該教學課程，然後再回到這裡以深入了解 LINQ。</span><span class="sxs-lookup"><span data-stu-id="954b2-134">You can read that and then return here to learn more about LINQ.</span></span>

## <a name="create-the-data-set"></a><span data-ttu-id="954b2-135">建立資料集</span><span class="sxs-lookup"><span data-stu-id="954b2-135">Create the Data Set</span></span>

<span data-ttu-id="954b2-136">開始之前，請確定下列程式碼行位於 `dotnet new console` 所產生的`Program.cs` 檔案最上方：</span><span class="sxs-lookup"><span data-stu-id="954b2-136">Before you begin, make sure that the following lines are at the top of the `Program.cs` file generated by `dotnet new console`:</span></span>

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
```

<span data-ttu-id="954b2-137">如果這三行程式碼 (`using` 陳述式) 不在檔案最上方，我們的程式將不會編譯。</span><span class="sxs-lookup"><span data-stu-id="954b2-137">If these three lines (`using` statements) aren't at the top of the file, our program will not compile.</span></span>

<span data-ttu-id="954b2-138">現在已具備您所需的所有參考，請考慮構成一副撲克牌的內容。</span><span class="sxs-lookup"><span data-stu-id="954b2-138">Now that you have all of the references that you'll need, consider what constitutes a deck of cards.</span></span> <span data-ttu-id="954b2-139">通常，一副撲克牌有四種花色，而每種花色有十三個值。</span><span class="sxs-lookup"><span data-stu-id="954b2-139">Commonly, a deck of playing cards has four suits, and each suit has thirteen values.</span></span> <span data-ttu-id="954b2-140">一般來說，您可以考慮立即建立 `Card` 類別，並以手動方式填入 `Card` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="954b2-140">Normally, you might consider creating a `Card` class right off the bat and populating a collection of `Card` objects by hand.</span></span> <span data-ttu-id="954b2-141">使用 LINQ，您就能使用比平常方式更簡潔的方法來處理一副撲克牌的建立。</span><span class="sxs-lookup"><span data-stu-id="954b2-141">With LINQ, you can be more concise than the usual way of dealing with creating a deck of cards.</span></span> <span data-ttu-id="954b2-142">您不需建立 `Card` 類別，而是改為建立兩個序列，分別代表花色和順位。</span><span class="sxs-lookup"><span data-stu-id="954b2-142">Instead of creating a `Card` class, you can create two sequences to represent suits and ranks, respectively.</span></span> <span data-ttu-id="954b2-143">您將建立一對非常簡單的[迭代器方法\*\*](../iterators.md#enumeration-sources-with-iterator-methods)，其將會產生順位和花色作為字串的 <xref:System.Collections.Generic.IEnumerable%601>：</span><span class="sxs-lookup"><span data-stu-id="954b2-143">You'll create a really simple pair of [*iterator methods*](../iterators.md#enumeration-sources-with-iterator-methods) that will generate the ranks and suits as <xref:System.Collections.Generic.IEnumerable%601>s of strings:</span></span>

```csharp
// Program.cs
// The Main() method

static IEnumerable<string> Suits()
{
    yield return "clubs";
    yield return "diamonds";
    yield return "hearts";
    yield return "spades";
}

static IEnumerable<string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
```

<span data-ttu-id="954b2-144">將這些方法放置於 `Program.cs` 檔案中的 `Main` 方法下方。</span><span class="sxs-lookup"><span data-stu-id="954b2-144">Place these underneath the `Main` method in your `Program.cs` file.</span></span> <span data-ttu-id="954b2-145">這兩個方法都利用 `yield return` 語法，來在執行時產生序列。</span><span class="sxs-lookup"><span data-stu-id="954b2-145">These two methods both utilize the `yield return` syntax to produce a sequence as they run.</span></span> <span data-ttu-id="954b2-146">編譯器會建置能實作 <xref:System.Collections.Generic.IEnumerable%601>，並會在要求它們時產生字串序列的物件。</span><span class="sxs-lookup"><span data-stu-id="954b2-146">The compiler builds an object that implements <xref:System.Collections.Generic.IEnumerable%601> and generates the sequence of strings as they are requested.</span></span>

<span data-ttu-id="954b2-147">現在，使用這些迭代器方法來建立一副牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-147">Now, use these iterator methods to create the deck of cards.</span></span> <span data-ttu-id="954b2-148">您將在 `Main` 方法中放置 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-148">You'll place the LINQ query in our `Main` method.</span></span> <span data-ttu-id="954b2-149">以下就來看看此程序：</span><span class="sxs-lookup"><span data-stu-id="954b2-149">Here's a look at it:</span></span>

```csharp
// Program.cs
static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    // Display each card that we've generated and placed in startingDeck in the console
    foreach (var card in startingDeck)
    {
        Console.WriteLine(card);
    }
}
```

<span data-ttu-id="954b2-150">多個 `from` 子句會產生 <xref:System.Linq.Enumerable.SelectMany%2A>，這會將第一個序列與第二個序列中的每個元素相互結合，來建立單一序列。</span><span class="sxs-lookup"><span data-stu-id="954b2-150">The multiple `from` clauses produce a <xref:System.Linq.Enumerable.SelectMany%2A>, which creates a single sequence from combining each element in the first sequence with each element in the second sequence.</span></span> <span data-ttu-id="954b2-151">其順序對我們來說很重要。</span><span class="sxs-lookup"><span data-stu-id="954b2-151">The order is important for our purposes.</span></span> <span data-ttu-id="954b2-152">第一個來源序列 (花色) 中的第一個元素，會與第二個序列 (順位) 中的每個元素結合。</span><span class="sxs-lookup"><span data-stu-id="954b2-152">The first element in the first source sequence (Suits) is combined with every element in the second sequence (Ranks).</span></span> <span data-ttu-id="954b2-153">這樣會產生第一個花色的十三張紙牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-153">This produces all thirteen cards of first suit.</span></span> <span data-ttu-id="954b2-154">該程序會針對第一個序列 (花色) 中的每個元素重複執行。</span><span class="sxs-lookup"><span data-stu-id="954b2-154">That process is repeated with each element in the first sequence (Suits).</span></span> <span data-ttu-id="954b2-155">最終結果是一疊先依花色，並接著依值排序的牌堆。</span><span class="sxs-lookup"><span data-stu-id="954b2-155">The end result is a deck of cards ordered by suits, followed by values.</span></span>

<span data-ttu-id="954b2-156">請務必牢記在心，無論您選擇要在上述使用的查詢語法中撰寫 LINQ，還是改用方法語法，一律可從某種語法形式移至另一種語法形式。</span><span class="sxs-lookup"><span data-stu-id="954b2-156">It's important to keep in mind that whether you choose to write your LINQ in the query syntax used above or use method syntax instead, it's always possible to go from one form of syntax to the other.</span></span> <span data-ttu-id="954b2-157">上述以查詢語法撰寫的查詢可利用方法語法撰寫為：</span><span class="sxs-lookup"><span data-stu-id="954b2-157">The above query written in query syntax can be written in method syntax as:</span></span>

```csharp
var startingDeck = Suits().SelectMany(suit => Ranks().Select(rank => new { Suit = suit, Rank = rank }));
```

<span data-ttu-id="954b2-158">編譯器會將以查詢語法撰寫的 LINQ 陳述式轉譯為相等的方法呼叫語法。</span><span class="sxs-lookup"><span data-stu-id="954b2-158">The compiler translates LINQ statements written with query syntax into the equivalent method call syntax.</span></span> <span data-ttu-id="954b2-159">因此，不論您的語法選擇為何，這兩個查詢版本都會產生相同的結果。</span><span class="sxs-lookup"><span data-stu-id="954b2-159">Therefore, regardless of your syntax choice, the two versions of the query produce the same result.</span></span> <span data-ttu-id="954b2-160">選擇最適合您情況的語法：例如，如果您所在的小組中有部分成員對於使用方法語法有困難，請嘗試使用查詢語法。</span><span class="sxs-lookup"><span data-stu-id="954b2-160">Choose which syntax works best for your situation: for instance, if you're working in a team where some of the members have difficulty with method syntax, try to prefer using query syntax.</span></span>

<span data-ttu-id="954b2-161">現在，請執行您目前所建置的範例。</span><span class="sxs-lookup"><span data-stu-id="954b2-161">Go ahead and run the sample you've built at this point.</span></span> <span data-ttu-id="954b2-162">它會顯示牌堆中全部 52 張紙牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-162">It will display all 52 cards in the deck.</span></span> <span data-ttu-id="954b2-163">您會發現以偵錯工具執行此範例，對於觀察 `Suits()` 和 `Ranks()` 方法的執行方式非常有用。</span><span class="sxs-lookup"><span data-stu-id="954b2-163">You may find it very helpful to run this sample under a debugger to observe how the `Suits()` and `Ranks()` methods execute.</span></span> <span data-ttu-id="954b2-164">您可以清楚地看見每個序列中的每個字串都只會在需要時產生。</span><span class="sxs-lookup"><span data-stu-id="954b2-164">You can clearly see that each string in each sequence is generated only as it is needed.</span></span>

![主控台視窗顯示寫出 52 張紙牌的應用程式。](./media/working-with-linq/console-52-card-application.png)

## <a name="manipulate-the-order"></a><span data-ttu-id="954b2-166">操作訂單</span><span class="sxs-lookup"><span data-stu-id="954b2-166">Manipulate the Order</span></span>

<span data-ttu-id="954b2-167">接著，專注於您將如何在這副牌中洗牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-167">Next, focus on how you're going to shuffle the cards in the deck.</span></span> <span data-ttu-id="954b2-168">所有好好洗牌步驟中的第一個步驟是將這副牌一分為二。</span><span class="sxs-lookup"><span data-stu-id="954b2-168">The first step in any good shuffle is to split the deck in two.</span></span> <span data-ttu-id="954b2-169">包含於 LINQ API 的<xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 方法可為您提供該功能。</span><span class="sxs-lookup"><span data-stu-id="954b2-169">The <xref:System.Linq.Enumerable.Take%2A> and <xref:System.Linq.Enumerable.Skip%2A> methods that are part of the LINQ APIs provide that feature for you.</span></span> <span data-ttu-id="954b2-170">將它們放在 `foreach` 迴圈下方：</span><span class="sxs-lookup"><span data-stu-id="954b2-170">Place them underneath the `foreach` loop:</span></span>

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    // 52 cards in a deck, so 52 / 2 = 26
    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
}
```

<span data-ttu-id="954b2-171">不過，標準程式庫中並未利用任何洗牌方法，所以您將必須自行撰寫。</span><span class="sxs-lookup"><span data-stu-id="954b2-171">However, there's no shuffle method to take advantage of in the standard library, so you'll have to write your own.</span></span> <span data-ttu-id="954b2-172">您將建立的洗牌方法會舉例說明您將與 LINQ 型程式搭配使用的數種技術，以便在步驟中說明此程序的每個部分。</span><span class="sxs-lookup"><span data-stu-id="954b2-172">The shuffle method you'll be creating illustrates several techniques that you'll use with LINQ-based programs, so each part of this process will be explained in steps.</span></span>

<span data-ttu-id="954b2-173">若要針對您與從 LINQ 查詢中取回的 <xref:System.Collections.Generic.IEnumerable%601> 進行互動的方式新增一些功能，您必須撰寫一些稱為[擴充方法](../programming-guide/classes-and-structs/extension-methods.md)的特殊種類方法。</span><span class="sxs-lookup"><span data-stu-id="954b2-173">In order to add some functionality to how you interact with the <xref:System.Collections.Generic.IEnumerable%601> you'll get back from LINQ queries, you'll need to write some special kinds of methods called [extension methods](../programming-guide/classes-and-structs/extension-methods.md).</span></span> <span data-ttu-id="954b2-174">簡單地說，擴充方法是具有特殊用途的「靜態方法」\*\*，其會將新功能新增到已經存在的類型，而不需修改您想要將功能新增到其中的原始類型。</span><span class="sxs-lookup"><span data-stu-id="954b2-174">Briefly, an extension method is a special purpose *static method* that adds new functionality to an already-existing type without having to modify the original type you want to add functionality to.</span></span>

<span data-ttu-id="954b2-175">藉由將新的「靜態」\*\* 類別檔案新增到名為 `Extensions.cs` 的程式，來為您的擴充方法提供一個新家，然後開始建置第一個擴充方法：</span><span class="sxs-lookup"><span data-stu-id="954b2-175">Give your extension methods a new home by adding a new *static* class file to your program called `Extensions.cs`, and then start building out the first extension method:</span></span>

```csharp
// Extensions.cs
using System;
using System.Collections.Generic;
using System.Linq;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>(this IEnumerable<T> first, IEnumerable<T> second)
        {
            // Your implementation will go here soon enough
        }
    }
}
```

<span data-ttu-id="954b2-176">查看一下方法簽章，特別是參數：</span><span class="sxs-lookup"><span data-stu-id="954b2-176">Look at the method signature for a moment, specifically the parameters:</span></span>

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T> (this IEnumerable<T> first, IEnumerable<T> second)
```

<span data-ttu-id="954b2-177">您可以方法的第一個引數上看到加入的 `this` 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="954b2-177">You can see the addition of the `this` modifier on the first argument to the method.</span></span> <span data-ttu-id="954b2-178">這表示您會將方法當作第一個引數之型別的成員方法來呼叫。</span><span class="sxs-lookup"><span data-stu-id="954b2-178">That means you call the method as though it were a member method of the type of the first argument.</span></span> <span data-ttu-id="954b2-179">此方法宣告也遵循標準慣用語，其中輸入和輸出型別為 `IEnumerable<T>`。</span><span class="sxs-lookup"><span data-stu-id="954b2-179">This method declaration also follows a standard idiom where the input and output types are `IEnumerable<T>`.</span></span> <span data-ttu-id="954b2-180">該作法可使 LINQ 方法鏈結在一起，以執行更複雜的查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-180">That practice enables LINQ methods to be chained together to perform more complex queries.</span></span>

<span data-ttu-id="954b2-181">當然，因為您將這副牌分成數堆，所以必須將這幾堆聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="954b2-181">Naturally, since you split the deck into halves, you'll need to join those halves together.</span></span> <span data-ttu-id="954b2-182">在程式碼中，這表示您將會列舉您透過和一次取得的兩個序列 <xref:System.Linq.Enumerable.Take%2A> <xref:System.Linq.Enumerable.Skip%2A> 、 *`interleaving`* 元素，以及建立一個序列：您現在已隨機的卡片組。</span><span class="sxs-lookup"><span data-stu-id="954b2-182">In code, this means you'll be enumerating both of the sequences you acquired through <xref:System.Linq.Enumerable.Take%2A> and <xref:System.Linq.Enumerable.Skip%2A> at once, *`interleaving`* the elements, and creating one sequence: your now-shuffled deck of cards.</span></span> <span data-ttu-id="954b2-183">若要撰寫可搭配兩個序列使用的 LINQ 方法，您必須先了解 <xref:System.Collections.Generic.IEnumerable%601> 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="954b2-183">Writing a LINQ method that works with two sequences requires that you understand how <xref:System.Collections.Generic.IEnumerable%601> works.</span></span>

<span data-ttu-id="954b2-184"><xref:System.Collections.Generic.IEnumerable%601> 介面具有單一方法：<xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>。</span><span class="sxs-lookup"><span data-stu-id="954b2-184">The <xref:System.Collections.Generic.IEnumerable%601> interface has one method: <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>.</span></span> <span data-ttu-id="954b2-185"><xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 傳回的物件具有可移動到下一個元素的方法，以及可擷取目前序列中元素的屬性。</span><span class="sxs-lookup"><span data-stu-id="954b2-185">The object returned by <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> has a method to move to the next element, and a property that retrieves the current element in the sequence.</span></span> <span data-ttu-id="954b2-186">您將會使用那兩個成員來列舉集合並傳回元素。</span><span class="sxs-lookup"><span data-stu-id="954b2-186">You will use those two members to enumerate the collection and return the elements.</span></span> <span data-ttu-id="954b2-187">此交錯方法將會是迭代器方法，因此您將使用上述的 `yield return` 語法，而不是建置集合並傳回集合。</span><span class="sxs-lookup"><span data-stu-id="954b2-187">This Interleave method will be an iterator method, so instead of building a collection and returning the collection, you'll use the `yield return` syntax shown above.</span></span>

<span data-ttu-id="954b2-188">以下是該方法的實作：</span><span class="sxs-lookup"><span data-stu-id="954b2-188">Here's the implementation of that method:</span></span>

[!CODE-csharp[InterleaveSequenceWith](../../../samples/snippets/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

<span data-ttu-id="954b2-189">現在您已經撰寫了此方法，請回到 `Main` 方法，然後對牌堆洗牌一次：</span><span class="sxs-lookup"><span data-stu-id="954b2-189">Now that you've written this method, go back to the `Main` method and shuffle the deck once:</span></span>

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
    var shuffle = top.InterleaveSequenceWith(bottom);

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
```

## <a name="comparisons"></a><span data-ttu-id="954b2-190">比較</span><span class="sxs-lookup"><span data-stu-id="954b2-190">Comparisons</span></span>

<span data-ttu-id="954b2-191">需要洗牌多少次，才能將這副牌還原為其原始的順序？</span><span class="sxs-lookup"><span data-stu-id="954b2-191">How many shuffles it takes to set the deck back to its original order?</span></span> <span data-ttu-id="954b2-192">若要進行了解，您必須撰寫一個方法來判斷兩個序列是否相等。</span><span class="sxs-lookup"><span data-stu-id="954b2-192">To find out, you'll need to write a method that determines if two sequences are equal.</span></span> <span data-ttu-id="954b2-193">在您完成該方法後，您需要將洗牌的程式碼放入迴圈中，然後看看牌堆何時會回到原始順序。</span><span class="sxs-lookup"><span data-stu-id="954b2-193">After you have that method, you'll need to place the code that shuffles the deck in a loop, and check to see when the deck is back in order.</span></span>

<span data-ttu-id="954b2-194">撰寫判斷兩個序列是否相等的方法應該很單純。</span><span class="sxs-lookup"><span data-stu-id="954b2-194">Writing a method to determine if the two sequences are equal should be straightforward.</span></span> <span data-ttu-id="954b2-195">它的架構與您先前撰寫的洗牌方法類似。</span><span class="sxs-lookup"><span data-stu-id="954b2-195">It's a similar structure to the method you wrote to shuffle the deck.</span></span> <span data-ttu-id="954b2-196">只是這次不使用 `yield return` 每個元素，而是比較各序列的相符元素。</span><span class="sxs-lookup"><span data-stu-id="954b2-196">Only this time, instead of `yield return`ing each element, you'll compare the matching elements of each sequence.</span></span> <span data-ttu-id="954b2-197">當整個序列都已列舉後，如果每個元素都相符，則序列便為相同：</span><span class="sxs-lookup"><span data-stu-id="954b2-197">When the entire sequence has been enumerated, if every element matches, the sequences are the same:</span></span>

[!CODE-csharp[SequenceEquals](../../../samples/snippets/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

<span data-ttu-id="954b2-198">這裡示範第二個 LINQ 慣用語：終端方法。</span><span class="sxs-lookup"><span data-stu-id="954b2-198">This shows a second LINQ idiom: terminal methods.</span></span> <span data-ttu-id="954b2-199">它們會將序列 (在此範例中為兩個序列) 當作輸入，並傳回單一純量值。</span><span class="sxs-lookup"><span data-stu-id="954b2-199">They take a sequence as input (or in this case, two sequences), and return a single scalar value.</span></span> <span data-ttu-id="954b2-200">使用終端方法時，它們永遠都是適用於 LINQ 查詢之方法鏈結中的最終方法，因此有「終端」的名稱。</span><span class="sxs-lookup"><span data-stu-id="954b2-200">When using terminal methods, they are always the final method in a chain of methods for a LINQ query, hence the name "terminal".</span></span>

<span data-ttu-id="954b2-201">當您使用它來判斷牌堆何時回到原始順序時，便可以看到其作用。</span><span class="sxs-lookup"><span data-stu-id="954b2-201">You can see this in action when you use it to determine when the deck is back in its original order.</span></span> <span data-ttu-id="954b2-202">將洗牌程式碼放到迴圈中，並透過套用 `SequenceEquals()` 方法，來在序列回到原始順序時停止迴圈。</span><span class="sxs-lookup"><span data-stu-id="954b2-202">Put the shuffle code inside a loop, and stop when the sequence is back in its original order by applying the `SequenceEquals()` method.</span></span> <span data-ttu-id="954b2-203">您可以看到它在任何查詢中都一律是最終方法，因為它會傳回單一值而非序列：</span><span class="sxs-lookup"><span data-stu-id="954b2-203">You can see it would always be the final method in any query, because it returns a single value instead of a sequence:</span></span>

```csharp
// Program.cs
static void Main(string[] args)
{
    // Query for building the deck

    // Shuffling using InterleaveSequenceWith<T>();

    var times = 0;
    // We can re-use the shuffle variable from earlier, or you can make a new one
    shuffle = startingDeck;
    do
    {
        shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

        foreach (var card in shuffle)
        {
            Console.WriteLine(card);
        }
        Console.WriteLine();
        times++;

    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

<span data-ttu-id="954b2-204">執行您到目前為止所取得的程式碼，並記下這副牌在每次洗牌之後的重新排列方式。</span><span class="sxs-lookup"><span data-stu-id="954b2-204">Run the code you've got so far and take note of how the deck rearranges on each shuffle.</span></span> <span data-ttu-id="954b2-205">在 8 次洗牌 (反覆執行 do-while 迴圈) 之後，這副牌會回到您從開始 LINQ 查詢之後第一次建立它時它所處的原始設定。</span><span class="sxs-lookup"><span data-stu-id="954b2-205">After 8 shuffles (iterations of the do-while loop), the deck returns to the original configuration it was in when you first created it from the starting LINQ query.</span></span>

## <a name="optimizations"></a><span data-ttu-id="954b2-206">最佳化</span><span class="sxs-lookup"><span data-stu-id="954b2-206">Optimizations</span></span>

<span data-ttu-id="954b2-207">您目前建置的範例會執行「外部洗牌」\*\*，牌堆頂端和底部的紙牌，在每次執行時會保持不變。</span><span class="sxs-lookup"><span data-stu-id="954b2-207">The sample you've built so far executes an *out shuffle*, where the top and bottom cards stay the same on each run.</span></span> <span data-ttu-id="954b2-208">讓我們做個變化：我們將改用「內部洗牌」\*\*，這會變更全部 52 張牌的位置。</span><span class="sxs-lookup"><span data-stu-id="954b2-208">Let's make one change: we'll use an *in shuffle* instead, where all 52 cards change position.</span></span> <span data-ttu-id="954b2-209">對於內部洗牌而言，您要交錯牌堆，讓下半部的第一張紙牌變為牌堆的第一張紙牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-209">For an in shuffle, you interleave the deck so that the first card in the bottom half becomes the first card in the deck.</span></span> <span data-ttu-id="954b2-210">這表示上半部的最後一張紙牌會變為底部的排。</span><span class="sxs-lookup"><span data-stu-id="954b2-210">That means the last card in the top half becomes the bottom card.</span></span> <span data-ttu-id="954b2-211">這是對單行程式碼的簡單變更。</span><span class="sxs-lookup"><span data-stu-id="954b2-211">This is a simple change to a singular line of code.</span></span> <span data-ttu-id="954b2-212">藉由切換 <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 的位置來更新目前的洗牌查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-212">Update the current shuffle query by switching the positions of <xref:System.Linq.Enumerable.Take%2A> and <xref:System.Linq.Enumerable.Skip%2A>.</span></span> <span data-ttu-id="954b2-213">這將會變更這副牌上下半部的順序：</span><span class="sxs-lookup"><span data-stu-id="954b2-213">This will change the order of the top and bottom halves of the deck:</span></span>

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

<span data-ttu-id="954b2-214">再次執行程式，您將會看到需要反覆運算 52 次，才能使牌堆重新排列回原始順序。</span><span class="sxs-lookup"><span data-stu-id="954b2-214">Run the program again, and you'll see that it takes 52 iterations for the deck to reorder itself.</span></span> <span data-ttu-id="954b2-215">隨著程式持續執行，您也會開始注意到一些效能嚴重降低的情況。</span><span class="sxs-lookup"><span data-stu-id="954b2-215">You'll also start to notice some serious performance degradations as the program continues to run.</span></span>

<span data-ttu-id="954b2-216">這有幾個原因。</span><span class="sxs-lookup"><span data-stu-id="954b2-216">There are a number of reasons for this.</span></span> <span data-ttu-id="954b2-217">您可以處理導致這個效能降低的其中一個主要原因：無法有效使用[延遲評估\*\*](../../standard/linq/deferred-execution-lazy-evaluation.md)。</span><span class="sxs-lookup"><span data-stu-id="954b2-217">You can tackle one of the major causes of this performance drop: inefficient use of [*lazy evaluation*](../../standard/linq/deferred-execution-lazy-evaluation.md).</span></span>

<span data-ttu-id="954b2-218">簡單來說，延遲評估表示，在需要陳述式的值之前不會執行該陳述式的評估。</span><span class="sxs-lookup"><span data-stu-id="954b2-218">Briefly, lazy evaluation states that the evaluation of a statement is not performed until its value is needed.</span></span> <span data-ttu-id="954b2-219">LINQ 查詢是以延遲方式評估的陳述式。</span><span class="sxs-lookup"><span data-stu-id="954b2-219">LINQ queries are statements that are evaluated lazily.</span></span> <span data-ttu-id="954b2-220">序列只會隨著要求元素產生。</span><span class="sxs-lookup"><span data-stu-id="954b2-220">The sequences are generated only as the elements are requested.</span></span> <span data-ttu-id="954b2-221">通常，這是 LINQ 的主要優點。</span><span class="sxs-lookup"><span data-stu-id="954b2-221">Usually, that's a major benefit of LINQ.</span></span> <span data-ttu-id="954b2-222">不過，在使用如範例中的程式時，這會導致執行時間呈指數成長。</span><span class="sxs-lookup"><span data-stu-id="954b2-222">However, in a use such as this program, this causes exponential growth in execution time.</span></span>

<span data-ttu-id="954b2-223">請記住，我們使用了 LINQ 查詢來產生這副原始的牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-223">Remember that we generated the original deck using a LINQ query.</span></span> <span data-ttu-id="954b2-224">每次洗牌都是透過對之前的牌堆執行三個 LINQ 查詢來產生。</span><span class="sxs-lookup"><span data-stu-id="954b2-224">Each shuffle is generated by performing three LINQ queries on the previous deck.</span></span> <span data-ttu-id="954b2-225">這些都是以延遲方式執行。</span><span class="sxs-lookup"><span data-stu-id="954b2-225">All these are performed lazily.</span></span> <span data-ttu-id="954b2-226">這也表示每次要求序列時，它們都會再次執行。</span><span class="sxs-lookup"><span data-stu-id="954b2-226">That also means they are performed again each time the sequence is requested.</span></span> <span data-ttu-id="954b2-227">當您達到第 52 次反覆運算時，您會非常多次地重複產生原始牌堆。</span><span class="sxs-lookup"><span data-stu-id="954b2-227">By the time you get to the 52nd iteration, you're regenerating the original deck many, many times.</span></span> <span data-ttu-id="954b2-228">讓我們撰寫記錄以示範這個行為。</span><span class="sxs-lookup"><span data-stu-id="954b2-228">Let's write a log to demonstrate this behavior.</span></span> <span data-ttu-id="954b2-229">接著，您將會修正它。</span><span class="sxs-lookup"><span data-stu-id="954b2-229">Then, you'll fix it.</span></span>

<span data-ttu-id="954b2-230">在您的 `Extensions.cs` 檔案中，輸入或複製下列方法。</span><span class="sxs-lookup"><span data-stu-id="954b2-230">In your `Extensions.cs` file, type in or copy the method below.</span></span> <span data-ttu-id="954b2-231">這個擴充方法會在您的專案目錄內建立稱為 `debug.log` 的新檔案，並記錄目前正在對記錄檔執行哪一個查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-231">This extension method creates a new file called `debug.log` within your project directory and records what query is currently being executed to the log file.</span></span> <span data-ttu-id="954b2-232">此擴充方法可附加到任何查詢，以標示查詢所執行的內容。</span><span class="sxs-lookup"><span data-stu-id="954b2-232">This extension method can be appended to any query to mark that the query executed.</span></span>

[!CODE-csharp[LogQuery](../../../samples/snippets/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

<span data-ttu-id="954b2-233">您會在 `File` 下看到紅色波浪線，表示它不存在。</span><span class="sxs-lookup"><span data-stu-id="954b2-233">You will see a red squiggle under `File`, meaning it doesn't exist.</span></span> <span data-ttu-id="954b2-234">它不會編譯，原因是編譯器不知道 `File` 是什麼。</span><span class="sxs-lookup"><span data-stu-id="954b2-234">It won't compile, since the compiler doesn't know what `File` is.</span></span> <span data-ttu-id="954b2-235">若要解決這個問題，請務必將下列這一行程式碼新增至 `Extensions.cs` 的第一行下：</span><span class="sxs-lookup"><span data-stu-id="954b2-235">To solve this problem, make sure to add the following line of code under the very first line in `Extensions.cs`:</span></span>

```csharp
using System.IO;
```

<span data-ttu-id="954b2-236">這應可解決此問題，讓紅色的錯誤消失。</span><span class="sxs-lookup"><span data-stu-id="954b2-236">This should solve the issue and the red error disappears.</span></span>

<span data-ttu-id="954b2-237">接下來，使用記錄訊息檢測每個查詢的定義：</span><span class="sxs-lookup"><span data-stu-id="954b2-237">Next, instrument the definition of each query with a log message:</span></span>

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                        from r in Ranks().LogQuery("Rank Generation")
                        select new { Suit = s, Rank = r }).LogQuery("Starting Deck");

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;

    do
    {
        // Out shuffle
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        // In shuffle
        shuffle = shuffle.Skip(26).LogQuery("Bottom Half")
                .InterleaveSequenceWith(shuffle.Take(26).LogQuery("Top Half"))
                .LogQuery("Shuffle");

        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }

        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

<span data-ttu-id="954b2-238">請注意，您不用在每次存取查詢時進行記錄。</span><span class="sxs-lookup"><span data-stu-id="954b2-238">Notice that you don't log every time you access a query.</span></span> <span data-ttu-id="954b2-239">您只需要在建立原始查詢時做出記錄。</span><span class="sxs-lookup"><span data-stu-id="954b2-239">You log only when you create the original query.</span></span> <span data-ttu-id="954b2-240">程式仍然會花費很長的時間執行，但現在您可以看到原因。</span><span class="sxs-lookup"><span data-stu-id="954b2-240">The program still takes a long time to run, but now you can see why.</span></span> <span data-ttu-id="954b2-241">如果您在執行開啟記錄的內部洗牌期間失去耐心，請切換回外部洗牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-241">If you run out of patience running the in shuffle with logging turned on, switch back to the out shuffle.</span></span> <span data-ttu-id="954b2-242">您仍然會看到延遲評估的效果。</span><span class="sxs-lookup"><span data-stu-id="954b2-242">You'll still see the lazy evaluation effects.</span></span> <span data-ttu-id="954b2-243">在單次執行中，它會執行 2592 次查詢，其中包括所有值和花色的產生。</span><span class="sxs-lookup"><span data-stu-id="954b2-243">In one run, it executes 2592 queries, including all the value and suit generation.</span></span>

<span data-ttu-id="954b2-244">您可以在此處改善程式碼的效能，以減少您所進行的執行次數。</span><span class="sxs-lookup"><span data-stu-id="954b2-244">You can improve the performance of the code here to reduce the number of executions you make.</span></span> <span data-ttu-id="954b2-245">您可進行的簡單修正是「快取」\*\* 建構這副牌的原始 LINQ 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="954b2-245">A simple fix you can make is to *cache* the results of the original LINQ query that constructs the deck of cards.</span></span> <span data-ttu-id="954b2-246">目前，您會在每次 do-while 迴圈經歷反覆執行時一再地執行查詢、重新建構這副牌，而且每次都會對它進行重新洗牌。</span><span class="sxs-lookup"><span data-stu-id="954b2-246">Currently, you're executing the queries again and again every time the do-while loop goes through an iteration, re-constructing the deck of cards and reshuffling it every time.</span></span> <span data-ttu-id="954b2-247">若要快取這副牌，您可以利用 LINQ 方法 <xref:System.Linq.Enumerable.ToArray%2A> 和 <xref:System.Linq.Enumerable.ToList%2A>；當您將它們附加至查詢時，它們將執行您已告訴它們的相同動作，但現在它們會根據您選擇呼叫的方法，將結果儲存在陣列或清單中。</span><span class="sxs-lookup"><span data-stu-id="954b2-247">To cache the deck of cards, you can leverage the LINQ methods <xref:System.Linq.Enumerable.ToArray%2A> and <xref:System.Linq.Enumerable.ToList%2A>; when you append them to the queries, they'll perform the same actions you've told them to, but now they'll store the results in an array or a list, depending on which method you choose to call.</span></span> <span data-ttu-id="954b2-248">將 LINQ 方法 <xref:System.Linq.Enumerable.ToArray%2A> 附加至這兩個查詢，然後再次執行程式：</span><span class="sxs-lookup"><span data-stu-id="954b2-248">Append the LINQ method <xref:System.Linq.Enumerable.ToArray%2A> to both queries and run the program again:</span></span>

[!CODE-csharp[Main](../../../samples/snippets/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

<span data-ttu-id="954b2-249">現在，已將外部洗牌減少至 30 個查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-249">Now the out shuffle is down to 30 queries.</span></span> <span data-ttu-id="954b2-250">搭配內部洗牌再次執行，您將會看到類似的改善：它現在會執行 162 個查詢。</span><span class="sxs-lookup"><span data-stu-id="954b2-250">Run again with the in shuffle and you'll see similar improvements: it now executes 162 queries.</span></span>

<span data-ttu-id="954b2-251">請注意這個範例的**設計**，用意在於凸顯因延遲執行而造成效能問題的使用案例。</span><span class="sxs-lookup"><span data-stu-id="954b2-251">Please note that this example is **designed** to highlight the use cases where lazy evaluation can cause performance difficulties.</span></span> <span data-ttu-id="954b2-252">儘管查看延遲評估可能會影響程式碼效能的位置很重要，但了解並非所有查詢都應立即執行也很重要。</span><span class="sxs-lookup"><span data-stu-id="954b2-252">While it's important to see where lazy evaluation can impact code performance, it's equally important to understand that not all queries should run eagerly.</span></span> <span data-ttu-id="954b2-253">您在不使用 <xref:System.Linq.Enumerable.ToArray%2A> 的情況下所遇到的效能影響，是因為對於這副牌的每個排列都是從前一個排列建置的。</span><span class="sxs-lookup"><span data-stu-id="954b2-253">The performance hit you incur without using <xref:System.Linq.Enumerable.ToArray%2A> is because each new arrangement of the deck of cards is built from the previous arrangement.</span></span> <span data-ttu-id="954b2-254">使用延遲評估表示每個新的牌堆設定都是從原始牌堆建立，甚至會執行建置 `startingDeck` 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="954b2-254">Using lazy evaluation means each new deck configuration is built from the original deck, even executing the code that built the `startingDeck`.</span></span> <span data-ttu-id="954b2-255">這會導致大量的額外工作。</span><span class="sxs-lookup"><span data-stu-id="954b2-255">That causes a large amount of extra work.</span></span>

<span data-ttu-id="954b2-256">實際上，某些演算法適合使用立即評估來執行，而其他演算法則適合使用延遲評估來執行。</span><span class="sxs-lookup"><span data-stu-id="954b2-256">In practice, some algorithms run well using eager evaluation, and others run well using lazy evaluation.</span></span> <span data-ttu-id="954b2-257">針對每日使用方式，當資料來源為獨立程序 (例如資料庫引擎) 時，通常比較適合選擇延遲評估。</span><span class="sxs-lookup"><span data-stu-id="954b2-257">For daily usage, lazy evaluation is usually a better choice when the data source is a separate process, like a database engine.</span></span> <span data-ttu-id="954b2-258">針對資料庫，延遲評估讓更複雜的查詢僅針對資料庫程序執行單次來回行程，並返回您程式碼的剩餘部分。</span><span class="sxs-lookup"><span data-stu-id="954b2-258">For databases, lazy evaluation allows more complex queries to execute only one round trip to the database process and back to the rest of your code.</span></span> <span data-ttu-id="954b2-259">無論您選擇利用延遲或立即評估，LINQ 都極具彈性，因此，請測量您的程序，並挑選可為您提供最佳效能的評估種類。</span><span class="sxs-lookup"><span data-stu-id="954b2-259">LINQ is flexible whether you choose to utilize lazy or eager evaluation, so measure your processes and pick whichever kind of evaluation gives you the best performance.</span></span>

## <a name="conclusion"></a><span data-ttu-id="954b2-260">結論</span><span class="sxs-lookup"><span data-stu-id="954b2-260">Conclusion</span></span>

<span data-ttu-id="954b2-261">在此專案中，您已涵蓋：</span><span class="sxs-lookup"><span data-stu-id="954b2-261">In this project, you covered:</span></span>

- <span data-ttu-id="954b2-262">使用 LINQ 查詢來將資料彙總到有意義的序列</span><span class="sxs-lookup"><span data-stu-id="954b2-262">using LINQ queries to aggregate data into a meaningful sequence</span></span>
- <span data-ttu-id="954b2-263">撰寫擴充方法，將自己的自訂功能新增到 LINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="954b2-263">writing Extension methods to add our own custom functionality to LINQ queries</span></span>
- <span data-ttu-id="954b2-264">在程式碼中尋找 LINQ 查詢可能遇到效能問題 (例如降低速度) 的區域</span><span class="sxs-lookup"><span data-stu-id="954b2-264">locating areas in our code where our LINQ queries might run into performance issues like degraded speed</span></span>
- <span data-ttu-id="954b2-265">有關 LINQ 查詢的延遲和立即評估，以及它們可能對查詢效能產生的影響</span><span class="sxs-lookup"><span data-stu-id="954b2-265">lazy and eager evaluation in regards to LINQ queries and the implications they might have on query performance</span></span>

<span data-ttu-id="954b2-266">除了 LINQ，您還了解到魔術師使用撲克牌的技巧。</span><span class="sxs-lookup"><span data-stu-id="954b2-266">Aside from LINQ, you learned a bit about a technique magicians use for card tricks.</span></span> <span data-ttu-id="954b2-267">魔術師之所以使用完美洗牌，是因為他們可以控制每張牌在牌堆中的動向。</span><span class="sxs-lookup"><span data-stu-id="954b2-267">Magicians use the Faro shuffle because they can control where every card moves in the deck.</span></span> <span data-ttu-id="954b2-268">既然您已經知道，就不要為其他人破壞了它！</span><span class="sxs-lookup"><span data-stu-id="954b2-268">Now that you know, don't spoil it for everyone else!</span></span>

<span data-ttu-id="954b2-269">如需有關 LINQ 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="954b2-269">For more information on LINQ, see:</span></span>

- [<span data-ttu-id="954b2-270">Language Integrated Query (LINQ)</span><span class="sxs-lookup"><span data-stu-id="954b2-270">Language Integrated Query (LINQ)</span></span>](../programming-guide/concepts/linq/index.md)
- [<span data-ttu-id="954b2-271">LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="954b2-271">Introduction to LINQ</span></span>](../programming-guide/concepts/linq/index.md)
- [<span data-ttu-id="954b2-272">基本 LINQ 查詢作業 (C#)</span><span class="sxs-lookup"><span data-stu-id="954b2-272">Basic LINQ Query Operations (C#)</span></span>](../programming-guide/concepts/linq/basic-linq-query-operations.md)
- [<span data-ttu-id="954b2-273">使用 LINQ (c # ) 的資料轉換 </span><span class="sxs-lookup"><span data-stu-id="954b2-273">Data Transformations With LINQ (C#)</span></span>](../programming-guide/concepts/linq/data-transformations-with-linq.md)
- [<span data-ttu-id="954b2-274">LINQ 中的查詢語法及方法語法 (C#)</span><span class="sxs-lookup"><span data-stu-id="954b2-274">Query Syntax and Method Syntax in LINQ (C#)</span></span>](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)
- [<span data-ttu-id="954b2-275">支援 LINQ 的 C# 功能</span><span class="sxs-lookup"><span data-stu-id="954b2-275">C# Features That Support LINQ</span></span>](../programming-guide/concepts/linq/features-that-support-linq.md)

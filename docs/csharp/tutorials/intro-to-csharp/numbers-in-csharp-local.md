---
title: C# 中的數字 - C# 教學課程簡介
description: '藉由探索數位類型、其使用方式、屬性和方法來學習 c #。'
ms.date: 10/31/2017
ms.custom: mvc
ms.openlocfilehash: 3dc2a5afc6321da45351525a632f586cb84bf7fe
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794607"
---
# <a name="manipulate-integral-and-floating-point-numbers-in-c"></a>在 C\# 中操作整數和浮點數數字

此教學課程會以互動方式教導您有關 C# 中的數字型別。 您將會撰寫少量程式碼，然後編譯並執行該程式碼。 教學課程包含一系列探索 C# 中數字和數學運算的課程。 這些課程會教導您 C# 語言的基本概念。

此教學課程要求您必須有可用於開發的電腦。 .NET 教學課程[Hello World 在10分鐘內](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)，有在 Windows、Linux 或 macOS 上設定本機開發環境的指示。 您可以在[熟悉開發工具](local-environment.md)中快速檢視將會用到的命令，並取得可提供詳細資料的連結。

## <a name="explore-integer-math"></a>探索整數運算

建立名為 *numbers-quickstart* 的目錄。 將它設為目前的目錄，然後執行下列命令：

```dotnetcli
dotnet new console -n NumbersInCSharp -o .
```

在您最愛的編輯器中開啟 *Program.cs*，並以下列程式碼取代 `Console.WriteLine("Hello World!");` 程式碼行：

```csharp
int a = 18;
int b = 6;
int c = a + b;
Console.WriteLine(c);
```

在命令視窗中輸入 `dotnet run` 來執行此程式碼。

您已經看過其中一個具有整數的基本數學運算。 `int`類型代表**整數**、零、正數或負整數。 您使用 `+` 符號來執行加法。 整數常用的其他數學運算包括：

- `-` 用於減法
- `*` 用於乘法
- `/` 用於除法

讓我們開始探索這些不同的運算。 將下列程式碼行新增至撰寫 `c` 值的程式碼行後方：

```csharp

// subtraction
c = a - b;
Console.WriteLine(c);

// multiplication
c = a * b;
Console.WriteLine(c);

// division
c = a / b;
Console.WriteLine(c);
```

在命令視窗中輸入 `dotnet run` 來執行此程式碼。

如果您想要的話，也可以在同一行中撰寫多個數學運算來進行實驗。 嘗試使用 `c = a + b - 12 * 17;` 作為範例。 允許混合變數和常數數字。

> [!TIP]
> 在您探索 C# (或任何程式設計語言) 時，可能會在撰寫程式碼時犯錯。 **編譯器**會找出那些錯誤並回報給您。 當輸出包含錯誤訊息時，請仔細查看範例程式碼及視窗中的程式碼，看看有哪些可以修正。
> 該練習將有助於您了解 C# 程式碼的結構。

您已完成第一個步驟。 在開始下一節之前，讓我們將目前的程式碼移到另一個個別的方法。 這可讓您更輕鬆地開始處理新的範例。 將 `Main` 方法重新命名為 `WorkingWithIntegers`，然後撰寫會呼叫 `WorkingWithIntegers` 的新 `Main` 方法。 當您完成時，您的程式碼看起來應該像這樣：

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();
        }
    }
}
```

## <a name="explore-order-of-operations"></a>探索運算的順序

將針對 `WorkingWithIntegers()` 的呼叫註解化。 這會在您處理本節的內容時，使輸出變得較為整齊：

```csharp
//WorkingWithIntegers();
```

`//` 會在 C# 中起始一段**註解**。 註解是您想保留在原始程式碼中，但不想要作為程式碼執行的任何文字。 編譯器不會從批註產生任何可執行檔程式碼。

針對不同數學運算的優先順序，C# 語言所定義的規則與您在數學所學的規則一致。
乘法和除法的優先順序高於加法和減法。
將下列程式碼新增至 `Main` 方法，並執行 `dotnet run` 來探索：

```csharp
int a = 5;
int b = 4;
int c = 2;
int d = a + b * c;
Console.WriteLine(d);
 ```

輸出示範了程式會先執行乘法，然後再執行加法。

您可以在想要優先執行的一個或多個運算前後加上括號，以強制執行不同的運算順序。 新增下列程式碼行並再次執行：

```csharp
d = (a + b) * c;
Console.WriteLine(d);
```

結合許多不同的運算來深入探索。 在 `Main` 方法的底部新增類似下列程式碼行的內容。 再次嘗試執行 `dotnet run`。

```csharp
d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
Console.WriteLine(d);
```

您可能已注意到整數某個有趣的行為。 整數的除法一律會產生整數結果，即使您認為結果應有小數或分數部分也一樣。

如果您沒有看到此行為，請在 `Main` 方法的末端嘗試下列程式碼：

```csharp
int e = 7;
int f = 4;
int g = 3;
int h = (e + f) / g;
Console.WriteLine(h);
```

再次輸入 `dotnet run` 來查看結果。

在繼續後續內容之前，讓我們將您在本節中所撰寫的所有程式碼置於新的方法中。 將新方法命名為 `OrderPrecedence`。
您應該撰寫如下的內容：

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void OrderPrecedence()
        {
            int a = 5;
            int b = 4;
            int c = 2;
            int d = a + b * c;
            Console.WriteLine(d);

            d = (a + b) * c;
            Console.WriteLine(d);

            d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
            Console.WriteLine(d);

            int e = 7;
            int f = 4;
            int g = 3;
            int h = (e  + f) / g;
            Console.WriteLine(h);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();

            OrderPrecedence();

        }
    }
}
```

## <a name="explore-integer-precision-and-limits"></a>探索整數的精確度與限制

上一個範例示範了整數除法運算會將結果截斷。
您可以使用**模數**運算子 (`%` 字元) 來取得**餘數**。 在 `Main` 方法中嘗試下列程式碼：

```csharp
int a = 7;
int b = 4;
int c = 3;
int d = (a + b) / c;
int e = (a + b) % c;
Console.WriteLine($"quotient: {d}");
Console.WriteLine($"remainder: {e}");
```

C# 整數型別有一個地方與數學上的整數不同：`int` 型別有最小和最大限制。 將下列程式碼新增至 `Main` 方法以查看那些限制：

```csharp
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine($"The range of integers is {min} to {max}");
```

如果計算產生的值超出這些限制，就會發生**反向溢位**或**溢位**的情況。 答案看起來會是從其中一個限制回繞至另一個限制。 將下列兩行新增至 `Main` 方法以查看範例：

```csharp
int what = max + 3;
Console.WriteLine($"An example of overflow: {what}");
```

請注意，答案非常接近最小 (負) 整數。 這與 `min + 2` 相同。
此加法運算已**溢出**整數允許的值。
此答案是非常大的負數，這是因為溢位會從最大整數值「回繞」至最小整數值。

當 `int` 型別不符合您的需求時，還有其他具有不同限制和精確度的數字型別可供使用。 接下來讓我們來探索這些其他類型。

同樣地，讓我們將您在本節中所撰寫的程式碼置於個別的方法中。 將它命名為 `TestLimits`

## <a name="work-with-the-double-type"></a>使用 Double 型別

`double` 數字型別代表雙精確度浮點數。 您可能不熟悉這些字詞。 **浮點**數位非常適合用來代表可能非常大或非常小的非整數數位。 **雙精確度**是一個相對詞彙，描述用來儲存值的二進位數位數目。 **雙精確度**數位的二進位位數數目為**單精確度**的兩倍。 在新式電腦上，使用雙精確度比單精確度數位更常見。 使用`float`關鍵字來宣告**單精確度**數位。
讓我們開始探索吧。 新增下列程式碼並查看結果：

```csharp
double a = 5;
double b = 4;
double c = 2;
double d = (a + b) / c;
Console.WriteLine(d);
```

請注意答案包括商數的小數部分。 請嘗試略為複雜的雙精確度浮點數運算式：

```csharp
double e = 19;
double f = 23;
double g = 8;
double h = (e + f) / g;
Console.WriteLine(h);
```

雙精確度浮點數值的範圍遠大於整數值。 在您目前已撰寫的程式碼下方嘗試下列程式碼：

```csharp
double max = double.MaxValue;
double min = double.MinValue;
Console.WriteLine($"The range of double is {min} to {max}");
```

這些值會以科學記號標記法呈現。 `E` 左邊的數字是有效數字。 右邊的數字則為指數，亦即 10 的次方。

就像數學上的小數數字，C# 中的雙精確度浮點數會發生捨入誤差。 請嘗試此程式碼：

```csharp
double third = 1.0 / 3.0;
Console.WriteLine(third);
```

您知道`0.3`重複的並不完全相同`1/3`。

***挑戰***

嘗試使用`double`類型的大量、小型數位、乘法和除法的其他計算。 嘗試更複雜的計算。

在嘗試完成挑戰之後，請將您所撰寫的程式碼置於新的方法中。 將新方法命名為 `WorkWithDoubles`。

## <a name="work-with-decimal-types"></a>使用十進位類型

您已經看過 C# 中的基本數字型別：整數和雙精確度浮點數。  還有另一個要瞭解的`decimal`型別：型別。 `decimal` 類型的範圍較小，但精確度較 `double` 來得高。 讓我們來看一下：

```csharp
decimal min = decimal.MinValue;
decimal max = decimal.MaxValue;
Console.WriteLine($"The range of the decimal type is {min} to {max}");
```

請注意該範圍小於 `double` 型別。 透過嘗試下列程式碼，您可以看到 decimal (小數) 型別有較高的精確度：

```csharp
double a = 1.0;
double b = 3.0;
Console.WriteLine(a / b);

decimal c = 1.0M;
decimal d = 3.0M;
Console.WriteLine(c / d);
```

數字上的 `M` 尾碼乃是指示常數應使用 `decimal` 型別。 否則，編譯器會假設`double`型別。

> [!NOTE]
> 在`M` `double`和`decimal`關鍵字之間，選擇了字母做為最具視覺效果的相異字母。

請注意，使用 decimal (小數) 型別的運算在小數點右邊會有更多的數字。

***挑戰***

您已經了解不同的數字型別，接著請撰寫程式碼，以計算半徑 2.50 公分的圓形面積。 提醒您圓形面積是 PI 乘以半徑的平方。 提示：.NET 包含 PI 的常數：<xref:System.Math.PI?displayProperty=nameWithType>，可用來作為該值。 <xref:System.Math.PI?displayProperty=nameWithType>與`System.Math`命名空間中宣告的所有常數一樣，都`double`是一個值。 基於這個理由，您應該使用`double`而不`decimal`是這項挑戰的值。

您應該會取得介於 19 和 20 的答案。
您可以[查看 GitHub 上已完成的範例程式碼](https://github.com/dotnet/samples/tree/master/csharp/numbers-quickstart/Program.cs#L104-L106)來檢查您的答案。

如果您想要的話，可以嘗試其他公式。

您已完成＜C# 中的數字＞快速入門。 您可以在自己的開發環境中，繼續完成[分支和迴圈](branches-and-loops-local.md)快速入門中的內容。

您可以在下列文章中深入瞭解 c # 中的數位：

- [整數數值類型](../../language-reference/builtin-types/integral-numeric-types.md)
- [浮點數值類型](../../language-reference/builtin-types/floating-point-numeric-types.md)
- [內建數值轉換](../../language-reference/builtin-types/numeric-conversions.md)

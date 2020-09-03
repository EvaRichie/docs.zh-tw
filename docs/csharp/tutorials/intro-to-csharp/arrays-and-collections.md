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
# <a name="learn-to-manage-data-collections-using-the-generic-list-type"></a>了解如何使用一般清單類型管理資料收集

此入門教學課程提供 C# 語言的簡介，以及 <xref:System.Collections.Generic.List%601> 類別的基礎知識。

此教學課程要求您必須有可用於開發的電腦。 .NET 教學課程 [Hello World 10 分鐘內](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) 的指示，說明如何在 Windows、Linux 或 macOS 上設定您的本機開發環境。 您可以在[熟悉開發工具](local-environment.md)中快速檢視將會用到的命令，並取得可提供詳細資料的連結。

## <a name="a-basic-list-example"></a>基本的清單範例

建立名為 *list-tutorial* 的目錄。 將該目錄設為目前的目錄，並執行 `dotnet new console`。

在您最愛的編輯器中開啟 *Program.cs*，並以下列內容取代現有的程式碼：

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

以您的名稱取代 `<name>`。 儲存 *Program.cs*。 在主控台視窗中輸入 `dotnet run` 來嘗試它。

您已建立字串清單，在該清單中新增三個名稱，並以全部大寫的形式列印出那些名稱。 您會使用從先前教學課程中學習到的概念，在清單中執行迴圈。

顯示名稱的程式碼會運用[字串內插補點](../../language-reference/tokens/interpolated.md)功能。  當您在 `string` 的前方放置 `$` 時，您可以在字串宣告中內嵌 C# 程式碼。 實際的字串會以它所產生的值取代 C# 程式碼。 在此範例中，它會以每個 (轉換成大寫字母的) 名稱取代 `{name.ToUpper()}`，因為您呼叫了 <xref:System.String.ToUpper%2A> 方法。

讓我們繼續探索。

## <a name="modify-list-contents"></a>修改清單內容

您所建立的集合會使用 <xref:System.Collections.Generic.List%601> 類型。 此類型會儲存元素的序列。 您會在角括弧之間指定元素的類型。

此 <xref:System.Collections.Generic.List%601> 類型的其中一個重要層面，在於它可以擴張或縮小，使您可以新增或移除元素。 在 `Main` 方法中關閉 `}` 之前，新增下列程式碼：

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

您已在清單末端新增兩個額外的名稱。 您也移除了一個名稱。 儲存檔案，並輸入 `dotnet run` 來嘗試它。

<xref:System.Collections.Generic.List%601> 也可讓您透過**索引**參考個別的項目。 您需將索引放在 `[` 和 `]` 語彙基元之間，位於清單名稱之後。 C# 使用 0 作為第一個索引。 將下列程式碼新增至您剛才新增的程式碼下方，然後嘗試它：

```csharp
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

您無法存取清單結尾以外的索引。 請記住，索引是從 0 開始，因此最大的有效索引數目為清單項目數目減去 1。 您可以使用 <xref:System.Collections.Generic.List%601.Count%2A> 屬性檢查清單的長度。 在 Main 方法的結尾，加入下列程式碼：

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
 ```

儲存檔案，然後再次輸入 `dotnet run` 以查看結果。

## <a name="search-and-sort-lists"></a>針對清單進行搜尋和排序

我們的範例所使用的清單相對較小，但是您的應用程式可能經常會建立具有更多元素的清單，數量甚至會達數千個之多。 若要在這些較大的集合中尋找元素，您需要在清單中搜尋不同的項目。 <xref:System.Collections.Generic.List%601.IndexOf%2A> 方法會搜尋項目，並傳回該項目的索引。 如果專案不在清單中，則 `IndexOf` 傳回 `-1` 。 將下列程式碼新增到 `Main` 方法的底部：

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

也可以對您清單中的項目進行排序。 <xref:System.Collections.Generic.List%601.Sort%2A>方法會依標準順序排序清單中的所有專案， (以字母順序排序字串) 。 將下列程式碼新增到 `Main` 方法的底部：

```csharp
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

儲存檔案並輸入 `dotnet run` 以嘗試此最新版本。

在開始下一節之前，讓我們將目前的程式碼移到另一個個別的方法。 這可讓您更輕鬆地開始處理新的範例。 將 `Main` 方法重新命名為 `WorkingWithStrings`，然後撰寫會呼叫 `WorkingWithStrings` 的新 `Main` 方法。 當您完成時，您的程式碼看起來應該像這樣：

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

## <a name="lists-of-other-types"></a>其他類型的清單

到目前為止，您都是使用清單中的 `string` 類型。 讓我們使用不同的類型建立 <xref:System.Collections.Generic.List%601>。 讓我們來建置一組數字。

將下列內容新增到新 `Main` 方法的底部：

```csharp
var fibonacciNumbers = new List<int> {1, 1};
```

這將會建立整數清單，並將前兩個整數設定為 1 的值。 這是*費氏數列*的前兩個值。 這兩個值之後每個費式數列數字，都會是其前兩個數字的總和。 新增下列程式碼：

```csharp
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach (var item in fibonacciNumbers)
    Console.WriteLine(item);
```

儲存檔案並輸入 `dotnet run` 來查看結果。

> [!TIP]
> 若要僅專注於本節的內容，您可以對呼叫 `WorkingWithStrings();` 的程式碼進行註解化。 請在該呼叫之前放置兩個 `/` 字元，例如：`// WorkingWithStrings();`。

## <a name="challenge"></a>挑戰

看看您是否可以結合運用來自此課程和先前課程的概念。 請依費式數列數字，擴展您到目前為止所建立的內容。 請嘗試將程式碼撰寫成可產生該數列的前 20 個數字。 (小提示：第 20 個費式數列數字為 6765)。

## <a name="complete-challenge"></a>完成挑戰

您可以查看 [GitHub 上已完成的範例程式碼](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23)，以查看範例解決方案。

在迴圈每次反覆運算時，您都必須取清單中的最後兩個整數，將它們加總，並將該值新增至清單。 迴圈會持續重複，直到將 20 個項目新增至清單為止。

恭喜，您已完成清單的教學課程。 您可以在自己的開發環境中，繼續完成[類別簡介](introduction-to-classes.md)教學課程中的內容。

您可以在 .NET 基礎檔的集合中深入瞭解如何使用此 `List` 類型[collections](../../../standard/collections/index.md)。 您也能學習到許多其他的集合類型。

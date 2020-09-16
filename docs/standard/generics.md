---
title: 泛型型別 (泛型) 概觀
description: 了解泛型如何作為程式碼範本，讓您定義型別安全資料結構，而不需要認可至實際資料類型。
author: kuhlenh
ms.author: wiwagn
ms.date: 10/09/2018
ms.openlocfilehash: 5f6e84e23b5bcdcb3dcd742823d83728fb43d195
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557940"
---
# <a name="generic-types-overview"></a>泛型型別概觀

開發人員經常會在 .NET 中使用泛型，不論是隱含使用或明確使用。 當您在 .NET 中使用 LINQ 時，您是否曾注意到您正在使用 <xref:System.Collections.Generic.IEnumerable%601>？ 或者，如果您看到「一般存放庫」的線上範例使用 Entity Framework 來與資料庫交談，您是否看到大部分的方法都會傳回 `IQueryable<T>` ？ 您可能想知道這些範例中的 **T** 為何，以及它出現在這裡的原因。

在 .NET Framework 2.0 中首次引進，泛型基本上是「程式碼範本」，可讓開發人員定義[型別安全](/previous-versions/dotnet/netframework-4.0/hbzz1a9a(v=vs.100))資料結構，而不需要認可至實際資料類型。 例如， <xref:System.Collections.Generic.List%601> 是一個 [泛型集合](xref:System.Collections.Generic) ，可以使用任何型別（例如、或）來宣告和使用 `List<int>` `List<string>` `List<Person>` 。

若要了解為什麼泛型十分實用，讓我們看看加入泛型前後的特定類別：<xref:System.Collections.ArrayList>。 在 .NET Framework 1.0 中，`ArrayList` 元素的型別為 <xref:System.Object>。 加入至集合的任何元素都會以無訊息模式轉換成 `Object` 。 從清單中讀取專案時，也會發生相同的情況。 此程序稱為 [Boxing 和 Unboxing](../csharp/programming-guide/types/boxing-and-unboxing.md)，它會影響效能。 不過除了效能之外，在編譯時期並沒有任何方法可以判斷清單中的資料類型，這會產生一些脆弱的程式碼。 泛型可以透過定義每個清單執行個體將包含之資料的型別解決這個問題。 例如，您只能將整數加入 `List<int>`，以及只能將 Persons 加入 `List<Person>`。

泛型也可在執行時間使用。 執行時間知道您所使用的資料結構類型，而且可以更有效率地將它儲存在記憶體中。

下列範例是一個小程式，說明在執行時間瞭解資料結構類型的效率：

```csharp
  using System;
  using System.Collections;
  using System.Collections.Generic;
  using System.Diagnostics;

  namespace GenericsExample {
    class Program {
      static void Main(string[] args) {
        //generic list
        List<int> ListGeneric = new List<int> { 5, 9, 1, 4 };
        //non-generic list
        ArrayList ListNonGeneric = new ArrayList { 5, 9, 1, 4 };
        // timer for generic list sort
        Stopwatch s = Stopwatch.StartNew();
        ListGeneric.Sort();
        s.Stop();
        Console.WriteLine($"Generic Sort: {ListGeneric}  \n Time taken: {s.Elapsed.TotalMilliseconds}ms");

        //timer for non-generic list sort
        Stopwatch s2 = Stopwatch.StartNew();
        ListNonGeneric.Sort();
        s2.Stop();
        Console.WriteLine($"Non-Generic Sort: {ListNonGeneric}  \n Time taken: {s2.Elapsed.TotalMilliseconds}ms");
        Console.ReadLine();
      }
    }
  }
```

此程式會產生類似下列內容的輸出：

```console
Generic Sort: System.Collections.Generic.List`1[System.Int32]
 Time taken: 0.0034ms
Non-Generic Sort: System.Collections.ArrayList
 Time taken: 0.2592ms
```

您在此首先可以注意到，泛型清單的排序速度比非泛型清單的排序速度明顯更快。 您也可能注意到，泛型清單的類型是獨特的 ([System.Int32])，而非泛型清單的類型則是一般化。 因為執行時間知道泛型 `List<int>` 是型別 <xref:System.Int32> ，所以它可以將清單專案儲存在記憶體中的基礎整數陣列，而非泛型 `ArrayList` 必須將每個清單專案轉換成物件。 如此範例所示，額外的轉換需要時間，因此會使清單排序速度變慢。

執行階段知道您的泛型型別的另一個優點是改進偵錯體驗。 當您偵錯 C# 中的泛型時，您知道資料結構中的每個元素是何種型別。 如果沒有泛型，您就無法得知每個項目是何種類型。

## <a name="see-also"></a>另請參閱

- [C# 程式設計手冊 - 泛型](../csharp/programming-guide/generics/index.md)

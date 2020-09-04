---
title: 事件簡介
description: 透過此概觀了解 .NET Core 中的事件，以及事件的語言設計目標。
ms.date: 06/20/2016
ms.assetid: 9b8d2a00-1584-4a5b-8994-5003d54d8e0c
ms.openlocfilehash: 4da44c151244e8b5de34f550040c271131d9598c
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465230"
---
# <a name="introduction-to-events"></a>事件簡介

[[上一步]](delegates-patterns.md)

事件就像委派，是「晚期繫結」** 機制。 事實上，事件是建立在委派的語言支援上。

事件一種物件 (向系統中所有感興趣的元件) 廣播有事發生的方式。 任何其他元件皆可以訂閱事件，並在引發事件時收到通知。

您可能在自己的某些程式設計中使用過事件。 許多圖形系統都有報告使用者互動的事件模型。 這些事件會報告滑鼠移動、按下按鈕和類似的互動。 這是其中最常見的，但不是使用事件的唯一狀況。

您可以為您的類別定義應該引發的事件。 處理事件時有一項重要考量，就是特定事件可能沒有任何登錄的物件。 您必須撰寫程式碼，讓它在未設定任何接聽程式時不會引發事件。

訂閱事件也會建立兩個物件 (事件來源和事件接收) 的結合程度。 您需要確保，對事件不再感興趣時，事件接收會取消訂閱事件來源。

## <a name="design-goals-for-event-support"></a>事件支援的設計目標

事件的語言設計會以這些目標為目標：

- 在事件來源和事件接收之間啟用極短的結合。 這兩個元件可能不是由相同的組織所撰寫，甚至可能依完全不同的排程更新。

- 訂閱事件和取消訂閱該相同事件應該非常簡單。

- 事件來源應支援多個事件訂閱者。 它也應該支援不附加任何事件訂閱者。

您可以看到事件的目標與委派的目標非常相似。
這就是事件語言支援建立在委派語言支援上的原因。

## <a name="language-support-for-events"></a>事件的語言支援

定義事件以及訂閱或取消訂閱事件的語法，是委派的語法延伸模組。

若要定義事件請使用 `event` 關鍵字︰

```csharp
public event EventHandler<FileListArgs> Progress;
```

事件類型 (本例中為 `EventHandler<FileListArgs>`) 必須是委派類型。 宣告事件時應該遵循一些慣例。 一般而言，事件委派類型具有 void 傳回。
事件宣告應該是動詞或動詞片語。
當事件回報發生的事件時，請使用過去的時態。 報告將要發生的事件時，請使用現在式動詞 (例如，`Closing`)。 通常使用現在式是表示您的類別支援某類的自訂行為。 最常見的情況之一就是支援取消。 例如，`Closing` 事件可包括一個引數，指出關閉作業是否應該繼續。  其他情況可讓呼叫端更新事件引數的屬性以修改行為。 您可引發事件，指出演算法會採用的下一個提議動作。 事件處理常式可透過修改事件引數的屬性來要求不同的動作。

當您想要引發事件時，可使用委派引動過程語法呼叫事件處理常式︰

```csharp
Progress?.Invoke(this, new FileListArgs(file));
```

如上一節中討論的[委派](delegates-patterns.md)，?。
當該事件沒有訂閱者時，運算子讓您輕鬆確定不用嘗試引發事件。

使用 `+=` 運算子訂閱事件︰

```csharp
EventHandler<FileListArgs> onProgress = (sender, eventArgs) =>
    Console.WriteLine(eventArgs.FoundFile);

fileLister.Progress += onProgress;
```

處理常式方法通常的前置詞為 ' On '，後面接著事件名稱，如上所示。

使用 `-=` 運算子取消訂閱事件：

```csharp
fileLister.Progress -= onProgress;
```

請務必為代表事件處理常式的運算式宣告本機變數。 這可確保取消訂閱移除處理常式。
但若改用 Lambda 運算式的主體，就要嘗試移除永遠不會附加的處理常式，其不執行任何作業。

在下一篇文章中，您會深入了解一般的事件模式，以及本例的不同變化。

[下一個](event-pattern.md)

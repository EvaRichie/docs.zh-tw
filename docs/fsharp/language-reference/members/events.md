---
title: 事件
description: '瞭解 F # 事件如何讓您將函式呼叫與使用者動作產生關聯，這在 GUI 程式設計中很重要。'
ms.date: 08/15/2020
ms.openlocfilehash: 17e0cc8840053bf24d5c69694fe94d544c44510d
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740337"
---
# <a name="events"></a>事件

事件可讓您產生函式呼叫與使用者動作的關聯，而且對 GUI 程式設計而言十分重要。 事件也可以由應用程式或作業系統觸發。

## <a name="handling-events"></a>處理事件

當您使用 GUI 程式庫如 Windows Forms 或 Windows Presentation Foundation (WPF) 時，應用程式中的大部分程式碼都會執行以回應程式庫預先定義的事件。 這些預先定義的事件是 GUI 類別的成員，例如表單和控制項。 您可以參考特定重要具名事件 (例如 `Click` 類別的 `Form` 事件)，以及叫用 `Add` 方法，將自訂行為加入至預先存在的事件 (例如按一下按鈕事件)，如下列程式碼所示。 如果您從 F# Interactive 執行此程式碼，請省略 `System.Windows.Forms.Application.Run(System.Windows.Forms.Form)` 的呼叫。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3601.fs)]

`Add` 方法的類型為 `('a -> unit) -> unit`。 因此，事件處理常式方法會接受一個參數 (通常是事件引數)，並傳回 `unit`。 上述範例示範事件處理常式做為 Lambda 運算式。 事件處理常式也可以是函式值，如下列程式碼範例所示。 範例中也會示範事件處理常式參數如何用來提供事件類型專屬資訊。 對於 `MouseMove` 事件，系統會傳遞 `System.Windows.Forms.MouseEventArgs` 物件，其中包含指標的 `X` 和 `Y` 位置。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3602.fs)]

## <a name="creating-custom-events"></a>建立自訂事件

F # 事件是以 F # [事件](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html) 類型表示，它會實 [IEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-ievent-1.html) 介面。 `IEvent`本身是結合兩個其他介面的功能和 IDelegateEvent 的介面 `System.IObservable<'T>` 。 [IDelegateEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-idelegateevent-1.html) 因此，`Event` 具有相當於其他語言中委派的功能，加上來自 `IObservable` 的額外功能，這表示 F# 事件支援事件篩選，以及使用 F# 第一級函式和 Lambda 運算式做為事件處理常式。 這項功能是在 [事件模組](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html)中提供。

若要在類別上建立其運作方式與任何其他 .NET Framework 事件類似的事件，請將 `let` 繫結 (將 `Event` 定義為類別中的欄位) 加入至類別。 您可以指定所需的事件引數類型做為型別引數，或是空過，讓編譯器推斷適當類型。 您也必須定義將事件公開為 CLI 事件的事件成員。 這個成員應具有 [CLIEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-clieventattribute.html) 屬性。 它的宣告方式與屬性類似，而且其實作只是呼叫事件的 [Publish](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html#Publish) 屬性。 您類別的使用者可以使用已發行事件的 `Add` 方法加入處理常式。 `Add` 方法的引數可以是 Lambda 運算式。 您可以使用事件的 `Trigger` 屬性引發事件，將引數傳遞至處理函式。 下列程式碼範例會說明這點。 在此範例中，推斷的事件類型引數是 Tuple，代表 Lambda 運算式的引數。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3605.fs)]

輸出如下。

```console
Event1 occurred! Object data: Hello World!
```

這裡會說明 `Event` 模組所提供的額外功能。 下列程式碼範例說明如何使用 `Event.create` 建立事件和觸發程序方法，並以 Lambda 運算式形式加入兩個事件處理常式，然後觸發事件以執行這兩個 Lambda 運算式。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3603.fs)]

上述程式碼的輸出如下。

```console
Event occurred.
Given a value: Event occurred.
```

## <a name="processing-event-streams"></a>處理事件資料流

您可以使用模組中的函式， [Event.add](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html#add) `Event` 以高度自訂的方式處理事件的資料流程，而不只是使用事件加入事件的事件處理常式。 若要這麼做，請使用正向管道 (`|>`) 與事件做為一連串函式呼叫中的第一個值，並且使用 `Event` 模組函式做為後續函式呼叫。

下列程式碼範例顯示如何設定只在特定條件下才會呼叫其處理常式的事件。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3604.fs)]

可 [觀察模組](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-observablemodule.html) 包含可在可觀察物件上運作的類似函式。 可預見物件與事件類似，但是只有在已訂閱可預見物件時，才會主動訂閱事件。

## <a name="implementing-an-interface-event"></a>實作介面事件

當您開發 UI 元件時，通常會從建立新表單或繼承自現有表單或控制項的新控制項開始進行。 事件經常是在介面上定義，在這種情況下，您必須實作介面才能實作事件。 `System.ComponentModel.INotifyPropertyChanged` 介面會定義單一 `System.ComponentModel.INotifyPropertyChanged.PropertyChanged` 事件。 下列程式碼將示範如何實作這個繼承的介面所定義的事件：

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

type AppForm() as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs ->
            this.Property1 <- "text2"
            this.Property2 <- "text3")

    // This property does not have the property-changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property-changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    // Expose the PropertyChanged event as a first class .NET event.
    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = propertyChanged.Publish.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = propertyChanged.Publish.RemoveHandler(handler)

    // This is the event-handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property {args.PropertyName} changed its value to {newValue}"

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
let inpc = appForm :> INotifyPropertyChanged
inpc.PropertyChanged.Add(appForm.OnPropertyChanged)
Application.Run(appForm)
```

如果您要在建構函式中連接事件，程式碼會稍微複雜，因為事件連結必須位於另一個建構函式的 `then` 區塊內，如下面範例所示：

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

// Create a private constructor with a dummy argument so that the public
// constructor can have no arguments.
type AppForm private (dummy) as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs ->
            this.Property1 <- "text2"
            this.Property2 <- "text3")

    // This property does not have the property changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = this.PropertyChanged.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = this.PropertyChanged.RemoveHandler(handler)

    // This is the event handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property {args.PropertyName} changed its value to {newValue}"

    new() as this =
        new AppForm(0)
        then
            let inpc = this :> INotifyPropertyChanged
            inpc.PropertyChanged.Add(this.OnPropertyChanged)

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
Application.Run(appForm)
```

## <a name="see-also"></a>另請參閱

- [成員](index.md)
- [處理和引發事件](../../../standard/events/index.md)
- [Lambda 運算式： `fun` 關鍵字](../functions/lambda-expressions-the-fun-keyword.md)

---
title: 非同步程式中的控制流程
ms.date: 07/20/2015
ms.assetid: b0443af7-c586-4cb0-b476-742ae4098a96
ms.openlocfilehash: 0c479b9dd2a691b1b353fac54ee3320a895b1c7f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396658"
---
# <a name="control-flow-in-async-programs-visual-basic"></a>非同步程式中的控制流程 (Visual Basic)

您可以使用 `Async` 和 `Await` 關鍵字更輕鬆地撰寫和維護非同步程式。 不過，如果您不了解程式的運作方式，則結果可能會讓您大吃一驚。 本主題透過簡單非同步程式來追蹤控制流程，以顯示控制何時從某個方法移至另一個方法以及每次傳輸的資訊。

> [!NOTE]
> `Async` 和 `Await` 關鍵字是在 Visual Studio 2012 中引入。

一般來說，您可以使用[Async](../../../language-reference/modifiers/async.md)修飾詞來標示包含非同步程式碼的方法。 在以 async 修飾詞標示的方法中，您可以使用[Await （Visual Basic）](../../../language-reference/operators/await-operator.md)運算子來指定方法要暫停的位置，以等候呼叫的非同步進程完成。 如需詳細資訊，請參閱[使用 Async 和 Await 進行非同步程式設計（Visual Basic）](index.md)。

下列範例會使用非同步方法，將所指定網站的內容下載為字串，以及顯示字串的長度。 這個範例包含下列兩個方法。

- `startButton_Click`，其呼叫 `AccessTheWebAsync` 並顯示結果。

- `AccessTheWebAsync`，會將網站的內容下載為字串，並傳回字串的長度。 `AccessTheWebAsync`使用非同步的 <xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 來下載內容。

編號的顯示行會出現在程式中的策略點，協助您了解程式的執行方式，以及說明每個標記點所發生的情況。 顯示行會標上 "ONE" 到 "SIX"。 標籤代表程式到達這些程式碼行的順序。

下列程式碼示範程式的大綱。

```vb
Class MainWindow

    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click

        ' ONE
        Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()

        ' FOUR
        Dim contentLength As Integer = Await getLengthTask

        ' SIX
        ResultsTextBox.Text &=
            vbCrLf & $"Length of the downloaded string: {contentLength}." & vbCrLf

    End Sub

    Async Function AccessTheWebAsync() As Task(Of Integer)

        ' TWO
        Dim client As HttpClient = New HttpClient()
        Dim getStringTask As Task(Of String) =
            client.GetStringAsync("https://msdn.microsoft.com")

        ' THREE
        Dim urlContents As String = Await getStringTask

        ' FIVE
        Return urlContents.Length
    End Function

End Class
```

每個標記位置 "ONE" 到 "SIX" 都會顯示程式目前狀態的資訊。 會產生下列輸出：

```console
ONE:   Entering startButton_Click.
           Calling AccessTheWebAsync.

TWO:   Entering AccessTheWebAsync.
           Calling HttpClient.GetStringAsync.

THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.

FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.

FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.

SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.

Length of the downloaded string: 33946.
```

## <a name="set-up-the-program"></a>設定程式

您可以從 MSDN 下載本主題所使用的程式碼，也可以自行建置。

> [!NOTE]
> 若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本，以及 .NET Framework 4.5 或更新版本。

### <a name="download-the-program"></a>下載程式

您可以從 [Async Sample: Control Flow in Async Programs](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0) (非同步範例：非同步程式中的控制流程) 下載本主題的應用程式。 下列步驟會開啟和執行程式。

1. 解壓縮下載的檔案，然後啟動 Visual Studio。

2. 在功能表列上，依序選擇 [檔案] ****、[開啟舊檔] **** 及 [專案/方案] ****。

3. 巡覽至保存解壓縮之範例程式碼的資料夾，並開啟方案 (.sln) 檔案，然後選擇 F5 鍵來建置和執行專案。

### <a name="build-the-program-yourself"></a>自行建立程式

下列 Windows Presentation Foundation (WPF) 專案包含本主題的程式碼範例。

若要執行專案，請執行下列步驟：

1. 啟動 Visual Studio。

2. 從功能表列依序選擇 [**檔案**]、[**新增**] 及 [**專案**]。

    此時會開啟 [新增專案]**** 對話方塊。

3. 在 [**已安裝的範本**] 窗格中，選擇 [ **Visual Basic**]，然後從專案類型清單中選擇 [ **WPF 應用程式**]。

4. 輸入 `AsyncTracer` 作為專案的名稱，然後選擇 [確定]**** 按鈕。

    新的專案隨即會出現在方案總管**** 中。

5. 在 Visual Studio 程式碼編輯器中，選擇 [ **MainWindow.xaml** ] 索引標籤。

    如未顯示索引標籤，請在方案總管**** 中開啟 MainWindow.xaml 的捷徑功能表，然後選擇 [檢視程式碼]****。

6. 在 MainWindow.xaml 的 [XAML]**** 檢視中，以下列程式碼取代程式碼。

    ```vb
    <Window
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="MainWindow"
        Title="Control Flow Trace" Height="350" Width="525">
        <Grid>
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="221,10,0,0" VerticalAlignment="Top" Width="75"/>
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="510" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" d:LayoutOverrides="HorizontalMargin"/>

        </Grid>
    </Window>
    ```

    包含文字方塊和按鈕的簡易視窗會出現在 MainWindow.xaml 的 [設計]**** 檢視中。

7. 加入 <xref:System.Net.Http> 的參考。

8. 在**方案總管**中，開啟 mainwindow.xaml 的快捷方式功能表，然後選擇 [ **View Code**]。

9. 在 Mainwindow.xaml 中，將程式碼取代為下列程式碼。

    ```vb
    ' Add an Imports statement and a reference for System.Net.Http.
    Imports System.Net.Http

    Class MainWindow

        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click

            ' The display lines in the example lead you through the control shifts.
            ResultsTextBox.Text &= "ONE:   Entering StartButton_Click." & vbCrLf &
                "           Calling AccessTheWebAsync." & vbCrLf

            Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()

            ResultsTextBox.Text &= vbCrLf & "FOUR:  Back in StartButton_Click." & vbCrLf &
                "           Task getLengthTask is started." & vbCrLf &
                "           About to await getLengthTask -- no caller to return to." & vbCrLf

            Dim contentLength As Integer = Await getLengthTask

            ResultsTextBox.Text &= vbCrLf & "SIX:   Back in StartButton_Click." & vbCrLf &
                "           Task getLengthTask is finished." & vbCrLf &
                "           Result from AccessTheWebAsync is stored in contentLength." & vbCrLf &
                "           About to display contentLength and exit." & vbCrLf

            ResultsTextBox.Text &=
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)
        End Sub

        Async Function AccessTheWebAsync() As Task(Of Integer)

            ResultsTextBox.Text &= vbCrLf & "TWO:   Entering AccessTheWebAsync."

            ' Declare an HttpClient object.
            Dim client As HttpClient = New HttpClient()

            ResultsTextBox.Text &= vbCrLf & "           Calling HttpClient.GetStringAsync." & vbCrLf

            ' GetStringAsync returns a Task(Of String).
            Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")

            ResultsTextBox.Text &= vbCrLf & "THREE: Back in AccessTheWebAsync." & vbCrLf &
                "           Task getStringTask is started."

            ' AccessTheWebAsync can continue to work until getStringTask is awaited.

            ResultsTextBox.Text &=
                vbCrLf & "           About to await getStringTask & return a Task(Of Integer) to StartButton_Click." & vbCrLf

            ' Retrieve the website contents when task is complete.
            Dim urlContents As String = Await getStringTask

            ResultsTextBox.Text &= vbCrLf & "FIVE:  Back in AccessTheWebAsync." &
                vbCrLf & "           Task getStringTask is complete." &
                vbCrLf & "           Processing the return statement." &
                vbCrLf & "           Exiting from AccessTheWebAsync." & vbCrLf

            Return urlContents.Length
        End Function

    End Class
    ```

10. 選擇 F5 鍵以執行程式，然後選擇 [開始]**** 按鈕。

    應該會出現下列輸出：

    ```console
    ONE:   Entering startButton_Click.
               Calling AccessTheWebAsync.

    TWO:   Entering AccessTheWebAsync.
               Calling HttpClient.GetStringAsync.

    THREE: Back in AccessTheWebAsync.
               Task getStringTask is started.
               About to await getStringTask & return a Task<int> to startButton_Click.

    FOUR:  Back in startButton_Click.
               Task getLengthTask is started.
               About to await getLengthTask -- no caller to return to.

    FIVE:  Back in AccessTheWebAsync.
               Task getStringTask is complete.
               Processing the return statement.
               Exiting from AccessTheWebAsync.

    SIX:   Back in startButton_Click.
               Task getLengthTask is finished.
               Result from AccessTheWebAsync is stored in contentLength.
               About to display contentLength and exit.

    Length of the downloaded string: 33946.
    ```

## <a name="trace-the-program"></a>追蹤程式

### <a name="steps-one-and-two"></a>步驟一和二

前兩個顯示當 `startButton_Click` 呼叫 `AccessTheWebAsync`，以及 `AccessTheWebAsync` 呼叫非同步 <xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 時，追蹤路徑的程式碼行。 下圖概述不同方法的呼叫。

![步驟一和二](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "Asynctrace-six-ONETWO")

`AccessTheWebAsync` 和 `client.GetStringAsync` 傳回的類型都是 <xref:System.Threading.Tasks.Task%601>。 針對 `AccessTheWebAsync`，TResult 是整數。 針對 `GetStringAsync`，TResult 是字串。 如需非同步方法傳回類型的詳細資訊，請參閱[非同步傳回類型（Visual Basic）](async-return-types.md)。

控制權返回呼叫端時，工作傳回非同步方法會傳回工作執行個體。 在被呼叫的方法中發現 `Await` 運算子時，或被呼叫的方法結束時，控制權會從非同步方法返回其呼叫端。 標上 "THREE" 到 "SIX" 的顯示行會追蹤處理程序的這個部分。

### <a name="step-three"></a>步驟三

在 `AccessTheWebAsync` 中，呼叫非同步方法 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> 以下載目標網頁的內容。 傳回 `client.GetStringAsync` 時，控制項會從 `client.GetStringAsync` 返回 `AccessTheWebAsync`。

`client.GetStringAsync` 方法會傳回指派給 `AccessTheWebAsync` 中 `getStringTask` 變數的字串工作。 範例程式中的下行示範 `client.GetStringAsync` 呼叫和指派。

```vb
Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")
```

您可以透過 `client.GetStringAsync` 將工作視為承諾，最後產生實際字串。 同時，如果 `AccessTheWebAsync` 的工作未依存於來自 `client.GetStringAsync` 的承諾字串，則該工作可以在 `client.GetStringAsync` 等候時繼續進行。 在此範例中，下列數行的輸出 (標上 "THREE”) 代表執行獨立工作的機會。

```console
THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.
```

 下列陳述式會在等候 `getStringTask` 時暫止 `AccessTheWebAsync` 中的進度。

```vb
Dim urlContents As String = Await getStringTask
```

下圖顯示從 `client.GetStringAsync` 到指派， `getStringTask` 以及從建立到對 `getStringTask` Await 運算子之應用程式的控制流程。

![步驟三](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "Asynctrace-six-三")

除非傳回 `client.GetStringAsync`，否則 await 運算式會暫止 `AccessTheWebAsync`。 同時，控制項會返回 `AccessTheWebAsync` 的呼叫端 `startButton_Click`。

> [!NOTE]
> 一般而言，您會立即等候非同步方法呼叫。 例如，下列指派可以取代可建立後等候 `getStringTask` 的先前程式碼：`Dim urlContents As String = Await client.GetStringAsync("https://msdn.microsoft.com")`
>
> 在本主題中，稍後會套用 await 運算子，以容納透過程式標記控制流程的輸出行。

### <a name="step-four"></a>步驟四

`AccessTheWebAsync` 的已宣告傳回型別為 `Task(Of Integer)`。 因此，暫止 `AccessTheWebAsync` 時，會將整數工作傳回給 `startButton_Click`。 您應該了解所傳回的工作不是 `getStringTask`。 傳回的工作是新整數工作，代表仍要在已暫止方法 `AccessTheWebAsync` 中執行的作業。 這個工作是來自 `AccessTheWebAsync` 的承諾，可在工作完成時產生整數。

下列陳述式會將這個工作指派給 `getLengthTask` 變數。

```vb
Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()
```

如同 `AccessTheWebAsync`，除非等候非同步工作 (`getLengthTask`)，否則 `startButton_Click` 可以繼續執行未依存於該工作結果的工作。 下列輸出行會代表該工作：

```console
FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.
```

等候 `getLengthTask` 時，會暫止 `startButton_Click` 中的進度。 除非 `AccessTheWebAsync` 完成，否則下列指派陳述式會暫止 `startButton_Click`。

```vb
Dim contentLength As Integer = Await getLengthTask
```

在下圖中，除非等候 `getLengthTask`，否則箭頭會顯示從 `AccessTheWebAsync` 中的 await 運算式到將值指派給 `getLengthTask` (後接 `startButton_Click` 中的正常處理) 的控制流程。

![步驟四](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "Asynctrace-six-四")

### <a name="step-five"></a>步驟五

`client.GetStringAsync` 指出完成時，會取消暫止 `AccessTheWebAsync` 中的處理，而且可以繼續略過 await 陳述式。 下列幾行輸出代表繼續處理：

```console
FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.
```

return 陳述式的運算元 `urlContents.Length` 儲存在 `AccessTheWebAsync` 所傳回的工作中。 await 運算式會從 `startButton_Click` 中的 `getLengthTask` 擷取該值。

下圖顯示 `client.GetStringAsync` (和 `getStringTask`) 完成後的控制權轉移。

![步驟五](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "Asynctrace-six-五")

`AccessTheWebAsync` 會執行直到完成，而且控制項會返回正在等待完成的 `startButton_Click`。

### <a name="step-six"></a>步驟六

`AccessTheWebAsync` 指出完成時，會繼續略過 `startButton_Async` 中 await 陳述式的處理。 事實上，程式不需要再執行任何動作。

下列數行的輸出代表在 `startButton_Async` 中繼續處理：

```console
SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.
```

await 運算式會從 `getLengthTask` 擷取整數值，而整數值是 `AccessTheWebAsync` 中 return 陳述式的運算元。 下列陳述式會將該值指派給 `contentLength` 變數。

```vb
Dim contentLength As Integer = Await getLengthTask
```

下圖顯示從 `AccessTheWebAsync` 到 `startButton_Click` 的控制項返回。

![步驟六](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "Asynctrace-six-六")

## <a name="see-also"></a>另請參閱

- [使用 Async 和 Await 進行非同步程式設計 (Visual Basic)](index.md)
- [非同步方法的傳回型別 (Visual Basic)](async-return-types.md)
- [逐步解說：使用 Async 和 Await 存取 Web (Visual Basic)](walkthrough-accessing-the-web-by-using-async-and-await.md)
- [Async Sample: Control Flow in Async Programs (C# and Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0) (非同步範例：非同步程式中的控制流程 (C# 和 Visual Basic))

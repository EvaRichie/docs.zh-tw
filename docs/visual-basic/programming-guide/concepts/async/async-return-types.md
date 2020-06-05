---
title: Async 傳回型別
ms.date: 07/20/2015
ms.assetid: 07890291-ee72-42d3-932a-fa4d312f2c60
ms.openlocfilehash: 5d19fc9831580412da24333be0885fce55384658
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396710"
---
# <a name="async-return-types-visual-basic"></a>非同步方法的傳回型別 (Visual Basic)

非同步方法有三種可能的傳回類型：<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.Task> 和 void。 在 Visual Basic 中，void 傳回型別會撰寫為 [Sub](../../language-features/procedures/sub-procedures.md) 程序。 如需非同步方法的詳細資訊，請參閱[使用 async 和 Await 進行非同步程式設計（Visual Basic）](index.md)。

每個傳回型別在下列其中一節探討，您可以在主題結尾處找到使用全部三種類型的完整範例。

> [!NOTE]
> 若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本以及 .NET Framework 4.5 或更新版本。

## <a name="taskt-return-type"></a><a name="BKMK_TaskTReturnType"></a> Task(T) 傳回型別

傳回 <xref:System.Threading.Tasks.Task%601> 型別用於非同步方法，其中包含運算元具有類型的[return](../../../language-reference/statements/return-statement.md)語句 `TResult` 。

在下列範例中，`TaskOfT_MethodAsync` 非同步方法包含一個傳回整數的 return 陳述式。 因此，方法宣告必須指定 `Task(Of Integer)` 傳回型別。

```vb
' TASK(OF T) EXAMPLE
Async Function TaskOfT_MethodAsync() As Task(Of Integer)

    ' The body of an async method is expected to contain an awaited
    ' asynchronous call.
    ' Task.FromResult is a placeholder for actual work that returns a string.
    Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())

    ' The method then can process the result in some way.
    Dim leisureHours As Integer
    If today.First() = "S" Then
        leisureHours = 16
    Else
        leisureHours = 5
    End If

    ' Because the return statement specifies an operand of type Integer, the
    ' method must have a return type of Task(Of Integer).
    Return leisureHours
End Function
```

從 await 運算式內呼叫 `TaskOfT_MethodAsync` 時，await 運算式會擷取儲存在 `TaskOfT_MethodAsync` 所傳回之工作中的整數值 (`leisureHours` 的值)。 如需 await 運算式的詳細資訊，請參閱[Await 運算子](../../../language-reference/operators/await-operator.md)。

下列程式碼會呼叫並等候方法 `TaskOfT_MethodAsync`。 結果會指派給 `result1` 變數。

```vb
' Call and await the Task(Of T)-returning async method in the same statement.
Dim result1 As Integer = Await TaskOfT_MethodAsync()
```

您可以藉由區隔對 `TaskOfT_MethodAsync` 的呼叫與 `Await` 的應用，深入了解這種運作方式，如下列程式碼所示。 呼叫不會立即等候的 `TaskOfT_MethodAsync` 方法，會傳回 `Task(Of Integer)`，如您所預期的方法宣告。 在範例中，工作會指派給 `integerTask` 變數。 因為 `integerTask` 是 <xref:System.Threading.Tasks.Task%601>，所以它包含 `TResult` 類型的 <xref:System.Threading.Tasks.Task%601.Result> 屬性。 在此情況下，TResult 代表整數類型。 當 `Await` 套用至 `integerTask` 時，await 運算式評估為 `integerTask` 之 <xref:System.Threading.Tasks.Task%601.Result%2A> 屬性的內容。 值會指派給 `result2` 變數。

> [!WARNING]
> <xref:System.Threading.Tasks.Task%601.Result%2A> 屬性是封鎖的屬性。 如果您嘗試在其工作完成之前先存取它，目前使用中的執行緒會封鎖，直到工作完成並且有可用的值為止。 在大部分情況下，您應該使用 `Await` 來存取值，而不是直接存取屬性。

```vb
' Call and await in separate statements.
Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()

' You can do other work that does not rely on resultTask before awaiting.
textBox1.Text &= "Application can continue working while the Task(Of T) runs. . . . " & vbCrLf

Dim result2 As Integer = Await integerTask
```

下列程式碼中的 display 陳述式會驗證 `result1` 變數、`result2` 變數和 `Result` 屬性的值相同。 請記住，`Result` 屬性是封鎖屬性，在等候其工作之前不應該存取它。

```vb
' Display the values of the result1 variable, the result2 variable, and
' the resultTask.Result property.
textBox1.Text &= vbCrLf & $"Value of result1 variable:   {result1}" & vbCrLf
textBox1.Text &= $"Value of result2 variable:   {result2}" & vbCrLf
textBox1.Text &= $"Value of resultTask.Result:  {integerTask.Result}" & vbCrLf
```

## <a name="task-return-type"></a><a name="BKMK_TaskReturnType"></a> 工作傳回型別

不包含 return 陳述式的非同步方法，或包含不會傳回運算元的 return 陳述式的非同步方法，通常具有傳回型別 <xref:System.Threading.Tasks.Task>。 這類方法是撰寫成同步執行的[Sub](../../language-features/procedures/sub-procedures.md)程式。 如果您針對非同步方法使用 `Task` 傳回型別，則除非被呼叫的非同步方法完成，否則呼叫的方法可以使用 `Await` 運算子暫止呼叫端完成。

在下列範例中，非同步方法 `Task_MethodAsync` 不包含 return 陳述式。 因此，您為方法指定 `Task` 傳回型別，如此可等候 `Task_MethodAsync`。 `Task` 類型的定義不包含用來儲存傳回值的 `Result` 屬性。

```vb
' TASK EXAMPLE
Async Function Task_MethodAsync() As Task

    ' The body of an async method is expected to contain an awaited
    ' asynchronous call.
    ' Task.Delay is a placeholder for actual work.
    Await Task.Delay(2000)
    textBox1.Text &= vbCrLf & "Sorry for the delay. . . ." & vbCrLf

    ' This method has no return statement, so its return type is Task.
End Function
```

使用 await 陳述式呼叫並等候 `Task_MethodAsync`，而不是使用 await 運算式，類似於同步 `Sub` 或傳回 void 方法的呼叫陳述式。 `Await`在此情況下，運算子的應用不會產生值。

下列程式碼會呼叫並等候方法 `Task_MethodAsync`。

```vb
' Call and await the Task-returning async method in the same statement.
Await Task_MethodAsync()
```

如先前範例所示 <xref:System.Threading.Tasks.Task%601> ，您可以 `Task_MethodAsync` 從運算子的應用程式中分隔的呼叫 `Await` ，如下列程式碼所示。 不過，請記住，`Task` 沒有 `Result` 屬性，且將 await 運算子套用至 `Task` 時不會產生任何值。

下列程式碼會區隔 `Task_MethodAsync` 的呼叫與等候 `Task_MethodAsync` 傳回的工作。

```vb
' Call and await in separate statements.
Dim simpleTask As Task = Task_MethodAsync()

' You can do other work that does not rely on simpleTask before awaiting.
textBox1.Text &= vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf

Await simpleTask
```

## <a name="void-return-type"></a><a name="BKMK_VoidReturnType"></a>Void 傳回型別

程式的主要用途 `Sub` 是在事件處理常式中，沒有傳回型別（稱為其他語言的 void 傳回型別）。 void 傳回也可用來覆寫傳回 void 的方法，或執行可分類為「射後不理」(fire and forget) 之活動的方法。 不過，您應該盡可能傳回 `Task`，因為無法等候傳回 void 的非同步方法。 這種方法的任何呼叫端必須要能夠繼續完成而不需等待呼叫的非同步方法完成，且呼叫端必須與非同步方法產生的任何值或例外狀況無關。

傳回 void 的非同步方法的呼叫端無法攔截方法擲回的例外狀況，這類未處理的例外狀況有可能造成應用程式失敗。 如果例外狀況發生在會傳回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的非同步方法，則例外狀況會儲存在傳回的工作中，並在等候工作時再次擲回。 因此，請確定任何可能會產生例外狀況的非同步方法具有傳回型別 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>，且會等候對方法的呼叫。

如需如何在非同步方法中攔截例外狀況的詳細資訊，請參閱 [Try...Catch...Finally 陳述式](../../../language-reference/statements/try-catch-finally-statement.md)。

下列程式碼會定義非同步事件處理常式。

```vb
' SUB EXAMPLE
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click

    textBox1.Clear()

    ' Start the process and await its completion. DriverAsync is a
    ' Task-returning async method.
    Await DriverAsync()

    ' Say goodbye.
    textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."
End Sub
```

## <a name="complete-example"></a><a name="BKMK_Example"></a>完整範例

下列 Windows Presentation Foundation (WPF) 專案包含本土的程式碼範例。

 若要執行專案，請執行下列步驟：

1. 啟動 Visual Studio。

2. 從功能表列依序選擇 [**檔案**]、[**新增**] 及 [**專案**]。

     此時會開啟 [新增專案]**** 對話方塊。

3. 在 [**已安裝**的**範本**] 分類中，選擇 [ **Visual Basic**]，然後選擇 [ **Windows**]。 在專案類型清單中，選擇 [WPF 應用程式]****。

4. 輸入 `AsyncReturnTypes` 作為專案的名稱，然後選擇 [確定]**** 按鈕。

     新的專案隨即會出現在方案總管**** 中。

5. 在 Visual Studio 程式碼編輯器中，選擇 [ **MainWindow.xaml** ] 索引標籤。

     如果未顯示索引標籤，請在方案總管**** 中開啟 MainWindow.xaml 的捷徑功能表，然後選擇 [開啟]****。

6. 在 MainWindow.xaml 的 [XAML]**** 視窗中，將程式碼取代為下列程式碼。

    ```vb
    <Window x:Class="MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            Title="MainWindow" Height="350" Width="525">
        <Grid>
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>

        </Grid>
    </Window>
    ```

     包含文字方塊和按鈕的簡單視窗會出現在 MainWindow.xaml 的 [設計]**** 視窗中。

7. 在**方案總管**中，開啟 mainwindow.xaml 的快捷方式功能表，然後選擇 [ **View Code**]。

8. 以下列程式碼取代 MainWindow.xaml.vb 中的程式碼。

    ```vb
    Class MainWindow

        ' SUB EXAMPLE
        Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click

            textBox1.Clear()

            ' Start the process and await its completion. DriverAsync is a
            ' Task-returning async method.
            Await DriverAsync()

            ' Say goodbye.
            textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."
        End Sub

        Async Function DriverAsync() As Task

            ' Task(Of T)
            ' Call and await the Task(Of T)-returning async method in the same statement.
            Dim result1 As Integer = Await TaskOfT_MethodAsync()

            ' Call and await in separate statements.
            Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()

            ' You can do other work that does not rely on resultTask before awaiting.
            textBox1.Text &= "Application can continue working while the Task(Of T) runs. . . . " & vbCrLf

            Dim result2 As Integer = Await integerTask

            ' Display the values of the result1 variable, the result2 variable, and
            ' the resultTask.Result property.
            textBox1.Text &= vbCrLf & $"Value of result1 variable:   {result1}" & vbCrLf
            textBox1.Text &= $"Value of result2 variable:   {result2}" & vbCrLf
            textBox1.Text &= $"Value of resultTask.Result:  {integerTask.Result}" & vbCrLf

            ' Task
            ' Call and await the Task-returning async method in the same statement.
            Await Task_MethodAsync()

            ' Call and await in separate statements.
            Dim simpleTask As Task = Task_MethodAsync()

            ' You can do other work that does not rely on simpleTask before awaiting.
            textBox1.Text &= vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf

            Await simpleTask
        End Function

        ' TASK(OF T) EXAMPLE
        Async Function TaskOfT_MethodAsync() As Task(Of Integer)

            ' The body of an async method is expected to contain an awaited
            ' asynchronous call.
            ' Task.FromResult is a placeholder for actual work that returns a string.
            Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())

            ' The method then can process the result in some way.
            Dim leisureHours As Integer
            If today.First() = "S" Then
                leisureHours = 16
            Else
                leisureHours = 5
            End If

            ' Because the return statement specifies an operand of type Integer, the
            ' method must have a return type of Task(Of Integer).
            Return leisureHours
        End Function

        ' TASK EXAMPLE
        Async Function Task_MethodAsync() As Task

            ' The body of an async method is expected to contain an awaited
            ' asynchronous call.
            ' Task.Delay is a placeholder for actual work.
            Await Task.Delay(2000)
            textBox1.Text &= vbCrLf & "Sorry for the delay. . . ." & vbCrLf

            ' This method has no return statement, so its return type is Task.
        End Function

    End Class
    ```

9. 選擇 F5 鍵以執行程式，然後選擇 [開始]**** 按鈕。

     應該會出現下列輸出：

    ```console
    Application can continue working while the Task<T> runs. . . .

    Value of result1 variable:   5
    Value of result2 variable:   5
    Value of integerTask.Result: 5

    Sorry for the delay. . . .

    Application can continue working while the Task runs. . . .

    Sorry for the delay. . . .

    All done, exiting button-click event handler.
    ```

## <a name="see-also"></a>另請參閱

- <xref:System.Threading.Tasks.Task.FromResult%2A>
- [逐步解說：使用 Async 和 Await 存取 Web (Visual Basic)](walkthrough-accessing-the-web-by-using-async-and-await.md)
- [非同步程式中的控制流程 (Visual Basic)](control-flow-in-async-programs.md)
- [非同步](../../../language-reference/modifiers/async.md)
- [Await 運算子](../../../language-reference/operators/await-operator.md)

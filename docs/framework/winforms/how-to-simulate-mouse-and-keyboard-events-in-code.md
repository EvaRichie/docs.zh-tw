---
title: 作法：以程式碼模擬滑鼠和鍵盤事件
description: 瞭解如何使用 Windows Forms 提供的選項，以程式設計方式模擬滑鼠和鍵盤輸入。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboards [Windows Forms], event simulation
- user input [Windows Forms], simulating
- SendKeys [Windows Forms], using
- mouse clicks [Windows Forms], simulating
- mouse [Windows Forms], event simulation
ms.assetid: 6abcb67e-3766-4af2-9590-bf5dabd17e41
ms.openlocfilehash: 9b453787f7fa7f5041f75e04d65557a0a3838bee
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904360"
---
# <a name="how-to-simulate-mouse-and-keyboard-events-in-code"></a><span data-ttu-id="a04af-103">作法：以程式碼模擬滑鼠和鍵盤事件</span><span class="sxs-lookup"><span data-stu-id="a04af-103">How to: Simulate Mouse and Keyboard Events in Code</span></span>

<span data-ttu-id="a04af-104">Windows Form 提供以程式設計方式模擬滑鼠和鍵盤輸入的數個選項。</span><span class="sxs-lookup"><span data-stu-id="a04af-104">Windows Forms provides several options for programmatically simulating mouse and keyboard input.</span></span> <span data-ttu-id="a04af-105">本主題提供這些選項的概觀。</span><span class="sxs-lookup"><span data-stu-id="a04af-105">This topic provides an overview of these options.</span></span>

## <a name="simulating-mouse-input"></a><span data-ttu-id="a04af-106">模擬滑鼠輸入</span><span class="sxs-lookup"><span data-stu-id="a04af-106">Simulating Mouse Input</span></span>

<span data-ttu-id="a04af-107">模擬滑鼠事件的最佳方式是呼叫 `On`*EventName* 方法，這個方法會引發您要模擬的滑鼠事件。</span><span class="sxs-lookup"><span data-stu-id="a04af-107">The best way to simulate mouse events is to call the `On`*EventName* method that raises the mouse event you want to simulate.</span></span> <span data-ttu-id="a04af-108">通常只有在自訂控制項和表單內才能使用這個選項，因為引發事件的方法會受到保護，而且無法在控制項或表單外進行存取。</span><span class="sxs-lookup"><span data-stu-id="a04af-108">This option is usually possible only within custom controls and forms, because the methods that raise events are protected and cannot be accessed outside the control or form.</span></span> <span data-ttu-id="a04af-109">例如，下列步驟說明如何以程式碼模擬按一下滑鼠右鍵的動作。</span><span class="sxs-lookup"><span data-stu-id="a04af-109">For example, the following steps illustrate how to simulate clicking the right mouse button in code.</span></span>

#### <a name="to-programmatically-click-the-right-mouse-button"></a><span data-ttu-id="a04af-110">以程式設計方式按一下滑鼠右鍵</span><span class="sxs-lookup"><span data-stu-id="a04af-110">To programmatically click the right mouse button</span></span>

1. <span data-ttu-id="a04af-111">建立 <xref:System.Windows.Forms.MouseEventArgs> ，並將其 <xref:System.Windows.Forms.MouseEventArgs.Button%2A> 屬性設定為 <xref:System.Windows.Forms.MouseButtons.Right?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="a04af-111">Create a <xref:System.Windows.Forms.MouseEventArgs> whose <xref:System.Windows.Forms.MouseEventArgs.Button%2A> property is set to the <xref:System.Windows.Forms.MouseButtons.Right?displayProperty=nameWithType> value.</span></span>

2. <span data-ttu-id="a04af-112">呼叫 <xref:System.Windows.Forms.Control.OnMouseClick%2A> 方法，並以這個 <xref:System.Windows.Forms.MouseEventArgs> 做為引數。</span><span class="sxs-lookup"><span data-stu-id="a04af-112">Call the <xref:System.Windows.Forms.Control.OnMouseClick%2A> method with this <xref:System.Windows.Forms.MouseEventArgs> as the argument.</span></span>

<span data-ttu-id="a04af-113">如需自訂控制項的詳細資訊，請參閱[在設計階段開發 Windows Form 控制項](./controls/developing-windows-forms-controls-at-design-time.md)。</span><span class="sxs-lookup"><span data-stu-id="a04af-113">For more information on custom controls, see [Developing Windows Forms Controls at Design Time](./controls/developing-windows-forms-controls-at-design-time.md).</span></span>

<span data-ttu-id="a04af-114">還有其他方式可以模擬滑鼠輸入。</span><span class="sxs-lookup"><span data-stu-id="a04af-114">There are other ways to simulate mouse input.</span></span> <span data-ttu-id="a04af-115">例如，您可以透過程式設計方式設定代表狀態的控制項屬性，這個狀態通常是透過滑鼠輸入來設定 (例如 <xref:System.Windows.Forms.CheckBox.Checked%2A> 控制項的 <xref:System.Windows.Forms.CheckBox> 屬性)，您也可以直接呼叫附加至所要模擬之事件的委派。</span><span class="sxs-lookup"><span data-stu-id="a04af-115">For example, you can programmatically set a control property that represents a state that is typically set through mouse input (such as the <xref:System.Windows.Forms.CheckBox.Checked%2A> property of the <xref:System.Windows.Forms.CheckBox> control), or you can directly call the delegate that is attached to the event you want to simulate.</span></span>

## <a name="simulating-keyboard-input"></a><span data-ttu-id="a04af-116">模擬鍵盤輸入</span><span class="sxs-lookup"><span data-stu-id="a04af-116">Simulating Keyboard Input</span></span>

<span data-ttu-id="a04af-117">除了可以使用上述用於滑鼠輸入的策略來模擬鍵盤輸入之外，Windows Form 還提供 <xref:System.Windows.Forms.SendKeys> 類別，以便將按鍵動作傳送至作用中應用程式。</span><span class="sxs-lookup"><span data-stu-id="a04af-117">Although you can simulate keyboard input by using the strategies discussed above for mouse input, Windows Forms also provides the <xref:System.Windows.Forms.SendKeys> class for sending keystrokes to the active application.</span></span>

> [!CAUTION]
> <span data-ttu-id="a04af-118">如果您的應用程式是設計成可搭配國際上現有的各種鍵盤來使用，則使用 <xref:System.Windows.Forms.SendKeys.Send%2A?displayProperty=nameWithType> 可能會產生無法預期的結果，應該予以避免。</span><span class="sxs-lookup"><span data-stu-id="a04af-118">If your application is intended for international use with a variety of keyboards, the use of <xref:System.Windows.Forms.SendKeys.Send%2A?displayProperty=nameWithType> could yield unpredictable results and should be avoided.</span></span>

> [!NOTE]
> <span data-ttu-id="a04af-119"><xref:System.Windows.Forms.SendKeys> 類別已針對 .NET Framework 3.0 進行更新，以便能夠在 Windows Vista 上執行的應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="a04af-119">The <xref:System.Windows.Forms.SendKeys> class has been updated for the .NET Framework 3.0 to enable its use in applications that run on Windows Vista.</span></span> <span data-ttu-id="a04af-120">Windows Vista 的增強式安全性 (稱為使用者帳戶控制或 UAC) 會讓之前的實作無法如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="a04af-120">The enhanced security of Windows Vista (known as User Account Control or UAC) prevents the previous implementation from working as expected.</span></span>
>
> <span data-ttu-id="a04af-121"><xref:System.Windows.Forms.SendKeys> 類別容易受到時間問題的影響，某些開發人員必須解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="a04af-121">The <xref:System.Windows.Forms.SendKeys> class is susceptible to timing issues, which some developers have had to work around.</span></span> <span data-ttu-id="a04af-122">更新的實作仍然容易受到時間問題的影響，但是速度會稍微快一些，而且可能需要對解決方法進行變更。</span><span class="sxs-lookup"><span data-stu-id="a04af-122">The updated implementation is still susceptible to timing issues, but is slightly faster and may require changes to the workarounds.</span></span> <span data-ttu-id="a04af-123"><xref:System.Windows.Forms.SendKeys> 類別會先嘗試使用之前的實作；如果失敗，則使用新的實作。</span><span class="sxs-lookup"><span data-stu-id="a04af-123">The <xref:System.Windows.Forms.SendKeys> class tries to use the previous implementation first, and if that fails, uses the new implementation.</span></span> <span data-ttu-id="a04af-124">因此， <xref:System.Windows.Forms.SendKeys> 類別在不同的作業系統上可能會有不同的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a04af-124">As a result, the <xref:System.Windows.Forms.SendKeys> class may behave differently on different operating systems.</span></span> <span data-ttu-id="a04af-125">此外，當 <xref:System.Windows.Forms.SendKeys> 類別使用新的實作時， <xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法不會在將訊息傳送至另一個處理序時，等候處理這些訊息。</span><span class="sxs-lookup"><span data-stu-id="a04af-125">Additionally, when the <xref:System.Windows.Forms.SendKeys> class uses the new implementation, the <xref:System.Windows.Forms.SendKeys.SendWait%2A> method will not wait for messages to be processed when they are sent to another process.</span></span>
>
> <span data-ttu-id="a04af-126">如果不論作業系統為何，應用程式都需要一致的行為，您可以強制 <xref:System.Windows.Forms.SendKeys> 類別使用新的實作，方式是將下列應用程式設定加入 app.config 檔中。</span><span class="sxs-lookup"><span data-stu-id="a04af-126">If your application relies on consistent behavior regardless of the operating system, you can force the <xref:System.Windows.Forms.SendKeys> class to use the new implementation by adding the following application setting to your app.config file.</span></span>
>
> ```xml
> <appSettings>
>  <add key="SendKeys" value="SendInput"/>
> </appSettings>
> ```
>
> <span data-ttu-id="a04af-127">若要強制 <xref:System.Windows.Forms.SendKeys> 類別使用之前的實作，請改用 `"JournalHook"` 值。</span><span class="sxs-lookup"><span data-stu-id="a04af-127">To force the <xref:System.Windows.Forms.SendKeys> class to use the previous implementation, use the value `"JournalHook"` instead.</span></span>

#### <a name="to-send-a-keystroke-to-the-same-application"></a><span data-ttu-id="a04af-128">將按鍵動作傳送至相同的應用程式</span><span class="sxs-lookup"><span data-stu-id="a04af-128">To send a keystroke to the same application</span></span>

1. <span data-ttu-id="a04af-129">請呼叫 <xref:System.Windows.Forms.SendKeys.Send%2A> 類別的 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 或 <xref:System.Windows.Forms.SendKeys> 方法。</span><span class="sxs-lookup"><span data-stu-id="a04af-129">Call the <xref:System.Windows.Forms.SendKeys.Send%2A> or <xref:System.Windows.Forms.SendKeys.SendWait%2A> method of the <xref:System.Windows.Forms.SendKeys> class.</span></span> <span data-ttu-id="a04af-130">應用程式的作用控制項會接收指定的按鍵動作。</span><span class="sxs-lookup"><span data-stu-id="a04af-130">The specified keystrokes will be received by the active control of the application.</span></span> <span data-ttu-id="a04af-131">下列程式碼範例使用 <xref:System.Windows.Forms.SendKeys.Send%2A> 來模擬當使用者按兩下表單介面時，按下 ENTER 鍵的動作。</span><span class="sxs-lookup"><span data-stu-id="a04af-131">The following code example uses <xref:System.Windows.Forms.SendKeys.Send%2A> to simulate pressing the ENTER key when the user double-clicks the surface of the form.</span></span> <span data-ttu-id="a04af-132">這個範例假設 <xref:System.Windows.Forms.Form> 含有一個定位點索引為 0 的 <xref:System.Windows.Forms.Button> 控制項。</span><span class="sxs-lookup"><span data-stu-id="a04af-132">This example assumes a <xref:System.Windows.Forms.Form> with a single <xref:System.Windows.Forms.Button> control that has a tab index of 0.</span></span>

    [!code-cpp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#10)]
    [!code-csharp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#10)]
    [!code-vb[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#10)]

#### <a name="to-send-a-keystroke-to-a-different-application"></a><span data-ttu-id="a04af-133">將按鍵動作傳送至不同的應用程式</span><span class="sxs-lookup"><span data-stu-id="a04af-133">To send a keystroke to a different application</span></span>

1. <span data-ttu-id="a04af-134">啟動會接收按鍵動作的應用程式視窗，然後呼叫 <xref:System.Windows.Forms.SendKeys.Send%2A> 或 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="a04af-134">Activate the application window that will receive the keystrokes, and then call the <xref:System.Windows.Forms.SendKeys.Send%2A> or <xref:System.Windows.Forms.SendKeys.SendWait%2A> method.</span></span> <span data-ttu-id="a04af-135">由於沒有可啟動另一個應用程式的 Managed 方法，因此您必須使用原生 Windows 方法強制將焦點放在其他應用程式上。</span><span class="sxs-lookup"><span data-stu-id="a04af-135">Because there is no managed method to activate another application, you must use native Windows methods to force focus on other applications.</span></span> <span data-ttu-id="a04af-136">下列程式碼範例使用平台叫用呼叫 `FindWindow` 和 `SetForegroundWindow` 方法，以啟動 [小算盤] 應用程式視窗，然後再呼叫 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 對 [小算盤] 應用程式發出一連串計算。</span><span class="sxs-lookup"><span data-stu-id="a04af-136">The following code example uses platform invoke to call the `FindWindow` and `SetForegroundWindow` methods to activate the Calculator application window, and then calls <xref:System.Windows.Forms.SendKeys.SendWait%2A> to issue a series of calculations to the Calculator application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a04af-137">用於尋找 [小算盤] 應用程式之 `FindWindow` 呼叫的正確參數會隨您的 Windows 版本而異。</span><span class="sxs-lookup"><span data-stu-id="a04af-137">The correct parameters of the `FindWindow` call that locates the Calculator application vary based on your version of Windows.</span></span>  <span data-ttu-id="a04af-138">下列程式碼會在 Windows 7 上尋找計算機應用程式。</span><span class="sxs-lookup"><span data-stu-id="a04af-138">The following code finds the Calculator application on Windows 7.</span></span> <span data-ttu-id="a04af-139">在 Windows Vista 上，將第一個參數變更為 "SciCalc"。</span><span class="sxs-lookup"><span data-stu-id="a04af-139">On Windows Vista, change the first parameter to "SciCalc".</span></span> <span data-ttu-id="a04af-140">您可以使用 Visual Studio 隨附的 Spy++ 工具來判斷正確的參數。</span><span class="sxs-lookup"><span data-stu-id="a04af-140">You can use the Spy++ tool, included with Visual Studio, to determine the correct parameters.</span></span>

    [!code-cpp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#5)]
    [!code-csharp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#5)]
    [!code-vb[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#5)]

## <a name="example"></a><span data-ttu-id="a04af-141">範例</span><span class="sxs-lookup"><span data-stu-id="a04af-141">Example</span></span>

<span data-ttu-id="a04af-142">下列程式碼範例是先前程式碼範例的完整應用。</span><span class="sxs-lookup"><span data-stu-id="a04af-142">The following code example is the complete application for the previous code examples.</span></span>

[!code-cpp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#0)]
[!code-csharp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#0)]
[!code-vb[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#0)]

## <a name="compiling-the-code"></a><span data-ttu-id="a04af-143">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="a04af-143">Compiling the Code</span></span>

<span data-ttu-id="a04af-144">這個範例需要：</span><span class="sxs-lookup"><span data-stu-id="a04af-144">This example requires:</span></span>

- <span data-ttu-id="a04af-145">System、System.Drawing 和 System.Windows.Forms 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="a04af-145">References to the System, System.Drawing and System.Windows.Forms assemblies.</span></span>

## <a name="see-also"></a><span data-ttu-id="a04af-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a04af-146">See also</span></span>

- [<span data-ttu-id="a04af-147">Windows Form 中的使用者輸入</span><span class="sxs-lookup"><span data-stu-id="a04af-147">User Input in Windows Forms</span></span>](user-input-in-windows-forms.md)

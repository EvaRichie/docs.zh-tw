---
title: 篩選 My.Application.Log 輸出
ms.date: 07/20/2015
helpviewer_keywords:
- My.Log object, filtering output
- My.Application.Log object, filtering output
- application event logs, output filtering
ms.assetid: 2c0a457a-38a4-49e1-934d-a51320b7b4ca
ms.openlocfilehash: aa63e7d23641ad71b135f15236e29399a535784f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398249"
---
# <a name="walkthrough-filtering-myapplicationlog-output-visual-basic"></a><span data-ttu-id="685a1-102">逐步解說：篩選 My.Application.Log 輸出 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="685a1-102">Walkthrough: Filtering My.Application.Log Output (Visual Basic)</span></span>

<span data-ttu-id="685a1-103">本逐步解說示範如何變更 `My.Application.Log` 物件的預設記錄檔篩選，以控制哪些資訊會從 `Log` 物件傳遞至接聽程式，而哪些資訊會由接聽程式寫入。</span><span class="sxs-lookup"><span data-stu-id="685a1-103">This walkthrough demonstrates how to change the default log filtering for the `My.Application.Log` object, to control what information is passed from the `Log` object to the listeners and what information is written by the listeners.</span></span> <span data-ttu-id="685a1-104">由於組態資訊是儲存在應用程式的組態檔中，因此即使在建置應用程式之後，您仍可以變更記錄行為。</span><span class="sxs-lookup"><span data-stu-id="685a1-104">You can change the logging behavior even after building the application, because the configuration information is stored in the application's configuration file.</span></span>

## <a name="getting-started"></a><span data-ttu-id="685a1-105">開始使用</span><span class="sxs-lookup"><span data-stu-id="685a1-105">Getting Started</span></span>

<span data-ttu-id="685a1-106">`My.Application.Log` 寫入的每個訊息都有相關聯的嚴重性層級，而篩選機制會使用這個層級來控制記錄檔輸出。</span><span class="sxs-lookup"><span data-stu-id="685a1-106">Each message that `My.Application.Log` writes has an associated severity level, which filtering mechanisms use to control the log output.</span></span> <span data-ttu-id="685a1-107">此範例應用程式會使用 `My.Application.Log` 方法，寫入數個不同嚴重性層級的記錄檔訊息。</span><span class="sxs-lookup"><span data-stu-id="685a1-107">This sample application uses `My.Application.Log` methods to write several log messages with different severity levels.</span></span>

#### <a name="to-build-the-sample-application"></a><span data-ttu-id="685a1-108">若要安裝範例應用程式</span><span class="sxs-lookup"><span data-stu-id="685a1-108">To build the sample application</span></span>

1. <span data-ttu-id="685a1-109">開啟新的 Visual Basic Windows 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="685a1-109">Open a new Visual Basic Windows Application project.</span></span>

2. <span data-ttu-id="685a1-110">加入名為 "Button1 to Form1" 的按鈕。</span><span class="sxs-lookup"><span data-stu-id="685a1-110">Add a button named Button1 to Form1.</span></span>

3. <span data-ttu-id="685a1-111">在 Button1 的 <xref:System.Windows.Forms.Control.Click> 事件處理常式中新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="685a1-111">In the <xref:System.Windows.Forms.Control.Click> event handler for Button1, add the following code:</span></span>

     [!code-vb[VbVbcnMyApplicationLogFiltering#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyApplicationLogFiltering/VB/Form1.vb#1)]

4. <span data-ttu-id="685a1-112">在偵錯工具中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-112">Run the application in the debugger.</span></span>

5. <span data-ttu-id="685a1-113">按下 **Button1**。</span><span class="sxs-lookup"><span data-stu-id="685a1-113">Press **Button1**.</span></span>

     <span data-ttu-id="685a1-114">應用程式會將下列資訊寫入應用程式的偵錯輸出與記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="685a1-114">The application writes the following information to the application's debug output and log file.</span></span>

     `DefaultSource Information: 0 : In Button1_Click`

     `DefaultSource Error: 2 : Error in the application.`

6. <span data-ttu-id="685a1-115">關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-115">Close the application.</span></span>

     <span data-ttu-id="685a1-116">如需如何檢視應用程式偵錯輸出視窗的資訊，請參閱[輸出視窗](/visualstudio/ide/reference/output-window)。</span><span class="sxs-lookup"><span data-stu-id="685a1-116">For information on how to view the application's debug output window, see [Output Window](/visualstudio/ide/reference/output-window).</span></span> <span data-ttu-id="685a1-117">如需應用程式記錄檔位置的資訊，請參閱[逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)。</span><span class="sxs-lookup"><span data-stu-id="685a1-117">For information on the location of the application's log file, see [Walkthrough: Determining Where My.Application.Log Writes Information](walkthrough-determining-where-my-application-log-writes-information.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="685a1-118">根據預設，應用程式會在應用程式關閉時清除記錄檔輸出。</span><span class="sxs-lookup"><span data-stu-id="685a1-118">By default, the application flushes the log-file output when the application closes.</span></span>

     <span data-ttu-id="685a1-119">在上述範例，第二次呼叫 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> 方法和呼叫 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> 方法會產生記錄輸出，而第一次和最後一次呼叫 `WriteEntry` 方法則不會。</span><span class="sxs-lookup"><span data-stu-id="685a1-119">In the example above, the second call to the <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> method and the call to the <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> method produces log output, while the first and last calls to the `WriteEntry` method do not.</span></span> <span data-ttu-id="685a1-120">這是因為 `WriteEntry` 和 `WriteException` 的嚴重性層級為 "Information" 和 "Error"，兩者皆為 `My.Application.Log` 物件的預設記錄檔篩選所允許。</span><span class="sxs-lookup"><span data-stu-id="685a1-120">This is because the severity levels of `WriteEntry` and `WriteException` are "Information" and "Error", both of which are allowed by the `My.Application.Log` object's default log filtering.</span></span> <span data-ttu-id="685a1-121">不過，具有 "Start" 和 "Stop" 嚴重性層級的事件會阻礙記錄檔輸出的產生。</span><span class="sxs-lookup"><span data-stu-id="685a1-121">However, events with "Start" and "Stop" severity levels are prevented from producing log output.</span></span>

## <a name="filtering-for-all-myapplicationlog-listeners"></a><span data-ttu-id="685a1-122">篩選所有 My.Application.Log 接聽程式</span><span class="sxs-lookup"><span data-stu-id="685a1-122">Filtering for All My.Application.Log Listeners</span></span>

<span data-ttu-id="685a1-123">`My.Application.Log` 物件會使用名為 `DefaultSwitch` 的 <xref:System.Diagnostics.SourceSwitch>，來控制要將 `WriteEntry` 和 `WriteException` 方法的哪些訊息傳遞給記錄檔接聽程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-123">The `My.Application.Log` object uses a <xref:System.Diagnostics.SourceSwitch> named `DefaultSwitch` to control which messages it passes from the `WriteEntry` and `WriteException` methods to the log listeners.</span></span> <span data-ttu-id="685a1-124">您可以將 `DefaultSwitch` 的值設定為 <xref:System.Diagnostics.SourceLevels> 列舉值之一，以在應用程式的組態檔中設定它。</span><span class="sxs-lookup"><span data-stu-id="685a1-124">You can configure `DefaultSwitch` in the application's configuration file by setting its value to one of the <xref:System.Diagnostics.SourceLevels> enumeration values.</span></span> <span data-ttu-id="685a1-125">根據預設，其值為 "Information"。</span><span class="sxs-lookup"><span data-stu-id="685a1-125">By default, its value is "Information".</span></span>

<span data-ttu-id="685a1-126">下表顯示依據特定 `DefaultSwitch` 設定的假設，記錄檔要將訊息寫入接聽程式所需的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="685a1-126">This table shows the severity level required for Log to write a message to the listeners, given a particular `DefaultSwitch` setting.</span></span>

|<span data-ttu-id="685a1-127">DefaultSwitch 值</span><span class="sxs-lookup"><span data-stu-id="685a1-127">DefaultSwitch Value</span></span>|<span data-ttu-id="685a1-128">輸出所需的訊息嚴重性</span><span class="sxs-lookup"><span data-stu-id="685a1-128">Message severity required for output</span></span>|
|---|---|
|`Critical`|`Critical`|
|`Error`|<span data-ttu-id="685a1-129">`Critical` 或 `Error`</span><span class="sxs-lookup"><span data-stu-id="685a1-129">`Critical` or `Error`</span></span>|
|`Warning`|<span data-ttu-id="685a1-130">`Critical`、`Error` 或 `Warning`</span><span class="sxs-lookup"><span data-stu-id="685a1-130">`Critical`, `Error`, or `Warning`</span></span>|
|`Information`|<span data-ttu-id="685a1-131">`Critical`、`Error`、`Warning` 或 `Information`</span><span class="sxs-lookup"><span data-stu-id="685a1-131">`Critical`, `Error`, `Warning`, or `Information`</span></span>|
|`Verbose`|<span data-ttu-id="685a1-132">`Critical`、`Error`、`Warning`、`Information` 或 `Verbose`</span><span class="sxs-lookup"><span data-stu-id="685a1-132">`Critical`, `Error`, `Warning`, `Information`, or `Verbose`</span></span>|
|`ActivityTracing`|<span data-ttu-id="685a1-133">`Start`、`Stop`、`Suspend`、`Resume` 或 `Transfer`</span><span class="sxs-lookup"><span data-stu-id="685a1-133">`Start`, `Stop`, `Suspend`, `Resume`, or `Transfer`</span></span>|
|`All`|<span data-ttu-id="685a1-134">允許所有訊息。</span><span class="sxs-lookup"><span data-stu-id="685a1-134">All messages are allowed.</span></span>|
|`Off`|<span data-ttu-id="685a1-135">封鎖所有訊息。</span><span class="sxs-lookup"><span data-stu-id="685a1-135">All messages are blocked.</span></span>|

> [!NOTE]
> <span data-ttu-id="685a1-136">`WriteEntry` 和 `WriteException` 方法都有未指定嚴重性層級的多載。</span><span class="sxs-lookup"><span data-stu-id="685a1-136">The `WriteEntry` and `WriteException` methods each have an overload that does not specify a severity level.</span></span> <span data-ttu-id="685a1-137">`WriteEntry` 多載的隱含嚴重性層級是 "Information"，而 `WriteException` 多載的隱含嚴重性層級是 "Error"。</span><span class="sxs-lookup"><span data-stu-id="685a1-137">The implicit severity level for the `WriteEntry` overload is "Information", and the implicit severity level for the `WriteException` overload is "Error".</span></span>

<span data-ttu-id="685a1-138">下表說明上一個範例中所顯示的記錄檔輸出︰使用 "Information" 的預設 `DefaultSwitch` 設定時，僅有第二個 `WriteEntry` 方法呼叫，以及 `WriteException` 方法呼叫會產生記錄檔輸出。</span><span class="sxs-lookup"><span data-stu-id="685a1-138">This table explains the log output shown in the previous example: with the default `DefaultSwitch` setting of "Information", only the second call to the `WriteEntry` method and the call to the `WriteException` method produce log output.</span></span>

#### <a name="to-log-only-activity-tracing-events"></a><span data-ttu-id="685a1-139">若只要記錄活動追蹤事件</span><span class="sxs-lookup"><span data-stu-id="685a1-139">To log only activity tracing events</span></span>

1. <span data-ttu-id="685a1-140">在方案總管中，以滑鼠右鍵按一下 app.config，並選取 [開啟]。\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="685a1-140">Right-click app.config in the **Solution Explorer** and select **Open**.</span></span>

     <span data-ttu-id="685a1-141">-或-</span><span class="sxs-lookup"><span data-stu-id="685a1-141">-or-</span></span>

     <span data-ttu-id="685a1-142">如果沒有 app.config 檔案︰</span><span class="sxs-lookup"><span data-stu-id="685a1-142">If there is no app.config file:</span></span>

    1. <span data-ttu-id="685a1-143">在 [ **專案** ] 功能表中，選擇 [ **加入新項目**]。</span><span class="sxs-lookup"><span data-stu-id="685a1-143">On the **Project** menu, choose **Add New Item**.</span></span>

    2. <span data-ttu-id="685a1-144">在 [加入新項目] \*\*\*\* 對話方塊中，選擇 [應用程式組態檔] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="685a1-144">From the **Add New Item** dialog box, choose **Application Configuration File**.</span></span>

    3. <span data-ttu-id="685a1-145">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="685a1-145">Click **Add**.</span></span>

2. <span data-ttu-id="685a1-146">找出位於最上層 `<configuration>` 區段中 `<system.diagnostics>` 區段的 `<switches>` 區段。</span><span class="sxs-lookup"><span data-stu-id="685a1-146">Locate the `<switches>` section, which is in the `<system.diagnostics>` section, which is in the top-level `<configuration>` section.</span></span>

3. <span data-ttu-id="685a1-147">尋找可將 `DefaultSwitch` 新增至參數集合的項目。</span><span class="sxs-lookup"><span data-stu-id="685a1-147">Find the element that adds `DefaultSwitch` to the collection of switches.</span></span> <span data-ttu-id="685a1-148">該項目應該與下列項目類似：</span><span class="sxs-lookup"><span data-stu-id="685a1-148">It should look similar to this element:</span></span>

     `<add name="DefaultSwitch" value="Information" />`

4. <span data-ttu-id="685a1-149">將 `value` 屬性值變更為 "ActivityTracing"。</span><span class="sxs-lookup"><span data-stu-id="685a1-149">Change the value of the `value` attribute to "ActivityTracing".</span></span>

5. <span data-ttu-id="685a1-150">App.config 檔案的內容應該類似下列 XML：</span><span class="sxs-lookup"><span data-stu-id="685a1-150">The content of the app.config file should be similar to the following XML:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <system.diagnostics>
        <sources>
          <!-- This section configures My.Application.Log -->
          <source name="DefaultSource" switchName="DefaultSwitch">
            <listeners>
              <add name="FileLog"/>
            </listeners>
          </source>
        </sources>
        <switches>
          <add name="DefaultSwitch" value="ActivityTracing" />
        </switches>
        <sharedListeners>
          <add name="FileLog"
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
                     Microsoft.VisualBasic, Version=8.0.0.0,
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,
                     processorArchitecture=MSIL"
               initializeData="FileLogWriter"/>
        </sharedListeners>
      </system.diagnostics>
    </configuration>
    ```

6. <span data-ttu-id="685a1-151">在偵錯工具中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-151">Run the application in the debugger.</span></span>

7. <span data-ttu-id="685a1-152">按下 **Button1**。</span><span class="sxs-lookup"><span data-stu-id="685a1-152">Press **Button1**.</span></span>

     <span data-ttu-id="685a1-153">應用程式會將下列資訊寫入應用程式的偵錯輸出與記錄檔中：</span><span class="sxs-lookup"><span data-stu-id="685a1-153">The application writes the following information to the application's debug output and log file:</span></span>

     `DefaultSource Start: 4 : Entering Button1_Click`

     `DefaultSource Stop: 5 : Leaving Button1_Click`

8. <span data-ttu-id="685a1-154">關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-154">Close the application.</span></span>

9. <span data-ttu-id="685a1-155">將 `value` 屬性值變更回 "Information"。</span><span class="sxs-lookup"><span data-stu-id="685a1-155">Change the value of the `value` attribute back to "Information".</span></span>

    > [!NOTE]
    > <span data-ttu-id="685a1-156">`DefaultSwitch` 參數設定只會控制 `My.Application.Log`。</span><span class="sxs-lookup"><span data-stu-id="685a1-156">The `DefaultSwitch` switch setting controls only `My.Application.Log`.</span></span> <span data-ttu-id="685a1-157">它不會變更 <xref:System.Diagnostics.Trace?displayProperty=nameWithType> 和 <xref:System.Diagnostics.Debug?displayProperty=nameWithType> 類別的行為。</span><span class="sxs-lookup"><span data-stu-id="685a1-157">It does not change how the .NET Framework <xref:System.Diagnostics.Trace?displayProperty=nameWithType> and <xref:System.Diagnostics.Debug?displayProperty=nameWithType> classes behave.</span></span>

## <a name="individual-filtering-for-myapplicationlog-listeners"></a><span data-ttu-id="685a1-158">個別篩選 My.Application.Log 接聽程式</span><span class="sxs-lookup"><span data-stu-id="685a1-158">Individual Filtering For My.Application.Log Listeners</span></span>

<span data-ttu-id="685a1-159">上一個範例示範如何變更所有 `My.Application.Log` 輸出的篩選。</span><span class="sxs-lookup"><span data-stu-id="685a1-159">The previous example shows how to change the filtering for all `My.Application.Log` output.</span></span> <span data-ttu-id="685a1-160">此範例示範如何篩選個別的記錄檔接聽程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-160">This example demonstrates how to filter an individual log listener.</span></span> <span data-ttu-id="685a1-161">應用程式預設會有兩個接聽程式，以寫入應用程式的偵錯輸出和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="685a1-161">By default, an application has two listeners that write to the application's debug output and the log file.</span></span>

<span data-ttu-id="685a1-162">組態檔可讓每個記錄檔接聽程式都有一個篩選條件 (類似 `My.Application.Log` 的參數)，以控制記錄檔接聽程式的行為。</span><span class="sxs-lookup"><span data-stu-id="685a1-162">The configuration file controls the behavior of the log listeners by allowing each one to have a filter, which is similar to a switch for `My.Application.Log`.</span></span> <span data-ttu-id="685a1-163">僅有當記錄檔的 `DefaultSwitch` 和記錄檔接聽程式的篩選條件皆允許訊息的嚴重性時，記錄檔接聽程式才會輸出訊息。</span><span class="sxs-lookup"><span data-stu-id="685a1-163">A log listener will output a message only if the message's severity is allowed by both the log's `DefaultSwitch` and the log listener's filter.</span></span>

<span data-ttu-id="685a1-164">此範例示範如何設定新偵錯接聽程式的篩選，並將它新增至 `Log` 物件。</span><span class="sxs-lookup"><span data-stu-id="685a1-164">This example demonstrates how to configure filtering for a new debug listener and add it to the `Log` object.</span></span> <span data-ttu-id="685a1-165">您應該從 `Log` 物件移除預設的偵錯接聽程式，以保證偵錯訊息是來自新的偵錯接聽程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-165">The default debug listener should be removed from the `Log` object, so it is clear that the debug messages come from the new debug listener.</span></span>

#### <a name="to-log-only-activity-tracing-events"></a><span data-ttu-id="685a1-166">若只要記錄活動追蹤事件</span><span class="sxs-lookup"><span data-stu-id="685a1-166">To log only activity-tracing events</span></span>

1. <span data-ttu-id="685a1-167">在方案總管中，以滑鼠右鍵按一下 app.config，並選擇 [開啟]。\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="685a1-167">Right-click app.config in the **Solution Explorer** and choose **Open**.</span></span>

     <span data-ttu-id="685a1-168">\-或-</span><span class="sxs-lookup"><span data-stu-id="685a1-168">\-or-</span></span>

     <span data-ttu-id="685a1-169">如果沒有 app.config 檔案︰</span><span class="sxs-lookup"><span data-stu-id="685a1-169">If there is no app.config file:</span></span>

    1. <span data-ttu-id="685a1-170">在 [ **專案** ] 功能表中，選擇 [ **加入新項目**]。</span><span class="sxs-lookup"><span data-stu-id="685a1-170">On the **Project** menu, choose **Add New Item**.</span></span>

    2. <span data-ttu-id="685a1-171">在 [加入新項目] \*\*\*\* 對話方塊中，選擇 [應用程式組態檔] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="685a1-171">From the **Add New Item** dialog box, choose **Application Configuration File**.</span></span>

    3. <span data-ttu-id="685a1-172">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="685a1-172">Click **Add**.</span></span>

2. <span data-ttu-id="685a1-173">在方案總管中，以滑鼠右鍵按一下 app.config。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="685a1-173">Right-click app.config in **Solution Explorer**.</span></span> <span data-ttu-id="685a1-174">選擇 [開啟]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="685a1-174">Choose **Open**.</span></span>

3. <span data-ttu-id="685a1-175">找出 `<listeners>` 區段，其位於具有 `name` 屬性 "DefaultSource" 之 `<source>` 區段中的 `<sources>` 區段下方。</span><span class="sxs-lookup"><span data-stu-id="685a1-175">Locate the `<listeners>` section, in the `<source>` section with the `name` attribute "DefaultSource", which is under the `<sources>` section.</span></span> <span data-ttu-id="685a1-176">`<sources>` 區段位於最上層 `<configuration>` 區段中的 `<system.diagnostics>` 區段下方。</span><span class="sxs-lookup"><span data-stu-id="685a1-176">The `<sources>` section is under the `<system.diagnostics>` section, in the top-level `<configuration>` section.</span></span>

4. <span data-ttu-id="685a1-177">將此項目新增至 `<listeners>` 區段：</span><span class="sxs-lookup"><span data-stu-id="685a1-177">Add this element to the `<listeners>` section:</span></span>

    ```xml
    <!-- Remove the default debug listener. -->
    <remove name="Default"/>
    <!-- Add a filterable debug listener. -->
    <add name="NewDefault"/>
    ```

5. <span data-ttu-id="685a1-178">找出位於最上層 `<sharedListeners>` 區段中 `<system.diagnostics>` 區段的 `<configuration>` 區段。</span><span class="sxs-lookup"><span data-stu-id="685a1-178">Locate the `<sharedListeners>` section, in the `<system.diagnostics>` section, in the top-level `<configuration>` section.</span></span>

6. <span data-ttu-id="685a1-179">將此項目加入至該 `<sharedListeners>` 區段︰</span><span class="sxs-lookup"><span data-stu-id="685a1-179">Add this element to that `<sharedListeners>` section:</span></span>

    ```xml
    <add name="NewDefault"
         type="System.Diagnostics.DefaultTraceListener,
               System, Version=2.0.0.0, Culture=neutral,
               PublicKeyToken=b77a5c561934e089,
               processorArchitecture=MSIL">
        <filter type="System.Diagnostics.EventTypeFilter"
                initializeData="Error" />
    </add>
    ```

     <span data-ttu-id="685a1-180"><xref:System.Diagnostics.EventTypeFilter> 篩選會採用 <xref:System.Diagnostics.SourceLevels> 列舉值之一作為其 `initializeData` 屬性。</span><span class="sxs-lookup"><span data-stu-id="685a1-180">The <xref:System.Diagnostics.EventTypeFilter> filter takes one of the <xref:System.Diagnostics.SourceLevels> enumeration values as its `initializeData` attribute.</span></span>

7. <span data-ttu-id="685a1-181">App.config 檔案的內容應該類似下列 XML：</span><span class="sxs-lookup"><span data-stu-id="685a1-181">The content of the app.config file should be similar to the following XML:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <system.diagnostics>
        <sources>
          <!-- This section configures My.Application.Log -->
          <source name="DefaultSource" switchName="DefaultSwitch">
            <listeners>
              <add name="FileLog"/>
              <!-- Remove the default debug listener. -->
              <remove name="Default"/>
              <!-- Add a filterable debug listener. -->
              <add name="NewDefault"/>
            </listeners>
          </source>
        </sources>
        <switches>
          <add name="DefaultSwitch" value="Information" />
        </switches>
        <sharedListeners>
          <add name="FileLog"
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
                     Microsoft.VisualBasic, Version=8.0.0.0,
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,
                     processorArchitecture=MSIL"
               initializeData="FileLogWriter"/>
          <add name="NewDefault"
               type="System.Diagnostics.DefaultTraceListener,
                     System, Version=2.0.0.0, Culture=neutral,
                     PublicKeyToken=b77a5c561934e089,
                     processorArchitecture=MSIL">
            <filter type="System.Diagnostics.EventTypeFilter"
                    initializeData="Error" />
          </add>
        </sharedListeners>
      </system.diagnostics>
    </configuration>
    ```

8. <span data-ttu-id="685a1-182">在偵錯工具中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-182">Run the application in the debugger.</span></span>

9. <span data-ttu-id="685a1-183">按下 **Button1**。</span><span class="sxs-lookup"><span data-stu-id="685a1-183">Press **Button1**.</span></span>

     <span data-ttu-id="685a1-184">應用程式會將下列資訊寫入應用程式的記錄檔中：</span><span class="sxs-lookup"><span data-stu-id="685a1-184">The application writes the following information to the application's log file:</span></span>

     `Default Information: 0 : In Button1_Click`

     `Default Error: 2 : Error in the application.`

     <span data-ttu-id="685a1-185">由於篩選更加嚴格，因此應用程式會將較少資訊寫入應用程式的偵錯輸出。</span><span class="sxs-lookup"><span data-stu-id="685a1-185">The application writes less information to the application's debug output because of the more restrictive filtering.</span></span>

     `Default Error   2   Error`

10. <span data-ttu-id="685a1-186">關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="685a1-186">Close the application.</span></span>

<span data-ttu-id="685a1-187">如需在部署後變更記錄檔設定的詳細資訊，請參閱[使用應用程式記錄檔](working-with-application-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="685a1-187">For more information about changing log settings after deployment, see [Working with Application Logs](working-with-application-logs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="685a1-188">另請參閱</span><span class="sxs-lookup"><span data-stu-id="685a1-188">See also</span></span>

- [<span data-ttu-id="685a1-189">逐步解說：判斷 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="685a1-189">Walkthrough: Determining Where My.Application.Log Writes Information</span></span>](walkthrough-determining-where-my-application-log-writes-information.md)
- [<span data-ttu-id="685a1-190">逐步解說：變更 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="685a1-190">Walkthrough: Changing Where My.Application.Log Writes Information</span></span>](walkthrough-changing-where-my-application-log-writes-information.md)
- [<span data-ttu-id="685a1-191">逐步解說：建立自訂記錄檔接聽程式</span><span class="sxs-lookup"><span data-stu-id="685a1-191">Walkthrough: Creating Custom Log Listeners</span></span>](walkthrough-creating-custom-log-listeners.md)
- [<span data-ttu-id="685a1-192">作法：寫入記錄檔訊息</span><span class="sxs-lookup"><span data-stu-id="685a1-192">How to: Write Log Messages</span></span>](how-to-write-log-messages.md)
- [<span data-ttu-id="685a1-193">追蹤參數</span><span class="sxs-lookup"><span data-stu-id="685a1-193">Trace Switches</span></span>](../../../../framework/debug-trace-profile/trace-switches.md)
- [<span data-ttu-id="685a1-194">記錄來自應用程式的資訊</span><span class="sxs-lookup"><span data-stu-id="685a1-194">Logging Information from the Application</span></span>](index.md)

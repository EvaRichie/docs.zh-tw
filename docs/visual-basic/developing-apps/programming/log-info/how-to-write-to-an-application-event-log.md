---
title: 作法：寫入應用程式事件記錄檔
ms.date: 07/20/2015
helpviewer_keywords:
- Computer.EventLog element
- WriteEntry method [Visual Basic]
- My.Computer.EventLog element
- event logs, writing to
ms.assetid: cadbc8c1-87af-4746-934e-55b79a4f6e2b
ms.openlocfilehash: 298d6d85f8b21176b72db8e676617577eb03fada
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410032"
---
# <a name="how-to-write-to-an-application-event-log-visual-basic"></a><span data-ttu-id="1f83b-102">如何：寫入應用程式事件記錄檔 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1f83b-102">How to: Write to an Application Event Log (Visual Basic)</span></span>

<span data-ttu-id="1f83b-103">您可以使用 `My.Application.Log` 和 `My.Log` 物件寫入發生在應用程式中之事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1f83b-103">You can use the `My.Application.Log` and `My.Log` objects to write information about events that occur in your application.</span></span> <span data-ttu-id="1f83b-104">此範例示範如何設定事件記錄檔接聽程式，讓 `My.Application.Log` 將追蹤資訊寫入至應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1f83b-104">This example shows how to configure an event log listener so `My.Application.Log` writes tracing information to the Application event log.</span></span>

<span data-ttu-id="1f83b-105">您無法寫入至安全性記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1f83b-105">You cannot write to the Security log.</span></span> <span data-ttu-id="1f83b-106">要寫入至系統記錄檔，您必須是 LocalSystem 或 Administrator 帳戶的成員。</span><span class="sxs-lookup"><span data-stu-id="1f83b-106">In order to write to the System log, you must be a member of the LocalSystem or Administrator account.</span></span>

<span data-ttu-id="1f83b-107">若要檢視事件記錄檔，您可以使用 [伺服器總管] \*\*\*\* 或 [Windows 事件檢視器] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="1f83b-107">To view an event log, you can use **Server Explorer** or **Windows Event Viewer**.</span></span> <span data-ttu-id="1f83b-108">如需詳細資訊，請參閱 [ETW Events in the .NET Framework](../../../../framework/performance/etw-events.md)。</span><span class="sxs-lookup"><span data-stu-id="1f83b-108">For more information, see [ETW Events in the .NET Framework](../../../../framework/performance/etw-events.md).</span></span>

## <a name="to-add-and-configure-the-event-log-listener"></a><span data-ttu-id="1f83b-109">加入及設定事件記錄檔接聽程式</span><span class="sxs-lookup"><span data-stu-id="1f83b-109">To add and configure the event log listener</span></span>

1. <span data-ttu-id="1f83b-110">在 方案總管 中，以滑鼠右鍵按一下 app.config 並選擇 [開啟]。\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="1f83b-110">Right-click app.config in **Solution Explorer** and choose **Open**.</span></span>

    <span data-ttu-id="1f83b-111">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="1f83b-111">\- or -</span></span>

    <span data-ttu-id="1f83b-112">如果沒有 app.config 檔案，</span><span class="sxs-lookup"><span data-stu-id="1f83b-112">If there is no app.config file,</span></span>

    1. <span data-ttu-id="1f83b-113">在 [ **專案** ] 功能表中，選擇 [ **加入新項目**]。</span><span class="sxs-lookup"><span data-stu-id="1f83b-113">On the **Project** menu, choose **Add New Item**.</span></span>

    2. <span data-ttu-id="1f83b-114">在 [加入新項目] \*\*\*\* 對話方塊中，選擇 [應用程式組態檔] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="1f83b-114">From the **Add New Item** dialog box, choose **Application Configuration File**.</span></span>

    3. <span data-ttu-id="1f83b-115">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1f83b-115">Click **Add**.</span></span>

2. <span data-ttu-id="1f83b-116">在應用程式組態檔中找出 `<listeners>` 區段。</span><span class="sxs-lookup"><span data-stu-id="1f83b-116">Locate the `<listeners>` section in the application configuration file.</span></span>

    <span data-ttu-id="1f83b-117">您會找到名稱屬性為 "DefaultSource" 之 `<listeners>` 區段 (位於最上層 `<source>` 區段底下 `<system.diagnostics>` 區段中) 中的 `<configuration>` 區段。</span><span class="sxs-lookup"><span data-stu-id="1f83b-117">You will find the `<listeners>` section in the `<source>` section with the name attribute "DefaultSource", which is nested under the `<system.diagnostics>` section, which is nested under the top-level `<configuration>` section.</span></span>

3. <span data-ttu-id="1f83b-118">將此項目加入至該 `<listeners>` 區段︰</span><span class="sxs-lookup"><span data-stu-id="1f83b-118">Add this element to that `<listeners>` section:</span></span>

    ```xml
    <add name="EventLog"/>
    ```

4. <span data-ttu-id="1f83b-119">找出位於最上層 `<sharedListeners>` 區段中 `<system.diagnostics>` 區段的 `<configuration>` 區段。</span><span class="sxs-lookup"><span data-stu-id="1f83b-119">Locate the `<sharedListeners>` section, in the `<system.diagnostics>` section, in the top-level `<configuration>` section.</span></span>

5. <span data-ttu-id="1f83b-120">將此項目加入至該 `<sharedListeners>` 區段︰</span><span class="sxs-lookup"><span data-stu-id="1f83b-120">Add this element to that `<sharedListeners>` section:</span></span>

    ```xml
    <add name="EventLog"
        type="System.Diagnostics.EventLogTraceListener, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="APPLICATION_NAME"/>
    ```

    <span data-ttu-id="1f83b-121">以應用程式名稱取代 `APPLICATION_NAME` 。</span><span class="sxs-lookup"><span data-stu-id="1f83b-121">Replace `APPLICATION_NAME` with the name of your application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f83b-122">一般而言，應用程式僅將錯誤寫入至事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1f83b-122">Typically, an application writes only errors to the event log.</span></span> <span data-ttu-id="1f83b-123">如需篩選記錄檔輸出的相關資訊，請參閱 [Walkthrough: Filtering My.Application.Log Output](walkthrough-filtering-my-application-log-output.md)。</span><span class="sxs-lookup"><span data-stu-id="1f83b-123">For information on filtering log output, see [Walkthrough: Filtering My.Application.Log Output](walkthrough-filtering-my-application-log-output.md).</span></span>

## <a name="to-write-event-information-to-the-event-log"></a><span data-ttu-id="1f83b-124">將事件資訊寫入至事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="1f83b-124">To write event information to the event log</span></span>

<span data-ttu-id="1f83b-125">使用 `My.Application.Log.WriteEntry` 或 `My.Application.Log.WriteException` 方法，將資訊寫入事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1f83b-125">Use the `My.Application.Log.WriteEntry` or `My.Application.Log.WriteException` method to write information to the event log.</span></span> <span data-ttu-id="1f83b-126">如需詳細資訊，請參閱[如何：寫入記錄訊息](how-to-write-log-messages.md)和[如何：記錄例外狀況](how-to-log-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="1f83b-126">For more information, see [How to: Write Log Messages](how-to-write-log-messages.md) and [How to: Log Exceptions](how-to-log-exceptions.md).</span></span>

<span data-ttu-id="1f83b-127">設定組件的事件記錄檔接聽程式之後，接聽程式會接收從該組件寫入的所有訊息 `My.Application.Log` 。</span><span class="sxs-lookup"><span data-stu-id="1f83b-127">After you configure the event log listener for an assembly, it receives all messages that `My.Application.Log` writes from that assembly.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f83b-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f83b-128">See also</span></span>

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [<span data-ttu-id="1f83b-129">使用應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="1f83b-129">Working with Application Logs</span></span>](working-with-application-logs.md)
- [<span data-ttu-id="1f83b-130">作法：記錄例外狀況</span><span class="sxs-lookup"><span data-stu-id="1f83b-130">How to: Log Exceptions</span></span>](how-to-log-exceptions.md)
- [<span data-ttu-id="1f83b-131">逐步解說：判斷 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="1f83b-131">Walkthrough: Determining Where My.Application.Log Writes Information</span></span>](walkthrough-determining-where-my-application-log-writes-information.md)

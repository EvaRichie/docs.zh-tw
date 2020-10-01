---
title: 教學課程：建立 Windows 服務應用程式
description: 在本教學課程中，請在 Visual Studio 中建立 Windows 服務應用程式，以將訊息寫入至事件記錄檔。 新增功能、設定狀態、新增安裝程式等。
ms.date: 03/27/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows service applications, walkthroughs
- Windows service applications, creating
ms.assetid: e24d8a3d-edc6-485c-b6e0-5672d91fb607
ms.openlocfilehash: bbf9ab7d06c952aa2e076fc36c71f37f1bb10884
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608383"
---
# <a name="tutorial-create-a-windows-service-app"></a><span data-ttu-id="0805a-104">教學課程：建立 Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0805a-104">Tutorial: Create a Windows service app</span></span>

<span data-ttu-id="0805a-105">本文示範如何在 Visual Studio 中建立將訊息寫入事件記錄的 Windows 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-105">This article demonstrates how to create a Windows service app in Visual Studio that writes messages to an event log.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="0805a-106">建立服務</span><span class="sxs-lookup"><span data-stu-id="0805a-106">Create a service</span></span>

<span data-ttu-id="0805a-107">首先，請建立專案並設定服務正常運作所需的值。</span><span class="sxs-lookup"><span data-stu-id="0805a-107">To begin, create the project and set the values that are required for the service to function correctly.</span></span>

1. <span data-ttu-id="0805a-108">從 Visual Studio 的 [檔案]\*\*\*\* 功能表中，選取 [新增]\*\*\*\* > [專案]\*\*\*\* (或按 **Ctrl**+**Shift**+**N**)，開啟 [新增專案]\*\*\*\* 視窗。</span><span class="sxs-lookup"><span data-stu-id="0805a-108">From the Visual Studio **File** menu, select **New** > **Project** (or press **Ctrl**+**Shift**+**N**) to open the **New Project** window.</span></span>

2. <span data-ttu-id="0805a-109">巡覽至 [Windows 服務] (.NET Framework)\*\*\*\* 專案範本，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="0805a-109">Navigate to and select the **Windows Service (.NET Framework)** project template.</span></span> <span data-ttu-id="0805a-110">若要尋找它，請展開 [已安裝]\*\*\*\* 和 [Visual C#]\*\*\*\* 或 [Visual Basic]\*\*\*\*，然後選取 [Windows Desktop]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-110">To find it, expand **Installed** and **Visual C#** or **Visual Basic**, then select **Windows Desktop**.</span></span> <span data-ttu-id="0805a-111">或者，在右上方的搜尋方塊中輸入 *Windows Service*，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="0805a-111">Or, enter *Windows Service* in the search box on the upper right and press **Enter**.</span></span>

   ![Visual Studio 新增專案對話方塊中的 Windows 服務範本](./media/new-project-dialog.png)

   > [!NOTE]
   > <span data-ttu-id="0805a-113">如果您沒有看到 **Windows 服務** 範本，您可能需要安裝 **.net 桌面開發** 工作負載：</span><span class="sxs-lookup"><span data-stu-id="0805a-113">If you don't see the **Windows Service** template, you may need to install the **.NET desktop development** workload:</span></span>
   >
   > <span data-ttu-id="0805a-114">在 [新增專案]\*\*\*\* 對話方塊中，選取左下角的 [開啟 Visual Studio 安裝程式]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-114">In the **New Project** dialog, select **Open Visual Studio Installer** on the lower left.</span></span> <span data-ttu-id="0805a-115">選取 **.NET 桌面開發**工作負載，然後選取 [修改]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-115">Select the **.NET desktop development** workload, and then select **Modify**.</span></span>

3. <span data-ttu-id="0805a-116">針對 [名稱]\*\*\*\* 輸入 *MyNewService*，然後選取 [確定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-116">For **Name**, enter *MyNewService*, and then select **OK**.</span></span>

   <span data-ttu-id="0805a-117">[設計]\*\*\*\* 索引標籤隨即出現 (**Service1.cs [Design]** 或 **Service1.vb [Design]**)。</span><span class="sxs-lookup"><span data-stu-id="0805a-117">The **Design** tab appears (**Service1.cs [Design]** or **Service1.vb [Design]**).</span></span>

   <span data-ttu-id="0805a-118">專案範本會包含繼承自 <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> 且名為 `Service1` 的元件類別。</span><span class="sxs-lookup"><span data-stu-id="0805a-118">The project template includes a component class named `Service1` that inherits from <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType>.</span></span> <span data-ttu-id="0805a-119">其中包含大部分的基本服務程式碼，例如啟動服務的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0805a-119">It includes much of the basic service code, such as the code to start the service.</span></span>

## <a name="rename-the-service"></a><span data-ttu-id="0805a-120">重新命名服務</span><span class="sxs-lookup"><span data-stu-id="0805a-120">Rename the service</span></span>

<span data-ttu-id="0805a-121">將服務 **Service1** 重新命名為 **MyNewService**。</span><span class="sxs-lookup"><span data-stu-id="0805a-121">Rename the service from **Service1** to **MyNewService**.</span></span>

1. <span data-ttu-id="0805a-122">在 [方案總管]\*\*\*\* 中，選取 **Service1.cs** 或 **Service1.vb**，然後從捷徑功能表選擇 [重新命名]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-122">In **Solution Explorer**, select **Service1.cs**, or **Service1.vb**, and choose **Rename** from the shortcut menu.</span></span> <span data-ttu-id="0805a-123">將檔案重新命名為 **MyNewService.cs** 或 **MyNewService.vb**，然後按 **Enter**</span><span class="sxs-lookup"><span data-stu-id="0805a-123">Rename the file to **MyNewService.cs**, or **MyNewService.vb**, and then press **Enter**</span></span>

    <span data-ttu-id="0805a-124">快顯視窗隨即出現，詢問您是否要重新命名程式碼項目 *Service1* 的所有參考。</span><span class="sxs-lookup"><span data-stu-id="0805a-124">A pop-up window appears asking whether you would like to rename all references to the code element *Service1*.</span></span>

2. <span data-ttu-id="0805a-125">在快顯視窗中，選取 [是]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-125">In the pop-up window, select **Yes**.</span></span>

    <span data-ttu-id="0805a-126">![重新命名提示](./media/windows-service-rename.png "Windows 服務重新命名提示")</span><span class="sxs-lookup"><span data-stu-id="0805a-126">![Rename prompt](./media/windows-service-rename.png "Windows service rename prompt")</span></span>

3. <span data-ttu-id="0805a-127">在 [設計]\*\*\*\* 索引標籤中，從捷徑功能表選取 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-127">In the **Design** tab, select **Properties** from the shortcut menu.</span></span> <span data-ttu-id="0805a-128">從 [屬性]\*\*\*\* 視窗中，將 **ServiceName** 值變更為 *MyNewService*。</span><span class="sxs-lookup"><span data-stu-id="0805a-128">From the **Properties** window, change the **ServiceName** value to *MyNewService*.</span></span>

    <span data-ttu-id="0805a-129">![服務屬性](./media/windows-service-properties.png "Windows 服務屬性")</span><span class="sxs-lookup"><span data-stu-id="0805a-129">![Service properties](./media/windows-service-properties.png "Windows service properties")</span></span>

4. <span data-ttu-id="0805a-130">從 [檔案]\*\*\*\* 功能表中選取 [全部儲存]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-130">Select **Save All** from the **File** menu.</span></span>

## <a name="add-features-to-the-service"></a><span data-ttu-id="0805a-131">在服務中新增功能</span><span class="sxs-lookup"><span data-stu-id="0805a-131">Add features to the service</span></span>

<span data-ttu-id="0805a-132">在本節中，您要將自訂事件記錄檔加入 Windows 服務中。</span><span class="sxs-lookup"><span data-stu-id="0805a-132">In this section, you add a custom event log to the Windows service.</span></span> <span data-ttu-id="0805a-133"><xref:System.Diagnostics.EventLog> 元件是您可新增至 Windows 服務的元件類型範例。</span><span class="sxs-lookup"><span data-stu-id="0805a-133">The <xref:System.Diagnostics.EventLog> component is an example of the type of component you can add to a Windows service.</span></span>

### <a name="add-custom-event-log-functionality"></a><span data-ttu-id="0805a-134">新增自訂事件記錄功能</span><span class="sxs-lookup"><span data-stu-id="0805a-134">Add custom event log functionality</span></span>

1. <span data-ttu-id="0805a-135">在 [方案總管]\*\*\*\* 中，從 **MyNewService.cs** 或 **MyNewService.vb** 的捷徑功能表選擇 [檢視表設計師]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-135">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Designer**.</span></span>

2. <span data-ttu-id="0805a-136">在 [工具箱]\*\*\*\* 中，展開 [元件]\*\*\*\*，然後將 [事件記錄檔]\*\*\*\* 元件拖曳至 [Service1.cs [Design]]\*\*\*\* 或 [Service1.vb [Design]]\*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0805a-136">In **Toolbox**, expand **Components**, and then drag the **EventLog** component to the **Service1.cs [Design]**, or **Service1.vb [Design]** tab.</span></span>

3. <span data-ttu-id="0805a-137">在 [方案總管]\*\*\*\* 中，從 **MyNewService.cs** 或 **MyNewService.vb** 的捷徑功能表選擇 [檢視程式碼]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-137">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Code**.</span></span>

4. <span data-ttu-id="0805a-138">定義自訂的事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0805a-138">Define a custom event log.</span></span> <span data-ttu-id="0805a-139">針對C#，編輯現有的 `MyNewService()` 建構函式；針對 Visual Basic，新增 `New()` 建構函式：</span><span class="sxs-lookup"><span data-stu-id="0805a-139">For C#, edit the existing `MyNewService()` constructor; for Visual Basic, add the `New()` constructor:</span></span>

   [!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#2)]
   [!code-vb[VbRadconService#2](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#2)]

5. <span data-ttu-id="0805a-140">針對 <xref:System.Diagnostics?displayProperty=nameWithType> 命名空間，將 `using` 陳述式新增至 **MyNewService.cs** (如果它尚未存在)，或將 `Imports` 陳述式新增至 **MyNewService.vb**：</span><span class="sxs-lookup"><span data-stu-id="0805a-140">Add a `using` statement to **MyNewService.cs** (if it doesn't already exist), or an `Imports` statement **MyNewService.vb**, for the <xref:System.Diagnostics?displayProperty=nameWithType> namespace:</span></span>

    ```csharp
    using System.Diagnostics;
    ```

    ```vb
    Imports System.Diagnostics
    ```

6. <span data-ttu-id="0805a-141">從 [檔案]\*\*\*\* 功能表中選取 [全部儲存]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-141">Select **Save All** from the **File** menu.</span></span>

### <a name="define-what-occurs-when-the-service-starts"></a><span data-ttu-id="0805a-142">定義服務啟動時所執行的動作</span><span class="sxs-lookup"><span data-stu-id="0805a-142">Define what occurs when the service starts</span></span>

<span data-ttu-id="0805a-143">在 **MyNewService.cs** 或 **MyNewService.vb** 的程式碼編輯器中，找到 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法；Visual Studio 會在您建立專案時，自動建立空白的方法定義。</span><span class="sxs-lookup"><span data-stu-id="0805a-143">In the code editor for **MyNewService.cs** or **MyNewService.vb**, locate the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method; Visual Studio automatically created an empty method definition when you created the project.</span></span> <span data-ttu-id="0805a-144">新增程式碼，在服務啟動時將項目寫入事件記錄檔：</span><span class="sxs-lookup"><span data-stu-id="0805a-144">Add code that writes an entry to the event log when the service starts:</span></span>

[!code-csharp[VbRadconService#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#3)]
[!code-vb[VbRadconService#3](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#3)]

#### <a name="polling"></a><span data-ttu-id="0805a-145">輪詢</span><span class="sxs-lookup"><span data-stu-id="0805a-145">Polling</span></span>

<span data-ttu-id="0805a-146">因為服務應用程式設計為長時間執行，所以通常會輪詢或監視系統，它是您使用 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法設定的。</span><span class="sxs-lookup"><span data-stu-id="0805a-146">Because a service application is designed to be long-running, it usually polls or monitors the system, which you set up in the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method.</span></span> <span data-ttu-id="0805a-147">`OnStart` 方法必須在服務作業開始後返回作業系統，這樣才不會封鎖系統。</span><span class="sxs-lookup"><span data-stu-id="0805a-147">The `OnStart` method must return to the operating system after the service's operation has begun so that the system isn't blocked.</span></span>

<span data-ttu-id="0805a-148">若要設定簡單的輪詢機制，請使用 <xref:System.Timers.Timer?displayProperty=nameWithType> 元件。</span><span class="sxs-lookup"><span data-stu-id="0805a-148">To set up a simple polling mechanism, use the <xref:System.Timers.Timer?displayProperty=nameWithType> component.</span></span> <span data-ttu-id="0805a-149">計時器會按固定的間隔引發 <xref:System.Timers.Timer.Elapsed> 事件，您的服務可在這段時間執行監視作業。</span><span class="sxs-lookup"><span data-stu-id="0805a-149">The timer raises an <xref:System.Timers.Timer.Elapsed> event at regular intervals, at which time your service can do its monitoring.</span></span> <span data-ttu-id="0805a-150">您使用 <xref:System.Timers.Timer> 元件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0805a-150">You use the <xref:System.Timers.Timer> component as follows:</span></span>

- <span data-ttu-id="0805a-151">設定 `MyNewService.OnStart` 方法中的 <xref:System.Timers.Timer> 元件屬性。</span><span class="sxs-lookup"><span data-stu-id="0805a-151">Set the properties of the <xref:System.Timers.Timer> component in the `MyNewService.OnStart` method.</span></span>
- <span data-ttu-id="0805a-152">呼叫 <xref:System.Timers.Timer.Start%2A> 方法來啟動計時器。</span><span class="sxs-lookup"><span data-stu-id="0805a-152">Start the timer by calling the <xref:System.Timers.Timer.Start%2A> method.</span></span>

##### <a name="set-up-the-polling-mechanism"></a><span data-ttu-id="0805a-153">設定輪詢機制。</span><span class="sxs-lookup"><span data-stu-id="0805a-153">Set up the polling mechanism.</span></span>

1. <span data-ttu-id="0805a-154">在 `MyNewService.OnStart` 事件中新增下列程式碼來設定輪詢機制：</span><span class="sxs-lookup"><span data-stu-id="0805a-154">Add the following code in the `MyNewService.OnStart` event to set up the polling mechanism:</span></span>

   ```csharp
   // Set up a timer that triggers every minute.
   Timer timer = new Timer();
   timer.Interval = 60000; // 60 seconds
   timer.Elapsed += new ElapsedEventHandler(this.OnTimer);
   timer.Start();
   ```

   ```vb
   ' Set up a timer that triggers every minute.
   Dim timer As Timer = New Timer()
   timer.Interval = 60000 ' 60 seconds
   AddHandler timer.Elapsed, AddressOf Me.OnTimer
   timer.Start()
   ```

2. <span data-ttu-id="0805a-155">針對 <xref:System.Timers?displayProperty=nameWithType> 命名空間，將 `using` 陳述式新增至 **MyNewService.cs**，或將 `Imports` 陳述式新增至 **MyNewService.vb**：</span><span class="sxs-lookup"><span data-stu-id="0805a-155">Add a `using` statement to **MyNewService.cs**, or an `Imports` statement to **MyNewService.vb**, for the <xref:System.Timers?displayProperty=nameWithType> namespace:</span></span>

   ```csharp
   using System.Timers;
   ```

   ```vb
   Imports System.Timers
   ```

3. <span data-ttu-id="0805a-156">在 `MyNewService` 類別中，新增 `OnTimer` 方法以處理 <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> 事件：</span><span class="sxs-lookup"><span data-stu-id="0805a-156">In the `MyNewService` class, add the `OnTimer` method to handle the <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> event:</span></span>

   ```csharp
   public void OnTimer(object sender, ElapsedEventArgs args)
   {
       // TODO: Insert monitoring activities here.
       eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId++);
   }
   ```

   ```vb
   Private Sub OnTimer(sender As Object, e As Timers.ElapsedEventArgs)
      ' TODO: Insert monitoring activities here.
      eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId)
      eventId = eventId + 1
   End Sub
   ```

4. <span data-ttu-id="0805a-157">在 `MyNewService` 類別中，新增成員變數。</span><span class="sxs-lookup"><span data-stu-id="0805a-157">In the `MyNewService` class, add a member variable.</span></span> <span data-ttu-id="0805a-158">它會包含要寫入事件記錄檔之下個事件的識別碼：</span><span class="sxs-lookup"><span data-stu-id="0805a-158">It contains the identifier of the next event to write into the event log:</span></span>

   ```csharp
   private int eventId = 1;
   ```

   ```vb
   Private eventId As Integer = 1
   ```

<span data-ttu-id="0805a-159">您可能會使用背景工作執行緒來執行工作，而不是在主執行緒上執行所有工作。</span><span class="sxs-lookup"><span data-stu-id="0805a-159">Instead of running all your work on the main thread, you can run tasks by using background worker threads.</span></span> <span data-ttu-id="0805a-160">如需詳細資訊，請參閱<xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>。</span><span class="sxs-lookup"><span data-stu-id="0805a-160">For more information, see <xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>.</span></span>

### <a name="define-what-occurs-when-the-service-is-stopped"></a><span data-ttu-id="0805a-161">定義服務停止時所執行的動作</span><span class="sxs-lookup"><span data-stu-id="0805a-161">Define what occurs when the service is stopped</span></span>

<span data-ttu-id="0805a-162">在 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 方法插入一行程式碼，以在服務停止時於事件記錄檔中新增項目：</span><span class="sxs-lookup"><span data-stu-id="0805a-162">Insert a line of code in the <xref:System.ServiceProcess.ServiceBase.OnStop%2A> method that adds an entry to the event log when the service is stopped:</span></span>

[!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#4)]
[!code-vb[VbRadconService#4](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#4)]

### <a name="define-other-actions-for-the-service"></a><span data-ttu-id="0805a-163">為服務定義其他動作</span><span class="sxs-lookup"><span data-stu-id="0805a-163">Define other actions for the service</span></span>

<span data-ttu-id="0805a-164">您可以覆寫 <xref:System.ServiceProcess.ServiceBase.OnPause%2A>、<xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> 方法，以定義額外的元件處理方式。</span><span class="sxs-lookup"><span data-stu-id="0805a-164">You can override the <xref:System.ServiceProcess.ServiceBase.OnPause%2A>, <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>, and <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> methods to define additional processing for your component.</span></span>

<span data-ttu-id="0805a-165">下列程式碼示範如何在 `MyNewService` 類別中覆寫 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 方法：</span><span class="sxs-lookup"><span data-stu-id="0805a-165">The following code shows how you to override the <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> method in the `MyNewService` class:</span></span>

[!code-csharp[VbRadconService#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#5)]
[!code-vb[VbRadconService#5](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#5)]

## <a name="set-service-status"></a><span data-ttu-id="0805a-166">設定服務狀態</span><span class="sxs-lookup"><span data-stu-id="0805a-166">Set service status</span></span>

<span data-ttu-id="0805a-167">服務將它們的狀態報告給[服務控制管理員](/windows/desktop/Services/service-control-manager)，讓使用者也可以知道服務是否運作正常。</span><span class="sxs-lookup"><span data-stu-id="0805a-167">Services report their status to the [Service Control Manager](/windows/desktop/Services/service-control-manager) so that a user can tell whether a service is functioning correctly.</span></span> <span data-ttu-id="0805a-168">根據預設，繼承自 <xref:System.ServiceProcess.ServiceBase>服務會報告一組有限狀態設定，其中包括 SERVICE_STOPPED, SERVICE_PAUSED, and SERVICE_RUNNING。</span><span class="sxs-lookup"><span data-stu-id="0805a-168">By default, a service that inherits from <xref:System.ServiceProcess.ServiceBase> reports a limited set of status settings, which include SERVICE_STOPPED, SERVICE_PAUSED, and SERVICE_RUNNING.</span></span> <span data-ttu-id="0805a-169">如果服務需要一些時間才能啟動，則報告 SERVICE_START_PENDING 狀態會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="0805a-169">If a service takes a while to start up, it's useful to report a SERVICE_START_PENDING status.</span></span>

<span data-ttu-id="0805a-170">您也可以新增程式碼，呼叫 Windows [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) 函式，以實作 SERVICE_START_PENDING 和 SERVICE_STOP_PENDING 狀態設定。</span><span class="sxs-lookup"><span data-stu-id="0805a-170">You can implement the SERVICE_START_PENDING and SERVICE_STOP_PENDING status settings by adding code that calls the Windows [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) function.</span></span>

### <a name="implement-service-pending-status"></a><span data-ttu-id="0805a-171">實作服務暫止狀態</span><span class="sxs-lookup"><span data-stu-id="0805a-171">Implement service pending status</span></span>

1. <span data-ttu-id="0805a-172">針對 <xref:System.Runtime.InteropServices?displayProperty=nameWithType> 命名空間，將 `using` 陳述式新增至 **MyNewService.cs**，或將 `Imports` 陳述式新增至 **MyNewService.vb**：</span><span class="sxs-lookup"><span data-stu-id="0805a-172">Add a `using` statement to **MyNewService.cs**, or an `Imports` statement to **MyNewService.vb**, for the <xref:System.Runtime.InteropServices?displayProperty=nameWithType> namespace:</span></span>

    ```csharp
    using System.Runtime.InteropServices;
    ```

    ```vb
    Imports System.Runtime.InteropServices
    ```

2. <span data-ttu-id="0805a-173">將下列程式碼新增至 **MyNewService.cs** 或 **MyNewService.vb**，宣告 `ServiceState` 值及新增狀態結構，您會在平台叫用呼叫中用到它們：</span><span class="sxs-lookup"><span data-stu-id="0805a-173">Add the following code to **MyNewService.cs**, or **MyNewService.vb**, to declare the `ServiceState` values and to add a structure for the status, which you'll use in a platform invoke call:</span></span>

    ```csharp
    public enum ServiceState
    {
        SERVICE_STOPPED = 0x00000001,
        SERVICE_START_PENDING = 0x00000002,
        SERVICE_STOP_PENDING = 0x00000003,
        SERVICE_RUNNING = 0x00000004,
        SERVICE_CONTINUE_PENDING = 0x00000005,
        SERVICE_PAUSE_PENDING = 0x00000006,
        SERVICE_PAUSED = 0x00000007,
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct ServiceStatus
    {
        public int dwServiceType;
        public ServiceState dwCurrentState;
        public int dwControlsAccepted;
        public int dwWin32ExitCode;
        public int dwServiceSpecificExitCode;
        public int dwCheckPoint;
        public int dwWaitHint;
    };
    ```

    ```vb
    Public Enum ServiceState
        SERVICE_STOPPED = 1
        SERVICE_START_PENDING = 2
        SERVICE_STOP_PENDING = 3
        SERVICE_RUNNING = 4
        SERVICE_CONTINUE_PENDING = 5
        SERVICE_PAUSE_PENDING = 6
        SERVICE_PAUSED = 7
    End Enum

    <StructLayout(LayoutKind.Sequential)>
    Public Structure ServiceStatus
        Public dwServiceType As Long
        Public dwCurrentState As ServiceState
        Public dwControlsAccepted As Long
        Public dwWin32ExitCode As Long
        Public dwServiceSpecificExitCode As Long
        Public dwCheckPoint As Long
        Public dwWaitHint As Long
    End Structure
    ```

    > [!NOTE]
    > <span data-ttu-id="0805a-174">服務控制管理員會使用 `dwWaitHint` `dwCheckpoint` [SERVICE_STATUS 結構](/windows/win32/api/winsvc/ns-winsvc-service_status) 的和成員，來判斷要等待 Windows 服務啟動或關閉的時間長短。</span><span class="sxs-lookup"><span data-stu-id="0805a-174">The Service Control Manager uses the `dwWaitHint` and `dwCheckpoint` members of the [SERVICE_STATUS structure](/windows/win32/api/winsvc/ns-winsvc-service_status) to determine how much time to wait for a Windows service to start or shut down.</span></span> <span data-ttu-id="0805a-175">如果您的 `OnStart` 和 `OnStop` 方法需長時間執行，則服務可以使用遞增的 `dwCheckPoint` 值再次呼叫 `SetServiceStatus` 以要求更多時間。</span><span class="sxs-lookup"><span data-stu-id="0805a-175">If your `OnStart` and `OnStop` methods run long, your service can request more time by calling `SetServiceStatus` again with an incremented `dwCheckPoint` value.</span></span>

3. <span data-ttu-id="0805a-176">在 `MyNewService` 類別中，使用[平台叫用](../interop/consuming-unmanaged-dll-functions.md)宣告 [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) 函式：</span><span class="sxs-lookup"><span data-stu-id="0805a-176">In the `MyNewService` class, declare the [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) function by using [platform invoke](../interop/consuming-unmanaged-dll-functions.md):</span></span>

    ```csharp
    [DllImport("advapi32.dll", SetLastError = true)]
    private static extern bool SetServiceStatus(System.IntPtr handle, ref ServiceStatus serviceStatus);
    ```

    ```vb
    Declare Auto Function SetServiceStatus Lib "advapi32.dll" (ByVal handle As IntPtr, ByRef serviceStatus As ServiceStatus) As Boolean
    ```

4. <span data-ttu-id="0805a-177">若要實作 SERVICE_START_PENDING 狀態，請將下列程式碼新增至 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法的開頭：</span><span class="sxs-lookup"><span data-stu-id="0805a-177">To implement the SERVICE_START_PENDING status, add the following code to the beginning of the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method:</span></span>

    ```csharp
    // Update the service state to Start Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Start Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

5. <span data-ttu-id="0805a-178">將程式碼新增至 `OnStart` 方法的結尾處，將狀態設為 SERVICE_RUNNING：</span><span class="sxs-lookup"><span data-stu-id="0805a-178">Add code to the end of the `OnStart` method to set the status to SERVICE_RUNNING:</span></span>

    ```csharp
    // Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

6. <span data-ttu-id="0805a-179">(選擇性) 如果 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 是長時間執行的方法，請在 `OnStop` 方法中重複此程序。</span><span class="sxs-lookup"><span data-stu-id="0805a-179">(Optional) If <xref:System.ServiceProcess.ServiceBase.OnStop%2A> is a long-running method, repeat this procedure in the `OnStop` method.</span></span> <span data-ttu-id="0805a-180">實作 SERVICE_STOP_PENDING 狀態，並在 `OnStop` 方法結束前傳回 SERVICE_STOPPED 狀態。</span><span class="sxs-lookup"><span data-stu-id="0805a-180">Implement the SERVICE_STOP_PENDING status and return the SERVICE_STOPPED status before the `OnStop` method exits.</span></span>

   <span data-ttu-id="0805a-181">例如：</span><span class="sxs-lookup"><span data-stu-id="0805a-181">For example:</span></span>

    ```csharp
    // Update the service state to Stop Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);

    // Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Stop Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)

    ' Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

## <a name="add-installers-to-the-service"></a><span data-ttu-id="0805a-182">將安裝程式新增至服務</span><span class="sxs-lookup"><span data-stu-id="0805a-182">Add installers to the service</span></span>

<span data-ttu-id="0805a-183">您必須先安裝 Windows 服務向服務控制管理員登錄，才能執行此服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-183">Before you run a Windows service, you need to install it, which registers it with the Service Control Manager.</span></span> <span data-ttu-id="0805a-184">將安裝程式新增至專案，以處理登錄詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0805a-184">Add installers to your project to handle the registration details.</span></span>

1. <span data-ttu-id="0805a-185">在 [方案總管]\*\*\*\* 中，從 **MyNewService.cs** 或 **MyNewService.vb** 的捷徑功能表選擇 [檢視表設計師]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-185">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Designer**.</span></span>

2. <span data-ttu-id="0805a-186">在 [設計]\*\*\*\* 檢視中，選取背景區域，然後從捷徑功能表選擇 [新增安裝程式]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-186">In the **Design** view, select the background area, then choose **Add Installer** from the shortcut menu.</span></span>

     <span data-ttu-id="0805a-187">根據預設，Visual Studio 會將名為 `ProjectInstaller` 的元件類別新增至您的專案，此類別包含兩個安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-187">By default, Visual Studio adds a component class named `ProjectInstaller`, which contains two installers, to your project.</span></span> <span data-ttu-id="0805a-188">這些安裝程式適用於您的服務及該服務的相關聯流程。</span><span class="sxs-lookup"><span data-stu-id="0805a-188">These installers are for your service and for the service's associated process.</span></span>

3. <span data-ttu-id="0805a-189">在 **ProjectInstaller** 的 [設計]\*\*\*\* 檢視中，針對 Visual C# 專案選取 [serviceInstaller1]\*\*\*\*，或針對 Visual Basic 專案選取 [ServiceInstaller1]\*\*\*\*，然後從捷徑功能表選擇 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-189">In the **Design** view for **ProjectInstaller**, select **serviceInstaller1** for a Visual C# project, or **ServiceInstaller1** for a Visual Basic project, then choose **Properties** from the shortcut menu.</span></span>

4. <span data-ttu-id="0805a-190">在 [屬性]\*\*\*\* 視窗中，驗證 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 屬性已設為 **MyNewService**。</span><span class="sxs-lookup"><span data-stu-id="0805a-190">In the **Properties** window, verify the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property is set to **MyNewService**.</span></span>

5. <span data-ttu-id="0805a-191">將文字新增至 <xref:System.ServiceProcess.ServiceInstaller.Description%2A> 屬性，例如「範例服務」\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-191">Add text to the <xref:System.ServiceProcess.ServiceInstaller.Description%2A> property, such as *A sample service*.</span></span>

     <span data-ttu-id="0805a-192">此文字會出現在 [服務]\*\*\*\* 視窗的 [描述]\*\*\*\* 欄中，向使用者說明服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-192">This text appears in the **Description** column of the **Services** window and describes the service to the user.</span></span>

    <span data-ttu-id="0805a-193">![服務視窗中的服務描述。](./media/windows-service-description.png "服務說明")</span><span class="sxs-lookup"><span data-stu-id="0805a-193">![Service description in the Services window.](./media/windows-service-description.png "Service description")</span></span>

6. <span data-ttu-id="0805a-194">將文字新增至 <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="0805a-194">Add text to the <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> property.</span></span> <span data-ttu-id="0805a-195">例如，「MyNewService 顯示名稱」\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-195">For example, *MyNewService Display Name*.</span></span>

     <span data-ttu-id="0805a-196">此文字會出現在 [服務]\*\*\*\* 視窗的 [顯示名稱]\*\*\*\* 欄中。</span><span class="sxs-lookup"><span data-stu-id="0805a-196">This text appears in the **Display Name** column of the **Services** window.</span></span> <span data-ttu-id="0805a-197">這個名稱可以和系統使用的 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 屬性名稱不同 (例如，您用於 `net start` 命令來啟動服務的名稱)。</span><span class="sxs-lookup"><span data-stu-id="0805a-197">This name can be different from the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property, which is the name the system uses (for example, the name you use for the `net start` command to start your service).</span></span>

7. <span data-ttu-id="0805a-198">從下拉式清單中將 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 屬性設為 <xref:System.ServiceProcess.ServiceStartMode.Automatic>。</span><span class="sxs-lookup"><span data-stu-id="0805a-198">Set the <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> property to <xref:System.ServiceProcess.ServiceStartMode.Automatic> from the drop-down list.</span></span>

8. <span data-ttu-id="0805a-199">完成後，[屬性]\*\*\*\* 視窗看起來應該如下圖：</span><span class="sxs-lookup"><span data-stu-id="0805a-199">When you're finished, the **Properties** windows should look like the following figure:</span></span>

     <span data-ttu-id="0805a-200">![Windows 服務的安裝程式屬性](./media/windows-service-installer-properties.png "Windows 服務安裝程式屬性")</span><span class="sxs-lookup"><span data-stu-id="0805a-200">![Installer Properties for a Windows service](./media/windows-service-installer-properties.png "Windows service installer properties")</span></span>

9. <span data-ttu-id="0805a-201">在 **ProjectInstaller** 的 [設計]\*\*\*\* 檢視中，針對 Visual C# 專案選擇 **serviceProcessInstaller1**，或針對 Visual Basic 專案選擇 **ServiceProcessInstaller1**，然後從捷徑功能表選擇 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-201">In the **Design** view for **ProjectInstaller**, choose **serviceProcessInstaller1** for a Visual C# project, or **ServiceProcessInstaller1** for a Visual Basic project, then choose **Properties** from the shortcut menu.</span></span> <span data-ttu-id="0805a-202">從下拉式清單中將 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 屬性設為 <xref:System.ServiceProcess.ServiceAccount.LocalSystem>。</span><span class="sxs-lookup"><span data-stu-id="0805a-202">Set the <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> property to <xref:System.ServiceProcess.ServiceAccount.LocalSystem> from the drop-down list.</span></span>

     <span data-ttu-id="0805a-203">此設定會安裝服務，並使用本機系統帳戶來加以執行。</span><span class="sxs-lookup"><span data-stu-id="0805a-203">This setting installs the service and runs it by using the local system account.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0805a-204"><xref:System.ServiceProcess.ServiceAccount.LocalSystem> 帳戶具有概括性的使用權限，包括寫入事件記錄檔的能力。</span><span class="sxs-lookup"><span data-stu-id="0805a-204">The <xref:System.ServiceProcess.ServiceAccount.LocalSystem> account has broad permissions, including the ability to write to the event log.</span></span> <span data-ttu-id="0805a-205">因此，請謹慎使用這個帳戶，因為它會增加您遭受惡意軟體攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="0805a-205">Use this account with caution, because it might increase your risk of attacks from malicious software.</span></span> <span data-ttu-id="0805a-206">至於其他工作，建議使用 <xref:System.ServiceProcess.ServiceAccount.LocalService> 帳戶，可在本機電腦上做為沒有權限的使用者，並提供匿名認證給任何遠端伺服器。</span><span class="sxs-lookup"><span data-stu-id="0805a-206">For other tasks, consider using the <xref:System.ServiceProcess.ServiceAccount.LocalService> account, which acts as a non-privileged user on the local computer and presents anonymous credentials to any remote server.</span></span> <span data-ttu-id="0805a-207">如果您嘗試使用 <xref:System.ServiceProcess.ServiceAccount.LocalService> 帳戶，因為需要寫入事件記錄檔的權限，所以這個範例會失敗。</span><span class="sxs-lookup"><span data-stu-id="0805a-207">This example fails if you try to use the <xref:System.ServiceProcess.ServiceAccount.LocalService> account, because it needs permission to write to the event log.</span></span>

<span data-ttu-id="0805a-208">如需安裝程式的詳細資訊，請參閱 [如何：將安裝程式新增至您的服務應用程式](how-to-add-installers-to-your-service-application.md)。</span><span class="sxs-lookup"><span data-stu-id="0805a-208">For more information about installers, see [How to: Add installers to your service application](how-to-add-installers-to-your-service-application.md).</span></span>

## <a name="optional-set-startup-parameters"></a><span data-ttu-id="0805a-209">(選擇性) 設定啟動參數</span><span class="sxs-lookup"><span data-stu-id="0805a-209">(Optional) Set startup parameters</span></span>

> [!NOTE]
> <span data-ttu-id="0805a-210">決定新增啟動參數之前，請考慮這是否為將資訊傳遞至服務的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="0805a-210">Before you decide to add startup parameters, consider whether it's the best way to pass information to your service.</span></span> <span data-ttu-id="0805a-211">雖然它們容易使用及剖析，且使用者也可以輕鬆覆寫它們，但在沒有文件時，使用者可能很難探索及使用它們。</span><span class="sxs-lookup"><span data-stu-id="0805a-211">Although they're easy to use and parse, and a user can easily override them, they might be harder for a user to discover and use without documentation.</span></span> <span data-ttu-id="0805a-212">一般而言，如果服務需要的不只是幾個啟動參數，則您應該考慮改用登錄或組態檔。</span><span class="sxs-lookup"><span data-stu-id="0805a-212">Generally, if your service requires more than just a few startup parameters, you should use the registry or a configuration file instead.</span></span>

<span data-ttu-id="0805a-213">Windows 服務可以接受命令列引數或啟動參數。</span><span class="sxs-lookup"><span data-stu-id="0805a-213">A Windows service can accept command-line arguments, or startup parameters.</span></span> <span data-ttu-id="0805a-214">當您新增程式碼以處理啟動參數時，使用者可在服務的 [屬性] 視窗中，以自己的自訂啟動參數來啟動服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-214">When you add code to process startup parameters, a user can start your service with their own custom startup parameters in the service properties window.</span></span> <span data-ttu-id="0805a-215">不過，這些啟動參數不會保留到下次服務啟動時。</span><span class="sxs-lookup"><span data-stu-id="0805a-215">However, these startup parameters aren't persisted the next time the service starts.</span></span> <span data-ttu-id="0805a-216">若要永久設定啟動參數，請在登錄中設定。</span><span class="sxs-lookup"><span data-stu-id="0805a-216">To set startup parameters permanently, set them in the registry.</span></span>

<span data-ttu-id="0805a-217">每項 Windows 服務在 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services** 子機碼下都有登錄項目。</span><span class="sxs-lookup"><span data-stu-id="0805a-217">Each Windows service has a registry entry under the **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services** subkey.</span></span> <span data-ttu-id="0805a-218">在每項服務的子機碼下，使用 **Parameters** 子機碼即可儲存您服務可以存取的資訊。</span><span class="sxs-lookup"><span data-stu-id="0805a-218">Under each service's subkey, use the **Parameters** subkey to store information that your service can access.</span></span> <span data-ttu-id="0805a-219">對於 Windows 服務，您可以用與其他類型的程式相同的方式來使用應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="0805a-219">You can use application configuration files for a Windows service the same way you do for other types of programs.</span></span> <span data-ttu-id="0805a-220">如需範例程式碼，請參閱 <xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="0805a-220">For sample code, see <xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType>.</span></span>

### <a name="to-add-startup-parameters"></a><span data-ttu-id="0805a-221">新增啟動參數</span><span class="sxs-lookup"><span data-stu-id="0805a-221">To add startup parameters</span></span>

1. <span data-ttu-id="0805a-222">選取 **Program.cs** 或 **MyNewService.Designer.vb**，然後從捷徑功能表選擇 [檢視程式碼]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-222">Select **Program.cs**, or **MyNewService.Designer.vb**, then choose **View Code** from the shortcut menu.</span></span> <span data-ttu-id="0805a-223">在 `Main` 方法中，變更程式碼以新增輸入參數，並將它傳遞至服務建構函式：</span><span class="sxs-lookup"><span data-stu-id="0805a-223">In the `Main` method, change the code to add an input parameter and pass it to the service constructor:</span></span>

   [!code-csharp[VbRadconService](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/Program-add-parameter.cs?highlight=1,6)]
   [!code-vb[VbRadconService](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.Designer-add-parameter.vb?highlight=1-2)]

2. <span data-ttu-id="0805a-224">在 **MyNewService.cs** 或 **MyNewService.vb** 中，變更 `MyNewService` 建構函式以處理輸入參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0805a-224">In **MyNewService.cs**, or **MyNewService.vb**, change the `MyNewService` constructor to process the input parameter as follows:</span></span>

   ```csharp
   using System.Diagnostics;

   public MyNewService(string[] args)
   {
       InitializeComponent();

       string eventSourceName = "MySource";
       string logName = "MyNewLog";

       if (args.Length > 0)
       {
          eventSourceName = args[0];
       }

       if (args.Length > 1)
       {
           logName = args[1];
       }

       eventLog1 = new EventLog();

       if (!EventLog.SourceExists(eventSourceName))
       {
           EventLog.CreateEventSource(eventSourceName, logName);
       }

       eventLog1.Source = eventSourceName;
       eventLog1.Log = logName;
   }
   ```

   ```vb
   Imports System.Diagnostics

   Public Sub New(ByVal cmdArgs() As String)
       InitializeComponent()
       Dim eventSourceName As String = "MySource"
       Dim logName As String = "MyNewLog"
       If (cmdArgs.Count() > 0) Then
           eventSourceName = cmdArgs(0)
       End If
       If (cmdArgs.Count() > 1) Then
           logName = cmdArgs(1)
       End If
       eventLog1 = New EventLog()
       If (Not EventLog.SourceExists(eventSourceName)) Then
           EventLog.CreateEventSource(eventSourceName, logName)
       End If
       eventLog1.Source = eventSourceName
       eventLog1.Log = logName
   End Sub
   ```

   <span data-ttu-id="0805a-225">此程式碼會根據使用者提供的啟動參數來設定事件來源和記錄檔名稱。</span><span class="sxs-lookup"><span data-stu-id="0805a-225">This code sets the event source and log name according to the startup parameters that the user supplies.</span></span> <span data-ttu-id="0805a-226">如未提供任何引數，則它會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="0805a-226">If no arguments are supplied, it uses default values.</span></span>

3. <span data-ttu-id="0805a-227">若要指定命令列引數，請將下列程式碼新增至 **ProjectInstaller.cs** 或 **ProjectInstaller.vb** 中的 `ProjectInstaller` 類別：</span><span class="sxs-lookup"><span data-stu-id="0805a-227">To specify the command-line arguments, add the following code to the `ProjectInstaller` class in **ProjectInstaller.cs**, or **ProjectInstaller.vb**:</span></span>

   ```csharp
   protected override void OnBeforeInstall(IDictionary savedState)
   {
       string parameter = "MySource1\" \"MyLogFile1";
       Context.Parameters["assemblypath"] = "\"" + Context.Parameters["assemblypath"] + "\" \"" + parameter + "\"";
       base.OnBeforeInstall(savedState);
   }
   ```

   ```vb
   Protected Overrides Sub OnBeforeInstall(ByVal savedState As IDictionary)
       Dim parameter As String = "MySource1"" ""MyLogFile1"
       Context.Parameters("assemblypath") = """" + Context.Parameters("assemblypath") + """ """ + parameter + """"
       MyBase.OnBeforeInstall(savedState)
   End Sub
   ```

   <span data-ttu-id="0805a-228">一般而言，這個值包含 Windows 服務的可執行檔完整路徑。</span><span class="sxs-lookup"><span data-stu-id="0805a-228">Typically, this value contains the full path to the executable for the Windows service.</span></span> <span data-ttu-id="0805a-229">使用者必須以引號括住路徑和每個個別參數，服務才能正確啟動。</span><span class="sxs-lookup"><span data-stu-id="0805a-229">For the service to start up correctly, the user must supply quotation marks for the path and each individual parameter.</span></span> <span data-ttu-id="0805a-230">使用者可以變更 **ImagePath** 登錄項目中的參數，以變更 Windows 服務的啟動參數。</span><span class="sxs-lookup"><span data-stu-id="0805a-230">A user can change the parameters in the **ImagePath** registry entry to change the startup parameters for the Windows service.</span></span> <span data-ttu-id="0805a-231">不過，更好的方法是以程式設計方式變更此值，並以使用者方便的方式公開功能，例如使用管理或組態公用程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-231">However, a better way is to change the value programmatically and expose the functionality in a user-friendly way, such as by using a management or configuration utility.</span></span>

## <a name="build-the-service"></a><span data-ttu-id="0805a-232">建置服務</span><span class="sxs-lookup"><span data-stu-id="0805a-232">Build the service</span></span>

1. <span data-ttu-id="0805a-233">在 [方案總管]\*\*\*\* 中，從 **MyNewService** 專案的捷徑功能表選擇 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-233">In **Solution Explorer**, choose **Properties** from the shortcut menu for the **MyNewService** project.</span></span>

   <span data-ttu-id="0805a-234">專案的屬性頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0805a-234">The property pages for your project appear.</span></span>

2. <span data-ttu-id="0805a-235">在 [應用程式]\*\*\*\* 索引標籤的 [啟始物件]\*\*\*\* 清單中，針對 Visual Basic 專案選擇 **MyNewService.Program** 或 **Sub Main**。</span><span class="sxs-lookup"><span data-stu-id="0805a-235">On the **Application** tab, in the **Startup object** list, choose **MyNewService.Program**, or **Sub Main** for Visual Basic projects.</span></span>

3. <span data-ttu-id="0805a-236">若要建置專案，請在 [方案總管]\*\*\*\* 中，從專案的捷徑功能表選擇 [建置]\*\*\*\* (或按 **Ctrl**+**Shift**+**B**)。</span><span class="sxs-lookup"><span data-stu-id="0805a-236">To build the project, in **Solution Explorer**, choose **Build** from the shortcut menu for your project (or press **Ctrl**+**Shift**+**B**).</span></span>

## <a name="install-the-service"></a><span data-ttu-id="0805a-237">安裝服務</span><span class="sxs-lookup"><span data-stu-id="0805a-237">Install the service</span></span>

<span data-ttu-id="0805a-238">建置 Windows 服務之後，您就可以安裝它了。</span><span class="sxs-lookup"><span data-stu-id="0805a-238">Now that you've built the Windows service, you can install it.</span></span> <span data-ttu-id="0805a-239">若要安裝 Windows 服務，您必須有安裝所在電腦的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="0805a-239">To install a Windows service, you must have administrator credentials on the computer where it's installed.</span></span>

1. <span data-ttu-id="0805a-240">以系統管理認證開啟 [Visual Studio 的開發人員命令提示字元][](../tools/developer-command-prompt-for-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="0805a-240">Open [Developer Command Prompt for Visual Studio](../tools/developer-command-prompt-for-vs.md) with administrative credentials.</span></span> <span data-ttu-id="0805a-241">從 Windows 的 [開始]\*\*\*\* 功能表選取 [Visual Studio] 資料夾的 [VS 2017 開發人員命令提示字元]\*\*\*\*，然後從捷徑功能表選取 [更多]\*\*\*\* > [以系統管理員身分執行]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-241">From the Windows **Start** menu, select **Developer Command Prompt for VS 2017** in the Visual Studio folder, then select **More** > **Run as Administrator** from the shortcut menu.</span></span>

2. <span data-ttu-id="0805a-242">在 [Visual Studio 開發人員命令提示字元]\*\*\*\* 視窗中，巡覽至包含專案輸出的資料夾 (預設為專案的 *\bin\Debug* 子目錄)。</span><span class="sxs-lookup"><span data-stu-id="0805a-242">In the **Developer Command Prompt for Visual Studio** window, navigate to the folder that contains your project's output (by default, the *\bin\Debug* subdirectory of your project).</span></span>

3. <span data-ttu-id="0805a-243">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="0805a-243">Enter the following command:</span></span>

    ```shell
    installutil MyNewService.exe
    ```

    <span data-ttu-id="0805a-244">如果服務安裝成功，則命令會報告成功。</span><span class="sxs-lookup"><span data-stu-id="0805a-244">If the service installs successfully, the command reports success.</span></span>

    <span data-ttu-id="0805a-245">如果系統找不到 *installutil.exe*，請確定它存在於您的電腦中。</span><span class="sxs-lookup"><span data-stu-id="0805a-245">If the system can't find *installutil.exe*, make sure that it exists on your computer.</span></span> <span data-ttu-id="0805a-246">此工具隨 .NET Framework 安裝到資料夾 \*%windir%\Microsoft.NET\Framework [64] \\ &lt; Framework 版本 &gt; \*。</span><span class="sxs-lookup"><span data-stu-id="0805a-246">This tool is installed with the .NET Framework to the folder *%windir%\Microsoft.NET\Framework[64]\\&lt;framework version&gt;*.</span></span> <span data-ttu-id="0805a-247">例如，64 位元版本的預設路徑是 *%windir%\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*。</span><span class="sxs-lookup"><span data-stu-id="0805a-247">For example, the default path for the 64-bit version is *%windir%\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*.</span></span>

    <span data-ttu-id="0805a-248">如果 **installutil.exe** 程序失敗，請檢查安裝記錄以找出原因。</span><span class="sxs-lookup"><span data-stu-id="0805a-248">If the **installutil.exe** process fails, check the install log to find out why.</span></span> <span data-ttu-id="0805a-249">根據預設，記錄檔與服務可執行檔位於同一資料夾。</span><span class="sxs-lookup"><span data-stu-id="0805a-249">By default, the log is in the same folder as the service executable.</span></span> <span data-ttu-id="0805a-250">安裝可能失敗的原因：</span><span class="sxs-lookup"><span data-stu-id="0805a-250">The installation can fail if:</span></span>
    - <span data-ttu-id="0805a-251"><xref:System.ComponentModel.RunInstallerAttribute> 類別不存在於 `ProjectInstaller` 類別中。</span><span class="sxs-lookup"><span data-stu-id="0805a-251">The <xref:System.ComponentModel.RunInstallerAttribute> class isn't present on the `ProjectInstaller` class.</span></span>
    - <span data-ttu-id="0805a-252">屬性未設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="0805a-252">The attribute isn't set to `true`.</span></span>
    - <span data-ttu-id="0805a-253">`ProjectInstaller` 類別未定義為 `public`。</span><span class="sxs-lookup"><span data-stu-id="0805a-253">The `ProjectInstaller` class isn't defined as `public`.</span></span>

<span data-ttu-id="0805a-254">如需詳細資訊，請參閱 [如何：安裝和卸載服務](how-to-install-and-uninstall-services.md)。</span><span class="sxs-lookup"><span data-stu-id="0805a-254">For more information, see [How to: Install and uninstall services](how-to-install-and-uninstall-services.md).</span></span>

## <a name="start-and-run-the-service"></a><span data-ttu-id="0805a-255">啟動並執行服務</span><span class="sxs-lookup"><span data-stu-id="0805a-255">Start and run the service</span></span>

1. <span data-ttu-id="0805a-256">在 Windows 中，開啟 [服務]\*\*\*\* 桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-256">In Windows, open the **Services** desktop app.</span></span> <span data-ttu-id="0805a-257">按**Windows** + **R**以開啟 [**執行**] 方塊，輸入*services.msc*，然後按**enter**鍵或選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="0805a-257">Press **Windows**+**R** to open the **Run** box, enter *services.msc*, and then press **Enter** or select **OK**.</span></span>

     <span data-ttu-id="0805a-258">您應該會看到您的服務列在 [服務]\*\*\*\* 中，並以您為其設定的顯示名稱按字母順序顯示。</span><span class="sxs-lookup"><span data-stu-id="0805a-258">You should see your service listed in **Services**, displayed alphabetically by the display name that you set for it.</span></span>

     ![在 [服務] 視窗中的 MyNewService。](./media/windowsservices-serviceswindow.PNG)

2. <span data-ttu-id="0805a-260">若要啟動服務，請從服務的捷徑功能表選擇 [啟動]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-260">To start the service, choose **Start** from the service's shortcut menu.</span></span>

3. <span data-ttu-id="0805a-261">若要停止服務，請從服務的捷徑功能表選擇 [停止]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-261">To stop the service, choose **Stop** from the service's shortcut menu.</span></span>

4. <span data-ttu-id="0805a-262">(選擇性) 在命令列中，使用 **net start &lt;服務名稱&gt;** 和 **net stop &lt;服務名稱&gt;** 命令來啟動和停止您的服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-262">(Optional) From the command line, use the commands **net start &lt;service name&gt;** and **net stop &lt;service name&gt;** to start and stop your service.</span></span>

### <a name="verify-the-event-log-output-of-your-service"></a><span data-ttu-id="0805a-263">確認服務的事件記錄輸出</span><span class="sxs-lookup"><span data-stu-id="0805a-263">Verify the event log output of your service</span></span>

1. <span data-ttu-id="0805a-264">在 Windows 中，開啟**事件檢視器**桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-264">In Windows, open the **Event Viewer** desktop app.</span></span> <span data-ttu-id="0805a-265">在 Windows 搜尋列中輸入*事件檢視器*，然後從搜尋結果選取 [事件檢視器]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-265">Enter *Event Viewer* in the Windows search bar, and then select **Event Viewer** from the search results.</span></span>

   > [!TIP]
   > <span data-ttu-id="0805a-266">在 Visual Studio 中，您可以從 [檢視]\*\*\*\* 功能表開啟 [伺服器總管]\*\*\*\* (或按 **Ctrl**+**Alt**+**S**)，然後展開本機電腦的 [事件記錄檔]\*\*\*\* 節點來存取事件記錄。</span><span class="sxs-lookup"><span data-stu-id="0805a-266">In Visual Studio, you can access event logs by opening **Server Explorer** from the **View** menu (or press **Ctrl**+**Alt**+**S**) and expanding the **Event Logs** node for the local computer.</span></span>

2. <span data-ttu-id="0805a-267">在 [事件檢視器]\*\*\*\* 中，展開 [應用程式及服務記錄]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-267">In **Event Viewer**, expand **Applications and Services Logs**.</span></span>

3. <span data-ttu-id="0805a-268">找到並展開 **MyNewLog** 的清單 (如果遵循新增命令列引數的程序，則為 **MyLogFile1**)。</span><span class="sxs-lookup"><span data-stu-id="0805a-268">Locate the listing for **MyNewLog** (or **MyLogFile1** if you followed the procedure to add command-line arguments) and expand it.</span></span> <span data-ttu-id="0805a-269">您應該會看到服務所執行兩個動作 (啟動和停止) 的項目。</span><span class="sxs-lookup"><span data-stu-id="0805a-269">You should see the entries for the two actions (start and stop) that your service performed.</span></span>

     ![使用事件檢視器查看事件記錄項目](./media/windows-service-event-viewer.png)

## <a name="clean-up-resources"></a><span data-ttu-id="0805a-271">清除資源</span><span class="sxs-lookup"><span data-stu-id="0805a-271">Clean up resources</span></span>

<span data-ttu-id="0805a-272">如果您不再需要 Windows 服務應用程式，您可以移除它。</span><span class="sxs-lookup"><span data-stu-id="0805a-272">If you no longer need the Windows service app, you can remove it.</span></span>

1. <span data-ttu-id="0805a-273">以系統管理認證開啟 [Visual Studio 的開發人員命令提示字元]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="0805a-273">Open **Developer Command Prompt for Visual Studio** with administrative credentials.</span></span>

2. <span data-ttu-id="0805a-274">在 [Visual Studio 開發人員命令提示字元]\*\*\*\* 視窗中，巡覽至包含專案輸出的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0805a-274">In the **Developer Command Prompt for Visual Studio** window, navigate to the folder that contains your project's output.</span></span>

3. <span data-ttu-id="0805a-275">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="0805a-275">Enter the following command:</span></span>

    ```shell
    installutil.exe /u MyNewService.exe
    ```

   <span data-ttu-id="0805a-276">如已成功解除安裝服務，命令會回報已成功移除您的服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-276">If the service uninstalls successfully, the command reports that your service was successfully removed.</span></span> <span data-ttu-id="0805a-277">如需詳細資訊，請參閱 [如何：安裝和卸載服務](how-to-install-and-uninstall-services.md)。</span><span class="sxs-lookup"><span data-stu-id="0805a-277">For more information, see [How to: Install and uninstall services](how-to-install-and-uninstall-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0805a-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0805a-278">Next steps</span></span>

<span data-ttu-id="0805a-279">建立服務之後，您就可以：</span><span class="sxs-lookup"><span data-stu-id="0805a-279">Now that you've created the service, you can:</span></span>

- <span data-ttu-id="0805a-280">建立獨立安裝程式，供其他人用來安裝您的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-280">Create a standalone setup program for others to use to install your Windows service.</span></span> <span data-ttu-id="0805a-281">使用 [WiX 工具組](https://wixtoolset.org/) 建立 Windows 服務的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0805a-281">Use the [WiX Toolset](https://wixtoolset.org/) to create an installer for a Windows service.</span></span> <span data-ttu-id="0805a-282">如需相關資訊，請參閱[建立安裝程式套件](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)。</span><span class="sxs-lookup"><span data-stu-id="0805a-282">For other ideas, see [Create an installer package](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop).</span></span>

- <span data-ttu-id="0805a-283">探索 <xref:System.ServiceProcess.ServiceController> 元件，它可讓您將命令傳送至已安裝的服務。</span><span class="sxs-lookup"><span data-stu-id="0805a-283">Explore the <xref:System.ServiceProcess.ServiceController> component, which enables you to send commands to the service you've installed.</span></span>

- <span data-ttu-id="0805a-284">在安裝應用程式時使用安裝程式建立事件記錄檔，而不是在應用程式執行時建立事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0805a-284">Instead of creating the event log when the application runs, use an installer to create an event log when you install the application.</span></span> <span data-ttu-id="0805a-285">當您解除安裝應用程式時，安裝程式會刪除事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0805a-285">The event log is deleted by the installer when you uninstall the application.</span></span> <span data-ttu-id="0805a-286">如需詳細資訊，請參閱<xref:System.Diagnostics.EventLogInstaller>。</span><span class="sxs-lookup"><span data-stu-id="0805a-286">For more information, see <xref:System.Diagnostics.EventLogInstaller>.</span></span>

## <a name="see-also"></a><span data-ttu-id="0805a-287">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0805a-287">See also</span></span>

- [<span data-ttu-id="0805a-288">Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0805a-288">Windows service applications</span></span>](index.md)
- [<span data-ttu-id="0805a-289">Windows 服務應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="0805a-289">Introduction to Windows service applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="0805a-290">如何：偵錯工具 Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0805a-290">How to: Debug Windows service applications</span></span>](how-to-debug-windows-service-applications.md)
- [<span data-ttu-id="0805a-291">服務 (Windows)</span><span class="sxs-lookup"><span data-stu-id="0805a-291">Services (Windows)</span></span>](/windows/desktop/Services/services)

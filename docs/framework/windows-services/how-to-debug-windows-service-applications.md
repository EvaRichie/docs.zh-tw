---
title: 作法：偵錯 Windows 服務應用程式
description: 瞭解如何對 Windows 服務應用程式進行 debug 錯，這並不像其他 Visual Studio 應用程式類型一樣簡單。
ms.date: 03/30/2017
helpviewer_keywords:
- debugging Windows Service applications
- debugging [Visual Studio], Windows services
- Windows NT services, debugging
- Windows Service applications, debugging
- services, debugging
ms.assetid: 63ab0800-0f05-4f1e-88e6-94c73fd920a2
ms.openlocfilehash: 4d8ac0316e47925d253e7220597ab9953252521e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270624"
---
# <a name="how-to-debug-windows-service-applications"></a><span data-ttu-id="7d4a3-103">作法：偵錯 Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="7d4a3-103">How to: Debug Windows Service Applications</span></span>

<span data-ttu-id="7d4a3-104">服務必須從服務控制管理員內容之中執行，而不是從 Visual Studio 之中執行。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-104">A service must be run from within the context of the Services Control Manager rather than from within Visual Studio.</span></span> <span data-ttu-id="7d4a3-105">因此，對服務進行偵錯不像是對其他 Visual Studio 應用程式類型進行偵錯那樣簡單直接。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-105">For this reason, debugging a service is not as straightforward as debugging other Visual Studio application types.</span></span> <span data-ttu-id="7d4a3-106">若要對服務進行偵錯，您必須啟動服務，然後將偵錯工具附加至執行中的處理序。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-106">To debug a service, you must start the service and then attach a debugger to the process in which it is running.</span></span> <span data-ttu-id="7d4a3-107">之後就可以使用 Visual Studio 所有的標準偵錯功能，對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-107">You can then debug your application by using all of the standard debugging functionality of Visual Studio.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="7d4a3-108">除非您知道處理序的內容，並了解附加至處理序以及可能會刪除該處理序的後果，否則就不應該附加至處理序。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-108">You should not attach to a process unless you know what the process is and understand the consequences of attaching to and possibly killing that process.</span></span> <span data-ttu-id="7d4a3-109">例如，如果您附加至 WinLogon 處理序，再停止偵錯，系統將會中止，因為系統沒有 WinLogon 就無法運作。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-109">For example, if you attach to the WinLogon process and then stop debugging, the system will halt because it can’t operate without WinLogon.</span></span>  
  
 <span data-ttu-id="7d4a3-110">您只可以將偵錯工具附加至執行中的服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-110">You can attach the debugger only to a running service.</span></span> <span data-ttu-id="7d4a3-111">附加程序會中斷服務的目前運作，但不會實際停止或暫停服務的處理。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-111">The attachment process interrupts the current functioning of your service; it doesn’t actually stop or pause the service's processing.</span></span> <span data-ttu-id="7d4a3-112">也就是說，當您開始偵錯時，如果您的服務正在執行，技術上來說，正在進行偵錯的服務還是處於啟動狀態，但已暫停其處理。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-112">That is, if your service is running when you begin debugging, it is still technically in the Started state as you debug it, but its processing has been suspended.</span></span>  
  
 <span data-ttu-id="7d4a3-113">附加至處理序之後，您可以設定中斷點，並使用這些中斷點對程式碼進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-113">After attaching to the process, you can set breakpoints and use these to debug your code.</span></span> <span data-ttu-id="7d4a3-114">一旦您結束用來附加至處理序的對話方塊，就會立即處於偵錯模式中。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-114">Once you exit the dialog box you use to attach to the process, you are effectively in debug mode.</span></span> <span data-ttu-id="7d4a3-115">您可以使用服務控制管理員來啟動、停止、暫停及繼續服務，以此方式來叫用您所設定的中斷點。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-115">You can use the Services Control Manager to start, stop, pause and continue your service, thus hitting the breakpoints you've set.</span></span> <span data-ttu-id="7d4a3-116">偵錯成功之後，您就可以移除這項虛擬服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-116">You can later remove this dummy service after debugging is successful.</span></span>  
  
 <span data-ttu-id="7d4a3-117">本文涵蓋對本機電腦上執行的服務進行偵錯，但您也可以對遠端電腦上執行的 Windows 服務進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-117">This article covers debugging a service that's running on the local computer, but you can also debug Windows Services that are running on a remote computer.</span></span> <span data-ttu-id="7d4a3-118">請參閱 [遠端偵錯](/visualstudio/debugger/debug-installed-app-package)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-118">See [Remote Debugging](/visualstudio/debugger/debug-installed-app-package).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7d4a3-119">對 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法進行偵錯可能是項困難的工作，因為服務控制管理員對於啟動服務的所有嘗試都強加上 30 秒的限制。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-119">Debugging the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method can be difficult because the Services Control Manager imposes a 30-second limit on all attempts to start a service.</span></span> <span data-ttu-id="7d4a3-120">如需詳細資訊，請參閱[疑難排解：對 Windows 服務進行偵錯](troubleshooting-debugging-windows-services.md)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-120">For more information, see [Troubleshooting: Debugging Windows Services](troubleshooting-debugging-windows-services.md).</span></span>  
  
> [!WARNING]
> <span data-ttu-id="7d4a3-121">若要取得有關偵錯的有意義資訊，Visual Studio 偵錯工具必須在符號檔中找到正在進行偵錯的二進位檔案。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-121">To get meaningful information for debugging, the Visual Studio debugger needs to find symbol files for the binaries that are being debugged.</span></span> <span data-ttu-id="7d4a3-122">如果您想要對建置於 Visual Studio 中的服務進行偵錯，符號檔 (.pdb 檔) 會與可執行檔或程式庫位於同一個資料夾中，並且偵錯工具會自動載入檔案。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-122">If you are debugging a service that you built in Visual Studio, the symbol files (.pdb files) are in the same folder as the executable or library, and the debugger loads them automatically.</span></span> <span data-ttu-id="7d4a3-123">如果您想要對非您所建置的服務進行偵錯，則應該先找到服務的符號，並確定偵錯工具可以找到這些符號。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-123">If you are debugging a service that you didn't build, you should first find symbols for the service and make sure they can be found by the debugger.</span></span> <span data-ttu-id="7d4a3-124">請參閱[在 Visual Studio 偵錯工具中指定符號 (.pdb) 和來源檔案](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-124">See [Specify Symbol (.pdb) and Source Files in the Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span></span> <span data-ttu-id="7d4a3-125">如果您想要對系統處理序進行偵錯，或想要在您的服務中有系統呼叫的符號，則應該加入 Microsoft 符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-125">If you're debugging a system process or want to have symbols for system calls in your services, you should add the Microsoft Symbol Servers.</span></span> <span data-ttu-id="7d4a3-126">請參閱[偵錯符號](/windows/desktop/DxTechArts/debugging-with-symbols) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-126">See [Debugging Symbols](/windows/desktop/DxTechArts/debugging-with-symbols).</span></span>  
  
### <a name="to-debug-a-service"></a><span data-ttu-id="7d4a3-127">偵錯服務</span><span class="sxs-lookup"><span data-stu-id="7d4a3-127">To debug a service</span></span>  
  
1. <span data-ttu-id="7d4a3-128">在偵錯組態中建置您的服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-128">Build your service in the Debug configuration.</span></span>  
  
2. <span data-ttu-id="7d4a3-129">安裝您的服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-129">Install your service.</span></span> <span data-ttu-id="7d4a3-130">如需詳細資訊，請參閱 [How to: Install and Uninstall Services](how-to-install-and-uninstall-services.md)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-130">For more information, see [How to: Install and Uninstall Services](how-to-install-and-uninstall-services.md).</span></span>  
  
3. <span data-ttu-id="7d4a3-131">從 [服務控制管理員]、[伺服器總管] 或從程式碼啟動您的服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-131">Start your service, either from **Services Control Manager**, **Server Explorer**, or from code.</span></span> <span data-ttu-id="7d4a3-132">如需詳細資訊，請參閱[如何：啟動服務](how-to-start-services.md)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-132">For more information, see [How to: Start Services](how-to-start-services.md).</span></span>  
  
4. <span data-ttu-id="7d4a3-133">使用系統管理認證啟動 Visual Studio，以便能夠附加至系統處理程序。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-133">Start Visual Studio with administrative credentials so you can attach to system processes.</span></span>  
  
5. <span data-ttu-id="7d4a3-134">(選擇性) 在 Visual Studio 功能表列上，選擇 [工具]、[選項]。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-134">(Optional) On the Visual Studio menu bar, choose **Tools**, **Options**.</span></span> <span data-ttu-id="7d4a3-135">在 [選項] 對話方塊中，選擇 [偵錯]、[符號]，選取 [Microsoft 符號伺服器] 核取方塊，然後選擇 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-135">In the **Options** dialog box, choose **Debugging**, **Symbols**, select the **Microsoft Symbol Servers** check box, and then choose the **OK** button.</span></span>  
  
6. <span data-ttu-id="7d4a3-136">在功能表列上，從 [偵錯] 或 [工具] 功能表中選擇 [附加至處理序]。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-136">On the menu bar, choose **Attach to Process** from the **Debug** or **Tools** menu.</span></span> <span data-ttu-id="7d4a3-137">(鍵盤：Ctrl+Alt+P)</span><span class="sxs-lookup"><span data-stu-id="7d4a3-137">(Keyboard: Ctrl+Alt+P)</span></span>  
  
     <span data-ttu-id="7d4a3-138">[處理序] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-138">The **Processes** dialog box appears.</span></span>  
  
7. <span data-ttu-id="7d4a3-139">選取 [顯示所有使用者的處理序] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-139">Select the **Show processes from all users** check box.</span></span>  
  
8. <span data-ttu-id="7d4a3-140">在 [可使用的處理序] 區段中，選擇服務的處理序，然後選擇 [附加]。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-140">In the **Available Processes** section, choose the process for your service, and then choose **Attach**.</span></span>  
  
    > [!TIP]
    > <span data-ttu-id="7d4a3-141">處理序的名稱和您的服務可執行檔名稱相同。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-141">The process will have the same name as the executable file for your service.</span></span>  
  
     <span data-ttu-id="7d4a3-142">[附加至處理序]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-142">The **Attach to Process** dialog box appears.</span></span>  
  
9. <span data-ttu-id="7d4a3-143">選擇適當選項，然後選擇 [確定] 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-143">Choose the appropriate options, and then choose **OK** to close the dialog box.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="7d4a3-144">您現在已處於偵錯模式中。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-144">You are now in debug mode.</span></span>  
  
10. <span data-ttu-id="7d4a3-145">在程式碼中設定任何想要使用的中斷點。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-145">Set any breakpoints you want to use in your code.</span></span>  
  
11. <span data-ttu-id="7d4a3-146">存取服務控制管理員並操作您的服務，傳送停止、暫停和繼續命令來叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-146">Access the Services Control Manager and manipulate your service, sending stop, pause, and continue commands to hit your breakpoints.</span></span> <span data-ttu-id="7d4a3-147">如需執行服務控制管理員的詳細資訊，請參閱[如何：啟動服務](how-to-start-services.md)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-147">For more information about running the Services Control Manager, see [How to: Start Services](how-to-start-services.md).</span></span> <span data-ttu-id="7d4a3-148">另請參閱[疑難排解：對 Windows 服務進行偵錯](troubleshooting-debugging-windows-services.md)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-148">Also, see [Troubleshooting: Debugging Windows Services](troubleshooting-debugging-windows-services.md).</span></span>  
  
## <a name="debugging-tips-for-windows-services"></a><span data-ttu-id="7d4a3-149">Windows 服務的偵錯秘訣</span><span class="sxs-lookup"><span data-stu-id="7d4a3-149">Debugging Tips for Windows Services</span></span>  

 <span data-ttu-id="7d4a3-150">附加至服務的處理序可讓您對大多數的服務程式碼進行偵錯，但並非所有的服務程式碼都可用這種方式偵錯。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-150">Attaching to the service's process allows you to debug most, but not all, the code for that service.</span></span> <span data-ttu-id="7d4a3-151">例如，由於已經啟動服務，因此您無法以這種方式對服務之 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法中的程式碼，或對用來載入服務之 `Main` 方法中的程式碼進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-151">For example, because the service has already been started, you cannot debug the code in the service's <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method or the code in the `Main` method that is used to load the service this way.</span></span> <span data-ttu-id="7d4a3-152">解決這個限制的其中一個方法，是在您的服務應用程式中，建立僅用於協助偵錯的第二個暫時性服務。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-152">One way to work around this limitation is to create a temporary second service in your service application that exists only to aid in debugging.</span></span> <span data-ttu-id="7d4a3-153">您可以安裝這兩項服務，然後再啟動這個虛擬服務以載入服務處理序。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-153">You can install both services, and then start this dummy service to load the service process.</span></span> <span data-ttu-id="7d4a3-154">一旦暫時性服務啟動了處理序，您就可以使用 Visual Studio 中的 [偵錯] 功能表來附加至服務處理序。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-154">Once the temporary service has started the process, you can use the **Debug** menu in Visual Studio to attach to the service process.</span></span>  
  
 <span data-ttu-id="7d4a3-155">嘗試加入對 <xref:System.Threading.Thread.Sleep%2A> 方法的呼叫，將動作延遲到能夠附加至處理序之後。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-155">Try adding calls to the <xref:System.Threading.Thread.Sleep%2A> method to delay action until you’re able to attach to the process.</span></span>  
  
 <span data-ttu-id="7d4a3-156">嘗試將程式變更為一般主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-156">Try changing the program to a regular console application.</span></span> <span data-ttu-id="7d4a3-157">若要執行這項操作，請依照下列方式重寫 `Main` 方法，以根據程式的啟動方式，將程式當做 Windows 服務或主控台應用程式來執行。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-157">To do this, rewrite the `Main` method as follows so it can run both as a Windows Service and as a console application, depending on how it's started.</span></span>  
  
#### <a name="how-to-run-a-windows-service-as-a-console-application"></a><span data-ttu-id="7d4a3-158">如何：將 Windows 服務當做主控台應用程式來執行</span><span class="sxs-lookup"><span data-stu-id="7d4a3-158">How to: Run a Windows Service as a console application</span></span>  
  
1. <span data-ttu-id="7d4a3-159">將方法加入執行 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 方法的服務：</span><span class="sxs-lookup"><span data-stu-id="7d4a3-159">Add a method to your service that runs the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> and <xref:System.ServiceProcess.ServiceBase.OnStop%2A> methods:</span></span>  
  
    ```csharp  
    internal void TestStartupAndStop(string[] args)  
    {  
        this.OnStart(args);  
        Console.ReadLine();  
        this.OnStop();  
    }  
    ```  
  
2. <span data-ttu-id="7d4a3-160">依照下列方式重寫 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="7d4a3-160">Rewrite the `Main` method as follows:</span></span>  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        if (Environment.UserInteractive)  
        {  
            MyNewService service1 = new MyNewService(args);  
            service1.TestStartupAndStop(args);  
        }  
        else  
        {  
            // Put the body of your old Main method here.  
        }  
    }
    ```  
  
3. <span data-ttu-id="7d4a3-161">在專案屬性的 [應用程式] 索引標籤中，將 [輸出類型] 設定為 [主控台應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-161">In the **Application** tab of the project's properties, set the **Output type** to **Console Application**.</span></span>  
  
4. <span data-ttu-id="7d4a3-162">選擇 [開始偵錯] (F5)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-162">Choose **Start Debugging** (F5).</span></span>  
  
5. <span data-ttu-id="7d4a3-163">若要再次將程式當做 Windows 服務來執行，請以適用於 Windows 服務的方式來安裝及啟動程式。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-163">To run the program as a Windows Service again, install it and start it as usual for a Windows Service.</span></span> <span data-ttu-id="7d4a3-164">您不需要回復這些變更。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-164">It's not necessary to reverse these changes.</span></span>  
  
 <span data-ttu-id="7d4a3-165">在某些情況下 (例如當您想要偵錯只在系統啟動時發生的問題時)，您必須使用 Windows 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-165">In some cases, such as when you want to debug an issue that occurs only on system startup, you have to use the Windows debugger.</span></span> <span data-ttu-id="7d4a3-166">[下載 Windows 驅動程式套件 (WDK)](/windows-hardware/drivers/download-the-wdk)，並參閱[如何偵錯 Windows 服務](https://support.microsoft.com/kb/824344)。</span><span class="sxs-lookup"><span data-stu-id="7d4a3-166">[Download the Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk) and see [How to debug Windows Services](https://support.microsoft.com/kb/824344).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7d4a3-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7d4a3-167">See also</span></span>

- [<span data-ttu-id="7d4a3-168">Windows 服務應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="7d4a3-168">Introduction to Windows Service Applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="7d4a3-169">作法：安裝和解除安裝服務</span><span class="sxs-lookup"><span data-stu-id="7d4a3-169">How to: Install and Uninstall Services</span></span>](how-to-install-and-uninstall-services.md)
- [<span data-ttu-id="7d4a3-170">作法：啟動服務</span><span class="sxs-lookup"><span data-stu-id="7d4a3-170">How to: Start Services</span></span>](how-to-start-services.md)
- [<span data-ttu-id="7d4a3-171">對服務進行偵錯</span><span class="sxs-lookup"><span data-stu-id="7d4a3-171">Debugging a Service</span></span>](/windows/desktop/Services/debugging-a-service)

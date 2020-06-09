---
title: ETW 追蹤
ms.date: 03/30/2017
ms.assetid: ac99a063-e2d2-40cc-b659-d23c2f783f92
ms.openlocfilehash: 0bdbf6699a0cfa3dce58abda4c989fb25d764459
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600554"
---
# <a name="etw-tracing"></a><span data-ttu-id="6b770-102">ETW 追蹤</span><span class="sxs-lookup"><span data-stu-id="6b770-102">ETW Tracing</span></span>
<span data-ttu-id="6b770-103">這個範例示範如何使用 Event Tracing for Windows (ETW) 和範例隨附的 `ETWTraceListener`，以實作端對端 (E2E) 追蹤。</span><span class="sxs-lookup"><span data-stu-id="6b770-103">This sample demonstrates how to implement End-to-End (E2E) tracing using Event Tracing for Windows (ETW) and the `ETWTraceListener` that is provided with this sample.</span></span> <span data-ttu-id="6b770-104">此範例是以[消費者入門](getting-started-sample.md)為基礎，並包含 ETW 追蹤。</span><span class="sxs-lookup"><span data-stu-id="6b770-104">The sample is based on the [Getting Started](getting-started-sample.md) and includes ETW tracing.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6b770-105">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="6b770-105">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="6b770-106">這個範例假設您已熟悉[追蹤和訊息記錄](tracing-and-message-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="6b770-106">This sample assumes that you are familiar with [Tracing and Message Logging](tracing-and-message-logging.md).</span></span>  
  
 <span data-ttu-id="6b770-107"><xref:System.Diagnostics> 追蹤模型中的每個追蹤來源都可以有多個追蹤接聽項，這些接聽項將決定追蹤資料的位置和方式。</span><span class="sxs-lookup"><span data-stu-id="6b770-107">Each trace source in the <xref:System.Diagnostics> tracing model can have multiple trace listeners that determine where and how the data is traced.</span></span> <span data-ttu-id="6b770-108">接聽項的類型會定義記錄追蹤資料的格式。</span><span class="sxs-lookup"><span data-stu-id="6b770-108">The type of listener defines the format in which trace data is logged.</span></span> <span data-ttu-id="6b770-109">下列程式碼範例示範如何將接聽項新增至組態。</span><span class="sxs-lookup"><span data-stu-id="6b770-109">The following code sample shows how to add the listener to configuration.</span></span>  
  
```xml  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel"
             switchValue="Verbose,ActivityTracing"  
             propagateActivity="true">  
            <listeners>  
                <add type=  
                   "System.Diagnostics.DefaultTraceListener"  
                   name="Default">  
                   <filter type="" />  
                </add>  
                <add name="ETW">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
        <add type=  
            "Microsoft.ServiceModel.Samples.EtwTraceListener, ETWTraceListener"  
            name="ETW" traceOutputOptions="Timestamp">  
            <filter type="" />  
       </add>  
    </sharedListeners>  
</system.diagnostics>  
```  
  
 <span data-ttu-id="6b770-110">使用這個接聽項之前，必須先啟動 ETW 追蹤工作階段。</span><span class="sxs-lookup"><span data-stu-id="6b770-110">Before using this listener, an ETW Trace Session must be started.</span></span> <span data-ttu-id="6b770-111">您可以使用 Logman.exe 或 Tracelog.exe 啟動這個工作階段。</span><span class="sxs-lookup"><span data-stu-id="6b770-111">This session can be started by using Logman.exe or Tracelog.exe.</span></span> <span data-ttu-id="6b770-112">此範例隨附可供您設定 ETW 追蹤工作階段的 SetupETW.bat 檔案，以及可用來關閉工作階段與完成記錄檔的 CleanupETW.bat 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b770-112">A SetupETW.bat file is included with this sample so that you can set up the ETW Trace Session along with a CleanupETW.bat file for closing the session and completing the log file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6b770-113">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="6b770-113">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span> <span data-ttu-id="6b770-114">如需這些工具的詳細資訊，請參閱<https://go.microsoft.com/fwlink/?LinkId=56580></span><span class="sxs-lookup"><span data-stu-id="6b770-114">For more information about these tools, see <https://go.microsoft.com/fwlink/?LinkId=56580></span></span>  
  
 <span data-ttu-id="6b770-115">使用 ETWTraceListener 時，追蹤會記錄在二進位的 .etl 檔案中。</span><span class="sxs-lookup"><span data-stu-id="6b770-115">When using the ETWTraceListener, traces are logged in binary .etl files.</span></span> <span data-ttu-id="6b770-116">開啟 ServiceModel 追蹤之後，所有產生的追蹤都會出現在同一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="6b770-116">With ServiceModel tracing turned on, all generated traces appear in the same file.</span></span> <span data-ttu-id="6b770-117">使用[服務追蹤檢視器工具（svctraceviewer.exe .exe）](../service-trace-viewer-tool-svctraceviewer-exe.md)來查看 .etl 和 .svclog 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6b770-117">Use [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) for viewing .etl and .svclog log files.</span></span> <span data-ttu-id="6b770-118">此檢視器會建立系統的端對端檢視，讓您能夠從訊息的來源至其目的端及消費點追蹤該訊息。</span><span class="sxs-lookup"><span data-stu-id="6b770-118">The viewer creates an end-to-end view of the system that makes it possible to trace a message from its source to its destination and point of consumption.</span></span>  
  
 <span data-ttu-id="6b770-119">ETW 追蹤接聽項支援循環記錄。</span><span class="sxs-lookup"><span data-stu-id="6b770-119">The ETW Trace Listener supports circular logging.</span></span> <span data-ttu-id="6b770-120">若要啟用這項功能，請移至 [**開始**]、[**執行**]，然後輸入 `cmd` 以啟動命令主控台。</span><span class="sxs-lookup"><span data-stu-id="6b770-120">To enable this feature, go to **Start**, **Run** and type `cmd` to start a command console.</span></span> <span data-ttu-id="6b770-121">以記錄檔名稱取代下列命令中的 `<logfilename>` 參數。</span><span class="sxs-lookup"><span data-stu-id="6b770-121">In the following command, replace the `<logfilename>` parameter with the name of your log file.</span></span>  
  
```console  
logman create trace Wcf -o <logfilename> -p "{411a0819-c24b-428c-83e2-26b41091702e}" -f bincirc -max 1000  
```  
  
 <span data-ttu-id="6b770-122">`-f` 和 `-max` 參數是選擇項，</span><span class="sxs-lookup"><span data-stu-id="6b770-122">The `-f` and `-max` switches are optional.</span></span> <span data-ttu-id="6b770-123">可以分別指定二進位循環格式以及最多 1000MB 的記錄檔大小上限。</span><span class="sxs-lookup"><span data-stu-id="6b770-123">They specify the binary circular format and max log size of 1000MB respectively.</span></span> <span data-ttu-id="6b770-124">`-p` 參數會用來指定追蹤提供者。</span><span class="sxs-lookup"><span data-stu-id="6b770-124">The `-p` switch is used to specify the trace provider.</span></span> <span data-ttu-id="6b770-125">在範例中，`"{411a0819-c24b-428c-83e2-26b41091702e}"` 即是「XML ETW 範例提供者」的 GUID。</span><span class="sxs-lookup"><span data-stu-id="6b770-125">In our example, `"{411a0819-c24b-428c-83e2-26b41091702e}"` is the GUID for "XML ETW Sample Provider".</span></span>  
  
 <span data-ttu-id="6b770-126">若要啟動工作階段，請輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="6b770-126">To start the session, type in the following command.</span></span>  
  
```console  
logman start Wcf  
```  
  
 <span data-ttu-id="6b770-127">完成記錄之後，您可以使用下列命令停止工作階段。</span><span class="sxs-lookup"><span data-stu-id="6b770-127">After you have finished logging, you can stop the session with the following command.</span></span>  
  
```console  
logman stop Wcf  
```  
  
 <span data-ttu-id="6b770-128">這個程式會產生二進位迴圈記錄檔，您可以使用您選擇的工具來處理，包括[服務追蹤檢視器工具（svctraceviewer.exe）](../service-trace-viewer-tool-svctraceviewer-exe.md)或 Tracerpt。</span><span class="sxs-lookup"><span data-stu-id="6b770-128">This process generates binary circular logs that you can process with your tool of choice, including [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) or Tracerpt.</span></span>  
  
 <span data-ttu-id="6b770-129">您也可以參閱[迴圈追蹤](circular-tracing.md)範例，以取得替代接聽程式執行迴圈記錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6b770-129">You can also review the [Circular Tracing](circular-tracing.md) sample for more information on an alternative listener to perform circular logging.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="6b770-130">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="6b770-130">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="6b770-131">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="6b770-131">Be sure you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="6b770-132">若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="6b770-132">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="6b770-133">若要使用 RegisterProvider.bat、SetupETW.bat 與 CleanupETW.bat 命令，您必須使用本機系統管理員帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="6b770-133">To use the RegisterProvider.bat, SetupETW.bat and CleanupETW.bat commands, you must run under a local administrator account.</span></span> <span data-ttu-id="6b770-134">如果您使用的是 Windows Vista 或更新版本，也必須以較高的許可權來執行命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="6b770-134">If you are using Windows Vista or later, you must also run the command prompt with elevated privileges.</span></span> <span data-ttu-id="6b770-135">若要這樣做，請以滑鼠右鍵按一下命令提示字元圖示，然後按一下 [以**系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="6b770-135">To do so, right-click the command prompt icon, then click **Run as administrator**.</span></span>  
  
3. <span data-ttu-id="6b770-136">執行範例前，請先在用戶端和伺服器上執行 RegisterProvider.bat。</span><span class="sxs-lookup"><span data-stu-id="6b770-136">Before running the sample, run RegisterProvider.bat on the client and server.</span></span> <span data-ttu-id="6b770-137">這會設定產生的 ETWTracingSampleLog.etl 檔案，以產生可由服務追蹤檢視器讀取的追蹤。</span><span class="sxs-lookup"><span data-stu-id="6b770-137">This sets up the resulting ETWTracingSampleLog.etl file to generate traces that can be read by the Service Trace Viewer.</span></span> <span data-ttu-id="6b770-138">您可以在 C:\logs 資料夾中找到這個檔案。</span><span class="sxs-lookup"><span data-stu-id="6b770-138">This file can be found in the C:\logs folder.</span></span> <span data-ttu-id="6b770-139">如果此資料夾不存在，必須先建立一個才能產生追蹤。</span><span class="sxs-lookup"><span data-stu-id="6b770-139">If this folder does not exist, it must be created or no traces are generated.</span></span> <span data-ttu-id="6b770-140">然後，在用戶端和伺服器電腦上執行 SetupETW.bat，以便開始 ETW 追蹤工作階段。</span><span class="sxs-lookup"><span data-stu-id="6b770-140">Then, run SetupETW.bat on the client and server computers to begin the ETW Trace Session.</span></span> <span data-ttu-id="6b770-141">SetupETW.bat 檔案可以在 CS\Client 資料夾中找到。</span><span class="sxs-lookup"><span data-stu-id="6b770-141">The SetupETW.bat file can be found under the CS\Client folder.</span></span>  
  
4. <span data-ttu-id="6b770-142">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="6b770-142">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
5. <span data-ttu-id="6b770-143">當您完成範例時，請執行 CleanupETW.bat 以完成建立 ETWTracingSampleLog.etl 檔案的工作。</span><span class="sxs-lookup"><span data-stu-id="6b770-143">When the sample is completed, run CleanupETW.bat to complete the creation of the ETWTracingSampleLog.etl file.</span></span>  
  
6. <span data-ttu-id="6b770-144">在 [服務追蹤檢視器] 中開啟 ETWTracingSampleLog.etl 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b770-144">Open the ETWTracingSampleLog.etl file from within the Service Trace Viewer.</span></span> <span data-ttu-id="6b770-145">系統會提示您將二進位格式的檔案儲存為 .svclog 檔。</span><span class="sxs-lookup"><span data-stu-id="6b770-145">You will be prompted to save the binary formatted file as a .svclog file.</span></span>  
  
7. <span data-ttu-id="6b770-146">在 [服務追蹤檢視器] 中開啟新建立的 .svclog 檔，以檢視 ETW 和 ServiceModel 追蹤。</span><span class="sxs-lookup"><span data-stu-id="6b770-146">Open the newly created .svclog file from within the Service Trace Viewer to view the ETW and ServiceModel traces.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="6b770-147">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6b770-147">The samples may already be installed on your computer.</span></span> <span data-ttu-id="6b770-148">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="6b770-148">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="6b770-149">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="6b770-149">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="6b770-150">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="6b770-150">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\AnalyticTrace`  
  
## <a name="see-also"></a><span data-ttu-id="6b770-151">請參閱</span><span class="sxs-lookup"><span data-stu-id="6b770-151">See also</span></span>

- <span data-ttu-id="6b770-152">[AppFabric 監控範例](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="6b770-152">[AppFabric Monitoring Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span></span>

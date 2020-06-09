---
title: 追蹤和訊息記錄
ms.date: 03/30/2017
helpviewer_keywords:
- Tracing and logging
ms.assetid: a4f39bfc-3c5e-4d51-a312-71c5c3ce0afd
ms.openlocfilehash: 9af50f138a2788fc7af0ce5d07e95df49d6675cb
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602644"
---
# <a name="tracing-and-message-logging"></a><span data-ttu-id="d56e7-102">追蹤和訊息記錄</span><span class="sxs-lookup"><span data-stu-id="d56e7-102">Tracing and Message Logging</span></span>
<span data-ttu-id="d56e7-103">這個範例示範如何啟用追蹤和訊息記錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-103">This sample demonstrates how to enable tracing and message logging.</span></span> <span data-ttu-id="d56e7-104">系統會使用[服務追蹤檢視器工具（svctraceviewer.exe）](../service-trace-viewer-tool-svctraceviewer-exe.md)來查看產生的追蹤和訊息記錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-104">The resulting traces and message logs are viewed using the [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md).</span></span> <span data-ttu-id="d56e7-105">這個範例是以[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="d56e7-105">This sample is based on the [Getting Started](getting-started-sample.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d56e7-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="d56e7-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
## <a name="tracing"></a><span data-ttu-id="d56e7-107">追蹤</span><span class="sxs-lookup"><span data-stu-id="d56e7-107">Tracing</span></span>  
 <span data-ttu-id="d56e7-108">Windows Communication Foundation （WCF）會使用命名空間中定義的追蹤機制 <xref:System.Diagnostics> 。</span><span class="sxs-lookup"><span data-stu-id="d56e7-108">Windows Communication Foundation (WCF) uses the tracing mechanism defined in the <xref:System.Diagnostics> namespace.</span></span> <span data-ttu-id="d56e7-109">在這個追蹤模型中，應用程式實作的追蹤來源會產生追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="d56e7-109">In this tracing model, trace data is produced by trace sources that applications implement.</span></span> <span data-ttu-id="d56e7-110">每個來源都是以名稱來識別。</span><span class="sxs-lookup"><span data-stu-id="d56e7-110">Each source is identified by a name.</span></span> <span data-ttu-id="d56e7-111">追蹤消費者會為他們要擷取資訊的追蹤來源建立追蹤接聽項。</span><span class="sxs-lookup"><span data-stu-id="d56e7-111">Trace consumers create trace listeners for the trace sources for which they want to retrieve information.</span></span> <span data-ttu-id="d56e7-112">若要接收追蹤資料，就必須建立追蹤來源的接聽項。</span><span class="sxs-lookup"><span data-stu-id="d56e7-112">To receive trace data, you must create a listener for the trace source.</span></span> <span data-ttu-id="d56e7-113">在 WCF 中，您可以藉由設定服務模型追蹤來源，將下列程式碼新增至服務或用戶端的設定檔來完成這項作業 `switchValue` ：</span><span class="sxs-lookup"><span data-stu-id="d56e7-113">In WCF, this can be done by adding the following code to either the service’s or client’s configuration file by setting the Service Model trace source `switchValue`:</span></span>  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-service.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>  
```  
  
 <span data-ttu-id="d56e7-114">如需追蹤來源的詳細資訊，請參閱設定[追蹤主題中](../diagnostics/tracing/configuring-tracing.md)的追蹤來源一節。</span><span class="sxs-lookup"><span data-stu-id="d56e7-114">For more information about trace sources, see the Trace Source section in the [Configuring Tracing](../diagnostics/tracing/configuring-tracing.md) topic.</span></span>  
  
## <a name="activity-tracing-and-propagation"></a><span data-ttu-id="d56e7-115">活動追蹤和傳播</span><span class="sxs-lookup"><span data-stu-id="d56e7-115">Activity Tracing and Propagation</span></span>  
 <span data-ttu-id="d56e7-116">當 `ActivityTracing` `propagateActivity` `true` 用戶端和服務的追蹤來源中啟用並設定為時，會在 `system.ServiceModel` 處理的邏輯單元（活動）中提供追蹤的相互關聯、端點內的活動（透過活動傳輸），以及跨越多個端點的活動（透過活動識別碼傳播）。</span><span class="sxs-lookup"><span data-stu-id="d56e7-116">Having `ActivityTracing` enabled and `propagateActivity` set to `true` in the `system.ServiceModel` trace sources for both the client and service provide correlation of traces within logical units of processing (activities), across activities within endpoints (through activity transfers), and across activities spanning multiple endpoints (through activity ID propagation).</span></span>  
  
 <span data-ttu-id="d56e7-117">這三種機制 (活動、傳輸和傳播) 可以協助您使用 [服務追蹤檢閱器] 工具，迅速找到錯誤的根本原因。</span><span class="sxs-lookup"><span data-stu-id="d56e7-117">These three mechanisms (activities, transfers, and propagation) can help you locate the root cause of an error more quickly using the Service Trace Viewer tool.</span></span> <span data-ttu-id="d56e7-118">如需詳細資訊，請參閱[使用服務追蹤檢視器來查看相互關聯的追蹤和疑難排解](../diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="d56e7-118">For more information, see [Using Service Trace Viewer for Viewing Correlated Traces and Troubleshooting](../diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).</span></span>  
  
 <span data-ttu-id="d56e7-119">您可以建立使用者定義的活動追蹤，來延伸 ServiceModel 所提供的追蹤。</span><span class="sxs-lookup"><span data-stu-id="d56e7-119">It is possible to extend the tracing that is provided by the ServiceModel by creating user-defined activity traces.</span></span> <span data-ttu-id="d56e7-120">使用者定義的活動追蹤允許使用者建立追蹤活動，以進行下列工作：</span><span class="sxs-lookup"><span data-stu-id="d56e7-120">User-defined activity tracing allows the user to create trace activities to:</span></span>  
  
- <span data-ttu-id="d56e7-121">將追蹤集合成工作邏輯單位的群組。</span><span class="sxs-lookup"><span data-stu-id="d56e7-121">Group traces into logical units of work.</span></span>  
  
- <span data-ttu-id="d56e7-122">透過傳輸和傳播將活動相互關聯。</span><span class="sxs-lookup"><span data-stu-id="d56e7-122">Correlate activities through transfers and propagation.</span></span>  
  
- <span data-ttu-id="d56e7-123">減少 WCF 追蹤的效能成本（例如，記錄檔的磁碟空間成本）。</span><span class="sxs-lookup"><span data-stu-id="d56e7-123">Lessen the performance cost of WCF tracing (for example, the disk space cost of a log file).</span></span>  
  
 <span data-ttu-id="d56e7-124">如需使用者定義活動追蹤的詳細資訊，請參閱[擴充追蹤](extending-tracing.md)範例。</span><span class="sxs-lookup"><span data-stu-id="d56e7-124">For more information about user-defined activity trace, please see the [Extending Tracing](extending-tracing.md) sample.</span></span>  
  
## <a name="message-logging"></a><span data-ttu-id="d56e7-125">訊息記錄</span><span class="sxs-lookup"><span data-stu-id="d56e7-125">Message Logging</span></span>  
 <span data-ttu-id="d56e7-126">可以在任何 WCF 應用程式的用戶端和服務上啟用訊息記錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-126">Message logging can be enabled both on the client and service of any WCF application.</span></span> <span data-ttu-id="d56e7-127">若要啟用訊息記錄，您必須將下列程式碼新增至用戶端或服務：</span><span class="sxs-lookup"><span data-stu-id="d56e7-127">To enable message logging, you must add the following code to either the client or service:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <diagnostics>  
      <!-- Enable Message Logging here. -->  
      <!-- log all messages received or sent at the transport or service model levels -->  
      <messageLogging logEntireMessage="true"  
                      maxMessagesToLog="300"  
                      logMessagesAtServiceLevel="true"  
                      logMalformedMessages="true"  
                      logMessagesAtTransportLevel="true" />  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="d56e7-128">記錄訊息時，追蹤類型將依據是在用戶端或在伺服器上追蹤而定。</span><span class="sxs-lookup"><span data-stu-id="d56e7-128">When a message is recorded, the trace type depends on whether it is being traced at the client or the server.</span></span> <span data-ttu-id="d56e7-129">例如，在用戶端，傳送給用戶端的「新增」訊息會受到 "TransportWrite" 類型的追蹤，然而在服務上，相同的訊息則會受到 "TransportRead" 類型的追蹤。</span><span class="sxs-lookup"><span data-stu-id="d56e7-129">For example, an "Add" message that is sent to a client is traced under the "TransportWrite" category at the client, whereas the same message is traced under the "TransportRead" category at the service.</span></span>  
  
 <span data-ttu-id="d56e7-130">設定追蹤接聽項，方式是將下列程式碼新增至用戶端的 App.config 檔案或服務的 Web.config 檔案的 <xref:System.Diagnostics> 區段：</span><span class="sxs-lookup"><span data-stu-id="d56e7-130">Configure the trace listener by adding the following code to the <xref:System.Diagnostics> section of the client's App.config file or the service's Web.config file:</span></span>  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-client.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
```  
  
 <span data-ttu-id="d56e7-131">在組態檔內指定的目標目錄中，會使用 XML 格式來記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="d56e7-131">Messages are logged in XML format in the target directory specified in the configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d56e7-132">如果一開始並未建立記錄目錄，就不會建立追蹤檔。</span><span class="sxs-lookup"><span data-stu-id="d56e7-132">Trace files are not created without initially creating the log directory.</span></span> <span data-ttu-id="d56e7-133">請確定目錄 C:\logs\ 存在，不然就在接聽項組態中指定其他記錄目錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-133">Make sure that the directory C:\logs\ exists, or specify an alternate logging directory in the listener configuration.</span></span> <span data-ttu-id="d56e7-134">如需詳細資訊，請參閱本文件結尾的初始安裝指示。</span><span class="sxs-lookup"><span data-stu-id="d56e7-134">See the initial setup instructions at the end of this document for more information.</span></span>  
  
 <span data-ttu-id="d56e7-135">如需訊息記錄的詳細資訊，請參閱設定[訊息記錄](../diagnostics/configuring-message-logging.md)主題。</span><span class="sxs-lookup"><span data-stu-id="d56e7-135">For more information about message logging, see the [Configuring Message Logging](../diagnostics/configuring-message-logging.md) topic.</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="d56e7-136">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="d56e7-136">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="d56e7-137">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d56e7-137">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="d56e7-138">在執行追蹤和訊息記錄範例前，請先建立可供服務將 .svclog 檔寫入的 C:\logs\ 目錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-138">Before running the Tracing and Message Logging sample, create the directory C:\logs\ for the service to write the .svclog files to.</span></span> <span data-ttu-id="d56e7-139">這個目錄名稱會在組態檔中定義為所要記錄之追蹤和訊息的路徑，而您可以變更此名稱。</span><span class="sxs-lookup"><span data-stu-id="d56e7-139">The name of this directory is defined in the configuration file as the path for the traces and messages to be logged and can be changed.</span></span> <span data-ttu-id="d56e7-140">請提供使用者對記錄目錄的網路服務寫入權限。</span><span class="sxs-lookup"><span data-stu-id="d56e7-140">Give the user Network Service write access to the logs directory.</span></span>  
  
3. <span data-ttu-id="d56e7-141">若要建立解決方案的 c #、c + + 或 Visual Basic .NET 版本，請遵循[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d56e7-141">To build the C#, C++, or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="d56e7-142">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d56e7-142">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="d56e7-143">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d56e7-143">The samples may already be installed on your computer.</span></span> <span data-ttu-id="d56e7-144">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="d56e7-144">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="d56e7-145">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="d56e7-145">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d56e7-146">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="d56e7-146">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\TracingAndLogging`  
  
## <a name="see-also"></a><span data-ttu-id="d56e7-147">請參閱</span><span class="sxs-lookup"><span data-stu-id="d56e7-147">See also</span></span>

- [<span data-ttu-id="d56e7-148">追蹤</span><span class="sxs-lookup"><span data-stu-id="d56e7-148">Tracing</span></span>](../diagnostics/tracing/index.md)
- <span data-ttu-id="d56e7-149">[AppFabric 監控範例](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="d56e7-149">[AppFabric Monitoring Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span></span>

---
title: Windows 服務主機
ms.date: 03/30/2017
helpviewer_keywords:
- NT Service
- NT Service Host Sample [Windows Communication Foundation]
ms.assetid: 1b2f45c5-2bed-4979-b0ee-8f9efcfec028
ms.openlocfilehash: 9c041f6e9505d2ec5865dd512359b497a411cb40
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602280"
---
# <a name="windows-service-host"></a><span data-ttu-id="8900d-102">Windows 服務主機</span><span class="sxs-lookup"><span data-stu-id="8900d-102">Windows Service Host</span></span>
<span data-ttu-id="8900d-103">這個範例會示範裝載于 managed Windows 服務中的 Windows Communication Foundation （WCF）服務。</span><span class="sxs-lookup"><span data-stu-id="8900d-103">This sample demonstrates a Windows Communication Foundation (WCF) service hosted in a managed Windows Service.</span></span> <span data-ttu-id="8900d-104">Windows 服務是使用 [**控制台**] 中的 [服務] 小程式來控制，而且可以設定為在系統重新開機後自動啟動。</span><span class="sxs-lookup"><span data-stu-id="8900d-104">Windows Services are controlled using the Services applet in **Control Panel** and can be configured to start up automatically after a system reboot.</span></span> <span data-ttu-id="8900d-105">範例是由用戶端程式與 Windows 服務程式所組成。</span><span class="sxs-lookup"><span data-stu-id="8900d-105">The sample consists of a client program and an Windows Service program.</span></span> <span data-ttu-id="8900d-106">服務會實作為 .exe 程式並包含專屬的裝載程式碼。</span><span class="sxs-lookup"><span data-stu-id="8900d-106">The service is implemented as an .exe program and contains its own hosting code.</span></span> <span data-ttu-id="8900d-107">在其他裝載環境中，例如 Windows 處理序啟用服務 (WAS) 或 Internet Information Services (IIS)，就不需要撰寫裝載程式碼。</span><span class="sxs-lookup"><span data-stu-id="8900d-107">In other hosting environments, such as Windows Process Activation Services (WAS) or Internet Information Services (IIS), it is not necessary for you to write hosting code.</span></span>

> [!NOTE]
> <span data-ttu-id="8900d-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="8900d-108">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8900d-109">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8900d-109">The samples may already be installed on your computer.</span></span> <span data-ttu-id="8900d-110">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="8900d-110">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="8900d-111">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="8900d-111">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="8900d-112">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="8900d-112">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WindowsService`  
  
 <span data-ttu-id="8900d-113">在這個服務完成建置後，它必須像任何其他 Windows 服務一樣使用 Installutil.exe 公用程式安裝。</span><span class="sxs-lookup"><span data-stu-id="8900d-113">After building this service, it must be installed with the Installutil.exe utility like any other Windows Service.</span></span> <span data-ttu-id="8900d-114">如果要變更服務，就必須先以 `installutil /u` 將它解除安裝。</span><span class="sxs-lookup"><span data-stu-id="8900d-114">If you are going to make changes to the service, you must first uninstall it with `installutil /u`.</span></span> <span data-ttu-id="8900d-115">這個範例中包含的 Setup.bat 和 Cleanup.bat 檔是用來安裝和啟動 Windows 服務，以及關閉和解除安裝 Windows 服務的命令。</span><span class="sxs-lookup"><span data-stu-id="8900d-115">The Setup.bat and Cleanup.bat files included in this sample are the commands to install and start up the Windows Service, and to shut down and uninstall the Windows Service.</span></span> <span data-ttu-id="8900d-116">只有在 Windows 服務正在執行時，WCF 服務才會回應用戶端。</span><span class="sxs-lookup"><span data-stu-id="8900d-116">The WCF service can only respond to clients if the Windows Service is running.</span></span> <span data-ttu-id="8900d-117">如果您使用 [**控制台**] 中的 [服務] 小程式來停止 Windows 服務，並執行用戶端，則 <xref:System.ServiceModel.EndpointNotFoundException> 當用戶端嘗試存取服務時，就會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8900d-117">If you stop the Windows Service by using the Services applet from **Control Panel** and run the client, a <xref:System.ServiceModel.EndpointNotFoundException> exception occurs when a client attempts to access the service.</span></span> <span data-ttu-id="8900d-118">如果重新啟動 Windows 服務然後重新執行用戶端，就可成功進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8900d-118">If you restart the Windows Service and rerun the client, communication succeeds.</span></span>  
  
 <span data-ttu-id="8900d-119">服務程式代碼包含 installer 類別、執行 ICalculator 合約的 WCF 服務實作用類別，以及做為執行時間主機的 Windows 服務類別。</span><span class="sxs-lookup"><span data-stu-id="8900d-119">The service code includes an installer class, a WCF service implementation class which implements the ICalculator contract, and a Windows Service class that acts as the run-time host.</span></span> <span data-ttu-id="8900d-120">繼承自 <xref:System.Configuration.Install.Installer> 的安裝程式類別，會允許 Installutil.exe 工具將程式當做 NT 服務進行安裝。</span><span class="sxs-lookup"><span data-stu-id="8900d-120">The installer class, which inherits from <xref:System.Configuration.Install.Installer>, allows the program to be installed as an NT service by the Installutil.exe tool.</span></span> <span data-ttu-id="8900d-121">服務實類別 `WcfCalculatorService` 是一個 WCF 服務，它會執行基本的服務合約。</span><span class="sxs-lookup"><span data-stu-id="8900d-121">The service implementation class, `WcfCalculatorService`, is an WCF service that implements a basic service contract.</span></span> <span data-ttu-id="8900d-122">這個 WCF 服務裝載在名為的 Windows 服務類別內 `WindowsCalculatorService` 。</span><span class="sxs-lookup"><span data-stu-id="8900d-122">This WCF service is hosted inside a Windows Service class called `WindowsCalculatorService`.</span></span> <span data-ttu-id="8900d-123">為了限定為 Windows 服務，此類別會繼承自 <xref:System.ServiceProcess.ServiceBase>，並且實作 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 和 <xref:System.ServiceProcess.ServiceBase.OnStop> 方法。</span><span class="sxs-lookup"><span data-stu-id="8900d-123">To qualify as a Windows Service, the class inherits from <xref:System.ServiceProcess.ServiceBase> and implements the <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> and <xref:System.ServiceProcess.ServiceBase.OnStop> methods.</span></span> <span data-ttu-id="8900d-124">使用 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 時，會建立並開啟型別為 <xref:System.ServiceModel.ServiceHost> 的 `WcfCalculatorService` 物件。</span><span class="sxs-lookup"><span data-stu-id="8900d-124">In <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>, a <xref:System.ServiceModel.ServiceHost> object is created for the `WcfCalculatorService` type and opened.</span></span> <span data-ttu-id="8900d-125">使用 <xref:System.ServiceProcess.ServiceBase.OnStop> 時，會呼叫 <xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> 物件的 <xref:System.ServiceModel.ServiceHost> 方法來關閉 ServiceHost。</span><span class="sxs-lookup"><span data-stu-id="8900d-125">In <xref:System.ServiceProcess.ServiceBase.OnStop>, the ServiceHost is closed by calling the <xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> method of the <xref:System.ServiceModel.ServiceHost> object.</span></span> <span data-ttu-id="8900d-126">主機的基底位址是使用專案來設定，這個專案是專案的子系，也就是元素的子系 [\<add>](../../configure-apps/file-schema/wcf/add-of-baseaddresses.md) [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md) [\<host>](../../configure-apps/file-schema/wcf/host.md) [\<service>](../../configure-apps/file-schema/wcf/service.md) 。</span><span class="sxs-lookup"><span data-stu-id="8900d-126">The host's base address is configured using the [\<add>](../../configure-apps/file-schema/wcf/add-of-baseaddresses.md) element, which is a child of [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md), which is a child of the [\<host>](../../configure-apps/file-schema/wcf/host.md) element, which is a child of the [\<service>](../../configure-apps/file-schema/wcf/service.md) element.</span></span>  
  
 <span data-ttu-id="8900d-127">定義的端點會使用基底位址和 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 。</span><span class="sxs-lookup"><span data-stu-id="8900d-127">The endpoint that is defined uses the base address and a [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md).</span></span> <span data-ttu-id="8900d-128">下列範例會示範設定基底位址，以及會公開 (Expose) CalculatorService 的端點。</span><span class="sxs-lookup"><span data-stu-id="8900d-128">The following sample shows the configuration of the base address as well as the endpoint that exposes the CalculatorService.</span></span>  
  
```xml  
<services>  
  <service name="Microsoft.ServiceModel.Samples.WcfCalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    <host>  
      <baseAddresses>  
        <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
      </baseAddresses>  
    </host>  
    <!-- This endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service.  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
```  
  
 <span data-ttu-id="8900d-129">當您執行範例時，作業要求和回應會顯示在服務與用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="8900d-129">When you run the sample, the operation requests and responses are displayed in both the service and client console windows.</span></span> <span data-ttu-id="8900d-130">在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。</span><span class="sxs-lookup"><span data-stu-id="8900d-130">Press ENTER in each console window to shut down the service and client.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="8900d-131">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="8900d-131">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="8900d-132">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="8900d-132">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="8900d-133">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="8900d-133">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="8900d-134">建立解決方案之後，請從提高許可權的 Visual Studio 2012 命令提示字元執行 .bat，以使用 Installutil.exe 工具安裝 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="8900d-134">After the solution has been built, run Setup.bat from an elevated Visual Studio 2012 command prompt to install the Windows service using the Installutil.exe tool.</span></span> <span data-ttu-id="8900d-135">此時該服務就會出現在 [服務] 中。</span><span class="sxs-lookup"><span data-stu-id="8900d-135">The service should appear in Services.</span></span>  
  
4. <span data-ttu-id="8900d-136">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="8900d-136">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8900d-137">請參閱</span><span class="sxs-lookup"><span data-stu-id="8900d-137">See also</span></span>

- <span data-ttu-id="8900d-138">[AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="8900d-138">[AppFabric Hosting and Persistence Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span></span>

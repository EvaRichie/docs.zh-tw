---
title: 自我裝載
ms.date: 03/30/2017
helpviewer_keywords:
- Self hosted service
- Self Host Sample [Windows Communication Foundation]
ms.assetid: 05e68661-1ddf-4abf-a899-9bb1b8272a5b
ms.openlocfilehash: 544ae8c0bc88d49c281810714225dbadecfd443b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558403"
---
# <a name="self-host"></a><span data-ttu-id="a7a22-102">自我裝載</span><span class="sxs-lookup"><span data-stu-id="a7a22-102">Self-Host</span></span>
<span data-ttu-id="a7a22-103">這個範例會示範如何在主控台應用程式中實作自我裝載的服務。</span><span class="sxs-lookup"><span data-stu-id="a7a22-103">This sample demonstrates how to implement a self-hosted service in a console application.</span></span> <span data-ttu-id="a7a22-104">這個範例是以 [消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="a7a22-104">This sample is based on the [Getting Started](getting-started-sample.md).</span></span> <span data-ttu-id="a7a22-105">服務的組態檔已經從 Web.config 重新命名為 App.config，並且修改為設定主機使用的基底位址。</span><span class="sxs-lookup"><span data-stu-id="a7a22-105">The service configuration file has been renamed from Web.config to App.config and modified to configure a base address, which the host uses.</span></span> <span data-ttu-id="a7a22-106">服務的原始程式碼已經修改為實作靜態 `Main` 函式，這個函式會建立和開啟提供已設定之基底位址的服務主機。</span><span class="sxs-lookup"><span data-stu-id="a7a22-106">The service source code has been modified to implement a static `Main` function that creates and opens a service host that provides the configured base address.</span></span> <span data-ttu-id="a7a22-107">服務實作已經修改為將每個作業的輸出寫入至主控台。</span><span class="sxs-lookup"><span data-stu-id="a7a22-107">The service implementation has been modified to write output to the console for each operation.</span></span> <span data-ttu-id="a7a22-108">除了設定服務的正確端點位址外，用戶端未經過修改。</span><span class="sxs-lookup"><span data-stu-id="a7a22-108">The client has been unmodified, except for configuring the correct endpoint address of the service.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a7a22-109">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="a7a22-109">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="a7a22-110">此範例會實作靜態的 main 函式，以便為指定的 <xref:System.ServiceModel.ServiceHost> 型別建立 `CalculatorService`，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="a7a22-110">The sample implements a static main function to create a <xref:System.ServiceModel.ServiceHost> for the given `CalculatorService` type, as shown in the following sample code.</span></span>  
  
```csharp
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost =
           new ServiceHost(typeof(CalculatorService)))  
    {  
        // Open the ServiceHost to create listeners
        // and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
    }  
}  
```  
  
 <span data-ttu-id="a7a22-111">當服務裝載於網際網路資訊服務 (IIS) 或 Windows Process Activation Service (WAS) 時，服務的基底位址是由裝載環境提供。</span><span class="sxs-lookup"><span data-stu-id="a7a22-111">When a service is hosted in Internet Information Services (IIS) or Windows Process Activation Service (WAS), the base address of the service is provided by the hosting environment.</span></span> <span data-ttu-id="a7a22-112">在自我裝載案例中，您必須自行指定基底位址。</span><span class="sxs-lookup"><span data-stu-id="a7a22-112">In the self-hosted case, you must specify the base address yourself.</span></span> <span data-ttu-id="a7a22-113">這是使用 `add` [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md) [\<host>](../../configure-apps/file-schema/wcf/host.md) 下列範例設定中所示範的子項目、子系的子系來完成 [\<service>](../../configure-apps/file-schema/wcf/service.md) 。</span><span class="sxs-lookup"><span data-stu-id="a7a22-113">This is done using the `add` element, child of [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md), child of [\<host>](../../configure-apps/file-schema/wcf/host.md), child of [\<service>](../../configure-apps/file-schema/wcf/service.md) as demonstrated in the following sample configuration.</span></span>  
  
```xml  
<service
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
  ...  
</service>  
```  
  
 <span data-ttu-id="a7a22-114">當您執行範例時，作業要求和回應會顯示在服務與用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="a7a22-114">When you run the sample, the operation requests and responses are displayed in both the service and client console windows.</span></span> <span data-ttu-id="a7a22-115">在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7a22-115">Press ENTER in each console window to shut down the service and client.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="a7a22-116">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="a7a22-116">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="a7a22-117">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="a7a22-117">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="a7a22-118">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="a7a22-118">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="a7a22-119">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="a7a22-119">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="a7a22-120">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a7a22-120">The samples may already be installed on your computer.</span></span> <span data-ttu-id="a7a22-121">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="a7a22-121">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="a7a22-122">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="a7a22-122">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="a7a22-123">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="a7a22-123">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\SelfHost`  
  
## <a name="see-also"></a><span data-ttu-id="a7a22-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a7a22-124">See also</span></span>

- <span data-ttu-id="a7a22-125">[AppFabric 主控與持續性範例](/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="a7a22-125">[AppFabric Hosting and Persistence Samples](/previous-versions/appfabric/ff383418(v=azure.10))</span></span>

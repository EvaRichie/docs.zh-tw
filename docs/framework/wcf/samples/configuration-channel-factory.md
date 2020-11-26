---
title: 組態通道處理站
ms.date: 03/30/2017
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
ms.openlocfilehash: bebdd7e5913fd3bbc1ab88d32e6612b9bc951852
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241144"
---
# <a name="configuration-channel-factory"></a><span data-ttu-id="8539e-102">組態通道處理站</span><span class="sxs-lookup"><span data-stu-id="8539e-102">Configuration Channel Factory</span></span>

<span data-ttu-id="8539e-103">此範例涵蓋 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> 的使用方法。</span><span class="sxs-lookup"><span data-stu-id="8539e-103">This sample covers the usage of the <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>.</span></span> <span data-ttu-id="8539e-104"><xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>允許 WCF 用戶端設定的集中管理。</span><span class="sxs-lookup"><span data-stu-id="8539e-104">The <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> allows central management of WCF client configuration.</span></span> <span data-ttu-id="8539e-105">如果在應用程式網域載入時間之後選取或變更組態，這可能也相當實用。</span><span class="sxs-lookup"><span data-stu-id="8539e-105">This can also be useful in scenarios in which configuration is selected or changed after the application domain load time.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="8539e-106">示範</span><span class="sxs-lookup"><span data-stu-id="8539e-106">Demonstrates</span></span>

 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>

## <a name="discussion"></a><span data-ttu-id="8539e-107">討論</span><span class="sxs-lookup"><span data-stu-id="8539e-107">Discussion</span></span>

 <span data-ttu-id="8539e-108">此範例示範如何使用 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> 將特定組態檔加入至用戶端應用程式，而不必使用預設的應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="8539e-108">This sample shows how to use <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> to add a particular configuration file to a client application, without having to use the default application configuration file.</span></span>

 <span data-ttu-id="8539e-109">此範例包含二個專案。</span><span class="sxs-lookup"><span data-stu-id="8539e-109">The sample consists of two projects.</span></span> <span data-ttu-id="8539e-110">第一個專案是簡單服務，執行這個服務可回覆來自用戶端的訊息。</span><span class="sxs-lookup"><span data-stu-id="8539e-110">The first project is a simple service that runs to reply to messages coming from the clients.</span></span> <span data-ttu-id="8539e-111">第二個專案是用戶端應用程式，這個應用程式可以針對 Test.config 組態檔使用 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> 建立兩個 <xref:System.Configuration.ExeConfigurationFileMap> 物件，並使用這兩個物件與服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8539e-111">The second project is a client application that builds two <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> objects using a <xref:System.Configuration.ExeConfigurationFileMap> for the Test.config configuration file and uses them to communicate with the service.</span></span> <span data-ttu-id="8539e-112">兩個用戶端都會使用 Test.config 中指定的組態，與服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8539e-112">Both clients communicate with the service using the configuration specified in Test.config.</span></span>

 <span data-ttu-id="8539e-113">下列程式碼會將自訂組態檔加入至用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="8539e-113">The following code adds a custom configuration file to a client application.</span></span>

```csharp
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();
fileMap.ExeConfigFilename = "Test.config";
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);

ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));
ICalculatorChannel client1 = factory1.CreateChannel();
```

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="8539e-114">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="8539e-114">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="8539e-115">以系統管理員許可權開啟 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="8539e-115">Open Visual Studio 2012 with administrator privileges.</span></span>

2. <span data-ttu-id="8539e-116">以滑鼠右鍵按一下 [ConfigurationChannelFactory 方案 (2 個專案]) 然後選取 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="8539e-116">Right-click the ConfigurationChannelFactory solution (2 projects) and then select **Properties**.</span></span>

3. <span data-ttu-id="8539e-117">在 [ **通用屬性**] 中，選取 [ **啟始專案**]，然後按一下 [ **多個啟始專案**]。</span><span class="sxs-lookup"><span data-stu-id="8539e-117">In **Common Properties**, select **Startup Project**, and then click **Multiple startup projects**.</span></span>

4. <span data-ttu-id="8539e-118">使用 **動作 [開始**] 將 **服務** 專案移至清單的開頭，然後在 **服務** 專案之後移動 **用戶端** 專案，並使用 **動作 [開始**]，以便在 **服務** 專案之後執行 **用戶端** 專案。</span><span class="sxs-lookup"><span data-stu-id="8539e-118">Move the **Service** project to the beginning of the list, with the **Action ‘Start’**, and then move the **Client** project after the **Service** project, also with the **Action ‘Start’**, so the **Client** project is executed after the **Service** project.</span></span>

5. <span data-ttu-id="8539e-119">按一下 **[確定]**，然後按下 f5 (或 CTRL + f5) 來執行範例。</span><span class="sxs-lookup"><span data-stu-id="8539e-119">Click **OK**, and then press F5 (or CTRL+F5) to run the sample.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8539e-120">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8539e-120">The samples may already be installed on your machine.</span></span> <span data-ttu-id="8539e-121">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="8539e-121">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="8539e-122">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="8539e-122">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="8539e-123">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="8539e-123">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`

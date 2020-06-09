---
title: 自訂繫結可靠工作階段
ms.date: 03/30/2017
ms.assetid: c5fcd409-246f-4f3e-b3f1-629506ca4c04
ms.openlocfilehash: bd690f96eea885c4d414f9725125e1918fdffa23
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585139"
---
# <a name="custom-binding-reliable-session"></a><span data-ttu-id="9b039-102">自訂繫結可靠工作階段</span><span class="sxs-lookup"><span data-stu-id="9b039-102">Custom Binding Reliable Session</span></span>

<span data-ttu-id="9b039-103">自訂繫結由經過排序的獨立繫結項目清單所定義。</span><span class="sxs-lookup"><span data-stu-id="9b039-103">A custom binding is defined by an ordered list of discrete binding elements.</span></span> <span data-ttu-id="9b039-104">此範例示範如何使用各種傳輸與訊息編碼項目設定自訂繫結，特別是啟用可靠工作階段。</span><span class="sxs-lookup"><span data-stu-id="9b039-104">This sample demonstrates how to configure a custom binding with various transport and message encoding elements, especially enabling reliable sessions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b039-105">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9b039-105">The samples may already be installed on your machine.</span></span> <span data-ttu-id="9b039-106">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="9b039-106">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="9b039-107">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="9b039-107">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="9b039-108">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="9b039-108">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\ReliableSession`

## <a name="sample-details"></a><span data-ttu-id="9b039-109">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="9b039-109">Sample Details</span></span>

<span data-ttu-id="9b039-110">可靠的工作階段會提供可靠傳訊和工作階段功能。</span><span class="sxs-lookup"><span data-stu-id="9b039-110">Reliable sessions provide features for reliable messaging and sessions.</span></span> <span data-ttu-id="9b039-111">可靠的傳訊失敗時會重試通訊，而且允許指定傳遞保證，例如訊息依序到達。</span><span class="sxs-lookup"><span data-stu-id="9b039-111">Reliable messaging retries communication on failure and allows delivery assurances such as in-order arrival of messages to be specified.</span></span> <span data-ttu-id="9b039-112">工作階段會保持呼叫之間的用戶端狀態。</span><span class="sxs-lookup"><span data-stu-id="9b039-112">Sessions maintain state for clients between calls.</span></span> <span data-ttu-id="9b039-113">此範例會實作維持用戶端狀態的工作階段，並且指定依序傳遞保證。</span><span class="sxs-lookup"><span data-stu-id="9b039-113">The sample implements sessions for maintaining client state and specifies in-order delivery assurances.</span></span> <span data-ttu-id="9b039-114">此範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="9b039-114">The sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service.</span></span> <span data-ttu-id="9b039-115">可靠工作階段的功能已在用戶端和服務的應用程式組態檔中啟用和設定。</span><span class="sxs-lookup"><span data-stu-id="9b039-115">The reliable session features are enabled and configured in the application configuration files for the client and service.</span></span>

> [!NOTE]
> <span data-ttu-id="9b039-116">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="9b039-116">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="9b039-117">繫結項目的順序對於定義自訂系結很重要，因為每個都代表通道堆疊中的一層（請參閱[自訂](../extending/custom-bindings.md)系結）。</span><span class="sxs-lookup"><span data-stu-id="9b039-117">The ordering of binding elements is important in defining a custom binding, because each represents a layer in the channel stack (see [Custom Bindings](../extending/custom-bindings.md)).</span></span>

<span data-ttu-id="9b039-118">範例的服務組態會如下列程式碼範例所示加以定義。</span><span class="sxs-lookup"><span data-stu-id="9b039-118">The service configuration for the sample is defined as shown in the following code example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"
          behaviorConfiguration="CalculatorServiceBehavior">
        <!-- This endpoint is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc  -->
        <!-- specify customBinding binding and a binding configuration to use -->
        <endpoint address=""
                  binding="customBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexHttpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>

    <!-- custom binding configuration - configures HTTP transport, reliable sessions -->
    <bindings>
      <customBinding>
        <binding name="Binding1">
          <reliableSession />
          <security authenticationMode="SecureConversation"
                     requireSecurityContextCancellation="true">
          </security>
          <compositeDuplex />
          <oneWay />
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8" />
          <httpTransport authenticationScheme="Anonymous" bypassProxyOnLocal="false"
                        hostNameComparisonMode="StrongWildcard"
                        proxyAuthenticationScheme="Anonymous" realm=""
                        useDefaultWebProxy="true" />
        </binding>
      </customBinding>
    </bindings>

    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata httpGetEnabled="True"/>
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>

</configuration>
```

<span data-ttu-id="9b039-119">執行跨電腦案例時，您必須變更用戶端的端點位址以反映出服務的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="9b039-119">When running in a cross-machine scenario, you must change client's endpoint address to reflect the host name of the service.</span></span>

<span data-ttu-id="9b039-120">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="9b039-120">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="9b039-121">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b039-121">Press ENTER in the client window to shut down the client.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="9b039-122">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="9b039-122">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="9b039-123">使用下列命令安裝 ASP.NET 4.0：</span><span class="sxs-lookup"><span data-stu-id="9b039-123">Install ASP.NET 4.0 using the following command:</span></span>

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. <span data-ttu-id="9b039-124">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="9b039-124">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

3. <span data-ttu-id="9b039-125">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9b039-125">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

4. <span data-ttu-id="9b039-126">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9b039-126">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9b039-127">在跨電腦設定中執行用戶端時，請務必將專案的屬性和的屬性中的 "localhost" 取代為 `address` [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) `clientBaseAddress` [\<compositeDuplex>](../../configure-apps/file-schema/wcf/compositeduplex.md) 適當電腦的名稱，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="9b039-127">When running the client in a cross-machine configuration, be sure to replace "localhost" in both the `address` attribute of the [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) element and the `clientBaseAddress` attribute of the [\<compositeDuplex>](../../configure-apps/file-schema/wcf/compositeduplex.md) with the name of the appropriate machine, as shown in the following example.</span></span>

    ```xml
    <endpoint name = ""
    address="http://service_machine_name/servicemodelsamples/service.svc" />
    <compositeDuplex clientBaseAddress="http://client_machine_name:8000/myClient/" />
    ```

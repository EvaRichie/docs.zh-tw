---
title: 具備傳輸安全性的 BasicBinding
ms.date: 03/30/2017
ms.assetid: f49b1de6-0254-4362-8ef2-fccd8ff9688b
ms.openlocfilehash: 822a7dcb20c6559a70ba77719b6e7a62633bb31c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575663"
---
# <a name="basicbinding-with-transport-security"></a><span data-ttu-id="548b0-102">具備傳輸安全性的 BasicBinding</span><span class="sxs-lookup"><span data-stu-id="548b0-102">BasicBinding with Transport Security</span></span>

<span data-ttu-id="548b0-103">這個範例會示範透過基本繫結來使用 SSL 傳輸安全性。</span><span class="sxs-lookup"><span data-stu-id="548b0-103">This sample demonstrates the use of SSL transport security with the basic binding.</span></span> <span data-ttu-id="548b0-104">這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="548b0-104">This sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="548b0-105">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="548b0-105">The samples may already be installed on your machine.</span></span> <span data-ttu-id="548b0-106">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="548b0-106">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="548b0-107">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="548b0-107">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="548b0-108">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="548b0-108">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\TransportSecurity`

## <a name="sample-details"></a><span data-ttu-id="548b0-109">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="548b0-109">Sample Details</span></span>

<span data-ttu-id="548b0-110">根據預設，基本繫結支援 HTTP 通訊。</span><span class="sxs-lookup"><span data-stu-id="548b0-110">By default, the basic binding supports HTTP communication.</span></span> <span data-ttu-id="548b0-111">此範例會示範如何啟用基本繫結的傳輸安全性。</span><span class="sxs-lookup"><span data-stu-id="548b0-111">The sample shows how to enable transport security for the basic binding.</span></span> <span data-ttu-id="548b0-112">在執行範例之前，您必須使用 [Web 伺服器憑證精靈] 建立並指派憑證。</span><span class="sxs-lookup"><span data-stu-id="548b0-112">Before you run the sample, you must create a certificate and assign it by using the Web Server Certificate Wizard.</span></span>

> [!NOTE]
> <span data-ttu-id="548b0-113">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="548b0-113">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="548b0-114">範例中的程式碼與[消費者入門](getting-started-sample.md)服務相同。</span><span class="sxs-lookup"><span data-stu-id="548b0-114">The program code in the sample is identical to that of the [Getting Started](getting-started-sample.md) service.</span></span> <span data-ttu-id="548b0-115">組態檔設定中的端點定義與繫結定義會修改成啟用安全通訊，如下列範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="548b0-115">The endpoint definition and binding definition in the configuration file settings are modified to enable secure communication, as shown in the following sample configuration.</span></span>

```xml
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
   </services>
  <bindings>
    <basicHttpBinding>
      <!-- Configure basicHttpBinding with Transport security -->
      <!-- mode and clientCredentialType set to None. -->
      <binding name="Binding1">
        <security mode="Transport">
          <transport clientCredentialType="None"/>
        </security>
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```

<span data-ttu-id="548b0-116">因為此範例中使用的憑證是使用 Makecert 建立的測試憑證，所以當您嘗試在瀏覽器中存取 HTTPS：位址時（例如），就會出現安全性警示 `https://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="548b0-116">Because the certificate used in this sample is a test certificate created with Makecert.exe, a security alert appears when you try to access an HTTPS: address in your browser, such as `https://localhost/servicemodelsamples/service.svc`.</span></span> <span data-ttu-id="548b0-117">為了讓 Windows Communication Foundation （WCF）用戶端使用測試憑證，會將一些額外的程式碼新增至用戶端，以隱藏安全性警示。</span><span class="sxs-lookup"><span data-stu-id="548b0-117">To allow the Windows Communication Foundation (WCF) client to work with a test certificate, some additional code is added to the client to suppress the security alert.</span></span> <span data-ttu-id="548b0-118">使用實際憑證時，不需要這個程式碼及伴隨的類別。</span><span class="sxs-lookup"><span data-stu-id="548b0-118">This code, and the accompanying class, is not necessary when using real certificates.</span></span>

```csharp
// This code is required only for test certificates such as those
// created by Makecert.exe.
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");
```

<span data-ttu-id="548b0-119">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="548b0-119">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="548b0-120">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="548b0-120">Press ENTER in the client window to shut down the client.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="548b0-121">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="548b0-121">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="548b0-122">使用下列命令安裝 ASP.NET 4.0：</span><span class="sxs-lookup"><span data-stu-id="548b0-122">Install ASP.NET 4.0 using the following command:</span></span>

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. <span data-ttu-id="548b0-123">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="548b0-123">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

3. <span data-ttu-id="548b0-124">請確定您已執行[Internet Information Services （IIS）伺服器憑證安裝指示](iis-server-certificate-installation-instructions.md)。</span><span class="sxs-lookup"><span data-stu-id="548b0-124">Ensure that you have performed the [Internet Information Services (IIS) Server Certificate Installation Instructions](iis-server-certificate-installation-instructions.md).</span></span>

4. <span data-ttu-id="548b0-125">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="548b0-125">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

5. <span data-ttu-id="548b0-126">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="548b0-126">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

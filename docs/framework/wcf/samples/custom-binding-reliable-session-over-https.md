---
title: HTTPS 上的自訂繫結可靠工作階段
ms.date: 03/30/2017
ms.assetid: 16aaa80d-3ffe-47c4-8b16-ec65c4d25f8d
ms.openlocfilehash: aec9bc11fab71a8e3adfe60e0c19b0ac4a9e3699
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241885"
---
# <a name="custom-binding-reliable-session-over-https"></a><span data-ttu-id="abf1f-102">HTTPS 上的自訂繫結可靠工作階段</span><span class="sxs-lookup"><span data-stu-id="abf1f-102">Custom Binding Reliable Session over HTTPS</span></span>

<span data-ttu-id="abf1f-103">這個範例示範透過可靠工作階段來使用 SSL 傳輸安全性。</span><span class="sxs-lookup"><span data-stu-id="abf1f-103">This sample demonstrates the use of SSL transport security with Reliable Sessions.</span></span> <span data-ttu-id="abf1f-104">可靠工作階段會實作 WS-Reliable Messaging 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="abf1f-104">Reliable Sessions implements the WS-Reliable Messaging protocol.</span></span> <span data-ttu-id="abf1f-105">您可以經由在可靠工作階段上撰寫 WS-Security 來建立安全可靠工作階段。</span><span class="sxs-lookup"><span data-stu-id="abf1f-105">You can have a secure reliable session by composing WS-Security over Reliable Sessions.</span></span> <span data-ttu-id="abf1f-106">但有時候，您可以改成選擇搭配 SSL 來使用 HTTP 傳輸安全性。</span><span class="sxs-lookup"><span data-stu-id="abf1f-106">But sometimes, you may choose to instead use HTTP transport security with SSL.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="abf1f-107">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="abf1f-107">The samples may already be installed on your machine.</span></span> <span data-ttu-id="abf1f-108">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="abf1f-108">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="abf1f-109">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="abf1f-109">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="abf1f-110">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="abf1f-110">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\ReliableSessionOverHttps`  
  
## <a name="sample-details"></a><span data-ttu-id="abf1f-111">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="abf1f-111">Sample Details</span></span>  

 <span data-ttu-id="abf1f-112">SSL 會確定封包本身的安全性。</span><span class="sxs-lookup"><span data-stu-id="abf1f-112">SSL ensures that the packets themselves are secured.</span></span> <span data-ttu-id="abf1f-113">值得注意的是，這種做法不同於使用 WS-Secure Conversation 來保護可靠工作階段。</span><span class="sxs-lookup"><span data-stu-id="abf1f-113">It is important to note that this is different from securing the reliable session using WS-Secure Conversation.</span></span>  
  
 <span data-ttu-id="abf1f-114">若要在 HTTPS 上使用可靠工作階段，您必須建立自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="abf1f-114">To use reliable session over HTTPS, you must create a custom binding.</span></span> <span data-ttu-id="abf1f-115">這個範例是以實作為計算機服務的 [消費者入門](getting-started-sample.md) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="abf1f-115">This sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service.</span></span> <span data-ttu-id="abf1f-116">使用可靠會話繫結項目和來建立自訂系結 [\<httpsTransport>](../../configure-apps/file-schema/wcf/httpstransport.md) 。</span><span class="sxs-lookup"><span data-stu-id="abf1f-116">A custom binding is created using the reliable session binding element and the [\<httpsTransport>](../../configure-apps/file-schema/wcf/httpstransport.md).</span></span> <span data-ttu-id="abf1f-117">下列組態是使用自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="abf1f-117">The following configuration is of the custom binding.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="reliableSessionOverHttps"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is exposed as http://localhost/servicemodelsamples/service.svc/mex-->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="reliableSessionOverHttps">  
          <reliableSession />  
          <httpsTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="true" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 <span data-ttu-id="abf1f-118">範例中的程式碼與 [消費者入門](getting-started-sample.md) 服務的程式碼相同。</span><span class="sxs-lookup"><span data-stu-id="abf1f-118">The program code in the sample is identical to that of the [Getting Started](getting-started-sample.md) service.</span></span> <span data-ttu-id="abf1f-119">您必須建立一個憑證並使用 [Web 伺服器憑證精靈] 指派憑證，再建置及執行範例。</span><span class="sxs-lookup"><span data-stu-id="abf1f-119">You must create a certificate and assign it by using the Web Server Certificate Wizard before building and running the sample.</span></span> <span data-ttu-id="abf1f-120">組態檔設定中的端點定義與繫結定義會啟用自訂繫結，如同下列用戶端的範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="abf1f-120">The endpoint definition and binding definition in the configuration file settings enable the use of custom binding as shown in the following sample configuration for the client.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint name=""  
                address="https://localhost/servicemodelsamples/service.svc"
                binding="customBinding"
                bindingConfiguration="reliableSessionOverHttps"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </client>  
  
      <bindings>  
        <customBinding>  
          <binding name="reliableSessionOverHttps">  
            <reliableSession />  
            <httpsTransport />  
          </binding>  
        </customBinding>
    </bindings>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 <span data-ttu-id="abf1f-121">指定的位址會使用 `https://` 配置。</span><span class="sxs-lookup"><span data-stu-id="abf1f-121">The address specified uses the `https://` scheme.</span></span>  
  
 <span data-ttu-id="abf1f-122">因為此範例中使用的憑證是使用 Makecert.exe 建立的測試憑證，所以當您嘗試從瀏覽器存取 HTTPs：位址（例如）時，就會出現安全性警示 `https://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="abf1f-122">Because the certificate used in this sample is a test certificate created with Makecert.exe, a security alert appears when you try to access an https: address, such as `https://localhost/servicemodelsamples/service.svc`, from your browser.</span></span> <span data-ttu-id="abf1f-123">為了讓 Windows Communication Foundation (WCF) 用戶端使用測試憑證，用戶端已新增一些額外的程式碼來隱藏安全性警示。</span><span class="sxs-lookup"><span data-stu-id="abf1f-123">To allow the Windows Communication Foundation (WCF) client to work with a test certificate in place, some additional code has been added to the client to suppress the security alert.</span></span> <span data-ttu-id="abf1f-124">使用實際執行憑證時，不需要這個程式碼及伴隨的類別。</span><span class="sxs-lookup"><span data-stu-id="abf1f-124">This code, and the accompanying class, is not required when using production certificates.</span></span>  

```csharp
// This code is required only for test certificates like those created by Makecert.exe.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```

 <span data-ttu-id="abf1f-125">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="abf1f-125">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="abf1f-126">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="abf1f-126">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="abf1f-127">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="abf1f-127">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="abf1f-128">使用下列命令安裝 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="abf1f-128">Install  ASP.NET 4.0 using the following command.</span></span>  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. <span data-ttu-id="abf1f-129">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="abf1f-129">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
3. <span data-ttu-id="abf1f-130">確定您已執行 [Internet Information Services (IIS) 伺服器憑證安裝指示](iis-server-certificate-installation-instructions.md)。</span><span class="sxs-lookup"><span data-stu-id="abf1f-130">Ensure that you have performed the [Internet Information Services (IIS) Server Certificate Installation Instructions](iis-server-certificate-installation-instructions.md).</span></span>  
  
4. <span data-ttu-id="abf1f-131">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="abf1f-131">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
5. <span data-ttu-id="abf1f-132">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="abf1f-132">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  

---
title: NamedPipe 啟用
ms.date: 03/30/2017
ms.assetid: f3c0437d-006c-442e-bfb0-6b29216e4e29
ms.openlocfilehash: 8d9a10b94c52514db611144352653b911d109056
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602462"
---
# <a name="namedpipe-activation"></a><span data-ttu-id="b98b8-102">NamedPipe 啟用</span><span class="sxs-lookup"><span data-stu-id="b98b8-102">NamedPipe Activation</span></span>

<span data-ttu-id="b98b8-103">此範例示範裝載服務，該服務使用 Windows Process Activation Service (WAS) 啟用透過名稱管道通訊的服務。</span><span class="sxs-lookup"><span data-stu-id="b98b8-103">This sample demonstrates hosting a service that uses Windows Process Activation Service (WAS) to activate a service that communicates over names pipes.</span></span> <span data-ttu-id="b98b8-104">這個範例是以[消費者入門](getting-started-sample.md)為基礎，而且需要 Windows Vista 才能執行。</span><span class="sxs-lookup"><span data-stu-id="b98b8-104">This sample is based on the [Getting Started](getting-started-sample.md) and requires Windows Vista to run.</span></span>

> [!NOTE]
> <span data-ttu-id="b98b8-105">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="b98b8-105">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b98b8-106">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b98b8-106">The samples may already be installed on your computer.</span></span> <span data-ttu-id="b98b8-107">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="b98b8-107">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="b98b8-108">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="b98b8-108">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="b98b8-109">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="b98b8-109">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\NamedPipeActivation`

## <a name="sample-details"></a><span data-ttu-id="b98b8-110">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="b98b8-110">Sample Details</span></span>

<span data-ttu-id="b98b8-111">此範例由用戶端主控台程式 (.exe) 和 Windows Process Activation Services (WAS) 啟動的工作處理序中裝載的服務程式庫 (.dll) 所組成。</span><span class="sxs-lookup"><span data-stu-id="b98b8-111">The sample consists of a client console program (.exe) and a service library (.dll) hosted in a worker process activated by the Windows Process Activation Services (WAS).</span></span> <span data-ttu-id="b98b8-112">您可以在主控台視窗中看到用戶端活動。</span><span class="sxs-lookup"><span data-stu-id="b98b8-112">Client activity is visible in the console window.</span></span>

<span data-ttu-id="b98b8-113">服務會實作定義要求-回覆通訊模式的合約。</span><span class="sxs-lookup"><span data-stu-id="b98b8-113">The service implements a contract that defines a request-reply communication pattern.</span></span> <span data-ttu-id="b98b8-114">合約是由 `ICalculator` 介面所定義，這個介面會公開數學運算 (加、減、乘、除)，如下列範例程式碼中所示。</span><span class="sxs-lookup"><span data-stu-id="b98b8-114">The contract is defined by the `ICalculator` interface, which exposes math operations (Add, Subtract, Multiply, and Divide), as shown in the following sample code.</span></span>

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

<span data-ttu-id="b98b8-115">用戶端會對指定的數學運算提出同步要求，然後服務實作計算並傳回適當結果。</span><span class="sxs-lookup"><span data-stu-id="b98b8-115">The client makes synchronous requests to a given math operation and the service implementation calculates and returns the appropriate result.</span></span>

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

<span data-ttu-id="b98b8-116">範例使用沒有安全性且經過修改的 `netNamedPipeBinding` 繫結。</span><span class="sxs-lookup"><span data-stu-id="b98b8-116">The sample uses a modified `netNamedPipeBinding` binding with no security.</span></span> <span data-ttu-id="b98b8-117">用戶端和服務的組態檔中會指定繫結。</span><span class="sxs-lookup"><span data-stu-id="b98b8-117">The binding is specified in the configuration files for the client and service.</span></span> <span data-ttu-id="b98b8-118">服務的繫結類型在端點項目的 `binding` 屬性中指定，如下列範例組態中所示。</span><span class="sxs-lookup"><span data-stu-id="b98b8-118">The binding type for the service is specified in the endpoint element’s `binding` attribute as shown in the following sample configuration.</span></span>

<span data-ttu-id="b98b8-119">如果您要使用安全的具名管理繫結，請將伺服器的安全性模式變更為需要的安全性設定，並在用戶端上再次執行 svcutil.exe 以取得更新的用戶端組態檔。</span><span class="sxs-lookup"><span data-stu-id="b98b8-119">If you want use a secured named pipe binding, change the server's security mode to the desired security setting and run svcutil.exe again on the client to obtain an updated client configuration file.</span></span>

```xml
<system.serviceModel>
        <services>
            <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">

        <!-- This endpoint is exposed at the base address provided by host: net.pipe://localhost/servicemodelsamples/service.svc  -->
        <endpoint address=""
                  binding="netNamedPipeBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at net.pipe://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexNamedPipeBinding"
                  contract="IMetadataExchange" />
      </service>
        </services>
        <bindings>
            <netNamedPipeBinding>
                <binding name="Binding1" >
                    <security mode = "None">
                    </security>
                </binding >
            </netNamedPipeBinding>
        </bindings>

    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
```

<span data-ttu-id="b98b8-120">用戶端的端點資訊設定如下列範例程式碼中所示。</span><span class="sxs-lookup"><span data-stu-id="b98b8-120">The client’s endpoint information is configured as shown in the following sample code.</span></span>

```xml
<system.serviceModel>

    <client>
      <endpoint name=""
                          address="net.pipe://localhost/servicemodelsamples/service.svc"
                          binding="netNamedPipeBinding"
                          bindingConfiguration="Binding1"
                          contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </client>

    <bindings>

      <!--  Following is the expanded configuration section for a NetNamedPipeBinding.
            Each property is configured with the default value. -->

      <netNamedPipeBinding>
        <binding name="Binding1"
                         maxBufferSize="65536"
                         maxConnections="10">
          <security mode = "None">
          </security>
        </binding >

      </netNamedPipeBinding>
    </bindings>

  </system.serviceModel>
```

<span data-ttu-id="b98b8-121">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="b98b8-121">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="b98b8-122">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="b98b8-122">Press ENTER in the client window to shut down the client.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="b98b8-123">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="b98b8-123">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="b98b8-124">請確定已安裝 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="b98b8-124">Ensure that IIS 7.0 is installed.</span></span> <span data-ttu-id="b98b8-125">WAS 啟用需要 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="b98b8-125">IIS 7.0 is required for WAS activation.</span></span>

2. <span data-ttu-id="b98b8-126">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b98b8-126">Ensure you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

    <span data-ttu-id="b98b8-127">此外，您必須安裝 WCF 非 HTTP 啟用元件：</span><span class="sxs-lookup"><span data-stu-id="b98b8-127">In addition, you must install the WCF non-HTTP activation components:</span></span>

    1. <span data-ttu-id="b98b8-128">在 [開始]\*\*\*\* 功能表內選擇 [控制台]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b98b8-128">From the **Start** menu, choose **Control Panel**.</span></span>

    2. <span data-ttu-id="b98b8-129">選取 [**程式和功能**]。</span><span class="sxs-lookup"><span data-stu-id="b98b8-129">Select **Programs and Features**.</span></span>

    3. <span data-ttu-id="b98b8-130">按一下 [**開啟或關閉 Windows 元件**]。</span><span class="sxs-lookup"><span data-stu-id="b98b8-130">Click **Turn Windows Components on or Off**.</span></span>

    4. <span data-ttu-id="b98b8-131">展開 [ **Microsoft .NET Framework 3.0** ] 節點，並檢查 [ **Windows Communication Foundation 非 HTTP 啟用**] 功能。</span><span class="sxs-lookup"><span data-stu-id="b98b8-131">Expand the **Microsoft .NET Framework 3.0** node and check the **Windows Communication Foundation Non-HTTP Activation** feature.</span></span>

3. <span data-ttu-id="b98b8-132">設定 Windows Process Activation Service (WAS) 以支援具名管道啟動。</span><span class="sxs-lookup"><span data-stu-id="b98b8-132">Configure the Windows Process Activation Service (WAS) to support named pipe activation.</span></span>

    <span data-ttu-id="b98b8-133">為了方便起見，在位於範例目錄中稱為 AddNetPipeSiteBinding.cmd 的批次檔中實作下列兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="b98b8-133">As a convenience, the following two steps are implemented in a batch file called AddNetPipeSiteBinding.cmd located in the sample directory.</span></span>

    1. <span data-ttu-id="b98b8-134">若要支援 net.pipe 啟動，預設的網站必須先繫結至 net.pipe 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b98b8-134">To support net.pipe activation, the default Web site must first be bound to the net.pipe protocol.</span></span> <span data-ttu-id="b98b8-135">使用以 IIS 7.0 管理工具集安裝的 appcmd.exe 完成此操作。</span><span class="sxs-lookup"><span data-stu-id="b98b8-135">This can be done using appcmd.exe, which is installed with the IIS 7.0 management toolset.</span></span> <span data-ttu-id="b98b8-136">從提高權限的 (系統管理員) 命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b98b8-136">From an elevated (administrator) command prompt, run the following command.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        -+bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > <span data-ttu-id="b98b8-137">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b98b8-137">This command is a single line of text.</span></span>

        <span data-ttu-id="b98b8-138">此命令新增繫結至預設網站的 net.pipe 網站。</span><span class="sxs-lookup"><span data-stu-id="b98b8-138">This command adds a net.pipe site binding to the default Web site.</span></span>

    2. <span data-ttu-id="b98b8-139">雖然網站中的所有應用程式共用常見的 net.pipe 繫結，但每個應用程式都可以個別啟用 net.pipe 支援。</span><span class="sxs-lookup"><span data-stu-id="b98b8-139">Although all applications within a site share a common net.pipe binding, each application can enable net.pipe support individually.</span></span> <span data-ttu-id="b98b8-140">若要啟用 /servicemodelsamples 應用程式的 net.pipe，請從提高權限的命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b98b8-140">To enable net.pipe for the /servicemodelsamples application, run the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.pipe
        ```

        > [!NOTE]
        > <span data-ttu-id="b98b8-141">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="b98b8-141">This command is a single line of text.</span></span>

        <span data-ttu-id="b98b8-142">此命令可讓您使用和來存取/servicemodelsamples 應用 `http://localhost/servicemodelsamples` 程式 `net.tcp://localhost/servicemodelsamples` 。</span><span class="sxs-lookup"><span data-stu-id="b98b8-142">This command enables the /servicemodelsamples application to be accessed using both `http://localhost/servicemodelsamples` and `net.tcp://localhost/servicemodelsamples`.</span></span>

4. <span data-ttu-id="b98b8-143">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="b98b8-143">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

5. <span data-ttu-id="b98b8-144">移除您為此範例新增的 net.pipe 網站繫結。</span><span class="sxs-lookup"><span data-stu-id="b98b8-144">Remove the net.pipe site binding you added for this sample.</span></span>

    <span data-ttu-id="b98b8-145">為了方便起見，下列兩個步驟會以位於範例目錄中的 RemoveNetPipeSiteBinding.cmd 批次檔實作：</span><span class="sxs-lookup"><span data-stu-id="b98b8-145">As a convenience, the following two steps are implemented in a batch file called RemoveNetPipeSiteBinding.cmd located in the sample directory:</span></span>

    1. <span data-ttu-id="b98b8-146">從提高權限的命令提示字元中執行下列命令，以從啟用的通訊協定清單中移除 net.tcp。</span><span class="sxs-lookup"><span data-stu-id="b98b8-146">Remove net.tcp from the list of enabled protocols by running the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > <span data-ttu-id="b98b8-147">這個命令必須輸入為單行文字。</span><span class="sxs-lookup"><span data-stu-id="b98b8-147">This command must be entered as a single line of text.</span></span>

    2. <span data-ttu-id="b98b8-148">從提高權限的命令提示字元中執行下列命令以移除 net.tcp 網站繫結。</span><span class="sxs-lookup"><span data-stu-id="b98b8-148">Remove the net.tcp site binding by running the following command from an elevated command prompt.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" --bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > <span data-ttu-id="b98b8-149">這個命令必須輸入為單行文字。</span><span class="sxs-lookup"><span data-stu-id="b98b8-149">This command must be typed in as a single line of text.</span></span>

## <a name="see-also"></a><span data-ttu-id="b98b8-150">請參閱</span><span class="sxs-lookup"><span data-stu-id="b98b8-150">See also</span></span>

- <span data-ttu-id="b98b8-151">[AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="b98b8-151">[AppFabric Hosting and Persistence Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span></span>

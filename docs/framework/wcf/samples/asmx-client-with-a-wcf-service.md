---
title: 含 WCF 服務的 ASMX 用戶端
ms.date: 03/30/2017
ms.assetid: 3ea381ee-ac7d-4d62-8c6c-12dc3650879f
ms.openlocfilehash: fd13d4907f1be09440387a36e14ecdc4926ba7e7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594773"
---
# <a name="asmx-client-with-a-wcf-service"></a><span data-ttu-id="9d218-102">含 WCF 服務的 ASMX 用戶端</span><span class="sxs-lookup"><span data-stu-id="9d218-102">ASMX Client with a WCF Service</span></span>

<span data-ttu-id="9d218-103">這個範例會示範如何使用 Windows Communication Foundation （WCF）建立服務，然後從非 WCF 用戶端（例如，.ASMX 用戶端）存取服務。</span><span class="sxs-lookup"><span data-stu-id="9d218-103">This sample demonstrates how to create a service using Windows Communication Foundation (WCF) and then access the service from a non-WCF client, such as an ASMX client.</span></span>

> [!NOTE]
> <span data-ttu-id="9d218-104">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="9d218-104">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="9d218-105">這個範例是由用戶端主控台程式 (.exe) 和網際網路資訊服務 (IIS) 所裝載的服務程式庫 (.dll) 所組成。</span><span class="sxs-lookup"><span data-stu-id="9d218-105">This sample consists of a client console program (.exe) and a service library (.dll) hosted by Internet Information Services (IIS).</span></span> <span data-ttu-id="9d218-106">服務會實作定義要求-回覆通訊模式的合約。</span><span class="sxs-lookup"><span data-stu-id="9d218-106">The service implements a contract that defines a request-reply communication pattern.</span></span> <span data-ttu-id="9d218-107">合約是由 `ICalculator` 介面所定義，這個介面會公開數學運算作業 (`Add`、`Subtract`、`Multiply` 和 `Divide`)。</span><span class="sxs-lookup"><span data-stu-id="9d218-107">The contract is defined by the `ICalculator` interface, which exposes math operations (`Add`, `Subtract`, `Multiply`, and `Divide`).</span></span> <span data-ttu-id="9d218-108">ASMX 用戶端會對數學運算作業提出同步要求，服務則會以結果回覆。</span><span class="sxs-lookup"><span data-stu-id="9d218-108">The ASMX client makes synchronous requests to a math operation and the service replies with the result.</span></span>

<span data-ttu-id="9d218-109">此服務會實作 `ICalculator` 合約，如下列程式碼中所定義。</span><span class="sxs-lookup"><span data-stu-id="9d218-109">The service implements an `ICalculator` contract as defined in the following code.</span></span>

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"), XmlSerializerFormat]
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

<span data-ttu-id="9d218-110"><xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 會將 CLR 型別對應成 XML 表示。</span><span class="sxs-lookup"><span data-stu-id="9d218-110">The <xref:System.Runtime.Serialization.DataContractSerializer> and <xref:System.Xml.Serialization.XmlSerializer> map CLR types to an XML representation.</span></span> <span data-ttu-id="9d218-111"><xref:System.Runtime.Serialization.DataContractSerializer> 解譯某些 XML 表示的方式與 XmlSerializer 的方式不同。</span><span class="sxs-lookup"><span data-stu-id="9d218-111">The <xref:System.Runtime.Serialization.DataContractSerializer> interprets some XML representations differently than XmlSerializer.</span></span> <span data-ttu-id="9d218-112">當使用 XmlSerializer 時，非 WCF proxy 產生器（例如 Wsdl.exe）會產生更能使用的介面。</span><span class="sxs-lookup"><span data-stu-id="9d218-112">Non-WCF proxy generators, such as Wsdl.exe, generate a more usable interface when the XmlSerializer is being used.</span></span> <span data-ttu-id="9d218-113"><xref:System.ServiceModel.XmlSerializerFormatAttribute>會套用至 `ICalculator` 介面，以確保使用 XMLSERIALIZER 將 CLR 類型對應至 XML。</span><span class="sxs-lookup"><span data-stu-id="9d218-113">The <xref:System.ServiceModel.XmlSerializerFormatAttribute> is applied to the `ICalculator` interface, to ensure that the XmlSerializer is used for mapping CLR types to XML.</span></span> <span data-ttu-id="9d218-114">服務實作會計算並傳回適當結果。</span><span class="sxs-lookup"><span data-stu-id="9d218-114">The service implementation calculates and returns the appropriate result.</span></span>

<span data-ttu-id="9d218-115">此服務會公開 (Expose) 單一的端點來與已使用組態檔 Web.config 定義之服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="9d218-115">The service exposes a single endpoint for communicating with the service, defined using a configuration file (Web.config).</span></span> <span data-ttu-id="9d218-116">端點是由位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="9d218-116">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="9d218-117">服務會公開位在網際網路資訊服務 (IIS) 主機提供之基底位址上的端點。</span><span class="sxs-lookup"><span data-stu-id="9d218-117">The service exposes the endpoint at the base address provided by the Internet Information Services (IIS) host.</span></span> <span data-ttu-id="9d218-118">`binding` 屬性會設定為 basicHttpBinding，它會提供使用 SOAP 1.1 並與 WS-I BasicProfile 1.1 相容的 HTTP 通訊，如下列範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="9d218-118">The `binding` attribute is set to basicHttpBinding that provides HTTP communications using SOAP 1.1, which is compliant with WS-I BasicProfile 1.1 as shown in the following sample configuration.</span></span>

```xml
<services>
  <service name="Microsoft.ServiceModel.Samples.CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc.  -->
    <endpoint address=""
              binding="basicHttpBinding"
              contract="Microsoft.ServiceModel.Samples.ICalculator" />
  </service>
</services>
```

<span data-ttu-id="9d218-119">.ASMX 用戶端會使用 Web 服務描述語言（WSDL）公用程式（Wsdl.exe）所產生的具型別 proxy，與 WCF 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="9d218-119">The ASMX client communicates with the WCF service using a typed proxy that is generated by the Web Services Description Language (WSDL) utility (Wsdl.exe).</span></span> <span data-ttu-id="9d218-120">此具型別的 Proxy 會包含在 generatedClient.cs 檔中。</span><span class="sxs-lookup"><span data-stu-id="9d218-120">The typed proxy is contained in the file generatedClient.cs.</span></span> <span data-ttu-id="9d218-121">WSDL 公用程式會擷取所指定服務的中繼資料，然後產生讓用戶端用來進行通訊的具型別 Proxy。</span><span class="sxs-lookup"><span data-stu-id="9d218-121">The WSDL utility retrieves metadata for the specified service and generates a typed proxy for use by a client to communicate.</span></span> <span data-ttu-id="9d218-122">根據預設，此架構不會公開任何中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d218-122">By default, the framework does not expose any metadata.</span></span> <span data-ttu-id="9d218-123">若要公開產生 proxy 所需的中繼資料，您必須加入 [\<serviceMetadata>](../../configure-apps/file-schema/wcf/servicemetadata.md) ，並將其 `httpGetEnabled` 屬性設為， `True` 如下列設定所示。</span><span class="sxs-lookup"><span data-stu-id="9d218-123">To expose the metadata required to generate the proxy, you must add a [\<serviceMetadata>](../../configure-apps/file-schema/wcf/servicemetadata.md) and set its `httpGetEnabled` attribute to `True` as shown in the following configuration.</span></span>

```xml
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <!-- Setting httpGetEnabled to True on the serviceMetadata
           behavior exposes the service's wsdl at <base address>?wsdl :
           http://localhost/servicemodelsamples/service.svc?wsdl -->
      <serviceMetadata httpGetEnabled="True"/>
      <serviceDebug includeExceptionDetailInFaults="False" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```

<span data-ttu-id="9d218-124">請從用戶端目錄中的命令提示字元執行下列命令，以產生具有型別的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="9d218-124">Run the following command from a command prompt in the client directory to generate the typed proxy.</span></span>

```console
wsdl /n:Microsoft.ServiceModel.Samples /o:generatedClient.cs /urlkey:CalculatorServiceAddress http://localhost/servicemodelsamples/service.svc?wsdl
```

<span data-ttu-id="9d218-125">藉由使用產生之具型別的 Proxy，用戶端便可以設定適當的位址來存取指定的服務端點。</span><span class="sxs-lookup"><span data-stu-id="9d218-125">By using the generated typed proxy, the client can access a given service endpoint by configuring the appropriate address.</span></span> <span data-ttu-id="9d218-126">用戶端會使用組態檔 (App.config) 來指定要進行通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="9d218-126">The client uses a configuration file (App.config) to specify the endpoint to communicate with.</span></span>

```xml
<appSettings>
  <add key="CalculatorServiceAddress"
       value="http://localhost/ServiceModelSamples/service.svc"/>
</appSettings>
```

<span data-ttu-id="9d218-127">用戶端實作會建構要開始與服務進行通訊之具型別 Proxy 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9d218-127">The client implementation constructs an instance of the typed proxy to begin communicating with the service.</span></span>

```csharp
// Create a client to the CalculatorService.
using (CalculatorService client = new CalculatorService())
{
    // Call the Add service operation.
    double value1 = 100.00D;
    double value2 = 15.99D;
    double result = client.Add(value1, value2);
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

    // Call the Subtract service operation.
    value1 = 145.00D;
    value2 = 76.54D;
    result = client.Subtract(value1, value2);
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);

    // Call the Multiply service operation.
    value1 = 9.00D;
    value2 = 81.25D;
    result = client.Multiply(value1, value2);
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);

    // Call the Divide service operation.
    value1 = 22.00D;
    value2 = 7.00D;
    result = client.Divide(value1, value2);
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);

}

Console.WriteLine();
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

<span data-ttu-id="9d218-128">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="9d218-128">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="9d218-129">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="9d218-129">Press ENTER in the client window to shut down the client.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="9d218-130">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="9d218-130">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="9d218-131">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="9d218-131">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="9d218-132">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9d218-132">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="9d218-133">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9d218-133">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9d218-134">如需傳遞和傳回復雜資料類型的詳細資訊，請參閱： [Windows Forms 用戶端中的資料](data-binding-in-a-windows-forms-client.md)系結、 [Windows Presentation Foundation 用戶端中的資料](data-binding-in-a-wpf-client.md)系結，以及[ASP.NET 用戶端中的資料](data-binding-in-an-aspnet-client.md)系結。</span><span class="sxs-lookup"><span data-stu-id="9d218-134">For more information about passing and returning complex data types see: [Data Binding in a Windows Forms Client](data-binding-in-a-windows-forms-client.md), [Data Binding in a Windows Presentation Foundation Client](data-binding-in-a-wpf-client.md), and [Data Binding in an ASP.NET Client](data-binding-in-an-aspnet-client.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d218-135">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9d218-135">The samples may already be installed on your machine.</span></span> <span data-ttu-id="9d218-136">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="9d218-136">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="9d218-137">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="9d218-137">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="9d218-138">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="9d218-138">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Interop\ASMX`

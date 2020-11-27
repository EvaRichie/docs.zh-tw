---
title: 中繼資料發行行為
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, metadata publishing sample
- Metadata Publishing Behaviors Sample [Windows Communication Foundation]
ms.assetid: 78c13633-d026-4814-910e-1c801cffdac7
ms.openlocfilehash: 7df0a8ce41b7a26f70a010b377213c8438fe659d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294335"
---
# <a name="metadata-publishing-behavior"></a><span data-ttu-id="9d57b-102">中繼資料發行行為</span><span class="sxs-lookup"><span data-stu-id="9d57b-102">Metadata Publishing Behavior</span></span>

<span data-ttu-id="9d57b-103">中繼資料發行行為範例會示範如何控制服務的中繼資料發行功能。</span><span class="sxs-lookup"><span data-stu-id="9d57b-103">The Metadata Publishing Behavior sample demonstrates how to control the metadata publishing features of a service.</span></span> <span data-ttu-id="9d57b-104">為了避免意外洩漏潛在的機密服務中繼資料，Windows Communication Foundation (WCF) 服務的預設設定會停用中繼資料發行。</span><span class="sxs-lookup"><span data-stu-id="9d57b-104">To prevent unintentional disclosure of potentially sensitive service metadata, the default configuration for Windows Communication Foundation (WCF) services disables metadata publishing.</span></span> <span data-ttu-id="9d57b-105">這個行為依預設為安全行為，但也表示您無法使用中繼資料匯入工具 (例如 Svcutil.exe) 來產生呼叫服務所需的用戶端程式碼，除非組態中已明確啟用服務的中繼發行行為。</span><span class="sxs-lookup"><span data-stu-id="9d57b-105">This behavior is secure by default, but also means that you cannot use a metadata import tool (such as Svcutil.exe) to generate the client code required to call the service unless the service’s metadata publishing behavior is explicitly enabled in configuration.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="9d57b-106">為了清楚說明，這個範例示範如何建立不安全的中繼資料發行端點。</span><span class="sxs-lookup"><span data-stu-id="9d57b-106">For clarity, this sample demonstrates how to create an unsecured metadata publishing endpoint.</span></span> <span data-ttu-id="9d57b-107">未經驗證的匿名使用者可能可以使用這類端點，所以部署前必須小心謹慎，才能確保公開服務中繼資料是否適切。</span><span class="sxs-lookup"><span data-stu-id="9d57b-107">Such endpoints are potentially available to anonymous unauthenticated consumers and care must be taken before deploying such endpoints to ensure that publicly disclosing a service’s metadata is appropriate.</span></span> <span data-ttu-id="9d57b-108">如需保護中繼資料端點的範例，請參閱 [自訂安全中繼資料端點](custom-secure-metadata-endpoint.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="9d57b-108">See the [Custom Secure Metadata Endpoint](custom-secure-metadata-endpoint.md) sample for a sample that secures a metadata endpoint.</span></span>  
  
 <span data-ttu-id="9d57b-109">此範例是以執行服務合約的 [消費者入門](getting-started-sample.md)為基礎 `ICalculator` 。</span><span class="sxs-lookup"><span data-stu-id="9d57b-109">The sample is based on the [Getting Started](getting-started-sample.md), which implements the `ICalculator` service contract.</span></span> <span data-ttu-id="9d57b-110">在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。</span><span class="sxs-lookup"><span data-stu-id="9d57b-110">In this sample, the client is a console application (.exe) and the service is hosted by Internet Information Services (IIS).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9d57b-111">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="9d57b-111">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="9d57b-112">為了讓服務公開中繼資料，服務上必須設定 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>。</span><span class="sxs-lookup"><span data-stu-id="9d57b-112">For a service to expose metadata, the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> must be configured on the service.</span></span> <span data-ttu-id="9d57b-113">當這個行為存在時，您便可以發行中繼資料，方法是將端點設定成將 <xref:System.ServiceModel.Description.IMetadataExchange> 合約當做 WS-MetadataExchange (MEX) 通訊協定的實作來進行公開。</span><span class="sxs-lookup"><span data-stu-id="9d57b-113">When this behavior is present, you can publish metadata by configuring an endpoint to expose the <xref:System.ServiceModel.Description.IMetadataExchange> contract as an implementation of a WS-MetadataExchange (MEX) protocol.</span></span> <span data-ttu-id="9d57b-114">為了方便起見，這個合約已經被指定成縮寫組態名稱，"IMetadataExchange"。</span><span class="sxs-lookup"><span data-stu-id="9d57b-114">As a convenience, this contract has been given the abbreviated configuration name of "IMetadataExchange".</span></span> <span data-ttu-id="9d57b-115">這個範例會使用 `mexHttpBinding`，這個快捷標準繫結等同於安全性模式設為 `wsHttpBinding` 的 `None`。</span><span class="sxs-lookup"><span data-stu-id="9d57b-115">This sample uses the `mexHttpBinding`, which is a convenience standard binding that is equivalent to the `wsHttpBinding` with the security mode set to `None`.</span></span> <span data-ttu-id="9d57b-116">端點中會使用 "mex" 的相對位址，當針對服務基底位址進行解析時，會產生的端點位址 `http://localhost/servicemodelsamples/service.svc/mex` 。</span><span class="sxs-lookup"><span data-stu-id="9d57b-116">A relative address of "mex" is used in the endpoint, which when resolved against the services base address results in an endpoint address of `http://localhost/servicemodelsamples/service.svc/mex`.</span></span> <span data-ttu-id="9d57b-117">此行為組態列出如下：</span><span class="sxs-lookup"><span data-stu-id="9d57b-117">The following shows the behavior configuration:</span></span>  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <!-- The serviceMetadata behavior publishes metadata through   
           the IMetadataExchange contract. When this behavior is   
           present, you can expose this contract through an endpoint   
           as shown below. Setting httpGetEnabled to true publishes   
           the service's WSDL at the <baseaddress>?wsdl, for example,  
           http://localhost/servicemodelsamples/service.svc?wsdl -->  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 <span data-ttu-id="9d57b-118">此 MEX 端點列出如下。</span><span class="sxs-lookup"><span data-stu-id="9d57b-118">The following shows the MEX endpoint.</span></span>  
  
```xml  
<!-- the MEX endpoint is exposed at   
     http://localhost/servicemodelsamples/service.svc/mex   
     To expose the IMetadataExchange contract, you   
     must enable the serviceMetadata behavior as demonstrated                           
     previously. -->  
<endpoint address="mex"  
          binding="mexHttpBinding"  
          contract="IMetadataExchange" />  
```  
  
 <span data-ttu-id="9d57b-119">這個範例會將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 屬性設定為 `true`，也會使用 HTTP GET 公開服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d57b-119">This sample sets the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> property to `true`, which also exposes the service's metadata using HTTP GET.</span></span> <span data-ttu-id="9d57b-120">若要啟用 HTTP GET 中繼資料端點，服務必須有 HTTP 基底位址。</span><span class="sxs-lookup"><span data-stu-id="9d57b-120">To enable an HTTP GET metadata endpoint, the service must have an HTTP base address.</span></span> <span data-ttu-id="9d57b-121">查詢字串 `?wsdl` 會用於服務的基底位址上，以便存取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d57b-121">The query string `?wsdl` is used on the base address of the service to access the metadata.</span></span> <span data-ttu-id="9d57b-122">例如，若要在網頁瀏覽器中查看服務的 WSDL，您可以使用此位址 `http://localhost/servicemodelsamples/service.svc?wsdl` 。</span><span class="sxs-lookup"><span data-stu-id="9d57b-122">For example, to see the WSDL for the service in a Web browser you would use the address `http://localhost/servicemodelsamples/service.svc?wsdl`.</span></span> <span data-ttu-id="9d57b-123">此外，您可以將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 設定為 `true`，以便使用這個行為來透過 HTTPS 公開中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d57b-123">Alternatively, you can use this behavior to expose metadata over HTTPS by setting <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> to `true`.</span></span> <span data-ttu-id="9d57b-124">這個作業需要 HTTPS 基底位址。</span><span class="sxs-lookup"><span data-stu-id="9d57b-124">This requires an HTTPS base address.</span></span>  
  
 <span data-ttu-id="9d57b-125">若要存取服務的 MEX 端點，請使用 [System.servicemodel Metadata Utility 工具 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="9d57b-125">To access the service's MEX endpoint use the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md).</span></span>  
  
 `svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs`  
  
 <span data-ttu-id="9d57b-126">這樣便會產生以該服務中繼資料為基礎的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9d57b-126">This generates a client based on the service's metadata.</span></span>  
  
 <span data-ttu-id="9d57b-127">若要使用 HTTP GET 存取服務的中繼資料，請將您的瀏覽器指向 `http://localhost/servicemodelsamples/service.svc?wsdl` 。</span><span class="sxs-lookup"><span data-stu-id="9d57b-127">To access the service's metadata using HTTP GET, point your browser to `http://localhost/servicemodelsamples/service.svc?wsdl`.</span></span>  
  
 <span data-ttu-id="9d57b-128">如果您移除這項行為並嘗試開啟服務，這時會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9d57b-128">If you remove this behavior and try to open the service you get an exception.</span></span> <span data-ttu-id="9d57b-129">這個錯誤的發生原因是如果不使用這項行為，透過 `IMetadataExchange` 合約設定的端點就不會有任何實作。</span><span class="sxs-lookup"><span data-stu-id="9d57b-129">This error occurs because without the behavior, the endpoint configured with the `IMetadataExchange` contract has no implementation.</span></span>  
  
 <span data-ttu-id="9d57b-130">如果將 `HttpGetEnabled` 設定為 `false`，您就會看到 CalculatorService 說明網頁而不是服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d57b-130">If you set `HttpGetEnabled` to `false`, you see the CalculatorService help page instead of seeing the service's metadata.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="9d57b-131">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="9d57b-131">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="9d57b-132">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="9d57b-132">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="9d57b-133">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9d57b-133">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="9d57b-134">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="9d57b-134">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="9d57b-135">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9d57b-135">The samples may already be installed on your machine.</span></span> <span data-ttu-id="9d57b-136">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="9d57b-136">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="9d57b-137">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="9d57b-137">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="9d57b-138">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="9d57b-138">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Metadata`  

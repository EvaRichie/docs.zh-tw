---
title: 服務描述
ms.date: 03/30/2017
ms.assetid: 7034b5d6-d608-45f3-b57d-ec135f83ff24
ms.openlocfilehash: c0fa389e9c894bcfec49ce7538b512c96f176c23
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262576"
---
# <a name="service-description"></a><span data-ttu-id="3915e-102">服務描述</span><span class="sxs-lookup"><span data-stu-id="3915e-102">Service Description</span></span>

<span data-ttu-id="3915e-103">服務描述範例會示範服務如何在執行階段擷取其服務描述資訊。</span><span class="sxs-lookup"><span data-stu-id="3915e-103">The Service Description sample demonstrates how a service can retrieve its service description information at runtime.</span></span> <span data-ttu-id="3915e-104">此範例是以 [消費者入門](getting-started-sample.md)為基礎，並已定義額外的服務作業來傳回有關服務的描述性資訊。</span><span class="sxs-lookup"><span data-stu-id="3915e-104">The sample is based on the [Getting Started](getting-started-sample.md), with an additional service operation defined to return descriptive information about the service.</span></span> <span data-ttu-id="3915e-105">傳回的資訊會列出服務的基底位址與端點。</span><span class="sxs-lookup"><span data-stu-id="3915e-105">The information that is returned lists the base addresses and endpoints for the service.</span></span> <span data-ttu-id="3915e-106">服務會使用 <xref:System.ServiceModel.OperationContext>、<xref:System.ServiceModel.ServiceHost> 和 <xref:System.ServiceModel.Description.ServiceDescription> 類別提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="3915e-106">The service provides this information using the <xref:System.ServiceModel.OperationContext>, <xref:System.ServiceModel.ServiceHost>, and <xref:System.ServiceModel.Description.ServiceDescription> classes.</span></span>  
  
 <span data-ttu-id="3915e-107">在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。</span><span class="sxs-lookup"><span data-stu-id="3915e-107">In this sample, the client is a console application (.exe) and the service is hosted by Internet Information Services (IIS).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3915e-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="3915e-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="3915e-109">這個範例有個修改版本的計算機合約，名稱為 `IServiceDescriptionCalculator`。</span><span class="sxs-lookup"><span data-stu-id="3915e-109">This sample has a modified version of the calculator contract called `IServiceDescriptionCalculator`.</span></span> <span data-ttu-id="3915e-110">該合約會定義名為 `GetServiceDescriptionInfo` 的其他服務作業，此作業會將描述服務的基底位址或位址以及服務端點或端點的多行字串傳回至用戶端。</span><span class="sxs-lookup"><span data-stu-id="3915e-110">The contract defines an additional service operation named `GetServiceDescriptionInfo` that returns a multi-line string to the client that describes the base address or addresses and service endpoint or endpoints for the service.</span></span>  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IServiceDescriptionCalculator  
{  
    [OperationContract]  
    int Add(int n1, int n2);  
    [OperationContract]  
    int Subtract(int n1, int n2);  
    [OperationContract]  
    int Multiply(int n1, int n2);  
    [OperationContract]  
    int Divide(int n1, int n2);  
    [OperationContract]  
    string GetServiceDescriptionInfo();  
}  
```  
  
 <span data-ttu-id="3915e-111">`GetServiceDescriptionInfo` 的實作程式碼會使用 <xref:System.ServiceModel.Description.ServiceDescription> 來列出服務端點。</span><span class="sxs-lookup"><span data-stu-id="3915e-111">The implementation code for `GetServiceDescriptionInfo` uses the <xref:System.ServiceModel.Description.ServiceDescription> to list the service endpoints.</span></span> <span data-ttu-id="3915e-112">因為服務端點可以有相對位址，所以它會先列出服務的基底位址。</span><span class="sxs-lookup"><span data-stu-id="3915e-112">Because service endpoints can have relative addresses, it first lists the base addresses for the service.</span></span> <span data-ttu-id="3915e-113">為了取得完整的這份資訊，該程式碼會使用 <xref:System.ServiceModel.OperationContext.Current%2A> 取得作業內容。</span><span class="sxs-lookup"><span data-stu-id="3915e-113">To get all of this information, the code obtains its operation context using <xref:System.ServiceModel.OperationContext.Current%2A>.</span></span> <span data-ttu-id="3915e-114"><xref:System.ServiceModel.ServiceHost> 和其 <xref:System.ServiceModel.Description.ServiceDescription> 物件，都是擷取自此作業內容。</span><span class="sxs-lookup"><span data-stu-id="3915e-114">The <xref:System.ServiceModel.ServiceHost> and its <xref:System.ServiceModel.Description.ServiceDescription> object are retrieved from the operation context.</span></span> <span data-ttu-id="3915e-115">為了列出服務的基底端點，該程式碼會逐一查看服務主機的 <xref:System.ServiceModel.ServiceHostBase.BaseAddresses%2A> 集合。</span><span class="sxs-lookup"><span data-stu-id="3915e-115">To list the base endpoints for the service, the code iterates through the service host's <xref:System.ServiceModel.ServiceHostBase.BaseAddresses%2A> collection.</span></span> <span data-ttu-id="3915e-116">為了列出服務的服務端點，該程式碼會逐一查看服務描述的端點集合。</span><span class="sxs-lookup"><span data-stu-id="3915e-116">To list the service endpoints for the service, the code iterates through the service description's endpoints collection.</span></span>  
  
```csharp
public string GetServiceDescriptionInfo()  
{  
    string info = "";  
    OperationContext operationContext = OperationContext.Current;  
    ServiceHost host = (ServiceHost)operationContext.Host;  
    ServiceDescription desc = host.Description;  
    // Enumerate the base addresses in the service host.  
    info += "Base addresses:\n";  
    foreach (Uri uri in host.BaseAddresses)  
    {  
        info += "    " + uri + "\n";  
    }  
    // Enumerate the service endpoints in the service description.  
    info += "Service endpoints:\n";  
    foreach (ServiceEndpoint endpoint in desc.Endpoints)  
    {  
        info += "    Address:  " + endpoint.Address + "\n";  
        info += "    Binding:  " + endpoint.Binding.Name + "\n";  
        info += "    Contract: " + endpoint.Contract.Name + "\n";  
    }  
     return info;  
}  
```  
  
 <span data-ttu-id="3915e-117">當執行範例時，您會看到計算機作業，然後服務資訊會由 `GetServiceDescriptionInfo` 作業傳回。</span><span class="sxs-lookup"><span data-stu-id="3915e-117">When you run the sample, you see the calculator operations and then the service information returned by the `GetServiceDescriptionInfo` operation.</span></span> <span data-ttu-id="3915e-118">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="3915e-118">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
Divide(22,7) = 3  
GetServiceDescriptionInfo  
Base addresses:  
    http://<machine-name>/ServiceModelSamples/service.svc  
    https://<machine-name>/ServiceModelSamples/service.svc  
Service endpoints:  
    Address:  http://<machine-name>/ServiceModelSamples/service.svc  
    Binding:  WSHttpBinding  
    Contract: IServiceDescriptionCalculator  
    Address:  http://<machine-name>/ServiceModelSamples/service.svc/mex  
    Binding:  MetadataExchangeHttpBinding  
    Contract: IMetadataExchange  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="3915e-119">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="3915e-119">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="3915e-120">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="3915e-120">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="3915e-121">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="3915e-121">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="3915e-122">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="3915e-122">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="3915e-123">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3915e-123">The samples may already be installed on your machine.</span></span> <span data-ttu-id="3915e-124">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="3915e-124">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="3915e-125">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="3915e-125">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="3915e-126">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="3915e-126">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ServiceDescription`  

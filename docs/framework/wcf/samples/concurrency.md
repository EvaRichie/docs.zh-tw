---
title: 並行
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, concurency sample
- Concurrency Sample [Windows Communication Foundation]
ms.assetid: f8dbdfb3-6858-4f95-abe3-3a1db7878926
ms.openlocfilehash: 69692f48cc1f45057e865a3908ddf41afc599bb1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96243248"
---
# <a name="concurrency"></a><span data-ttu-id="7dbce-102">並行</span><span class="sxs-lookup"><span data-stu-id="7dbce-102">Concurrency</span></span>

<span data-ttu-id="7dbce-103">並行範例會示範搭配 <xref:System.ServiceModel.ServiceBehaviorAttribute> 列舉使用 <xref:System.ServiceModel.ConcurrencyMode>，以控制服務的執行個體要循序處理或並行處理訊息。</span><span class="sxs-lookup"><span data-stu-id="7dbce-103">The Concurrency sample demonstrates using the <xref:System.ServiceModel.ServiceBehaviorAttribute> with the <xref:System.ServiceModel.ConcurrencyMode> enumeration, which controls whether an instance of a service processes messages sequentially or concurrently.</span></span> <span data-ttu-id="7dbce-104">此範例是以執行服務合約的 [消費者入門](getting-started-sample.md)為基礎 `ICalculator` 。</span><span class="sxs-lookup"><span data-stu-id="7dbce-104">The sample is based on the [Getting Started](getting-started-sample.md), which implements the `ICalculator` service contract.</span></span> <span data-ttu-id="7dbce-105">這個範例會定義繼承自 `ICalculatorConcurrency` 的新合約 `ICalculator`，並提供兩個額外作業來檢查服務的並行狀態。</span><span class="sxs-lookup"><span data-stu-id="7dbce-105">This sample defines a new contract, `ICalculatorConcurrency`, which inherits from `ICalculator`, providing two additional operations for inspecting the state of the service concurrency.</span></span> <span data-ttu-id="7dbce-106">藉由改變並行設定，您可以在執行用戶端時觀察行為上的改變。</span><span class="sxs-lookup"><span data-stu-id="7dbce-106">By altering the concurrency setting, you can observe the change in behavior by running the client.</span></span>  
  
 <span data-ttu-id="7dbce-107">在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。</span><span class="sxs-lookup"><span data-stu-id="7dbce-107">In this sample, the client is a console application (.exe) and the service is hosted by Internet Information Services (IIS).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7dbce-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="7dbce-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="7dbce-109">其中提供三種可用的並行模式：</span><span class="sxs-lookup"><span data-stu-id="7dbce-109">There are three concurrency modes available:</span></span>  
  
- <span data-ttu-id="7dbce-110">`Single`：每個服務執行個體都會一次處理一個訊息。</span><span class="sxs-lookup"><span data-stu-id="7dbce-110">`Single`: Each service instance processes one message at a time.</span></span> <span data-ttu-id="7dbce-111">這是預設的並行存取模式。</span><span class="sxs-lookup"><span data-stu-id="7dbce-111">This is the default concurrency mode.</span></span>  
  
- <span data-ttu-id="7dbce-112">`Multiple`：每個服務執行個體都會並行處理多個訊息。</span><span class="sxs-lookup"><span data-stu-id="7dbce-112">`Multiple`: Each service instance processes multiple messages concurrently.</span></span> <span data-ttu-id="7dbce-113">此服務實作必須是安全執行緒，才能使用這種並行模式。</span><span class="sxs-lookup"><span data-stu-id="7dbce-113">The service implementation must be thread-safe to use this concurrency mode.</span></span>  
  
- <span data-ttu-id="7dbce-114">`Reentrant`：每個服務執行個體都會一次處理一個訊息，但是接受可重新進入 (Re-entrant) 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7dbce-114">`Reentrant`: Each service instance processes one message at a time, but accepts reentrant calls.</span></span> <span data-ttu-id="7dbce-115">服務只會在呼叫時接受這些呼叫。重新進入範例會示範 [ConcurrencyMode](concurrencymode-reentrant.md) 中的可重入。</span><span class="sxs-lookup"><span data-stu-id="7dbce-115">The service only accepts these calls when it is calling out. Reentrant is demonstrated in the [ConcurrencyMode.Reentrant](concurrencymode-reentrant.md) sample.</span></span>  
  
 <span data-ttu-id="7dbce-116">並存的使用與執行個體模式有關。</span><span class="sxs-lookup"><span data-stu-id="7dbce-116">The use of concurrency is related to the instancing mode.</span></span> <span data-ttu-id="7dbce-117">在 <xref:System.ServiceModel.InstanceContextMode.PerCall> 執行個體中，並行模式沒有任何相關，因為每個訊息都是由新的服務執行個體處理。</span><span class="sxs-lookup"><span data-stu-id="7dbce-117">In <xref:System.ServiceModel.InstanceContextMode.PerCall> instancing, concurrency is not relevant, because each message is processed by a new service instance.</span></span> <span data-ttu-id="7dbce-118">在 <xref:System.ServiceModel.InstanceContextMode.Single> 執行個體中，只有 <xref:System.ServiceModel.ConcurrencyMode.Single> 或 <xref:System.ServiceModel.ConcurrencyMode.Multiple>，並行模式才相關，這點會依單一執行個體是循序處理或並行處理訊息而定。</span><span class="sxs-lookup"><span data-stu-id="7dbce-118">In <xref:System.ServiceModel.InstanceContextMode.Single> instancing, either <xref:System.ServiceModel.ConcurrencyMode.Single> or <xref:System.ServiceModel.ConcurrencyMode.Multiple> concurrency is relevant, depending on whether the single instance processes messages sequentially or concurrently.</span></span> <span data-ttu-id="7dbce-119">在 <xref:System.ServiceModel.InstanceContextMode.PerSession> 執行個體中，任何並行模式都可能相關。</span><span class="sxs-lookup"><span data-stu-id="7dbce-119">In <xref:System.ServiceModel.InstanceContextMode.PerSession> instancing, any of the concurrency modes may be relevant.</span></span>  
  
 <span data-ttu-id="7dbce-120">此服務類別會指定具有 `[ServiceBehavior(ConcurrencyMode=<setting>)]` 屬性的並行行為，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="7dbce-120">The service class specifies concurrency behavior with the `[ServiceBehavior(ConcurrencyMode=<setting>)]` attribute as shown in the code sample that follows.</span></span> <span data-ttu-id="7dbce-121">藉由變更要標記為註解的程式碼行，您便可以體驗 `Single` 和 `Multiple` 並行模式。</span><span class="sxs-lookup"><span data-stu-id="7dbce-121">By changing which lines are commented out, you can experiment with the `Single` and `Multiple` concurrency modes.</span></span> <span data-ttu-id="7dbce-122">請記得在變更並行模式後重建服務。</span><span class="sxs-lookup"><span data-stu-id="7dbce-122">Remember to rebuild the service after changing the concurrency mode.</span></span>  
  
```csharp
// Single allows a single message to be processed sequentially by each service instance.  
//[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, InstanceContextMode = InstanceContextMode.Single)]  
  
// Multiple allows concurrent processing of multiple messages by a service instance.  
// The service implementation should be thread-safe. This can be used to increase throughput.  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple, InstanceContextMode = InstanceContextMode.Single)]  
  
// Uses Thread.Sleep to vary the execution time of each operation.  
public class CalculatorService : ICalculatorConcurrency  
{  
    int operationCount;  
  
    public double Add(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(180);  
        return n1 + n2;  
    }  
  
    public double Subtract(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(100);  
        return n1 - n2;  
    }  
  
    public double Multiply(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(150);  
        return n1 * n2;  
    }  
  
    public double Divide(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(120);  
        return n1 / n2;  
    }  
  
    public string GetConcurrencyMode()  
    {
        // Return the ConcurrencyMode of the service.  
        ServiceHost host = (ServiceHost)OperationContext.Current.Host;  
        ServiceBehaviorAttribute behavior = host.Description.Behaviors.Find<ServiceBehaviorAttribute>();  
        return behavior.ConcurrencyMode.ToString();  
    }  
  
    public int GetOperationCount()  
    {
        // Return the number of operations.  
        return operationCount;  
    }  
}  
```  
  
 <span data-ttu-id="7dbce-123">此範例預設會搭配 <xref:System.ServiceModel.ConcurrencyMode.Multiple> 執行個體使用 <xref:System.ServiceModel.InstanceContextMode.Single> 並行。</span><span class="sxs-lookup"><span data-stu-id="7dbce-123">The sample uses <xref:System.ServiceModel.ConcurrencyMode.Multiple> concurrency with <xref:System.ServiceModel.InstanceContextMode.Single> instancing by default.</span></span> <span data-ttu-id="7dbce-124">用戶端程式碼已修改成使用非同步 Proxy。</span><span class="sxs-lookup"><span data-stu-id="7dbce-124">The client code has been modified to use an asynchronous proxy.</span></span> <span data-ttu-id="7dbce-125">這樣可以讓用戶端多次呼叫服務，而不用在每次呼叫之間等候回應。</span><span class="sxs-lookup"><span data-stu-id="7dbce-125">This allows the client to make multiple calls to the service without waiting for a response between each call.</span></span> <span data-ttu-id="7dbce-126">您可以觀察服務並行模式之行為的差異。</span><span class="sxs-lookup"><span data-stu-id="7dbce-126">You can observe the difference in behavior of the service concurrency mode.</span></span>  
  
 <span data-ttu-id="7dbce-127">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="7dbce-127">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="7dbce-128">這時會顯示用於執行服務的並行模式，同時呼叫每個作業，並接著顯示作業計數。</span><span class="sxs-lookup"><span data-stu-id="7dbce-128">The concurrency mode that the service is running under is displayed, each operation is called, and then the operation count is displayed.</span></span> <span data-ttu-id="7dbce-129">請注意，當並行模式為 `Multiple` 時，因為服務是同時處理多個訊息，所以結果的傳回順序會有別於作業的呼叫順序。</span><span class="sxs-lookup"><span data-stu-id="7dbce-129">Notice that when the concurrency mode is `Multiple`, the results are returned in a different order than how they were called, because the service processes multiple messages concurrently.</span></span> <span data-ttu-id="7dbce-130">藉由將並行模式變更為 `Single`，因為服務會循序處理每個訊息，所以結果的傳回順序就會相同於作業的呼叫順序。</span><span class="sxs-lookup"><span data-stu-id="7dbce-130">By changing the concurrency mode to `Single`, the results are returned in the order they were called, because the service processes each message sequentially.</span></span> <span data-ttu-id="7dbce-131">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="7dbce-131">Press ENTER in the client window to shut down the client.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="7dbce-132">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="7dbce-132">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="7dbce-133">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="7dbce-133">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="7dbce-134">如果您使用 Svcutil.exe 來產生 proxy 用戶端，請確定您包含此 `/async` 選項。</span><span class="sxs-lookup"><span data-stu-id="7dbce-134">If you use Svcutil.exe to generate the proxy client, ensure that you include the `/async` option.</span></span>  
  
3. <span data-ttu-id="7dbce-135">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="7dbce-135">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="7dbce-136">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="7dbce-136">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="7dbce-137">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7dbce-137">The samples may already be installed on your machine.</span></span> <span data-ttu-id="7dbce-138">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="7dbce-138">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="7dbce-139">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="7dbce-139">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="7dbce-140">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="7dbce-140">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Concurrency`  

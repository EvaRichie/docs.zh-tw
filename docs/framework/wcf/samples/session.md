---
title: 工作階段
ms.date: 03/30/2017
helpviewer_keywords:
- Sessions
ms.assetid: 36e1db50-008c-4b32-8d09-b56e790b8417
ms.openlocfilehash: 283c8b9641dcce8b0207d3be0024b57369d125ff
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591445"
---
# <a name="session"></a><span data-ttu-id="d0d60-102">工作階段</span><span class="sxs-lookup"><span data-stu-id="d0d60-102">Session</span></span>
<span data-ttu-id="d0d60-103">工作階段範例會示範如何實作需要工作階段的合約。</span><span class="sxs-lookup"><span data-stu-id="d0d60-103">The Session sample demonstrates how to implement a contract that requires a session.</span></span> <span data-ttu-id="d0d60-104">工作階段提供執行多個作業的內容。</span><span class="sxs-lookup"><span data-stu-id="d0d60-104">A session provides context for performing multiple operations.</span></span> <span data-ttu-id="d0d60-105">這可以讓服務將狀態與指定工作階段相關聯，如此一來後續作業就能夠使用之前作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="d0d60-105">This allows a service to associate state with a given session, such that subsequent operations can use the state of a previous operation.</span></span> <span data-ttu-id="d0d60-106">這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="d0d60-106">This sample is based on the [Getting Started](getting-started-sample.md), which implements a calculator service.</span></span> <span data-ttu-id="d0d60-107">`ICalculator` 合約已修改成允許執行一組算數運算，並同時保留執行結果。</span><span class="sxs-lookup"><span data-stu-id="d0d60-107">The `ICalculator` contract has been modified to allow a set of arithmetic operations to be performed, while keeping a running result.</span></span> <span data-ttu-id="d0d60-108">`ICalculatorSession` 合約會定義這項功能。</span><span class="sxs-lookup"><span data-stu-id="d0d60-108">This functionality is defined by the `ICalculatorSession` contract.</span></span> <span data-ttu-id="d0d60-109">此服務會維護用戶端的狀態，因為在進行計算時已呼叫了多個服務作業。</span><span class="sxs-lookup"><span data-stu-id="d0d60-109">The service maintains the state for a client as multiple service operations are called to perform a calculation.</span></span> <span data-ttu-id="d0d60-110">用戶端會呼叫 `Result()` 以擷取目前的結果，並且呼叫 `Clear()` 將結果清除為零。</span><span class="sxs-lookup"><span data-stu-id="d0d60-110">The client can retrieve the current result by calling `Result()` and clear the result to zero by calling `Clear()`.</span></span>  
  
 <span data-ttu-id="d0d60-111">在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。</span><span class="sxs-lookup"><span data-stu-id="d0d60-111">In this sample, the client is a console application (.exe) and the service is hosted by Internet Information Services (IIS).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d0d60-112">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="d0d60-112">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="d0d60-113">將合約的 <xref:System.ServiceModel.SessionMode> 設定為 `Required`，可以確定當合約透過特定繫結公開時，該繫結能夠支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="d0d60-113">Setting the <xref:System.ServiceModel.SessionMode> of the contract to `Required` ensures that when the contract is exposed over a particular binding, the binding supports sessions.</span></span> <span data-ttu-id="d0d60-114">如果繫結不支援工作階段，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d0d60-114">If the binding does not support sessions an exception is thrown.</span></span> <span data-ttu-id="d0d60-115">`ICalculatorSession` 介面已定義為可以呼叫一或多個作業以修改執行結果，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d0d60-115">The `ICalculatorSession` interface is defined such that one or more operations can be called, which modifies a running result, as shown in the following sample code.</span></span>  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required)]  
public interface ICalculatorSession  
{  
    [OperationContract(IsOneWay=true)]  
    void Clear();  
    [OperationContract(IsOneWay = true)]  
    void AddTo(double n);  
    [OperationContract(IsOneWay = true)]  
    void SubtractFrom(double n);  
    [OperationContract(IsOneWay = true)]  
    void MultiplyBy(double n);  
    [OperationContract(IsOneWay = true)]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
```  
  
 <span data-ttu-id="d0d60-116">服務會使用 <xref:System.ServiceModel.InstanceContextMode> 的 <xref:System.ServiceModel.InstanceContextMode.PerSession>，將指定的服務執行個體內容繫結至每個傳入工作階段。</span><span class="sxs-lookup"><span data-stu-id="d0d60-116">The service uses a <xref:System.ServiceModel.InstanceContextMode> of <xref:System.ServiceModel.InstanceContextMode.PerSession> to bind a given service instance context to each incoming session.</span></span> <span data-ttu-id="d0d60-117">這樣服務便可在本機成員變數中維護每個工作階段的執行結果。</span><span class="sxs-lookup"><span data-stu-id="d0d60-117">This allows the service to maintain the running result for each session in a local member variable.</span></span>  
  
```csharp
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class CalculatorService : ICalculatorSession  
{  
    double result = 0.0D;  
  
    public void Clear()  
    {  result = 0.0D; }  
  
    public void AddTo(double n)  
    {  result += n;   }  
  
    public void SubtractFrom(double n)  
    {  result -= n;   }  
  
    public void MultiplyBy(double n)  
    {  result *= n;   }  
  
    public void DivideBy(double n)  
    {  result /= n;   }  
  
    public double Result()  
    {  return result; }  
}  
```  
  
 <span data-ttu-id="d0d60-118">當您執行此範例時，用戶端會對伺服器提出幾個要求並要求結果，而該結果接著會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="d0d60-118">When you run the sample, the client makes several requests to the server and requests the result, which it then displays in the client console window.</span></span> <span data-ttu-id="d0d60-119">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="d0d60-119">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
(((0 + 100) - 50) * 17.65) / 2 = 441.25  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="d0d60-120">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="d0d60-120">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="d0d60-121">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d0d60-121">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="d0d60-122">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d0d60-122">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="d0d60-123">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d0d60-123">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="d0d60-124">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d0d60-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="d0d60-125">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="d0d60-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="d0d60-126">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="d0d60-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d0d60-127">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="d0d60-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Session`  

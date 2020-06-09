---
title: 延伸對錯誤處理和報告的控制
ms.date: 03/30/2017
ms.assetid: 45f996a7-fa00-45cb-9d6f-b368f5778aaa
ms.openlocfilehash: c7ca8d85220d65905bc4d9d220de366c331504a4
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600538"
---
# <a name="extending-control-over-error-handling-and-reporting"></a><span data-ttu-id="7d62a-102">延伸對錯誤處理和報告的控制</span><span class="sxs-lookup"><span data-stu-id="7d62a-102">Extending Control Over Error Handling and Reporting</span></span>
<span data-ttu-id="7d62a-103">這個範例會示範如何使用介面，在 Windows Communication Foundation （WCF）服務中擴充錯誤處理和錯誤報表的控制 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 。</span><span class="sxs-lookup"><span data-stu-id="7d62a-103">This sample demonstrates how to extend control over error handling and error reporting in a Windows Communication Foundation (WCF) service using the <xref:System.ServiceModel.Dispatcher.IErrorHandler> interface.</span></span> <span data-ttu-id="7d62a-104">此範例是以[消費者入門](getting-started-sample.md)為基礎，並在服務中加入一些額外的程式碼來處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d62a-104">The sample is based on the [Getting Started](getting-started-sample.md) with some additional code added to the service to handle errors.</span></span> <span data-ttu-id="7d62a-105">用戶端會強制產生數個錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="7d62a-105">The client forces several error conditions.</span></span> <span data-ttu-id="7d62a-106">服務則攔截這些錯誤並記錄在檔案中。</span><span class="sxs-lookup"><span data-stu-id="7d62a-106">The service intercepts the errors and logs them in a file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7d62a-107">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="7d62a-107">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="7d62a-108">服務可以使用 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面來攔截錯誤、進行處理，並影響報告錯誤的方式。</span><span class="sxs-lookup"><span data-stu-id="7d62a-108">Services can intercept errors, perform processing, and affect how errors are reported using the <xref:System.ServiceModel.Dispatcher.IErrorHandler> interface.</span></span> <span data-ttu-id="7d62a-109">這個介面有兩個可加以實作的方法：<xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 和 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>。</span><span class="sxs-lookup"><span data-stu-id="7d62a-109">The interface has two methods that can be implemented: <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> and <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>.</span></span> <span data-ttu-id="7d62a-110"><xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 方法可讓您新增、修改或隱藏回應例外狀況所產生的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7d62a-110">The <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> method allows you to add, modify, or suppress a fault message that is generated in response to an exception.</span></span> <span data-ttu-id="7d62a-111"><xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 方法可以在發生錯誤時進行錯誤處理，並控制是否可以執行其他錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="7d62a-111">The <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> method allows error processing to take place in the event of an error and controls whether additional error handling can run.</span></span>  
  
 <span data-ttu-id="7d62a-112">在這個範例中，`CalculatorErrorHandler` 型別會實作 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面。</span><span class="sxs-lookup"><span data-stu-id="7d62a-112">In this sample, the `CalculatorErrorHandler` type implements the <xref:System.ServiceModel.Dispatcher.IErrorHandler> interface.</span></span> <span data-ttu-id="7d62a-113">在</span><span class="sxs-lookup"><span data-stu-id="7d62a-113">In the</span></span>  
  
 <span data-ttu-id="7d62a-114"><xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 方法中，`CalculatorErrorHandler` 會將錯誤記錄寫入 c:\logs 中的 Error.txt 文字檔。</span><span class="sxs-lookup"><span data-stu-id="7d62a-114"><xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> method, the `CalculatorErrorHandler` writes a log of the error to an Error.txt text file in c:\logs.</span></span> <span data-ttu-id="7d62a-115">請注意，此範例會記錄錯誤，但不加以隱藏，目的是為了將該錯誤回報到用戶端。</span><span class="sxs-lookup"><span data-stu-id="7d62a-115">Note that the sample logs the fault and does not suppress it, allowing it to be reported back to the client.</span></span>  
  
```csharp
public class CalculatorErrorHandler : IErrorHandler
{
    // Provide a fault. The Message fault parameter can be replaced, or set to
    // null to suppress reporting a fault.

    public void ProvideFault(Exception error, MessageVersion version, ref Message fault)
    {
    }

    // HandleError. Log an error, then allow the error to be handled as usual.
    // Return true if the error is considered as already handled

    public bool HandleError(Exception error)
    {
        using (TextWriter tw = File.AppendText(@"c:\logs\error.txt"))
        {
            if (error != null)
            {
                tw.WriteLine("Exception: " + error.GetType().Name + " - " + error.Message);
            }
            tw.Close();
        }
        return true;
    }
}  
```  
  
 <span data-ttu-id="7d62a-116">`ErrorBehaviorAttribute` 是向服務註冊錯誤處理常式的機制。</span><span class="sxs-lookup"><span data-stu-id="7d62a-116">The `ErrorBehaviorAttribute` exists as a mechanism to register an error handler with a service.</span></span> <span data-ttu-id="7d62a-117">這個屬性接受單一型別參數。</span><span class="sxs-lookup"><span data-stu-id="7d62a-117">This attribute takes a single type parameter.</span></span> <span data-ttu-id="7d62a-118">此型別必須實作 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面，而且必須具有空的公用建構函式。</span><span class="sxs-lookup"><span data-stu-id="7d62a-118">That type should implement the <xref:System.ServiceModel.Dispatcher.IErrorHandler> interface and should have a public, empty constructor.</span></span> <span data-ttu-id="7d62a-119">屬性會接著產生錯誤處理常式型別執行個體的實體，然後將它安裝到服務中。</span><span class="sxs-lookup"><span data-stu-id="7d62a-119">The attribute then instantiates an instance of that error handler type and installs it into the service.</span></span> <span data-ttu-id="7d62a-120">而方式是實作 <xref:System.ServiceModel.Description.IServiceBehavior> 介面，然後再使用 <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> 方法將錯誤處理常式的執行個體新增至服務。</span><span class="sxs-lookup"><span data-stu-id="7d62a-120">It does this by implementing the <xref:System.ServiceModel.Description.IServiceBehavior> interface and then using the <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> method to add instances of the error handler to the service.</span></span>  
  
```csharp
// This attribute can be used to install a custom error handler for a service.  
public class ErrorBehaviorAttribute : Attribute, IServiceBehavior  
{  
    Type errorHandlerType;  
  
    public ErrorBehaviorAttribute(Type errorHandlerType)  
    {  
        this.errorHandlerType = errorHandlerType;  
    }  
  
    void IServiceBehavior.Validate(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
    }  
  
    void IServiceBehavior.AddBindingParameters(ServiceDescription description, ServiceHostBase serviceHostBase, System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints, BindingParameterCollection parameters)  
    {  
    }  
  
    void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
        IErrorHandler errorHandler;  
  
        try  
        {  
            errorHandler = (IErrorHandler)Activator.CreateInstance(errorHandlerType);  
        }  
        catch (MissingMethodException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must have a public empty constructor.", e);  
        }  
        catch (InvalidCastException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must implement System.ServiceModel.Dispatcher.IErrorHandler.", e);  
        }  
  
        foreach (ChannelDispatcherBase channelDispatcherBase in serviceHostBase.ChannelDispatchers)  
        {  
            ChannelDispatcher channelDispatcher = channelDispatcherBase as ChannelDispatcher;  
            channelDispatcher.ErrorHandlers.Add(errorHandler);  
        }
    }  
}  
```  
  
 <span data-ttu-id="7d62a-121">這個範例會實作一個計算機服務。</span><span class="sxs-lookup"><span data-stu-id="7d62a-121">The sample implements a calculator service.</span></span> <span data-ttu-id="7d62a-122">用戶端刻意將不合法的值提供給參數，導致服務上發生兩個錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d62a-122">The client deliberately causes two errors to occur on the service by providing parameters with illegal values.</span></span> <span data-ttu-id="7d62a-123">`CalculatorErrorHandler` 使用 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面將錯誤記錄到本機檔案，然後讓這些錯誤回報至用戶端。</span><span class="sxs-lookup"><span data-stu-id="7d62a-123">The `CalculatorErrorHandler` uses the <xref:System.ServiceModel.Dispatcher.IErrorHandler> interface to log the errors to a local file and then allows them to be reported back to the client.</span></span> <span data-ttu-id="7d62a-124">用戶端便會強制產生「除以零」和「引數超出範圍」的狀況。</span><span class="sxs-lookup"><span data-stu-id="7d62a-124">The client forces a divide by zero and an argument-out-of-range condition.</span></span>  
  
```csharp
try
{  
    Console.WriteLine("Forcing an error in Divide");  
    // Call the Divide service operation - trigger a divide by 0 error.  
    value1 = 22;  
    value2 = 0;  
    result = proxy.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
}  
catch (FaultException e)  
{  
    Console.WriteLine("FaultException: " + e.GetType().Name + " - " + e.Message);  
}  
catch (Exception e)  
{  
    Console.WriteLine("Exception: " + e.GetType().Name + " - " + e.Message);  
}  
```  
  
 <span data-ttu-id="7d62a-125">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="7d62a-125">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="7d62a-126">您將會看到其中已將「除以零」和「引數超出範圍」的狀況回報為錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d62a-126">You see the division by zero and the argument-out-of-range conditions being reported as faults.</span></span> <span data-ttu-id="7d62a-127">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="7d62a-127">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
Forcing an error in Divide  
FaultException: FaultException - Invalid Argument: The second argument must not be zero.  
Forcing an error in Factorial  
FaultException: FaultException - Invalid Argument: The argument must be greater than zero.  
  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="7d62a-128">c:\logs\errors.txt 檔案包含服務所記錄關於錯誤的資訊。</span><span class="sxs-lookup"><span data-stu-id="7d62a-128">The file c:\logs\errors.txt contains the information logged about the errors by the service.</span></span> <span data-ttu-id="7d62a-129">請注意，若要讓服務寫入目錄，您必須確定執行服務的程式（通常是 ASP.NET 或 Network Service）具有寫入目錄的許可權。</span><span class="sxs-lookup"><span data-stu-id="7d62a-129">Note that for the service to write to the directory you must make sure that the process under which the service is running (typically ASP.NET or Network Service) has permission to write to the directory.</span></span>  
  
```txt
Fault: Reason = Invalid Argument: The second argument must not be zero.  
Fault: Reason = Invalid Argument: The argument must be greater than zero.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="7d62a-130">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="7d62a-130">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="7d62a-131">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="7d62a-131">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="7d62a-132">若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="7d62a-132">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="7d62a-133">確定您已為 error.txt 檔案建立 c:\logs 目錄。</span><span class="sxs-lookup"><span data-stu-id="7d62a-133">Ensure you have created the c:\logs directory for the error.txt file.</span></span> <span data-ttu-id="7d62a-134">或者，修改 `CalculatorErrorHandler.HandleError` 中使用的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="7d62a-134">Or modify the file name used in `CalculatorErrorHandler.HandleError`.</span></span>  
  
4. <span data-ttu-id="7d62a-135">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="7d62a-135">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="7d62a-136">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d62a-136">The samples may already be installed on your machine.</span></span> <span data-ttu-id="7d62a-137">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="7d62a-137">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="7d62a-138">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="7d62a-138">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="7d62a-139">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="7d62a-139">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\ErrorHandling`  

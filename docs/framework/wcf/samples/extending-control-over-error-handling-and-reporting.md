---
title: 延伸對錯誤處理和報告的控制
ms.date: 03/30/2017
ms.assetid: 45f996a7-fa00-45cb-9d6f-b368f5778aaa
ms.openlocfilehash: 2e9298c6a282b9df8499458ad166e320d41e63a9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283324"
---
# <a name="extending-control-over-error-handling-and-reporting"></a>延伸對錯誤處理和報告的控制

這個範例示範如何使用介面，在 Windows Communication Foundation (WCF) 服務中擴充錯誤處理和錯誤報表的控制 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 。 此範例是以 [消費者入門](getting-started-sample.md) 為基礎，並將一些額外的程式碼新增至服務來處理錯誤。 用戶端會強制產生數個錯誤狀況。 服務則攔截這些錯誤並記錄在檔案中。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 服務可以使用 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面來攔截錯誤、進行處理，並影響報告錯誤的方式。 這個介面有兩個可加以實作的方法：<xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 和 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>。 <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 方法可讓您新增、修改或隱藏回應例外狀況所產生的錯誤訊息。 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 方法可以在發生錯誤時進行錯誤處理，並控制是否可以執行其他錯誤處理。  
  
 在這個範例中，`CalculatorErrorHandler` 型別會實作 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面。 在  
  
 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 方法中，`CalculatorErrorHandler` 會將錯誤記錄寫入 c:\logs 中的 Error.txt 文字檔。 請注意，此範例會記錄錯誤，但不加以隱藏，目的是為了將該錯誤回報到用戶端。  
  
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
  
 `ErrorBehaviorAttribute` 是向服務註冊錯誤處理常式的機制。 這個屬性接受單一型別參數。 此型別必須實作 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面，而且必須具有空的公用建構函式。 屬性會接著產生錯誤處理常式型別執行個體的實體，然後將它安裝到服務中。 而方式是實作 <xref:System.ServiceModel.Description.IServiceBehavior> 介面，然後再使用 <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> 方法將錯誤處理常式的執行個體新增至服務。  
  
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
  
 這個範例會實作一個計算機服務。 用戶端刻意將不合法的值提供給參數，導致服務上發生兩個錯誤。 `CalculatorErrorHandler` 使用 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 介面將錯誤記錄到本機檔案，然後讓這些錯誤回報至用戶端。 用戶端便會強制產生「除以零」和「引數超出範圍」的狀況。  
  
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
  
 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 您將會看到其中已將「除以零」和「引數超出範圍」的狀況回報為錯誤。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
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
  
 c:\logs\errors.txt 檔案包含服務所記錄關於錯誤的資訊。 請注意，若要讓服務寫入至目錄，您必須確定執行服務的進程 (通常是 ASP.NET 或網路服務) 有寫入目錄的許可權。  
  
```txt
Fault: Reason = Invalid Argument: The second argument must not be zero.  
Fault: Reason = Invalid Argument: The argument must be greater than zero.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。  
  
3. 確定您已為 error.txt 檔案建立 c:\logs 目錄。 或者，修改 `CalculatorErrorHandler.HandleError` 中使用的檔案名稱。  
  
4. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\ErrorHandling`  

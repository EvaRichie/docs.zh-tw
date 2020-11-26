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
# <a name="concurrency"></a>並行

並行範例會示範搭配 <xref:System.ServiceModel.ServiceBehaviorAttribute> 列舉使用 <xref:System.ServiceModel.ConcurrencyMode>，以控制服務的執行個體要循序處理或並行處理訊息。 此範例是以執行服務合約的 [消費者入門](getting-started-sample.md)為基礎 `ICalculator` 。 這個範例會定義繼承自 `ICalculatorConcurrency` 的新合約 `ICalculator`，並提供兩個額外作業來檢查服務的並行狀態。 藉由改變並行設定，您可以在執行用戶端時觀察行為上的改變。  
  
 在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 其中提供三種可用的並行模式：  
  
- `Single`：每個服務執行個體都會一次處理一個訊息。 這是預設的並行存取模式。  
  
- `Multiple`：每個服務執行個體都會並行處理多個訊息。 此服務實作必須是安全執行緒，才能使用這種並行模式。  
  
- `Reentrant`：每個服務執行個體都會一次處理一個訊息，但是接受可重新進入 (Re-entrant) 的呼叫。 服務只會在呼叫時接受這些呼叫。重新進入範例會示範 [ConcurrencyMode](concurrencymode-reentrant.md) 中的可重入。  
  
 並存的使用與執行個體模式有關。 在 <xref:System.ServiceModel.InstanceContextMode.PerCall> 執行個體中，並行模式沒有任何相關，因為每個訊息都是由新的服務執行個體處理。 在 <xref:System.ServiceModel.InstanceContextMode.Single> 執行個體中，只有 <xref:System.ServiceModel.ConcurrencyMode.Single> 或 <xref:System.ServiceModel.ConcurrencyMode.Multiple>，並行模式才相關，這點會依單一執行個體是循序處理或並行處理訊息而定。 在 <xref:System.ServiceModel.InstanceContextMode.PerSession> 執行個體中，任何並行模式都可能相關。  
  
 此服務類別會指定具有 `[ServiceBehavior(ConcurrencyMode=<setting>)]` 屬性的並行行為，如下列程式碼範例所示。 藉由變更要標記為註解的程式碼行，您便可以體驗 `Single` 和 `Multiple` 並行模式。 請記得在變更並行模式後重建服務。  
  
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
  
 此範例預設會搭配 <xref:System.ServiceModel.ConcurrencyMode.Multiple> 執行個體使用 <xref:System.ServiceModel.InstanceContextMode.Single> 並行。 用戶端程式碼已修改成使用非同步 Proxy。 這樣可以讓用戶端多次呼叫服務，而不用在每次呼叫之間等候回應。 您可以觀察服務並行模式之行為的差異。  
  
 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 這時會顯示用於執行服務的並行模式，同時呼叫每個作業，並接著顯示作業計數。 請注意，當並行模式為 `Multiple` 時，因為服務是同時處理多個訊息，所以結果的傳回順序會有別於作業的呼叫順序。 藉由將並行模式變更為 `Single`，因為服務會循序處理每個訊息，所以結果的傳回順序就會相同於作業的呼叫順序。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 如果您使用 Svcutil.exe 來產生 proxy 用戶端，請確定您包含此 `/async` 選項。  
  
3. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
4. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Concurrency`  

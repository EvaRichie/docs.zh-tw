---
title: 自我裝載
ms.date: 03/30/2017
helpviewer_keywords:
- Self hosted service
- Self Host Sample [Windows Communication Foundation]
ms.assetid: 05e68661-1ddf-4abf-a899-9bb1b8272a5b
ms.openlocfilehash: f5c46bc486e03cf86ada3a565a3c282cd81db286
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599941"
---
# <a name="self-host"></a>自我裝載
這個範例會示範如何在主控台應用程式中實作自我裝載的服務。 這個範例是以[消費者入門](getting-started-sample.md)為基礎。 服務的組態檔已經從 Web.config 重新命名為 App.config，並且修改為設定主機使用的基底位址。 服務的原始程式碼已經修改為實作靜態 `Main` 函式，這個函式會建立和開啟提供已設定之基底位址的服務主機。 服務實作已經修改為將每個作業的輸出寫入至主控台。 除了設定服務的正確端點位址外，用戶端未經過修改。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 此範例會實作靜態的 main 函式，以便為指定的 <xref:System.ServiceModel.ServiceHost> 型別建立 `CalculatorService`，如下列範例程式碼所示。  
  
```csharp
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost =
           new ServiceHost(typeof(CalculatorService)))  
    {  
        // Open the ServiceHost to create listeners
        // and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
    }  
}  
```  
  
 當服務裝載於網際網路資訊服務 (IIS) 或 Windows Process Activation Service (WAS) 時，服務的基底位址是由裝載環境提供。 在自我裝載案例中，您必須自行指定基底位址。 這項作業是使用的專案、子系的子系（子系）來完成 `add` [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md) [\<host>](../../configure-apps/file-schema/wcf/host.md) ， [\<service>](../../configure-apps/file-schema/wcf/service.md) 如下列範例設定所示。  
  
```xml  
<service
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
  ...  
</service>  
```  
  
 當您執行範例時，作業要求和回應會顯示在服務與用戶端主控台視窗中。 在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\SelfHost`  
  
## <a name="see-also"></a>請參閱

- [AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))

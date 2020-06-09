---
title: 擴充追蹤
ms.date: 03/30/2017
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
ms.openlocfilehash: 59bdfeea41bac812840ffe166895050a6cd1ad2d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600512"
---
# <a name="extend-tracing"></a>延伸追蹤

這個範例會示範如何在用戶端和服務程式代碼中撰寫使用者定義的活動追蹤，以擴充 Windows Communication Foundation （WCF）追蹤功能。 撰寫使用者定義的活動追蹤，可讓使用者建立追蹤活動，並將追蹤群組為工作的邏輯單位。 也可以透過傳輸 (在相同的端點內) 以及傳播 (跨端點) 方式來關聯活動。 在此範例中，用戶端與服務都會啟用追蹤。 如需如何在用戶端和服務設定檔中啟用追蹤的詳細資訊，請參閱[追蹤和訊息記錄](tracing-and-message-logging.md)。  
  
 這個範例是以[消費者入門](getting-started-sample.md)為基礎。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## <a name="tracing-and-activity-propagation"></a>追蹤與活動傳播  
 使用者定義的活動追蹤可讓使用者建立自己的追蹤活動，將追蹤分組成工作邏輯單元、透過傳輸和傳播來使活動相互關聯，以及降低 WCF 追蹤的效能成本（例如，記錄檔的磁碟空間成本）。  
  
### <a name="add-custom-sources"></a>新增自訂來源  
 使用者定義的追蹤可以同時新增至用戶端與服務程式碼。 將追蹤來源加入至用戶端或服務設定檔，可讓您記錄這些自訂追蹤，並顯示在[服務追蹤檢視器工具（svctraceviewer.exe .exe）](../service-trace-viewer-tool-svctraceviewer-exe.md)中。 下列程式碼示範如何將名為 `ServerCalculatorTraceSource` 之使用者定義的追蹤來源新增至組態檔。  
  
```xml  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>
....
```  
  
### <a name="correlate-activities"></a>相互關聯活動  
 若要直接關聯跨端點的活動，在 `propagateActivity` 追蹤來源中的 `true` 屬性必須設定為 `System.ServiceModel`。 此外，若要傳播追蹤而不經過 WCF 活動，必須關閉 [System.servicemodel 活動追蹤]。 這項設定將如下列程式碼範例所示。  
  
> [!NOTE]
> 關閉 ServiceModel 活動追蹤的方式不同於指定追蹤層級 (以設定為 Off 的 `switchValue` 屬性表示)。  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### <a name="lessen-performance-cost"></a>降低效能成本  
 將 `ActivityTracing` 追蹤來源中的 `System.ServiceModel` 設定為 Off 時會產生追蹤檔，其中只包含使用者定義的活動追蹤，而不包含任何 ServiceModel 活動追蹤。 排除 System.servicemodel 活動追蹤會產生更小的記錄檔。 不過，與 WCF 處理追蹤相互關聯的機會會遺失。  
  
## <a name="set-up-build-and-run-the-sample"></a>設定、建立和執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
## <a name="see-also"></a>請參閱

- [AppFabric 監控範例](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))

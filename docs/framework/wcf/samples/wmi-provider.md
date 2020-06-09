---
title: WMI 提供者
ms.date: 03/30/2017
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
ms.openlocfilehash: a01b4b70d4c497d1efb93bb53a7339f5f7f29ef9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591042"
---
# <a name="wmi-provider"></a>WMI 提供者
這個範例示範如何使用 WCF 內建的 Windows Management Instrumentation （WMI）提供者，在執行時間從 Windows Communication Foundation （WCF）服務收集資料。 此外，這個範例還會示範如何將使用者定義的 WMI 物件新增至服務。 此範例會啟用[消費者入門](getting-started-sample.md)的 WMI 提供者，並示範如何 `ICalculator` 在執行時間從服務收集資料。  
  
 WMI 是 Microsoft 對「Web 架構企業管理」(Web-Based Enterprise Management，WBEM) 標準的實作。 如需 WMI SDK 的詳細資訊，請參閱[Windows Management Instrumentation](/windows/desktop/WmiSdk/wmi-start-page)。 WBEM 是一套業界標準，說明應用程式如何將管理測試設備公開至外部管理工具。  
  
 WCF 會執行 WMI 提供者，這是在執行時間透過 WBEM 相容介面公開檢測的元件。 管理工具可以在執行階段，透過介面連接到服務。 WCF 會公開服務的屬性，例如位址、系結、行為和接聽程式。  
  
 內建 WMI 提供者可以在應用程式的組態檔中啟動。 這會透過 `wmiProviderEnabled` [\<diagnostics>](../../configure-apps/file-schema/wcf/diagnostics.md) 一節中的屬性完成 [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) ，如下列範例設定所示：  
  
```xml  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
```  
  
 這個組態項目會公開 WMI 介面。 現在，管理應用程式可以透過這個介面進行連線，並存取應用程式的管理測試設備。  
  
## <a name="custom-wmi-object"></a>自訂 WMI 物件  
 新增 WMI 物件至服務，可以將使用者定義的資訊連同內建 WMI 提供者的資訊一併公開。 只要使用 Installutil.exe 應用程式將服務的結構描述發行至 WMI，就能達成這個目的。 有關完成這項作業的指示以及詳細資料，可在本主題結尾的安裝指示中找到。  
  
## <a name="accessing-wmi-information"></a>存取 WMI 資訊  

您可以使用各種不同的方式來存取 WMI 資料。 Microsoft 提供腳本、Visual Basic 應用程式、c + + 應用程式和 .NET Framework 的 WMI Api。 如需詳細資訊，請參閱[使用 WMI](/windows/desktop/wmisdk/using-wmi)。
  
 這個範例會使用兩個 Java 指令碼：一個是用來列舉電腦上執行的服務及其部分屬性，而第二個則是用來檢視使用者定義的 WMI 資料。 指令碼會開啟 WMI 提供者的連線、剖析資料，以及顯示收集到的資料。  
  
 啟動範例以建立 WCF 服務的執行中實例。 在服務執行的同時，請於命令提示字元中使用下列命令來執行各個 Java 指令碼：  
  
```console  
cscript EnumerateServices.js  
```  
  
 指令碼會存取服務中包含的測試設備，然後產生下列輸出：  
  
```console  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 接下來，請執行第二個 Java 指令碼以顯示使用者定義的 WMI 資料：  
  
```console  
cscript EnumerateCustomObjects.js  
```  
  
 指令碼會存取服務中包含的使用者定義測試設備，然後產生下列輸出：  
  
```console
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
```  
  
 這項輸出顯示電腦上有一個服務在執行。 服務會公開一個實作 `ICalculator` 合約的端點。 端點所實作之行為和繫結的設定會以訊息堆疊個別項目的總和列出。  
  
 WMI 不限於公開 WCF 基礎結構的管理檢測。 應用程式也可以透過同樣的機制公開自己網域的特定資料項目。 WMI 是適用於檢查並控制 Web 服務的統一機制。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 您可以對裝載目錄中的 service.dll 檔案執行 InstallUtil.exe (InstallUtil.exe 的預設位置在 "%WINDIR%\Microsoft.NET\Framework\v4.0.30319")，將服務結構描述發行至 WMI。 只有在已對 service.dll 檔案進行變更時，才需要執行這個步驟。
  
4. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
    > [!NOTE]
    > 如果您在安裝 ASP.NET 之後安裝了 WCF，可能需要執行 "% WINDIR% \Net\Framework\v3.0\Windows Communication Foundation\servicemodelreg.exe "-r-x，授與 ASPNET 帳戶發行 WMI 物件的許可權。  
  
5. 請使用命令 `cscript EnumerateServices.js` 或 `cscript EnumerateCustomObjects.js`，檢視由範例透過 WMI 呈現的資料。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## <a name="see-also"></a>請參閱

- [AppFabric 監控範例](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))

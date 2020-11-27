---
title: WCF 效能計數器
ms.date: 03/30/2017
helpviewer_keywords:
- performance counters [WCF]
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
ms.openlocfilehash: a5b00980cb8c2b06b224630e766e49bafe343c76
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266099"
---
# <a name="wcf-performance-counters"></a>WCF 效能計數器

Windows Communication Foundation (WCF) 包含一組大量的效能計數器，可協助您測量應用程式的效能。  
  
## <a name="enabling-performance-counters"></a>啟用效能計數器  

 您可以透過 WCF 服務的 app.config 設定檔啟用 WCF 服務的效能計數器，如下所示：  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 `performanceCounters` 屬性可設為啟用特定類型的效能計數器。 有效值為  
  
- All：所有類別的計數器 (ServiceModelService、ServiceModelEndpoint 和 ServiceModelOperation) 都會啟用。  
  
- ServiceOnly：只啟用 ServiceModelService 類別的計數器。 這是預設值。  
  
- Off：ServiceModel* 效能計數器會停用。  
  
 如果您想要啟用所有 WCF 應用程式的效能計數器，您可以將設定設定放在 Machine.config 檔案中。  如需有關為電腦上的效能計數器設定足夠記憶體的詳細資訊，請參閱下面的 **效能計數器的增加記憶體大小** 一節。  
  
 如果您使用 WCF 擴充性點，例如自訂作業啟動程式，您也應該發出自己的效能計數器。 這是因為如果您執行了擴充點，WCF 可能不會再于預設路徑中發出標準效能計數器資料。 如果您沒有實作手動效能計數器支援，可能無法看見預期的效能計數器資料。  
  
 您也可以在程式碼中啟用效能計數器，如下所示：  
  
```csharp
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## <a name="viewing-performance-data"></a>檢視效能資料  

 若要檢視效能計數器所擷取的資料，您可以使用隨附於 Windows 的效能監視器 (Perfmon.exe)。 您可以藉由前往 [ **開始**]，然後按一下 [ **執行** ]，然後在對話方塊中輸入，來啟動這 `perfmon.exe` 項工具。  
  
> [!NOTE]
> 效能計數器執行個體可能會在端點發送器處理完成最後一個訊息之前釋出。 如此可能導致少數訊息的效能資料未能予以擷取  
  
## <a name="increasing-memory-size-for-performance-counters"></a>為效能計數器增加記憶體大小  

 WCF 針對其效能計數器類別使用不同的共用記憶體。  
  
 根據預設，不同的共用記憶體會設為全域效能計數器記憶體的四分之一。 預設的全域效能計數器記憶體為 524,288 個位元組。 因此，三個 WCF 效能計數器類別的預設大小為大約128KB。 視電腦上 WCF 應用程式的執行時間特性而定，效能計數器記憶體可能會耗盡。 發生這種情況時，WCF 會將錯誤寫入應用程式事件記錄檔。 錯誤的內容會說明效能計數器並未載入，且項目中會包含例外狀況「System.InvalidOperationException：自訂計數器檔案檢視記憶體不足」。 如果已啟用錯誤層級的追蹤，則同樣會追蹤這個錯誤。 如果效能計數器記憶體用盡，繼續執行您的 WCF 應用程式並啟用效能計數器，可能會導致效能降低。 如果您是電腦的系統管理員，則應為電腦設定配置足夠的記憶體，支援可隨時存在的效能計數器數目上限。  
  
 您可以在登錄中變更 WCF 類別的效能計數器記憶體量。 若要執行這項操作，您必須將名為 `FileMappingSize` 的新 DWORD 值加入下列三個位置，並且將它設為所需的值 (以位元組為單位)。 重新啟動您的電腦，讓這些變更生效。  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance  
  
 處置掉大量物件 (例如 ServiceHost)，但在等待進行記憶體回收時，`PrivateBytes` 效能計數器將登錄相當大的數目。 若要解決這個問題，您可以加入自己的應用程式專屬計數器，或是使用 `performanceCounters` 屬性，僅啟用服務層級的計數器。  
  
## <a name="types-of-performance-counters"></a>效能計數器類型  

 效能計數器分成三種不同的層級：服務、端點和作業。  
  
 您可以使用 WMI 擷取效能計數器執行個體的名稱。 例如，  
  
- 您可以透過 WMI [服務](../wmi/service.md) 實例的 "CounterInstanceName" 屬性取得服務計數器實例名稱。  
  
- 端點計數器實例名稱可透過 WMI [端點](../wmi/endpoint.md) 實例的 "CounterInstanceName" 屬性取得。  
  
- 您可以透過 WMI [端點](../wmi/endpoint.md) 實例的 "GetOperationCounterInstanceName" 方法取得作業計數器實例名稱。  
  
 如需 WMI 的詳細資訊，請參閱 [使用 Windows Management Instrumentation 進行診斷](../wmi/index.md)。  
  
### <a name="service-performance-counters"></a>服務效能計數器  

 服務效能計數器會測量整體的服務行為，而且可用於診斷整個服務的效能。 以效能監視器進行檢視時，可以在 `ServiceModelService 4.0.0.0` 效能物件下找到它們。 執行個體會使用以下模式來命名：  
  
`ServiceName@ServiceBaseAddress`
  
 服務範圍中之計數器是從端點集合中的計數器彙總而來的。  
  
 當建立新的 InstanceContext 時，會遞增服務執行個體建立的效能計數器。 請注意，即使您收到不停用訊息 (現有服務)，或者您從一個工作階段連接到執行個體、結束執行個體，然後再重新從另一個執行個體連線，都還是會建立新的 InstanceContext。  
  
### <a name="endpoint-performance-counters"></a>端點效能計數器  

 您以端點效能計數器查看的資料，反映了端點接受訊息的方式。 使用效能監視器進行檢視時，可以在 `ServiceModelEndpoint 4.0.0.0` 效能物件下找到它們。 執行個體會使用以下模式來命名：  
  
`(ServiceName).(ContractName)@(endpoint listener address)`
  
 這些資料與針對個別作業所收集的資料類似，但是只會彙總端點之間的資料。  
  
 端點範圍中的計數器是從作業集合中的計數器彙總而來的。  
  
> [!NOTE]
> 如果兩個端點擁有相同的合約名稱和位址，則它們都會對應到相同的計數器執行個體。  
  
### <a name="operation-performance-counters"></a>作業效能計數器  

 當使用效能監視器進行檢視時，您可以在 `ServiceModelOperation 4.0.0.0` 效能物件中找到作業效能計數器。 每個作業都有個別的執行個體。 也就是，如果指定的合約有 10 個作業，就會有 10 個作業計數器執行個體與該合約產生關聯。 物件執行個體會使用以下模式來命名：  
  
`(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)`
  
 這個計數器能夠讓您測量呼叫的使用狀況，以及作業的執行效能。  
  
 如果可在多個範圍內看見此類計數器，則從較高範圍所收集的資料會與來自較低範圍的資料進行彙總。 例如，在端點的 `Calls` 代表該端點內所有作業呼叫的加總，而在服務中的 `Calls`，則代表服務內所有端點之所有呼叫的加總。  
  
> [!NOTE]
> 如果您的合約上有重複的作業名稱，則這兩個作業只能取得一個計數器執行個體。  
  
## <a name="programming-the-wcf-performance-counters"></a>WCF 效能計數器程式設計  

SDK 安裝資料夾中安裝了數個檔案，因此您可以透過程式設計的方式存取 WCF 效能計數器。 這些檔案列示如下：
  
- *\_ServiceModelEndpointPerfCounters.vrg*
- *\_ServiceModelOperationPerfCounters.vrg*
- *\_ServiceModelServicePerfCounters.vrg*  
- *\_SMSvcHostPerfCounters.vrg*
- *\_TransactionBridgePerfCounters.vrg*
  
如需如何以程式設計方式存取計數器的詳細資訊，請參閱 [效能計數器程式設計架構](/previous-versions/visualstudio/visual-studio-2008/5f9bkxzf(v=vs.90))。
  
## <a name="see-also"></a>另請參閱

- [系統管理與診斷](../index.md)

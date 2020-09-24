---
title: <serviceThrottling>
ms.date: 03/30/2017
ms.assetid: a337d064-1e64-4209-b4a9-db7fdb7e3eaf
ms.openlocfilehash: 0c6d844ac287037b7a546d3a48e7cd924e8a63d1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153608"
---
# \<serviceThrottling>

指定 Windows Communication Foundation (WCF) 服務的節流機制。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceThrottling>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<serviceThrottling maxConcurrentCalls="Integer"
                   maxConcurrentInstances="Integer"
                   maxConcurrentSessions="Integer" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|maxConcurrentCalls|正整數，限制同時在 <xref:System.ServiceModel.ServiceHost> 上進行處理的訊息數目。 超出上限的呼叫將排入佇列。 將這個值設定為 0 相當於設定為 Int32.MaxValue。 預設值是 16 * 處理器計數。|  
|maxConcurrentInstances|正整數，限制同時在 <xref:System.ServiceModel.InstanceContext> 上執行的 <xref:System.ServiceModel.ServiceHost> 物件數目。 當限制之內的位置可供使用時，建立其他執行個體的要求便會進入佇列並完成。 預設值是 maxConcurrentSessions 和 MaxConcurrentCalls 的總和|  
|maxConcurrentSessions|正整數，限制 <xref:System.ServiceModel.ServiceHost> 物件可以接受的工作階段數目。<br /><br /> 服務將接受超過限制的連線，但只有低於限制個數的通道為作用中 (可從該通道讀取訊息)。 將這個值設定為 0 相當於設定為 Int32.MaxValue。 預設值是 100 * 處理器計數。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|指定行為項目。|  
  
## <a name="remarks"></a>備註  

 節流控制會限制同時呼叫、並行執行個體或工作階段的數目，以防止過度消耗資源。  
  
 每次達到這些屬性值時，就會寫入追蹤。 第一個追蹤會寫入成為警告。  
  
## <a name="example"></a>範例  

 下列組態範例指定服務將同時呼叫上限限制為 2，且將並行執行個體上限限制為 10。 如需執行這個範例的詳細範例，請參閱 [節流](../../../wcf/samples/throttling.md)。  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <serviceDebug includeExceptionDetailInFaults="False" />
      <serviceMetadata httpGetEnabled="True" />
      <!-- Specify throttling behavior -->
      <serviceThrottling maxConcurrentCalls="2"
                         maxConcurrentInstances="10" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.Configuration.ServiceThrottlingElement>
- [使用 ServiceThrottlingBehavior 來控制 WCF 服務效能](../../../wcf/feature-details/using-servicethrottlingbehavior-to-control-wcf-service-performance.md)

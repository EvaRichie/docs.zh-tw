---
title: 使用 ServiceThrottlingBehavior 來控制 WCF 服務效能
ms.date: 03/30/2017
helpviewer_keywords:
- behavior [WCF], service performance
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
ms.openlocfilehash: 44cc924de0c3079bb2f8125a7ac63fa494d4aca1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289408"
---
# <a name="using-servicethrottlingbehavior-to-control-wcf-service-performance"></a>使用 ServiceThrottlingBehavior 來控制 WCF 服務效能

<xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 類別會公開可用來限制應用程式層級上所能建立之執行個體或工作階段數目的屬性。 您可以使用此行為，微調 Windows Communication Foundation (WCF) 應用程式的效能。  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a>控制服務執行個體及同時呼叫的數目  

 您可以使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 屬性指定透過 <xref:System.ServiceModel.ServiceHost> 類別主動處理的訊息數目上限，並使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 屬性來指定服務中 <xref:System.ServiceModel.InstanceContext> 物件的數目上限。  
  
 因為決定這些屬性的設定，通常會在執行應用程式的實際體驗進行負載的實際經驗之後發生，因此 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 屬性的設定通常是在應用程式佈建檔中使用元素來指定 [\<serviceThrottling>](../../configure-apps/file-schema/wcf/servicethrottling.md) 。  
  
 下列程式碼範例簡單示範如何從應用程式組態檔使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 類別，將 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 和 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 屬性設定為 1。 至於特定應用程式的最佳設定，則需要透過實際經驗來判斷。  
  
 [!code-xml[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  
  
 確切的執行階段行為將取決於 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 屬性的值，因為這兩個屬性分別控制可在作業中同時執行的訊息數目，以及 <xref:System.ServiceModel.InstanceContext> 服務相對於傳入通道工作階段的存留期。  
  
 如需詳細資訊，請參閱 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 和 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>

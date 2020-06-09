---
title: 使用 ServiceThrottlingBehavior 來控制 WCF 服務效能
ms.date: 03/30/2017
helpviewer_keywords:
- behavior [WCF], service performance
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
ms.openlocfilehash: 9cc5141805504bc46391105f475860b032f12d32
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600227"
---
# <a name="using-servicethrottlingbehavior-to-control-wcf-service-performance"></a><span data-ttu-id="99c4e-102">使用 ServiceThrottlingBehavior 來控制 WCF 服務效能</span><span class="sxs-lookup"><span data-stu-id="99c4e-102">Using ServiceThrottlingBehavior to Control WCF Service Performance</span></span>
<span data-ttu-id="99c4e-103"><xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 類別會公開可用來限制應用程式層級上所能建立之執行個體或工作階段數目的屬性。</span><span class="sxs-lookup"><span data-stu-id="99c4e-103">The <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> class exposes properties that you can use to limit how many instances or sessions are created at the application level.</span></span> <span data-ttu-id="99c4e-104">使用這種行為，您可以微調 Windows Communication Foundation （WCF）應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="99c4e-104">Using this behavior, you can fine-tune the performance of your Windows Communication Foundation (WCF) application.</span></span>  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a><span data-ttu-id="99c4e-105">控制服務執行個體及同時呼叫的數目</span><span class="sxs-lookup"><span data-stu-id="99c4e-105">Controlling Service Instances and Concurrent Calls</span></span>  
 <span data-ttu-id="99c4e-106">您可以使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 屬性指定透過 <xref:System.ServiceModel.ServiceHost> 類別主動處理的訊息數目上限，並使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 屬性來指定服務中 <xref:System.ServiceModel.InstanceContext> 物件的數目上限。</span><span class="sxs-lookup"><span data-stu-id="99c4e-106">Use the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> property to specify the maximum number of messages actively processing across a <xref:System.ServiceModel.ServiceHost> class, and the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> property to specify the maximum number of <xref:System.ServiceModel.InstanceContext> objects in the service.</span></span>  
  
 <span data-ttu-id="99c4e-107">由於判斷這些屬性的設定通常會在針對載入執行應用程式的實際經驗之後發生，因此屬性的設定 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 通常會使用專案指定于應用程式佈建檔中 [\<serviceThrottling>](../../configure-apps/file-schema/wcf/servicethrottling.md) 。</span><span class="sxs-lookup"><span data-stu-id="99c4e-107">Because determining the settings for these properties usually takes place after real-world experience running the application against loads, the settings for the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> properties is typically specified in an application configuration file using the [\<serviceThrottling>](../../configure-apps/file-schema/wcf/servicethrottling.md) element.</span></span>  
  
 <span data-ttu-id="99c4e-108">下列程式碼範例簡單示範如何從應用程式組態檔使用 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> 類別，將 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 和 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 屬性設定為 1。</span><span class="sxs-lookup"><span data-stu-id="99c4e-108">The following code example shows the use of the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> class from an application configuration file that sets the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>, <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>, and <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> properties to 1 as a trivial example.</span></span> <span data-ttu-id="99c4e-109">至於特定應用程式的最佳設定，則需要透過實際經驗來判斷。</span><span class="sxs-lookup"><span data-stu-id="99c4e-109">Real-world experience determines the optimal settings for any particular application.</span></span>  
  
 [!code-xml[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  
  
 <span data-ttu-id="99c4e-110">確切的執行階段行為將取決於 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 屬性的值，因為這兩個屬性分別控制可在作業中同時執行的訊息數目，以及 <xref:System.ServiceModel.InstanceContext> 服務相對於傳入通道工作階段的存留期。</span><span class="sxs-lookup"><span data-stu-id="99c4e-110">The exact run-time behavior depends upon the values of the <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> and <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> properties, which control how many messages can execute inside an operation at once and the lifetimes of the service <xref:System.ServiceModel.InstanceContext> relative to incoming channel sessions, respectively.</span></span>  
  
 <span data-ttu-id="99c4e-111">如需詳細資訊，請參閱 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 和 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>。</span><span class="sxs-lookup"><span data-stu-id="99c4e-111">For details, see <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>, and <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="99c4e-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="99c4e-112">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>

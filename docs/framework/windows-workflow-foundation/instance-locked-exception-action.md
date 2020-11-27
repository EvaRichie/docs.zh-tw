---
title: 執行個體鎖定的例外狀況動作
ms.date: 03/30/2017
ms.assetid: 164a5419-315c-4987-ad72-54cbdb88d402
ms.openlocfilehash: 3554975589bb6d55cef3611320d25687d1ee9ba6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279853"
---
# <a name="instance-locked-exception-action"></a>執行個體鎖定的例外狀況動作

SQL 工作流程執行個體存放區的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> 屬性可讓您指定當 SQL 持續性提供者收到 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 時應執行的動作。 當持續性提供者嘗試鎖定目前由其他服務主機鎖定的工作流程服務執行個體時，就會收到這個例外狀況。 此屬性的值為 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>、<xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry> 和 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>。 預設值為 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>。 下列清單描述這三種選項：  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>. 服務主機不會嘗試鎖定工作流程服務實例，並將傳遞 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 給呼叫端。  如果工作流程停留在記憶體中的期間超過60秒，請使用 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry> 做為重試。 預設值為 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.NoRetry>。  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry>. 服務主機在每次重試之間以線性間隔重新嘗試鎖定工作流程服務執行個體，並在序列結尾處將 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 傳遞給呼叫端。 如果工作流程停留在記憶體中 5-60 秒，並且郵件會分批到達，可能會將訊息傳送到同一個主機的同一個執行個體上，以便在卸載工作流程之前處理所有訊息，使用 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry> 在不浪費資源的情況下達到最佳延遲。  
  
- <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>. 服務主機在每次重試之間以後退演算法間隔重新嘗試鎖定工作流程服務執行個體，並在序列結尾處將例外狀況傳遞給呼叫端。 如果工作流程停留在記憶體中的時間非常短 (不到 5 秒)，或者 Web 伺服陣列非常大，且將另一個訊息傳送到同一個主機的機率不高，請使用<xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry> 達到最佳的延遲。  
  
 執行個體鎖定的例外狀況動作功能支援下列案例。 在所有案例中，如果 SqlWorkflowInstanceStore 的 instanceLockedExceptionAction 屬性設為 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.BasicRetry> 或 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction.AggressiveRetry>，主機會公開地定期重試取得鎖定執行個體。  
  
1. **啟用正常關機與應用程式定義域重疊回收：** 假設具有正在執行工作流程服務實例之服務主機的 **appdomain** 正在回收，而新的 **appdomain** 將會以平行方式處理新的要求，而舊的 **appdomain** 會正常關閉。 關機作業會等到工作流程服務執行個體閒置時才進行，然後才保存及卸載執行個體。 當新 **AppDomain** 中的主機嘗試鎖定實例時，會造成 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 。  
  
2. **水準調整跨同質伺服器陣列的持久工作流程。** 假設正在執行工作流程執行個體的伺服器陣列節點當機，且該工作流程主機無法移除其所執行之執行個體的鎖定。 在伺服器陣列其他節點上執行的服務主機收到給該工作流程的訊息時，該服務主機就會嘗試取得鎖定這些會收到 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 的執行個體。 鎖定會在一段時間後逾期，因為應更新鎖定的主機已不存在。  
  
     **水準調整跨同質伺服器陣列的持久工作流程。**  假設您要使用 NLB (網路負載平衡器) 之後的多部主機水平縮放長期工作流程，在其中一個陣列節點上執行的工作流程主機會載入工作流程執行個體並處理訊息，傳送至該執行個體的下一個訊息會路由至執行在其他節點上執行的主機，因為 NLB 沒有可將訊息傳遞至已執行該執行個體之主機的路由演算法。 第二部主機收到訊息時，會嘗試載入工作流程執行個體並接收 <xref:System.Runtime.DurableInstancing.InstanceLockedException>，因為第一部主機已在該執行個體上鎖定。 第一部主機會在完成處理第一個訊息時解除鎖定該執行個體，而第二部主機會在下次重試時取得鎖定、載入執行個體，並且處理第二個訊息。

---
title: WF 中的控制流程活動
description: 本文摘要說明在工作流程內控制執行流程的 .NET Framework 4.6.1 活動。
ms.date: 03/30/2017
ms.assetid: 6892885b-f7c5-4aea-8f5e-28863fb4ae75
ms.openlocfilehash: 18ff982d3f215e3fd46108eb2411f3d1a5ab9745
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420067"
---
# <a name="control-flow-activities-in-wf"></a>WF 中的控制流程活動
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 提供數種活動，可用於控制工作流程內的執行流程。 其中一些活動（例如 `Switch` 和）會 `If` 執行與 Visual c # 等程式設計環境中類似的流程式控制制結構，而其他專案（例如 `Pick` ）則是模型新的程式設計結構。  
  
 請注意，雖然 `Parallel` 和 `ParallelForEach` 之類的活動會排定多個同時執行的子活動，但只會使用單一執行緒來進行工作流程。 這些活動的每個子活動會循序執行，在先前的活動完成或閒置之前，後續的活動均不會執行。 因此，最適合使用這些活動的應用程式即為必須交錯執行數個可能封鎖之活動的應用程式。 如果這些活動中沒有任何子活動閒置，`Parallel` 活動會像 `Sequence` 活動般執行，而 `ParallelForEach` 活動會像 `ForEach` 活動般執行。 然而，如果使用非同步活動 (例如衍生自 <xref:System.Activities.AsyncCodeActivity> 的活動) 或傳訊活動，控制項會轉移至下一個分支，而子活動會等候其訊息被接收，或其非同步工作完成。  
  
## <a name="flow-control-activities"></a>流量控制活動  
  
|活動|描述|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.DoWhile>|執行所包含的活動一次，並繼續執行直到條件為 `true` 為止。|  
|<xref:System.Activities.Statements.ForEach%601>|針對集合中的每個元素，循序執行內嵌陳述式。 <xref:System.Activities.Statements.ForEach%601> 與關鍵字 `foreach` 相似，但會當做活動而非語言陳述式來實作。|  
|<xref:System.Activities.Statements.If>|如果條件為 `true` 則執行所包含的活動，如果條件為 <xref:System.Activities.Statements.If.Else%2A>，則可執行包含在 `false` 屬性中的活動。|  
|<xref:System.Activities.Statements.Parallel>|平行執行所包含的活動。|  
|<xref:System.Activities.Statements.ParallelForEach%601>|針對集合中的每個項目，平行執行內嵌陳述式。|  
|<xref:System.Activities.Statements.Pick>|提供事件架構控制流程模型。|  
|<xref:System.Activities.Statements.PickBranch>|在 <xref:System.Activities.Statements.Pick> 活動中代表潛在的執行路徑。|  
|<xref:System.Activities.Statements.Sequence>|循序執行所包含的活動。|  
|<xref:System.Activities.Statements.Switch%601>|根據此指定運算式的值，從活動成員中選取要執行的一個選項。|  
|<xref:System.Activities.Statements.While>|當條件為 `true` 時執行所包含的活動。|

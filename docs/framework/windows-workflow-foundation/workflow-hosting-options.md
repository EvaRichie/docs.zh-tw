---
title: 工作流程裝載選項
ms.date: 03/30/2017
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
ms.openlocfilehash: 8ddb83f068eab8480bacc8b80bc5d44b7755fa59
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293776"
---
# <a name="workflow-hosting-options"></a>工作流程裝載選項

大部分的 Windows Workflow Foundation (WF) 範例都會使用裝載于主控台應用程式中的工作流程，但這不是實際工作流程的實際案例。 實際商務應用程式中的工作流程將裝載于持續性程式中，也就是開發人員所撰寫的 Windows 服務，或是 IIS 7.0 或 AppFabric 等伺服器應用程式。 這些方法之間差異如下。

## <a name="hosting-workflows-in-iis-with-windows-appfabric"></a>在具有 Windows AppFabric 的 IIS 中裝載工作流程

使用具有 AppFabric 的 IIS 是工作流程的慣用主機。 使用 AppFabric 的工作流程主應用程式是 Windows 啟用服務，它會單獨由 IIS 中移除對 HTTP 的相依性。

## <a name="hosting-workflows-in-iis-alone"></a>只在 IIS 中裝載工作流程

建議您單獨使用 IIS 7.0，因為 AppFabric 有提供管理和監視工具，可協助維護執行中的應用程式。 如果移至 AppFabric 的基礎結構有問題，工作流程應該只裝載在 IIS 7.0 中。

> [!WARNING]
> IIS 7.0 會基於各種原因定期回收應用程式集區。 回收應用程式集區時，IIS 會停止接受訊息至舊集區，並產生新的應用程式集區以接受新的要求。 如果工作流程在傳送回應之後仍繼續運作，IIS 7.0 將不會察覺完成的工作，而且可能會回收裝載應用程式集區。 如果發生這種情況，工作流程將會中止，而且追蹤服務會使用空白的原因欄位來記錄 [1004 WorkflowInstanceAborted](1004-workflowinstanceaborted.md) 的訊息。
>
> 如果使用持續性，主機必須從上次的保存點，明確地將中止的執行個體重新啟動。
>
> 如果使用 AppFabric，工作流程管理服務最後會從上次的成功保存點 (如果使用持續性) 繼續工作流程。 如果沒有使用持續性，而且工作流程不是以「要求/回應」模式執行作業，資料將會在工作流程中止時遺失。

## <a name="hosting-a-workflow-in-a-custom-windows-service"></a>在自訂 Windows 服務中裝載工作流程

建立自訂工作流程服務來裝載工作流程，需要開發人員重複許多由 AppFabric 提供的全新功能，不過在自訂功能方面較有彈性。 唯有確定 AppFabric 不是選項時，才能考慮此選項。

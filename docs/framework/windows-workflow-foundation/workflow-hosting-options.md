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
# <a name="workflow-hosting-options"></a><span data-ttu-id="538dd-102">工作流程裝載選項</span><span class="sxs-lookup"><span data-stu-id="538dd-102">Workflow Hosting Options</span></span>

<span data-ttu-id="538dd-103">大部分的 Windows Workflow Foundation (WF) 範例都會使用裝載于主控台應用程式中的工作流程，但這不是實際工作流程的實際案例。</span><span class="sxs-lookup"><span data-stu-id="538dd-103">Most of the Windows Workflow Foundation (WF) samples use workflows that are hosted in a console application, but this isn't a realistic scenario for real-world workflows.</span></span> <span data-ttu-id="538dd-104">實際商務應用程式中的工作流程將裝載于持續性程式中，也就是開發人員所撰寫的 Windows 服務，或是 IIS 7.0 或 AppFabric 等伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="538dd-104">Workflows in actual business applications will be hosted in persistent processes- either a Windows service authored by the developer, or a server application such as IIS 7.0 or AppFabric.</span></span> <span data-ttu-id="538dd-105">這些方法之間差異如下。</span><span class="sxs-lookup"><span data-stu-id="538dd-105">The differences between these approaches are as follows.</span></span>

## <a name="hosting-workflows-in-iis-with-windows-appfabric"></a><span data-ttu-id="538dd-106">在具有 Windows AppFabric 的 IIS 中裝載工作流程</span><span class="sxs-lookup"><span data-stu-id="538dd-106">Hosting workflows in IIS with Windows AppFabric</span></span>

<span data-ttu-id="538dd-107">使用具有 AppFabric 的 IIS 是工作流程的慣用主機。</span><span class="sxs-lookup"><span data-stu-id="538dd-107">Using IIS with AppFabric is the preferred host for workflows.</span></span> <span data-ttu-id="538dd-108">使用 AppFabric 的工作流程主應用程式是 Windows 啟用服務，它會單獨由 IIS 中移除對 HTTP 的相依性。</span><span class="sxs-lookup"><span data-stu-id="538dd-108">The host application for workflows using AppFabric is Windows Activation Service, which removes the dependency on HTTP over IIS alone.</span></span>

## <a name="hosting-workflows-in-iis-alone"></a><span data-ttu-id="538dd-109">只在 IIS 中裝載工作流程</span><span class="sxs-lookup"><span data-stu-id="538dd-109">Hosting workflows in IIS alone</span></span>

<span data-ttu-id="538dd-110">建議您單獨使用 IIS 7.0，因為 AppFabric 有提供管理和監視工具，可協助維護執行中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="538dd-110">Using IIS 7.0 alone is not recommended, as there are management and monitoring tools available with AppFabric that facilitate maintenance of running applications.</span></span> <span data-ttu-id="538dd-111">如果移至 AppFabric 的基礎結構有問題，工作流程應該只裝載在 IIS 7.0 中。</span><span class="sxs-lookup"><span data-stu-id="538dd-111">Workflows should only be hosted in IIS 7.0 alone if there are infrastructure concerns with moving to AppFabric.</span></span>

> [!WARNING]
> <span data-ttu-id="538dd-112">IIS 7.0 會基於各種原因定期回收應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="538dd-112">IIS 7.0 recycles application pools periodically for various reasons.</span></span> <span data-ttu-id="538dd-113">回收應用程式集區時，IIS 會停止接受訊息至舊集區，並產生新的應用程式集區以接受新的要求。</span><span class="sxs-lookup"><span data-stu-id="538dd-113">When an application pool is recycled, IIS stops accepting messages to the old pool, and instantiates a new application pool to accept new requests.</span></span> <span data-ttu-id="538dd-114">如果工作流程在傳送回應之後仍繼續運作，IIS 7.0 將不會察覺完成的工作，而且可能會回收裝載應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="538dd-114">If a workflow continues working after sending a response, IIS 7.0 will not be aware of the work being done, and may recycle the hosting application pool.</span></span> <span data-ttu-id="538dd-115">如果發生這種情況，工作流程將會中止，而且追蹤服務會使用空白的原因欄位來記錄 [1004 WorkflowInstanceAborted](1004-workflowinstanceaborted.md) 的訊息。</span><span class="sxs-lookup"><span data-stu-id="538dd-115">If this happens, the workflow will abort, and tracking services will record a [1004 - WorkflowInstanceAborted](1004-workflowinstanceaborted.md) message with an empty Reason field.</span></span>
>
> <span data-ttu-id="538dd-116">如果使用持續性，主機必須從上次的保存點，明確地將中止的執行個體重新啟動。</span><span class="sxs-lookup"><span data-stu-id="538dd-116">If persistence is used, the host must explicitly restart aborted instances from the last persistence point.</span></span>
>
> <span data-ttu-id="538dd-117">如果使用 AppFabric，工作流程管理服務最後會從上次的成功保存點 (如果使用持續性) 繼續工作流程。</span><span class="sxs-lookup"><span data-stu-id="538dd-117">If AppFabric is used, the workflow management service will eventually resume the workflow from the last successful persistence point if persistence is used.</span></span> <span data-ttu-id="538dd-118">如果沒有使用持續性，而且工作流程不是以「要求/回應」模式執行作業，資料將會在工作流程中止時遺失。</span><span class="sxs-lookup"><span data-stu-id="538dd-118">If no persistence is used, and the workflow performs operations outside a Request/Response pattern, data will be lost when the workflow aborts.</span></span>

## <a name="hosting-a-workflow-in-a-custom-windows-service"></a><span data-ttu-id="538dd-119">在自訂 Windows 服務中裝載工作流程</span><span class="sxs-lookup"><span data-stu-id="538dd-119">Hosting a workflow in a custom Windows Service</span></span>

<span data-ttu-id="538dd-120">建立自訂工作流程服務來裝載工作流程，需要開發人員重複許多由 AppFabric 提供的全新功能，不過在自訂功能方面較有彈性。</span><span class="sxs-lookup"><span data-stu-id="538dd-120">Creating a custom workflow service to host the workflow will require the developer to duplicate a lot of the functionality provided out-of-box by AppFabric, but will allow for more flexibility with custom functionality.</span></span> <span data-ttu-id="538dd-121">唯有確定 AppFabric 不是選項時，才能考慮此選項。</span><span class="sxs-lookup"><span data-stu-id="538dd-121">This option should only be considered if AppFabric proves to not be an option.</span></span>

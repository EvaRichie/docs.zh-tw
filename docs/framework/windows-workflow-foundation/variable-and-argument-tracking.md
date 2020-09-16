---
title: 變數及引數追蹤
ms.date: 03/30/2017
ms.assetid: 8f3d9d30-d899-49aa-b7ce-a8d0d32c4ff0
ms.openlocfilehash: af5c21b75f3238546acac0755ec4e6149ee50d95
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90552488"
---
# <a name="variable-and-argument-tracking"></a><span data-ttu-id="f451a-102">變數及引數追蹤</span><span class="sxs-lookup"><span data-stu-id="f451a-102">Variable and Argument Tracking</span></span>
<span data-ttu-id="f451a-103">追蹤工作流程的執行時，擷取資料通常很實用。</span><span class="sxs-lookup"><span data-stu-id="f451a-103">When tracking the execution of a workflow, it is often useful to extract data.</span></span> <span data-ttu-id="f451a-104">它可在存取追蹤記錄後期執行時，提供額外的內容。</span><span class="sxs-lookup"><span data-stu-id="f451a-104">This provides additional context when accessing a tracking record post execution.</span></span> <span data-ttu-id="f451a-105">在 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中，您可以在使用追蹤的工作流程中的任何活動範圍內擷取任何可見的變數或引數。</span><span class="sxs-lookup"><span data-stu-id="f451a-105">In [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], you can extract any visible variable or argument within the scope of any activity in a workflow using tracking.</span></span> <span data-ttu-id="f451a-106">追蹤設定檔讓擷取資料變得非常容易。</span><span class="sxs-lookup"><span data-stu-id="f451a-106">Tracking profiles make it easy to extract data.</span></span>  
  
## <a name="variables-and-arguments"></a><span data-ttu-id="f451a-107">變數與引數</span><span class="sxs-lookup"><span data-stu-id="f451a-107">Variables and Arguments</span></span>  
 <span data-ttu-id="f451a-108">變數和引數的擷取會在活動發出 ActivityStateRecord 時進行。</span><span class="sxs-lookup"><span data-stu-id="f451a-108">Variables and arguments are extracted when an activity emits an ActivityStateRecord.</span></span>  <span data-ttu-id="f451a-109">如果變數在活動的範圍內，則僅供擷取使用。</span><span class="sxs-lookup"><span data-stu-id="f451a-109">A variable is available for extraction only if it is within the scope of the activity.</span></span> <span data-ttu-id="f451a-110">要在活動內擷取的變數會以下列方式指定：</span><span class="sxs-lookup"><span data-stu-id="f451a-110">A variable to be extracted within an activity is specified in the following manner:</span></span>  
  
- <span data-ttu-id="f451a-111">如果以變數名稱指定變數，則追蹤會在目前所追蹤的活動及父活動內尋找該變數。</span><span class="sxs-lookup"><span data-stu-id="f451a-111">If a variable is specified by the variable name, then tracking looks for the variable within the current activity being tracked and in parent activities.</span></span> <span data-ttu-id="f451a-112">追蹤會在目前活動範圍及父範圍中搜尋變數。</span><span class="sxs-lookup"><span data-stu-id="f451a-112">The variable is searched in current activity scope and in parent scope.</span></span>  
  
- <span data-ttu-id="f451a-113">如果要解壓縮的變數是使用 name = "" 來指定 \* ，則會解壓縮目前正在追蹤之活動內的所有變數。</span><span class="sxs-lookup"><span data-stu-id="f451a-113">If variables to be extracted are specified by using name="\*", then all variables within the current activity being tracked are extracted.</span></span> <span data-ttu-id="f451a-114">在此情況下，則不會擷取在範圍內但未在父活動中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="f451a-114">In this case variables that are in scope but defined in parent activities are not extracted.</span></span>  
  
 <span data-ttu-id="f451a-115">擷取引數時，會根據活動的狀態擷取引數。</span><span class="sxs-lookup"><span data-stu-id="f451a-115">When extracting arguments, the arguments extracted depend on the state of the activity.</span></span> <span data-ttu-id="f451a-116">當活動的狀態是 Executing 時，則只有 `InArguments` 可供擷取。</span><span class="sxs-lookup"><span data-stu-id="f451a-116">When the state of an activity is Executing, then only the `InArguments` are available for extraction.</span></span> <span data-ttu-id="f451a-117">若為其他任何活動狀態 (Closed、Faulted、Canceled)，則 InArgument 和 OutArgument 皆可供擷取。</span><span class="sxs-lookup"><span data-stu-id="f451a-117">For any other activity state (Closed, Faulted, Canceled), all arguments, both InArguments and OutArguments, are available for extraction.</span></span>  
  
 <span data-ttu-id="f451a-118">下列範例示範活動狀態查詢，此查詢會在發出活動的 `Closed` 追蹤記錄時擷取變數及引數。</span><span class="sxs-lookup"><span data-stu-id="f451a-118">The following example shows an activity state query that extracts variables and arguments when the activity’s `Closed` tracking record is emitted.</span></span> <span data-ttu-id="f451a-119">變數和引數只能使用 <xref:System.Activities.Tracking.ActivityStateRecord> 擷取，因此可在追蹤設定檔中使用 <xref:System.Activities.Tracking.ActivityStateQuery> 訂閱。</span><span class="sxs-lookup"><span data-stu-id="f451a-119">Variables and arguments can be extracted only with an <xref:System.Activities.Tracking.ActivityStateRecord> and thus are subscribed to within a tracking profile using <xref:System.Activities.Tracking.ActivityStateQuery>.</span></span>  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
```  
  
## <a name="protecting-information-stored-within-variables-and-arguments"></a><span data-ttu-id="f451a-120">保護變數和引數中所儲存的資訊</span><span class="sxs-lookup"><span data-stu-id="f451a-120">Protecting Information Stored Within Variables and Arguments</span></span>  
 <span data-ttu-id="f451a-121">WF 執行階段預設會顯示所追蹤的變數或引數。</span><span class="sxs-lookup"><span data-stu-id="f451a-121">A tracked variable or argument is by default made visible by the WF runtime.</span></span> <span data-ttu-id="f451a-122">工作流程開發人員可以採取以下步驟，保護變數或引數不受存取：</span><span class="sxs-lookup"><span data-stu-id="f451a-122">A workflow developer can protect it from being accessed by taking the following steps:</span></span>  
  
1. <span data-ttu-id="f451a-123">加密變數的值。</span><span class="sxs-lookup"><span data-stu-id="f451a-123">Encrypt the value of a variable.</span></span>  
  
2. <span data-ttu-id="f451a-124">控制追蹤設定檔的撰寫，以防止擷取變數或引數。</span><span class="sxs-lookup"><span data-stu-id="f451a-124">Control the authoring of a tracking profile to prevent the extraction of a variable or argument.</span></span>  
  
3. <span data-ttu-id="f451a-125">若為自訂追蹤參與者，請確定 WF 程式碼不會公開儲存在變數或引數中的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="f451a-125">For custom tracking participants ensure that the WF code does not disclose sensitive information that is stored in variables or arguments.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f451a-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f451a-126">See also</span></span>

- <span data-ttu-id="f451a-127">[Windows Server App Fabric 監視](/previous-versions/appfabric/ee677251(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="f451a-127">[Windows Server App Fabric Monitoring](/previous-versions/appfabric/ee677251(v=azure.10))</span></span>
- <span data-ttu-id="f451a-128">[使用 App Fabric 監視應用程式](/previous-versions/appfabric/ee677276(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="f451a-128">[Monitoring Applications with App Fabric](/previous-versions/appfabric/ee677276(v=azure.10))</span></span>

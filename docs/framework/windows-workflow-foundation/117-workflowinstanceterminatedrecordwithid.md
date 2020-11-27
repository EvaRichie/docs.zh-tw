---
title: 117 - WorkflowInstanceTerminatedRecordWithId
ms.date: 03/30/2017
ms.assetid: e68539d0-5338-468a-9f75-7e5b09d39a3c
ms.openlocfilehash: 5e16eff8e8ce9815cac604be110e899a29b4af3d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96281725"
---
# <a name="117---workflowinstanceterminatedrecordwithid"></a><span data-ttu-id="e6396-102">117 - WorkflowInstanceTerminatedRecordWithId</span><span class="sxs-lookup"><span data-stu-id="e6396-102">117 - WorkflowInstanceTerminatedRecordWithId</span></span>

## <a name="properties"></a><span data-ttu-id="e6396-103">屬性</span><span class="sxs-lookup"><span data-stu-id="e6396-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="e6396-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="e6396-104">ID</span></span>|<span data-ttu-id="e6396-105">117</span><span class="sxs-lookup"><span data-stu-id="e6396-105">117</span></span>|  
|<span data-ttu-id="e6396-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="e6396-106">Keywords</span></span>|<span data-ttu-id="e6396-107">HealthMonitoring、WFTracking</span><span class="sxs-lookup"><span data-stu-id="e6396-107">HealthMonitoring, WFTracking</span></span>|  
|<span data-ttu-id="e6396-108">層級</span><span class="sxs-lookup"><span data-stu-id="e6396-108">Level</span></span>|<span data-ttu-id="e6396-109">錯誤</span><span class="sxs-lookup"><span data-stu-id="e6396-109">Error</span></span>|  
|<span data-ttu-id="e6396-110">通路</span><span class="sxs-lookup"><span data-stu-id="e6396-110">Channel</span></span>|<span data-ttu-id="e6396-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="e6396-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="e6396-112">描述</span><span class="sxs-lookup"><span data-stu-id="e6396-112">Description</span></span>  

 <span data-ttu-id="e6396-113">此事件是當工作流程執行個體發出 WorkflowInstanceTerminatedRecord 時，由 ETW 追蹤參與者發出。</span><span class="sxs-lookup"><span data-stu-id="e6396-113">This event is emitted by the ETW tracking participant when a workflow instance emits WorkflowInstanceTerminatedRecord.</span></span>  
  
## <a name="message"></a><span data-ttu-id="e6396-114">訊息</span><span class="sxs-lookup"><span data-stu-id="e6396-114">Message</span></span>  

 <span data-ttu-id="e6396-115">TrackRecord = WorkflowInstanceTerminatedRecord、InstanceID = %1、RecordNumber = %2、EventTime = %3、ActivityDefinitionId = %4、Reason = %5、Annotations = %6、ProfileName = %7、WorkflowDefinitionIdentity = %8</span><span class="sxs-lookup"><span data-stu-id="e6396-115">TrackRecord = WorkflowInstanceTerminatedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, Reason = %5,  Annotations = %6, ProfileName = %7, WorkflowDefinitionIdentity = %8</span></span>  
  
## <a name="details"></a><span data-ttu-id="e6396-116">詳細資料</span><span class="sxs-lookup"><span data-stu-id="e6396-116">Details</span></span>  
  
|<span data-ttu-id="e6396-117">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="e6396-117">Data Item Name</span></span>|<span data-ttu-id="e6396-118">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="e6396-118">Data Item Type</span></span>|<span data-ttu-id="e6396-119">描述</span><span class="sxs-lookup"><span data-stu-id="e6396-119">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="e6396-120">InstanceId</span><span class="sxs-lookup"><span data-stu-id="e6396-120">InstanceId</span></span>|<span data-ttu-id="e6396-121">xs:GUID</span><span class="sxs-lookup"><span data-stu-id="e6396-121">xs:GUID</span></span>|<span data-ttu-id="e6396-122">工作流程的執行個體 ID。</span><span class="sxs-lookup"><span data-stu-id="e6396-122">The instance id for the workflow</span></span>|  
|<span data-ttu-id="e6396-123">RecordNumber</span><span class="sxs-lookup"><span data-stu-id="e6396-123">RecordNumber</span></span>|<span data-ttu-id="e6396-124">xs:long</span><span class="sxs-lookup"><span data-stu-id="e6396-124">xs:long</span></span>|<span data-ttu-id="e6396-125">發出之記錄的序號。</span><span class="sxs-lookup"><span data-stu-id="e6396-125">The sequence number of the emitted record</span></span>|  
|<span data-ttu-id="e6396-126">EventTime</span><span class="sxs-lookup"><span data-stu-id="e6396-126">EventTime</span></span>|<span data-ttu-id="e6396-127">xs:dateTime</span><span class="sxs-lookup"><span data-stu-id="e6396-127">xs:dateTime</span></span>|<span data-ttu-id="e6396-128">發出事件時的 UTC 時間。</span><span class="sxs-lookup"><span data-stu-id="e6396-128">The time in UTC when the event was emitted</span></span>|  
|<span data-ttu-id="e6396-129">ActivityDefinitionId</span><span class="sxs-lookup"><span data-stu-id="e6396-129">ActivityDefinitionId</span></span>|<span data-ttu-id="e6396-130">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-130">xs:string</span></span>|<span data-ttu-id="e6396-131">工作流程中根活動的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6396-131">The name of the root activity in the workflow</span></span>|  
|<span data-ttu-id="e6396-132">州</span><span class="sxs-lookup"><span data-stu-id="e6396-132">State</span></span>|<span data-ttu-id="e6396-133">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-133">xs:string</span></span>|<span data-ttu-id="e6396-134">工作流程的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="e6396-134">The current state of the Workflow.</span></span>|  
|<span data-ttu-id="e6396-135">註解</span><span class="sxs-lookup"><span data-stu-id="e6396-135">Annotations</span></span>|<span data-ttu-id="e6396-136">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-136">xs:string</span></span>|<span data-ttu-id="e6396-137">加入至此事件中的附註。</span><span class="sxs-lookup"><span data-stu-id="e6396-137">The annotations that were added to this event.</span></span> <span data-ttu-id="e6396-138">這些值會以 a 格式儲存在 xml 元素中 \<items> \< item name = "annotationName" type="System.String"> \</item> \</items> 。</span><span class="sxs-lookup"><span data-stu-id="e6396-138">The values are stored in an xml element in the format \<items>\< item name = "annotationName" type="System.String">annotationValue\</item>\</items>.</span></span> <span data-ttu-id="e6396-139">如果未指定任何批註，則字串會包含 \<items/> 。</span><span class="sxs-lookup"><span data-stu-id="e6396-139">If no annotations are specified then the string contains \<items/>.</span></span> <span data-ttu-id="e6396-140">ETW 事件大小會受到 ETW 緩衝區大小或 ETW 事件的最大承載所限制。</span><span class="sxs-lookup"><span data-stu-id="e6396-140">The ETW event size is limited by the ETW buffer size or the max payload for an ETW event.</span></span> <span data-ttu-id="e6396-141">如果事件大小超過 ETW 限制，則會捨棄注釋並以 ... 取代注釋值來截斷事件。 \<items> \</items></span><span class="sxs-lookup"><span data-stu-id="e6396-141">If the size of the event exceeds the ETW limits, then the event is truncated by dropping the annotations and replacing the annotation value with \<items>...\</items>.</span></span>|  
|<span data-ttu-id="e6396-142">ProfileName</span><span class="sxs-lookup"><span data-stu-id="e6396-142">ProfileName</span></span>|<span data-ttu-id="e6396-143">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-143">xs:string</span></span>|<span data-ttu-id="e6396-144">造成發送這個事件的名稱或追蹤設定檔。</span><span class="sxs-lookup"><span data-stu-id="e6396-144">The name or the tracking profile that resulted in this event being emitted</span></span>|  
|<span data-ttu-id="e6396-145">WorkflowDefinitionIdentity</span><span class="sxs-lookup"><span data-stu-id="e6396-145">WorkflowDefinitionIdentity</span></span>|<span data-ttu-id="e6396-146">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-146">xs:string</span></span>|<span data-ttu-id="e6396-147">工作流程定義 ID</span><span class="sxs-lookup"><span data-stu-id="e6396-147">The workflow definition id</span></span>|  
|<span data-ttu-id="e6396-148">AppDomain</span><span class="sxs-lookup"><span data-stu-id="e6396-148">AppDomain</span></span>|<span data-ttu-id="e6396-149">xs:string</span><span class="sxs-lookup"><span data-stu-id="e6396-149">xs:string</span></span>|<span data-ttu-id="e6396-150">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="e6396-150">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

---
title: 1009 - ActivityScheduled
ms.date: 03/30/2017
ms.assetid: 307e38b6-d47e-47a4-9708-e74d8314b1a1
ms.openlocfilehash: 812531d4206dfee20f183b9461330e71263b0bf8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239766"
---
# <a name="1009---activityscheduled"></a><span data-ttu-id="a3037-102">1009 - ActivityScheduled</span><span class="sxs-lookup"><span data-stu-id="a3037-102">1009 - ActivityScheduled</span></span>

## <a name="properties"></a><span data-ttu-id="a3037-103">屬性</span><span class="sxs-lookup"><span data-stu-id="a3037-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="a3037-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="a3037-104">ID</span></span>|<span data-ttu-id="a3037-105">1009</span><span class="sxs-lookup"><span data-stu-id="a3037-105">1009</span></span>|  
|<span data-ttu-id="a3037-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="a3037-106">Keywords</span></span>|<span data-ttu-id="a3037-107">WFRuntime</span><span class="sxs-lookup"><span data-stu-id="a3037-107">WFRuntime</span></span>|  
|<span data-ttu-id="a3037-108">層級</span><span class="sxs-lookup"><span data-stu-id="a3037-108">Level</span></span>|<span data-ttu-id="a3037-109">資訊</span><span class="sxs-lookup"><span data-stu-id="a3037-109">Information</span></span>|  
|<span data-ttu-id="a3037-110">通路</span><span class="sxs-lookup"><span data-stu-id="a3037-110">Channel</span></span>|<span data-ttu-id="a3037-111">Microsoft-Windows-Application Server-Applications/Debug</span><span class="sxs-lookup"><span data-stu-id="a3037-111">Microsoft-Windows-Application Server-Applications/Debug</span></span>|  
  
## <a name="description"></a><span data-ttu-id="a3037-112">描述</span><span class="sxs-lookup"><span data-stu-id="a3037-112">Description</span></span>  

 <span data-ttu-id="a3037-113">表示活動正在排定執行。</span><span class="sxs-lookup"><span data-stu-id="a3037-113">Indicates an activity is being scheduled for execution.</span></span>  
  
## <a name="message"></a><span data-ttu-id="a3037-114">訊息</span><span class="sxs-lookup"><span data-stu-id="a3037-114">Message</span></span>  

 <span data-ttu-id="a3037-115">父活動 '%1'、DisplayName：'%2'、InstanceId：'%3' 已排程子活動 '%4'、DisplayName：'%5'、InstanceId：'%6'。</span><span class="sxs-lookup"><span data-stu-id="a3037-115">Parent Activity '%1', DisplayName: '%2', InstanceId: '%3' scheduled child Activity '%4', DisplayName: '%5', InstanceId: '%6'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="a3037-116">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a3037-116">Details</span></span>  
  
|<span data-ttu-id="a3037-117">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="a3037-117">Data Item Name</span></span>|<span data-ttu-id="a3037-118">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="a3037-118">Data Item Type</span></span>|<span data-ttu-id="a3037-119">描述</span><span class="sxs-lookup"><span data-stu-id="a3037-119">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="a3037-120">ParentActivity</span><span class="sxs-lookup"><span data-stu-id="a3037-120">ParentActivity</span></span>|<span data-ttu-id="a3037-121">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-121">xs:string</span></span>|<span data-ttu-id="a3037-122">父活動的型別名稱。</span><span class="sxs-lookup"><span data-stu-id="a3037-122">The type name of the parent activity.</span></span>|  
|<span data-ttu-id="a3037-123">ParentDisplayName</span><span class="sxs-lookup"><span data-stu-id="a3037-123">ParentDisplayName</span></span>|<span data-ttu-id="a3037-124">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-124">xs:string</span></span>|<span data-ttu-id="a3037-125">父活動的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a3037-125">The display name of the parent activity.</span></span>|  
|<span data-ttu-id="a3037-126">ParentInstanceId</span><span class="sxs-lookup"><span data-stu-id="a3037-126">ParentInstanceId</span></span>|<span data-ttu-id="a3037-127">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-127">xs:string</span></span>|<span data-ttu-id="a3037-128">父活動的執行個體 ID。</span><span class="sxs-lookup"><span data-stu-id="a3037-128">The instance id of the parent activity.</span></span>|  
|<span data-ttu-id="a3037-129">ChildActivity</span><span class="sxs-lookup"><span data-stu-id="a3037-129">ChildActivity</span></span>|<span data-ttu-id="a3037-130">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-130">xs:string</span></span>|<span data-ttu-id="a3037-131">已排程之子活動的型別名稱。</span><span class="sxs-lookup"><span data-stu-id="a3037-131">The type name of the scheduled child activity.</span></span>|  
|<span data-ttu-id="a3037-132">ChildDisplayName</span><span class="sxs-lookup"><span data-stu-id="a3037-132">ChildDisplayName</span></span>|<span data-ttu-id="a3037-133">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-133">xs:string</span></span>|<span data-ttu-id="a3037-134">已排程之子活動的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a3037-134">The display name of the scheduled child activity.</span></span>|  
|<span data-ttu-id="a3037-135">ChildInstanceId</span><span class="sxs-lookup"><span data-stu-id="a3037-135">ChildInstanceId</span></span>|<span data-ttu-id="a3037-136">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-136">xs:string</span></span>|<span data-ttu-id="a3037-137">已排程之子活動的執行個體 ID。</span><span class="sxs-lookup"><span data-stu-id="a3037-137">The instance id of the scheduled child activity.</span></span>|  
|<span data-ttu-id="a3037-138">AppDomain</span><span class="sxs-lookup"><span data-stu-id="a3037-138">AppDomain</span></span>|<span data-ttu-id="a3037-139">xs:string</span><span class="sxs-lookup"><span data-stu-id="a3037-139">xs:string</span></span>|<span data-ttu-id="a3037-140">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="a3037-140">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

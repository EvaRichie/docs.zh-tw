---
title: 1035 - RuntimeTransactionSet
ms.date: 03/30/2017
ms.assetid: 03b37de9-778c-4beb-b0e3-de73ece6088e
ms.openlocfilehash: b8bf8431c4e2b82c6aac95820eb45de2a404e976
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294270"
---
# <a name="1035---runtimetransactionset"></a><span data-ttu-id="1255e-102">1035 - RuntimeTransactionSet</span><span class="sxs-lookup"><span data-stu-id="1255e-102">1035 - RuntimeTransactionSet</span></span>

## <a name="properties"></a><span data-ttu-id="1255e-103">屬性</span><span class="sxs-lookup"><span data-stu-id="1255e-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="1255e-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="1255e-104">ID</span></span>|<span data-ttu-id="1255e-105">1035</span><span class="sxs-lookup"><span data-stu-id="1255e-105">1035</span></span>|  
|<span data-ttu-id="1255e-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="1255e-106">Keywords</span></span>|<span data-ttu-id="1255e-107">WFRuntime</span><span class="sxs-lookup"><span data-stu-id="1255e-107">WFRuntime</span></span>|  
|<span data-ttu-id="1255e-108">層級</span><span class="sxs-lookup"><span data-stu-id="1255e-108">Level</span></span>|<span data-ttu-id="1255e-109">「詳細資訊」</span><span class="sxs-lookup"><span data-stu-id="1255e-109">Verbose</span></span>|  
|<span data-ttu-id="1255e-110">通路</span><span class="sxs-lookup"><span data-stu-id="1255e-110">Channel</span></span>|<span data-ttu-id="1255e-111">Microsoft-Windows-Application Server-Applications/Debug</span><span class="sxs-lookup"><span data-stu-id="1255e-111">Microsoft-Windows-Application Server-Applications/Debug</span></span>|  
  
## <a name="description"></a><span data-ttu-id="1255e-112">描述</span><span class="sxs-lookup"><span data-stu-id="1255e-112">Description</span></span>  

 <span data-ttu-id="1255e-113">表示活動已設定執行階段異動。</span><span class="sxs-lookup"><span data-stu-id="1255e-113">Indicates an activity has set the runtime transaction.</span></span>  
  
## <a name="message"></a><span data-ttu-id="1255e-114">訊息</span><span class="sxs-lookup"><span data-stu-id="1255e-114">Message</span></span>  

 <span data-ttu-id="1255e-115">活動 ' %1 '、DisplayName： ' %2 '、InstanceId： ' %3 ' 已設定執行時間交易。</span><span class="sxs-lookup"><span data-stu-id="1255e-115">The runtime transaction has been set by Activity '%1', DisplayName: '%2', InstanceId: '%3'.</span></span>  <span data-ttu-id="1255e-116">執行已隔離到活動 ' %4 '、DisplayName： ' %5 '、InstanceId： ' %6 '。</span><span class="sxs-lookup"><span data-stu-id="1255e-116">Execution isolated to Activity '%4', DisplayName: '%5', InstanceId: '%6'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="1255e-117">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1255e-117">Details</span></span>  
  
|<span data-ttu-id="1255e-118">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="1255e-118">Data Item Name</span></span>|<span data-ttu-id="1255e-119">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="1255e-119">Data Item Type</span></span>|<span data-ttu-id="1255e-120">描述</span><span class="sxs-lookup"><span data-stu-id="1255e-120">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="1255e-121">活動</span><span class="sxs-lookup"><span data-stu-id="1255e-121">Activity</span></span>|<span data-ttu-id="1255e-122">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-122">xs:string</span></span>|<span data-ttu-id="1255e-123">活動的型別名稱。</span><span class="sxs-lookup"><span data-stu-id="1255e-123">The type name of the activity.</span></span>|  
|<span data-ttu-id="1255e-124">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1255e-124">DisplayName</span></span>|<span data-ttu-id="1255e-125">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-125">xs:string</span></span>|<span data-ttu-id="1255e-126">活動的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1255e-126">The display name of the activity.</span></span>|  
|<span data-ttu-id="1255e-127">InstanceId</span><span class="sxs-lookup"><span data-stu-id="1255e-127">InstanceId</span></span>|<span data-ttu-id="1255e-128">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-128">xs:string</span></span>|<span data-ttu-id="1255e-129">活動的執行個體 ID。</span><span class="sxs-lookup"><span data-stu-id="1255e-129">The instance id of the activity.</span></span>|  
|<span data-ttu-id="1255e-130">IsolatedActivity</span><span class="sxs-lookup"><span data-stu-id="1255e-130">IsolatedActivity</span></span>|<span data-ttu-id="1255e-131">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-131">xs:string</span></span>|<span data-ttu-id="1255e-132">隔離交易之目標活動的型別名稱。</span><span class="sxs-lookup"><span data-stu-id="1255e-132">The type name of the activity that the transaction is isolated to.</span></span>|  
|<span data-ttu-id="1255e-133">IsolatedActivityDisplayName</span><span class="sxs-lookup"><span data-stu-id="1255e-133">IsolatedActivityDisplayName</span></span>|<span data-ttu-id="1255e-134">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-134">xs:string</span></span>|<span data-ttu-id="1255e-135">隔離異動之目標活動的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1255e-135">The display name of the activity that the transaction is isolated to.</span></span>|  
|<span data-ttu-id="1255e-136">IsolatedActivityInstanceId</span><span class="sxs-lookup"><span data-stu-id="1255e-136">IsolatedActivityInstanceId</span></span>|<span data-ttu-id="1255e-137">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-137">xs:string</span></span>|<span data-ttu-id="1255e-138">隔離異動之目標活動的執行個體 ID。</span><span class="sxs-lookup"><span data-stu-id="1255e-138">The instance id of the activity that the transaction is isolated to.</span></span>|  
|<span data-ttu-id="1255e-139">AppDomain</span><span class="sxs-lookup"><span data-stu-id="1255e-139">AppDomain</span></span>|<span data-ttu-id="1255e-140">xs:string</span><span class="sxs-lookup"><span data-stu-id="1255e-140">xs:string</span></span>|<span data-ttu-id="1255e-141">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="1255e-141">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

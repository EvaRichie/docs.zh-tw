---
title: 214 - OperationCompleted
ms.date: 03/30/2017
ms.assetid: a6287eef-023f-4816-813c-1802c82366df
ms.openlocfilehash: 6147c70448efb122cb43a2b42a1e9b59980fab29
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96278943"
---
# <a name="214---operationcompleted"></a><span data-ttu-id="03957-102">214 - OperationCompleted</span><span class="sxs-lookup"><span data-stu-id="03957-102">214 - OperationCompleted</span></span>

## <a name="properties"></a><span data-ttu-id="03957-103">屬性</span><span class="sxs-lookup"><span data-stu-id="03957-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="03957-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="03957-104">ID</span></span>|<span data-ttu-id="03957-105">214</span><span class="sxs-lookup"><span data-stu-id="03957-105">214</span></span>|  
|<span data-ttu-id="03957-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="03957-106">Keywords</span></span>|<span data-ttu-id="03957-107">HealthMonitoring，EndToEndMonitoring，Troubleshooting，ServiceModel</span><span class="sxs-lookup"><span data-stu-id="03957-107">HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel</span></span>|  
|<span data-ttu-id="03957-108">層級</span><span class="sxs-lookup"><span data-stu-id="03957-108">Level</span></span>|<span data-ttu-id="03957-109">資訊</span><span class="sxs-lookup"><span data-stu-id="03957-109">Information</span></span>|  
|<span data-ttu-id="03957-110">通路</span><span class="sxs-lookup"><span data-stu-id="03957-110">Channel</span></span>|<span data-ttu-id="03957-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="03957-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="03957-112">描述</span><span class="sxs-lookup"><span data-stu-id="03957-112">Description</span></span>  

 <span data-ttu-id="03957-113">此事件是在服務模型的預設 `OperationInvoker` 完成呼叫方法，且該方法未擲回例外狀況時發出。</span><span class="sxs-lookup"><span data-stu-id="03957-113">This event is emitted when the Service Model's default `OperationInvoker` has completed a call to a method without that method throwing an exception.</span></span>  
  
## <a name="message"></a><span data-ttu-id="03957-114">訊息</span><span class="sxs-lookup"><span data-stu-id="03957-114">Message</span></span>  

 <span data-ttu-id="03957-115">OperationInvoker 完成了對 '%1' 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="03957-115">An OperationInvoker completed the call to the '%1' method.</span></span> <span data-ttu-id="03957-116">此方法的呼叫持續時間為 '%2' 毫秒。</span><span class="sxs-lookup"><span data-stu-id="03957-116">The method call duration was '%2' ms.</span></span>  
  
## <a name="details"></a><span data-ttu-id="03957-117">詳細資料</span><span class="sxs-lookup"><span data-stu-id="03957-117">Details</span></span>  
  
|<span data-ttu-id="03957-118">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="03957-118">Data Item Name</span></span>|<span data-ttu-id="03957-119">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="03957-119">Data Item Type</span></span>|<span data-ttu-id="03957-120">描述</span><span class="sxs-lookup"><span data-stu-id="03957-120">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="03957-121">方法名稱</span><span class="sxs-lookup"><span data-stu-id="03957-121">Method Name</span></span>|`xs:string`|<span data-ttu-id="03957-122">`OperationInvoker` 叫用之方法的 CLR 名稱。</span><span class="sxs-lookup"><span data-stu-id="03957-122">The CLR name of the method that was invoked by the `OperationInvoker`.</span></span>|  
|<span data-ttu-id="03957-123">持續時間</span><span class="sxs-lookup"><span data-stu-id="03957-123">Duration</span></span>|`xs:long`|<span data-ttu-id="03957-124">`OperationInvoker` 叫用方法所花費的時間，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="03957-124">The time, in milliseconds, that it took the `OperationInvoker` to invoke the method.</span></span>|  
|<span data-ttu-id="03957-125">HostReference</span><span class="sxs-lookup"><span data-stu-id="03957-125">HostReference</span></span>|`xs:string`|<span data-ttu-id="03957-126">若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。</span><span class="sxs-lookup"><span data-stu-id="03957-126">For web-hosted services, this field uniquely identifies the service in the Web hierarchy.</span></span> <span data-ttu-id="03957-127">其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。</span><span class="sxs-lookup"><span data-stu-id="03957-127">Its format is defined as 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'.</span></span> <span data-ttu-id="03957-128">範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。</span><span class="sxs-lookup"><span data-stu-id="03957-128">Example: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.</span></span>|  
|<span data-ttu-id="03957-129">AppDomain</span><span class="sxs-lookup"><span data-stu-id="03957-129">AppDomain</span></span>|`xs:string`|<span data-ttu-id="03957-130">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="03957-130">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

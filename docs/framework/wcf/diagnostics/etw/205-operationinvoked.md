---
title: 205 - OperationInvoked
ms.date: 03/30/2017
ms.assetid: 9c8d6c90-dfa5-4ae0-a589-96679a8fb3ba
ms.openlocfilehash: c36294a4a430c3e372e8213246e85dba45ce03c8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286015"
---
# <a name="205---operationinvoked"></a><span data-ttu-id="21dc2-102">205 - OperationInvoked</span><span class="sxs-lookup"><span data-stu-id="21dc2-102">205 - OperationInvoked</span></span>

## <a name="properties"></a><span data-ttu-id="21dc2-103">屬性</span><span class="sxs-lookup"><span data-stu-id="21dc2-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="21dc2-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="21dc2-104">ID</span></span>|<span data-ttu-id="21dc2-105">205</span><span class="sxs-lookup"><span data-stu-id="21dc2-105">205</span></span>|  
|<span data-ttu-id="21dc2-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="21dc2-106">Keywords</span></span>|<span data-ttu-id="21dc2-107">Troubleshooting，ServiceModel</span><span class="sxs-lookup"><span data-stu-id="21dc2-107">Troubleshooting, ServiceModel</span></span>|  
|<span data-ttu-id="21dc2-108">層級</span><span class="sxs-lookup"><span data-stu-id="21dc2-108">Level</span></span>|<span data-ttu-id="21dc2-109">資訊</span><span class="sxs-lookup"><span data-stu-id="21dc2-109">Information</span></span>|  
|<span data-ttu-id="21dc2-110">通路</span><span class="sxs-lookup"><span data-stu-id="21dc2-110">Channel</span></span>|<span data-ttu-id="21dc2-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="21dc2-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="21dc2-112">描述</span><span class="sxs-lookup"><span data-stu-id="21dc2-112">Description</span></span>  

 <span data-ttu-id="21dc2-113">此事件會在服務模型的預設 `OperationInvoker` 開始呼叫方法之前發出。</span><span class="sxs-lookup"><span data-stu-id="21dc2-113">This event is emitted just before the Service Model's default `OperationInvoker` begins a call to a method.</span></span>  
  
## <a name="message"></a><span data-ttu-id="21dc2-114">訊息</span><span class="sxs-lookup"><span data-stu-id="21dc2-114">Message</span></span>  

 <span data-ttu-id="21dc2-115">OperationInvoker 已叫用 '%1' 方法。</span><span class="sxs-lookup"><span data-stu-id="21dc2-115">An OperationInvoker invoked the '%1' method.</span></span> <span data-ttu-id="21dc2-116">呼叫端資訊: '%2'。</span><span class="sxs-lookup"><span data-stu-id="21dc2-116">Caller information: '%2'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="21dc2-117">詳細資料</span><span class="sxs-lookup"><span data-stu-id="21dc2-117">Details</span></span>  
  
|<span data-ttu-id="21dc2-118">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="21dc2-118">Data Item Name</span></span>|<span data-ttu-id="21dc2-119">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="21dc2-119">Data Item Type</span></span>|<span data-ttu-id="21dc2-120">描述</span><span class="sxs-lookup"><span data-stu-id="21dc2-120">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="21dc2-121">方法名稱</span><span class="sxs-lookup"><span data-stu-id="21dc2-121">Method Name</span></span>|`xs:string`|<span data-ttu-id="21dc2-122">`OperationInvoker` 叫用之方法的 CLR 名稱。</span><span class="sxs-lookup"><span data-stu-id="21dc2-122">The CLR name of the method that was invoked by the `OperationInvoker`.</span></span>|  
|<span data-ttu-id="21dc2-123">呼叫端資訊</span><span class="sxs-lookup"><span data-stu-id="21dc2-123">Caller Information</span></span>|`xs:string`|<span data-ttu-id="21dc2-124">用戶端的 IP 位址和連接埠號碼，格式為 'IPAddress:PortNumber'。</span><span class="sxs-lookup"><span data-stu-id="21dc2-124">The IP address and port number of the client in the format 'IPAddress:PortNumber'.</span></span> <span data-ttu-id="21dc2-125">這兩個值都是從作業內容內的 'System.ServiceModel.Channels.RemoteEndpointMessageProperty' 訊息屬性擷取。</span><span class="sxs-lookup"><span data-stu-id="21dc2-125">The two values are retrieved from the 'System.ServiceModel.Channels.RemoteEndpointMessageProperty' message property within the operation context.</span></span> <span data-ttu-id="21dc2-126">請注意，針對非 TCP 繫結，此值為 `null`。</span><span class="sxs-lookup"><span data-stu-id="21dc2-126">Note that for non-TCP bindings this value `null`.</span></span>|  
|<span data-ttu-id="21dc2-127">HostReference</span><span class="sxs-lookup"><span data-stu-id="21dc2-127">HostReference</span></span>|`xs:string`|<span data-ttu-id="21dc2-128">若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。</span><span class="sxs-lookup"><span data-stu-id="21dc2-128">For Web-hosted services, this field uniquely identifies the service in the Web hierarchy.</span></span> <span data-ttu-id="21dc2-129">其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。</span><span class="sxs-lookup"><span data-stu-id="21dc2-129">Its format is defined as 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'.</span></span> <span data-ttu-id="21dc2-130">範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。</span><span class="sxs-lookup"><span data-stu-id="21dc2-130">Example: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.</span></span>|  
|<span data-ttu-id="21dc2-131">AppDomain</span><span class="sxs-lookup"><span data-stu-id="21dc2-131">AppDomain</span></span>|`xs:string`|<span data-ttu-id="21dc2-132">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="21dc2-132">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

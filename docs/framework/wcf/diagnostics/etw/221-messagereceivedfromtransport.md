---
title: 221 - MessageReceivedFromTransport
ms.date: 03/30/2017
ms.assetid: 4995f0d5-c182-4d97-981f-6951da6df1fb
ms.openlocfilehash: 47e871b70e3ef2419543b4710c2988736665cb46
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263096"
---
# <a name="221---messagereceivedfromtransport"></a><span data-ttu-id="a10fc-102">221 - MessageReceivedFromTransport</span><span class="sxs-lookup"><span data-stu-id="a10fc-102">221 - MessageReceivedFromTransport</span></span>

## <a name="properties"></a><span data-ttu-id="a10fc-103">屬性</span><span class="sxs-lookup"><span data-stu-id="a10fc-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="a10fc-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="a10fc-104">ID</span></span>|<span data-ttu-id="a10fc-105">221</span><span class="sxs-lookup"><span data-stu-id="a10fc-105">221</span></span>|  
|<span data-ttu-id="a10fc-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="a10fc-106">Keywords</span></span>|<span data-ttu-id="a10fc-107">EndToEndMonitoring，Troubleshooting，ServiceModel</span><span class="sxs-lookup"><span data-stu-id="a10fc-107">EndToEndMonitoring, Troubleshooting, ServiceModel</span></span>|  
|<span data-ttu-id="a10fc-108">層級</span><span class="sxs-lookup"><span data-stu-id="a10fc-108">Level</span></span>|<span data-ttu-id="a10fc-109">資訊</span><span class="sxs-lookup"><span data-stu-id="a10fc-109">Information</span></span>|  
|<span data-ttu-id="a10fc-110">通路</span><span class="sxs-lookup"><span data-stu-id="a10fc-110">Channel</span></span>|<span data-ttu-id="a10fc-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="a10fc-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="a10fc-112">描述</span><span class="sxs-lookup"><span data-stu-id="a10fc-112">Description</span></span>  

 <span data-ttu-id="a10fc-113">當服務模型收到來自傳輸的訊息時，便會發生此事件。</span><span class="sxs-lookup"><span data-stu-id="a10fc-113">This event is emitted when the Service Model receives a message from the transport.</span></span>  
  
## <a name="message"></a><span data-ttu-id="a10fc-114">訊息</span><span class="sxs-lookup"><span data-stu-id="a10fc-114">Message</span></span>  

 <span data-ttu-id="a10fc-115">發送器收到來自傳輸的訊息。</span><span class="sxs-lookup"><span data-stu-id="a10fc-115">The Dispatcher received a message from the transport.</span></span> <span data-ttu-id="a10fc-116">相互關聯 ID == '%1'。</span><span class="sxs-lookup"><span data-stu-id="a10fc-116">Correlation ID == '%1'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="a10fc-117">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a10fc-117">Details</span></span>  
  
|<span data-ttu-id="a10fc-118">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="a10fc-118">Data Item Name</span></span>|<span data-ttu-id="a10fc-119">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="a10fc-119">Data Item Type</span></span>|<span data-ttu-id="a10fc-120">描述</span><span class="sxs-lookup"><span data-stu-id="a10fc-120">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="a10fc-121">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="a10fc-121">Correlation ID</span></span>|`xs:GUID`|<span data-ttu-id="a10fc-122">活動識別碼，會將來自服務或用戶端的 `MessageSentToTransport` 事件，與另一端對應的 `MessageReceivedFromTransport` 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="a10fc-122">The activity ID used to correlate a `MessageSentToTransport` event from a service or client to its corresponding `MessageReceivedFromTransport` on the other end.</span></span>|  
|<span data-ttu-id="a10fc-123">HostReference</span><span class="sxs-lookup"><span data-stu-id="a10fc-123">HostReference</span></span>|`xs:string`|<span data-ttu-id="a10fc-124">若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。</span><span class="sxs-lookup"><span data-stu-id="a10fc-124">For Web-hosted services, this field uniquely identifies the service in the Web hierarchy.</span></span> <span data-ttu-id="a10fc-125">其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。</span><span class="sxs-lookup"><span data-stu-id="a10fc-125">Its format is defined as 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'.</span></span> <span data-ttu-id="a10fc-126">範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。</span><span class="sxs-lookup"><span data-stu-id="a10fc-126">Example: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.</span></span>|  
|<span data-ttu-id="a10fc-127">AppDomain</span><span class="sxs-lookup"><span data-stu-id="a10fc-127">AppDomain</span></span>|`xs:string`|<span data-ttu-id="a10fc-128">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="a10fc-128">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

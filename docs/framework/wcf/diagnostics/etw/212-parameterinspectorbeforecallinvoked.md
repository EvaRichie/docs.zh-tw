---
title: 212 - ParameterInspectorBeforeCallInvoked
ms.date: 03/30/2017
ms.assetid: 063fc8d2-ceac-4c18-8368-de84f2c78035
ms.openlocfilehash: 28c2aca4555d2e4ff498e450deae55ad6a87743c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279034"
---
# <a name="212---parameterinspectorbeforecallinvoked"></a><span data-ttu-id="26f95-102">212 - ParameterInspectorBeforeCallInvoked</span><span class="sxs-lookup"><span data-stu-id="26f95-102">212 - ParameterInspectorBeforeCallInvoked</span></span>

## <a name="properties"></a><span data-ttu-id="26f95-103">屬性</span><span class="sxs-lookup"><span data-stu-id="26f95-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="26f95-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="26f95-104">ID</span></span>|<span data-ttu-id="26f95-105">212</span><span class="sxs-lookup"><span data-stu-id="26f95-105">212</span></span>|  
|<span data-ttu-id="26f95-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="26f95-106">Keywords</span></span>|<span data-ttu-id="26f95-107">Troubleshooting，ServiceModel</span><span class="sxs-lookup"><span data-stu-id="26f95-107">Troubleshooting, ServiceModel</span></span>|  
|<span data-ttu-id="26f95-108">層級</span><span class="sxs-lookup"><span data-stu-id="26f95-108">Level</span></span>|<span data-ttu-id="26f95-109">資訊</span><span class="sxs-lookup"><span data-stu-id="26f95-109">Information</span></span>|  
|<span data-ttu-id="26f95-110">通路</span><span class="sxs-lookup"><span data-stu-id="26f95-110">Channel</span></span>|<span data-ttu-id="26f95-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="26f95-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="26f95-112">描述</span><span class="sxs-lookup"><span data-stu-id="26f95-112">Description</span></span>  

 <span data-ttu-id="26f95-113">服務模型已在 `BeforeCall` 上叫用 `ParameterInspector` 方法之後，即會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="26f95-113">This event is emitted after the Service Model has invoked the `BeforeCall` method on a `ParameterInspector`.</span></span>  
  
## <a name="message"></a><span data-ttu-id="26f95-114">訊息</span><span class="sxs-lookup"><span data-stu-id="26f95-114">Message</span></span>  

 <span data-ttu-id="26f95-115">發送器在型別 '%1' 的 ParameterInspector 上叫用了 'BeforeCall'。</span><span class="sxs-lookup"><span data-stu-id="26f95-115">The Dispatcher invoked 'BeforeCall' on a ParameterInspector of type '%1'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="26f95-116">詳細資料</span><span class="sxs-lookup"><span data-stu-id="26f95-116">Details</span></span>  
  
|<span data-ttu-id="26f95-117">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="26f95-117">Data Item Name</span></span>|<span data-ttu-id="26f95-118">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="26f95-118">Data Item Type</span></span>|<span data-ttu-id="26f95-119">描述</span><span class="sxs-lookup"><span data-stu-id="26f95-119">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="26f95-120">TypeName</span><span class="sxs-lookup"><span data-stu-id="26f95-120">TypeName</span></span>|`xs:string`|<span data-ttu-id="26f95-121">叫用之偵測器型別的 CLR FullName。</span><span class="sxs-lookup"><span data-stu-id="26f95-121">The CLR FullName of the invoked inspector's type.</span></span>|  
|<span data-ttu-id="26f95-122">HostReference</span><span class="sxs-lookup"><span data-stu-id="26f95-122">HostReference</span></span>|`xs:string`|<span data-ttu-id="26f95-123">若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。</span><span class="sxs-lookup"><span data-stu-id="26f95-123">For Web-hosted services, this field uniquely identifies the service in the Web hierarchy.</span></span> <span data-ttu-id="26f95-124">其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。</span><span class="sxs-lookup"><span data-stu-id="26f95-124">Its format is defined as 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'.</span></span> <span data-ttu-id="26f95-125">範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。</span><span class="sxs-lookup"><span data-stu-id="26f95-125">Example: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.</span></span>|  
|<span data-ttu-id="26f95-126">AppDomain</span><span class="sxs-lookup"><span data-stu-id="26f95-126">AppDomain</span></span>|`xs:string`|<span data-ttu-id="26f95-127">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="26f95-127">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|

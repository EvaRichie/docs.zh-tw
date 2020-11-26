---
title: 端點效能計數器
ms.date: 03/30/2017
ms.assetid: 7d44d576-bd4e-453b-8b76-a818ce90b806
ms.openlocfilehash: cdddd8be962df0b295eb394fcaba3756e8a1a50f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96237955"
---
# <a name="endpoint-performance-counters"></a><span data-ttu-id="cd98c-102">端點效能計數器</span><span class="sxs-lookup"><span data-stu-id="cd98c-102">Endpoint Performance Counters</span></span>

<span data-ttu-id="cd98c-103">端點效能計數器會擷取顯示端點如何接受訊息的資料。</span><span class="sxs-lookup"><span data-stu-id="cd98c-103">Endpoint performance counters capture data that reveals how an endpoint is accepting messages.</span></span> <span data-ttu-id="cd98c-104">使用效能監視器檢視時，可以在 `ServiceModelEndpoint 4.0.0.0` 效能物件下找到它們。</span><span class="sxs-lookup"><span data-stu-id="cd98c-104">They can be found under the `ServiceModelEndpoint 4.0.0.0` performance object when viewing with the Performance Monitor.</span></span> <span data-ttu-id="cd98c-105">執行個體是使用下列模式來命名：</span><span class="sxs-lookup"><span data-stu-id="cd98c-105">The instances are named using this pattern:</span></span>  
  
`(ServiceName).(ContractName)@(endpoint listener address)`  
  
 <span data-ttu-id="cd98c-106">此資料與針對個別作業而收集的資料類似，但只彙總了端點之間的資料。</span><span class="sxs-lookup"><span data-stu-id="cd98c-106">The data is similar to that collected for individual operations, but is only aggregated across the endpoint.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="cd98c-107">效能計數器執行個體的名稱具有長度限制。</span><span class="sxs-lookup"><span data-stu-id="cd98c-107">There is a limit on the length of a performance counter instance's name.</span></span> <span data-ttu-id="cd98c-108">當 Windows Communication Foundation (WCF) 的計數器實例名稱超過最大長度時，WCF 會以雜湊值取代實例名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="cd98c-108">When a Windows Communication Foundation (WCF) counter instance name exceeds the maximum length, WCF replaces a portion of the instance name with a hash value.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cd98c-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cd98c-109">See also</span></span>

- [<span data-ttu-id="cd98c-110">效能計數器</span><span class="sxs-lookup"><span data-stu-id="cd98c-110">Performance Counters</span></span>](index.md)

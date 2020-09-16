---
title: 每秒認可的交易作業數
ms.date: 03/30/2017
ms.assetid: 7318921b-47c4-4c8c-9fdd-41a92061c53f
ms.openlocfilehash: 047640e9b5cc22f2d443832fb7bd5afd47aef5be
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550634"
---
# <a name="transacted-operations-committed-per-second"></a><span data-ttu-id="d913e-102">每秒認可的交易作業數</span><span class="sxs-lookup"><span data-stu-id="d913e-102">Transacted Operations Committed Per Second</span></span>
<span data-ttu-id="d913e-103">計數器名稱：每秒認可的交易作業數。</span><span class="sxs-lookup"><span data-stu-id="d913e-103">Counter Name: Transacted Operations Committed Per Second.</span></span>  
  
## <a name="description"></a><span data-ttu-id="d913e-104">描述</span><span class="sxs-lookup"><span data-stu-id="d913e-104">Description</span></span>  
 <span data-ttu-id="d913e-105">此服務每秒所認可的異動作業數。</span><span class="sxs-lookup"><span data-stu-id="d913e-105">Number of transactional operations that have been committed in this service in a second.</span></span>  
  
 <span data-ttu-id="d913e-106">此計數器是效能計數器類型 [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10))，其值是使用下列公式來計算。</span><span class="sxs-lookup"><span data-stu-id="d913e-106">This counter is of performance counter type [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), whose value is calculated using the following formula.</span></span>  
  
 <span data-ttu-id="d913e-107">(N 1 - N 0 ) / ( (D 1 -D 0 ) / F)</span><span class="sxs-lookup"><span data-stu-id="d913e-107">(N 1 - N 0 ) / ( (D 1 -D 0 ) / F)</span></span>

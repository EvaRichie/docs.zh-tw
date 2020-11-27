---
title: Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure
ms.date: 03/30/2017
ms.assetid: 3a4ead79-8550-4037-84e3-fd70ff56e001
ms.openlocfilehash: 2f0198d3c288b4c3833cdac8e5f943ba822c22e9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96252019"
---
# <a name="microsofttransactionstransactionbridgeregisterparticipantfailure"></a><span data-ttu-id="522a4-102">Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure</span><span class="sxs-lookup"><span data-stu-id="522a4-102">Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure</span></span>

<span data-ttu-id="522a4-103">WS-AT 通訊協定服務無法登錄控制通訊協定的參與者。</span><span class="sxs-lookup"><span data-stu-id="522a4-103">The WS-AT protocol service failed to register a participant for a control protocol.</span></span>  
  
## <a name="description"></a><span data-ttu-id="522a4-104">描述</span><span class="sxs-lookup"><span data-stu-id="522a4-104">Description</span></span>  

 <span data-ttu-id="522a4-105">如果 MSDTC 偵測到無效的登錄要求則會進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="522a4-105">Traced if MSDTC detects an invalid Registration request.</span></span> <span data-ttu-id="522a4-106">這種情形可能是因為多個完成登錄要求和內部錯誤所造成。</span><span class="sxs-lookup"><span data-stu-id="522a4-106">This can be caused by  multiple Completion registration requests and internal errors.</span></span>  
  
## <a name="troubleshooting"></a><span data-ttu-id="522a4-107">疑難排解</span><span class="sxs-lookup"><span data-stu-id="522a4-107">Troubleshooting</span></span>  

 <span data-ttu-id="522a4-108">請勿嘗試多次登錄完成。</span><span class="sxs-lookup"><span data-stu-id="522a4-108">Do not try to Register for Completion more than once.</span></span>  <span data-ttu-id="522a4-109">同時，檢查追蹤訊息內的狀態字串，以判斷是否有任何可執行動作的項目存在。</span><span class="sxs-lookup"><span data-stu-id="522a4-109">Also, inspect the status string within the trace message to determine if any actionable item exists.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="522a4-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="522a4-110">See also</span></span>

- [<span data-ttu-id="522a4-111">追蹤</span><span class="sxs-lookup"><span data-stu-id="522a4-111">Tracing</span></span>](index.md)
- [<span data-ttu-id="522a4-112">使用追蹤來疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="522a4-112">Using Tracing to Troubleshoot Your Application</span></span>](using-tracing-to-troubleshoot-your-application.md)
- [<span data-ttu-id="522a4-113">系統管理與診斷</span><span class="sxs-lookup"><span data-stu-id="522a4-113">Administration and Diagnostics</span></span>](../index.md)

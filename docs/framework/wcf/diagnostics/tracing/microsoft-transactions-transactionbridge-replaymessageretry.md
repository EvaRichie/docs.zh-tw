---
title: Microsoft.Transactions.TransactionBridge.ReplayMessageRetry
ms.date: 03/30/2017
ms.assetid: e5b820ae-504d-405a-926a-9effa41d2369
ms.openlocfilehash: 162452d5d12859571d78ef19cf1d838953ee7acd
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596203"
---
# <a name="microsofttransactionstransactionbridgereplaymessageretry"></a><span data-ttu-id="68591-102">Microsoft.Transactions.TransactionBridge.ReplayMessageRetry</span><span class="sxs-lookup"><span data-stu-id="68591-102">Microsoft.Transactions.TransactionBridge.ReplayMessageRetry</span></span>
<span data-ttu-id="68591-103">重新執行訊息重試已傳送給沒有回應的協調器。</span><span class="sxs-lookup"><span data-stu-id="68591-103">A replay message retry was sent to an unresponsive coordinator.</span></span>  
  
## <a name="description"></a><span data-ttu-id="68591-104">描述</span><span class="sxs-lookup"><span data-stu-id="68591-104">Description</span></span>  
 <span data-ttu-id="68591-105">追蹤本機異動管理員是否因為上層協調器未在指定時間內接收到回應，而需要重新傳送「重新執行」訊息給上層協調器。</span><span class="sxs-lookup"><span data-stu-id="68591-105">Traced if the local Transaction Manager needed to resend a Replay message to a superior coordinator because it did not receive a response in a given amount of time.</span></span>  
  
## <a name="troubleshooting"></a><span data-ttu-id="68591-106">疑難排解</span><span class="sxs-lookup"><span data-stu-id="68591-106">Troubleshooting</span></span>  
 <span data-ttu-id="68591-107">調查讓回應無法準時傳遞的潛在網路或產品問題。</span><span class="sxs-lookup"><span data-stu-id="68591-107">Investigate potential network or product issues that prevent the response from being delivered on time.</span></span>  <span data-ttu-id="68591-108">如果看到許多這類訊息，這可能表示基礎結構發生問題或回應時間異常地長。</span><span class="sxs-lookup"><span data-stu-id="68591-108">If many of these messages are seen, it can indicate infrastructure problems or abnormally long response times.</span></span> <span data-ttu-id="68591-109">這兩個問題都會大幅降低系統內的異動量。</span><span class="sxs-lookup"><span data-stu-id="68591-109">Both issues will drastically reduce the throughput of transactions within the system.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="68591-110">請參閱</span><span class="sxs-lookup"><span data-stu-id="68591-110">See also</span></span>

- [<span data-ttu-id="68591-111">追蹤</span><span class="sxs-lookup"><span data-stu-id="68591-111">Tracing</span></span>](index.md)
- [<span data-ttu-id="68591-112">使用追蹤來疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="68591-112">Using Tracing to Troubleshoot Your Application</span></span>](using-tracing-to-troubleshoot-your-application.md)
- [<span data-ttu-id="68591-113">系統管理與診斷</span><span class="sxs-lookup"><span data-stu-id="68591-113">Administration and Diagnostics</span></span>](../index.md)

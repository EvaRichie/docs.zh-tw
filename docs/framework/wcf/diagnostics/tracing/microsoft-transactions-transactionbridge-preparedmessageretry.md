---
title: Microsoft.Transactions.TransactionBridge.PreparedMessageRetry
ms.date: 03/30/2017
ms.assetid: 2194292d-bf5f-4aef-9336-cd3c4795cb71
ms.openlocfilehash: edab153123ae48702811532df3b5b5bf0849c26a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275914"
---
# <a name="microsofttransactionstransactionbridgepreparedmessageretry"></a><span data-ttu-id="6ab6c-102">Microsoft.Transactions.TransactionBridge.PreparedMessageRetry</span><span class="sxs-lookup"><span data-stu-id="6ab6c-102">Microsoft.Transactions.TransactionBridge.PreparedMessageRetry</span></span>

<span data-ttu-id="6ab6c-103">準備訊息重試已傳送給沒有回應的協調器。</span><span class="sxs-lookup"><span data-stu-id="6ab6c-103">A prepared message retry was sent to an unresponsive coordinator.</span></span>  
  
## <a name="description"></a><span data-ttu-id="6ab6c-104">描述</span><span class="sxs-lookup"><span data-stu-id="6ab6c-104">Description</span></span>  

 <span data-ttu-id="6ab6c-105">追蹤本機交易管理員是否因為上層協調器未在指定時間內接收到回應，而需要重新傳送「準備」訊息給上層協調器。</span><span class="sxs-lookup"><span data-stu-id="6ab6c-105">Traced if the local Transaction Manager needed to resend a Prepared message to a superior coordinator because it did not receive a response in a given amount of time/</span></span>  
  
## <a name="troubleshooting"></a><span data-ttu-id="6ab6c-106">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6ab6c-106">Troubleshooting</span></span>  

 <span data-ttu-id="6ab6c-107">調查讓回應無法準時傳遞的潛在網路或產品問題。</span><span class="sxs-lookup"><span data-stu-id="6ab6c-107">Investigate potential network or product issues that prevent the response from being delivered on time.</span></span>  <span data-ttu-id="6ab6c-108">如果看到許多這類訊息，這可能表示基礎結構發生問題或回應時間異常地長。</span><span class="sxs-lookup"><span data-stu-id="6ab6c-108">If many of these messages are seen, it can indicate infrastructure problems or abnormally long response times.</span></span> <span data-ttu-id="6ab6c-109">這兩個問題都會大幅降低系統內的異動量。</span><span class="sxs-lookup"><span data-stu-id="6ab6c-109">Both issues will drastically reduce the throughput of transactions within the system.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6ab6c-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6ab6c-110">See also</span></span>

- [<span data-ttu-id="6ab6c-111">追蹤</span><span class="sxs-lookup"><span data-stu-id="6ab6c-111">Tracing</span></span>](index.md)
- [<span data-ttu-id="6ab6c-112">使用追蹤來疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="6ab6c-112">Using Tracing to Troubleshoot Your Application</span></span>](using-tracing-to-troubleshoot-your-application.md)
- [<span data-ttu-id="6ab6c-113">系統管理與診斷</span><span class="sxs-lookup"><span data-stu-id="6ab6c-113">Administration and Diagnostics</span></span>](../index.md)

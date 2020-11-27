---
title: 每秒的安全性驗證和驗證失敗數
ms.date: 03/30/2017
ms.assetid: 266c3bd3-2ffc-4471-94b7-3675443be1ac
ms.openlocfilehash: c64c121550043127db674fac6287a870449d789d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253115"
---
# <a name="security-validation-and-authentication-failures-per-second"></a><span data-ttu-id="74370-102">每秒的安全性驗證和驗證失敗數</span><span class="sxs-lookup"><span data-stu-id="74370-102">Security Validation and Authentication Failures Per Second</span></span>

<span data-ttu-id="74370-103">計數器名稱：每秒的安全性驗證和驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="74370-103">Counter name: Security Validation and Authentication Failures Per Second.</span></span>  
  
## <a name="description"></a><span data-ttu-id="74370-104">描述</span><span class="sxs-lookup"><span data-stu-id="74370-104">Description</span></span>  

 <span data-ttu-id="74370-105">每當因為「未授權的安全性呼叫數」計數器所未涵蓋的安全性問題而拒絕訊息時，這個計數器就會遞增。</span><span class="sxs-lookup"><span data-stu-id="74370-105">This counter is incremented whenever a message is rejected due to a security problem not covered by the "Security Calls Not Authorized" counter.</span></span> <span data-ttu-id="74370-106">這類問題包括：</span><span class="sxs-lookup"><span data-stu-id="74370-106">Such problems include:</span></span>  
  
- <span data-ttu-id="74370-107">無法從訊息中讀取用戶端權杖。</span><span class="sxs-lookup"><span data-stu-id="74370-107">Client token cannot be read from the message.</span></span>  
  
- <span data-ttu-id="74370-108">用戶端權杖已經驗證失敗 (例如密碼錯誤)。</span><span class="sxs-lookup"><span data-stu-id="74370-108">Client token has failed authentication (for example, bad password).</span></span>  
  
- <span data-ttu-id="74370-109">簽章驗證已經失敗 (例如訊息遭到竄改)。</span><span class="sxs-lookup"><span data-stu-id="74370-109">Signature verification has failed (for example, the message has been tampered).</span></span>  
  
- <span data-ttu-id="74370-110">此訊息與之前的訊息重複，這可能會在重新執行攻擊時發生。</span><span class="sxs-lookup"><span data-stu-id="74370-110">The message is a duplicate from a previous one, which can happen during a replay attack.</span></span>  
  
- <span data-ttu-id="74370-111">發生解密失敗。</span><span class="sxs-lookup"><span data-stu-id="74370-111">A decryption failure has occurred.</span></span>  
  
- <span data-ttu-id="74370-112">訊息中遺失某些必要的項目 (例如遺失時間戳記或加密的資料區塊)。</span><span class="sxs-lookup"><span data-stu-id="74370-112">Some required elements (for example, missing timestamp or encrypted data block) are missing from the message.</span></span>  
  
- <span data-ttu-id="74370-113">在 TLSNEGO/SPNEGO 交換期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="74370-113">Errors have occurred during TLSNEGO/SPNEGO handshake.</span></span>  
  
 <span data-ttu-id="74370-114">此計數器是效能計數器類型 [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10))，其值是使用下列公式計算的：</span><span class="sxs-lookup"><span data-stu-id="74370-114">This counter is of performance counter type [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), whose value is calculated using the following formula:</span></span>  
  
 <span data-ttu-id="74370-115">(N1-N0)/((D1-D0)/F)</span><span class="sxs-lookup"><span data-stu-id="74370-115">(N1-N0)/((D1-D0)/F)</span></span>

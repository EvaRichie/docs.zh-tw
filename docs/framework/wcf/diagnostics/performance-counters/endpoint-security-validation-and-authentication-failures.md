---
title: 端點：安全性驗證和驗證失敗數
ms.date: 03/30/2017
ms.assetid: 5bad60aa-6084-4c7b-aefd-9b581f04382e
ms.openlocfilehash: a9a4758b26c744c55af200aee22a7e90c5a5cf57
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256465"
---
# <a name="endpoint-security-validation-and-authentication-failures"></a>端點：安全性驗證和驗證失敗數

計數器名稱：安全性驗證和驗證失敗數  
  
## <a name="description"></a>描述  

 每當因為「未授權的安全性呼叫數」計數器所未涵蓋的安全性問題而拒絕訊息時，這個計數器就會遞增。 這類問題包括：  
  
- 無法從訊息中讀取用戶端權杖。  
  
- 用戶端權杖已經驗證失敗 (密碼錯誤)。  
  
- 簽章驗證已經失敗 (訊息遭到竄改)。  
  
- 此訊息與之前的訊息重複，這可能會在重新執行攻擊時發生。  
  
- 發生解密失敗。  
  
- 訊息中遺失某些必要的元素 (遺失時間戳記或加密的資料區塊)。  
  
- 在 TLSNEGO/SPNEGO 交換期間發生錯誤。

---
title: 快取原則互動 — 最長使用期限和最長過時
ms.date: 03/30/2017
helpviewer_keywords:
- maximum staleness
- freshness of cached resources
- time, cached resources
- maximum age policy
- staleness of cached resources
- age of cached resources
ms.assetid: 7f775925-89a1-4956-ba90-c869c1749a94
ms.openlocfilehash: bdfa608b5169755b2b4daaaa26e562308ae2be01
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250602"
---
# <a name="cache-policy-interactionmaximum-age-and-maximum-staleness"></a>快取原則互動 — 最長使用期限和最長過時

為了協助確保將最新內容傳回給用戶端應用程式，用戶端快取原則與伺服器重新驗證需求的互動一律會導致最保守的快取原則。 本主題中的所有範例都會說明在 1 月 1 日快取並在 1 月 4 日到期之資源的快取原則。  
  
 在下列範例中，最長過時值 (`maxStale`) 是與最長使用期限 (`maxAge`) 一起使用：  
  
- 根據 `maxAge` 值，如果快取原則設定 `maxAge` = 5 天，但未指定 `maxStale` 值，則在 1 月 6 日之前可以使用內容。 不過，根據伺服器的重新驗證需求，內容會在 1 月 4 日到期。 因為內容到期日較為保守 (更快)，所以其優先順序高於 `maxAge` 原則。 因此，內容會在 1 月 4 日到期，而且必須重新驗證，即使未達到其最長使用期限也是一樣。  
  
- 根據 `maxAge` 值，如果快取原則設定 `maxAge` = 5 天且 `maxStale` = 3 天，則在1 月 6 日之前可以使用內容。 根據 `maxStale` 值，在 1 月 7 日之前可以使用內容。 因此，會在 1 月 6 日重新驗證內容。  
  
- 根據 `maxAge` 值，如果快取原則設定 `maxAge` = 5 天且 `maxStale` = 1 天，則在 1 月 6 日之前可以使用內容。 根據 `maxStale` 值，在 1 月 5 日之前可以使用內容。 因此，會在 1 月 5 日重新驗證內容。  
  
 最長使用期限小於內容到期日時，一律會使用更保守的快取行為，而且最長過時值沒有任何作用。 下列範例說明達到最長使用期限 (`maxAge`) 但在內容到期之前，設定最長過時 (`maxStale`) 值的效果：  
  
- 如果快取原則設定 `maxAge` = 1 天，但未指定 `maxStale` 值的值，則會在 1 月 2 日重新驗證內容，即使未到期也是一樣。  
  
- 如果快取原則設定 `maxAge` = 1 天且 `maxStale` = 3 天，則會在 1 月 2 日重新驗證內容，來強制執行更保守的原則設定。  
  
- 如果快取原則設定 `maxAge` = 1 天且 `maxStale` = 1 天，則會在 1 月 2 日重新驗證內容。  
  
## <a name="see-also"></a>另請參閱

- [網路應用程式的快取管理](cache-management-for-network-applications.md)
- [快取原則](cache-policy.md)
- [以位置為基礎的快取原則](location-based-cache-policies.md)
- [以時間為基礎的快取原則](time-based-cache-policies.md)
- [設定網路應用程式的快取功能](configuring-caching-in-network-applications.md)
- [快取原則互動 — 最長使用期限和最小有效期限](cache-policy-interaction-maximum-age-and-minimum-freshness.md)

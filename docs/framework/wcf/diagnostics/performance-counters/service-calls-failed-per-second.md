---
title: 服務：每秒失敗的呼叫數
ms.date: 03/30/2017
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
ms.openlocfilehash: 5629c55cba6f21de24a1de7e8d38a9c08fcf4fb1
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559105"
---
# <a name="service-calls-failed-per-second"></a>服務：每秒失敗的呼叫數
計數器名稱：每秒失敗的呼叫數。  
  
## <a name="description"></a>描述  
 未處理之例外狀況的呼叫數，以及此服務在一秒之內所收到的呼叫數。  
  
 此計數器是效能計數器類型 [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10))，其值是使用下列公式來計算。  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)  
  
 在 Managed 程式碼中，發生錯誤狀況時會擲回例外狀況。  
  
 在 Managed 程式碼中，發生錯誤狀況時會擲回例外狀況。  
  
 每當此服務有未處理的例外狀況時，此計數器就會遞增。  
  
## <a name="see-also"></a>另請參閱

- [指定與處理合約和服務中的錯誤](../../specifying-and-handling-faults-in-contracts-and-services.md)

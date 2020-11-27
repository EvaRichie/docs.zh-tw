---
title: 服務：每秒失敗的呼叫數
ms.date: 03/30/2017
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
ms.openlocfilehash: c97e4b0c6c2c71756a9bed7b1a2359ad0c118a98
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96252968"
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

---
title: ICLRGCManager::GetStats 方法
ms.date: 03/30/2017
api_name:
- ICLRGCManager.GetStats
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::GetStats
helpviewer_keywords:
- GetStats method, ICLRGCManager interface [.NET Framework hosting]
- ICLRGCManager::GetStats method [.NET Framework hosting]
ms.assetid: ce259d1d-cd81-4490-a7a1-0d0ea0804872
topic_type:
- apiref
ms.openlocfilehash: 70fe8b132f03925c41b6bc7aae8e60fea1b05202
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95678268"
---
# <a name="iclrgcmanagergetstats-method"></a>ICLRGCManager::GetStats 方法

取得有關 common language runtime 的垃圾收集系統的一組目前統計資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetStats (  
    [in, out] COR_GC_STATS *pStats  
);  
```  
  
## <a name="parameters"></a>參數  

 `pStats`  
 [in，out]包含所要求統計資料的 [COR_GC_STATS](cor-gc-stats-structure.md) 實例。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`GetStats` 傳回成功。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫已超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|當封鎖的執行緒或光纖正在等候時，已取消事件。|  
|E_FAIL|發生未知的嚴重失敗。 在方法傳回 E_FAIL 之後，就無法在進程中使用 CLR。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  

 CLR 只會計算並傳回由的欄位所指定的統計資料 `Flags` `pStats` 。  
  
 將 `Flags` 欄位設定為 [COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md) 列舉的一或多個值，以指定要設定 [COR_GC_STATS](cor-gc-stats-structure.md) 結構中的統計資料。  
  
 使用方式的範例如下：  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll  
  
 連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [自動記憶體管理](../../../standard/automatic-memory-management.md)
- [COR_GC_STATS 結構](cor-gc-stats-structure.md)
- [COR_GC_STAT_TYPES 列舉](cor-gc-stat-types-enumeration.md)
- [記憶體回收](../../../standard/garbage-collection/index.md)
- [ICLRControl 介面](iclrcontrol-interface.md)
- [ICLRGCManager 介面](iclrgcmanager-interface.md)
- [CLR 裝載介面](clr-hosting-interfaces.md)
- [裝載介面](hosting-interfaces.md)
- [裝載](index.md)

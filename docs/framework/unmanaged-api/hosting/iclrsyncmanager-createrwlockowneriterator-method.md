---
title: ICLRSyncManager::CreateRWLockOwnerIterator 方法
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.CreateRWLockOwnerIterator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator
helpviewer_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator method [.NET Framework hosting]
- CreateRWLockOwnerIterator method [.NET Framework hosting]
ms.assetid: b5535b87-9439-424e-b9b3-7d6fafb9819e
topic_type:
- apiref
ms.openlocfilehash: f8fde4905c41dffde90c6361b5a8cdffa15deb4a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503961"
---
# <a name="iclrsyncmanagercreaterwlockowneriterator-method"></a>ICLRSyncManager::CreateRWLockOwnerIterator 方法
要求 common language runtime （CLR）為主機建立反覆運算器，以用來判斷等候讀取器寫入器鎖定的一組工作。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CreateRWLockOwnerIterator (  
    [in]  SIZE_T    cookie,  
    [out] SIZE_T   *pIterator  
);  
```  
  
## <a name="parameters"></a>參數  
 `cookie`  
 在與所需讀取器寫入器鎖定相關聯的 cookie。  
  
 `pIterator`  
 脫銷可傳遞至[GetRWLockOwnerNext](iclrsyncmanager-getrwlockownernext-method.md)和[DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md)方法之反覆運算器的指標。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|`CreateRWLockOwnerIterator`已成功傳回。|  
|HOST_E_CLRNOTAVAILABLE|CLR 尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|已封鎖的執行緒或光纖在等候時取消了事件。|  
|E_FAIL|發生不明的嚴重失敗。 當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
|HOST_E_INVALIDOPERATION|`CreateRWLockOwnerIterator`在目前正在執行 managed 程式碼的執行緒上呼叫。|  
  
## <a name="remarks"></a>備註  
 主機通常會 `CreateRWLockOwnerIterator` `DeleteRWLockOwnerIterator` `GetRWLockOwnerNext` 在偵測到鎖死時呼叫、和方法。 主機負責確保讀取器寫入器的鎖定仍然有效，因為 CLR 不會嘗試讓讀取器寫入器鎖定保持運作。 有數個策略可供主機使用，以確保鎖定的有效性：  
  
- 主機可以封鎖讀取器寫入器鎖定（例如， [IHostSemaphore：： ReleaseSemaphore](ihostsemaphore-releasesemaphore-method.md)）的發行呼叫，同時確保此區塊不會造成鎖死。  
  
- 主機可以封鎖在與讀取器寫入器鎖定相關聯的事件物件上等待結束，再次確保此區塊不會造成鎖死。  
  
> [!NOTE]
> `CreateRWLockOwnerIterator`必須只在目前執行非受控碼的執行緒上呼叫。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRSyncManager 介面](iclrsyncmanager-interface.md)
- [IHostSyncManager 介面](ihostsyncmanager-interface.md)

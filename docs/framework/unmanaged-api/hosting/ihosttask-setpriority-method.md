---
title: IHostTask::SetPriority 方法
ms.date: 03/30/2017
api_name:
- IHostTask.SetPriority
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::SetPriority
helpviewer_keywords:
- IHostTask::SetPriority method [.NET Framework hosting]
- SetPriority method [.NET Framework hosting]
ms.assetid: cd8c379b-c7a0-434f-8e23-899bd26be75d
topic_type:
- apiref
ms.openlocfilehash: ac3a8479cdf05e55885bd55d4e4fb8e6e47686f9
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842394"
---
# <a name="ihosttasksetpriority-method"></a>IHostTask::SetPriority 方法
要求主機針對目前[IHostTask](ihosttask-interface.md)實例所代表的工作，調整執行緒優先順序層級。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetPriority (  
    [in] int newPriority  
);  
```  
  
## <a name="parameters"></a>參數  
 `newPriority`  
 在整數，表示目前實例所代表之工作的要求的執行緒優先順序值 `IHostTask` 。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`SetPriority`已成功傳回。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|已封鎖的執行緒或光纖在等候時取消了事件。|  
|E_FAIL|發生不明的嚴重失敗。 當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  
 執行緒會使用迴圈配置資源系統（部分根據執行緒的優先權層級）來授與處理時間。 `SetPriority`允許 CLR 設定目前工作的執行緒優先權層級。 支援下列 `newPriority` 值。  
  
- THREAD_PRIORITY_ABOVE_NORMAL  
  
- THREAD_PRIORITY_BELOW_NORMAL  
  
- THREAD_PRIORITY_HIGHEST  
  
- THREAD_PRIORITY_IDLE  
  
- THREAD_PRIORITY_LOWEST  
  
- THREAD_PRIORITY_NORMAL  
  
- THREAD_PRIORITY_TIME_CRITICAL  
  
 `SetPriority`當使用者程式碼修改的值時，CLR <xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType> 會呼叫。 主機可以針對執行緒優先順序指派定義自己的演算法，並可隨意忽略此要求。  
  
> [!NOTE]
> `SetPriority`不會報告執行緒優先權層級是否已變更。 呼叫[IHostTask：： GetPriority](ihosttask-getpriority-method.md)以判斷工作的執行緒優先順序層級值。  
  
 執行緒優先權層級的值是由 Win32 `SetThreadPriority` 函數所定義。 如需執行緒優先順序的詳細資訊，請參閱 Windows 平臺檔。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Threading.Thread>
- [ICLRTask 介面](iclrtask-interface.md)
- [ICLRTaskManager 介面](iclrtaskmanager-interface.md)
- [IHostTask 介面](ihosttask-interface.md)
- [GetPriority 方法](ihosttask-getpriority-method.md)
- [IHostTaskManager 介面](ihosttaskmanager-interface.md)

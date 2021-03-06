---
title: IHostMemoryManager::VirtualQuery 方法
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualQuery
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualQuery
helpviewer_keywords:
- IHostMemoryManager::VirtualQuery method [.NET Framework hosting]
- VirtualQuery method [.NET Framework hosting]
ms.assetid: 757af1e6-b9e8-49e7-b5db-342be3aa205f
topic_type:
- apiref
ms.openlocfilehash: 6e3cb5bcec831f143d45f733c9e2f977390aade6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731237"
---
# <a name="ihostmemorymanagervirtualquery-method"></a>IHostMemoryManager::VirtualQuery 方法

作為對應 Win32 函數的邏輯包裝函式。 的 Win32 實 `VirtualQuery` 址會在呼叫進程的虛擬位址空間中，抓取頁面範圍的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT VirtualQuery (  
    [in]  void*    lpAddress,  
    [out] void*    lpBuffer,  
    [in]  SIZE_T   dwLength,  
    [out] SIZE_T*  pResult  
);  
```  
  
## <a name="parameters"></a>參數  

 `lpAddress`  
 在要查詢之虛擬記憶體中的位址指標。  
  
 `lpBuffer`  
 擴展結構的指標，其中包含指定之記憶體區域的相關資訊。  
  
 `dwLength`  
 在指向的緩衝區大小（以位元組為單位） `lpBuffer` 。  
  
 `pResult`  
 擴展資訊緩衝區傳回的位元組數目指標。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`VirtualQuery` 傳回成功。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫已超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|當封鎖的執行緒或光纖正在等候時，已取消事件。|  
|E_FAIL|發生未知的嚴重失敗。 當方法傳回 E_FAIL 時，CLR 在進程內將無法再使用。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  

 `VirtualQuery` 提供有關呼叫進程的虛擬位址空間中的頁面範圍的資訊。 這個實值會將參數的值設定 `pResult` 為資訊緩衝區中傳回的位元組數，並傳回 HRESULT 值。 在 Win32 `VirtualQuery` 函數中，傳回值是緩衝區大小。 如需詳細資訊，請參閱 Windows 平臺檔。  
  
> [!IMPORTANT]
> 作業系統的執行 `VirtualQuery` 不會產生鎖死，而且可以執行至完成，並在使用者程式碼中暫停隨機執行緒。 在實作為此方法的裝載版本時，請特別小心。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll  
  
 連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IHostMemoryManager 介面](ihostmemorymanager-interface.md)

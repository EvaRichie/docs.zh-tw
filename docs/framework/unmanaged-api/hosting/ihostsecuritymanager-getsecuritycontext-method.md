---
title: IHostSecurityManager::GetSecurityContext 方法
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.GetSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::GetSecurityContext
helpviewer_keywords:
- GetSecurityContext method [.NET Framework hosting]
- IHostSecurityManager::GetSecurityContext method [.NET Framework hosting]
ms.assetid: 958970d6-f6a2-4b84-b32a-f555cbaf8f61
topic_type:
- apiref
ms.openlocfilehash: dfb96de02549e6d0f178c099793741f7fbd61d55
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724789"
---
# <a name="ihostsecuritymanagergetsecuritycontext-method"></a>IHostSecurityManager::GetSecurityContext 方法

從主機取得要求的 [IHostSecurityCoNtext](ihostsecuritycontext-interface.md) 。  
  
## <a name="syntax"></a>語法  
  
```cpp
HRESULT GetSecurityContext (  
    [in]  EContextType eContextType,
    [out] IHostSecurityContext** ppSecurityContext  
);  
```  
  
## <a name="parameters"></a>參數  

 `eContextType`  
 在其中一個 [ECoNtextType](econtexttype-enumeration.md) 值，指出要傳回哪一種類型的安全性內容。  
  
 `ppSecurityContext`  
 擴展之介面指標的位址 `IHostSecurityContext` `eContextType` 。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`GetSecurityContext` 傳回成功。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫已超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|當封鎖的執行緒或光纖正在等候時，已取消事件。|  
|E_FAIL|發生未知的嚴重失敗。 當方法傳回 E_FAIL 時，CLR 在進程內將無法再使用。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  

 主機可以透過 CLR 和使用者程式碼控制執行緒權杖的所有程式碼存取。 它也可以確保在非同步作業或具有限制程式碼存取的程式碼點之間傳遞完整的安全性內容資訊。 `IHostSecurityContext` 封裝此安全性內容資訊，這對 CLR 而言是不透明的。 CLR 會捕捉此資訊，並將其移動到執行緒集區背景工作專案分派、完成項執行，以及模組和類別結構。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll  
  
 連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [EContextType 列舉](econtexttype-enumeration.md)
- [IHostSecurityContext 介面](ihostsecuritycontext-interface.md)
- [IHostSecurityManager 介面](ihostsecuritymanager-interface.md)

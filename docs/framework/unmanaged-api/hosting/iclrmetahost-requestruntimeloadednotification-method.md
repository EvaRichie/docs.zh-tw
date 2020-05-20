---
title: ICLRMetaHost::RequestRuntimeLoadedNotification 方法
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
ms.openlocfilehash: 6813f72f9d27aeff90f797a6ca9370b22e03e6f0
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703701"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>ICLRMetaHost::RequestRuntimeLoadedNotification 方法
提供回呼函式，保證會在第一次載入 common language runtime （CLR）版本，但尚未啟動時呼叫。 這個方法會取代[LockClrVersion](lockclrversion-function.md)函數。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>參數  
 `pCallbackFunction`  
 在載入新的執行時間時所叫用的回呼函式。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|已成功完成命令。|  
|E_POINTER|`pCallbackFunction` 為 null。|  
  
## <a name="remarks"></a>備註  
 回呼會以下列方式運作：  
  
- 只有在第一次載入執行時間時，才會叫用回呼。  
  
- 不會針對相同執行時間的可重新進入負載叫用回呼。  
  
- 對於不可重新進入的執行時間載入，會序列化回呼函數的呼叫。  
  
 回呼函數具有下列原型：  
  
```cpp  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 回呼函數原型如下所示：  
  
- `pfnCallbackThreadSet`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 如果主機打算載入或造成另一個執行時間以可重新進入的方式載入，則 `pfnCallbackThreadSet` `pfnCallbackThreadUnset` 必須以下列方式使用回呼函式中提供的和參數：  
  
- `pfnCallbackThreadSet`必須由執行緒呼叫，可能會在嘗試進行這類負載之前造成執行時間載入。  
  
- `pfnCallbackThreadUnset`當執行緒不會再造成這類執行時間載入（以及從初始回呼傳回之前）時，必須呼叫。  
  
- `pfnCallbackThreadSet`和 `pfnCallbackThreadUnset` 都是不可重新進入的。  
  
> [!NOTE]
> 主應用程式不能 `pfnCallbackThreadSet` 在 `pfnCallbackThreadUnset` 參數的範圍之外呼叫和 `pCallbackFunction` 。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRMetaHost 介面](iclrmetahost-interface.md)
- [裝載](index.md)

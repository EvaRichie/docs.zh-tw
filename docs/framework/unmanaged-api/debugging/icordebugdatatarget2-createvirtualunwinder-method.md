---
title: ICorDebugDataTarget2::CreateVirtualUnwinder 方法
ms.date: 03/30/2017
ms.assetid: 354c8b4c-7d23-45c6-a7d7-3be4c2a5b772
ms.openlocfilehash: 0967b1cda86eab35015279edeed9a6b9852036b6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95713927"
---
# <a name="icordebugdatatarget2createvirtualunwinder-method"></a>ICorDebugDataTarget2::CreateVirtualUnwinder 方法

建立新的堆疊 unwinder，以從初始內容 (不一定是執行緒的分葉) 開始回溯。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CreateVirtualUnwinder(  
    [in] DWORD nativeThreadID,  
    [in] ULONG32 contextFlags,  
    [in] ULONG32 cbContext,  
    [in, size_is(cbContext)] BYTE initialContext[],  
    [out] ICorDebugVirtualUnwinder ** ppUnwinder);  
};  
```  
  
## <a name="parameters"></a>參數  

 nativeThreadID  
 [in] 其堆疊未回溯之執行緒的原生執行緒 ID。  
  
 contextFlags  
 [in] 指定哪些內容部分會在 `initialContext` 中定義的旗標。  
  
 cbContext  
 [in] `initialContext` 的大小。  
  
 initialContext  
 [in] 內容中的資料。  
  
 ppUnwinder  
 [out] ICorDebugVirtualUnwinder 介面物件的位址指標。  
  
## <a name="return-value"></a>傳回值  

 如果成功，則為 `S_OK`。 其他任何 `HRESULT` 表示失敗。 `HRESULT`Mscordbi.dll 收到的任何失敗都會被視為嚴重錯誤，而導致[ICorDebug](icordebug-interface.md)方法傳回 `CORDBG_E_DATA_TARGET_ERROR` 。  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個方法僅適用於 .NET Native。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorDebugDataTarget2 介面](icordebugdatatarget2-interface.md)
- [偵錯介面](debugging-interfaces.md)

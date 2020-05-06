---
title: 適用於 Silverlight 的 CreateDebuggingInterfaceFromVersion 函式
ms.date: 03/30/2017
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 35c7a18f-133a-4584-bd25-bb338568b0c6
ms.openlocfilehash: c83bdcca4fab75b4ae94500ceb785b6000cd802a
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860861"
---
# <a name="createdebugginginterfacefromversion-function-for-silverlight"></a>適用於 Silverlight 的 CreateDebuggingInterfaceFromVersion 函式
接受從[CreateVersionStringFromModule](createversionstringfrommodule-function.md)函式傳回的 common language RUNTIME （CLR）版本字串，並傳回對應的偵錯工具介面（通常是[ICorDebug](icordebug-interface.md)）。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  LPCWSTR      szDebuggeeVersion,  
    [out] IUnknown**   ppCordb,  
);  
```  
  
## <a name="parameters"></a>參數  
 `szDebuggeeVersion`  
 在目標偵錯工具中 CLR 的版本字串（由[CreateVersionStringFromModule 函數](createversionstringfrommodule-function.md)傳回）。  
  
 `ppCordb`  
 [out] COM 物件 (`IUnknown`) 指標的指標。 這個物件會在傳回之前轉換成[ICorDebug](icordebug-interface.md)物件。  
  
## <a name="return-value"></a>傳回值  
 S_OK  
 `ppCordb`參考實[ICorDebug 介面](icordebug-interface.md)介面的有效物件。  
  
 E_INVALIDARG  
 `szDebuggeeVersion` 或 `ppCordb` 為 null。  
  
 CORDBG_E_DEBUG_COMPONENT_MISSING  
 找不到 CLR 偵錯所需的元件。 這表示在目標 CoreCLR.dll 所在的相同目錄中找不到 mscordbi.dll 或 mscordaccore.dll。  
  
 CORDBG_E_INCOMPATIBLE_PROTOCOL  
 mscordbi.dll 或 mscordaccore.dll 的版本與目標 CoreCLR.dll 的版本不同。  
  
 E_FAIL (或其他 E_ 傳回碼)  
 無法傳回[ICorDebug 介面](icordebug-interface.md)。  
  
## <a name="remarks"></a>備註  
 傳回的介面提供了附加至目標處理序中的 CLR，以及對 CLR 正在執行之 Managed 程式碼進行偵錯的功能。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** dbgshim。h  
  
 連結**庫：** dbgshim  
  
 **.NET Framework 版本：** 3.5 SP1

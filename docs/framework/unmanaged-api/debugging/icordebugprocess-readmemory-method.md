---
title: ICorDebugProcess::ReadMemory 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ReadMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ReadMemory
helpviewer_keywords:
- ReadMemory method [.NET Framework debugging]
- ICorDebugProcess::ReadMemory method [.NET Framework debugging]
ms.assetid: 28e4b2f6-9589-445c-be24-24a3306795e7
topic_type:
- apiref
ms.openlocfilehash: a0abc7168ff7bffdbb835c1c1bc93de9df6e381c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95694863"
---
# <a name="icordebugprocessreadmemory-method"></a>ICorDebugProcess::ReadMemory 方法

讀取這個進程的指定記憶體區域。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT ReadMemory(  
    [in]  CORDB_ADDRESS address,
    [in]  DWORD size,  
    [out, size_is(size), length_is(size)] BYTE buffer[],  
    [out] SIZE_T *read);  
```  
  
## <a name="parameters"></a>參數  

 `address`  
 在 `CORDB_ADDRESS` 值，指定要讀取之記憶體的基底位址。  
  
 `size`  
 在要從記憶體讀取的位元組數目。  
  
 `buffer`  
 擴展接收記憶體內容的緩衝區。  
  
 `read`  
 擴展傳送至指定緩衝區的位元組數目指標。  
  
## <a name="remarks"></a>備註  

 `ReadMemory`方法主要是供 interop 偵錯工具用來檢查偵錯工具未受管理部分所使用的記憶體區域。 這個方法也可以用來讀取 Microsoft 中繼語言 (MSIL) 程式碼和原生 JIT 編譯的程式碼。  
  
 任何 managed 中斷點將會從參數中傳回的資料中移除 `buffer` 。 [ICorDebugProcess2：： SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md)所設定的原生中斷點不會進行任何調整。  
  
 不會執行進程記憶體的快取。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

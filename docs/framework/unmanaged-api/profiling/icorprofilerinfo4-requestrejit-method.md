---
title: ICorProfilerInfo4::RequestReJIT 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestReJIT
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestReJIT
helpviewer_keywords:
- RequestReJIT method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestReJIT method [.NET Framework profiling]
ms.assetid: 781ed736-f30c-4816-920e-3552e36542c6
topic_type:
- apiref
ms.openlocfilehash: 7dd82f2dfab885070df4789fe5efc16a49d50e06
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495797"
---
# <a name="icorprofilerinfo4requestrejit-method"></a>ICorProfilerInfo4::RequestReJIT 方法
要求指定函式的所有執行個體進行 JIT 重新編譯。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT RequestReJIT (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[]);  
```  
  
## <a name="parameters"></a>參數  
 `cFunctions`  
 [in] 要重新編譯的函式數目。  
  
 `moduleIds`  
 [in] 指定 (`module`, `methodDef`) 組的 `moduleId` 部分，這個部分可識別所要重新編譯的函式。  
  
 `methodIds`  
 [in] 指定 (`module`, `methodDef`) 組的 `methodId` 部分，這個部分可識別所要重新編譯的函式。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|已嘗試將所有方法標示為要進行 JIT 重新編譯。 分析工具必須執行[ICorProfilerCallback4：： ReJITError](icorprofilercallback4-rejiterror-method.md)方法，以判斷哪些方法已成功標示為要進行 JIT 重新編譯。|  
|CORPROF_E_CALLBACK4_REQUIRED|分析工具必須執行[ICorProfilerCallback4](icorprofilercallback4-interface.md)介面，才能支援此呼叫。|  
|CORPROF_E_REJIT_NOT_ENABLED|尚未啟用 JIT 重新編譯。 在初始化期間，您必須使用[ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md)方法來設定旗標，以啟用 JIT 重新編譯 `COR_PRF_ENABLE_REJIT` 。|  
|E_INVALIDARG|`cFunctions` 為 0，或者 `moduleIds` 或 `methodIds` 為 `NULL`。|  
|||  
|E_OUTOFMEMORY|CLR 無法完成要求，因為記憶體不足。|  
  
## <a name="remarks"></a>備註  
 呼叫 `RequestReJIT`，讓執行階段重新編譯所指定的一組函式。 然後，程式碼分析工具可以使用[ICorProfilerFunctionControl](icorprofilerfunctioncontrol-interface.md)介面來調整重新編譯函式時所產生的程式碼。 這不會影響目前正在執行的函式，只會影響未來的函式叫用。 如果所指定的任何函式先前已進行過 JIT 重新編譯，要求重新編譯就等於還原並重新編譯函式。 為了保留可反轉性，當 JIT 編譯器編譯函式的原始版本時，只會考慮其被呼叫端的原始版本來進行內嵌決策。 當 JIT 編譯器重新編譯函式時，它會考慮其被呼叫端的目前版本 (已重新編譯或原始) 來進行內嵌。  
  
 分析工具通常會呼叫 `RequestReJIT`，以回應要求分析工具檢測一或多個方法的使用者輸入。 `RequestReJIT` 通常會暫停執行階段，以執行某些工作，而且可能會觸發記憶體回收。 因此，分析工具應該從其先前建立的執行緒來呼叫 `RequestReJIT`，而不是從目前正在執行分析工具回呼的 CLR 建立的執行緒。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo4 介面](icorprofilerinfo4-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)

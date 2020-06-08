---
title: ICorProfilerInfo3::SetEnterLeaveFunctionHooks3 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.SetEnterLeaveFunctionHooks3 Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3
helpviewer_keywords:
- SetEnterLeaveFunctionHooks3 method [.NET Framework profiling]
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3 method [.NET Framework profiling]
ms.assetid: f0621465-b84f-40ab-a4e5-56a7abc776a7
topic_type:
- apiref
ms.openlocfilehash: eb658d682ce589b7dfdcfc0228d0c657310e6f7a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496229"
---
# <a name="icorprofilerinfo3setenterleavefunctionhooks3-method"></a>ICorProfilerInfo3::SetEnterLeaveFunctionHooks3 方法
指定將在[FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)和[FunctionTailcall3](functiontailcall3-function.md)函式上呼叫的分析工具所實函數。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetEnterLeaveFunctionHooks3(  
            [in] FunctionEnter3    *pFuncEnter3,  
            [in] FunctionLeave3    *pFuncLeave3,  
            [in] FunctionTailcall3 *pFuncTailcall3);  
```  
  
## <a name="parameters"></a>參數  
 `pFuncEnter3`  
 在要當做回呼使用的實作為指標 `FunctionEnter3` 。  
  
 `pFuncLeave3`  
 在要當做回呼使用的實作為指標 `FunctionLeave3` 。  
  
 `pFuncTailcall3`  
 在要當做回呼使用的實作為指標 `FunctionTailcall3` 。  
  
## <a name="remarks"></a>備註  
 [FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)和[FunctionTailcall3](functiontailcall3-function.md)勾點不提供堆疊框架和引數檢查。 若要存取該資訊， `COR_PRF_ENABLE_FUNCTION_ARGS` `COR_PRF_ENABLE_FUNCTION_RETVAL` 必須設定、和（或） `COR_PRF_ENABLE_FRAME_INFO` 旗標。 分析工具可以使用[ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md)方法來設定事件旗標，然後使用[ICorProfilerInfo3：： SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)方法來註冊此函式的實作為。  
  
 一次只能有一組回呼處於作用中狀態，而最新的版本會優先使用。 因此，如果 profiler 同時呼叫[SetEnterLeaveFunctionHooks2 方法](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)和 `SetEnterLeaveFunctionHooks3` 方法， `SetEnterLeaveFunctionHooks3` 就會使用。  
  
 `SetEnterLeaveFunctionHooks3`只能從分析工具的[ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md)回呼呼叫方法。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [分析全域靜態函式](profiling-global-static-functions.md)
- [ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)

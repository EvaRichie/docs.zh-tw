---
title: ICorProfilerInfo4::GetFunctionFromIP2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetFunctionFromIP2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2
helpviewer_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2 method [.NET Framework profiling]
- GetFunctionFromIP2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 46ff70f4-13e9-40a0-802a-0a40abcfc6a0
topic_type:
- apiref
ms.openlocfilehash: ea66474e809b3813faceef79a69dd8a639a72a3b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502791"
---
# <a name="icorprofilerinfo4getfunctionfromip2-method"></a>ICorProfilerInfo4::GetFunctionFromIP2 方法
將 managed 程式碼指令指標對應至 JIT 重新編譯的函式版本。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetFunctionFromIP2(  
    [in]  LPCBYTE    ip,  
    [out] FunctionID *pFunctionId,  
    [out] ReJITID *pReJitId);  
```  
  
## <a name="parameters"></a>參數  
 `ip`  
 在Managed 程式碼中的指令指標。  
  
 `pFunctionId`  
 脫銷函數識別碼。  
  
 `pReJitId`  
 脫銷函式之 JIT 重新編譯版本的識別。  
  
## <a name="remarks"></a>備註  
 `GetFunctionFromIP2`類似于 `GetFunctionFromIP` ，不同之處在于它會取得 JIT 重新編譯的識別碼，而不是包含指定之 IP 位址的函式的函數識別碼。  
  
> [!NOTE]
> `GetFunctionFromIP2`可以觸發垃圾收集，而 `GetFunctionFromIP` 則不會。  如需詳細資訊，請參閱[CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md)。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](icorprofilerinfo-interface.md)

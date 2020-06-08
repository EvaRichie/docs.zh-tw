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
# <a name="icorprofilerinfo4getfunctionfromip2-method"></a><span data-ttu-id="f5c36-102">ICorProfilerInfo4::GetFunctionFromIP2 方法</span><span class="sxs-lookup"><span data-stu-id="f5c36-102">ICorProfilerInfo4::GetFunctionFromIP2 Method</span></span>
<span data-ttu-id="f5c36-103">將 managed 程式碼指令指標對應至 JIT 重新編譯的函式版本。</span><span class="sxs-lookup"><span data-stu-id="f5c36-103">Maps a managed code instruction pointer to the JIT-recompiled version of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f5c36-104">語法</span><span class="sxs-lookup"><span data-stu-id="f5c36-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionFromIP2(  
    [in]  LPCBYTE    ip,  
    [out] FunctionID *pFunctionId,  
    [out] ReJITID *pReJitId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f5c36-105">參數</span><span class="sxs-lookup"><span data-stu-id="f5c36-105">Parameters</span></span>  
 `ip`  
 <span data-ttu-id="f5c36-106">在Managed 程式碼中的指令指標。</span><span class="sxs-lookup"><span data-stu-id="f5c36-106">[in] The instruction pointer in managed code.</span></span>  
  
 `pFunctionId`  
 <span data-ttu-id="f5c36-107">脫銷函數識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5c36-107">[out] The function ID.</span></span>  
  
 `pReJitId`  
 <span data-ttu-id="f5c36-108">脫銷函式之 JIT 重新編譯版本的識別。</span><span class="sxs-lookup"><span data-stu-id="f5c36-108">[out] The identity of the JIT-recompiled version of the function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f5c36-109">備註</span><span class="sxs-lookup"><span data-stu-id="f5c36-109">Remarks</span></span>  
 <span data-ttu-id="f5c36-110">`GetFunctionFromIP2`類似于 `GetFunctionFromIP` ，不同之處在于它會取得 JIT 重新編譯的識別碼，而不是包含指定之 IP 位址的函式的函數識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5c36-110">`GetFunctionFromIP2` is similar to `GetFunctionFromIP`, except that it gets the JIT-recompiled ID instead of the function ID of the function that contains the specified IP address.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f5c36-111">`GetFunctionFromIP2`可以觸發垃圾收集，而 `GetFunctionFromIP` 則不會。</span><span class="sxs-lookup"><span data-stu-id="f5c36-111">`GetFunctionFromIP2` can trigger a garbage collection, whereas `GetFunctionFromIP` will not.</span></span>  <span data-ttu-id="f5c36-112">如需詳細資訊，請參閱[CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md)。</span><span class="sxs-lookup"><span data-stu-id="f5c36-112">For more information, see [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f5c36-113">規格需求</span><span class="sxs-lookup"><span data-stu-id="f5c36-113">Requirements</span></span>  
 <span data-ttu-id="f5c36-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f5c36-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f5c36-115">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="f5c36-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="f5c36-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f5c36-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f5c36-117">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f5c36-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f5c36-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f5c36-118">See also</span></span>

- [<span data-ttu-id="f5c36-119">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="f5c36-119">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)

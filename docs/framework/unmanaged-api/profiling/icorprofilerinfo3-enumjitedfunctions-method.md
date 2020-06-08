---
title: ICorProfilerInfo3::EnumJITedFunctions 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.EnumJITedFunctions Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::EnumJITedFunctions
helpviewer_keywords:
- ICorProfilerInfo3::EnumJITedFunctions method [.NET Framework profiling]
- EnumJITedFunctions method [.NET Framework profiling]
ms.assetid: e2847a36-f460-45e2-9b6c-b33b008f40d9
topic_type:
- apiref
ms.openlocfilehash: 3ebf4a7706b3d3495e4a617b4f86a50281115436
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496551"
---
# <a name="icorprofilerinfo3enumjitedfunctions-method"></a><span data-ttu-id="8db0a-102">ICorProfilerInfo3::EnumJITedFunctions 方法</span><span class="sxs-lookup"><span data-stu-id="8db0a-102">ICorProfilerInfo3::EnumJITedFunctions Method</span></span>
<span data-ttu-id="8db0a-103">傳回先前已進行 JIT 編譯之所有函式的列舉值。</span><span class="sxs-lookup"><span data-stu-id="8db0a-103">Returns an enumerator for all functions that were previously JIT-compiled.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8db0a-104">語法</span><span class="sxs-lookup"><span data-stu-id="8db0a-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8db0a-105">參數</span><span class="sxs-lookup"><span data-stu-id="8db0a-105">Parameters</span></span>  
 `ppEnum`  
 <span data-ttu-id="8db0a-106">脫銷[ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)列舉值的指標。</span><span class="sxs-lookup"><span data-stu-id="8db0a-106">[out] A pointer to the [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) enumerator.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8db0a-107">備註</span><span class="sxs-lookup"><span data-stu-id="8db0a-107">Remarks</span></span>  
 <span data-ttu-id="8db0a-108">這個方法可能會與 `JITCompilation` 回呼（例如[ICorProfilerCallback：： JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)方法）重迭。</span><span class="sxs-lookup"><span data-stu-id="8db0a-108">This method may overlap with `JITCompilation` callbacks such as the [ICorProfilerCallback::JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) method.</span></span> <span data-ttu-id="8db0a-109">這個方法所傳回的列舉值不包含從 Ngen.exe 產生的原生映射載入的函式。</span><span class="sxs-lookup"><span data-stu-id="8db0a-109">The enumerator returned by this method does not include functions that are loaded from native images generated with Ngen.exe.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8db0a-110">傳回的列舉只包含 "0" 代表欄位的值 `COR_PRF_FUNCTION::reJitId` 。</span><span class="sxs-lookup"><span data-stu-id="8db0a-110">The returned enumeration includes only "0" for the value of the `COR_PRF_FUNCTION::reJitId` field.</span></span>  <span data-ttu-id="8db0a-111">如果您需要有效 `COR_PRF_FUNCTION::reJitId` 的值，請使用[ICorProfilerInfo4：： EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="8db0a-111">If you require valid `COR_PRF_FUNCTION::reJitId` values, use the [ICorProfilerInfo4::EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8db0a-112">規格需求</span><span class="sxs-lookup"><span data-stu-id="8db0a-112">Requirements</span></span>  
 <span data-ttu-id="8db0a-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8db0a-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8db0a-114">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="8db0a-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="8db0a-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="8db0a-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8db0a-116">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8db0a-116">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8db0a-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8db0a-117">See also</span></span>

- [<span data-ttu-id="8db0a-118">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="8db0a-118">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="8db0a-119">分析介面</span><span class="sxs-lookup"><span data-stu-id="8db0a-119">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="8db0a-120">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="8db0a-120">Profiling</span></span>](index.md)

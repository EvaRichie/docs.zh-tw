---
title: ICorProfilerInfo3::GetFunctionTailcall3Info 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetFunctionTailcall3Info Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetFunctionTailcall3Info
helpviewer_keywords:
- ICorProfilerInfo3::GetFunctionTailcall3Info method [.NET Framework profiling]
- GetFunctionTailcall3Info method [.NET Framework profiling]
ms.assetid: afdb5ac9-5bf5-4b91-b7cb-f81db23d7da3
topic_type:
- apiref
ms.openlocfilehash: e4d0d9ed07c707e51e5833483b71079f2c330505
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496525"
---
# <a name="icorprofilerinfo3getfunctiontailcall3info-method"></a><span data-ttu-id="17333-102">ICorProfilerInfo3::GetFunctionTailcall3Info 方法</span><span class="sxs-lookup"><span data-stu-id="17333-102">ICorProfilerInfo3::GetFunctionTailcall3Info Method</span></span>
<span data-ttu-id="17333-103">提供[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)函式向分析工具報告之函式的堆疊框架。</span><span class="sxs-lookup"><span data-stu-id="17333-103">Provides the stack frame of the function that is being reported to the profiler by the [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md) function.</span></span> <span data-ttu-id="17333-104">只能在 `FunctionTailcall3WithInfo` 回呼期間呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="17333-104">This method can be called only during the `FunctionTailcall3WithInfo` callback.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="17333-105">語法</span><span class="sxs-lookup"><span data-stu-id="17333-105">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionTailcall3Info(
            [in]  FunctionID functionId,
            [in]  COR_PRF_ELT_INFO eltInfo,  
            [out] COR_PRF_FRAME_INFO *pFrameInfo);  
```  
  
## <a name="parameters"></a><span data-ttu-id="17333-106">參數</span><span class="sxs-lookup"><span data-stu-id="17333-106">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="17333-107">在傳回之函式的 `FunctionID` 。</span><span class="sxs-lookup"><span data-stu-id="17333-107">[in] The `FunctionID` of the function that is returning.</span></span>  
  
 `eltInfo`  
 <span data-ttu-id="17333-108">[in] 代表特定堆疊框架之資訊的不透明控制代碼。</span><span class="sxs-lookup"><span data-stu-id="17333-108">[in] An opaque handle that represents information about a given stack frame.</span></span> <span data-ttu-id="17333-109">分析工具應提供函式所 `eltInfo` 指定給 profiler 的相同 `FunctionTailcall3WithInfo` 。</span><span class="sxs-lookup"><span data-stu-id="17333-109">The profiler should provide the same `eltInfo` that was given to the profiler by the `FunctionTailcall3WithInfo` function.</span></span>  
  
 `pFrameInfo`  
 <span data-ttu-id="17333-110">[out] 代表特定堆疊框架之泛型資訊的不透明控制代碼。</span><span class="sxs-lookup"><span data-stu-id="17333-110">[out] An opaque handle that represents generics information about a given stack frame.</span></span> <span data-ttu-id="17333-111">此控制代碼只有在程式碼剖析工具呼叫 `GetFunctionTailcall3Info` 方法的 `FunctionTailcall3WithInfo` 回呼中有效。</span><span class="sxs-lookup"><span data-stu-id="17333-111">This handle is valid only during the `FunctionTailcall3WithInfo` callback in which the profiler called the `GetFunctionTailcall3Info` method.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="17333-112">備註</span><span class="sxs-lookup"><span data-stu-id="17333-112">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="17333-113">需求</span><span class="sxs-lookup"><span data-stu-id="17333-113">Requirements</span></span>  
 <span data-ttu-id="17333-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="17333-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="17333-115">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="17333-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="17333-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="17333-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="17333-117">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="17333-117">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="17333-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="17333-118">See also</span></span>

- [<span data-ttu-id="17333-119">FunctionEnter3WithInfo</span><span class="sxs-lookup"><span data-stu-id="17333-119">FunctionEnter3WithInfo</span></span>](functionenter3withinfo-function.md)
- [<span data-ttu-id="17333-120">FunctionLeave3WithInfo</span><span class="sxs-lookup"><span data-stu-id="17333-120">FunctionLeave3WithInfo</span></span>](functionleave3withinfo-function.md)
- [<span data-ttu-id="17333-121">FunctionTailcall3WithInfo</span><span class="sxs-lookup"><span data-stu-id="17333-121">FunctionTailcall3WithInfo</span></span>](functiontailcall3withinfo-function.md)
- [<span data-ttu-id="17333-122">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="17333-122">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="17333-123">分析介面</span><span class="sxs-lookup"><span data-stu-id="17333-123">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="17333-124">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="17333-124">Profiling</span></span>](index.md)

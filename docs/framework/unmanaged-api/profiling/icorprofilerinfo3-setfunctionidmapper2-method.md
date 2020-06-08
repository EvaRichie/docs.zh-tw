---
title: ICorProfilerInfo3::SetFunctionIDMapper2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.SetFunctionIDMapper2 Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::SetFunctionIDMapper2
helpviewer_keywords:
- SetFunctionIDMapper2 method [.NET Framework profiling]
- ICorProfilerInfo3::SetFunctionIDMapper2 method [.NET Framework profiling]
ms.assetid: 8cdb1188-952a-4ba8-9f05-bfebc18cdd29
topic_type:
- apiref
ms.openlocfilehash: 723cb277a7df592e0494505018f7422e4e40f5f6
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496148"
---
# <a name="icorprofilerinfo3setfunctionidmapper2-method"></a><span data-ttu-id="67695-102">ICorProfilerInfo3::SetFunctionIDMapper2 方法</span><span class="sxs-lookup"><span data-stu-id="67695-102">ICorProfilerInfo3::SetFunctionIDMapper2 Method</span></span>
<span data-ttu-id="67695-103">指定將被呼叫來對應 `FunctionID` 值到替代值的程式碼剖析工具實作函式，這會被傳遞至分析工具函式進入/離開的攔截。</span><span class="sxs-lookup"><span data-stu-id="67695-103">Specifies the profiler-implemented function that will be called to map `FunctionID` values to alternative values, which are passed to the profiler's function entry/exit hooks.</span></span> <span data-ttu-id="67695-104">這個方法會以額外的資料參數擴充[ICorProfilerInfo：： SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)方法，而分析工具可能會使用它來區分執行時間。</span><span class="sxs-lookup"><span data-stu-id="67695-104">This method extends the [ICorProfilerInfo::SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md) method with an additional data parameter, which profilers may use to disambiguate among runtimes.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="67695-105">語法</span><span class="sxs-lookup"><span data-stu-id="67695-105">Syntax</span></span>  
  
```cpp  
HRESULT SetFunctionIDMapper2(  
       [in] FunctionIDMapper2 *pFunc,  
       [in] void *clientData);  
```  
  
## <a name="parameters"></a><span data-ttu-id="67695-106">參數</span><span class="sxs-lookup"><span data-stu-id="67695-106">Parameters</span></span>  
 `pFunc`  
 <span data-ttu-id="67695-107">在將呼叫以將[FunctionIDMapper2](functionidmapper2-function.md) `FunctionID` 值對應至其替代值的 FunctionIDMapper2 執行的指標。</span><span class="sxs-lookup"><span data-stu-id="67695-107">[in] A pointer to a [FunctionIDMapper2](functionidmapper2-function.md) implementation that will be called to map the `FunctionID` values to their alternative values.</span></span>  
  
 `clientData`  
 <span data-ttu-id="67695-108">在傳遞至目前執行時間所進行之每個[FunctionIDMapper2](functionidmapper2-function.md)函式呼叫的指標。</span><span class="sxs-lookup"><span data-stu-id="67695-108">[in] A pointer that is passed to every [FunctionIDMapper2](functionidmapper2-function.md) function call made by the current runtime.</span></span> <span data-ttu-id="67695-109">分析工具可以使用此資訊來區分執行時間。</span><span class="sxs-lookup"><span data-stu-id="67695-109">The profiler can use this information to disambiguate among runtimes.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="67695-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="67695-110">Return Value</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="67695-111">備註</span><span class="sxs-lookup"><span data-stu-id="67695-111">Remarks</span></span>  
 <span data-ttu-id="67695-112">FunctionID 值的替代專案會傳遞至分析工具的函式進入/結束攔截器（[FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)和[FunctionTailcall3](functiontailcall3-function.md) [; 或是 FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)和[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)），這是由[SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)或[SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)方法所指定。</span><span class="sxs-lookup"><span data-stu-id="67695-112">The alternatives for the FunctionID values will be passed to the profiler's function entry/exit hooks ([FunctionEnter3](functionenter3-function.md), [FunctionLeave3](functionleave3-function.md), and [FunctionTailcall3](functiontailcall3-function.md); or [FunctionEnter3WithInfo](functionenter3withinfo-function.md), [FunctionLeave3WithInfo](functionleave3withinfo-function.md), and [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)) that are specified by the [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md) or [SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) method.</span></span>  
  
 <span data-ttu-id="67695-113">`FunctionIDMapper2`方法只能設定一次，建議您在[ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md)回呼中加以設定。</span><span class="sxs-lookup"><span data-stu-id="67695-113">The `FunctionIDMapper2` method can be set only once; we recommend that you set it in the [ICorProfilerCallback::Initialize](icorprofilercallback-initialize-method.md) callback.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="67695-114">規格需求</span><span class="sxs-lookup"><span data-stu-id="67695-114">Requirements</span></span>  
 <span data-ttu-id="67695-115">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="67695-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="67695-116">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="67695-116">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="67695-117">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="67695-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="67695-118">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="67695-118">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="67695-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="67695-119">See also</span></span>

- [<span data-ttu-id="67695-120">SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="67695-120">SetFunctionIDMapper</span></span>](icorprofilerinfo-setfunctionidmapper-method.md)
- [<span data-ttu-id="67695-121">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="67695-121">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="67695-122">分析介面</span><span class="sxs-lookup"><span data-stu-id="67695-122">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="67695-123">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="67695-123">Profiling</span></span>](index.md)

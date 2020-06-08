---
title: FunctionIDMapper2 函式
ms.date: 03/30/2017
api_name:
- FunctionIDMapper2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionIDMapper2
helpviewer_keywords:
- FunctionIDMapper2 function [.NET Framework profiling]
ms.assetid: 466ad51b-8f0c-41d9-81f7-371aac3374cb
topic_type:
- apiref
ms.openlocfilehash: 65c5d2d4f288d927d79c233374edfec54c0b77ae
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500646"
---
# <a name="functionidmapper2-function"></a><span data-ttu-id="64b48-102">FunctionIDMapper2 函式</span><span class="sxs-lookup"><span data-stu-id="64b48-102">FunctionIDMapper2 Function</span></span>
<span data-ttu-id="64b48-103">通知分析工具，函式的指定識別碼可能會重新對應到替代識別碼，以便用於[FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)和[FunctionTailcall3](functiontailcall3-function.md)，或[FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)和[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)回呼（針對該函數）。</span><span class="sxs-lookup"><span data-stu-id="64b48-103">Notifies the profiler that the given identifier of a function may be remapped to an alternative ID to be used in the [FunctionEnter3](functionenter3-function.md), [FunctionLeave3](functionleave3-function.md), and [FunctionTailcall3](functiontailcall3-function.md), or[FunctionEnter3WithInfo](functionenter3withinfo-function.md), [FunctionLeave3WithInfo](functionleave3withinfo-function.md), and [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md) callbacks for that function.</span></span> <span data-ttu-id="64b48-104">`FunctionIDMapper2` 也可讓分析工具指出它是否要接收該函式的回呼。</span><span class="sxs-lookup"><span data-stu-id="64b48-104">`FunctionIDMapper2` also enables the profiler to indicate whether it wants to receive callbacks for that function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="64b48-105">語法</span><span class="sxs-lookup"><span data-stu-id="64b48-105">Syntax</span></span>  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper2 (  
    [in]  FunctionID  funcId,  
    [in]  void * clientData,  
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="64b48-106">參數</span><span class="sxs-lookup"><span data-stu-id="64b48-106">Parameters</span></span>

- `funcId`

  <span data-ttu-id="64b48-107">\[in] 要重新對應的函式識別碼。</span><span class="sxs-lookup"><span data-stu-id="64b48-107">\[in] The function identifier to be remapped.</span></span>

- `clientData`

  <span data-ttu-id="64b48-108">\[in] 用來區分執行時間之間的資料指標。</span><span class="sxs-lookup"><span data-stu-id="64b48-108">\[in] A pointer to data that is used to disambiguate among runtimes.</span></span>

- `pbHookFunction`

  <span data-ttu-id="64b48-109">\[out] 當分析工具 `true` 想要接收 `FunctionEnter3` 、 `FunctionLeave3` 、和、或、和回呼時，所設定的值指標 `FunctionTailcall3` `FunctionEnter3WithInfo` `FunctionLeave3WithInfo` `FunctionTailcall3WithInfo` ; 否則，它會將此值設定為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="64b48-109">\[out] A pointer to a value that the profiler sets to `true` if it wants to receive `FunctionEnter3`, `FunctionLeave3`, and `FunctionTailcall3`, or `FunctionEnter3WithInfo`, `FunctionLeave3WithInfo`, and `FunctionTailcall3WithInfo` callbacks; otherwise, it sets this value to `false`.</span></span>

## <a name="return-value"></a><span data-ttu-id="64b48-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="64b48-110">Return Value</span></span>  
 <span data-ttu-id="64b48-111">分析工具會傳回一個值，執行引擎會使用該值做為替代函式識別項。</span><span class="sxs-lookup"><span data-stu-id="64b48-111">The profiler returns a value that the execution engine uses as an alternative function identifier.</span></span> <span data-ttu-id="64b48-112">傳回值不可為 null，除非 `false` 傳回在 `pbHookFunction` 中。</span><span class="sxs-lookup"><span data-stu-id="64b48-112">The return value cannot be null unless `false` is returned in `pbHookFunction`.</span></span> <span data-ttu-id="64b48-113">否則，傳回的 null 值會產生無法預期的結果，包括可能暫止處理序。</span><span class="sxs-lookup"><span data-stu-id="64b48-113">Otherwise, a null return value produces unpredictable results, including possibly halting the process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="64b48-114">備註</span><span class="sxs-lookup"><span data-stu-id="64b48-114">Remarks</span></span>  
 <span data-ttu-id="64b48-115">這個方法會使用用來傳遞用戶端資料的額外參數來擴充[FunctionIDMapper](functionidmapper-function.md)函數。</span><span class="sxs-lookup"><span data-stu-id="64b48-115">This method extends the [FunctionIDMapper](functionidmapper-function.md) function with an additional parameter that is used to pass client data.</span></span> <span data-ttu-id="64b48-116">用戶端資料會用來區分執行階段。</span><span class="sxs-lookup"><span data-stu-id="64b48-116">The client data is used to disambiguate among runtimes.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="64b48-117">規格需求</span><span class="sxs-lookup"><span data-stu-id="64b48-117">Requirements</span></span>  
 <span data-ttu-id="64b48-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="64b48-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="64b48-119">**標頭：** Corprof.idl .idl</span><span class="sxs-lookup"><span data-stu-id="64b48-119">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="64b48-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="64b48-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="64b48-121">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="64b48-121">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="64b48-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64b48-122">See also</span></span>

- [<span data-ttu-id="64b48-123">ICorProfilerInfo::SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="64b48-123">ICorProfilerInfo::SetFunctionIDMapper</span></span>](icorprofilerinfo-setfunctionidmapper-method.md)
- [<span data-ttu-id="64b48-124">ICorProfilerInfo3::SetFunctionIDMapper2</span><span class="sxs-lookup"><span data-stu-id="64b48-124">ICorProfilerInfo3::SetFunctionIDMapper2</span></span>](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [<span data-ttu-id="64b48-125">FunctionEnter3</span><span class="sxs-lookup"><span data-stu-id="64b48-125">FunctionEnter3</span></span>](functionenter3-function.md)
- [<span data-ttu-id="64b48-126">FunctionLeave3</span><span class="sxs-lookup"><span data-stu-id="64b48-126">FunctionLeave3</span></span>](functionleave3-function.md)
- [<span data-ttu-id="64b48-127">FunctionTailcall3</span><span class="sxs-lookup"><span data-stu-id="64b48-127">FunctionTailcall3</span></span>](functiontailcall3-function.md)
- [<span data-ttu-id="64b48-128">FunctionEnter3WithInfo</span><span class="sxs-lookup"><span data-stu-id="64b48-128">FunctionEnter3WithInfo</span></span>](functionenter3withinfo-function.md)
- [<span data-ttu-id="64b48-129">FunctionLeave3WithInfo</span><span class="sxs-lookup"><span data-stu-id="64b48-129">FunctionLeave3WithInfo</span></span>](functionleave3withinfo-function.md)
- [<span data-ttu-id="64b48-130">FunctionTailcall3WithInfo</span><span class="sxs-lookup"><span data-stu-id="64b48-130">FunctionTailcall3WithInfo</span></span>](functiontailcall3withinfo-function.md)
- [<span data-ttu-id="64b48-131">分析全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="64b48-131">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)

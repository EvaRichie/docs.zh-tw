---
title: FunctionLeave 函式
ms.date: 03/30/2017
api_name:
- FunctionLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave
helpviewer_keywords:
- FunctionLeave function [.NET Framework profiling]
ms.assetid: 18e89f45-e068-426a-be16-9f53a4346860
topic_type:
- apiref
ms.openlocfilehash: 13636da9c3e8ac4aa9e8dc1fa02b2e33afef4717
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722254"
---
# <a name="functionleave-function"></a><span data-ttu-id="e22bd-102">FunctionLeave 函式</span><span class="sxs-lookup"><span data-stu-id="e22bd-102">FunctionLeave Function</span></span>

<span data-ttu-id="e22bd-103">通知分析工具，函式即將傳回到呼叫端。</span><span class="sxs-lookup"><span data-stu-id="e22bd-103">Notifies the profiler that a function is about to return to the caller.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e22bd-104">`FunctionLeave`函數在 .NET Framework 2.0 中已被取代。</span><span class="sxs-lookup"><span data-stu-id="e22bd-104">The `FunctionLeave` function is deprecated in the .NET Framework 2.0.</span></span> <span data-ttu-id="e22bd-105">它會繼續運作，但會導致效能下降。</span><span class="sxs-lookup"><span data-stu-id="e22bd-105">It will continue to work, but will incur a performance penalty.</span></span> <span data-ttu-id="e22bd-106">請改用 [FunctionLeave2](functionleave2-function.md) 函數。</span><span class="sxs-lookup"><span data-stu-id="e22bd-106">Use the [FunctionLeave2](functionleave2-function.md) function instead.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e22bd-107">語法</span><span class="sxs-lookup"><span data-stu-id="e22bd-107">Syntax</span></span>  
  
```cpp  
void __stdcall FunctionLeave (  
    [in] FunctionID funcID  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e22bd-108">參數</span><span class="sxs-lookup"><span data-stu-id="e22bd-108">Parameters</span></span>

- `funcID`

  <span data-ttu-id="e22bd-109">\[in] 傳回之函式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e22bd-109">\[in] The identifier of the function that is returning.</span></span>

## <a name="remarks"></a><span data-ttu-id="e22bd-110">備註</span><span class="sxs-lookup"><span data-stu-id="e22bd-110">Remarks</span></span>  

 <span data-ttu-id="e22bd-111">`FunctionLeave`函數是回呼; 您必須加以執行。</span><span class="sxs-lookup"><span data-stu-id="e22bd-111">The `FunctionLeave` function is a callback; you must implement it.</span></span> <span data-ttu-id="e22bd-112">實作為必須使用 `__declspec` (`naked`) 儲存類別屬性。</span><span class="sxs-lookup"><span data-stu-id="e22bd-112">The implementation must use the `__declspec`(`naked`) storage-class attribute.</span></span>  
  
 <span data-ttu-id="e22bd-113">在呼叫此函式之前，執行引擎不會儲存任何暫存器。</span><span class="sxs-lookup"><span data-stu-id="e22bd-113">The execution engine does not save any registers before calling this function.</span></span>  
  
- <span data-ttu-id="e22bd-114">輸入時，您必須儲存使用的所有暫存器，包括浮點數單位中的所有暫存器 (FPU) 。</span><span class="sxs-lookup"><span data-stu-id="e22bd-114">On entry, you must save all registers that you use, including those in the floating-point unit (FPU).</span></span>  
  
- <span data-ttu-id="e22bd-115">在結束時，您必須藉由關閉呼叫端所推送的所有參數來還原堆疊。</span><span class="sxs-lookup"><span data-stu-id="e22bd-115">On exit, you must restore the stack by popping off all the parameters that were pushed by its caller.</span></span>  
  
 <span data-ttu-id="e22bd-116">的執行 `FunctionLeave` 不應封鎖，因為它會延遲垃圾收集。</span><span class="sxs-lookup"><span data-stu-id="e22bd-116">The implementation of `FunctionLeave` should not block because it will delay garbage collection.</span></span> <span data-ttu-id="e22bd-117">執行不應嘗試垃圾收集，因為堆疊可能不是處於垃圾收集的易記狀態。</span><span class="sxs-lookup"><span data-stu-id="e22bd-117">The implementation should not attempt a garbage collection because the stack may not be in a garbage collection-friendly state.</span></span> <span data-ttu-id="e22bd-118">如果嘗試垃圾收集，則執行時間會封鎖直到傳回為止 `FunctionLeave` 。</span><span class="sxs-lookup"><span data-stu-id="e22bd-118">If a garbage collection is attempted, the runtime will block until `FunctionLeave` returns.</span></span>  
  
 <span data-ttu-id="e22bd-119">此外，此函式 `FunctionLeave` 不能呼叫 managed 程式碼，或以任何方式造成受控記憶體配置。</span><span class="sxs-lookup"><span data-stu-id="e22bd-119">Also, the `FunctionLeave` function must not call into managed code or in any way cause a managed memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e22bd-120">需求</span><span class="sxs-lookup"><span data-stu-id="e22bd-120">Requirements</span></span>  

 <span data-ttu-id="e22bd-121">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e22bd-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e22bd-122">**標頭：** Corprof.h .idl</span><span class="sxs-lookup"><span data-stu-id="e22bd-122">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="e22bd-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e22bd-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e22bd-124">**.NET Framework 版本：** 1.1、1。0</span><span class="sxs-lookup"><span data-stu-id="e22bd-124">**.NET Framework Versions:** 1.1, 1.0</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e22bd-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e22bd-125">See also</span></span>

- [<span data-ttu-id="e22bd-126">FunctionEnter2 函式</span><span class="sxs-lookup"><span data-stu-id="e22bd-126">FunctionEnter2 Function</span></span>](functionenter2-function.md)
- [<span data-ttu-id="e22bd-127">FunctionLeave2 函式</span><span class="sxs-lookup"><span data-stu-id="e22bd-127">FunctionLeave2 Function</span></span>](functionleave2-function.md)
- [<span data-ttu-id="e22bd-128">FunctionTailcall2 函式</span><span class="sxs-lookup"><span data-stu-id="e22bd-128">FunctionTailcall2 Function</span></span>](functiontailcall2-function.md)
- [<span data-ttu-id="e22bd-129">SetEnterLeaveFunctionHooks2 方法</span><span class="sxs-lookup"><span data-stu-id="e22bd-129">SetEnterLeaveFunctionHooks2 Method</span></span>](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [<span data-ttu-id="e22bd-130">分析全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="e22bd-130">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)

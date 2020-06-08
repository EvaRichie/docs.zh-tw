---
title: ICorProfilerCallback::JITCompilationStarted 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCompilationStarted
helpviewer_keywords:
- JITCompilationStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCompilationStarted method [.NET Framework profiling]
ms.assetid: 31782b36-d311-4518-8f45-25f65385af5b
topic_type:
- apiref
ms.openlocfilehash: 57981ef134dc3f30337d47f5cee426a25d0414cf
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500035"
---
# <a name="icorprofilercallbackjitcompilationstarted-method"></a><span data-ttu-id="6439e-102">ICorProfilerCallback::JITCompilationStarted 方法</span><span class="sxs-lookup"><span data-stu-id="6439e-102">ICorProfilerCallback::JITCompilationStarted Method</span></span>
<span data-ttu-id="6439e-103">通知分析工具，及時（JIT）編譯器已開始編譯函式。</span><span class="sxs-lookup"><span data-stu-id="6439e-103">Notifies the profiler that the just-in-time (JIT) compiler has started to compile a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6439e-104">語法</span><span class="sxs-lookup"><span data-stu-id="6439e-104">Syntax</span></span>  
  
```cpp  
HRESULT JITCompilationStarted(  
    [in] FunctionID functionId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6439e-105">參數</span><span class="sxs-lookup"><span data-stu-id="6439e-105">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="6439e-106">在正在啟動編譯之函式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6439e-106">[in] The ID of the function for which the compilation is starting.</span></span>  
  
 `fIsSafeToBlock`  
 <span data-ttu-id="6439e-107">在值，表示封鎖器是否會影響執行時間的作業。</span><span class="sxs-lookup"><span data-stu-id="6439e-107">[in] A value indicating to the profiler whether blocking will affect the operation of the runtime.</span></span> <span data-ttu-id="6439e-108">`true`如果封鎖可能會導致執行時間等候呼叫執行緒從這個回呼傳回，則值為，否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="6439e-108">The value is `true` if blocking may cause the runtime to wait for the calling thread to return from this callback; otherwise, `false`.</span></span>  
  
 <span data-ttu-id="6439e-109">雖然的值 `true` 不會傷害執行時間，但它可能會扭曲分析結果。</span><span class="sxs-lookup"><span data-stu-id="6439e-109">Although a value of `true` will not harm the runtime, it can skew the profiling results.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6439e-110">備註</span><span class="sxs-lookup"><span data-stu-id="6439e-110">Remarks</span></span>  
 <span data-ttu-id="6439e-111">您可以針對每個函式接收一對以上的 `JITCompilationStarted` 和[ICorProfilerCallback：： JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md)呼叫，因為執行時間處理類別的函式的方式。</span><span class="sxs-lookup"><span data-stu-id="6439e-111">It is possible to receive more than one pair of `JITCompilationStarted` and [ICorProfilerCallback::JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md) calls for each function because of the way the runtime handles class constructors.</span></span> <span data-ttu-id="6439e-112">例如，執行時間會開始 JIT 編譯方法 A，但必須執行類別 B 的類別構造函式。</span><span class="sxs-lookup"><span data-stu-id="6439e-112">For example, the runtime starts to JIT-compile method A, but the class constructor for class B needs to be run.</span></span> <span data-ttu-id="6439e-113">因此，執行時間會 JIT 編譯類別 B 的函式，並加以執行。</span><span class="sxs-lookup"><span data-stu-id="6439e-113">Therefore, the runtime JIT-compiles the constructor for class B and runs it.</span></span> <span data-ttu-id="6439e-114">當此函式正在執行時，它會呼叫方法 A，使方法 A 再次進行 JIT 編譯。</span><span class="sxs-lookup"><span data-stu-id="6439e-114">While the constructor is running, it makes a call to method A, which causes method A to be JIT-compiled again.</span></span> <span data-ttu-id="6439e-115">在此案例中，方法 A 的第一個 JIT 編譯會暫停。</span><span class="sxs-lookup"><span data-stu-id="6439e-115">In this scenario, the first JIT compilation of method A is halted.</span></span> <span data-ttu-id="6439e-116">不過，這兩次嘗試 JIT 編譯方法 A 都會使用 JIT 編譯事件來回報。</span><span class="sxs-lookup"><span data-stu-id="6439e-116">However, both attempts to JIT-compile method A are reported with JIT-compilation events.</span></span> <span data-ttu-id="6439e-117">如果分析工具會藉由呼叫[ICorProfilerInfo：： SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md)方法，來取代方法 A 的 Microsoft 中繼語言（MSIL）程式碼，則這兩個事件都必須這麼做，但這兩者 `JITCompilationStarted` 可能會同時使用相同的 MSIL 區塊。</span><span class="sxs-lookup"><span data-stu-id="6439e-117">If the profiler is going to replace Microsoft intermediate language (MSIL) code for method A by calling the [ICorProfilerInfo::SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md) method, it must do so for both `JITCompilationStarted` events, but it may use the same MSIL block for both.</span></span>  
  
 <span data-ttu-id="6439e-118">分析工具在兩個執行緒同時進行回呼的情況下，必須支援 JIT 回呼的順序。</span><span class="sxs-lookup"><span data-stu-id="6439e-118">Profilers must support the sequence of JIT callbacks in cases where two threads are simultaneously making callbacks.</span></span> <span data-ttu-id="6439e-119">例如，執行緒 A 會呼叫 `JITCompilationStarted` 。</span><span class="sxs-lookup"><span data-stu-id="6439e-119">For example, thread A calls `JITCompilationStarted`.</span></span> <span data-ttu-id="6439e-120">不過，線上程 A 呼叫之前 `JITCompilationFinished` ，執行緒 B 會呼叫[ICorProfilerCallback：： ExceptionSearchFunctionEnter](icorprofilercallback-exceptionsearchfunctionenter-method.md)與執行緒 a 的回呼的函式識別碼 `JITCompilationStarted` 。</span><span class="sxs-lookup"><span data-stu-id="6439e-120">However, before thread A calls `JITCompilationFinished`, thread B calls [ICorProfilerCallback::ExceptionSearchFunctionEnter](icorprofilercallback-exceptionsearchfunctionenter-method.md) with the function ID from thread A's `JITCompilationStarted` callback.</span></span> <span data-ttu-id="6439e-121">可能會出現函式識別碼尚未生效的情況，因為程式碼剖析工具尚未收到的呼叫 `JITCompilationFinished` 。</span><span class="sxs-lookup"><span data-stu-id="6439e-121">It might appear that the function ID should not yet be valid because a call to `JITCompilationFinished` had not yet been received by the profiler.</span></span> <span data-ttu-id="6439e-122">不過，在這種情況下，函數識別碼是有效的。</span><span class="sxs-lookup"><span data-stu-id="6439e-122">However, in a case like this one, the function ID is valid.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6439e-123">規格需求</span><span class="sxs-lookup"><span data-stu-id="6439e-123">Requirements</span></span>  
 <span data-ttu-id="6439e-124">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6439e-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6439e-125">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="6439e-125">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="6439e-126">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6439e-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6439e-127">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6439e-127">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6439e-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6439e-128">See also</span></span>

- [<span data-ttu-id="6439e-129">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="6439e-129">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="6439e-130">JITCompilationFinished 方法</span><span class="sxs-lookup"><span data-stu-id="6439e-130">JITCompilationFinished Method</span></span>](icorprofilercallback-jitcompilationfinished-method.md)

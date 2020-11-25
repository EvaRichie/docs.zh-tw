---
title: ICorProfilerCallback3 介面
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3
helpviewer_keywords:
- ICorProfilerCallback3 interface [.NET Framework profiling]
ms.assetid: be83af41-3dec-4c77-8529-9dd6b8042af6
topic_type:
- apiref
ms.openlocfilehash: fd482bfe8e95a53cafd1530c88f09df146a1b150
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729430"
---
# <a name="icorprofilercallback3-interface"></a><span data-ttu-id="29f54-102">ICorProfilerCallback3 介面</span><span class="sxs-lookup"><span data-stu-id="29f54-102">ICorProfilerCallback3 Interface</span></span>

<span data-ttu-id="29f54-103">提供 common language runtime (CLR) 用來將附加和卸離狀態資訊傳達給 profiler 的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="29f54-103">Provides callback methods that the common language runtime (CLR) uses to communicate attach and detach state information to the profiler.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="29f54-104">方法</span><span class="sxs-lookup"><span data-stu-id="29f54-104">Methods</span></span>  
  
|<span data-ttu-id="29f54-105">方法</span><span class="sxs-lookup"><span data-stu-id="29f54-105">Method</span></span>|<span data-ttu-id="29f54-106">描述</span><span class="sxs-lookup"><span data-stu-id="29f54-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="29f54-107">InitializeForAttach 方法</span><span class="sxs-lookup"><span data-stu-id="29f54-107">InitializeForAttach Method</span></span>](icorprofilercallback3-initializeforattach-method.md)|<span data-ttu-id="29f54-108">由 CLR 呼叫，讓分析工具在附加作業之後有機會初始化其狀態。</span><span class="sxs-lookup"><span data-stu-id="29f54-108">Called by the CLR to give the profiler an opportunity to initialize its state after an attach operation.</span></span>|  
|[<span data-ttu-id="29f54-109">ProfilerAttachComplete 方法</span><span class="sxs-lookup"><span data-stu-id="29f54-109">ProfilerAttachComplete Method</span></span>](icorprofilercallback3-profilerattachcomplete-method.md)|<span data-ttu-id="29f54-110">由 CLR 呼叫以指出分析工具現在可以呼叫 catch 方法。</span><span class="sxs-lookup"><span data-stu-id="29f54-110">Called by the CLR to indicate that the profiler can now call the catch-up methods.</span></span>|  
|[<span data-ttu-id="29f54-111">ProfilerDetachSucceeded 方法</span><span class="sxs-lookup"><span data-stu-id="29f54-111">ProfilerDetachSucceeded Method</span></span>](icorprofilercallback3-profilerdetachsucceeded-method.md)|<span data-ttu-id="29f54-112">通知分析工具 Common Language Runtime (CLR) 即將卸載分析工具 DLL。</span><span class="sxs-lookup"><span data-stu-id="29f54-112">Notifies the profiler that the common language runtime (CLR) is about to unload the profiler DLL.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="29f54-113">備註</span><span class="sxs-lookup"><span data-stu-id="29f54-113">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="29f54-114">需求</span><span class="sxs-lookup"><span data-stu-id="29f54-114">Requirements</span></span>  

 <span data-ttu-id="29f54-115">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="29f54-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="29f54-116">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="29f54-116">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="29f54-117">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="29f54-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="29f54-118">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="29f54-118">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="29f54-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="29f54-119">See also</span></span>

- [<span data-ttu-id="29f54-120">分析介面</span><span class="sxs-lookup"><span data-stu-id="29f54-120">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="29f54-121">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="29f54-121">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="29f54-122">ICorProfilerCallback2 介面</span><span class="sxs-lookup"><span data-stu-id="29f54-122">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)
- [<span data-ttu-id="29f54-123">ICorProfilerCallback4 介面</span><span class="sxs-lookup"><span data-stu-id="29f54-123">ICorProfilerCallback4 Interface</span></span>](icorprofilercallback4-interface.md)

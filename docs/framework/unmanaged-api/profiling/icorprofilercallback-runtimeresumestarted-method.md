---
title: ICorProfilerCallback::RuntimeResumeStarted 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeResumeStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeResumeStarted
helpviewer_keywords:
- ICorProfilerCallback::RuntimeResumeStarted method [.NET Framework profiling]
- RuntimeResumeStarted method [.NET Framework profiling]
ms.assetid: 5854bfb2-c568-4f19-904a-7c9d41e7b995
topic_type:
- apiref
ms.openlocfilehash: 9a283d305c1a19112574cbf3486b1c67e64ed24c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717219"
---
# <a name="icorprofilercallbackruntimeresumestarted-method"></a><span data-ttu-id="bbdac-102">ICorProfilerCallback::RuntimeResumeStarted 方法</span><span class="sxs-lookup"><span data-stu-id="bbdac-102">ICorProfilerCallback::RuntimeResumeStarted Method</span></span>

<span data-ttu-id="bbdac-103">通知分析工具，執行時間正在繼續所有運行時間表程。</span><span class="sxs-lookup"><span data-stu-id="bbdac-103">Notifies the profiler that the runtime is resuming all run-time threads.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bbdac-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="bbdac-104">Syntax</span></span>  
  
```cpp  
HRESULT RuntimeResumeStarted();  
```  
  
## <a name="requirements"></a><span data-ttu-id="bbdac-105">需求</span><span class="sxs-lookup"><span data-stu-id="bbdac-105">Requirements</span></span>  

 <span data-ttu-id="bbdac-106">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdac-106">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bbdac-107">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="bbdac-107">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="bbdac-108">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="bbdac-108">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="bbdac-109">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="bbdac-109">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bbdac-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bbdac-110">See also</span></span>

- [<span data-ttu-id="bbdac-111">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="bbdac-111">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="bbdac-112">RuntimeResumeFinished 方法</span><span class="sxs-lookup"><span data-stu-id="bbdac-112">RuntimeResumeFinished Method</span></span>](icorprofilercallback-runtimeresumefinished-method.md)

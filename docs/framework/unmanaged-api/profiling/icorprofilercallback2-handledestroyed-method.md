---
title: ICorProfilerCallback2::HandleDestroyed 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.HandleDestroyed
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::HandleDestroyed
helpviewer_keywords:
- ICorProfilerCallback2::HandleDestroyed method [.NET Framework profiling]
- HandleDestroyed method [.NET Framework profiling]
ms.assetid: ab4f4bbd-40c7-4667-bfde-60cd73803110
topic_type:
- apiref
ms.openlocfilehash: d7a4f7d08e6d8698dbb58c4c2d111a47d0ccc8db
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499775"
---
# <a name="icorprofilercallback2handledestroyed-method"></a><span data-ttu-id="a5c24-102">ICorProfilerCallback2::HandleDestroyed 方法</span><span class="sxs-lookup"><span data-stu-id="a5c24-102">ICorProfilerCallback2::HandleDestroyed Method</span></span>
<span data-ttu-id="a5c24-103">通知程式碼分析工具，垃圾收集控制碼已遭終結。</span><span class="sxs-lookup"><span data-stu-id="a5c24-103">Notifies the code profiler that a garbage collection handle has been destroyed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a5c24-104">語法</span><span class="sxs-lookup"><span data-stu-id="a5c24-104">Syntax</span></span>  
  
```cpp  
HRESULT HandleDestroyed(  
    [in] GCHandleID handleId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a5c24-105">參數</span><span class="sxs-lookup"><span data-stu-id="a5c24-105">Parameters</span></span>  
 `handleId`  
 <span data-ttu-id="a5c24-106">在垃圾收集的控制碼識別碼。</span><span class="sxs-lookup"><span data-stu-id="a5c24-106">[in] The ID of the handle for the garbage collection.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a5c24-107">規格需求</span><span class="sxs-lookup"><span data-stu-id="a5c24-107">Requirements</span></span>  
 <span data-ttu-id="a5c24-108">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a5c24-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a5c24-109">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="a5c24-109">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="a5c24-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a5c24-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a5c24-111">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a5c24-111">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a5c24-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a5c24-112">See also</span></span>

- [<span data-ttu-id="a5c24-113">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="a5c24-113">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="a5c24-114">ICorProfilerCallback2 介面</span><span class="sxs-lookup"><span data-stu-id="a5c24-114">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)

---
title: ICorProfilerCallback::ExceptionSearchFilterLeave 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionSearchFilterLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionSearchFilterLeave
helpviewer_keywords:
- ICorProfilerCallback::ExceptionSearchFilterLeave method [.NET Framework profiling]
- ExceptionSearchFilterLeave method [.NET Framework profiling]
ms.assetid: c28a2a82-dd11-4385-843f-b509fb61753b
topic_type:
- apiref
ms.openlocfilehash: fbece20701fbde5551e025b4f116f9873abf444d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500204"
---
# <a name="icorprofilercallbackexceptionsearchfilterleave-method"></a><span data-ttu-id="13fd1-102">ICorProfilerCallback::ExceptionSearchFilterLeave 方法</span><span class="sxs-lookup"><span data-stu-id="13fd1-102">ICorProfilerCallback::ExceptionSearchFilterLeave Method</span></span>
<span data-ttu-id="13fd1-103">通知分析工具，使用者篩選器已完成執行。</span><span class="sxs-lookup"><span data-stu-id="13fd1-103">Notifies the profiler that a user filter has just finished executing.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="13fd1-104">語法</span><span class="sxs-lookup"><span data-stu-id="13fd1-104">Syntax</span></span>  
  
```cpp  
HRESULT ExceptionSearchFilterLeave();  
```  
  
## <a name="requirements"></a><span data-ttu-id="13fd1-105">規格需求</span><span class="sxs-lookup"><span data-stu-id="13fd1-105">Requirements</span></span>  
 <span data-ttu-id="13fd1-106">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="13fd1-106">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="13fd1-107">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="13fd1-107">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="13fd1-108">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="13fd1-108">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="13fd1-109">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="13fd1-109">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13fd1-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13fd1-110">See also</span></span>

- [<span data-ttu-id="13fd1-111">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="13fd1-111">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="13fd1-112">ExceptionSearchFilterEnter 方法</span><span class="sxs-lookup"><span data-stu-id="13fd1-112">ExceptionSearchFilterEnter Method</span></span>](icorprofilercallback-exceptionsearchfilterenter-method.md)

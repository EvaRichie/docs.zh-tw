---
title: ICorProfilerFunctionEnum::GetCount 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum.GetCount Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum::GetCount
helpviewer_keywords:
- ICorProfilerFunctionEnum::GetCount method [.NET Framework profiling]
- GetCount method, ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 62ec65e3-3e9d-400b-ae61-d24b8963995b
topic_type:
- apiref
ms.openlocfilehash: 137b1da853535985b2fd383d52f0bcfc48f728ed
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503090"
---
# <a name="icorprofilerfunctionenumgetcount-method"></a><span data-ttu-id="e14ed-102">ICorProfilerFunctionEnum::GetCount 方法</span><span class="sxs-lookup"><span data-stu-id="e14ed-102">ICorProfilerFunctionEnum::GetCount Method</span></span>
<span data-ttu-id="e14ed-103">取得應用程式已載入的或分析工具強制載入的函式數目。</span><span class="sxs-lookup"><span data-stu-id="e14ed-103">Gets the number of functions that were loaded by the application or forcibly loaded by the profiler.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e14ed-104">語法</span><span class="sxs-lookup"><span data-stu-id="e14ed-104">Syntax</span></span>  
  
```cpp  
HRESULT GetCount([out] ULONG * pcelt);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e14ed-105">參數</span><span class="sxs-lookup"><span data-stu-id="e14ed-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="e14ed-106">脫銷已載入的函式數目。</span><span class="sxs-lookup"><span data-stu-id="e14ed-106">[out] The number of functions that were loaded.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e14ed-107">規格需求</span><span class="sxs-lookup"><span data-stu-id="e14ed-107">Requirements</span></span>  
 <span data-ttu-id="e14ed-108">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e14ed-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e14ed-109">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="e14ed-109">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="e14ed-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e14ed-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e14ed-111">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e14ed-111">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e14ed-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e14ed-112">See also</span></span>

- [<span data-ttu-id="e14ed-113">ICorProfilerFunctionEnum 介面</span><span class="sxs-lookup"><span data-stu-id="e14ed-113">ICorProfilerFunctionEnum Interface</span></span>](icorprofilerfunctionenum-interface.md)
- [<span data-ttu-id="e14ed-114">分析介面</span><span class="sxs-lookup"><span data-stu-id="e14ed-114">Profiling Interfaces</span></span>](profiling-interfaces.md)

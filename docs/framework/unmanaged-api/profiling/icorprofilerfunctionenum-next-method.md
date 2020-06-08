---
title: ICorProfilerFunctionEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum.Next Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum::Next
helpviewer_keywords:
- ICorProfilerFunctionEnum::Next method [.NET Framework profiling]
- Next method, ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 5ed4aa83-ce56-4b9f-9237-5da7587787fe
topic_type:
- apiref
ms.openlocfilehash: df62ad1af0ea91783cb62bb0590b6e36d812de3a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503064"
---
# <a name="icorprofilerfunctionenumnext-method"></a><span data-ttu-id="80446-102">ICorProfilerFunctionEnum::Next 方法</span><span class="sxs-lookup"><span data-stu-id="80446-102">ICorProfilerFunctionEnum::Next Method</span></span>
<span data-ttu-id="80446-103">從循序函式集合中取得指定的連續函式數目，從序列中列舉值的目前位置開始。</span><span class="sxs-lookup"><span data-stu-id="80446-103">Gets the specified number of contiguous functions from a sequential collection of functions, starting at the enumerator's current position in the sequence.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="80446-104">語法</span><span class="sxs-lookup"><span data-stu-id="80446-104">Syntax</span></span>  
  
```cpp  
HRESULT Next([in]  ULONG      celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                    COR_PRF_FUNCTION ids[],  
             [out] ULONG *   pceltFetched);  
```  
  
## <a name="parameters"></a><span data-ttu-id="80446-105">參數</span><span class="sxs-lookup"><span data-stu-id="80446-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="80446-106">[in] 要擷取的函式數目。</span><span class="sxs-lookup"><span data-stu-id="80446-106">[in] The number of functions to retrieve.</span></span>  
  
 `ids`  
 <span data-ttu-id="80446-107">[out] `COR_PRF_FUNCTION` 值的陣列，每個值各代表一個擷取的函式。</span><span class="sxs-lookup"><span data-stu-id="80446-107">[out] An array of `COR_PRF_FUNCTION` values, each of which represents a retrieved function.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="80446-108">[out] `ids` 陣列中實際傳回之函式數目的指標。</span><span class="sxs-lookup"><span data-stu-id="80446-108">[out] A pointer to the number of functions actually returned in the `ids` array.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="80446-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="80446-109">Return Value</span></span>  
 <span data-ttu-id="80446-110">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="80446-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="80446-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="80446-111">HRESULT</span></span>|<span data-ttu-id="80446-112">說明</span><span class="sxs-lookup"><span data-stu-id="80446-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="80446-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="80446-113">S_OK</span></span>|<span data-ttu-id="80446-114">已傳回 `celt` 項目。</span><span class="sxs-lookup"><span data-stu-id="80446-114">`celt` elements were returned.</span></span>|  
|<span data-ttu-id="80446-115">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="80446-115">S_FALSE</span></span>|<span data-ttu-id="80446-116">傳回少於 `celt` 的項目數，表示列舉已完成。</span><span class="sxs-lookup"><span data-stu-id="80446-116">Fewer than `celt` elements were returned, which indicates that the enumeration is complete.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="80446-117">規格需求</span><span class="sxs-lookup"><span data-stu-id="80446-117">Requirements</span></span>  
 <span data-ttu-id="80446-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="80446-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="80446-119">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="80446-119">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="80446-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="80446-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="80446-121">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="80446-121">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="80446-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80446-122">See also</span></span>

- [<span data-ttu-id="80446-123">ICorProfilerFunctionEnum 介面</span><span class="sxs-lookup"><span data-stu-id="80446-123">ICorProfilerFunctionEnum Interface</span></span>](icorprofilerfunctionenum-interface.md)
- [<span data-ttu-id="80446-124">分析介面</span><span class="sxs-lookup"><span data-stu-id="80446-124">Profiling Interfaces</span></span>](profiling-interfaces.md)

---
title: ICorProfilerThreadEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum::Next
helpviewer_keywords:
- ICorProfilerThreadEnum::Next method [.NET Framework profiling]
- Next method, ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: f3535279-3c63-41a2-ab0e-a129dc5a01e8
topic_type:
- apiref
ms.openlocfilehash: 37d1acfa70a1a2b2c18fb34fb5d6024f3b61e2ab
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494341"
---
# <a name="icorprofilerthreadenumnext-method"></a><span data-ttu-id="c8e7c-102">ICorProfilerThreadEnum::Next 方法</span><span class="sxs-lookup"><span data-stu-id="c8e7c-102">ICorProfilerThreadEnum::Next Method</span></span>
<span data-ttu-id="c8e7c-103">從循序執行緒集合中取得指定的連續執行緒數目，從序列中列舉值的目前位置開始。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-103">Gets the specified number of contiguous threads from a sequential collection of threads, starting at the enumerator's current position in the sequence.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c8e7c-104">語法</span><span class="sxs-lookup"><span data-stu-id="c8e7c-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (    [in]  ULONG      celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
                    ThreadID ids[],  
    [out] ULONG *   pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c8e7c-105">參數</span><span class="sxs-lookup"><span data-stu-id="c8e7c-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="c8e7c-106">[in] 要擷取的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-106">[in] The number of threads to retrieve.</span></span>  
  
 `ids`  
 <span data-ttu-id="c8e7c-107">[out] `ThreadID` 值的陣列，每個值各代表一個擷取的執行緒。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-107">[out] An array of `ThreadID` values, each of which represents a retrieved thread.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="c8e7c-108">[out] `ids` 陣列中實際傳回之執行緒數目的指標。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-108">[out] A pointer to the number of threads actually returned in the `ids` array.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c8e7c-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="c8e7c-109">Return Value</span></span>  
 <span data-ttu-id="c8e7c-110">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="c8e7c-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="c8e7c-111">HRESULT</span></span>|<span data-ttu-id="c8e7c-112">說明</span><span class="sxs-lookup"><span data-stu-id="c8e7c-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="c8e7c-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="c8e7c-113">S_OK</span></span>|<span data-ttu-id="c8e7c-114">已傳回 `celt` 項目。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-114">`celt` elements were returned.</span></span>|  
|<span data-ttu-id="c8e7c-115">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="c8e7c-115">S_FALSE</span></span>|<span data-ttu-id="c8e7c-116">傳回少於 `celt` 的項目數，表示列舉已完成。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-116">Fewer than `celt` elements were returned, which indicates that the enumeration is complete.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c8e7c-117">規格需求</span><span class="sxs-lookup"><span data-stu-id="c8e7c-117">Requirements</span></span>  
 <span data-ttu-id="c8e7c-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c8e7c-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c8e7c-119">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="c8e7c-119">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="c8e7c-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c8e7c-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c8e7c-121">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c8e7c-121">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c8e7c-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c8e7c-122">See also</span></span>

- [<span data-ttu-id="c8e7c-123">ICorProfilerThreadEnum 介面</span><span class="sxs-lookup"><span data-stu-id="c8e7c-123">ICorProfilerThreadEnum Interface</span></span>](icorprofilerthreadenum-interface.md)
- [<span data-ttu-id="c8e7c-124">分析介面</span><span class="sxs-lookup"><span data-stu-id="c8e7c-124">Profiling Interfaces</span></span>](profiling-interfaces.md)

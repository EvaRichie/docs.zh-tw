---
title: ICorProfilerInfo7：： GetInMemorySymbolsLength 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.GetInMemorySymbolsLength
api_location:
- mscorwks.dll
- icorprof.idl
api_type:
- COM
ms.assetid: d62c4a4c-8a62-45aa-8f01-a8387cf36159
ms.openlocfilehash: 43d6bdeae5f522bd73b0bdf3a5c403ec69ee384c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495434"
---
# <a name="icorprofilerinfo7getinmemorysymbolslength-method"></a><span data-ttu-id="761ab-102">ICorProfilerInfo7：： GetInMemorySymbolsLength 方法</span><span class="sxs-lookup"><span data-stu-id="761ab-102">ICorProfilerInfo7::GetInMemorySymbolsLength Method</span></span>
<span data-ttu-id="761ab-103">[在 .NET Framework 4.6.1 及更新版本中支援]</span><span class="sxs-lookup"><span data-stu-id="761ab-103">[Supported in the .NET Framework 4.6.1 and later versions]</span></span>  
  
 <span data-ttu-id="761ab-104">傳回記憶體中符號資料流程的長度。</span><span class="sxs-lookup"><span data-stu-id="761ab-104">Returns the length of an in-memory symbol stream.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="761ab-105">語法</span><span class="sxs-lookup"><span data-stu-id="761ab-105">Syntax</span></span>  
  
```cpp  
HRESULT GetInMemorySymbolsLength(  
        [in] ModuleID moduleId,  
        [out] DWORD* pCountSymbolBytes  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="761ab-106">參數</span><span class="sxs-lookup"><span data-stu-id="761ab-106">Parameters</span></span>  
 `moduleId`  
 <span data-ttu-id="761ab-107">在包含記憶體中資料流程之模組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="761ab-107">[in] The identifier of the module containing the in-memory stream.</span></span>  
  
 <span data-ttu-id="761ab-108">pCountSymbolBytes</span><span class="sxs-lookup"><span data-stu-id="761ab-108">pCountSymbolBytes</span></span>  
 <span data-ttu-id="761ab-109">脫銷`DWORD`值的指標，當方法傳回時，會包含資料流程的長度（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="761ab-109">[out] A pointer to a `DWORD` value that, when the method returns, contains the length of the stream in bytes.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="761ab-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="761ab-110">Return Value</span></span>  
 <span data-ttu-id="761ab-111">`S_OK`如果可以判斷記憶體資料流程的長度，則此方法會傳回，即使它是零（0）也一樣。</span><span class="sxs-lookup"><span data-stu-id="761ab-111">The method returns `S_OK` if the length of the memory stream can be determined, even if it is zero (0).</span></span>  
  
 <span data-ttu-id="761ab-112">`CORPROF_E_MODULE_IS_DYNAMIC`如果方法是使用建立的，則方法會傳回 <xref:System.Reflection.Emit?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="761ab-112">The method returns `CORPROF_E_MODULE_IS_DYNAMIC` if the method was created using <xref:System.Reflection.Emit?displayProperty=nameWithType>.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="761ab-113">備註</span><span class="sxs-lookup"><span data-stu-id="761ab-113">Remarks</span></span>  
 <span data-ttu-id="761ab-114">如果模組具有記憶體中的符號，資料流程的長度會放在中 `pCountSymbolBytes` 。</span><span class="sxs-lookup"><span data-stu-id="761ab-114">If the module has in-memory symbols, the length of the stream is placed in `pCountSymbolBytes`.</span></span> <span data-ttu-id="761ab-115">如果模組沒有記憶體中的符號，則為 `*pCountSymbolBytes = 0` 。</span><span class="sxs-lookup"><span data-stu-id="761ab-115">If the module doesn't have in-memory     symbols, `*pCountSymbolBytes = 0`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="761ab-116">目前的執行不支援反映。發出。</span><span class="sxs-lookup"><span data-stu-id="761ab-116">The current implementation does not support Reflection.Emit.</span></span> <span data-ttu-id="761ab-117">如果模組是使用反映所建立，則方法會傳回 `CORPROF_E_MODULE_IS_DYNAMIC` 。</span><span class="sxs-lookup"><span data-stu-id="761ab-117">If the module was created by using Reflection.Emit, the method returns `CORPROF_E_MODULE_IS_DYNAMIC`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="761ab-118">規格需求</span><span class="sxs-lookup"><span data-stu-id="761ab-118">Requirements</span></span>  
 <span data-ttu-id="761ab-119">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="761ab-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="761ab-120">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="761ab-120">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="761ab-121">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="761ab-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="761ab-122">**.NET Framework 版本：**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="761ab-122">**.NET Framework Versions:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="761ab-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="761ab-123">See also</span></span>

- [<span data-ttu-id="761ab-124">ICorProfilerInfo7 介面</span><span class="sxs-lookup"><span data-stu-id="761ab-124">ICorProfilerInfo7 Interface</span></span>](icorprofilerinfo7-interface.md)

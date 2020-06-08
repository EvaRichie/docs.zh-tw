---
title: ICorProfilerInfo::GetILToNativeMapping 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetILToNativeMapping
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorProfilerInfo interface [.NET Framework profiling]
- ICorProfilerInfo::GetILToNativeMapping method [.NET Framework profiling]
ms.assetid: 6a5431ef-22fb-4e53-bac5-703986297eb1
topic_type:
- apiref
ms.openlocfilehash: b3c0bee44bf49c7966b8fefcfe6460c6255375c5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502986"
---
# <a name="icorprofilerinfogetiltonativemapping-method"></a><span data-ttu-id="e1f2d-102">ICorProfilerInfo::GetILToNativeMapping 方法</span><span class="sxs-lookup"><span data-stu-id="e1f2d-102">ICorProfilerInfo::GetILToNativeMapping Method</span></span>
<span data-ttu-id="e1f2d-103">針對指定的函式中所包含的程式碼，取得從 Microsoft Intermediate Language (MSIL) 位移到原生位移的對應。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-103">Gets a map from Microsoft intermediate language (MSIL) offsets to native offsets for the code contained in the specified function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e1f2d-104">語法</span><span class="sxs-lookup"><span data-stu-id="e1f2d-104">Syntax</span></span>  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e1f2d-105">參數</span><span class="sxs-lookup"><span data-stu-id="e1f2d-105">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="e1f2d-106">[in] 包含程式碼的函式 ID。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-106">[in] The ID of the function that contains the code.</span></span>  
  
 `cMap`  
 <span data-ttu-id="e1f2d-107">[in] `map` 陣列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-107">[in] The maximum size of the `map` array.</span></span>  
  
 `pcMap`  
 <span data-ttu-id="e1f2d-108">[out] 可用的 COR_DEBUG_IL_TO_NATIVE_MAP 結構總數。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-108">[out] The total number of available COR_DEBUG_IL_TO_NATIVE_MAP structures.</span></span>  
  
 `map`  
 <span data-ttu-id="e1f2d-109">[out] `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的陣列，每個結構都有指定位移。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-109">[out] An array of `COR_DEBUG_IL_TO_NATIVE_MAP` structures, each of which specifies the offsets.</span></span> <span data-ttu-id="e1f2d-110">`GetILToNativeMapping` 方法傳回之後，`map` 將會包含部分或所有 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-110">After the `GetILToNativeMapping` method returns, `map` will contain some or all of the `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e1f2d-111">備註</span><span class="sxs-lookup"><span data-stu-id="e1f2d-111">Remarks</span></span>  
 <span data-ttu-id="e1f2d-112">`GetILToNativeMapping` 方法會傳回 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的陣列。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-112">The `GetILToNativeMapping` method returns an array of `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span> <span data-ttu-id="e1f2d-113">為了傳達原生指令的特定範圍對應至程式碼的特殊區域（例如初構），陣列中的專案可以 `ilOffset` 將其欄位設定為[CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md)列舉的值。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-113">To convey that certain ranges of native instructions correspond to special regions of code (for example, the prolog), an entry in the array can have its `ilOffset` field set to a value of the [CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md) enumeration.</span></span>  
  
 <span data-ttu-id="e1f2d-114">`GetILToNativeMapping` 傳回之後，您必須確認 `map` 緩衝區夠大，可以包含所有 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-114">After `GetILToNativeMapping` returns, you must verify that the `map` buffer was large enough to contain all the `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span> <span data-ttu-id="e1f2d-115">若要這樣做，請比較 `cMap` 的值與 `pcMap` 參數的值。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-115">To do this, compare the value of `cMap` with the value of the `pcMap` parameter.</span></span> <span data-ttu-id="e1f2d-116">如果 `pcMap` 值乘以 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的大小之後大於 `cMap`，請配置較大的 `map` 緩衝區，以新的較大大小更新 `cMap`，然後重新呼叫 `GetILToNativeMapping`。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-116">If the `pcMap` value, when it is multiplied by the size of a `COR_DEBUG_IL_TO_NATIVE_MAP` structure, is larger than `cMap`, allocate a larger `map` buffer, update `cMap` with the new, larger size, and call `GetILToNativeMapping` again.</span></span>  
  
 <span data-ttu-id="e1f2d-117">或者，您也可以先使用長度為零的 `map` 緩衝區來呼叫 `GetILToNativeMapping`，以取得正確的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-117">Alternatively, you can first call `GetILToNativeMapping` with a zero-length `map` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="e1f2d-118">接著您就可以將緩衝區大小設定為 `pcMap` 中傳回的值，並再次呼叫 `GetILToNativeMapping`。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-118">You can then set the buffer size to the value returned in `pcMap` and call `GetILToNativeMapping` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e1f2d-119">規格需求</span><span class="sxs-lookup"><span data-stu-id="e1f2d-119">Requirements</span></span>  
 <span data-ttu-id="e1f2d-120">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f2d-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e1f2d-121">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="e1f2d-121">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="e1f2d-122">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e1f2d-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e1f2d-123">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e1f2d-123">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e1f2d-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1f2d-124">See also</span></span>

- [<span data-ttu-id="e1f2d-125">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="e1f2d-125">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="e1f2d-126">GetILToNativeMapping2 方法</span><span class="sxs-lookup"><span data-stu-id="e1f2d-126">GetILToNativeMapping2 Method</span></span>](icorprofilerinfo4-getiltonativemapping2-method.md)
- [<span data-ttu-id="e1f2d-127">分析介面</span><span class="sxs-lookup"><span data-stu-id="e1f2d-127">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="e1f2d-128">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="e1f2d-128">Profiling</span></span>](index.md)

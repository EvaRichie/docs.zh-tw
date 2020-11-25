---
title: ICorProfilerInfo4::GetILToNativeMapping2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetILToNativeMapping2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2
helpviewer_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2 method [.NET Framework profiling]
- GetILToNativeMapping2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 756c1c25-08a7-4060-9798-dbeaa2f3bee5
topic_type:
- apiref
ms.openlocfilehash: 37d6b6d5112089df18fb138086db5e138a69629c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95697749"
---
# <a name="icorprofilerinfo4getiltonativemapping2-method"></a><span data-ttu-id="0e445-102">ICorProfilerInfo4::GetILToNativeMapping2 方法</span><span class="sxs-lookup"><span data-stu-id="0e445-102">ICorProfilerInfo4::GetILToNativeMapping2 Method</span></span>

<span data-ttu-id="0e445-103">針對指定函式的 JIT 重新編譯版本中所包含的程式碼，取得從 Microsoft Intermediate Language (MSIL) 位移到原生位移的對應。</span><span class="sxs-lookup"><span data-stu-id="0e445-103">Gets a map from Microsoft intermediate language (MSIL) offsets to native offsets for the code contained in the JIT-recompiled version of the specified function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0e445-104">語法</span><span class="sxs-lookup"><span data-stu-id="0e445-104">Syntax</span></span>  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ReJITID reJitId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="0e445-105">參數</span><span class="sxs-lookup"><span data-stu-id="0e445-105">Parameters</span></span>  

 `functionId`  
 <span data-ttu-id="0e445-106">[in] 包含程式碼的函式 ID。</span><span class="sxs-lookup"><span data-stu-id="0e445-106">[in] The ID of the function that contains the code.</span></span>  
  
 `pReJitId`  
 <span data-ttu-id="0e445-107">[in] 經過 JIT 重新編譯的函式識別。</span><span class="sxs-lookup"><span data-stu-id="0e445-107">[in] The identity of the JIT-recompiled function.</span></span> <span data-ttu-id="0e445-108">.NET Framework 4.5 中的身分識別必須為零。</span><span class="sxs-lookup"><span data-stu-id="0e445-108">The identity must be zero in the .NET Framework 4.5.</span></span>  
  
 `cMap`  
 <span data-ttu-id="0e445-109">[in] `map` 陣列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="0e445-109">[in] The maximum size of the `map` array.</span></span>  
  
 `pcMap`  
 <span data-ttu-id="0e445-110">[out] 可用的 COR_DEBUG_IL_TO_NATIVE_MAP 結構總數。</span><span class="sxs-lookup"><span data-stu-id="0e445-110">[out] The total number of available COR_DEBUG_IL_TO_NATIVE_MAP structures.</span></span>  
  
 `map`  
 <span data-ttu-id="0e445-111">[out] `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的陣列，每個結構都有指定位移。</span><span class="sxs-lookup"><span data-stu-id="0e445-111">[out] An array of `COR_DEBUG_IL_TO_NATIVE_MAP` structures, each of which specifies the offsets.</span></span> <span data-ttu-id="0e445-112">`GetILToNativeMapping2` 方法傳回之後，`map` 將會包含部分或所有 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構。</span><span class="sxs-lookup"><span data-stu-id="0e445-112">After the `GetILToNativeMapping2` method returns, `map` will contain some or all of the `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0e445-113">備註</span><span class="sxs-lookup"><span data-stu-id="0e445-113">Remarks</span></span>  

 <span data-ttu-id="0e445-114">`GetILToNativeMapping2` 類似于 [ICorProfilerInfo：： GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md) 方法，不同之處在于它可讓分析工具在未來的版本中指定重新編譯的函式識別碼。</span><span class="sxs-lookup"><span data-stu-id="0e445-114">`GetILToNativeMapping2` is similar to the [ICorProfilerInfo::GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md) method, except that it will allow the profiler to specify the ID of the recompiled function in future releases.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0e445-115">[ICorProfilerFunctionControl：： SetILInstrumentedCodeMap](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)方法未在 .NET Framework 4.5 中執行，因此已 JIT 重新編譯的函式不能有與原始編譯函式不同的 IL 對原生對應。</span><span class="sxs-lookup"><span data-stu-id="0e445-115">The [ICorProfilerFunctionControl::SetILInstrumentedCodeMap](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md) method is not implemented in the .NET Framework 4.5, so functions that have been JIT-recompiled cannot have an IL-to-native mapping that differs from the originally compiled function.</span></span> <span data-ttu-id="0e445-116">因此， `GetILToNativeMapping2` 在 .NET Framework 4.5 中，無法使用非零的 JIT 重新編譯識別碼來呼叫。</span><span class="sxs-lookup"><span data-stu-id="0e445-116">As such, `GetILToNativeMapping2` cannot be called with a nonzero JIT-recompiled ID in the .NET Framework 4.5.</span></span>  
  
 <span data-ttu-id="0e445-117">`GetILToNativeMapping2` 方法會傳回 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的陣列。</span><span class="sxs-lookup"><span data-stu-id="0e445-117">The `GetILToNativeMapping2` method returns an array of `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span> <span data-ttu-id="0e445-118">為了傳達原生指令的特定範圍對應至程式碼的特殊區域 (例如，初構) ，陣列中的專案可以 `ilOffset` 將其欄位設定為 [CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md) 列舉的值。</span><span class="sxs-lookup"><span data-stu-id="0e445-118">To convey that certain ranges of native instructions correspond to special regions of code (for example, the prolog), an entry in the array can have its `ilOffset` field set to a value of the [CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md) enumeration.</span></span>  
  
 <span data-ttu-id="0e445-119">`GetILToNativeMapping2` 傳回之後，您必須確認 `map` 緩衝區夠大，可以包含所有 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構。</span><span class="sxs-lookup"><span data-stu-id="0e445-119">After `GetILToNativeMapping2` returns, you must verify that the `map` buffer was large enough to contain all the `COR_DEBUG_IL_TO_NATIVE_MAP` structures.</span></span> <span data-ttu-id="0e445-120">若要這樣做，請比較 `cMap` 的值與 `pcMap` 參數的值。</span><span class="sxs-lookup"><span data-stu-id="0e445-120">To do this, compare the value of `cMap` with the value of the `pcMap` parameter.</span></span> <span data-ttu-id="0e445-121">如果 `pcMap` 值乘以 `COR_DEBUG_IL_TO_NATIVE_MAP` 結構的大小之後大於 `cMap`，請配置較大的 `map` 緩衝區，以新的較大大小更新 `cMap`，然後重新呼叫 `GetILToNativeMapping2`。</span><span class="sxs-lookup"><span data-stu-id="0e445-121">If the `pcMap` value, when it is multiplied by the size of a `COR_DEBUG_IL_TO_NATIVE_MAP` structure, is larger than `cMap`, allocate a larger `map` buffer, update `cMap` with the new, larger size, and call `GetILToNativeMapping2` again.</span></span>  
  
 <span data-ttu-id="0e445-122">或者，您也可以先使用長度為零的 `map` 緩衝區來呼叫 `GetILToNativeMapping2`，以取得正確的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="0e445-122">Alternatively, you can first call `GetILToNativeMapping2` with a zero-length `map` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="0e445-123">接著您就可以將緩衝區大小設定為 `pcMap` 中傳回的值，並再次呼叫 `GetILToNativeMapping2`。</span><span class="sxs-lookup"><span data-stu-id="0e445-123">You can then set the buffer size to the value returned in `pcMap` and call `GetILToNativeMapping2` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0e445-124">需求</span><span class="sxs-lookup"><span data-stu-id="0e445-124">Requirements</span></span>  

 <span data-ttu-id="0e445-125">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0e445-126">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="0e445-126">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="0e445-127">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="0e445-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="0e445-128">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0e445-128">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0e445-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0e445-129">See also</span></span>

- [<span data-ttu-id="0e445-130">GetILToNativeMapping 方法</span><span class="sxs-lookup"><span data-stu-id="0e445-130">GetILToNativeMapping Method</span></span>](icorprofilerinfo-getiltonativemapping-method.md)
- [<span data-ttu-id="0e445-131">ICorProfilerInfo4 介面</span><span class="sxs-lookup"><span data-stu-id="0e445-131">ICorProfilerInfo4 Interface</span></span>](icorprofilerinfo4-interface.md)
- [<span data-ttu-id="0e445-132">分析介面</span><span class="sxs-lookup"><span data-stu-id="0e445-132">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="0e445-133">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="0e445-133">Profiling</span></span>](index.md)

---
title: ICorProfilerInfo2::GetFunctionInfo2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionInfo2
helpviewer_keywords:
- GetFunctionInfo2 method [.NET Framework profiling]
- ICorProfilerInfo2::GetFunctionInfo2 method [.NET Framework profiling]
ms.assetid: 0aa60f24-8bbd-4c83-83c5-86ad191b1d82
topic_type:
- apiref
ms.openlocfilehash: f5438ddc655f0f6a7c11d978a47b1bf9e2a13059
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496998"
---
# <a name="icorprofilerinfo2getfunctioninfo2-method"></a><span data-ttu-id="6cf33-102">ICorProfilerInfo2::GetFunctionInfo2 方法</span><span class="sxs-lookup"><span data-stu-id="6cf33-102">ICorProfilerInfo2::GetFunctionInfo2 Method</span></span>
<span data-ttu-id="6cf33-103">取得函式的父類別、中繼資料語彙基元和每個類型引數的 `ClassID` (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="6cf33-103">Gets the parent class, the metadata token, and the `ClassID` of each type argument, if present, of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6cf33-104">語法</span><span class="sxs-lookup"><span data-stu-id="6cf33-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionInfo2(  
    [in]  FunctionID funcId,  
    [in]  COR_PRF_FRAME_INFO frameInfo,  
    [out] ClassID *pClassId,  
    [out] ModuleID *pModuleId,  
    [out] mdToken *pToken,  
    [in]  ULONG32 cTypeArgs,  
    [out] ULONG32 *pcTypeArgs,  
    [out] ClassID typeArgs[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6cf33-105">參數</span><span class="sxs-lookup"><span data-stu-id="6cf33-105">Parameters</span></span>  
 `funcId`  
 <span data-ttu-id="6cf33-106">[in] 用來取得父類別和其他資訊的函式 ID。</span><span class="sxs-lookup"><span data-stu-id="6cf33-106">[in] The ID of the function for which to get the parent class and other information.</span></span>  
  
 `frameInfo`  
 <span data-ttu-id="6cf33-107">[in] 指向堆疊框架相關資訊的 `COR_PRF_FRAME_INFO` 值。</span><span class="sxs-lookup"><span data-stu-id="6cf33-107">[in] A `COR_PRF_FRAME_INFO` value that points to information about a stack frame.</span></span>  
  
 `pClassId`  
 <span data-ttu-id="6cf33-108">[out] 函式父類別的指標。</span><span class="sxs-lookup"><span data-stu-id="6cf33-108">[out] A pointer to the parent class of the function.</span></span>  
  
 `pModuleId`  
 <span data-ttu-id="6cf33-109">[out] 定義函式父類別的模組指標。</span><span class="sxs-lookup"><span data-stu-id="6cf33-109">[out] A pointer to the module in which the function's parent class is defined.</span></span>  
  
 `pToken`  
 <span data-ttu-id="6cf33-110">[out] 此函式中繼資料語彙基元的指標。</span><span class="sxs-lookup"><span data-stu-id="6cf33-110">[out] A pointer to the metadata token for the function.</span></span>  
  
 `cTypeArgs`  
 <span data-ttu-id="6cf33-111">[in] `typeArgs` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="6cf33-111">[in] The size of the `typeArgs` array.</span></span>  
  
 `pcTypeArgs`  
 <span data-ttu-id="6cf33-112">[out] `ClassID` 值總數的指標。</span><span class="sxs-lookup"><span data-stu-id="6cf33-112">[out] A pointer to the total number of `ClassID` values.</span></span>  
  
 `typeArgs`  
 <span data-ttu-id="6cf33-113">[out] 一組 `ClassID`  值的陣列，其中每一項為該函式型別引數的 ID。</span><span class="sxs-lookup"><span data-stu-id="6cf33-113">[out] An array of `ClassID` values, each of which is the ID of a type argument of the function.</span></span> <span data-ttu-id="6cf33-114">方法傳回時， `typeArgs` 將包含部分或所有的 `ClassID` 值。</span><span class="sxs-lookup"><span data-stu-id="6cf33-114">When the method returns, `typeArgs` will contain some or all of the `ClassID` values.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6cf33-115">備註</span><span class="sxs-lookup"><span data-stu-id="6cf33-115">Remarks</span></span>  
 <span data-ttu-id="6cf33-116">分析工具程式碼可以呼叫[ICorProfilerInfo：： GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md)來取得給定模組的[中繼資料](../metadata/index.md)介面。</span><span class="sxs-lookup"><span data-stu-id="6cf33-116">The profiler code can call [ICorProfilerInfo::GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) to obtain a [metadata](../metadata/index.md) interface for a given module.</span></span> <span data-ttu-id="6cf33-117">然後，傳回至 `pToken` 所參考位置的中繼資料語彙基元可以用來存取此函式的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6cf33-117">The metadata token that is returned to the location referenced by `pToken` can then be used to access the metadata for the function.</span></span>  
  
 <span data-ttu-id="6cf33-118">透過 `pClassId` 和 `typeArgs` 參數傳回的類別 ID 與類型引數取決於在 `frameInfo` 參數中傳遞的值，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="6cf33-118">The class ID and type arguments that are returned through the `pClassId` and `typeArgs` parameters depend on the value that is passed in the `frameInfo` parameter, as shown in the following table.</span></span>  
  
|<span data-ttu-id="6cf33-119">`frameInfo` 參數的值</span><span class="sxs-lookup"><span data-stu-id="6cf33-119">Value of the `frameInfo` parameter</span></span>|<span data-ttu-id="6cf33-120">結果</span><span class="sxs-lookup"><span data-stu-id="6cf33-120">Result</span></span>|  
|----------------------------------------|------------|  
|<span data-ttu-id="6cf33-121">從 `COR_PRF_FRAME_INFO` 回呼取得的 `FunctionEnter2` 值</span><span class="sxs-lookup"><span data-stu-id="6cf33-121">A `COR_PRF_FRAME_INFO` value that was obtained from a `FunctionEnter2` callback</span></span>|<span data-ttu-id="6cf33-122">在 `pClassId` 所參考位置中傳回的 `ClassID` 和 `typeArgs` 陣列傳回的所有類型引數，都會是精確的。</span><span class="sxs-lookup"><span data-stu-id="6cf33-122">The `ClassID`, returned in the location referenced by `pClassId`, and all type arguments, returned in the `typeArgs` array, will be exact.</span></span>|  
|<span data-ttu-id="6cf33-123">從 `FunctionEnter2` 回呼以外來源取得的 `COR_PRF_FRAME_INFO`。</span><span class="sxs-lookup"><span data-stu-id="6cf33-123">A `COR_PRF_FRAME_INFO` that was obtained from a source other than a `FunctionEnter2` callback</span></span>|<span data-ttu-id="6cf33-124">無法決定精確的 `ClassID` 和類型引數。</span><span class="sxs-lookup"><span data-stu-id="6cf33-124">The exact `ClassID` and type arguments cannot be determined.</span></span> <span data-ttu-id="6cf33-125">也就是說，`ClassID` 可能是 null，而且可能會傳回某些類型引數做為 <xref:System.Object>。</span><span class="sxs-lookup"><span data-stu-id="6cf33-125">That is, the `ClassID` might be null and some type arguments might come back as <xref:System.Object>.</span></span>|  
|<span data-ttu-id="6cf33-126">零</span><span class="sxs-lookup"><span data-stu-id="6cf33-126">Zero</span></span>|<span data-ttu-id="6cf33-127">無法決定精確的 `ClassID` 和類型引數。</span><span class="sxs-lookup"><span data-stu-id="6cf33-127">The exact `ClassID` and type arguments cannot be determined.</span></span> <span data-ttu-id="6cf33-128">也就是說，`ClassID` 可能是 null，而且可能會傳回某些類型引數做為 <xref:System.Object>。</span><span class="sxs-lookup"><span data-stu-id="6cf33-128">That is, the `ClassID` might be null and some type arguments might come back as <xref:System.Object>.</span></span>|  
  
 <span data-ttu-id="6cf33-129">`GetFunctionInfo2` 傳回之後，您必須確認 `typeArgs` 緩衝區夠大，以包含所有 `ClassID` 的值。</span><span class="sxs-lookup"><span data-stu-id="6cf33-129">After `GetFunctionInfo2` returns, you must verify that the `typeArgs` buffer was large enough to contain all the `ClassID` values.</span></span> <span data-ttu-id="6cf33-130">若要這樣做，請比對 `pcTypeArgs` 指向的值和 `cTypeArgs` 參數。</span><span class="sxs-lookup"><span data-stu-id="6cf33-130">To do this, compare the value that `pcTypeArgs` points to with the value of the `cTypeArgs` parameter.</span></span> <span data-ttu-id="6cf33-131">如果 `pcTypeArgs` 指向一個值，該值大於 `cTypeArgs` 除以 `ClassID` 值的大小，請配置較大的 `pcTypeArgs` 緩衝區，以新的、較大的大小來更新 `cTypeArgs`，然後再呼叫 `GetFunctionInfo2` 一次。</span><span class="sxs-lookup"><span data-stu-id="6cf33-131">If `pcTypeArgs` points to a value that is larger than `cTypeArgs` divided by the size of a `ClassID` value, allocate a larger `pcTypeArgs` buffer, update `cTypeArgs` with the new, larger size, and call `GetFunctionInfo2` again.</span></span>  
  
 <span data-ttu-id="6cf33-132">或者，您也可以先使用長度為零的 `pcTypeArgs` 緩衝區來呼叫 `GetFunctionInfo2`，以取得正確的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="6cf33-132">Alternatively, you can first call `GetFunctionInfo2` with a zero-length `pcTypeArgs` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="6cf33-133">您可以將緩衝區大小設定為 `pcTypeArgs` 傳回的值除以 `ClassID` 值的大小，然後再呼叫 `GetFunctionInfo2` 一次。</span><span class="sxs-lookup"><span data-stu-id="6cf33-133">You can then set the buffer size to the value returned in `pcTypeArgs` divided by the size of a `ClassID` value, and call `GetFunctionInfo2` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6cf33-134">規格需求</span><span class="sxs-lookup"><span data-stu-id="6cf33-134">Requirements</span></span>  
 <span data-ttu-id="6cf33-135">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6cf33-135">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6cf33-136">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="6cf33-136">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="6cf33-137">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6cf33-137">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6cf33-138">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6cf33-138">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6cf33-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6cf33-139">See also</span></span>

- [<span data-ttu-id="6cf33-140">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="6cf33-140">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="6cf33-141">ICorProfilerInfo2 介面</span><span class="sxs-lookup"><span data-stu-id="6cf33-141">ICorProfilerInfo2 Interface</span></span>](icorprofilerinfo2-interface.md)
- [<span data-ttu-id="6cf33-142">分析介面</span><span class="sxs-lookup"><span data-stu-id="6cf33-142">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="6cf33-143">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="6cf33-143">Profiling</span></span>](index.md)

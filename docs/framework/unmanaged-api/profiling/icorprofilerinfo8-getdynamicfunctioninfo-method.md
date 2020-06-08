---
title: ICorProfilerInfo8::GetDynamicFunctionInfo
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.GetDynamicFunctionInfo
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: eaf33f3b0de7a18e400cd16d29c046784e2e190f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495316"
---
# <a name="icorprofilerinfo8getdynamicfunctioninfo-method"></a><span data-ttu-id="a525b-102">ICorProfilerInfo8：： GetDynamicFunctionInfo 方法</span><span class="sxs-lookup"><span data-stu-id="a525b-102">ICorProfilerInfo8::GetDynamicFunctionInfo Method</span></span>

<span data-ttu-id="a525b-103">抓取動態方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a525b-103">Retrieves information about dynamic methods.</span></span>

## <a name="syntax"></a><span data-ttu-id="a525b-104">語法</span><span class="sxs-lookup"><span data-stu-id="a525b-104">Syntax</span></span>

```cpp
HRESULT GetDynamicFunctionInfo( [in]  FunctionID              functionId,
                                [out] ModuleID                *moduleId,
                                [out] PCCOR_SIGNATURE         *ppvSig,
                                [out] ULONG                   *pbSig,
                                [in]  ULONG                   cchName,
                                [out] ULONG                   *pcchName,
                                [out] WCHAR                   wszName[]);
```

## <a name="parameters"></a><span data-ttu-id="a525b-105">參數</span><span class="sxs-lookup"><span data-stu-id="a525b-105">Parameters</span></span>

- `functionId`

  <span data-ttu-id="a525b-106">\[in] 要取得其資訊的函式識別碼。</span><span class="sxs-lookup"><span data-stu-id="a525b-106">\[in] The ID of the function for which to retrieve information.</span></span>

- `moduleId`

  <span data-ttu-id="a525b-107">\[in] 定義函式之父類別所在模組的指標。</span><span class="sxs-lookup"><span data-stu-id="a525b-107">\[in] A pointer to the module in which the function's parent class is defined.</span></span>

- `ppvSig`

  <span data-ttu-id="a525b-108">\[out] 函式簽章的指標。</span><span class="sxs-lookup"><span data-stu-id="a525b-108">\[out] A pointer to the signature for the function.</span></span>

- `pbSig`

  <span data-ttu-id="a525b-109">\[out] 函式簽章的位元組計數指標。</span><span class="sxs-lookup"><span data-stu-id="a525b-109">\[out] A pointer to the count of bytes for the function signature.</span></span>

- `cchName`

  <span data-ttu-id="a525b-110">\[in] 陣列的大小上限 `wszName` 。</span><span class="sxs-lookup"><span data-stu-id="a525b-110">\[in] The maximum size of the `wszName` array.</span></span>

- `pcchName`

  <span data-ttu-id="a525b-111">\[out] 陣列中的字元數 `wszName` 。</span><span class="sxs-lookup"><span data-stu-id="a525b-111">\[out] The number of characters in the `wszName` array.</span></span>

- `wszName`

  <span data-ttu-id="a525b-112">\[out] 陣列 `WCHAR` ，其中是函式的名稱（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="a525b-112">\[out] An array of `WCHAR` which is the name of the function, if one exists.</span></span>

## <a name="remarks"></a><span data-ttu-id="a525b-113">備註</span><span class="sxs-lookup"><span data-stu-id="a525b-113">Remarks</span></span>

<span data-ttu-id="a525b-114">某些方法（例如 IL Stub 或 LCG）沒有相關聯的中繼資料可使用[IMetaDataImport](../metadata/imetadataimport-interface.md)和[IMetaDataImport2](../metadata/imetadataimport2-interface.md) api 來抓取。</span><span class="sxs-lookup"><span data-stu-id="a525b-114">Certain methods like IL Stubs or LCG do not have associated metadata that can be retrieved using the [IMetaDataImport](../metadata/imetadataimport-interface.md) and [IMetaDataImport2](../metadata/imetadataimport2-interface.md) APIs.</span></span> <span data-ttu-id="a525b-115">分析工具可以透過指令指標或接聽[ICorProfilerCallback8：:D ynamicmethodjitcompilationstarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)，來遇到這類方法。</span><span class="sxs-lookup"><span data-stu-id="a525b-115">Such methods can be encountered by profilers through instruction pointers or by listening to [ICorProfilerCallback8::DynamicMethodJITCompilationStarted](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md).</span></span>

<span data-ttu-id="a525b-116">此 API 可用於抓取動態方法的相關資訊，包括易記名稱（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="a525b-116">This API can be used to retrieve information about dynamic methods, including a friendly name, if available.</span></span>

## <a name="requirements"></a><span data-ttu-id="a525b-117">規格需求</span><span class="sxs-lookup"><span data-stu-id="a525b-117">Requirements</span></span>

<span data-ttu-id="a525b-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a525b-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="a525b-119">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="a525b-119">**Header:** CorProf.idl, CorProf.h</span></span>

<span data-ttu-id="a525b-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a525b-120">**Library:** CorGuids.lib</span></span>

<span data-ttu-id="a525b-121">**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="a525b-121">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="a525b-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a525b-122">See also</span></span>

- [<span data-ttu-id="a525b-123">ICorProfilerInfo8 介面</span><span class="sxs-lookup"><span data-stu-id="a525b-123">ICorProfilerInfo8 Interface</span></span>](icorprofilerinfo8-interface.md)

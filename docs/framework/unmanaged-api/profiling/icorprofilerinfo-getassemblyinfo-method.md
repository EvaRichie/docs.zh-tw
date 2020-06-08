---
title: ICorProfilerInfo::GetAssemblyInfo 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetAssemblyInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- GetAssemblyInfo Method
helpviewer_keywords:
- GetAssemblyInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetAssemblyInfo method [.NET Framework profiling]
ms.assetid: 7a3c97c3-1e31-47b1-bf23-386785c509c4
topic_type:
- apiref
ms.openlocfilehash: 41083b2fcd61a9a726e835c3d5710308aa634600
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498605"
---
# <a name="icorprofilerinfogetassemblyinfo-method"></a><span data-ttu-id="27958-102">ICorProfilerInfo::GetAssemblyInfo 方法</span><span class="sxs-lookup"><span data-stu-id="27958-102">ICorProfilerInfo::GetAssemblyInfo Method</span></span>
<span data-ttu-id="27958-103">接受組件識別碼，並傳回組件的名稱及其資訊清單模組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="27958-103">Accepts an assembly ID, and returns the assembly's name and the ID of its manifest module.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="27958-104">語法</span><span class="sxs-lookup"><span data-stu-id="27958-104">Syntax</span></span>  
  
```cpp  
HRESULT GetAssemblyInfo(  
    [in]  AssemblyID  assemblyId,  
    [in]  ULONG       cchName,  
    [out] ULONG       *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR       szName[] ,  
    [out] AppDomainID *pAppDomainId,  
    [out] ModuleID    *pModuleId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="27958-105">參數</span><span class="sxs-lookup"><span data-stu-id="27958-105">Parameters</span></span>  
 `assemblyId`  
 <span data-ttu-id="27958-106">[in] 組件的識別項。</span><span class="sxs-lookup"><span data-stu-id="27958-106">[in] The identifier of the assembly.</span></span>  
  
 `cchName`  
 <span data-ttu-id="27958-107">[in] `szName` 的長度 (以字元為單位)。</span><span class="sxs-lookup"><span data-stu-id="27958-107">[in] The length, in characters, of `szName`.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="27958-108">[out] 組件名稱總字元長度的指標。</span><span class="sxs-lookup"><span data-stu-id="27958-108">[out] A pointer to the total character length of the assembly's name.</span></span>  
  
 `szName`  
 <span data-ttu-id="27958-109">[out] 呼叫端提供的寬字元緩衝區。</span><span class="sxs-lookup"><span data-stu-id="27958-109">[out] A caller-provided wide character buffer.</span></span> <span data-ttu-id="27958-110">函式傳回時，會包含組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="27958-110">When the function returns, it will contain the assembly's name.</span></span>  
  
 `pAppDomainId`  
 <span data-ttu-id="27958-111">[out] 包含組件之應用程式定義域的識別碼指標。</span><span class="sxs-lookup"><span data-stu-id="27958-111">[out] A pointer to the ID of the application domain that contains the assembly.</span></span>  
  
 `pModuleId`  
 <span data-ttu-id="27958-112">[out] 組件資訊清單模組的識別碼指標。</span><span class="sxs-lookup"><span data-stu-id="27958-112">[out] A pointer to the ID of the assembly's manifest module.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="27958-113">備註</span><span class="sxs-lookup"><span data-stu-id="27958-113">Remarks</span></span>  
 <span data-ttu-id="27958-114">在此方法傳回之後，您必須確認 `szName` 緩衝區的大小足以包含組件的完整檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="27958-114">After this method returns, you must verify that the `szName` buffer was large enough to contain the full name of the assembly.</span></span> <span data-ttu-id="27958-115">若要這樣做，請比對 `pcchName` 指向的值和 `cchName` 參數。</span><span class="sxs-lookup"><span data-stu-id="27958-115">To do this, compare the value that `pcchName` points to with the value of the `cchName` parameter.</span></span> <span data-ttu-id="27958-116">如果 `pcchName` 指向大於 `cchName` 的值，請配置較大的 `szName` 緩衝區，並以較大的大小來更新 `cchName`，然後再次呼叫 `GetAssemblyInfo`。</span><span class="sxs-lookup"><span data-stu-id="27958-116">If `pcchName` points to a value that is larger than `cchName`, allocate a larger `szName` buffer, update `cchName` with the new, larger size, and call `GetAssemblyInfo` again.</span></span>  
  
 <span data-ttu-id="27958-117">或者，您也可以先使用長度為零的 `szName` 緩衝區來呼叫 `GetAssemblyInfo`，以取得正確的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="27958-117">Alternatively, you can first call `GetAssemblyInfo` with a zero-length `szName` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="27958-118">接著您就可以依據 `pcchName` 中傳回的值來調整緩衝區大小，並再次呼叫 `GetAssemblyInfo`。</span><span class="sxs-lookup"><span data-stu-id="27958-118">You can then adjust the buffer size based on the value returned in `pcchName` and call `GetAssemblyInfo` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="27958-119">規格需求</span><span class="sxs-lookup"><span data-stu-id="27958-119">Requirements</span></span>  
 <span data-ttu-id="27958-120">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="27958-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="27958-121">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="27958-121">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="27958-122">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="27958-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="27958-123">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="27958-123">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="27958-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="27958-124">See also</span></span>

- [<span data-ttu-id="27958-125">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="27958-125">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="27958-126">分析介面</span><span class="sxs-lookup"><span data-stu-id="27958-126">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="27958-127">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="27958-127">Profiling</span></span>](index.md)

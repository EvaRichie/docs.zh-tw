---
title: ICorProfilerInfo3::GetModuleInfo2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetModuleInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetModuleInfo2
helpviewer_keywords:
- ICorProfilerInfo3::GetModuleInfo2 method [.NET Framework profiling]
- GetModuleInfo2 method [.NET Framework profiling]
ms.assetid: f1f6b8f3-dcfc-49e8-be76-ea50ea90d5a7
topic_type:
- apiref
ms.openlocfilehash: 2213b674cce27c77156b8de1bbf20d2975e3e55c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721591"
---
# <a name="icorprofilerinfo3getmoduleinfo2-method"></a><span data-ttu-id="1c708-102">ICorProfilerInfo3::GetModuleInfo2 方法</span><span class="sxs-lookup"><span data-stu-id="1c708-102">ICorProfilerInfo3::GetModuleInfo2 Method</span></span>

<span data-ttu-id="1c708-103">提供模組 ID，傳回該模組的檔案名稱、此模組父代組件的 ID 和描述模組屬性的位元遮罩。</span><span class="sxs-lookup"><span data-stu-id="1c708-103">Given a module ID, returns the file name of the module, the ID of the module's parent assembly, and a bitmask that describes the properties of the module.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1c708-104">語法</span><span class="sxs-lookup"><span data-stu-id="1c708-104">Syntax</span></span>  
  
```cpp  
HRESULT GetModuleInfo2(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, annotation("__out_ecount_part(cchName, *pcchName)")]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
    [out] DWORD                 *pdwModuleFlags);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1c708-105">參數</span><span class="sxs-lookup"><span data-stu-id="1c708-105">Parameters</span></span>  

 `moduleId`  
 <span data-ttu-id="1c708-106">[in] 將被擷取資訊的模組 ID。</span><span class="sxs-lookup"><span data-stu-id="1c708-106">[in] The ID of the module for which information will be retrieved.</span></span>  
  
 `ppBaseLoadAddress`  
 <span data-ttu-id="1c708-107">[out] 載入模組的基底位址。</span><span class="sxs-lookup"><span data-stu-id="1c708-107">[out] The base address at which the module is loaded.</span></span>  
  
 `cchName`  
 <span data-ttu-id="1c708-108">[in] `szName` 傳回緩衝區的長度 (以字元為單位)。</span><span class="sxs-lookup"><span data-stu-id="1c708-108">[in] The length, in characters, of the `szName` return buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="1c708-109">[out] 所傳回的模組檔案名稱之總字元長度的指標。</span><span class="sxs-lookup"><span data-stu-id="1c708-109">[out] A pointer to the total character length of the module's file name that is returned.</span></span>  
  
 `szName`  
 <span data-ttu-id="1c708-110">[out] 呼叫端提供的寬字元緩衝區。</span><span class="sxs-lookup"><span data-stu-id="1c708-110">[out] A caller-provided wide character buffer.</span></span> <span data-ttu-id="1c708-111">當方法傳回時，這個緩衝區會包含模組的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1c708-111">When the method returns, this buffer contains the file name of the module.</span></span>  
  
 `pAssemblyId`  
 <span data-ttu-id="1c708-112">[out] 模組父組件之 ID 的指標。</span><span class="sxs-lookup"><span data-stu-id="1c708-112">[out] A pointer to the ID of the module's parent assembly.</span></span>  
  
 `pdwModuleFlags`  
 <span data-ttu-id="1c708-113">擴展 [COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md) 列舉中值的位元遮罩，指定模組的屬性。</span><span class="sxs-lookup"><span data-stu-id="1c708-113">[out] A bitmask of values from the [COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md) enumeration that specify the properties of the module.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1c708-114">備註</span><span class="sxs-lookup"><span data-stu-id="1c708-114">Remarks</span></span>  

 <span data-ttu-id="1c708-115">若為動態模組，則 `szName` 參數為模組之中繼資料名稱，且基底位址為 0 (零)。</span><span class="sxs-lookup"><span data-stu-id="1c708-115">For dynamic modules, the `szName` parameter is the metadata name of the module, and the base address is 0 (zero).</span></span> <span data-ttu-id="1c708-116">中繼資料名稱是中繼資料內的模組資料表之「名稱」欄中的值。</span><span class="sxs-lookup"><span data-stu-id="1c708-116">The metadata name is the value in the Name column from the Module table inside metadata.</span></span> <span data-ttu-id="1c708-117">這也會公開為 <xref:System.Reflection.Module.ScopeName%2A?displayProperty=nameWithType> managed 程式碼的屬性，以及做為 `szName` 非受控中繼資料用戶端程式代碼之 [IMetaDataImport：： GetScopeProps](../metadata/imetadataimport-getscopeprops-method.md) 方法的參數。</span><span class="sxs-lookup"><span data-stu-id="1c708-117">This is also exposed as the <xref:System.Reflection.Module.ScopeName%2A?displayProperty=nameWithType> property to managed code, and as the `szName` parameter of the [IMetaDataImport::GetScopeProps](../metadata/imetadataimport-getscopeprops-method.md) method to unmanaged metadata client code.</span></span>  
  
 <span data-ttu-id="1c708-118">雖然此 `GetModuleInfo2` 方法可能會在模組的識別碼存在時立即呼叫，但是在分析工具收到 [ICorProfilerCallback：： ModuleAttachedToAssembly](icorprofilercallback-moduleattachedtoassembly-method.md) 回呼之前，將無法使用父元件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1c708-118">Although the `GetModuleInfo2` method may be called as soon as the module's ID exists, the ID of the parent assembly will not be available until the profiler receives the [ICorProfilerCallback::ModuleAttachedToAssembly](icorprofilercallback-moduleattachedtoassembly-method.md) callback.</span></span>  
  
 <span data-ttu-id="1c708-119">當 `GetModuleInfo2` 傳回時，您必須確認 `szName` 緩衝區的大小足以包含模組的完整檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1c708-119">When `GetModuleInfo2` returns, you must verify that the `szName` buffer was large enough to contain the full file name of the module.</span></span> <span data-ttu-id="1c708-120">若要這樣做，請比對 `pcchName` 指向的值和 `cchName` 參數。</span><span class="sxs-lookup"><span data-stu-id="1c708-120">To do this, compare the value that `pcchName` points to with the value of the `cchName` parameter.</span></span> <span data-ttu-id="1c708-121">如果 `pcchName` 指向大於 `cchName` 的值，請配置較大的 `szName` 緩衝區，並以較大的大小來更新 `cchName`，然後再次呼叫 `GetModuleInfo2`。</span><span class="sxs-lookup"><span data-stu-id="1c708-121">If `pcchName` points to a value that is larger than `cchName`, allocate a larger `szName` buffer, update `cchName` with the new, larger size, and call `GetModuleInfo2` again.</span></span>  
  
 <span data-ttu-id="1c708-122">或者，您也可以先使用長度為零的 `szName` 緩衝區來呼叫 `GetModuleInfo2`，以取得正確的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="1c708-122">Alternatively, you can first call `GetModuleInfo2` with a zero-length `szName` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="1c708-123">接著您就可以將緩衝區大小設定為 `pcchName` 中傳回的值，並再次呼叫 `GetModuleInfo2`。</span><span class="sxs-lookup"><span data-stu-id="1c708-123">You can then set the buffer size to the value returned in `pcchName` and call `GetModuleInfo2` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1c708-124">需求</span><span class="sxs-lookup"><span data-stu-id="1c708-124">Requirements</span></span>  

 <span data-ttu-id="1c708-125">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1c708-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1c708-126">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="1c708-126">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="1c708-127">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1c708-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1c708-128">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1c708-128">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1c708-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1c708-129">See also</span></span>

- [<span data-ttu-id="1c708-130">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="1c708-130">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="1c708-131">分析介面</span><span class="sxs-lookup"><span data-stu-id="1c708-131">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="1c708-132">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="1c708-132">Profiling</span></span>](index.md)

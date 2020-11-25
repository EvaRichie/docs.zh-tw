---
title: ICorProfilerInfo3::GetAppDomainsContainingModule 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetAppDomainsContainingModule Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetAppDomainsContainingModule
helpviewer_keywords:
- GetAppDomainsContainingModule method [.NET Framework profiling]
- ICorProfilerInfo3::GetAppDomainsContainingModule method [.NET Framework profiling]
ms.assetid: 603b3881-ea94-4dca-95cd-91eebac873a0
topic_type:
- apiref
ms.openlocfilehash: 5cc3436716bcfc2ed0f9fd7ff7982bac7a48de9a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731198"
---
# <a name="icorprofilerinfo3getappdomainscontainingmodule-method"></a><span data-ttu-id="13c76-102">ICorProfilerInfo3::GetAppDomainsContainingModule 方法</span><span class="sxs-lookup"><span data-stu-id="13c76-102">ICorProfilerInfo3::GetAppDomainsContainingModule Method</span></span>

<span data-ttu-id="13c76-103">取得已載入指定模組之應用程式定義域的識別項。</span><span class="sxs-lookup"><span data-stu-id="13c76-103">Gets the identifiers of the application domains in which the given module has been loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="13c76-104">語法</span><span class="sxs-lookup"><span data-stu-id="13c76-104">Syntax</span></span>  
  
```cpp  
HRESULT GetAppDomainsContainingModule(  
            [in] ModuleID moduleId,  
            [in] ULONG32 cAppDomainIds,  
            [out] ULONG32 *pcAppDomainIds,  
            [out, size_is(cAppDomainIds), length_is(*pcAppDomainIds)]  
                    AppDomainID appDomainIds[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="13c76-105">參數</span><span class="sxs-lookup"><span data-stu-id="13c76-105">Parameters</span></span>  

 `moduleId`  
 <span data-ttu-id="13c76-106">[in] 載入模組的 ID。</span><span class="sxs-lookup"><span data-stu-id="13c76-106">[in] The ID of the loaded module.</span></span>  
  
 `cAppDomainIds`  
 <span data-ttu-id="13c76-107">[in] `appDomainIds` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="13c76-107">[in] The size of the `appDomainIds` array.</span></span>  
  
 `pcAppDomainIds`  
 <span data-ttu-id="13c76-108">[out] 傳回項目之總數的指標。</span><span class="sxs-lookup"><span data-stu-id="13c76-108">[out] A pointer to the total number of returned elements.</span></span>  
  
 `appDomainIds`  
 <span data-ttu-id="13c76-109">[out] 應用程式定義域 ID 值的陣列。</span><span class="sxs-lookup"><span data-stu-id="13c76-109">[out] An array of application domain ID values.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="13c76-110">備註</span><span class="sxs-lookup"><span data-stu-id="13c76-110">Remarks</span></span>  

 <span data-ttu-id="13c76-111">這個方法會使用呼叫端配置的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="13c76-111">The method uses caller allocated buffers.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="13c76-112">需求</span><span class="sxs-lookup"><span data-stu-id="13c76-112">Requirements</span></span>  

 <span data-ttu-id="13c76-113">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="13c76-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="13c76-114">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="13c76-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="13c76-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="13c76-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="13c76-116">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="13c76-116">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13c76-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13c76-117">See also</span></span>

- [<span data-ttu-id="13c76-118">ICorProfilerFunctionEnum 介面</span><span class="sxs-lookup"><span data-stu-id="13c76-118">ICorProfilerFunctionEnum Interface</span></span>](icorprofilerfunctionenum-interface.md)
- [<span data-ttu-id="13c76-119">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="13c76-119">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="13c76-120">分析介面</span><span class="sxs-lookup"><span data-stu-id="13c76-120">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="13c76-121">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="13c76-121">Profiling</span></span>](index.md)

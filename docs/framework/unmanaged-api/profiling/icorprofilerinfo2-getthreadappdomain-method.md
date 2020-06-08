---
title: ICorProfilerInfo2::GetThreadAppDomain 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetThreadAppDomain
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetThreadAppDomain
helpviewer_keywords:
- ICorProfilerInfo2::GetThreadAppDomain method [.NET Framework profiling]
- GetThreadAppDomain method [.NET Framework profiling]
ms.assetid: 4a11b264-8540-4732-aa35-bc2d95b95b8e
topic_type:
- apiref
ms.openlocfilehash: 70535f8bcee95c2596c43617eb5893e2d92a355b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496774"
---
# <a name="icorprofilerinfo2getthreadappdomain-method"></a><span data-ttu-id="34f24-102">ICorProfilerInfo2::GetThreadAppDomain 方法</span><span class="sxs-lookup"><span data-stu-id="34f24-102">ICorProfilerInfo2::GetThreadAppDomain Method</span></span>
<span data-ttu-id="34f24-103">取得指定的執行緒目前正在執行程式碼的應用程式域識別碼。</span><span class="sxs-lookup"><span data-stu-id="34f24-103">Gets the ID of the application domain in which the specified thread is currently executing code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="34f24-104">語法</span><span class="sxs-lookup"><span data-stu-id="34f24-104">Syntax</span></span>  
  
```cpp  
HRESULT GetThreadAppDomain(  
    [in]  ThreadID threadId,  
    [out] AppDomainID *pAppDomainId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="34f24-105">參數</span><span class="sxs-lookup"><span data-stu-id="34f24-105">Parameters</span></span>  
 `threadId`  
 <span data-ttu-id="34f24-106">在指定執行緒的識別碼。</span><span class="sxs-lookup"><span data-stu-id="34f24-106">[in] The ID specifying the thread.</span></span>  
  
 `pAppDomainId`  
 <span data-ttu-id="34f24-107">脫銷應用程式域的識別碼指標。</span><span class="sxs-lookup"><span data-stu-id="34f24-107">[out] A pointer to the ID of the application domain.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="34f24-108">規格需求</span><span class="sxs-lookup"><span data-stu-id="34f24-108">Requirements</span></span>  
 <span data-ttu-id="34f24-109">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="34f24-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="34f24-110">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="34f24-110">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="34f24-111">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="34f24-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="34f24-112">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="34f24-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="34f24-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="34f24-113">See also</span></span>

- [<span data-ttu-id="34f24-114">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="34f24-114">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="34f24-115">ICorProfilerInfo2 介面</span><span class="sxs-lookup"><span data-stu-id="34f24-115">ICorProfilerInfo2 Interface</span></span>](icorprofilerinfo2-interface.md)

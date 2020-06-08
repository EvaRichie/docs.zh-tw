---
title: ICorProfilerModuleEnum::GetCount 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.GetCount Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::GetCount
helpviewer_keywords:
- ICorProfilerModuleEnum::GetCount method [.NET Framework profiling]
- GetCount method, ICorProfilerModuleEnum interface [.NET Framework profiling]
ms.assetid: f0a4a5e0-4689-474b-b0f4-37ca0639c918
topic_type:
- apiref
ms.openlocfilehash: 604ecb2122cce6e24f0e5168fa286a523d8bb4f7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495069"
---
# <a name="icorprofilermoduleenumgetcount-method"></a><span data-ttu-id="3ec25-102">ICorProfilerModuleEnum::GetCount 方法</span><span class="sxs-lookup"><span data-stu-id="3ec25-102">ICorProfilerModuleEnum::GetCount Method</span></span>
<span data-ttu-id="3ec25-103">取得已載入至應用程式之 Managed 模組的數目。</span><span class="sxs-lookup"><span data-stu-id="3ec25-103">Gets the number of managed modules that were loaded into the application.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3ec25-104">語法</span><span class="sxs-lookup"><span data-stu-id="3ec25-104">Syntax</span></span>  
  
```cpp  
HRESULT GetCount([out] ULONG * pcelt);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3ec25-105">參數</span><span class="sxs-lookup"><span data-stu-id="3ec25-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="3ec25-106">脫銷集合中執行時間模組的數目。</span><span class="sxs-lookup"><span data-stu-id="3ec25-106">[out] The number of runtime modules in the collection.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3ec25-107">規格需求</span><span class="sxs-lookup"><span data-stu-id="3ec25-107">Requirements</span></span>  
 <span data-ttu-id="3ec25-108">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3ec25-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3ec25-109">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="3ec25-109">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="3ec25-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3ec25-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3ec25-111">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3ec25-111">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3ec25-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ec25-112">See also</span></span>

- [<span data-ttu-id="3ec25-113">ICorProfilerModuleEnum 介面</span><span class="sxs-lookup"><span data-stu-id="3ec25-113">ICorProfilerModuleEnum Interface</span></span>](icorprofilermoduleenum-interface.md)
- [<span data-ttu-id="3ec25-114">分析介面</span><span class="sxs-lookup"><span data-stu-id="3ec25-114">Profiling Interfaces</span></span>](profiling-interfaces.md)

---
title: ICorProfilerInfo3::EnumModules 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.EnumModules Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::EnumModules
helpviewer_keywords:
- ICorProfilerInfo3::EnumModules method [.NET Framework profiling]
- EnumModules method [.NET Framework profiling]
ms.assetid: 1bf00b42-69da-4019-91b3-bf88026e83fb
topic_type:
- apiref
ms.openlocfilehash: 698f6abc872a7e072ae47520386aa9c7ddfb44fa
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95681466"
---
# <a name="icorprofilerinfo3enummodules-method"></a><span data-ttu-id="ab18d-102">ICorProfilerInfo3::EnumModules 方法</span><span class="sxs-lookup"><span data-stu-id="ab18d-102">ICorProfilerInfo3::EnumModules Method</span></span>

<span data-ttu-id="ab18d-103">傳回提供循序逐一查看 Managed 模組集合方法的列舉，其中該模組被載入至應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ab18d-103">Returns an enumerator that provides methods to sequentially iterate through a collection of managed modules that are loaded into the application.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ab18d-104">語法</span><span class="sxs-lookup"><span data-stu-id="ab18d-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumModules([out] ICorProfilerModuleEnum** ppEnum);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ab18d-105">參數</span><span class="sxs-lookup"><span data-stu-id="ab18d-105">Parameters</span></span>  

 `ppEnum`  
 <span data-ttu-id="ab18d-106">擴展 [ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md) 介面的指標。</span><span class="sxs-lookup"><span data-stu-id="ab18d-106">[out] A pointer to an [ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md) interface.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ab18d-107">備註</span><span class="sxs-lookup"><span data-stu-id="ab18d-107">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ab18d-108">需求</span><span class="sxs-lookup"><span data-stu-id="ab18d-108">Requirements</span></span>  

 <span data-ttu-id="ab18d-109">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ab18d-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ab18d-110">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="ab18d-110">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="ab18d-111">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ab18d-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ab18d-112">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ab18d-112">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ab18d-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ab18d-113">See also</span></span>

- [<span data-ttu-id="ab18d-114">ICorProfilerFunctionEnum 介面</span><span class="sxs-lookup"><span data-stu-id="ab18d-114">ICorProfilerFunctionEnum Interface</span></span>](icorprofilerfunctionenum-interface.md)
- [<span data-ttu-id="ab18d-115">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="ab18d-115">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="ab18d-116">分析介面</span><span class="sxs-lookup"><span data-stu-id="ab18d-116">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="ab18d-117">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="ab18d-117">Profiling</span></span>](index.md)

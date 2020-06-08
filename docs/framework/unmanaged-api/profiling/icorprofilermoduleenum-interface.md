---
title: ICorProfilerModuleEnum 介面
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum
api_location:
- mscorwks.cll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum
helpviewer_keywords:
- ICorProfilerModuleEnum interface [.NET Framework profiling]
ms.assetid: 24d0fcfa-1601-4fba-868f-da8c97303467
topic_type:
- apiref
ms.openlocfilehash: fe11c0bbe273ae07cdae43f681a558e07a291ffb
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494887"
---
# <a name="icorprofilermoduleenum-interface"></a><span data-ttu-id="083d5-102">ICorProfilerModuleEnum 介面</span><span class="sxs-lookup"><span data-stu-id="083d5-102">ICorProfilerModuleEnum Interface</span></span>
<span data-ttu-id="083d5-103">提供方法，以循序逐一查看由應用程式或分析工具所載入的模組集合。</span><span class="sxs-lookup"><span data-stu-id="083d5-103">Provides methods to sequentially iterate through a collection of modules loaded by the application or the profiler.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="083d5-104">方法</span><span class="sxs-lookup"><span data-stu-id="083d5-104">Methods</span></span>  
  
|<span data-ttu-id="083d5-105">方法</span><span class="sxs-lookup"><span data-stu-id="083d5-105">Method</span></span>|<span data-ttu-id="083d5-106">描述</span><span class="sxs-lookup"><span data-stu-id="083d5-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="083d5-107">Clone 方法</span><span class="sxs-lookup"><span data-stu-id="083d5-107">Clone Method</span></span>](icorprofilermoduleenum-clone-method.md)|<span data-ttu-id="083d5-108">取得這個 `ICorProfilerModuleEnum` 介面複本的介面指標。</span><span class="sxs-lookup"><span data-stu-id="083d5-108">Gets an interface pointer to a copy of this `ICorProfilerModuleEnum` interface.</span></span>|  
|[<span data-ttu-id="083d5-109">GetCount 方法</span><span class="sxs-lookup"><span data-stu-id="083d5-109">GetCount Method</span></span>](icorprofilermoduleenum-getcount-method.md)|<span data-ttu-id="083d5-110">取得已載入至應用程式之 Managed 模組的數目。</span><span class="sxs-lookup"><span data-stu-id="083d5-110">Gets the number of managed modules that were loaded into the application.</span></span>|  
|[<span data-ttu-id="083d5-111">下一個方法</span><span class="sxs-lookup"><span data-stu-id="083d5-111">Next Method</span></span>](icorprofilermoduleenum-next-method.md)|<span data-ttu-id="083d5-112">從循序物件集合中取得指定的連續模組數目，從序列中列舉值的目前位置開始。</span><span class="sxs-lookup"><span data-stu-id="083d5-112">Gets the specified number of contiguous modules from a sequential collection of objects, starting at the enumerator's current position in the sequence.</span></span>|  
|[<span data-ttu-id="083d5-113">Reset 方法</span><span class="sxs-lookup"><span data-stu-id="083d5-113">Reset Method</span></span>](icorprofilermoduleenum-reset-method.md)|<span data-ttu-id="083d5-114">將列舉值的資料指標移至序列的開始位置。</span><span class="sxs-lookup"><span data-stu-id="083d5-114">Moves the enumerator's cursor to the starting position of the sequence.</span></span>|  
|[<span data-ttu-id="083d5-115">Skip 方法</span><span class="sxs-lookup"><span data-stu-id="083d5-115">Skip Method</span></span>](icorprofilermoduleenum-skip-method.md)|<span data-ttu-id="083d5-116">將列舉值的資料指標位置前移，以略過指定數目的項目。</span><span class="sxs-lookup"><span data-stu-id="083d5-116">Advances the position of the enumerator's cursor so that the specified number of elements are skipped.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="083d5-117">備註</span><span class="sxs-lookup"><span data-stu-id="083d5-117">Remarks</span></span>  
 <span data-ttu-id="083d5-118">`ICorProfilerModuleEnum` 介面是列舉值。</span><span class="sxs-lookup"><span data-stu-id="083d5-118">The `ICorProfilerModuleEnum` interface is an enumerator.</span></span> <span data-ttu-id="083d5-119">它可讓陣列的接收端以適合接收端的速率，從傳送端提取項目。</span><span class="sxs-lookup"><span data-stu-id="083d5-119">It allows the receiver of an array to pull elements from the sender at a rate that is appropriate for the receiver.</span></span> <span data-ttu-id="083d5-120">換句話說，接收端能夠明確控制陣列項目的流程，因此可避免與傳遞大型陣列做為方法參數相關的問題發生。</span><span class="sxs-lookup"><span data-stu-id="083d5-120">In other words, the receiver is able to explicitly control the flow of array elements, thereby avoiding the problems associated with passing large arrays as method parameters.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="083d5-121">規格需求</span><span class="sxs-lookup"><span data-stu-id="083d5-121">Requirements</span></span>  
 <span data-ttu-id="083d5-122">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="083d5-122">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="083d5-123">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="083d5-123">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="083d5-124">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="083d5-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="083d5-125">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="083d5-125">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="083d5-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="083d5-126">See also</span></span>

- [<span data-ttu-id="083d5-127">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="083d5-127">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="083d5-128">分析介面</span><span class="sxs-lookup"><span data-stu-id="083d5-128">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="083d5-129">EnumModules 方法</span><span class="sxs-lookup"><span data-stu-id="083d5-129">EnumModules Method</span></span>](icorprofilerinfo3-enummodules-method.md)

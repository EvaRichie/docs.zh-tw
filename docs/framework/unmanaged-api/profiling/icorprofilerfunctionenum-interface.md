---
title: ICorProfilerFunctionEnum 介面
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum
helpviewer_keywords:
- ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 0a1d4a38-cd0b-4231-91df-13646218ae72
topic_type:
- apiref
ms.openlocfilehash: 84c3b504dff8a04172dde903c1681c9f3fb2fcd2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95669224"
---
# <a name="icorprofilerfunctionenum-interface"></a><span data-ttu-id="877b9-102">ICorProfilerFunctionEnum 介面</span><span class="sxs-lookup"><span data-stu-id="877b9-102">ICorProfilerFunctionEnum Interface</span></span>

<span data-ttu-id="877b9-103">提供方法以循序逐一查看 Common Language Runtime 中的函式集合。</span><span class="sxs-lookup"><span data-stu-id="877b9-103">Provides methods to sequentially iterate through a collection of functions in the common language runtime.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="877b9-104">方法</span><span class="sxs-lookup"><span data-stu-id="877b9-104">Methods</span></span>  
  
|<span data-ttu-id="877b9-105">方法</span><span class="sxs-lookup"><span data-stu-id="877b9-105">Method</span></span>|<span data-ttu-id="877b9-106">描述</span><span class="sxs-lookup"><span data-stu-id="877b9-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="877b9-107">Clone 方法</span><span class="sxs-lookup"><span data-stu-id="877b9-107">Clone Method</span></span>](icorprofilerfunctionenum-clone-method.md)|<span data-ttu-id="877b9-108">取得這個 `ICorProfilerFunctionEnum` 介面複本的介面指標。</span><span class="sxs-lookup"><span data-stu-id="877b9-108">Gets an interface pointer to a copy of this `ICorProfilerFunctionEnum` interface.</span></span>|  
|[<span data-ttu-id="877b9-109">GetCount 方法</span><span class="sxs-lookup"><span data-stu-id="877b9-109">GetCount Method</span></span>](icorprofilerfunctionenum-getcount-method.md)|<span data-ttu-id="877b9-110">取得應用程式已載入的或分析工具強制載入的函式數目。</span><span class="sxs-lookup"><span data-stu-id="877b9-110">Gets the number of functions that were loaded by the application or forcibly loaded by the profiler.</span></span>|  
|[<span data-ttu-id="877b9-111">下一個方法</span><span class="sxs-lookup"><span data-stu-id="877b9-111">Next Method</span></span>](icorprofilerfunctionenum-next-method.md)|<span data-ttu-id="877b9-112">從循序函式集合中取得指定的連續函式數目，從序列中列舉值的目前位置開始。</span><span class="sxs-lookup"><span data-stu-id="877b9-112">Gets the specified number of contiguous functions from a sequential collection of functions, starting at the enumerator's current position in the sequence.</span></span>|  
|[<span data-ttu-id="877b9-113">Reset 方法</span><span class="sxs-lookup"><span data-stu-id="877b9-113">Reset Method</span></span>](icorprofilerfunctionenum-reset-method.md)|<span data-ttu-id="877b9-114">將列舉值的資料指標移至序列的開始位置。</span><span class="sxs-lookup"><span data-stu-id="877b9-114">Moves the enumerator's cursor to the starting position of the sequence.</span></span>|  
|[<span data-ttu-id="877b9-115">Skip 方法</span><span class="sxs-lookup"><span data-stu-id="877b9-115">Skip Method</span></span>](icorprofilerfunctionenum-skip-method.md)|<span data-ttu-id="877b9-116">將列舉值的資料指標從其目前位置前移，以略過指定數目的項目。</span><span class="sxs-lookup"><span data-stu-id="877b9-116">Advances the enumerator's cursor from its current position so that the specified number of elements are skipped.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="877b9-117">備註</span><span class="sxs-lookup"><span data-stu-id="877b9-117">Remarks</span></span>  

 <span data-ttu-id="877b9-118">`ICorProfilerFunctionEnum` 介面是列舉值。</span><span class="sxs-lookup"><span data-stu-id="877b9-118">The `ICorProfilerFunctionEnum` interface is an enumerator.</span></span> <span data-ttu-id="877b9-119">它可讓陣列的接收端以適合接收端的速率，從傳送端提取項目。</span><span class="sxs-lookup"><span data-stu-id="877b9-119">It allows the receiver of an array to pull elements from the sender at a rate that is appropriate for the receiver.</span></span> <span data-ttu-id="877b9-120">換句話說，接收端能夠明確控制陣列項目的流程，因此可避免與傳遞大型陣列做為方法參數相關的問題發生。</span><span class="sxs-lookup"><span data-stu-id="877b9-120">In other words, the receiver is able to explicitly control the flow of array elements, thereby avoiding the problems associated with passing large arrays as method parameters.</span></span>  
  
 <span data-ttu-id="877b9-121">`ICorProfilerFunctionEnum` 列舉早已 JIT 編譯的函式，但此函式不包含從 Ngen.exe 產生的原生影像載入之函式。</span><span class="sxs-lookup"><span data-stu-id="877b9-121">`ICorProfilerFunctionEnum` enumerates over functions that have already been JIT-compiled, but does not include functions that are loaded from native images generated with Ngen.exe.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="877b9-122">需求</span><span class="sxs-lookup"><span data-stu-id="877b9-122">Requirements</span></span>  

 <span data-ttu-id="877b9-123">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="877b9-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="877b9-124">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="877b9-124">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="877b9-125">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="877b9-125">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="877b9-126">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="877b9-126">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="877b9-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="877b9-127">See also</span></span>

- [<span data-ttu-id="877b9-128">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="877b9-128">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="877b9-129">分析介面</span><span class="sxs-lookup"><span data-stu-id="877b9-129">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="877b9-130">EnumJITedFunctions 方法</span><span class="sxs-lookup"><span data-stu-id="877b9-130">EnumJITedFunctions Method</span></span>](icorprofilerinfo3-enumjitedfunctions-method.md)

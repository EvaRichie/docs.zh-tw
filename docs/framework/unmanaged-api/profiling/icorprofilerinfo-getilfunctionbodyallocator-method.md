---
title: ICorProfilerInfo::GetILFunctionBodyAllocator 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetILFunctionBodyAllocator
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetILFunctionBodyAllocator
helpviewer_keywords:
- GetILFunctionBodyAllocator method [.NET Framework profiling]
- ICorProfilerInfo::GetILFunctionBodyAllocator method [.NET Framework profiling]
ms.assetid: 5da1bf3d-dddf-4892-b266-578ee54d570b
topic_type:
- apiref
ms.openlocfilehash: 967f38add9ae5996c6ac33388203b55161a84e39
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498267"
---
# <a name="icorprofilerinfogetilfunctionbodyallocator-method"></a><span data-ttu-id="1df1e-102">ICorProfilerInfo::GetILFunctionBodyAllocator 方法</span><span class="sxs-lookup"><span data-stu-id="1df1e-102">ICorProfilerInfo::GetILFunctionBodyAllocator Method</span></span>
<span data-ttu-id="1df1e-103">取得介面，它會提供方法來配置記憶體，以用於交換 Microsoft 中繼語言（MSIL）程式碼中方法的主體。</span><span class="sxs-lookup"><span data-stu-id="1df1e-103">Gets an interface that provides a method to allocate memory to be used for swapping out the body of a method in Microsoft intermediate language (MSIL) code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1df1e-104">語法</span><span class="sxs-lookup"><span data-stu-id="1df1e-104">Syntax</span></span>  
  
```cpp  
HRESULT GetILFunctionBodyAllocator(  
    [in]  ModuleID      moduleId,  
    [out] IMethodMalloc **ppMalloc);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1df1e-105">參數</span><span class="sxs-lookup"><span data-stu-id="1df1e-105">Parameters</span></span>  
 `moduleId`  
 <span data-ttu-id="1df1e-106">在方法所在模組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1df1e-106">[in] The ID of the module in which the method resides.</span></span>  
  
 `ppMalloc`  
 <span data-ttu-id="1df1e-107">脫銷提供方法來配置記憶體的[IMethodMalloc](imethodmalloc-interface.md)介面指標。</span><span class="sxs-lookup"><span data-stu-id="1df1e-107">[out] A pointer to an [IMethodMalloc](imethodmalloc-interface.md) interface that provides a method to allocate the memory.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1df1e-108">備註</span><span class="sxs-lookup"><span data-stu-id="1df1e-108">Remarks</span></span>  
 <span data-ttu-id="1df1e-109">MSIL 程式碼中的方法主體必須位於相對於已載入模組的相對虛擬位址（RVA），這表示它會遵循 4 GB 內的模組。</span><span class="sxs-lookup"><span data-stu-id="1df1e-109">A method body in MSIL code must be located as a relative virtual address (RVA), relative to the loaded module, which means that it follows the module within 4 GB.</span></span> <span data-ttu-id="1df1e-110">為了讓工具能夠更輕鬆地交換方法的主體， `GetILFunctionBodyAllocator` 方法可確保記憶體會在該範圍內配置。</span><span class="sxs-lookup"><span data-stu-id="1df1e-110">To make it easier for a tool to swap out the body of a method, the `GetILFunctionBodyAllocator` method ensures that memory is allocated within that range.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1df1e-111">規格需求</span><span class="sxs-lookup"><span data-stu-id="1df1e-111">Requirements</span></span>  
 <span data-ttu-id="1df1e-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1df1e-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1df1e-113">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="1df1e-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="1df1e-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1df1e-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1df1e-115">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1df1e-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1df1e-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1df1e-116">See also</span></span>

- [<span data-ttu-id="1df1e-117">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="1df1e-117">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)

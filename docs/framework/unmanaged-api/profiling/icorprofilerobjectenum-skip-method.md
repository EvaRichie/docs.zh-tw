---
title: ICorProfilerObjectEnum::Skip 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.Skip
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::Skip
helpviewer_keywords:
- ICorProfilerObjectEnum::Skip method [.NET Framework profiling]
- Skip method, ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: f8e498f8-f93a-4b82-bd22-55bdbf5e8d45
topic_type:
- apiref
ms.openlocfilehash: 2248f99b76aaabff4bd3dc78b6e777a95692bb9c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494513"
---
# <a name="icorprofilerobjectenumskip-method"></a><span data-ttu-id="725b0-102">ICorProfilerObjectEnum::Skip 方法</span><span class="sxs-lookup"><span data-stu-id="725b0-102">ICorProfilerObjectEnum::Skip Method</span></span>
<span data-ttu-id="725b0-103">將此列舉值的資料指標從其目前位置前移，以略過指定數目的元素。</span><span class="sxs-lookup"><span data-stu-id="725b0-103">Advances the cursor of this enumerator from its current position so that the specified number of elements are skipped.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="725b0-104">語法</span><span class="sxs-lookup"><span data-stu-id="725b0-104">Syntax</span></span>  
  
```cpp  
HRESULT Skip (  
    [in] ULONG   celt  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="725b0-105">參數</span><span class="sxs-lookup"><span data-stu-id="725b0-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="725b0-106">在要略過的元素數目。</span><span class="sxs-lookup"><span data-stu-id="725b0-106">[in] The number of elements to be skipped.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="725b0-107">備註</span><span class="sxs-lookup"><span data-stu-id="725b0-107">Remarks</span></span>  
 <span data-ttu-id="725b0-108">這個列舉值的資料指標的新位置是：（目前的位置） + `celt` 。</span><span class="sxs-lookup"><span data-stu-id="725b0-108">The new position of this enumerator's cursor is: (current position) + `celt` .</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="725b0-109">規格需求</span><span class="sxs-lookup"><span data-stu-id="725b0-109">Requirements</span></span>  
 <span data-ttu-id="725b0-110">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="725b0-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="725b0-111">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="725b0-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="725b0-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="725b0-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="725b0-113">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="725b0-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="725b0-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="725b0-114">See also</span></span>

- [<span data-ttu-id="725b0-115">ICorProfilerObjectEnum 介面</span><span class="sxs-lookup"><span data-stu-id="725b0-115">ICorProfilerObjectEnum Interface</span></span>](icorprofilerobjectenum-interface.md)

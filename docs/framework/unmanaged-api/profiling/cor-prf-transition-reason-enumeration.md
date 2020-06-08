---
title: COR_PRF_TRANSITION_REASON 列舉
ms.date: 03/30/2017
api_name:
- COR_PRF_TRANSITION_REASON
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_TRANSITION_REASON
helpviewer_keywords:
- COR_PRF_TRANSITION_REASON enumeration [.NET Framework profiling]
ms.assetid: da941118-01b7-4197-ae5b-9f2f8adcd623
topic_type:
- apiref
ms.openlocfilehash: e890c62a54654e86bb4a825613807efe142c8d5a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500737"
---
# <a name="cor_prf_transition_reason-enumeration"></a><span data-ttu-id="85fa9-102">COR_PRF_TRANSITION_REASON 列舉</span><span class="sxs-lookup"><span data-stu-id="85fa9-102">COR_PRF_TRANSITION_REASON Enumeration</span></span>
<span data-ttu-id="85fa9-103">指出從 Managed 程式碼轉換為 Unmanaged 程式碼 (反之亦然) 的原因。</span><span class="sxs-lookup"><span data-stu-id="85fa9-103">Indicates the reason for a transition from managed to unmanaged code, or vice versa.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="85fa9-104">語法</span><span class="sxs-lookup"><span data-stu-id="85fa9-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    COR_PRF_TRANSITION_CALL,  
    COR_PRF_TRANSITION_RETURN  
} COR_PRF_TRANSITION_REASON;  
```  
  
## <a name="members"></a><span data-ttu-id="85fa9-105">成員</span><span class="sxs-lookup"><span data-stu-id="85fa9-105">Members</span></span>  
  
|<span data-ttu-id="85fa9-106">成員</span><span class="sxs-lookup"><span data-stu-id="85fa9-106">Member</span></span>|<span data-ttu-id="85fa9-107">說明</span><span class="sxs-lookup"><span data-stu-id="85fa9-107">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_TRANSITION_CALL`|<span data-ttu-id="85fa9-108">轉換是因為函式的呼叫所造成。</span><span class="sxs-lookup"><span data-stu-id="85fa9-108">The transition is due to a call into a function.</span></span>|  
|`COR_PRF_TRANSITION_RETURN`|<span data-ttu-id="85fa9-109">轉換是因為從函式傳回。</span><span class="sxs-lookup"><span data-stu-id="85fa9-109">The transition is due to a return from a function.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="85fa9-110">備註</span><span class="sxs-lookup"><span data-stu-id="85fa9-110">Remarks</span></span>  
 <span data-ttu-id="85fa9-111">當轉換發生時，分析工具會收到[ICorProfilerCallback：： ManagedToUnmanagedTransition](icorprofilercallback-managedtounmanagedtransition-method.md)或[ICorProfilerCallback：： UnmanagedToManagedTransition](icorprofilercallback-unmanagedtomanagedtransition-method.md)回呼，其中任一項都會提供列舉的值 `COR_PRF_TRANSITION_REASON` 來指出轉換的原因。</span><span class="sxs-lookup"><span data-stu-id="85fa9-111">When a transition occurs, the profiler receives an [ICorProfilerCallback::ManagedToUnmanagedTransition](icorprofilercallback-managedtounmanagedtransition-method.md) or [ICorProfilerCallback::UnmanagedToManagedTransition](icorprofilercallback-unmanagedtomanagedtransition-method.md) callback, either of which provides a value of the `COR_PRF_TRANSITION_REASON` enumeration to indicate the reason for the transition.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="85fa9-112">規格需求</span><span class="sxs-lookup"><span data-stu-id="85fa9-112">Requirements</span></span>  
 <span data-ttu-id="85fa9-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="85fa9-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="85fa9-114">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="85fa9-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="85fa9-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="85fa9-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="85fa9-116">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="85fa9-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

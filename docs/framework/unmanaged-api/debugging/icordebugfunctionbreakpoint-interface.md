---
title: ICorDebugFunctionBreakpoint 介面
ms.date: 03/30/2017
api_name:
- ICorDebugFunctionBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunctionBreakpoint
helpviewer_keywords:
- ICorDebugFunctionBreakpoint interface [.NET Framework debugging]
ms.assetid: 9c149303-14b1-4138-83d7-e8c3e0fcd332
topic_type:
- apiref
ms.openlocfilehash: 0f1e6bbdf16c953b0dd22d9dfa44bc3585f1269e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726245"
---
# <a name="icordebugfunctionbreakpoint-interface"></a><span data-ttu-id="e78f9-102">ICorDebugFunctionBreakpoint 介面</span><span class="sxs-lookup"><span data-stu-id="e78f9-102">ICorDebugFunctionBreakpoint Interface</span></span>

<span data-ttu-id="e78f9-103">擴充 ICorDebugBreakpoint 介面，以支援函數中的中斷點。</span><span class="sxs-lookup"><span data-stu-id="e78f9-103">Extends the ICorDebugBreakpoint interface to support breakpoints within functions.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e78f9-104">方法</span><span class="sxs-lookup"><span data-stu-id="e78f9-104">Methods</span></span>  
  
|<span data-ttu-id="e78f9-105">方法</span><span class="sxs-lookup"><span data-stu-id="e78f9-105">Method</span></span>|<span data-ttu-id="e78f9-106">描述</span><span class="sxs-lookup"><span data-stu-id="e78f9-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="e78f9-107">GetFunction 方法</span><span class="sxs-lookup"><span data-stu-id="e78f9-107">GetFunction Method</span></span>](icordebugfunctionbreakpoint-getfunction-method.md)|<span data-ttu-id="e78f9-108">取得參考中斷點設定之函式的 ICorDebugFunction 介面指標。</span><span class="sxs-lookup"><span data-stu-id="e78f9-108">Gets an interface pointer to an ICorDebugFunction that references the function in which the breakpoint is set.</span></span>|  
|[<span data-ttu-id="e78f9-109">GetOffset 方法</span><span class="sxs-lookup"><span data-stu-id="e78f9-109">GetOffset Method</span></span>](icordebugfunctionbreakpoint-getoffset-method.md)|<span data-ttu-id="e78f9-110">取得函數內中斷點的位移。</span><span class="sxs-lookup"><span data-stu-id="e78f9-110">Gets the offset of the breakpoint within the function.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e78f9-111">備註</span><span class="sxs-lookup"><span data-stu-id="e78f9-111">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e78f9-112">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="e78f9-112">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e78f9-113">需求</span><span class="sxs-lookup"><span data-stu-id="e78f9-113">Requirements</span></span>  

 <span data-ttu-id="e78f9-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e78f9-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e78f9-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e78f9-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e78f9-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e78f9-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e78f9-117">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e78f9-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e78f9-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e78f9-118">See also</span></span>

- [<span data-ttu-id="e78f9-119">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="e78f9-119">Debugging Interfaces</span></span>](debugging-interfaces.md)

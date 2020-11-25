---
title: CorDebugCodeInvokeKind 列舉
ms.date: 03/30/2017
api_name:
- CorDebugCodeInvokeKind
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: e795e6a2-1008-4a81-af88-d777888e942e
topic_type:
- apiref
ms.openlocfilehash: ece5bd5373fed1a10e6592ff884e98b614e7991d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95715986"
---
# <a name="cordebugcodeinvokekind-enumeration"></a><span data-ttu-id="2ea77-102">CorDebugCodeInvokeKind 列舉</span><span class="sxs-lookup"><span data-stu-id="2ea77-102">CorDebugCodeInvokeKind Enumeration</span></span>

<span data-ttu-id="2ea77-103">描述匯出函式如何叫用 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-103">Describes how an exported function invokes managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2ea77-104">語法</span><span class="sxs-lookup"><span data-stu-id="2ea77-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugCodeInvokeKind  
{  
    CODE_INVOKE_KIND_NONE,
    CODE_INVOKE_KIND_RETURN,
    CODE_INVOKE_KIND_TAILCALL,
} CorDebugCodeInvokeKind;  
```  
  
## <a name="members"></a><span data-ttu-id="2ea77-105">成員</span><span class="sxs-lookup"><span data-stu-id="2ea77-105">Members</span></span>  
  
|<span data-ttu-id="2ea77-106">member</span><span class="sxs-lookup"><span data-stu-id="2ea77-106">Member</span></span>|<span data-ttu-id="2ea77-107">描述</span><span class="sxs-lookup"><span data-stu-id="2ea77-107">Description</span></span>|  
|------------|-----------------|  
|`CODE_INVOKE_KIND_NONE`|<span data-ttu-id="2ea77-108">如果這個方法叫用任何 Managed 程式碼，明確事件或中斷點稍後必須找到這些程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-108">If any managed code is invoked by this method, it will have to be located by explicit events or breakpoints later.</span></span><br /><br /> <span data-ttu-id="2ea77-109">-或-</span><span class="sxs-lookup"><span data-stu-id="2ea77-109">--or--</span></span><br /><br /> <span data-ttu-id="2ea77-110">我們可能只是遺漏這個方法呼叫的一些 Managed 程式碼，因為沒有簡單的方法可以在其上停止。</span><span class="sxs-lookup"><span data-stu-id="2ea77-110">We may just miss some of the managed code this method calls because there is no easy way to stop on it.</span></span><br /><br /> <span data-ttu-id="2ea77-111">-或-</span><span class="sxs-lookup"><span data-stu-id="2ea77-111">--or--</span></span><br /><br /> <span data-ttu-id="2ea77-112">這個方法可能永遠不會叫用 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-112">The method may never invoke managed code.</span></span>|  
|`CODE_INVOKE_KIND_RETURN`|<span data-ttu-id="2ea77-113">這個方法會透過傳回指令叫用 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-113">This method will invoke managed code via a return instruction.</span></span> <span data-ttu-id="2ea77-114">跳離應該會抵達下一個 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-114">Stepping out should arrive at the next managed code.</span></span>|  
|`CODE_INVOKE_KIND_TAILCALL`|<span data-ttu-id="2ea77-115">這個方法會透過 tail 呼叫叫用 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-115">This method will invoke managed code via a tail-call.</span></span> <span data-ttu-id="2ea77-116">逐步執行和不進入任何呼叫指令應該會抵達 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ea77-116">Single-stepping and stepping over any call instructions should arrive at managed code.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2ea77-117">備註</span><span class="sxs-lookup"><span data-stu-id="2ea77-117">Remarks</span></span>  

 <span data-ttu-id="2ea77-118">[ICorDebugProcess6：： GetExportStepInfo](icordebugprocess6-getexportstepinfo-method.md)方法使用這個列舉來提供逐步執行 managed 程式碼的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2ea77-118">This enumeration is used by the [ICorDebugProcess6::GetExportStepInfo](icordebugprocess6-getexportstepinfo-method.md) method to provide information about stepping through managed code.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2ea77-119">這個列舉僅適用於 .NET Native 偵錯案例。</span><span class="sxs-lookup"><span data-stu-id="2ea77-119">This enumeration is intended for use in .NET Native debugging scenarios only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2ea77-120">需求</span><span class="sxs-lookup"><span data-stu-id="2ea77-120">Requirements</span></span>  

 <span data-ttu-id="2ea77-121">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2ea77-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2ea77-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="2ea77-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="2ea77-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2ea77-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2ea77-124">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2ea77-124">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2ea77-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2ea77-125">See also</span></span>

- [<span data-ttu-id="2ea77-126">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="2ea77-126">Debugging Enumerations</span></span>](debugging-enumerations.md)
- [<span data-ttu-id="2ea77-127">偵錯</span><span class="sxs-lookup"><span data-stu-id="2ea77-127">Debugging</span></span>](index.md)

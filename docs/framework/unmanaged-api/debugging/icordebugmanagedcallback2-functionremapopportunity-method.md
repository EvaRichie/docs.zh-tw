---
title: ICorDebugManagedCallback2::FunctionRemapOpportunity 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.FunctionRemapOpportunity
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::FunctionRemapOpportunity
helpviewer_keywords:
- FunctionRemapOpportunity method [.NET Framework debugging]
- ICorDebugManagedCallback2::FunctionRemapOpportunity method [.NET Framework debugging]
ms.assetid: 0d6471bc-ad9b-4b1d-a307-c10443918863
topic_type:
- apiref
ms.openlocfilehash: 50fabec08a63d348b0a1934f029582ae1446519e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729053"
---
# <a name="icordebugmanagedcallback2functionremapopportunity-method"></a><span data-ttu-id="e663f-102">ICorDebugManagedCallback2::FunctionRemapOpportunity 方法</span><span class="sxs-lookup"><span data-stu-id="e663f-102">ICorDebugManagedCallback2::FunctionRemapOpportunity Method</span></span>

<span data-ttu-id="e663f-103">通知偵錯工具程式碼執行已在較舊版本的已編輯函式中到達序列點。</span><span class="sxs-lookup"><span data-stu-id="e663f-103">Notifies the debugger that code execution has reached a sequence point in an older version of an edited function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e663f-104">語法</span><span class="sxs-lookup"><span data-stu-id="e663f-104">Syntax</span></span>  
  
```cpp  
HRESULT FunctionRemapOpportunity (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFunction    *pOldFunction,  
    [in] ICorDebugFunction    *pNewFunction,  
    [in] ULONG32              oldILOffset  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e663f-105">參數</span><span class="sxs-lookup"><span data-stu-id="e663f-105">Parameters</span></span>  

 `pAppDomain`  
 <span data-ttu-id="e663f-106">在ICorDebugAppDomain 物件的指標，代表包含已編輯函式的應用程式域。</span><span class="sxs-lookup"><span data-stu-id="e663f-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain containing the edited function.</span></span>  
  
 `pThread`  
 <span data-ttu-id="e663f-107">在ICorDebugThread 物件的指標，代表遇到重新對應中斷點的執行緒。</span><span class="sxs-lookup"><span data-stu-id="e663f-107">[in] A pointer to an ICorDebugThread object that represents the thread on which the remap breakpoint was encountered.</span></span>  
  
 `pOldFunction`  
 <span data-ttu-id="e663f-108">在ICorDebugFunction 物件的指標，表示執行緒上目前正在執行的函式版本。</span><span class="sxs-lookup"><span data-stu-id="e663f-108">[in] A pointer to an ICorDebugFunction object that represents the version of the function that is currently running on the thread.</span></span>  
  
 `pNewFunction`  
 <span data-ttu-id="e663f-109">在ICorDebugFunction 物件的指標，該物件表示函式的最新版本。</span><span class="sxs-lookup"><span data-stu-id="e663f-109">[in] A pointer to an ICorDebugFunction object that represents the latest version of the function.</span></span>  
  
 `oldILOffset`  
 <span data-ttu-id="e663f-110">在在舊版本的函式中，Microsoft 中繼語言 (MSIL 的指令指標) 位移。</span><span class="sxs-lookup"><span data-stu-id="e663f-110">[in] The Microsoft intermediate language (MSIL) offset of the instruction pointer in the old version of the function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e663f-111">備註</span><span class="sxs-lookup"><span data-stu-id="e663f-111">Remarks</span></span>  

 <span data-ttu-id="e663f-112">此回呼會藉由呼叫 [ICorDebugILFrame2：： RemapFunction](icordebugilframe2-remapfunction-method.md) 方法，讓偵錯工具有機會將指令指標重新對應至指定之函式的新版本中的適當位置。</span><span class="sxs-lookup"><span data-stu-id="e663f-112">This callback gives the debugger an opportunity to remap the instruction pointer to its proper place in the new version of the specified function by calling the [ICorDebugILFrame2::RemapFunction](icordebugilframe2-remapfunction-method.md) method.</span></span> <span data-ttu-id="e663f-113">如果偵錯工具在 `RemapFunction` 呼叫 [ICorDebugController：： Continue](icordebugcontroller-continue-method.md) 方法之前未呼叫，則執行時間會繼續執行舊的程式碼，並且會 `FunctionRemapOpportunity` 在下一個序列點引發另一個回呼。</span><span class="sxs-lookup"><span data-stu-id="e663f-113">If the debugger does not call `RemapFunction` before calling the [ICorDebugController::Continue](icordebugcontroller-continue-method.md) method, the runtime will continue to execute the old code and will fire another `FunctionRemapOpportunity` callback at the next sequence point.</span></span>  
  
 <span data-ttu-id="e663f-114">針對執行舊版指定函式的每個框架，將會叫用此回呼，直到偵錯工具傳回 S_OK 為止。</span><span class="sxs-lookup"><span data-stu-id="e663f-114">This callback will be invoked for every frame that is executing an older version of the given function until the debugger returns S_OK.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e663f-115">需求</span><span class="sxs-lookup"><span data-stu-id="e663f-115">Requirements</span></span>  

 <span data-ttu-id="e663f-116">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e663f-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e663f-117">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e663f-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e663f-118">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e663f-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e663f-119">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e663f-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e663f-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e663f-120">See also</span></span>

- [<span data-ttu-id="e663f-121">ICorDebugManagedCallback2 介面</span><span class="sxs-lookup"><span data-stu-id="e663f-121">ICorDebugManagedCallback2 Interface</span></span>](icordebugmanagedcallback2-interface.md)
- [<span data-ttu-id="e663f-122">ICorDebugManagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="e663f-122">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

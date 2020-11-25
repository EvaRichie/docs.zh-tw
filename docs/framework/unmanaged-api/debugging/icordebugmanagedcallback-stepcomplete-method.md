---
title: ICorDebugManagedCallback::StepComplete 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.StepComplete
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::StepComplete
helpviewer_keywords:
- StepComplete method [.NET Framework debugging]
- ICorDebugManagedCallback::StepComplete method [.NET Framework debugging]
ms.assetid: 5e1f2c47-81df-4530-826d-96489cd68719
topic_type:
- apiref
ms.openlocfilehash: 8de0858abe7db9ae1225f449083e417e13507b3d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703033"
---
# <a name="icordebugmanagedcallbackstepcomplete-method"></a><span data-ttu-id="49b74-102">ICorDebugManagedCallback::StepComplete 方法</span><span class="sxs-lookup"><span data-stu-id="49b74-102">ICorDebugManagedCallback::StepComplete Method</span></span>

<span data-ttu-id="49b74-103">通知偵錯工具已完成步驟。</span><span class="sxs-lookup"><span data-stu-id="49b74-103">Notifies the debugger that a step has completed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="49b74-104">語法</span><span class="sxs-lookup"><span data-stu-id="49b74-104">Syntax</span></span>  
  
```cpp  
HRESULT StepComplete (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] ICorDebugStepper    *pStepper,  
    [in] CorDebugStepReason   reason  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="49b74-105">參數</span><span class="sxs-lookup"><span data-stu-id="49b74-105">Parameters</span></span>  

 `pAppDomain`  
 <span data-ttu-id="49b74-106">在ICorDebugAppDomain 物件的指標，該物件代表包含步驟已完成之執行緒的應用程式域。</span><span class="sxs-lookup"><span data-stu-id="49b74-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain containing the thread in which the step has completed.</span></span>  
  
 `pThread`  
 <span data-ttu-id="49b74-107">在ICorDebugThread 物件的指標，該物件表示步驟已完成的執行緒。</span><span class="sxs-lookup"><span data-stu-id="49b74-107">[in] A pointer to an ICorDebugThread object that represents the thread in which the step has completed.</span></span>  
  
 `pStepper`  
 <span data-ttu-id="49b74-108">在ICorDebugStepper 物件的指標，代表程式碼執行中的步驟。</span><span class="sxs-lookup"><span data-stu-id="49b74-108">[in] A pointer to an ICorDebugStepper object that represents the step in code execution.</span></span>  
  
 `reason`  
 <span data-ttu-id="49b74-109">在CorDebugStepReason 列舉的值，表示個別步驟的結果。</span><span class="sxs-lookup"><span data-stu-id="49b74-109">[in] A value of the CorDebugStepReason enumeration that indicates the outcome of an individual step.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="49b74-110">備註</span><span class="sxs-lookup"><span data-stu-id="49b74-110">Remarks</span></span>  

 <span data-ttu-id="49b74-111">如果需要，可以使用分檔器繼續逐步執行，除非偵錯工具已終止。</span><span class="sxs-lookup"><span data-stu-id="49b74-111">The stepper may be used to continue stepping if desired, unless the debugging is terminated.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="49b74-112">需求</span><span class="sxs-lookup"><span data-stu-id="49b74-112">Requirements</span></span>  

 <span data-ttu-id="49b74-113">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="49b74-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="49b74-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="49b74-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="49b74-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="49b74-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="49b74-116">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="49b74-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="49b74-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49b74-117">See also</span></span>

- [<span data-ttu-id="49b74-118">ICorDebugManagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="49b74-118">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

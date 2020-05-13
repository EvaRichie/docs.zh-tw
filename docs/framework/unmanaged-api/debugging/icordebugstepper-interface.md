---
title: ICorDebugStepper 介面
ms.date: 03/30/2017
api_name:
- ICorDebugStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper
helpviewer_keywords:
- ICorDebugStepper interface [.NET Framework debugging]
ms.assetid: ed8364eb-f01b-46f6-b5e3-5dda9cae2dfe
topic_type:
- apiref
ms.openlocfilehash: 622fdfa37c93e406950e73941775828ae4b112fa
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379428"
---
# <a name="icordebugstepper-interface"></a><span data-ttu-id="8079a-102">ICorDebugStepper 介面</span><span class="sxs-lookup"><span data-stu-id="8079a-102">ICorDebugStepper Interface</span></span>
<span data-ttu-id="8079a-103">表示偵錯工具在程式碼執行作業中所執行的步驟，做為命令的發出和完成之間的識別項，並可提供方法來取消步驟。</span><span class="sxs-lookup"><span data-stu-id="8079a-103">Represents a step in code execution that is performed by a debugger, serves as an identifier between the issuance and completion of a command, and provides a way to cancel a step.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="8079a-104">方法</span><span class="sxs-lookup"><span data-stu-id="8079a-104">Methods</span></span>  
  
|<span data-ttu-id="8079a-105">方法</span><span class="sxs-lookup"><span data-stu-id="8079a-105">Method</span></span>|<span data-ttu-id="8079a-106">描述</span><span class="sxs-lookup"><span data-stu-id="8079a-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="8079a-107">Deactivate 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-107">Deactivate Method</span></span>](icordebugstepper-deactivate-method.md)|<span data-ttu-id="8079a-108">導致此動作 `ICorDebugStepper` 取消所收到的最後一個步驟命令。</span><span class="sxs-lookup"><span data-stu-id="8079a-108">Causes this `ICorDebugStepper` to cancel the last step command it received.</span></span>|  
|[<span data-ttu-id="8079a-109">IsActive 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-109">IsActive Method</span></span>](icordebugstepper-isactive-method.md)|<span data-ttu-id="8079a-110">取得值，指出這個是否 `ICorDebugStepper` 目前正在執行步驟。</span><span class="sxs-lookup"><span data-stu-id="8079a-110">Gets a value that indicates whether this `ICorDebugStepper` is currently executing a step.</span></span>|  
|[<span data-ttu-id="8079a-111">SetInterceptMask 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-111">SetInterceptMask Method</span></span>](icordebugstepper-setinterceptmask-method.md)|<span data-ttu-id="8079a-112">設定 CorDebugIntercept 值，指定要逐步執行的程式碼類型。</span><span class="sxs-lookup"><span data-stu-id="8079a-112">Sets a CorDebugIntercept value that specifies the types of code that are stepped into.</span></span>|  
|[<span data-ttu-id="8079a-113">SetRangeIL 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-113">SetRangeIL Method</span></span>](icordebugstepper-setrangeil-method.md)|<span data-ttu-id="8079a-114">設定值，指出是否呼叫[ICorDebugStepper：： StepRange](icordebugstepper-steprange-method.md)傳遞引數值相對於要逐步執行之方法的原生程式碼或 Microsoft 中繼語言（MSIL）程式碼。</span><span class="sxs-lookup"><span data-stu-id="8079a-114">Sets a value that indicates whether calls to [ICorDebugStepper::StepRange](icordebugstepper-steprange-method.md) pass argument values relative to the native code or to Microsoft intermediate language (MSIL) code of the method that is being stepped through.</span></span>|  
|[<span data-ttu-id="8079a-115">SetUnmappedStopMask 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-115">SetUnmappedStopMask Method</span></span>](icordebugstepper-setunmappedstopmask-method.md)|<span data-ttu-id="8079a-116">設定 CorDebugUnmappedStop 值，指定將暫停執行的未對應程式碼類型。</span><span class="sxs-lookup"><span data-stu-id="8079a-116">Sets a CorDebugUnmappedStop value that specifies the type of unmapped code in which execution will halt.</span></span>|  
|[<span data-ttu-id="8079a-117">Step 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-117">Step Method</span></span>](icordebugstepper-step-method.md)|<span data-ttu-id="8079a-118">會使此動作逐步 `ICorDebugStepper` 執行其包含的執行緒，並選擇性地繼續透過線上程內呼叫的函式進行單一逐步執行。</span><span class="sxs-lookup"><span data-stu-id="8079a-118">Causes this `ICorDebugStepper` to single-step through its containing thread, and optionally, to continue single-stepping through functions that are called within the thread.</span></span>|  
|[<span data-ttu-id="8079a-119">StepOut 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-119">StepOut Method</span></span>](icordebugstepper-stepout-method.md)|<span data-ttu-id="8079a-120">使此動作逐步 `ICorDebugStepper` 執行其包含的執行緒，並在目前的框架將控制項傳回至呼叫的框架時完成。</span><span class="sxs-lookup"><span data-stu-id="8079a-120">Causes this `ICorDebugStepper` to single-step through its containing thread, and to complete when the current frame returns control to the calling frame.</span></span>|  
|[<span data-ttu-id="8079a-121">StepRange 方法</span><span class="sxs-lookup"><span data-stu-id="8079a-121">StepRange Method</span></span>](icordebugstepper-steprange-method.md)|<span data-ttu-id="8079a-122">使此動作逐步 `ICorDebugStepper` 執行其包含的執行緒，並在到達超出指定範圍的最後一個程式碼時傳回。</span><span class="sxs-lookup"><span data-stu-id="8079a-122">Causes this `ICorDebugStepper` to single-step through its containing thread, and to return when it reaches code beyond the last of the specified ranges.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8079a-123">備註</span><span class="sxs-lookup"><span data-stu-id="8079a-123">Remarks</span></span>  
 <span data-ttu-id="8079a-124">`ICorDebugStepper`介面有下列用途：</span><span class="sxs-lookup"><span data-stu-id="8079a-124">The `ICorDebugStepper` interface serves the following purposes:</span></span>  
  
- <span data-ttu-id="8079a-125">它會做為所發出的步驟命令和該命令完成之間的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8079a-125">It acts as an identifier between a step command that is issued and the completion of that command.</span></span>  
  
- <span data-ttu-id="8079a-126">它提供一個中央介面來封裝可執行檔所有逐步執行。</span><span class="sxs-lookup"><span data-stu-id="8079a-126">It provides a central interface to encapsulate all the stepping that can be performed.</span></span>  
  
- <span data-ttu-id="8079a-127">它提供了一種方法，可讓您提前取消逐步操作。</span><span class="sxs-lookup"><span data-stu-id="8079a-127">It provides a way to prematurely cancel a stepping operation.</span></span>  
  
 <span data-ttu-id="8079a-128">每個執行緒可以有一個以上的分檔器。</span><span class="sxs-lookup"><span data-stu-id="8079a-128">There can be more than one stepper per thread.</span></span> <span data-ttu-id="8079a-129">例如，在逐步執行函式時，可能會叫用中斷點，而且使用者可能會想要在該函式內啟動新的逐步操作。</span><span class="sxs-lookup"><span data-stu-id="8079a-129">For example, a breakpoint may be hit while stepping over a function, and the user may wish to start a new stepping operation inside that function.</span></span> <span data-ttu-id="8079a-130">偵錯工具會決定如何處理這種情況。</span><span class="sxs-lookup"><span data-stu-id="8079a-130">It is up to the debugger to determine how to handle this situation.</span></span> <span data-ttu-id="8079a-131">偵錯工具可能會想要取消原始的逐步執行作業，或將兩個運算加以嵌套。</span><span class="sxs-lookup"><span data-stu-id="8079a-131">The debugger may want to cancel the original stepping operation or nest the two operations.</span></span> <span data-ttu-id="8079a-132">`ICorDebugStepper`介面支援這兩種選擇。</span><span class="sxs-lookup"><span data-stu-id="8079a-132">The `ICorDebugStepper` interface supports both choices.</span></span>  
  
 <span data-ttu-id="8079a-133">如果 common language runtime （CLR）進行跨執行緒、封送處理的呼叫，則分檔器可以線上程之間進行遷移。</span><span class="sxs-lookup"><span data-stu-id="8079a-133">A stepper may migrate between threads if the common language runtime (CLR) makes a cross-threaded, marshaled call.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8079a-134">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="8079a-134">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8079a-135">需求</span><span class="sxs-lookup"><span data-stu-id="8079a-135">Requirements</span></span>  
 <span data-ttu-id="8079a-136">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8079a-136">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8079a-137">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="8079a-137">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="8079a-138">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="8079a-138">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8079a-139">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8079a-139">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8079a-140">請參閱</span><span class="sxs-lookup"><span data-stu-id="8079a-140">See also</span></span>

- [<span data-ttu-id="8079a-141">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="8079a-141">Debugging Interfaces</span></span>](debugging-interfaces.md)

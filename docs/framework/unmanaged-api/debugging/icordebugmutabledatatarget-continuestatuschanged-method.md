---
title: ICorDebugMutableDataTarget::ContinueStatusChanged 方法
ms.date: 03/30/2017
ms.assetid: 5a66d3f4-dd16-4d62-9dcc-0eab7041d894
ms.openlocfilehash: 4910b125c2344505128a6979dfe4c9fad2b72c19
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95695786"
---
# <a name="icordebugmutabledatatargetcontinuestatuschanged-method"></a><span data-ttu-id="114e0-102">ICorDebugMutableDataTarget::ContinueStatusChanged 方法</span><span class="sxs-lookup"><span data-stu-id="114e0-102">ICorDebugMutableDataTarget::ContinueStatusChanged Method</span></span>

<span data-ttu-id="114e0-103">變更指定執行緒上未處理之偵錯事件的接續狀態。</span><span class="sxs-lookup"><span data-stu-id="114e0-103">Changes the continuation status for the outstanding debug event on the specified thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="114e0-104">語法</span><span class="sxs-lookup"><span data-stu-id="114e0-104">Syntax</span></span>  
  
```cpp  
HRESULT ContinueStatusChanged(  
   [in] DWORD dwThreadId,  
   [in] CORDB_CONTINUE_STATUS continueStatus);  
```  
  
## <a name="parameters"></a><span data-ttu-id="114e0-105">參數</span><span class="sxs-lookup"><span data-stu-id="114e0-105">Parameters</span></span>  

 `dwThreadId`  
 <span data-ttu-id="114e0-106">作業系統定義的執行緒識別項。</span><span class="sxs-lookup"><span data-stu-id="114e0-106">The operating system-defined thread identifier.</span></span>  
  
 `continueStatus`  
 <span data-ttu-id="114e0-107">[COREDB_CONTINUE_STATUS](../common-data-types-unmanaged-api-reference.md) 值，代表新要求的接續狀態。</span><span class="sxs-lookup"><span data-stu-id="114e0-107">A [COREDB_CONTINUE_STATUS](../common-data-types-unmanaged-api-reference.md) value that represents the new requested continuation status.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="114e0-108">備註</span><span class="sxs-lookup"><span data-stu-id="114e0-108">Remarks</span></span>  

 <span data-ttu-id="114e0-109">當偵錯工具呼叫 ICorDebug 方法時，如果該方法處理目前偵錯事件的方式可能與正常處理方式不同，則會呼叫 `ContinueStatusChanged` 方法。</span><span class="sxs-lookup"><span data-stu-id="114e0-109">The debugger calls the `ContinueStatusChanged` method when it calls an ICorDebug method that requires the current debug event to be handled in a way that is potentially different from the way in which it normally would be handled.</span></span> <span data-ttu-id="114e0-110">例如，如果有未處理的例外狀況，並且偵錯工具要求取消例外狀況的作業 (例如 [ICorDebugILFrame::SetIP](icordebugilframe-setip-method.md) 或 `FuncEval`)，則會使用這個應用程式開發介面來要求取消例外狀況。</span><span class="sxs-lookup"><span data-stu-id="114e0-110">For example, if there is an outstanding exception, and the debugger requests an operation that would cancel the exception (such as [ICorDebugILFrame::SetIP](icordebugilframe-setip-method.md) or `FuncEval`), this API is used to request that the exception be cancelled.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="114e0-111">需求</span><span class="sxs-lookup"><span data-stu-id="114e0-111">Requirements</span></span>  

 <span data-ttu-id="114e0-112">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="114e0-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="114e0-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="114e0-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="114e0-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="114e0-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="114e0-115">**.NET Framework 版本：**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="114e0-115">**.NET Framework Versions:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="114e0-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="114e0-116">See also</span></span>

- [<span data-ttu-id="114e0-117">ICorDebugMutableDataTarget 介面</span><span class="sxs-lookup"><span data-stu-id="114e0-117">ICorDebugMutableDataTarget Interface</span></span>](icordebugmutabledatatarget-interface.md)
- [<span data-ttu-id="114e0-118">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="114e0-118">Debugging Interfaces</span></span>](debugging-interfaces.md)

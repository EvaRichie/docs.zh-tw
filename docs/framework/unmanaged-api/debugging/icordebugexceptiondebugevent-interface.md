---
title: ICorDebugExceptionDebugEvent 介面
ms.date: 03/30/2017
ms.assetid: f9ba60d8-b54d-417e-bb3e-fde4b41ca44c
ms.openlocfilehash: dfa65aa1b63c996068e75ff1165111d5fcfe77eb
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976001"
---
# <a name="icordebugexceptiondebugevent-interface"></a><span data-ttu-id="6139d-102">ICorDebugExceptionDebugEvent 介面</span><span class="sxs-lookup"><span data-stu-id="6139d-102">ICorDebugExceptionDebugEvent Interface</span></span>
<span data-ttu-id="6139d-103">擴充[ICorDebugDebugEvent](icordebugdebugevent-interface.md)介面，以支援例外狀況事件。</span><span class="sxs-lookup"><span data-stu-id="6139d-103">Extends the [ICorDebugDebugEvent](icordebugdebugevent-interface.md) interface to support exception events.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="6139d-104">方法</span><span class="sxs-lookup"><span data-stu-id="6139d-104">Methods</span></span>  
  
|<span data-ttu-id="6139d-105">方法</span><span class="sxs-lookup"><span data-stu-id="6139d-105">Method</span></span>|<span data-ttu-id="6139d-106">描述</span><span class="sxs-lookup"><span data-stu-id="6139d-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="6139d-107">GetFlags 方法</span><span class="sxs-lookup"><span data-stu-id="6139d-107">GetFlags Method</span></span>](icordebugexceptiondebugevent-getflags-method.md)|<span data-ttu-id="6139d-108">取得指出例外狀況是否可以被攔截的旗標。</span><span class="sxs-lookup"><span data-stu-id="6139d-108">Gets a flag that indicates whether the exception is can be intercepted.</span></span>|  
|[<span data-ttu-id="6139d-109">GetNativeIP 方法</span><span class="sxs-lookup"><span data-stu-id="6139d-109">GetNativeIP Method</span></span>](icordebugexceptiondebugevent-getnativeip-method.md)|<span data-ttu-id="6139d-110">取得這個例外狀況偵錯事件的原生介面指標。</span><span class="sxs-lookup"><span data-stu-id="6139d-110">Gets the native interface pointer for this exception debug event.</span></span>|  
|[<span data-ttu-id="6139d-111">GetStackPointer 方法</span><span class="sxs-lookup"><span data-stu-id="6139d-111">GetStackPointer Method</span></span>](icordebugexceptiondebugevent-getstackpointer-method.md)|<span data-ttu-id="6139d-112">取得這個例外狀況偵錯事件的堆疊指標。</span><span class="sxs-lookup"><span data-stu-id="6139d-112">Gets the stack pointer for this exception debug event.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="6139d-113">備註</span><span class="sxs-lookup"><span data-stu-id="6139d-113">Remarks</span></span>  
 <span data-ttu-id="6139d-114">`ICorDebugExceptionDebugEvent` 介面由下列事件類型實作：</span><span class="sxs-lookup"><span data-stu-id="6139d-114">The `ICorDebugExceptionDebugEvent` interface is implemented by the following event types:</span></span>  
  
- [<span data-ttu-id="6139d-115">MANAGED_EXCEPTION_FIRST_CHANCE</span><span class="sxs-lookup"><span data-stu-id="6139d-115">MANAGED_EXCEPTION_FIRST_CHANCE</span></span>](cordebugrecordformat-enumeration.md)  
  
- [<span data-ttu-id="6139d-116">MANAGED_EXCEPTION_USER_FIRST_CHANCE</span><span class="sxs-lookup"><span data-stu-id="6139d-116">MANAGED_EXCEPTION_USER_FIRST_CHANCE</span></span>](cordebugrecordformat-enumeration.md)  
  
- [<span data-ttu-id="6139d-117">MANAGED_EXCEPTION_CATCH_HANDLER_FOUND</span><span class="sxs-lookup"><span data-stu-id="6139d-117">MANAGED_EXCEPTION_CATCH_HANDLER_FOUND</span></span>](cordebugrecordformat-enumeration.md)  
  
- [<span data-ttu-id="6139d-118">MANAGED_EXCEPTION_UNHANDLED</span><span class="sxs-lookup"><span data-stu-id="6139d-118">MANAGED_EXCEPTION_UNHANDLED</span></span>](cordebugrecordformat-enumeration.md)  
  
> [!NOTE]
> <span data-ttu-id="6139d-119">這個介面僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="6139d-119">The interface is available with .NET Native only.</span></span> <span data-ttu-id="6139d-120">嘗試在 .NET 原生之外的 ICorDebug 案例中呼叫 `QueryInterface` 以擷取介面指標，會傳回 `E_NOINTERFACE`。</span><span class="sxs-lookup"><span data-stu-id="6139d-120">Attempting to call `QueryInterface` to retrieve an interface pointer returns `E_NOINTERFACE` for ICorDebug scenarios outside of .NET Native.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6139d-121">需求</span><span class="sxs-lookup"><span data-stu-id="6139d-121">Requirements</span></span>  
 <span data-ttu-id="6139d-122">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6139d-122">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6139d-123">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="6139d-123">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="6139d-124">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6139d-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6139d-125">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6139d-125">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6139d-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6139d-126">See also</span></span>

- [<span data-ttu-id="6139d-127">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="6139d-127">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="6139d-128">偵錯</span><span class="sxs-lookup"><span data-stu-id="6139d-128">Debugging</span></span>](index.md)

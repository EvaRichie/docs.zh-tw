---
title: ICorDebugDataTarget2::CreateVirtualUnwinder 方法
ms.date: 03/30/2017
ms.assetid: 354c8b4c-7d23-45c6-a7d7-3be4c2a5b772
ms.openlocfilehash: 7a479fba9bbcf28c60474fffc6219af23e62c251
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976495"
---
# <a name="icordebugdatatarget2createvirtualunwinder-method"></a><span data-ttu-id="25d41-102">ICorDebugDataTarget2::CreateVirtualUnwinder 方法</span><span class="sxs-lookup"><span data-stu-id="25d41-102">ICorDebugDataTarget2::CreateVirtualUnwinder Method</span></span>
<span data-ttu-id="25d41-103">建立新的堆疊 unwinder，以從初始內容 (不一定是執行緒的分葉) 開始回溯。</span><span class="sxs-lookup"><span data-stu-id="25d41-103">Creates a new stack unwinder that starts unwinding from an initial context (which isn't necessarily the leaf of a thread).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="25d41-104">語法</span><span class="sxs-lookup"><span data-stu-id="25d41-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateVirtualUnwinder(  
    [in] DWORD nativeThreadID,  
    [in] ULONG32 contextFlags,  
    [in] ULONG32 cbContext,  
    [in, size_is(cbContext)] BYTE initialContext[],  
    [out] ICorDebugVirtualUnwinder ** ppUnwinder);  
};  
```  
  
## <a name="parameters"></a><span data-ttu-id="25d41-105">參數</span><span class="sxs-lookup"><span data-stu-id="25d41-105">Parameters</span></span>  
 <span data-ttu-id="25d41-106">nativeThreadID</span><span class="sxs-lookup"><span data-stu-id="25d41-106">nativeThreadID</span></span>  
 <span data-ttu-id="25d41-107">[in] 其堆疊未回溯之執行緒的原生執行緒 ID。</span><span class="sxs-lookup"><span data-stu-id="25d41-107">[in] The native thread ID of the thread whose stack is to be unwound.</span></span>  
  
 <span data-ttu-id="25d41-108">contextFlags</span><span class="sxs-lookup"><span data-stu-id="25d41-108">contextFlags</span></span>  
 <span data-ttu-id="25d41-109">[in] 指定哪些內容部分會在 `initialContext` 中定義的旗標。</span><span class="sxs-lookup"><span data-stu-id="25d41-109">[in] Flags that specify which parts of the context are defined in `initialContext`.</span></span>  
  
 <span data-ttu-id="25d41-110">cbContext</span><span class="sxs-lookup"><span data-stu-id="25d41-110">cbContext</span></span>  
 <span data-ttu-id="25d41-111">[in] `initialContext` 的大小。</span><span class="sxs-lookup"><span data-stu-id="25d41-111">[in] The size of `initialContext`.</span></span>  
  
 <span data-ttu-id="25d41-112">initialContext</span><span class="sxs-lookup"><span data-stu-id="25d41-112">initialContext</span></span>  
 <span data-ttu-id="25d41-113">[in] 內容中的資料。</span><span class="sxs-lookup"><span data-stu-id="25d41-113">[in] The data in the context.</span></span>  
  
 <span data-ttu-id="25d41-114">ppUnwinder</span><span class="sxs-lookup"><span data-stu-id="25d41-114">ppUnwinder</span></span>  
 <span data-ttu-id="25d41-115">[out] ICorDebugVirtualUnwinder 介面物件的位址指標。</span><span class="sxs-lookup"><span data-stu-id="25d41-115">[out] A pointer to the address of an ICorDebugVirtualUnwinder interface object.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="25d41-116">傳回值</span><span class="sxs-lookup"><span data-stu-id="25d41-116">Return Value</span></span>  
 <span data-ttu-id="25d41-117">如果成功，則為 `S_OK`。</span><span class="sxs-lookup"><span data-stu-id="25d41-117">`S_OK` if successful.</span></span> <span data-ttu-id="25d41-118">其他任何 `HRESULT` 表示失敗。</span><span class="sxs-lookup"><span data-stu-id="25d41-118">Any other `HRESULT` indicates failure.</span></span> <span data-ttu-id="25d41-119">Mscordbi.dll 收到`HRESULT`的任何失敗都會被視為嚴重錯誤，並導致[ICorDebug](icordebug-interface.md)方法傳回`CORDBG_E_DATA_TARGET_ERROR`。</span><span class="sxs-lookup"><span data-stu-id="25d41-119">Any failing `HRESULT` received by mscordbi is considered fatal and causes [ICorDebug](icordebug-interface.md) methods to return `CORDBG_E_DATA_TARGET_ERROR`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="25d41-120">備註</span><span class="sxs-lookup"><span data-stu-id="25d41-120">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="25d41-121">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="25d41-121">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="25d41-122">需求</span><span class="sxs-lookup"><span data-stu-id="25d41-122">Requirements</span></span>  
 <span data-ttu-id="25d41-123">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="25d41-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="25d41-124">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="25d41-124">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="25d41-125">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="25d41-125">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="25d41-126">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="25d41-126">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="25d41-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="25d41-127">See also</span></span>

- [<span data-ttu-id="25d41-128">ICorDebugDataTarget2 介面</span><span class="sxs-lookup"><span data-stu-id="25d41-128">ICorDebugDataTarget2 Interface</span></span>](icordebugdatatarget2-interface.md)
- [<span data-ttu-id="25d41-129">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="25d41-129">Debugging Interfaces</span></span>](debugging-interfaces.md)

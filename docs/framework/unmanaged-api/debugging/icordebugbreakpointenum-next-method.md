---
title: ICorDebugBreakpointEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpointEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpointEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBreakpointEnum interface [.NET Framework debugging]
- ICorDebugBreakpointEnum::Next method [.NET Framework debugging]
ms.assetid: 2e6bbaea-79ba-448c-a0e3-7c90fc7c2939
topic_type:
- apiref
ms.openlocfilehash: 14c89e808ea8e41bbee46a59a60bc1876f3800d2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730184"
---
# <a name="icordebugbreakpointenumnext-method"></a><span data-ttu-id="a90d2-102">ICorDebugBreakpointEnum::Next 方法</span><span class="sxs-lookup"><span data-stu-id="a90d2-102">ICorDebugBreakpointEnum::Next Method</span></span>

<span data-ttu-id="a90d2-103">從目前位置開始，取得列舉中指定的 ICorDebugBreakpoint 實例數目。</span><span class="sxs-lookup"><span data-stu-id="a90d2-103">Gets the specified number of ICorDebugBreakpoint instances from the enumeration, starting at the current position.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a90d2-104">語法</span><span class="sxs-lookup"><span data-stu-id="a90d2-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (  
    [in] ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugBreakpoint *breakpoints[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a90d2-105">參數</span><span class="sxs-lookup"><span data-stu-id="a90d2-105">Parameters</span></span>  

 `celt`  
 <span data-ttu-id="a90d2-106">在 `ICorDebugBreakpoint` 要取出的實例數目。</span><span class="sxs-lookup"><span data-stu-id="a90d2-106">[in] The number of `ICorDebugBreakpoint` instances to be retrieved.</span></span>  
  
 `breakpoints`  
 <span data-ttu-id="a90d2-107">擴展指標的陣列，每個指標 `ICorDebugBreakpoint` 都會指向代表中斷點的物件。</span><span class="sxs-lookup"><span data-stu-id="a90d2-107">[out] An array of pointers, each of which points to an `ICorDebugBreakpoint` object that represents a breakpoint.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="a90d2-108">擴展實際傳回之實例數目的指標 `ICorDebugBreakpoint` 。</span><span class="sxs-lookup"><span data-stu-id="a90d2-108">[out] A pointer to the number of `ICorDebugBreakpoint` instances actually returned.</span></span> <span data-ttu-id="a90d2-109">如果是1，則這個值可能是 null `celt` 。</span><span class="sxs-lookup"><span data-stu-id="a90d2-109">This value may be null if `celt` is one.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a90d2-110">需求</span><span class="sxs-lookup"><span data-stu-id="a90d2-110">Requirements</span></span>  

 <span data-ttu-id="a90d2-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a90d2-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a90d2-112">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a90d2-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a90d2-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a90d2-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a90d2-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a90d2-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

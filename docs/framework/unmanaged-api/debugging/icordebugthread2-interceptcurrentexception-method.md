---
title: ICorDebugThread2::InterceptCurrentException 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.InterceptCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::InterceptCurrentException
helpviewer_keywords:
- InterceptCurrentException method [.NET Framework debugging]
- ICorDebugThread2::InterceptCurrentException method [.NET Framework debugging]
ms.assetid: 536d2357-1b97-49e0-a10c-c860aed74e6e
topic_type:
- apiref
ms.openlocfilehash: 96e3a90bcb7700915bfd3618d7bae40c0ff64a75
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95678593"
---
# <a name="icordebugthread2interceptcurrentexception-method"></a><span data-ttu-id="80fc4-102">ICorDebugThread2::InterceptCurrentException 方法</span><span class="sxs-lookup"><span data-stu-id="80fc4-102">ICorDebugThread2::InterceptCurrentException Method</span></span>

<span data-ttu-id="80fc4-103">允許偵錯工具攔截這個執行緒上目前的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="80fc4-103">Allows a debugger to intercept the current exception on this thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="80fc4-104">語法</span><span class="sxs-lookup"><span data-stu-id="80fc4-104">Syntax</span></span>  
  
```cpp  
HRESULT InterceptCurrentException (  
    [in] ICorDebugFrame  *pFrame  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="80fc4-105">參數</span><span class="sxs-lookup"><span data-stu-id="80fc4-105">Parameters</span></span>  

 `pFrame`  
 <span data-ttu-id="80fc4-106">在代表使用中堆疊框架之 ICorDebugFrame 的指標。</span><span class="sxs-lookup"><span data-stu-id="80fc4-106">[in] A pointer to an ICorDebugFrame that represents the active stack frame.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="80fc4-107">備註</span><span class="sxs-lookup"><span data-stu-id="80fc4-107">Remarks</span></span>  

 <span data-ttu-id="80fc4-108">您 `InterceptCurrentException` 可以在例外狀況回呼 ([ICorDebugManagedCallback：： Exception](icordebugmanagedcallback-exception-method.md) 或 [ICorDebugManagedCallback2：： exception](icordebugmanagedcallback2-exception-method.md)) 以及相關聯的 [ICorDebugController：： Continue](icordebugcontroller-continue-method.md)呼叫之間呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="80fc4-108">The `InterceptCurrentException` method can be called between an exception callback ([ICorDebugManagedCallback::Exception](icordebugmanagedcallback-exception-method.md) or [ICorDebugManagedCallback2::Exception](icordebugmanagedcallback2-exception-method.md)) and the associated call to [ICorDebugController::Continue](icordebugcontroller-continue-method.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="80fc4-109">需求</span><span class="sxs-lookup"><span data-stu-id="80fc4-109">Requirements</span></span>  

 <span data-ttu-id="80fc4-110">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="80fc4-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="80fc4-111">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="80fc4-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="80fc4-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="80fc4-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="80fc4-113">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="80fc4-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>

---
title: CorDebugStepReason 列舉
ms.date: 03/30/2017
api_name:
- CorDebugStepReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugStepReason
helpviewer_keywords:
- CorDebugStepReason enumeration [.NET Framework debugging]
ms.assetid: fe248069-b33c-48e1-a777-06ac9b239c54
topic_type:
- apiref
ms.openlocfilehash: 288d7bfdf18be5cef032227c537032966fa68df4
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795699"
---
# <a name="cordebugstepreason-enumeration"></a><span data-ttu-id="f42bd-102">CorDebugStepReason 列舉</span><span class="sxs-lookup"><span data-stu-id="f42bd-102">CorDebugStepReason Enumeration</span></span>
<span data-ttu-id="f42bd-103">指出個別步驟的結果。</span><span class="sxs-lookup"><span data-stu-id="f42bd-103">Indicates the outcome of an individual step.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f42bd-104">語法</span><span class="sxs-lookup"><span data-stu-id="f42bd-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugStepReason {  
    STEP_NORMAL,  
    STEP_RETURN,  
    STEP_CALL,  
    STEP_EXCEPTION_FILTER,  
    STEP_EXCEPTION_HANDLER,  
    STEP_INTERCEPT,  
    STEP_EXIT  
} CorDebugStepReason;  
```  
  
## <a name="members"></a><span data-ttu-id="f42bd-105">成員</span><span class="sxs-lookup"><span data-stu-id="f42bd-105">Members</span></span>  
  
|<span data-ttu-id="f42bd-106">member</span><span class="sxs-lookup"><span data-stu-id="f42bd-106">Member</span></span>|<span data-ttu-id="f42bd-107">說明</span><span class="sxs-lookup"><span data-stu-id="f42bd-107">Description</span></span>|  
|------------|-----------------|  
|`STEP_NORMAL`|<span data-ttu-id="f42bd-108">在相同的函式中，以正常方式完成逐步執行。</span><span class="sxs-lookup"><span data-stu-id="f42bd-108">Stepping completed normally, within the same function.</span></span>|  
|`STEP_RETURN`|<span data-ttu-id="f42bd-109">在函式傳回之後，逐步執行正常。</span><span class="sxs-lookup"><span data-stu-id="f42bd-109">Stepping continued normally, after the function returned.</span></span>|  
|`STEP_CALL`|<span data-ttu-id="f42bd-110">在新呼叫函式的開頭，正常地繼續執行。</span><span class="sxs-lookup"><span data-stu-id="f42bd-110">Stepping continued normally, at the beginning of a newly called function.</span></span>|  
|`STEP_EXCEPTION_FILTER`|<span data-ttu-id="f42bd-111">產生例外狀況，並將控制權傳遞給例外狀況篩選準則。</span><span class="sxs-lookup"><span data-stu-id="f42bd-111">An exception was generated and control was passed to an exception filter.</span></span>|  
|`STEP_EXCEPTION_HANDLER`|<span data-ttu-id="f42bd-112">產生例外狀況，並將控制權傳遞給例外狀況處理常式。</span><span class="sxs-lookup"><span data-stu-id="f42bd-112">An exception was generated and control was passed to an exception handler.</span></span>|  
|`STEP_INTERCEPT`|<span data-ttu-id="f42bd-113">控制項已傳遞至攔截器。</span><span class="sxs-lookup"><span data-stu-id="f42bd-113">Control was passed to an interceptor.</span></span>|  
|`STEP_EXIT`|<span data-ttu-id="f42bd-114">執行緒已在步驟完成前結束。</span><span class="sxs-lookup"><span data-stu-id="f42bd-114">The thread exited before the step was completed.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="f42bd-115">需求</span><span class="sxs-lookup"><span data-stu-id="f42bd-115">Requirements</span></span>  
 <span data-ttu-id="f42bd-116">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f42bd-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f42bd-117">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f42bd-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f42bd-118">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f42bd-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f42bd-119">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f42bd-119">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f42bd-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="f42bd-120">See also</span></span>

- [<span data-ttu-id="f42bd-121">StepComplete 方法</span><span class="sxs-lookup"><span data-stu-id="f42bd-121">StepComplete Method</span></span>](icordebugmanagedcallback-stepcomplete-method.md)
- [<span data-ttu-id="f42bd-122">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="f42bd-122">Debugging Enumerations</span></span>](debugging-enumerations.md)

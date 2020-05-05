---
title: CorDebugExceptionCallbackType 列舉
ms.date: 03/30/2017
api_name:
- CorDebugExceptionCallbackType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugExceptionCallbackType
helpviewer_keywords:
- CorDebugExceptionCallbackType enumeration [.NET Framework debugging]
ms.assetid: 4d946ad4-3c19-42cb-bec9-8633325ba769
topic_type:
- apiref
ms.openlocfilehash: d5cdb8c6740970f6a7469be8c763961bf76d6ecc
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795934"
---
# <a name="cordebugexceptioncallbacktype-enumeration"></a><span data-ttu-id="c8174-102">CorDebugExceptionCallbackType 列舉</span><span class="sxs-lookup"><span data-stu-id="c8174-102">CorDebugExceptionCallbackType Enumeration</span></span>
<span data-ttu-id="c8174-103">表示從[ICorDebugManagedCallback2：： Exception](icordebugmanagedcallback2-exception-method.md)事件進行的回呼類型。</span><span class="sxs-lookup"><span data-stu-id="c8174-103">Indicates the type of callback that is made from an [ICorDebugManagedCallback2::Exception](icordebugmanagedcallback2-exception-method.md) event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c8174-104">語法</span><span class="sxs-lookup"><span data-stu-id="c8174-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugExceptionCallbackType {  
    DEBUG_EXCEPTION_FIRST_CHANCE         = 1,  
    DEBUG_EXCEPTION_USER_FIRST_CHANCE    = 2,  
    DEBUG_EXCEPTION_CATCH_HANDLER_FOUND  = 3,  
    DEBUG_EXCEPTION_UNHANDLED            = 4  
} CorDebugExceptionCallbackType;  
```  
  
## <a name="members"></a><span data-ttu-id="c8174-105">成員</span><span class="sxs-lookup"><span data-stu-id="c8174-105">Members</span></span>  
  
|<span data-ttu-id="c8174-106">member</span><span class="sxs-lookup"><span data-stu-id="c8174-106">Member</span></span>|<span data-ttu-id="c8174-107">說明</span><span class="sxs-lookup"><span data-stu-id="c8174-107">Description</span></span>|  
|------------|-----------------|  
|`DEBUG_EXCEPTION_FIRST_CHANCE`|<span data-ttu-id="c8174-108">擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c8174-108">An exception was thrown.</span></span>|  
|`DEBUG_EXCEPTION_USER_FIRST_CHANCE`|<span data-ttu-id="c8174-109">例外狀況 windup 處理常式已進入使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8174-109">The exception windup process entered user code.</span></span>|  
|`DEBUG_EXCEPTION_CATCH_HANDLER_FOUND`|<span data-ttu-id="c8174-110">例外狀況 windup 進程在使用者`catch`程式碼中發現區塊。</span><span class="sxs-lookup"><span data-stu-id="c8174-110">The exception windup process found a `catch` block in user code.</span></span>|  
|`DEBUG_EXCEPTION_UNHANDLED`|<span data-ttu-id="c8174-111">未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c8174-111">The exception was not handled.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c8174-112">需求</span><span class="sxs-lookup"><span data-stu-id="c8174-112">Requirements</span></span>  
 <span data-ttu-id="c8174-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c8174-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c8174-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="c8174-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="c8174-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c8174-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c8174-116">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c8174-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c8174-117">請參閱</span><span class="sxs-lookup"><span data-stu-id="c8174-117">See also</span></span>

- [<span data-ttu-id="c8174-118">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="c8174-118">Debugging Enumerations</span></span>](debugging-enumerations.md)

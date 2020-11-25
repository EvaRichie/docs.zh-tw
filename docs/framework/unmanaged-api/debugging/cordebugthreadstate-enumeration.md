---
title: CorDebugThreadState 列舉
ms.date: 03/30/2017
api_name:
- CorDebugThreadState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugThreadState
helpviewer_keywords:
- CorDebugThreadState enumeration [.NET Framework debugging]
ms.assetid: a3ccdf18-4ec6-494d-9024-48e5c8c724f5
topic_type:
- apiref
ms.openlocfilehash: 5eee2aee5873fe512136bc5407e395acdc31af29
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722605"
---
# <a name="cordebugthreadstate-enumeration"></a><span data-ttu-id="000d4-102">CorDebugThreadState 列舉</span><span class="sxs-lookup"><span data-stu-id="000d4-102">CorDebugThreadState Enumeration</span></span>

<span data-ttu-id="000d4-103">指定要偵錯的執行緒狀態。</span><span class="sxs-lookup"><span data-stu-id="000d4-103">Specifies the state of a thread for debugging.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="000d4-104">語法</span><span class="sxs-lookup"><span data-stu-id="000d4-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugThreadState {  
    THREAD_RUN,  
    THREAD_SUSPEND  
} CorDebugThreadState;  
```  
  
## <a name="members"></a><span data-ttu-id="000d4-105">成員</span><span class="sxs-lookup"><span data-stu-id="000d4-105">Members</span></span>  
  
|<span data-ttu-id="000d4-106">member</span><span class="sxs-lookup"><span data-stu-id="000d4-106">Member</span></span>|<span data-ttu-id="000d4-107">描述</span><span class="sxs-lookup"><span data-stu-id="000d4-107">Description</span></span>|  
|------------|-----------------|  
|`THREAD_RUN`|<span data-ttu-id="000d4-108">除非發生 debug 事件，否則執行緒會自由執行。</span><span class="sxs-lookup"><span data-stu-id="000d4-108">The thread runs freely, unless a debug event occurs.</span></span>|  
|`THREAD_SUSPEND`|<span data-ttu-id="000d4-109">執行緒無法執行。</span><span class="sxs-lookup"><span data-stu-id="000d4-109">The thread cannot run.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="000d4-110">備註</span><span class="sxs-lookup"><span data-stu-id="000d4-110">Remarks</span></span>  

 <span data-ttu-id="000d4-111">偵錯工具會使用 `CorDebugThreadState` 列舉來控制執行緒的執行。</span><span class="sxs-lookup"><span data-stu-id="000d4-111">The debugger uses the `CorDebugThreadState` enumeration to control a thread's execution.</span></span> <span data-ttu-id="000d4-112">您可以使用 [ICorDebugThread：： SetDebugState](icordebugthread-setdebugstate-method.md) 或 [ICorDebugController：： SetAllThreadsDebugState](icordebugcontroller-setallthreadsdebugstate-method.md) 方法來設定執行緒的狀態。</span><span class="sxs-lookup"><span data-stu-id="000d4-112">The state of a thread can be set by using the [ICorDebugThread::SetDebugState](icordebugthread-setdebugstate-method.md) or [ICorDebugController::SetAllThreadsDebugState](icordebugcontroller-setallthreadsdebugstate-method.md) method.</span></span>  
  
 <span data-ttu-id="000d4-113">提供給 [裝載 API](../hosting/index.md) 的回呼會啟用訊息提取，因此不需要中斷的狀態。</span><span class="sxs-lookup"><span data-stu-id="000d4-113">A callback provided to the [hosting API](../hosting/index.md) enables message pumping, so an interrupted state is not needed.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="000d4-114">需求</span><span class="sxs-lookup"><span data-stu-id="000d4-114">Requirements</span></span>  

 <span data-ttu-id="000d4-115">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="000d4-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="000d4-116">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="000d4-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="000d4-117">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="000d4-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="000d4-118">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="000d4-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="000d4-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="000d4-119">See also</span></span>

- [<span data-ttu-id="000d4-120">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="000d4-120">Debugging Enumerations</span></span>](debugging-enumerations.md)

---
title: CorDebugBlockingReason 列舉
ms.date: 03/30/2017
api_name:
- CorDebugBlockingReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugBlockingReason
helpviewer_keywords:
- CorDebugBlockingReason enumeration [.NET Framework debugging]
ms.assetid: a6ac2531-ddfe-46fd-88fe-8b1eabe0b255
topic_type:
- apiref
ms.openlocfilehash: ddd03d70656ad52fd9d577beedc60b51c7b305d5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95672847"
---
# <a name="cordebugblockingreason-enumeration"></a><span data-ttu-id="90e87-102">CorDebugBlockingReason 列舉</span><span class="sxs-lookup"><span data-stu-id="90e87-102">CorDebugBlockingReason Enumeration</span></span>

<span data-ttu-id="90e87-103">指定給定物件上封鎖執行緒的原因。</span><span class="sxs-lookup"><span data-stu-id="90e87-103">Specifies the reasons why a thread may become blocked on a given object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="90e87-104">語法</span><span class="sxs-lookup"><span data-stu-id="90e87-104">Syntax</span></span>  
  
```cpp  
Typedef enum CorDebugBlockingReason  
{  
   BLOCKING_NONE = 0  
   BLOCKING_MONITOR_CRITICAL_SECTION = 1  
   BLOCKING_MONITOR_EVENT = 2  
}  CorDebugBlockingReason;  
```  
  
## <a name="members"></a><span data-ttu-id="90e87-105">成員</span><span class="sxs-lookup"><span data-stu-id="90e87-105">Members</span></span>  
  
|<span data-ttu-id="90e87-106">member</span><span class="sxs-lookup"><span data-stu-id="90e87-106">Member</span></span>|<span data-ttu-id="90e87-107">描述</span><span class="sxs-lookup"><span data-stu-id="90e87-107">Description</span></span>|  
|------------|-----------------|  
|`BLOCKING_NONE`|<span data-ttu-id="90e87-108">僅供內部使用。</span><span class="sxs-lookup"><span data-stu-id="90e87-108">Internal use only.</span></span>|  
|`BLOCKING_MONITOR_CRITICAL_SECTION`|<span data-ttu-id="90e87-109">執行緒正在嘗試取得與物件上的監視器鎖定相關聯的重要區段。</span><span class="sxs-lookup"><span data-stu-id="90e87-109">A thread is trying to acquire the critical section that is associated with the monitor lock on an object.</span></span> <span data-ttu-id="90e87-110">一般來說，當您呼叫其中一個或方法時，就會發生這種情況 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="90e87-110">Typically, this occurs when you call one of the <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> or <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> methods.</span></span>|  
|`BLOCKING_MONITOR_EVENT`|<span data-ttu-id="90e87-111">執行緒正在等候與物件的監視器鎖定相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="90e87-111">A thread is waiting on the event that is associated with a monitor lock for an object.</span></span> <span data-ttu-id="90e87-112">一般來說，當您呼叫其中一個方法時，就會發生這種情況 <xref:System.Threading.Monitor?displayProperty=nameWithType> `Wait` 。</span><span class="sxs-lookup"><span data-stu-id="90e87-112">Typically, this occurs when you call one of the <xref:System.Threading.Monitor?displayProperty=nameWithType>`Wait` methods.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="90e87-113">備註</span><span class="sxs-lookup"><span data-stu-id="90e87-113">Remarks</span></span>  

 <span data-ttu-id="90e87-114">在 `BLOCKING_MONITOR_CRITICAL_SECTION` `BLOCKING_MONITOR_EVENT` [CorDebugBlockingObject](cordebugblockingobject-structure.md) 結構中使用或成員時， `pBlockingObject` 結構的成員會指向 "ICorDebugValue" 介面，此介面表示所要輸入的物件。</span><span class="sxs-lookup"><span data-stu-id="90e87-114">When the `BLOCKING_MONITOR_CRITICAL_SECTION` or `BLOCKING_MONITOR_EVENT` member is used in a [CorDebugBlockingObject](cordebugblockingobject-structure.md) structure, the `pBlockingObject` member of the structure points to an "ICorDebugValue" interface that represents the object that is being entered.</span></span> <span data-ttu-id="90e87-115">也保證會執行 [ICorDebugHeapValue3](icordebugheapvalue3-interface.md) 介面。</span><span class="sxs-lookup"><span data-stu-id="90e87-115">It is also guaranteed to implement the [ICorDebugHeapValue3](icordebugheapvalue3-interface.md) interface.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="90e87-116">需求</span><span class="sxs-lookup"><span data-stu-id="90e87-116">Requirements</span></span>  

 <span data-ttu-id="90e87-117">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="90e87-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="90e87-118">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="90e87-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="90e87-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="90e87-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="90e87-120">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="90e87-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="90e87-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="90e87-121">See also</span></span>

- [<span data-ttu-id="90e87-122">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="90e87-122">Debugging Enumerations</span></span>](debugging-enumerations.md)
- [<span data-ttu-id="90e87-123">偵錯</span><span class="sxs-lookup"><span data-stu-id="90e87-123">Debugging</span></span>](index.md)

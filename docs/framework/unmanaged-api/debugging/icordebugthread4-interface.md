---
title: ICorDebugThread4 介面
ms.date: 03/30/2017
api_name:
- ICorDebugThread4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread4
helpviewer_keywords:
- ICorDebugThread4 interface [.NET Framework debugging]
ms.assetid: a8c7719a-322b-4133-8566-4c27218dc104
topic_type:
- apiref
ms.openlocfilehash: a0d6f3e109f92ad44eeeb1b1dec05e53015992a6
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378353"
---
# <a name="icordebugthread4-interface"></a><span data-ttu-id="ac484-102">ICorDebugThread4 介面</span><span class="sxs-lookup"><span data-stu-id="ac484-102">ICorDebugThread4 Interface</span></span>
<span data-ttu-id="ac484-103">提供執行緒封鎖資訊。</span><span class="sxs-lookup"><span data-stu-id="ac484-103">Provides thread blocking information.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="ac484-104">方法</span><span class="sxs-lookup"><span data-stu-id="ac484-104">Methods</span></span>  
  
|<span data-ttu-id="ac484-105">方法</span><span class="sxs-lookup"><span data-stu-id="ac484-105">Method</span></span>|<span data-ttu-id="ac484-106">描述</span><span class="sxs-lookup"><span data-stu-id="ac484-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="ac484-107">GetBlockingObjects 方法</span><span class="sxs-lookup"><span data-stu-id="ac484-107">GetBlockingObjects Method</span></span>](icordebugthread4-getblockingobjects-method.md)|<span data-ttu-id="ac484-108">提供[CorDebugBlockingObject](cordebugblockingobject-structure.md)結構的已排序列舉，以提供執行緒封鎖資訊。</span><span class="sxs-lookup"><span data-stu-id="ac484-108">Provides an ordered enumeration of [CorDebugBlockingObject](cordebugblockingobject-structure.md) structures that provide thread blocking information.</span></span>|  
|[<span data-ttu-id="ac484-109">HadUnhandledException 方法</span><span class="sxs-lookup"><span data-stu-id="ac484-109">HadUnhandledException Method</span></span>](icordebugthread4-hadunhandledexception-method.md)|<span data-ttu-id="ac484-110">指出執行緒是否曾經有未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ac484-110">Indicates whether the thread has ever had an unhandled exception.</span></span>|  
|[<span data-ttu-id="ac484-111">GetCurrentCustomDebuggerNotification 方法</span><span class="sxs-lookup"><span data-stu-id="ac484-111">GetCurrentCustomDebuggerNotification Method</span></span>](icordebugthread4-getcurrentcustomdebuggernotification-method.md)|<span data-ttu-id="ac484-112">取得目前線程上的目前[ICorDebugManagedCallback3：： CustomNotification](icordebugmanagedcallback3-customnotification-method.md)物件。</span><span class="sxs-lookup"><span data-stu-id="ac484-112">Gets the current [ICorDebugManagedCallback3::CustomNotification](icordebugmanagedcallback3-customnotification-method.md) object on the current thread.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ac484-113">備註</span><span class="sxs-lookup"><span data-stu-id="ac484-113">Remarks</span></span>  
 <span data-ttu-id="ac484-114">這個介面是 ICorDebugThread、ICorDebugThread2 和[ICorDebugThread3](icordebugthread3-interface.md)介面的邏輯擴充。</span><span class="sxs-lookup"><span data-stu-id="ac484-114">This interface is a logical extension of the ICorDebugThread, ICorDebugThread2, and [ICorDebugThread3](icordebugthread3-interface.md) interfaces.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac484-115">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="ac484-115">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ac484-116">需求</span><span class="sxs-lookup"><span data-stu-id="ac484-116">Requirements</span></span>  
 <span data-ttu-id="ac484-117">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ac484-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ac484-118">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ac484-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ac484-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ac484-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ac484-120">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ac484-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ac484-121">請參閱</span><span class="sxs-lookup"><span data-stu-id="ac484-121">See also</span></span>

- [<span data-ttu-id="ac484-122">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="ac484-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="ac484-123">偵錯</span><span class="sxs-lookup"><span data-stu-id="ac484-123">Debugging</span></span>](index.md)

---
title: ICorDebugUnmanagedCallback 介面
ms.date: 03/30/2017
api_name:
- ICorDebugUnmanagedCallback
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugUnmanagedCallback
helpviewer_keywords:
- ICorDebugUnmanagedCallback interface [.NET Framework debugging]
ms.assetid: bc71cbca-7d73-40e5-84dd-2109fade3c2a
topic_type:
- apiref
ms.openlocfilehash: 73722c9fbc1571496159c32b0106f25bc05dbe65
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703014"
---
# <a name="icordebugunmanagedcallback-interface"></a><span data-ttu-id="68d5b-102">ICorDebugUnmanagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="68d5b-102">ICorDebugUnmanagedCallback Interface</span></span>

<span data-ttu-id="68d5b-103">提供與 common language runtime (CLR) 不直接相關的原生事件通知。</span><span class="sxs-lookup"><span data-stu-id="68d5b-103">Provides notification of native events that are not directly related to the common language runtime (CLR).</span></span>  
  
## <a name="methods"></a><span data-ttu-id="68d5b-104">方法</span><span class="sxs-lookup"><span data-stu-id="68d5b-104">Methods</span></span>  
  
|<span data-ttu-id="68d5b-105">方法</span><span class="sxs-lookup"><span data-stu-id="68d5b-105">Method</span></span>|<span data-ttu-id="68d5b-106">描述</span><span class="sxs-lookup"><span data-stu-id="68d5b-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="68d5b-107">DebugEvent 方法</span><span class="sxs-lookup"><span data-stu-id="68d5b-107">DebugEvent Method</span></span>](icordebugunmanagedcallback-debugevent-method.md)|<span data-ttu-id="68d5b-108">通知偵錯工具已引發原生事件。</span><span class="sxs-lookup"><span data-stu-id="68d5b-108">Notifies the debugger that a native event has been fired.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="68d5b-109">備註</span><span class="sxs-lookup"><span data-stu-id="68d5b-109">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="68d5b-110">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="68d5b-110">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="68d5b-111">需求</span><span class="sxs-lookup"><span data-stu-id="68d5b-111">Requirements</span></span>  

 <span data-ttu-id="68d5b-112">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="68d5b-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="68d5b-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="68d5b-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="68d5b-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="68d5b-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="68d5b-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="68d5b-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="68d5b-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="68d5b-116">See also</span></span>

- [<span data-ttu-id="68d5b-117">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="68d5b-117">Debugging Interfaces</span></span>](debugging-interfaces.md)

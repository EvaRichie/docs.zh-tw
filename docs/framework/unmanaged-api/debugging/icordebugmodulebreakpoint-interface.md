---
title: ICorDebugModuleBreakpoint Interface
ms.date: 03/30/2017
api_name:
- ICorDebugModuleBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModuleBreakpoint
helpviewer_keywords:
- ICorDebugModuleBreakpoint interface [.NET Framework debugging]
ms.assetid: 34667162-f314-475f-ae1b-ce9cb0fcbb83
topic_type:
- apiref
ms.openlocfilehash: 14f2b6822744070e649cf9a6722272992c0bf1c8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709514"
---
# <a name="icordebugmodulebreakpoint-interface"></a><span data-ttu-id="22de6-102">ICorDebugModuleBreakpoint Interface</span><span class="sxs-lookup"><span data-stu-id="22de6-102">ICorDebugModuleBreakpoint Interface</span></span>

<span data-ttu-id="22de6-103">提供特定模組的存取權。</span><span class="sxs-lookup"><span data-stu-id="22de6-103">Provides access to specific modules.</span></span> <span data-ttu-id="22de6-104">此介面是 ICorDebugBreakpoint 介面的子類別。</span><span class="sxs-lookup"><span data-stu-id="22de6-104">This interface is a subclass of the ICorDebugBreakpoint interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="22de6-105">方法</span><span class="sxs-lookup"><span data-stu-id="22de6-105">Methods</span></span>  
  
|<span data-ttu-id="22de6-106">方法</span><span class="sxs-lookup"><span data-stu-id="22de6-106">Method</span></span>|<span data-ttu-id="22de6-107">描述</span><span class="sxs-lookup"><span data-stu-id="22de6-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="22de6-108">GetModule 方法</span><span class="sxs-lookup"><span data-stu-id="22de6-108">GetModule Method</span></span>](icordebugmodulebreakpoint-getmodule-method.md)|<span data-ttu-id="22de6-109">取得 ICorDebugModule 的介面指標，該參考會參考設定此中斷點的模組。</span><span class="sxs-lookup"><span data-stu-id="22de6-109">Gets an interface pointer to an ICorDebugModule that references the module where this breakpoint is set.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="22de6-110">備註</span><span class="sxs-lookup"><span data-stu-id="22de6-110">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="22de6-111">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="22de6-111">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="22de6-112">需求</span><span class="sxs-lookup"><span data-stu-id="22de6-112">Requirements</span></span>  

 <span data-ttu-id="22de6-113">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="22de6-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="22de6-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="22de6-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="22de6-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="22de6-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="22de6-116">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="22de6-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="22de6-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="22de6-117">See also</span></span>

- [<span data-ttu-id="22de6-118">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="22de6-118">Debugging Interfaces</span></span>](debugging-interfaces.md)

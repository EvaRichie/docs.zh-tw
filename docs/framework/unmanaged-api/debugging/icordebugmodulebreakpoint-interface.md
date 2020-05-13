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
ms.openlocfilehash: 7026d135b02563b6c718be4096d2c5cad9d33cec
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212278"
---
# <a name="icordebugmodulebreakpoint-interface"></a><span data-ttu-id="33204-102">ICorDebugModuleBreakpoint Interface</span><span class="sxs-lookup"><span data-stu-id="33204-102">ICorDebugModuleBreakpoint Interface</span></span>

<span data-ttu-id="33204-103">提供特定模組的存取權。</span><span class="sxs-lookup"><span data-stu-id="33204-103">Provides access to specific modules.</span></span> <span data-ttu-id="33204-104">這個介面是 ICorDebugBreakpoint 介面的子類別。</span><span class="sxs-lookup"><span data-stu-id="33204-104">This interface is a subclass of the ICorDebugBreakpoint interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="33204-105">方法</span><span class="sxs-lookup"><span data-stu-id="33204-105">Methods</span></span>  
  
|<span data-ttu-id="33204-106">方法</span><span class="sxs-lookup"><span data-stu-id="33204-106">Method</span></span>|<span data-ttu-id="33204-107">描述</span><span class="sxs-lookup"><span data-stu-id="33204-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="33204-108">GetModule 方法</span><span class="sxs-lookup"><span data-stu-id="33204-108">GetModule Method</span></span>](icordebugmodulebreakpoint-getmodule-method.md)|<span data-ttu-id="33204-109">取得參考已設定此中斷點之模組的 ICorDebugModule 介面指標。</span><span class="sxs-lookup"><span data-stu-id="33204-109">Gets an interface pointer to an ICorDebugModule that references the module where this breakpoint is set.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="33204-110">備註</span><span class="sxs-lookup"><span data-stu-id="33204-110">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="33204-111">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="33204-111">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="33204-112">需求</span><span class="sxs-lookup"><span data-stu-id="33204-112">Requirements</span></span>  
 <span data-ttu-id="33204-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="33204-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="33204-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="33204-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="33204-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="33204-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="33204-116">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="33204-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="33204-117">請參閱</span><span class="sxs-lookup"><span data-stu-id="33204-117">See also</span></span>

- [<span data-ttu-id="33204-118">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="33204-118">Debugging Interfaces</span></span>](debugging-interfaces.md)

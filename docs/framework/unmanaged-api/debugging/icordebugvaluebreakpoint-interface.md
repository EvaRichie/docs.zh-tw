---
title: ICorDebugValueBreakpoint Interface
ms.date: 03/30/2017
api_name:
- ICorDebugValueBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValueBreakpoint
helpviewer_keywords:
- ICorDebugValueBreakpoint interface [.NET Framework debugging]
ms.assetid: c02338fe-da6c-467f-9567-70ebb387e901
topic_type:
- apiref
ms.openlocfilehash: 1183f9f6d1ac221b20767f0a1bab15b3e9665a61
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396603"
---
# <a name="icordebugvaluebreakpoint-interface"></a><span data-ttu-id="f4233-102">ICorDebugValueBreakpoint Interface</span><span class="sxs-lookup"><span data-stu-id="f4233-102">ICorDebugValueBreakpoint Interface</span></span>
<span data-ttu-id="f4233-103">擴充 ICorDebugBreakpoint 介面，以提供特定值的存取權。</span><span class="sxs-lookup"><span data-stu-id="f4233-103">Extends the ICorDebugBreakpoint interface to provide access to specific values.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="f4233-104">方法</span><span class="sxs-lookup"><span data-stu-id="f4233-104">Methods</span></span>  
  
|<span data-ttu-id="f4233-105">方法</span><span class="sxs-lookup"><span data-stu-id="f4233-105">Method</span></span>|<span data-ttu-id="f4233-106">描述</span><span class="sxs-lookup"><span data-stu-id="f4233-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="f4233-107">GetValue 方法</span><span class="sxs-lookup"><span data-stu-id="f4233-107">GetValue Method</span></span>](icordebugvaluebreakpoint-getvalue-method.md)|<span data-ttu-id="f4233-108">取得 ICorDebugValue 物件的介面指標，表示設定中斷點所在物件的值。</span><span class="sxs-lookup"><span data-stu-id="f4233-108">Gets an interface pointer to an ICorDebugValue object that represents the value of the object upon which the breakpoint is set.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="f4233-109">備註</span><span class="sxs-lookup"><span data-stu-id="f4233-109">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f4233-110">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="f4233-110">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f4233-111">需求</span><span class="sxs-lookup"><span data-stu-id="f4233-111">Requirements</span></span>  
 <span data-ttu-id="f4233-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f4233-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f4233-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f4233-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f4233-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f4233-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f4233-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f4233-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f4233-116">請參閱</span><span class="sxs-lookup"><span data-stu-id="f4233-116">See also</span></span>

- [<span data-ttu-id="f4233-117">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="f4233-117">Debugging Interfaces</span></span>](debugging-interfaces.md)

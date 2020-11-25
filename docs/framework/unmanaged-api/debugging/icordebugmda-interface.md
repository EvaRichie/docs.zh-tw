---
title: ICorDebugMDA 介面
ms.date: 03/30/2017
api_name:
- ICorDebugMDA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA
helpviewer_keywords:
- ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 8ecbb854-295c-4dd4-b9fc-01ebeac46e06
topic_type:
- apiref
ms.openlocfilehash: c4ff28ff1019b5314902a4e71f6d02b5a2fd8d70
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95710827"
---
# <a name="icordebugmda-interface"></a><span data-ttu-id="7be3d-102">ICorDebugMDA 介面</span><span class="sxs-lookup"><span data-stu-id="7be3d-102">ICorDebugMDA Interface</span></span>

<span data-ttu-id="7be3d-103">表示 Managed 偵錯助理 (MDA) 訊息。</span><span class="sxs-lookup"><span data-stu-id="7be3d-103">Represents a managed debugging assistant (MDA) message.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="7be3d-104">方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-104">Methods</span></span>  
  
|<span data-ttu-id="7be3d-105">方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-105">Method</span></span>|<span data-ttu-id="7be3d-106">描述</span><span class="sxs-lookup"><span data-stu-id="7be3d-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="7be3d-107">GetDescription 方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-107">GetDescription Method</span></span>](icordebugmda-getdescription-method.md)|<span data-ttu-id="7be3d-108">取得字串，其中包含此 MDA 的描述。</span><span class="sxs-lookup"><span data-stu-id="7be3d-108">Gets a string containing a description of this MDA.</span></span>|  
|[<span data-ttu-id="7be3d-109">GetFlags 方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-109">GetFlags Method</span></span>](icordebugmda-getflags-method.md)|<span data-ttu-id="7be3d-110">取得與此 MDA 相關聯的旗標。</span><span class="sxs-lookup"><span data-stu-id="7be3d-110">Gets the flags associated with this MDA.</span></span>|  
|[<span data-ttu-id="7be3d-111">GetName 方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-111">GetName Method</span></span>](icordebugmda-getname-method.md)|<span data-ttu-id="7be3d-112">取得字串，其中包含此 MDA 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7be3d-112">Gets a string containing the name of this MDA.</span></span>|  
|[<span data-ttu-id="7be3d-113">GetOSThreadId 方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-113">GetOSThreadId Method</span></span>](icordebugmda-getosthreadid-method.md)|<span data-ttu-id="7be3d-114">取得此 MDA 執行時所依據的作業系統執行緒識別碼。</span><span class="sxs-lookup"><span data-stu-id="7be3d-114">Gets the operating system thread identifier upon which this MDA is executing.</span></span>|  
|[<span data-ttu-id="7be3d-115">GetXML 方法</span><span class="sxs-lookup"><span data-stu-id="7be3d-115">GetXML Method</span></span>](icordebugmda-getxml-method.md)|<span data-ttu-id="7be3d-116">取得與此 MDA 相關聯的完整 XML 資料流程。</span><span class="sxs-lookup"><span data-stu-id="7be3d-116">Gets the full XML stream associated with this MDA.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="7be3d-117">備註</span><span class="sxs-lookup"><span data-stu-id="7be3d-117">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7be3d-118">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="7be3d-118">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7be3d-119">需求</span><span class="sxs-lookup"><span data-stu-id="7be3d-119">Requirements</span></span>  

 <span data-ttu-id="7be3d-120">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="7be3d-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7be3d-121">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="7be3d-121">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="7be3d-122">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7be3d-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7be3d-123">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7be3d-123">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7be3d-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7be3d-124">See also</span></span>

- [<span data-ttu-id="7be3d-125">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="7be3d-125">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="7be3d-126">診斷 Managed 偵錯助理的錯誤</span><span class="sxs-lookup"><span data-stu-id="7be3d-126">Diagnosing Errors with Managed Debugging Assistants</span></span>](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)

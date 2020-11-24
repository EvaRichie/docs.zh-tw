---
title: ICorDebugThread3::CreateStackWalk 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread3.CreateStackWalk Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread3::CreateStackWalk
helpviewer_keywords:
- CreateStackWalk method [.NET Framework debugging]
- ICorDebugThread3::CreateStackWalk method [.NET Framework debugging]
ms.assetid: c55e35d9-f9aa-4268-94b5-dce44c61acf2
topic_type:
- apiref
ms.openlocfilehash: fb9d07fffd2ec98225ce60b211f525f8dafd9725
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95691063"
---
# <a name="icordebugthread3createstackwalk-method"></a><span data-ttu-id="c5db9-102">ICorDebugThread3::CreateStackWalk 方法</span><span class="sxs-lookup"><span data-stu-id="c5db9-102">ICorDebugThread3::CreateStackWalk Method</span></span>

<span data-ttu-id="c5db9-103">為您想要回溯其堆疊的執行緒建立 [ICorDebugStackWalk](icordebugstackwalk-interface.md) 物件。</span><span class="sxs-lookup"><span data-stu-id="c5db9-103">Creates an [ICorDebugStackWalk](icordebugstackwalk-interface.md) object for the thread whose stack you want to unwind.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c5db9-104">語法</span><span class="sxs-lookup"><span data-stu-id="c5db9-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateStackWalk([out] ICorDebugStackWalk **ppStackWalk);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c5db9-105">參數</span><span class="sxs-lookup"><span data-stu-id="c5db9-105">Parameters</span></span>  

 `ppStackWalk`  
 <span data-ttu-id="c5db9-106">擴展您想要回溯其堆疊之執行緒的 [ICorDebugStackWalk](icordebugstackwalk-interface.md) 物件位址指標。</span><span class="sxs-lookup"><span data-stu-id="c5db9-106">[out] A pointer to address of the [ICorDebugStackWalk](icordebugstackwalk-interface.md) object for the thread whose stack you want to unwind.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c5db9-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="c5db9-107">Return Value</span></span>  

 <span data-ttu-id="c5db9-108">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c5db9-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="c5db9-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="c5db9-109">HRESULT</span></span>|<span data-ttu-id="c5db9-110">描述</span><span class="sxs-lookup"><span data-stu-id="c5db9-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="c5db9-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="c5db9-111">S_OK</span></span>|<span data-ttu-id="c5db9-112">已 `ICorDebugStackWalk` 成功建立物件。</span><span class="sxs-lookup"><span data-stu-id="c5db9-112">The `ICorDebugStackWalk` object was successfully created.</span></span>|  
|<span data-ttu-id="c5db9-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="c5db9-113">E_FAIL</span></span>|<span data-ttu-id="c5db9-114">`ICorDebugStackWalk`未建立物件。</span><span class="sxs-lookup"><span data-stu-id="c5db9-114">The `ICorDebugStackWalk` object was not created.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="c5db9-115">例外</span><span class="sxs-lookup"><span data-stu-id="c5db9-115">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c5db9-116">備註</span><span class="sxs-lookup"><span data-stu-id="c5db9-116">Remarks</span></span>  

 <span data-ttu-id="c5db9-117">如果 `CreateStackWalk` 方法成功，則傳回的 `ICorDebugStackWalk` 物件內容會設定為執行緒的目前內容。</span><span class="sxs-lookup"><span data-stu-id="c5db9-117">If the `CreateStackWalk` method succeeds, the returned `ICorDebugStackWalk` object's context is set to the thread's current context.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c5db9-118">需求</span><span class="sxs-lookup"><span data-stu-id="c5db9-118">Requirements</span></span>  

 <span data-ttu-id="c5db9-119">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c5db9-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c5db9-120">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="c5db9-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="c5db9-121">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c5db9-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c5db9-122">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c5db9-122">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c5db9-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c5db9-123">See also</span></span>

- [<span data-ttu-id="c5db9-124">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="c5db9-124">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="c5db9-125">偵錯</span><span class="sxs-lookup"><span data-stu-id="c5db9-125">Debugging</span></span>](index.md)

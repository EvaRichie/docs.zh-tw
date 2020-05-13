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
ms.openlocfilehash: f2850e6c9cbb2250a08ab4a0e34c69e377d3a23d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83375843"
---
# <a name="icordebugthread3createstackwalk-method"></a><span data-ttu-id="d0ce4-102">ICorDebugThread3::CreateStackWalk 方法</span><span class="sxs-lookup"><span data-stu-id="d0ce4-102">ICorDebugThread3::CreateStackWalk Method</span></span>
<span data-ttu-id="d0ce4-103">為您要回溯其堆疊的執行緒建立[ICorDebugStackWalk](icordebugstackwalk-interface.md)物件。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-103">Creates an [ICorDebugStackWalk](icordebugstackwalk-interface.md) object for the thread whose stack you want to unwind.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d0ce4-104">語法</span><span class="sxs-lookup"><span data-stu-id="d0ce4-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateStackWalk([out] ICorDebugStackWalk **ppStackWalk);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d0ce4-105">參數</span><span class="sxs-lookup"><span data-stu-id="d0ce4-105">Parameters</span></span>  
 `ppStackWalk`  
 <span data-ttu-id="d0ce4-106">脫銷要回溯其堆疊的執行緒之[ICorDebugStackWalk](icordebugstackwalk-interface.md)物件位址的指標。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-106">[out] A pointer to address of the [ICorDebugStackWalk](icordebugstackwalk-interface.md) object for the thread whose stack you want to unwind.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d0ce4-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="d0ce4-107">Return Value</span></span>  
 <span data-ttu-id="d0ce4-108">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="d0ce4-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="d0ce4-109">HRESULT</span></span>|<span data-ttu-id="d0ce4-110">描述</span><span class="sxs-lookup"><span data-stu-id="d0ce4-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="d0ce4-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="d0ce4-111">S_OK</span></span>|<span data-ttu-id="d0ce4-112">`ICorDebugStackWalk`已成功建立物件。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-112">The `ICorDebugStackWalk` object was successfully created.</span></span>|  
|<span data-ttu-id="d0ce4-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="d0ce4-113">E_FAIL</span></span>|<span data-ttu-id="d0ce4-114">`ICorDebugStackWalk`未建立物件。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-114">The `ICorDebugStackWalk` object was not created.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="d0ce4-115">例外狀況</span><span class="sxs-lookup"><span data-stu-id="d0ce4-115">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d0ce4-116">備註</span><span class="sxs-lookup"><span data-stu-id="d0ce4-116">Remarks</span></span>  
 <span data-ttu-id="d0ce4-117">如果 `CreateStackWalk` 方法成功，則傳回的 `ICorDebugStackWalk` 物件內容會設定為執行緒的目前內容。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-117">If the `CreateStackWalk` method succeeds, the returned `ICorDebugStackWalk` object's context is set to the thread's current context.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d0ce4-118">需求</span><span class="sxs-lookup"><span data-stu-id="d0ce4-118">Requirements</span></span>  
 <span data-ttu-id="d0ce4-119">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d0ce4-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d0ce4-120">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d0ce4-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d0ce4-121">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d0ce4-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d0ce4-122">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d0ce4-122">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d0ce4-123">請參閱</span><span class="sxs-lookup"><span data-stu-id="d0ce4-123">See also</span></span>

- [<span data-ttu-id="d0ce4-124">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="d0ce4-124">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="d0ce4-125">偵錯</span><span class="sxs-lookup"><span data-stu-id="d0ce4-125">Debugging</span></span>](index.md)

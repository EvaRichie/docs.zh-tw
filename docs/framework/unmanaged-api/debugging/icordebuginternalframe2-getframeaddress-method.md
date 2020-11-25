---
title: ICorDebugInternalFrame2::GetFrameAddress 方法
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2.GetFrameAddress Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2::GetFrameAddress
helpviewer_keywords:
- GetFrameAddress method [.NET Framework debugging]
- ICorDebugInternalFrame2::GetFrameAddress method [.NET Framework debugging]
ms.assetid: 4ee8d058-ffc8-4967-9133-a5adfef4e518
topic_type:
- apiref
ms.openlocfilehash: 05a9ab58acb3bf5829fd231ae6d8bcc96ae06da6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724867"
---
# <a name="icordebuginternalframe2getframeaddress-method"></a><span data-ttu-id="fc9b3-102">ICorDebugInternalFrame2::GetFrameAddress 方法</span><span class="sxs-lookup"><span data-stu-id="fc9b3-102">ICorDebugInternalFrame2::GetFrameAddress Method</span></span>

<span data-ttu-id="fc9b3-103">傳回內部框架的堆疊位址。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-103">Returns the stack address of the internal frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fc9b3-104">語法</span><span class="sxs-lookup"><span data-stu-id="fc9b3-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFrameAddress([out] CORDB_ADDRESS *pAddress);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fc9b3-105">參數</span><span class="sxs-lookup"><span data-stu-id="fc9b3-105">Parameters</span></span>  

 `pAddress`  
 <span data-ttu-id="fc9b3-106">擴展內部框架之的指標 `CORDB_ADDRESS` 。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-106">[out] Pointer to the `CORDB_ADDRESS` for the internal frame.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fc9b3-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="fc9b3-107">Return Value</span></span>  

 <span data-ttu-id="fc9b3-108">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="fc9b3-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="fc9b3-109">HRESULT</span></span>|<span data-ttu-id="fc9b3-110">描述</span><span class="sxs-lookup"><span data-stu-id="fc9b3-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="fc9b3-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="fc9b3-111">S_OK</span></span>|<span data-ttu-id="fc9b3-112">已成功傳回內部框架的位址。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-112">The address of the internal frame was successfully returned.</span></span>|  
|<span data-ttu-id="fc9b3-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="fc9b3-113">E_FAIL</span></span>|<span data-ttu-id="fc9b3-114">無法傳回內部框架的位址。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-114">The address of the internal frame could not be returned.</span></span>|  
|<span data-ttu-id="fc9b3-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="fc9b3-115">E_INVALIDARG</span></span>|<span data-ttu-id="fc9b3-116">`pAddress` 為 `null`。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-116">`pAddress` is `null`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fc9b3-117">備註</span><span class="sxs-lookup"><span data-stu-id="fc9b3-117">Remarks</span></span>  

 <span data-ttu-id="fc9b3-118">傳回的值 `pAddress` 可用於判斷內部框架相對於堆疊上其他框架的位置。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-118">The value returned in `pAddress` can be used to determine the location of the internal frame relative to other frames on the stack.</span></span> <span data-ttu-id="fc9b3-119">即使在以 IA-64 為基礎的電腦上，內部框架還是只會存在於堆疊上，而且不會有任何對應的備份存放區指標。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-119">Even on IA-64-based computers, the internal frame lives on the stack only, and there is no corresponding pointer to a backing store.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fc9b3-120">需求</span><span class="sxs-lookup"><span data-stu-id="fc9b3-120">Requirements</span></span>  

 <span data-ttu-id="fc9b3-121">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="fc9b3-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fc9b3-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="fc9b3-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="fc9b3-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="fc9b3-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fc9b3-124">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fc9b3-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc9b3-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fc9b3-125">See also</span></span>

- [<span data-ttu-id="fc9b3-126">ICorDebugInternalFrame2 介面</span><span class="sxs-lookup"><span data-stu-id="fc9b3-126">ICorDebugInternalFrame2 Interface</span></span>](icordebuginternalframe2-interface.md)
- [<span data-ttu-id="fc9b3-127">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="fc9b3-127">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="fc9b3-128">偵錯</span><span class="sxs-lookup"><span data-stu-id="fc9b3-128">Debugging</span></span>](index.md)

---
title: ICorDebugInternalFrame2::IsCloserToLeaf 方法
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2.IsCloserToLeaf Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf
helpviewer_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf method [.NET Framework debugging]
- IsCloserToLeaf method [.NET Framework debugging]
ms.assetid: c1d3d1eb-8370-4f25-8297-3bd262b4740a
topic_type:
- apiref
ms.openlocfilehash: 4a01ccd4e5cb9aadc6a693b2c6ceaff31c114bbc
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209886"
---
# <a name="icordebuginternalframe2isclosertoleaf-method"></a><span data-ttu-id="02425-102">ICorDebugInternalFrame2::IsCloserToLeaf 方法</span><span class="sxs-lookup"><span data-stu-id="02425-102">ICorDebugInternalFrame2::IsCloserToLeaf Method</span></span>
<span data-ttu-id="02425-103">檢查 `this` 內部框架是否比指定的 ICorDebugFrame 物件更接近分葉。</span><span class="sxs-lookup"><span data-stu-id="02425-103">Checks whether the `this` internal frame is closer to the leaf than the specified ICorDebugFrame object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="02425-104">語法</span><span class="sxs-lookup"><span data-stu-id="02425-104">Syntax</span></span>  
  
```cpp  
HRESULT IsCloserToLeaf([in] ICorDebugFrame * pFrameToCompare,  
                       [out] BOOL * pIsCloser);  
```  
  
## <a name="parameters"></a><span data-ttu-id="02425-105">參數</span><span class="sxs-lookup"><span data-stu-id="02425-105">Parameters</span></span>  
 `pFrameToCompare`  
 <span data-ttu-id="02425-106">在比較物件的指標 `ICorDebugFrame` 。</span><span class="sxs-lookup"><span data-stu-id="02425-106">[in] A pointer to the comparison `ICorDebugFrame` object.</span></span>  
  
 `pIsCloser`  
 <span data-ttu-id="02425-107">[out] `true`如果 `this` 內部框架比指定的框架更接近分葉 `pFrameToCompare` ，則為，否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="02425-107">[out] `true` if the `this` internal frame is closer to the leaf than the frame specified by `pFrameToCompare`; otherwise, `false`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="02425-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="02425-108">Return Value</span></span>  
 <span data-ttu-id="02425-109">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="02425-109">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="02425-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="02425-110">HRESULT</span></span>|<span data-ttu-id="02425-111">描述</span><span class="sxs-lookup"><span data-stu-id="02425-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="02425-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="02425-112">S_OK</span></span>|<span data-ttu-id="02425-113">已成功執行比較。</span><span class="sxs-lookup"><span data-stu-id="02425-113">The comparison was successfully performed.</span></span>|  
|<span data-ttu-id="02425-114">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="02425-114">E_FAIL</span></span>|<span data-ttu-id="02425-115">無法執行比較。</span><span class="sxs-lookup"><span data-stu-id="02425-115">The comparison could not be performed.</span></span>|  
|<span data-ttu-id="02425-116">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="02425-116">E_INVALIDARG</span></span>|<span data-ttu-id="02425-117">`pFrameToCompare` 或 `pIsCloser` 為 null。</span><span class="sxs-lookup"><span data-stu-id="02425-117">`pFrameToCompare` or `pIsCloser` is null.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="02425-118">備註</span><span class="sxs-lookup"><span data-stu-id="02425-118">Remarks</span></span>  
 <span data-ttu-id="02425-119">`IsCloserToLeaf`可以用來執行將內部框架與堆疊上的其他框架交錯的原則。</span><span class="sxs-lookup"><span data-stu-id="02425-119">`IsCloserToLeaf` can be used to implement a policy for interleaving internal frames with other frames on the stack.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="02425-120">需求</span><span class="sxs-lookup"><span data-stu-id="02425-120">Requirements</span></span>  
 <span data-ttu-id="02425-121">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="02425-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="02425-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="02425-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="02425-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="02425-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="02425-124">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="02425-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="02425-125">請參閱</span><span class="sxs-lookup"><span data-stu-id="02425-125">See also</span></span>

- [<span data-ttu-id="02425-126">ICorDebugInternalFrame2 介面</span><span class="sxs-lookup"><span data-stu-id="02425-126">ICorDebugInternalFrame2 Interface</span></span>](icordebuginternalframe2-interface.md)
- [<span data-ttu-id="02425-127">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="02425-127">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="02425-128">偵錯</span><span class="sxs-lookup"><span data-stu-id="02425-128">Debugging</span></span>](index.md)

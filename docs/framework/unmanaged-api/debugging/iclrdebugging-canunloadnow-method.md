---
title: ICLRDebugging::CanUnloadNow 方法
ms.date: 03/30/2017
api_name:
- ICLRDebugging.CanUnloadNow Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebugging::CanUnloadNow
helpviewer_keywords:
- CanUnloadNow method [.NET Framework debugging]
- ICLRDebugging::CanUnloadNow method [.NET Framework debugging]
ms.assetid: 62e0630c-8cb7-45d2-b622-5a472abfd8cf
topic_type:
- apiref
ms.openlocfilehash: 16d15101534b88d7da4093dab73b48b5c09a192c
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860397"
---
# <a name="iclrdebuggingcanunloadnow-method"></a><span data-ttu-id="dd4f2-102">ICLRDebugging::CanUnloadNow 方法</span><span class="sxs-lookup"><span data-stu-id="dd4f2-102">ICLRDebugging::CanUnloadNow Method</span></span>
<span data-ttu-id="dd4f2-103">判斷[ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md)介面所提供的程式庫是否仍在使用中，或是否可以卸載。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-103">Determines whether a library that was provided by an [ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md) interface is still in use or can be unloaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="dd4f2-104">語法</span><span class="sxs-lookup"><span data-stu-id="dd4f2-104">Syntax</span></span>  
  
```cpp  
HRESULT CanUnloadNow(HMODULE hModule);  
```  
  
## <a name="parameters"></a><span data-ttu-id="dd4f2-105">參數</span><span class="sxs-lookup"><span data-stu-id="dd4f2-105">Parameters</span></span>  
 `hmodule`  
 <span data-ttu-id="dd4f2-106">在目標進程中模組的基底位址。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-106">[in] The base address of a module in the target process.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="dd4f2-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="dd4f2-107">Return Value</span></span>  
 <span data-ttu-id="dd4f2-108">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="dd4f2-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="dd4f2-109">HRESULT</span></span>|<span data-ttu-id="dd4f2-110">描述</span><span class="sxs-lookup"><span data-stu-id="dd4f2-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="dd4f2-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="dd4f2-111">S_OK</span></span>|<span data-ttu-id="dd4f2-112">所參考的模組`hmodule`可以卸載。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-112">The module that is referenced by `hmodule` can be unloaded.</span></span>|  
|<span data-ttu-id="dd4f2-113">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="dd4f2-113">S_FALSE</span></span>|<span data-ttu-id="dd4f2-114">所參考`hmodule`的模組仍在使用中。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-114">The module that is referenced by `hmodule` is still in use.</span></span>|  
|<span data-ttu-id="dd4f2-115">COR_E_NOT_CLR</span><span class="sxs-lookup"><span data-stu-id="dd4f2-115">COR_E_NOT_CLR</span></span>|<span data-ttu-id="dd4f2-116">指出的模組不是 CLR 模組。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-116">The indicated module is not a CLR module.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="dd4f2-117">例外狀況</span><span class="sxs-lookup"><span data-stu-id="dd4f2-117">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="dd4f2-118">備註</span><span class="sxs-lookup"><span data-stu-id="dd4f2-118">Remarks</span></span>  
 <span data-ttu-id="dd4f2-119">這個方法會檢查是否已釋放介面的`ICorDebug*`所有實例，而且目前沒有任何執行緒在[ICLRDebugging：： OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md)方法的呼叫中。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-119">This method checks to see if all instances of `ICorDebug*` interfaces have been released and no thread is currently within a call to the [ICLRDebugging::OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="dd4f2-120">需求</span><span class="sxs-lookup"><span data-stu-id="dd4f2-120">Requirements</span></span>  
 <span data-ttu-id="dd4f2-121">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="dd4f2-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="dd4f2-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="dd4f2-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="dd4f2-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="dd4f2-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="dd4f2-124">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="dd4f2-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dd4f2-125">請參閱</span><span class="sxs-lookup"><span data-stu-id="dd4f2-125">See also</span></span>

- [<span data-ttu-id="dd4f2-126">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="dd4f2-126">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="dd4f2-127">偵錯</span><span class="sxs-lookup"><span data-stu-id="dd4f2-127">Debugging</span></span>](index.md)

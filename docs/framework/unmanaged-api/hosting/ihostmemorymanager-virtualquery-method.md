---
title: IHostMemoryManager::VirtualQuery 方法
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualQuery
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualQuery
helpviewer_keywords:
- IHostMemoryManager::VirtualQuery method [.NET Framework hosting]
- VirtualQuery method [.NET Framework hosting]
ms.assetid: 757af1e6-b9e8-49e7-b5db-342be3aa205f
topic_type:
- apiref
ms.openlocfilehash: 71c56b5dab2409be05e8260b1a2e39d28a709bba
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804374"
---
# <a name="ihostmemorymanagervirtualquery-method"></a><span data-ttu-id="4ce36-102">IHostMemoryManager::VirtualQuery 方法</span><span class="sxs-lookup"><span data-stu-id="4ce36-102">IHostMemoryManager::VirtualQuery Method</span></span>
<span data-ttu-id="4ce36-103">作為對應 Win32 函式的邏輯包裝函式。</span><span class="sxs-lookup"><span data-stu-id="4ce36-103">Serves as a logical wrapper for the corresponding Win32 function.</span></span> <span data-ttu-id="4ce36-104">的 Win32 執行會在 `VirtualQuery` 呼叫進程的虛擬位址空間中，抓取某個頁面範圍的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4ce36-104">The Win32 implementation of `VirtualQuery` retrieves information about a range of pages in the virtual address space of the calling process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4ce36-105">語法</span><span class="sxs-lookup"><span data-stu-id="4ce36-105">Syntax</span></span>  
  
```cpp  
HRESULT VirtualQuery (  
    [in]  void*    lpAddress,  
    [out] void*    lpBuffer,  
    [in]  SIZE_T   dwLength,  
    [out] SIZE_T*  pResult  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4ce36-106">參數</span><span class="sxs-lookup"><span data-stu-id="4ce36-106">Parameters</span></span>  
 `lpAddress`  
 <span data-ttu-id="4ce36-107">在要查詢之虛擬記憶體中的位址指標。</span><span class="sxs-lookup"><span data-stu-id="4ce36-107">[in] A pointer to the address in virtual memory to be queried.</span></span>  
  
 `lpBuffer`  
 <span data-ttu-id="4ce36-108">脫銷結構的指標，其中包含指定之記憶體區域的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4ce36-108">[out] A pointer to a structure that contains information about the specified memory region.</span></span>  
  
 `dwLength`  
 <span data-ttu-id="4ce36-109">在指向的緩衝區大小（以位元組為單位） `lpBuffer` 。</span><span class="sxs-lookup"><span data-stu-id="4ce36-109">[in] The size, in bytes, of the buffer that `lpBuffer` points to.</span></span>  
  
 `pResult`  
 <span data-ttu-id="4ce36-110">脫銷資訊緩衝區所傳回之位元組數的指標。</span><span class="sxs-lookup"><span data-stu-id="4ce36-110">[out] A pointer to the number of bytes returned by the information buffer.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4ce36-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="4ce36-111">Return Value</span></span>  
  
|<span data-ttu-id="4ce36-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="4ce36-112">HRESULT</span></span>|<span data-ttu-id="4ce36-113">描述</span><span class="sxs-lookup"><span data-stu-id="4ce36-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="4ce36-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="4ce36-114">S_OK</span></span>|<span data-ttu-id="4ce36-115">`VirtualQuery`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="4ce36-115">`VirtualQuery` returned successfully.</span></span>|  
|<span data-ttu-id="4ce36-116">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="4ce36-116">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="4ce36-117">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="4ce36-117">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="4ce36-118">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="4ce36-118">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="4ce36-119">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="4ce36-119">The call timed out.</span></span>|  
|<span data-ttu-id="4ce36-120">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="4ce36-120">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="4ce36-121">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="4ce36-121">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="4ce36-122">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="4ce36-122">HOST_E_ABANDONED</span></span>|<span data-ttu-id="4ce36-123">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="4ce36-123">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="4ce36-124">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="4ce36-124">E_FAIL</span></span>|<span data-ttu-id="4ce36-125">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="4ce36-125">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="4ce36-126">當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="4ce36-126">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="4ce36-127">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="4ce36-127">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="4ce36-128">備註</span><span class="sxs-lookup"><span data-stu-id="4ce36-128">Remarks</span></span>  
 <span data-ttu-id="4ce36-129">`VirtualQuery`提供有關呼叫進程的虛擬位址空間中的頁面範圍的資訊。</span><span class="sxs-lookup"><span data-stu-id="4ce36-129">`VirtualQuery` provides information about a range of pages in the virtual address space of the calling process.</span></span> <span data-ttu-id="4ce36-130">這個執行會將參數的值設定 `pResult` 為資訊緩衝區中傳回的位元組數目，並傳回 HRESULT 值。</span><span class="sxs-lookup"><span data-stu-id="4ce36-130">This implementation sets the value of the `pResult` parameter to the number of bytes returned in the information buffer, and returns an HRESULT value.</span></span> <span data-ttu-id="4ce36-131">在 Win32 `VirtualQuery` 函數中，傳回值是緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="4ce36-131">In the Win32 `VirtualQuery` function, the return value is the buffer size.</span></span> <span data-ttu-id="4ce36-132">如需詳細資訊，請參閱 Windows 平臺檔。</span><span class="sxs-lookup"><span data-stu-id="4ce36-132">For more information, see the Windows Platform documentation.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="4ce36-133">作業系統的執行 `VirtualQuery` 不會產生鎖死，而且可以在使用者程式碼中暫停的隨機執行緒執行到完成。</span><span class="sxs-lookup"><span data-stu-id="4ce36-133">The operating system's implementation of `VirtualQuery` does not incur deadlock and can run to completion with random threads suspended in user code.</span></span> <span data-ttu-id="4ce36-134">在執行這個方法的主控版本時，請特別小心。</span><span class="sxs-lookup"><span data-stu-id="4ce36-134">Use great caution when implementing a hosted version of this method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4ce36-135">規格需求</span><span class="sxs-lookup"><span data-stu-id="4ce36-135">Requirements</span></span>  
 <span data-ttu-id="4ce36-136">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4ce36-136">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4ce36-137">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="4ce36-137">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="4ce36-138">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="4ce36-138">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="4ce36-139">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4ce36-139">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4ce36-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4ce36-140">See also</span></span>

- [<span data-ttu-id="4ce36-141">IHostMemoryManager 介面</span><span class="sxs-lookup"><span data-stu-id="4ce36-141">IHostMemoryManager Interface</span></span>](ihostmemorymanager-interface.md)

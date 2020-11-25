---
title: ICorDebugMetaDataLocator::GetMetaData 方法
ms.date: 03/30/2017
api_name:
- ICorDebugMetaDataLocator.GetMetaData
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMetaDataLocator::GetMetaData
helpviewer_keywords:
- ICorDebugMetaDataLocator::GetMetaData method [.NET Framework debugging]
- GetMetaData method, ICorDebugMetaDataLocator interface [.NET Framework debugging]
ms.assetid: f9b0ff22-54db-45eb-9cc3-508000a3141d
topic_type:
- apiref
ms.openlocfilehash: 63efb788d8bca84da94921371309704cc7b20ac4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95710437"
---
# <a name="icordebugmetadatalocatorgetmetadata-method"></a><span data-ttu-id="6f5c4-102">ICorDebugMetaDataLocator::GetMetaData 方法</span><span class="sxs-lookup"><span data-stu-id="6f5c4-102">ICorDebugMetaDataLocator::GetMetaData Method</span></span>

<span data-ttu-id="6f5c4-103">要求偵錯工具傳回完整路徑到模組，其需要中繼資料以完成偵錯工具的要求。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-103">Asks the debugger to return the full path to a module whose metadata is needed to complete an operation the debugger requested.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6f5c4-104">語法</span><span class="sxs-lookup"><span data-stu-id="6f5c4-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMetaData(  
      [in] LPCWSTR wszImagePath,  
      [in] DWORD   dwImageTimeStamp,  
      [in] DWORD   dwImageSize,  
      [in] ULONG32 cchPathBuffer,  
      [out] ULONG32 * pcchPathBuffer,  
      [out, size_is(cchPathBuffer), length_is(*pcchPathBuffer)]  
               WCHAR wszPathBuffer[]  
      );  
```  
  
## <a name="parameters"></a><span data-ttu-id="6f5c4-105">參數</span><span class="sxs-lookup"><span data-stu-id="6f5c4-105">Parameters</span></span>  

 `wszImagePath`  
 <span data-ttu-id="6f5c4-106">[in] 以 null 結束的字串，表示檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-106">[in] A null-terminated string that represents the full path to the file.</span></span> <span data-ttu-id="6f5c4-107">如果無法使用完整路徑，檔案名和副檔名 (*檔案名*。*延伸* 模組) 。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-107">If the full path is not available, the name and extension of the file (*filename*.*extension*).</span></span>  
  
 `dwImageTimeStamp`  
 <span data-ttu-id="6f5c4-108">[in] 從映像的 PE 檔標頭的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-108">[in] The time stamp from the image's PE file headers.</span></span> <span data-ttu-id="6f5c4-109">此參數可能用於符號伺服器 ([SymSrv](/windows/desktop/debug/using-symsrv)) 查閱。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-109">This parameter can potentially be used for a symbol server ([SymSrv](/windows/desktop/debug/using-symsrv)) lookup.</span></span>  
  
 `dwImageSize`  
 <span data-ttu-id="6f5c4-110">[in] 從 PE 檔標頭的映像大小。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-110">[in] The image size from PE file headers.</span></span> <span data-ttu-id="6f5c4-111">此參數可能會用於 SymSrv 查閱。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-111">This parameter can potentially be used for a SymSrv lookup.</span></span>  
  
 `cchPathBuffer`  
 <span data-ttu-id="6f5c4-112">[in] 在 `wszPathBuffer` 中的字元計數。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-112">[in] The character count in `wszPathBuffer`.</span></span>  
  
 `pcchPathBuffer`  
 <span data-ttu-id="6f5c4-113">[out] `WCHAR` 的計數，寫入 `wszPathBuffer`。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-113">[out] The count of `WCHAR`s written to `wszPathBuffer`.</span></span>  
  
 <span data-ttu-id="6f5c4-114">如果此方法會傳回 E_NOT_SUFFICIENT_BUFFER，包含 `WCHAR` 的計數需要儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-114">If the method returns E_NOT_SUFFICIENT_BUFFER, contains the count of `WCHAR`s needed to store the path.</span></span>  
  
 `wszPathBuffer`  
 <span data-ttu-id="6f5c4-115">[out] 偵錯工具會將包含要求的中繼資料檔案的完整路徑複製到其中的緩衝區指標。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-115">[out] Pointer to a buffer into which the debugger will copy the full path of the file that contains the requested metadata.</span></span>  
  
 <span data-ttu-id="6f5c4-116">`ofReadOnly` [CorOpenFlags](../metadata/coropenflags-enumeration.md)列舉中的旗標是用來要求對此檔案中中繼資料的唯讀存取。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-116">The `ofReadOnly` flag from the [CorOpenFlags](../metadata/coropenflags-enumeration.md) enumeration is used to request read-only access to the metadata in this file.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="6f5c4-117">傳回值</span><span class="sxs-lookup"><span data-stu-id="6f5c4-117">Return Value</span></span>  

 <span data-ttu-id="6f5c4-118">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-118">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span> <span data-ttu-id="6f5c4-119">所有其他失敗的 HRESULT 表示無法擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-119">All other failure HRESULTs indicate that the file is not retrievable.</span></span>  
  
|<span data-ttu-id="6f5c4-120">HRESULT</span><span class="sxs-lookup"><span data-stu-id="6f5c4-120">HRESULT</span></span>|<span data-ttu-id="6f5c4-121">描述</span><span class="sxs-lookup"><span data-stu-id="6f5c4-121">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="6f5c4-122">S_OK</span><span class="sxs-lookup"><span data-stu-id="6f5c4-122">S_OK</span></span>|<span data-ttu-id="6f5c4-123">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-123">The method completed successfully.</span></span> <span data-ttu-id="6f5c4-124">`wszPathBuffer` 包含檔案的完整路徑，而且是以 null 結束。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-124">`wszPathBuffer` contains the full path to the file and is null-terminated.</span></span>|  
|<span data-ttu-id="6f5c4-125">E_NOT_SUFFICIENT_BUFFER</span><span class="sxs-lookup"><span data-stu-id="6f5c4-125">E_NOT_SUFFICIENT_BUFFER</span></span>|<span data-ttu-id="6f5c4-126">目前的大小 `wszPathBuffer` 不足以保存完整路徑。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-126">The current size of `wszPathBuffer` is not sufficient to hold the full path.</span></span> <span data-ttu-id="6f5c4-127">在此情況下， `pcchPathBuffer` 包含所需的 `WCHAR` 計數，包括結束的 null 字元且 `GetMetaData` 被稱為第二次的要求緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-127">In this case, `pcchPathBuffer` contains the needed count of `WCHAR`s, including the terminating null character, and `GetMetaData` is called a second time with the requested buffer size.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="6f5c4-128">備註</span><span class="sxs-lookup"><span data-stu-id="6f5c4-128">Remarks</span></span>  

 <span data-ttu-id="6f5c4-129">如果 `wszImagePath` 包含來自傾印的模組完整路徑，它會指定從收集傾印所在之電腦的路徑。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-129">If `wszImagePath` contains a full path for a module from a dump, it specifies the path from the computer where the dump was collected.</span></span> <span data-ttu-id="6f5c4-130">檔案可能不存在這個位置，或具有相同名稱的不正確檔案可能儲存在路徑上。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-130">The file may not exist at this location, or an incorrect file with the same name may be stored on the path.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6f5c4-131">需求</span><span class="sxs-lookup"><span data-stu-id="6f5c4-131">Requirements</span></span>  

 <span data-ttu-id="6f5c4-132">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6f5c4-132">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6f5c4-133">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="6f5c4-133">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="6f5c4-134">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6f5c4-134">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6f5c4-135">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6f5c4-135">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6f5c4-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6f5c4-136">See also</span></span>

- [<span data-ttu-id="6f5c4-137">ICorDebugThread4 介面</span><span class="sxs-lookup"><span data-stu-id="6f5c4-137">ICorDebugThread4 Interface</span></span>](icordebugthread4-interface.md)
- [<span data-ttu-id="6f5c4-138">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="6f5c4-138">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="6f5c4-139">偵錯</span><span class="sxs-lookup"><span data-stu-id="6f5c4-139">Debugging</span></span>](index.md)

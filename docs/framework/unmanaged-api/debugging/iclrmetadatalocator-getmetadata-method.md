---
title: ICLRMetadataLocator::GetMetadata 方法
ms.date: 03/30/2017
api_name:
- ICLRMetadataLocator.GetMetadata
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRMetadataLocator::GetMetadata
helpviewer_keywords:
- GetMetadata method, ICLRMetadataLocator interface [.NET Framework debugging]
- ICLRMetadataLocator::GetMetadata method [.NET Framework debugging]
ms.assetid: 704a8893-ac56-43b4-90ea-715f38ccb40e
topic_type:
- apiref
ms.openlocfilehash: f0ba2342e9704ba06dd1d3612f699298c734a5eb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723515"
---
# <a name="iclrmetadatalocatorgetmetadata-method"></a><span data-ttu-id="1129d-102">ICLRMetadataLocator::GetMetadata 方法</span><span class="sxs-lookup"><span data-stu-id="1129d-102">ICLRMetadataLocator::GetMetadata Method</span></span>

<span data-ttu-id="1129d-103">由 common language runtime 呼叫 (CLR) 資料存取服務來取得影像的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="1129d-103">Called by the common language runtime (CLR) data access services to retrieve the metadata of an image.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1129d-104">語法</span><span class="sxs-lookup"><span data-stu-id="1129d-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMetadata(  
    [in]  LPCWSTR         imagePath,  
    [in]  ULONG32         imageTimestamp,  
    [in]  ULONG32         imageSize,  
    [in]  GUID*           mvid,  
    [in]  ULONG32         mdRva,  
    [in]  ULONG32         flags,  
    [in]  ULONG32         bufferSize,  
    [out, size_is(bufferSize), length_is(*dataSize)]  
          BYTE*           buffer,  
    [out] ULONG32*        dataSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1129d-105">參數</span><span class="sxs-lookup"><span data-stu-id="1129d-105">Parameters</span></span>  

 `imagePath`  
 <span data-ttu-id="1129d-106">在字串，指定影像檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="1129d-106">[in] A string that specifies the path of the image file.</span></span>  
  
 `imageTimestamp`  
 <span data-ttu-id="1129d-107">在影像檔案的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="1129d-107">[in] The time stamp of the image file.</span></span>  
  
 `imageSize`  
 <span data-ttu-id="1129d-108">在影像檔案的大小。</span><span class="sxs-lookup"><span data-stu-id="1129d-108">[in] The size of the image file.</span></span>  
  
 `mvid`  
 <span data-ttu-id="1129d-109">在影像的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1129d-109">[in] The globally unique identifier of the image.</span></span>  
  
 `mdRva`  
 <span data-ttu-id="1129d-110">在中繼資料 (RVA) 的相對虛擬位址。</span><span class="sxs-lookup"><span data-stu-id="1129d-110">[in] The relative virtual address (RVA) of the metadata.</span></span> <span data-ttu-id="1129d-111">位址是相對於映射基底位址。</span><span class="sxs-lookup"><span data-stu-id="1129d-111">The address is relative to the image base address.</span></span>  
  
 `flags`  
 <span data-ttu-id="1129d-112">在保留供日後使用。</span><span class="sxs-lookup"><span data-stu-id="1129d-112">[in] Reserved for future use.</span></span>  
  
 `bufferSize`  
 <span data-ttu-id="1129d-113">在要在其中放置中繼資料的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="1129d-113">[in] The size of the buffer in which to place the metadata.</span></span>  
  
 `buffer`  
 <span data-ttu-id="1129d-114">擴展要在其中放置中繼資料的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="1129d-114">[out] The buffer in which to place the metadata.</span></span>  
  
 `dataSize`  
 <span data-ttu-id="1129d-115">擴展傳回的中繼資料大小。</span><span class="sxs-lookup"><span data-stu-id="1129d-115">[out] The size of the metadata that is returned.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1129d-116">備註</span><span class="sxs-lookup"><span data-stu-id="1129d-116">Remarks</span></span>  

 <span data-ttu-id="1129d-117">此方法是由偵錯應用程式的作者來實作。</span><span class="sxs-lookup"><span data-stu-id="1129d-117">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1129d-118">需求</span><span class="sxs-lookup"><span data-stu-id="1129d-118">Requirements</span></span>  

 <span data-ttu-id="1129d-119">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1129d-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1129d-120">**標頭：** ClrData .idl、ClrData。h</span><span class="sxs-lookup"><span data-stu-id="1129d-120">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="1129d-121">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1129d-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1129d-122">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1129d-122">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1129d-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1129d-123">See also</span></span>

- [<span data-ttu-id="1129d-124">ICLRMetadataLocator 介面</span><span class="sxs-lookup"><span data-stu-id="1129d-124">ICLRMetadataLocator Interface</span></span>](iclrmetadatalocator-interface.md)

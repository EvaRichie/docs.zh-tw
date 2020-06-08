---
title: ICLRRuntimeInfo::GetInterface 方法
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetInterface
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetInterface
helpviewer_keywords:
- GetInterface method [.NET Framework hosting]
- ICLRRuntimeInfo::GetInterface method [.NET Framework hosting]
ms.assetid: cc7b0e5b-48c3-4509-8ebb-611ddb1f7ec2
topic_type:
- apiref
ms.openlocfilehash: 9cf9d48bf50ffc1fc56270c13215acfef6d9c3af
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504052"
---
# <a name="iclrruntimeinfogetinterface-method"></a><span data-ttu-id="203da-102">ICLRRuntimeInfo::GetInterface 方法</span><span class="sxs-lookup"><span data-stu-id="203da-102">ICLRRuntimeInfo::GetInterface Method</span></span>
<span data-ttu-id="203da-103">將 CLR 載入目前的進程，並傳回執行時間介面指標，例如[ICLRRuntimeHost](iclrruntimehost-interface.md)、 [ICLRStrongName](iclrstrongname-interface.md)和[IMetaDataDispenserEx](../metadata/imetadatadispenser-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="203da-103">Loads the CLR into the current process and returns runtime interface pointers, such as [ICLRRuntimeHost](iclrruntimehost-interface.md), [ICLRStrongName](iclrstrongname-interface.md), and [IMetaDataDispenserEx](../metadata/imetadatadispenser-interface.md).</span></span>  
  
 <span data-ttu-id="203da-104">這個方法會取代已 `CorBindTo` [淘汰的 CLR 裝載](deprecated-clr-hosting-functions.md)函式一節中的所有 \* 函數。</span><span class="sxs-lookup"><span data-stu-id="203da-104">This method supersedes all the `CorBindTo`\* functions in the [Deprecated CLR Hosting Functions](deprecated-clr-hosting-functions.md) section.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="203da-105">語法</span><span class="sxs-lookup"><span data-stu-id="203da-105">Syntax</span></span>  
  
```cpp  
HRESULT GetInterface(  
[in]  REFCLSID rclsid,  
[in]  REFIID   riid,  
[out, iid_is(riid), retval] LPVOID *ppUnk);  
```  
  
## <a name="parameters"></a><span data-ttu-id="203da-106">參數</span><span class="sxs-lookup"><span data-stu-id="203da-106">Parameters</span></span>  
 `rclsid`  
 <span data-ttu-id="203da-107">在Coclass 的 CLSID 介面。</span><span class="sxs-lookup"><span data-stu-id="203da-107">[in] The CLSID interface for the coclass.</span></span>  
  
 `riid`  
 <span data-ttu-id="203da-108">在所要求介面的 IID `rclsid` 。</span><span class="sxs-lookup"><span data-stu-id="203da-108">[in] The IID of the requested `rclsid` interface.</span></span>  
  
 `ppUnk`  
 <span data-ttu-id="203da-109">脫銷所查詢介面的指標。</span><span class="sxs-lookup"><span data-stu-id="203da-109">[out] A pointer to the queried interface.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="203da-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="203da-110">Return Value</span></span>  
 <span data-ttu-id="203da-111">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="203da-111">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="203da-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="203da-112">HRESULT</span></span>|<span data-ttu-id="203da-113">說明</span><span class="sxs-lookup"><span data-stu-id="203da-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="203da-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="203da-114">S_OK</span></span>|<span data-ttu-id="203da-115">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="203da-115">The method completed successfully.</span></span>|  
|<span data-ttu-id="203da-116">E_POINTER</span><span class="sxs-lookup"><span data-stu-id="203da-116">E_POINTER</span></span>|<span data-ttu-id="203da-117">`ppUnk` 為 null。</span><span class="sxs-lookup"><span data-stu-id="203da-117">`ppUnk` is null.</span></span>|  
|<span data-ttu-id="203da-118">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="203da-118">E_OUTOFMEMORY</span></span>|<span data-ttu-id="203da-119">沒有足夠的記憶體可用來處理要求。</span><span class="sxs-lookup"><span data-stu-id="203da-119">Not enough memory is available to handle the request.</span></span>|  
|<span data-ttu-id="203da-120">CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND</span><span class="sxs-lookup"><span data-stu-id="203da-120">CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND</span></span>|<span data-ttu-id="203da-121">不同的執行時間已系結至舊版 CLR 第2版啟用原則。</span><span class="sxs-lookup"><span data-stu-id="203da-121">A different runtime was already bound to the legacy CLR version 2 activation policy.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="203da-122">備註</span><span class="sxs-lookup"><span data-stu-id="203da-122">Remarks</span></span>  
 <span data-ttu-id="203da-123">這個方法會載入 CLR，但不會初始化。</span><span class="sxs-lookup"><span data-stu-id="203da-123">This method causes the CLR to be loaded but not initialized.</span></span>  
  
 <span data-ttu-id="203da-124">下表顯示和支援的組合 `rclsid` `riid` 。</span><span class="sxs-lookup"><span data-stu-id="203da-124">The following table shows the supported combinations for `rclsid` and `riid`.</span></span>  
  
|`rclsid`|`riid`|  
|--------------|------------|  
|<span data-ttu-id="203da-125">CLSID_CorMetaDataDispenser</span><span class="sxs-lookup"><span data-stu-id="203da-125">CLSID_CorMetaDataDispenser</span></span>|<span data-ttu-id="203da-126">IID_IMetaDataDispenser，IID_IMetaDataDispenserEx</span><span class="sxs-lookup"><span data-stu-id="203da-126">IID_IMetaDataDispenser, IID_IMetaDataDispenserEx</span></span>|  
|<span data-ttu-id="203da-127">CLSID_CorMetaDataDispenserRuntime</span><span class="sxs-lookup"><span data-stu-id="203da-127">CLSID_CorMetaDataDispenserRuntime</span></span>|<span data-ttu-id="203da-128">IID_IMetaDataDispenser，IID_IMetaDataDispenserEx</span><span class="sxs-lookup"><span data-stu-id="203da-128">IID_IMetaDataDispenser, IID_IMetaDataDispenserEx</span></span>|  
|<span data-ttu-id="203da-129">CLSID_CorRuntimeHost</span><span class="sxs-lookup"><span data-stu-id="203da-129">CLSID_CorRuntimeHost</span></span>|<span data-ttu-id="203da-130">IID_ICorRuntimeHost</span><span class="sxs-lookup"><span data-stu-id="203da-130">IID_ICorRuntimeHost</span></span>|  
|<span data-ttu-id="203da-131">CLSID_CLRRuntimeHost</span><span class="sxs-lookup"><span data-stu-id="203da-131">CLSID_CLRRuntimeHost</span></span>|<span data-ttu-id="203da-132">IID_ICLRRuntimeHost</span><span class="sxs-lookup"><span data-stu-id="203da-132">IID_ICLRRuntimeHost</span></span>|  
|<span data-ttu-id="203da-133">CLSID_TypeNameFactory</span><span class="sxs-lookup"><span data-stu-id="203da-133">CLSID_TypeNameFactory</span></span>|<span data-ttu-id="203da-134">IID_ITypeNameFactory</span><span class="sxs-lookup"><span data-stu-id="203da-134">IID_ITypeNameFactory</span></span>|  
|<span data-ttu-id="203da-135">CLSID_CLRDebuggingLegacy</span><span class="sxs-lookup"><span data-stu-id="203da-135">CLSID_CLRDebuggingLegacy</span></span>|<span data-ttu-id="203da-136">IID_ICorDebug</span><span class="sxs-lookup"><span data-stu-id="203da-136">IID_ICorDebug</span></span>|  
|||  
|<span data-ttu-id="203da-137">CLSID_CLRStrongName</span><span class="sxs-lookup"><span data-stu-id="203da-137">CLSID_CLRStrongName</span></span>|<span data-ttu-id="203da-138">IID_ICLRStrongName</span><span class="sxs-lookup"><span data-stu-id="203da-138">IID_ICLRStrongName</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="203da-139">規格需求</span><span class="sxs-lookup"><span data-stu-id="203da-139">Requirements</span></span>  
 <span data-ttu-id="203da-140">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="203da-140">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="203da-141">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="203da-141">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="203da-142">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="203da-142">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="203da-143">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="203da-143">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="203da-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="203da-144">See also</span></span>

- [<span data-ttu-id="203da-145">ICLRRuntimeInfo 介面</span><span class="sxs-lookup"><span data-stu-id="203da-145">ICLRRuntimeInfo Interface</span></span>](iclrruntimeinfo-interface.md)
- [<span data-ttu-id="203da-146">裝載介面</span><span class="sxs-lookup"><span data-stu-id="203da-146">Hosting Interfaces</span></span>](hosting-interfaces.md)
- [<span data-ttu-id="203da-147">Hosting</span><span class="sxs-lookup"><span data-stu-id="203da-147">Hosting</span></span>](index.md)

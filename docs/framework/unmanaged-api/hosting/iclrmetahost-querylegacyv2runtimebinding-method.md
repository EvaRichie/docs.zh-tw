---
title: ICLRMetaHost::QueryLegacyV2RuntimeBinding 方法
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::QueryLegacyV2RuntimeBinding
helpviewer_keywords:
- QueryLegacyV2RuntimeBinding method [.NET Framework hosting]
- ICLRMetaHost::QueryLegacyV2RuntimeBinding method [.NET Framework hosting]
ms.assetid: 9929817e-acc9-40b7-960c-598664e04b60
topic_type:
- apiref
ms.openlocfilehash: b270a6691d4e4ee4a5d0b42f424694eb7993e4e7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504143"
---
# <a name="iclrmetahostquerylegacyv2runtimebinding-method"></a><span data-ttu-id="21e00-102">ICLRMetaHost::QueryLegacyV2RuntimeBinding 方法</span><span class="sxs-lookup"><span data-stu-id="21e00-102">ICLRMetaHost::QueryLegacyV2RuntimeBinding Method</span></span>
<span data-ttu-id="21e00-103">傳回介面，代表舊版啟用原則已系結的執行時間，例如，藉由使用 `useLegacyV2RuntimeActivationPolicy` [ \<startup> 元素](../../configure-apps/file-schema/startup/startup-element.md)設定檔案專案上的屬性、直接使用舊版啟用 Api，或呼叫[ICLRRuntimeInfo：： BindAsLegacyV2Runtime](iclrruntimeinfo-bindaslegacyv2runtime-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="21e00-103">Returns an interface that represents a runtime to which legacy activation policy has been bound, for example, by using the `useLegacyV2RuntimeActivationPolicy` attribute on the [\<startup> element](../../configure-apps/file-schema/startup/startup-element.md) configuration file entry, by direct use of the legacy activation APIs, or by calling the [ICLRRuntimeInfo::BindAsLegacyV2Runtime](iclrruntimeinfo-bindaslegacyv2runtime-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="21e00-104">語法</span><span class="sxs-lookup"><span data-stu-id="21e00-104">Syntax</span></span>  
  
```cpp  
HRESULT QueryLegacyV2RuntimeBinding (  
    [in] REFIID riid,  
    [out, iid_is(riid), retval] LPVOID *ppUnk);  
```  
  
## <a name="parameters"></a><span data-ttu-id="21e00-105">參數</span><span class="sxs-lookup"><span data-stu-id="21e00-105">Parameters</span></span>  
 `riid`  
 <span data-ttu-id="21e00-106">在必要。目前唯一適用于此參數的值為 `IID_ICLRRuntimeInfo` 。</span><span class="sxs-lookup"><span data-stu-id="21e00-106">[in] Required.Currently the only valid value for this parameter is `IID_ICLRRuntimeInfo`.</span></span>  
  
 `ppUnk`  
 <span data-ttu-id="21e00-107">[out] 必要項。</span><span class="sxs-lookup"><span data-stu-id="21e00-107">[out] Required.</span></span> <span data-ttu-id="21e00-108">當這個方法傳回時，會包含[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)介面的指標，代表已系結到舊版啟用原則的執行時間。</span><span class="sxs-lookup"><span data-stu-id="21e00-108">When this method returns, contains a pointer to the [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) interface that represents a runtime that has been bound to legacy activation policy.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="21e00-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="21e00-109">Return Value</span></span>  
 <span data-ttu-id="21e00-110">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="21e00-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="21e00-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="21e00-111">HRESULT</span></span>|<span data-ttu-id="21e00-112">說明</span><span class="sxs-lookup"><span data-stu-id="21e00-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="21e00-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="21e00-113">S_OK</span></span>|<span data-ttu-id="21e00-114">這個方法順利完成，且傳回已繫結到舊版啟用原則的執行階段。</span><span class="sxs-lookup"><span data-stu-id="21e00-114">The method completed successfully and returned a runtime that was bound to legacy activation policy.</span></span>|  
|<span data-ttu-id="21e00-115">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="21e00-115">S_FALSE</span></span>|<span data-ttu-id="21e00-116">這個方法順利完成，但是尚未已繫結舊版執行階段。</span><span class="sxs-lookup"><span data-stu-id="21e00-116">The method completed successfully, but a legacy runtime has not yet been bound.</span></span>|  
|<span data-ttu-id="21e00-117">E_NOINTERFACE</span><span class="sxs-lookup"><span data-stu-id="21e00-117">E_NOINTERFACE</span></span>|<span data-ttu-id="21e00-118">此方法找到的執行階段已繫結到舊版啟用原則，但該執行階段不支援 `riid`。</span><span class="sxs-lookup"><span data-stu-id="21e00-118">The method found a runtime that was bound to legacy activation policy, but `riid` is not supported by that runtime.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="21e00-119">備註</span><span class="sxs-lookup"><span data-stu-id="21e00-119">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="21e00-120">需求</span><span class="sxs-lookup"><span data-stu-id="21e00-120">Requirements</span></span>  
 <span data-ttu-id="21e00-121">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="21e00-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="21e00-122">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="21e00-122">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="21e00-123">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="21e00-123">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="21e00-124">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="21e00-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="21e00-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="21e00-125">See also</span></span>

- [<span data-ttu-id="21e00-126">ICLRMetaHost 介面</span><span class="sxs-lookup"><span data-stu-id="21e00-126">ICLRMetaHost Interface</span></span>](iclrmetahost-interface.md)
- [<span data-ttu-id="21e00-127">Hosting</span><span class="sxs-lookup"><span data-stu-id="21e00-127">Hosting</span></span>](index.md)

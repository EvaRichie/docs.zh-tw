---
title: METAHOST_CONFIG_FLAGS 列舉
ms.date: 03/30/2017
api_name:
- METAHOST_CONFIG_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- METAHOST_CONFIG_FLAGS
helpviewer_keywords:
- METAHOST_CONFIG_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 6f1e389f-ed99-4d6a-a0ba-72d7d869a01d
topic_type:
- apiref
ms.openlocfilehash: 6b37fcfc04e3ec880c67f102ec12d7f3e4b06a43
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493158"
---
# <a name="metahost_config_flags-enumeration"></a><span data-ttu-id="c3f73-102">METAHOST_CONFIG_FLAGS 列舉</span><span class="sxs-lookup"><span data-stu-id="c3f73-102">METAHOST_CONFIG_FLAGS Enumeration</span></span>
<span data-ttu-id="c3f73-103">描述在 `pdwConfigFlags` [ICLRMetaHostPolicy：： GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md)方法的參數中傳回的可能旗標，指出 `useLegacyV2RuntimeActivationPolicy` 設定檔[ \<startup> ](../../configure-apps/file-schema/startup/startup-element.md)的專案中屬性的目前狀態和設定。</span><span class="sxs-lookup"><span data-stu-id="c3f73-103">Describes the possible flags returned in the `pdwConfigFlags` parameter of the [ICLRMetaHostPolicy::GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md) method, indicating the presence and setting of the `useLegacyV2RuntimeActivationPolicy` attribute in the [\<startup> element](../../configure-apps/file-schema/startup/startup-element.md) of the configuration file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c3f73-104">語法</span><span class="sxs-lookup"><span data-stu-id="c3f73-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET  = 0x00,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE   = 0x01,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE  = 0x02,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK   = 0x03  
} METAHOST_CONFIG_FLAGS;  
```  
  
## <a name="members"></a><span data-ttu-id="c3f73-105">成員</span><span class="sxs-lookup"><span data-stu-id="c3f73-105">Members</span></span>  
  
|<span data-ttu-id="c3f73-106">成員</span><span class="sxs-lookup"><span data-stu-id="c3f73-106">Member</span></span>|<span data-ttu-id="c3f73-107">說明</span><span class="sxs-lookup"><span data-stu-id="c3f73-107">Description</span></span>|  
|------------|-----------------|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET`|<span data-ttu-id="c3f73-108">`useLegacyV2RuntimeActivationPolicy`屬性不存在於[ \<startup> 元素](../../configure-apps/file-schema/startup/startup-element.md)中。</span><span class="sxs-lookup"><span data-stu-id="c3f73-108">The `useLegacyV2RuntimeActivationPolicy` attribute was not present in the [\<startup> Element](../../configure-apps/file-schema/startup/startup-element.md).</span></span>|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE`|<span data-ttu-id="c3f73-109">`useLegacyV2RuntimeActivationPolicy`屬性存在且設定為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="c3f73-109">The `useLegacyV2RuntimeActivationPolicy` attribute was present and set to `true`.</span></span>|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE`|<span data-ttu-id="c3f73-110">`useLegacyV2RuntimeActivationPolicy`屬性存在且設定為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="c3f73-110">The `useLegacyV2RuntimeActivationPolicy` attribute was present and set to `false`.</span></span>|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK`|<span data-ttu-id="c3f73-111">將此遮罩套用至中傳回的值 `pdwConfigFlags` ，以取得與相關的值 `useLegacyV2RuntimeActivationPolicy` 。</span><span class="sxs-lookup"><span data-stu-id="c3f73-111">Apply this mask to the value returned in `pdwConfigFlags` to get the values relevant to `useLegacyV2RuntimeActivationPolicy`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c3f73-112">備註</span><span class="sxs-lookup"><span data-stu-id="c3f73-112">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c3f73-113">需求</span><span class="sxs-lookup"><span data-stu-id="c3f73-113">Requirements</span></span>  
 <span data-ttu-id="c3f73-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c3f73-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c3f73-115">**標頭：** Metahost。h</span><span class="sxs-lookup"><span data-stu-id="c3f73-115">**Header:** Metahost.h</span></span>  
  
 <span data-ttu-id="c3f73-116">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="c3f73-116">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c3f73-117">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c3f73-117">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c3f73-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c3f73-118">See also</span></span>

- [<span data-ttu-id="c3f73-119">裝載列舉</span><span class="sxs-lookup"><span data-stu-id="c3f73-119">Hosting Enumerations</span></span>](hosting-enumerations.md)
- [<span data-ttu-id="c3f73-120">GetRequestedRuntime 方法</span><span class="sxs-lookup"><span data-stu-id="c3f73-120">GetRequestedRuntime Method</span></span>](iclrmetahostpolicy-getrequestedruntime-method.md)
- [<span data-ttu-id="c3f73-121">\<startup>元素</span><span class="sxs-lookup"><span data-stu-id="c3f73-121">\<startup> Element</span></span>](../../configure-apps/file-schema/startup/startup-element.md)

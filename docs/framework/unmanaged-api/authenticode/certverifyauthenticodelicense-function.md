---
title: CertVerifyAuthenticodeLicense 函式
ms.date: 03/30/2017
api_name:
- CertVerifyAuthenticodeLicense
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 00118de7-33c6-41c4-8e1f-5d5e35e0da83
ms.openlocfilehash: 388814d1c63f048c0aa231a1d0058a390cba9493
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95674056"
---
# <a name="certverifyauthenticodelicense-function"></a><span data-ttu-id="9e248-102">CertVerifyAuthenticodeLicense 函式</span><span class="sxs-lookup"><span data-stu-id="9e248-102">CertVerifyAuthenticodeLicense Function</span></span>

<span data-ttu-id="9e248-103">驗證 Authenticode XrML 授權的有效性。</span><span class="sxs-lookup"><span data-stu-id="9e248-103">Verifies the validity of an Authenticode XrML license.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9e248-104">語法</span><span class="sxs-lookup"><span data-stu-id="9e248-104">Syntax</span></span>  
  
```cpp  
HRESULT CertVerifyAuthenticodeLicense (  
    [in]   PCRYPT_DATA_BLOB                   pLicenseBlob,  
    [in]   OPTIONAL DWORD                     dwFlags,  
    [out]  PAXL_AUTHENTICODE_SIGNER_INFO      pSignerInfo,  
    [out]  PAXL_AUTHENTICODE_TIMESTAMPER_INFO pTimestamperInfo  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9e248-105">參數</span><span class="sxs-lookup"><span data-stu-id="9e248-105">Parameters</span></span>  

 `pLicenseBlob`  
 <span data-ttu-id="9e248-106">[in] 要驗證的 Authenticode XrML 授權。</span><span class="sxs-lookup"><span data-stu-id="9e248-106">[in] The Authenticode XrML license to be verified.</span></span>  
  
 <span data-ttu-id="9e248-107">請參閱 [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) 結構。</span><span class="sxs-lookup"><span data-stu-id="9e248-107">See the [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) structure.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="9e248-108">[in] 選用。</span><span class="sxs-lookup"><span data-stu-id="9e248-108">[in] Optional.</span></span> <span data-ttu-id="9e248-109">下列值的組合：</span><span class="sxs-lookup"><span data-stu-id="9e248-109">A combination of following values:</span></span>  
  
- <span data-ttu-id="9e248-110">AXL_REVOCATION_NO_CHECK</span><span class="sxs-lookup"><span data-stu-id="9e248-110">AXL_REVOCATION_NO_CHECK</span></span>  
  
- <span data-ttu-id="9e248-111">AXL_REVOCATION_CHECK_END_CERT_ONLY</span><span class="sxs-lookup"><span data-stu-id="9e248-111">AXL_REVOCATION_CHECK_END_CERT_ONLY</span></span>  
  
- <span data-ttu-id="9e248-112">AXL_REVOCATION_CHECK_ENTIRE_CHAIN</span><span class="sxs-lookup"><span data-stu-id="9e248-112">AXL_REVOCATION_CHECK_ENTIRE_CHAIN</span></span>  
  
- <span data-ttu-id="9e248-113">AXL_URL_CACHE_ONLY_RETRIEVAL</span><span class="sxs-lookup"><span data-stu-id="9e248-113">AXL_URL_CACHE_ONLY_RETRIEVAL</span></span>  
  
- <span data-ttu-id="9e248-114">AXL_LIFETIME_SIGNING</span><span class="sxs-lookup"><span data-stu-id="9e248-114">AXL_LIFETIME_SIGNING</span></span>  
  
- <span data-ttu-id="9e248-115">AXL_TRUST_MICROSOFT_ROOT_ONLY</span><span class="sxs-lookup"><span data-stu-id="9e248-115">AXL_TRUST_MICROSOFT_ROOT_ONLY</span></span>  
  
 `pSignerInfo`  
 <span data-ttu-id="9e248-116">[out] 接收簽署者的資訊。</span><span class="sxs-lookup"><span data-stu-id="9e248-116">[out] To receive the signer's information.</span></span> <span data-ttu-id="9e248-117">若授權未經簽署，`dwError` 會設為 TRUST_E_NOSIGNATURE。</span><span class="sxs-lookup"><span data-stu-id="9e248-117">If the license wasn't signed, `dwError` is set to TRUST_E_NOSIGNATURE.</span></span> <span data-ttu-id="9e248-118">呼叫端會負責在使用後使用 [CertFreeAuthenticodeSignerInfo](certfreeauthenticodesignerinfo-function.md) 函式來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="9e248-118">It is the caller's responsibility to free resources by using the [CertFreeAuthenticodeSignerInfo](certfreeauthenticodesignerinfo-function.md) function after use.</span></span>  
  
 <span data-ttu-id="9e248-119">請參閱 [AXL_AUTHENTICODE_SIGNER_INFO 結構](axl-authenticode-signer-info-structure.md)。</span><span class="sxs-lookup"><span data-stu-id="9e248-119">See [AXL_AUTHENTICODE_SIGNER_INFO Structure](axl-authenticode-signer-info-structure.md).</span></span>  
  
 `pTimestamperInfo`  
 <span data-ttu-id="9e248-120">[out] 接收時間戳記設定者的資訊 (如有提供)。</span><span class="sxs-lookup"><span data-stu-id="9e248-120">[out] To receive time stamper's information, if available.</span></span> <span data-ttu-id="9e248-121">若授權未設定時間戳記，`dwError` 會設為 TRUST_E_NOSIGNATURE。</span><span class="sxs-lookup"><span data-stu-id="9e248-121">If the license was not time-stamped, `dwError` is set to TRUST_E_NOSIGNATURE.</span></span> <span data-ttu-id="9e248-122">呼叫端會負責在使用後使用 [CertFreeAuthenticodeTimestamperInfo](certfreeauthenticodetimestamperinfo-function.md) 函式來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="9e248-122">It is the caller's responsibility to free resources by using the [CertFreeAuthenticodeTimestamperInfo](certfreeauthenticodetimestamperinfo-function.md) function after use.</span></span>  
  
 <span data-ttu-id="9e248-123">請參閱 [AXL_AUTHENTICODE_TIMESTAMPER_INFO 結構](axl-authenticode-timestamper-info-structure.md)。</span><span class="sxs-lookup"><span data-stu-id="9e248-123">See [AXL_AUTHENTICODE_TIMESTAMPER_INFO Structure](axl-authenticode-timestamper-info-structure.md).</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="9e248-124">傳回值</span><span class="sxs-lookup"><span data-stu-id="9e248-124">Return Value</span></span>  

 <span data-ttu-id="9e248-125">若成功，會傳回 `S_OK`。</span><span class="sxs-lookup"><span data-stu-id="9e248-125">Returns `S_OK` if successful.</span></span> <span data-ttu-id="9e248-126">否則會傳回錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="9e248-126">Otherwise, returns an error code.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9e248-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9e248-127">See also</span></span>

- [<span data-ttu-id="9e248-128">Authenticode</span><span class="sxs-lookup"><span data-stu-id="9e248-128">Authenticode</span></span>](index.md)
- [<span data-ttu-id="9e248-129">GetHashFromHandle 方法</span><span class="sxs-lookup"><span data-stu-id="9e248-129">GetHashFromHandle Method</span></span>](../hosting/iclrstrongname-gethashfromhandle-method.md)
- [<span data-ttu-id="9e248-130">ICLRStrongName 介面</span><span class="sxs-lookup"><span data-stu-id="9e248-130">ICLRStrongName Interface</span></span>](../hosting/iclrstrongname-interface.md)

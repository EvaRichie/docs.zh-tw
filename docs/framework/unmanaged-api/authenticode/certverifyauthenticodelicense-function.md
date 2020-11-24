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
# <a name="certverifyauthenticodelicense-function"></a>CertVerifyAuthenticodeLicense 函式

驗證 Authenticode XrML 授權的有效性。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CertVerifyAuthenticodeLicense (  
    [in]   PCRYPT_DATA_BLOB                   pLicenseBlob,  
    [in]   OPTIONAL DWORD                     dwFlags,  
    [out]  PAXL_AUTHENTICODE_SIGNER_INFO      pSignerInfo,  
    [out]  PAXL_AUTHENTICODE_TIMESTAMPER_INFO pTimestamperInfo  
);  
```  
  
## <a name="parameters"></a>參數  

 `pLicenseBlob`  
 [in] 要驗證的 Authenticode XrML 授權。  
  
 請參閱 [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob) 結構。  
  
 `dwFlags`  
 [in] 選用。 下列值的組合：  
  
- AXL_REVOCATION_NO_CHECK  
  
- AXL_REVOCATION_CHECK_END_CERT_ONLY  
  
- AXL_REVOCATION_CHECK_ENTIRE_CHAIN  
  
- AXL_URL_CACHE_ONLY_RETRIEVAL  
  
- AXL_LIFETIME_SIGNING  
  
- AXL_TRUST_MICROSOFT_ROOT_ONLY  
  
 `pSignerInfo`  
 [out] 接收簽署者的資訊。 若授權未經簽署，`dwError` 會設為 TRUST_E_NOSIGNATURE。 呼叫端會負責在使用後使用 [CertFreeAuthenticodeSignerInfo](certfreeauthenticodesignerinfo-function.md) 函式來釋放資源。  
  
 請參閱 [AXL_AUTHENTICODE_SIGNER_INFO 結構](axl-authenticode-signer-info-structure.md)。  
  
 `pTimestamperInfo`  
 [out] 接收時間戳記設定者的資訊 (如有提供)。 若授權未設定時間戳記，`dwError` 會設為 TRUST_E_NOSIGNATURE。 呼叫端會負責在使用後使用 [CertFreeAuthenticodeTimestamperInfo](certfreeauthenticodetimestamperinfo-function.md) 函式來釋放資源。  
  
 請參閱 [AXL_AUTHENTICODE_TIMESTAMPER_INFO 結構](axl-authenticode-timestamper-info-structure.md)。  
  
## <a name="return-value"></a>傳回值  

 若成功，會傳回 `S_OK`。 否則會傳回錯誤碼。  
  
## <a name="see-also"></a>另請參閱

- [Authenticode](index.md)
- [GetHashFromHandle 方法](../hosting/iclrstrongname-gethashfromhandle-method.md)
- [ICLRStrongName 介面](../hosting/iclrstrongname-interface.md)

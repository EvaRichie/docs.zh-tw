---
title: Authenticode (Unmanaged API 參考)
ms.date: 03/30/2017
ms.assetid: 7e8cc303-6e77-4116-aa8b-7ea297a3a467
ms.openlocfilehash: 9b3e1585278bda82dedf7542e866a551867b9c9f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95674043"
---
# <a name="authenticode-unmanaged-api-reference"></a>Authenticode (Unmanaged API 參考)

支援 Authenticode XrML 授權的建立及驗證模組。  
  
## <a name="in-this-section"></a>本節內容  

 [_AxlGetIssuerPublicKeyHash 函式](axlgetissuerpublickeyhash-function.md)  
 擷取公開金鑰的 SHA-1 雜湊，該公開金鑰與用來簽署指定憑證的私密金鑰相關聯。  
  
 [_AxlPublicKeyBlobToPublicKeyToken 函式](axlpublickeyblobtopublickeytoken-function.md)  
 從 CSP PUBLICKEYBLOB 格式運算強式名稱公開金鑰語彙基元。  
  
 [_AxlRSAKeyValueToPublicKeyToken 函式](axlrsakeyvaluetopublickeytoken-function.md)  
 將模數和指數轉換成強式名稱公開金鑰語彙基元。  
  
 [CertFreeAuthenticodeSignerInfo 函式](certfreeauthenticodesignerinfo-function.md)  
 釋出配置給 AXL_AUTHENTICODE_SIGNER_INFO 結構的資源。  
  
 [CertFreeAuthenticodeTimestamperInfo 函式](certfreeauthenticodetimestamperinfo-function.md)  
 釋出配置給 AXL_AUTHENTICODE_TIMESTAMPER_INFO 結構的資源。  
  
 [CertTimestampAuthenticodeLicense 函式](certtimestampauthenticodelicense-function.md)  
 為 CertCreateAuthenticodeLicense 建立的 Authenticode XrML 授權加註時間戳記。  
  
 [CertVerifyAuthenticodeLicense 函式](certverifyauthenticodelicense-function.md)  
 驗證 Authenticode XrML 授權的有效性。  
  
 [AXL_AUTHENTICODE_SIGNER_INFO 結構](axl-authenticode-signer-info-structure.md)  
 定義 Authenticode 簽署人資訊。  
  
 [AXL_AUTHENTICODE_TIMESTAMPER_INFO 結構](axl-authenticode-timestamper-info-structure.md)  
 定義 Authenticode 時間戳記程式資訊。  
  
## <a name="see-also"></a>另請參閱

- [非受控 API 參考](../index.md)

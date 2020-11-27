---
title: 擴充安全性
ms.date: 03/30/2017
helpviewer_keywords:
- security [WCF], extending
ms.assetid: a015a040-9fdf-4147-9ea9-f83b570be1d4
ms.openlocfilehash: d91f4812dbccb7807be2e0780cccd1d0c38b1f40
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273057"
---
# <a name="extending-security"></a>擴充安全性

若要容納新的宣告類型和自訂權杖，您可以擴充 Windows Communication Foundation (WCF) 的安全性基礎結構。 本章節中的主題會示範如何做到這點。  
  
## <a name="in-this-section"></a>本節內容  
  
 [自訂認證與認證驗證](custom-credential-and-credential-validation.md)  
 說明如何在驗證自訂認證時使用身分識別模型。  
  
 [自訂權杖](custom-tokens.md)  
 通常從安全性權杖服務 (STS) 發行的權杖是 SAML 權杖。 本主題會說明如何建立自訂權杖類型。  
  
 [自訂授權](custom-authorization.md)  
 說明如何實作自訂授權。  
  
 [覆寫服務的身分識別以進行驗證](overriding-the-identity-of-a-service-for-authentication.md)  
 說明如何覆寫服務的身分識別來進行驗證。  
  
 [作法：建立自訂用戶端身分識別驗證器](how-to-create-a-custom-client-identity-verifier.md)  
 示範如何驗證自訂端點身分識別。  
  
 [作法：使用個別 X.509 憑證簽署與加密](how-to-use-separate-x-509-certificates-for-signing-and-encryption.md)  
 訊息通常會以單一憑證來簽署和加密。 本主題會說明如何能在必要時使用兩份憑證。  
  
 [作法：變更 X.509 憑證私密金鑰的密碼編譯提供者](change-cryptographic-provider-x509-certificate-private-key.md)  
 說明如何變更用來提供 x.509 憑證私密金鑰的密碼編譯提供者，以及如何將提供者整合至 Windows Communication Foundation (WCF) 架構。  
  
## <a name="reference"></a>參考  

 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
## <a name="related-sections"></a>相關章節  

 [安全性](../feature-details/security.md)  
  
 [基本 WCF 程式設計](../basic-wcf-programming.md)  
  
## <a name="see-also"></a>另請參閱

- [安全性概觀](../feature-details/security-overview.md)

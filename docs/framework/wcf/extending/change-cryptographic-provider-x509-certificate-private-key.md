---
title: 作法：變更 X.509 憑證私密金鑰的密碼編譯提供者
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptographic provider [WCF], changing
- cryptographic provider [WCF]
ms.assetid: b4254406-272e-4774-bd61-27e39bbb6c12
ms.openlocfilehash: 33d42f26407787b26e1447f8b8f619dd6fc15229
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262108"
---
# <a name="how-to-change-the-cryptographic-provider-for-an-x509-certificates-private-key"></a>作法：變更 X.509 憑證私密金鑰的密碼編譯提供者

本主題說明如何變更用來提供 x.509 憑證私密金鑰的密碼編譯提供者，以及如何將提供者整合至 Windows Communication Foundation (WCF) 安全性架構。 如需使用憑證的詳細資訊，請參閱使用 [憑證](../feature-details/working-with-certificates.md)。  
  
 WCF 安全性架構提供一種方式來引入新的安全性權杖類型，如 [如何：建立自訂權杖](how-to-create-a-custom-token.md)中所述。 也可以使用自訂權杖來取代現有由系統提供的權杖型別。  
  
 在本主題中，系統提供的 X.509 安全性權杖會由自訂 X.509 權杖取代，為憑證私密金鑰提供不同的實作。 在實際的私密金鑰是由與預設 Windows 密碼編譯提供者不同的密碼編譯提供者所提供的案例中，這十分有用。 替代密碼編譯提供者的其中一個範例是硬體安全性模組，它執行所有私密金鑰相關密碼編譯作業，且不會將私密金鑰儲存在記憶體中，因而增強系統的安全性。  
  
 下列範例僅供示範之用。 它不會取代預設的 Windows 密碼編譯提供者，但會顯示可以整合此類提供者之處。  
  
## <a name="procedures"></a>程序  

 每個具有相關安全性金鑰的安全性權杖都必須實作 <xref:System.IdentityModel.Tokens.SecurityToken.SecurityKeys%2A> 屬性，它會從安全性權杖執行個體傳回金鑰的集合。 如果權杖是 X.509 安全性權杖，集合就會包含 <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> 類別的單一執行個體，表示與憑證有關聯的公開和私密金鑰。 如果要取代用於提供憑證金鑰的預設密碼編譯提供者，請建立這個類別的新實作。  
  
#### <a name="to-create-a-custom-x509-asymmetric-key"></a>建立自訂 X.509 非對稱金鑰  
  
1. 定義衍生自 <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> 類別的新類別。  
  
2. 覆寫 <xref:System.IdentityModel.Tokens.SecurityKey.KeySize%2A> 唯讀屬性。 這個屬性會傳回憑證之公開/私密金鑰組的實際金鑰大小。  
  
3. 覆寫 <xref:System.IdentityModel.Tokens.SecurityKey.DecryptKey%2A> 方法。 WCF 安全性架構會呼叫這個方法，以使用憑證的私密金鑰來解密對稱金鑰。 (金鑰之前是使用憑證的公開金鑰來加密)。  
  
4. 覆寫 <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetAsymmetricAlgorithm%2A> 方法。 WCF 安全性架構會呼叫這個方法來取得類別的實例，這個實例 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 表示憑證之私用或公開金鑰的密碼編譯提供者，這取決於傳遞給方法的參數。  
  
5. 選擇性。 覆寫 <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetHashAlgorithmForSignature%2A> 方法。 如果需要 <xref:System.Security.Cryptography.HashAlgorithm> 類別的不同實作，請覆寫這個方法。  
  
6. 覆寫 <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetSignatureFormatter%2A> 方法。 這個方法會傳回與憑證私密金鑰有關聯之 <xref:System.Security.Cryptography.AsymmetricSignatureFormatter> 類別的執行個體。  
  
7. 覆寫 <xref:System.IdentityModel.Tokens.SecurityKey.IsSupportedAlgorithm%2A> 方法。 這個方法是用於指出安全性金鑰實作是否支援特定的密碼編譯演算法。  
  
     [!code-csharp[c_CustomX509Token#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#1)]
     [!code-vb[c_CustomX509Token#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#1)]  
  
 下列程式示範如何整合上述程式中所建立的自訂 x.509 非對稱安全性金鑰實作為 WCF 安全性架構，以取代系統提供的 x.509 安全性權杖。  
  
#### <a name="to-replace-the-system-provided-x509-security-token-with-a-custom-x509-asymmetric-security-key-token"></a>使用自訂的 X.509 非對稱安全性金鑰權杖來取代系統提供的 X.509 安全性權杖  
  
1. 請建立自訂 X.509 安全性權杖，它會傳回自訂 X.509 非對稱安全性金鑰而非系統提供的安全性金鑰，如下列範例所示。 如需有關自訂安全性權杖的詳細資訊，請參閱 how [to：建立自訂權杖](how-to-create-a-custom-token.md)。  
  
     [!code-csharp[c_CustomX509Token#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#2)]
     [!code-vb[c_CustomX509Token#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#2)]  
  
2. 請建立會傳回自訂 X.509 安全性權杖的自訂安全性權杖提供者，如範例所示。 如需有關自訂安全性權杖提供者的詳細資訊，請參閱 how [to：建立自訂安全性權杖提供者](how-to-create-a-custom-security-token-provider.md)。  
  
     [!code-csharp[c_CustomX509Token#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#3)]
     [!code-vb[c_CustomX509Token#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#3)]  
  
3. 如果自訂安全性金鑰需要用在啟動器端，請建立自訂用戶端安全性權杖管理員和自訂用戶端認證類別，如下列範例所示。 如需自訂用戶端認證和用戶端安全性權杖管理員的詳細資訊，請參閱 [逐步解說：建立自訂用戶端和服務認證](walkthrough-creating-custom-client-and-service-credentials.md)。  
  
     [!code-csharp[c_CustomX509Token#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#4)]
     [!code-vb[c_CustomX509Token#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#4)]  
  
     [!code-csharp[c_CustomX509Token#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#6)]
     [!code-vb[c_CustomX509Token#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#6)]  
  
4. 如果自訂安全性金鑰需要用在收件者端，請建立自訂服務安全性權杖管理員和自訂服務認證，如下列範例所示。 如需自訂服務認證和服務安全性權杖管理員的詳細資訊，請參閱 [逐步解說：建立自訂用戶端和服務認證](walkthrough-creating-custom-client-and-service-credentials.md)。  
  
     [!code-csharp[c_CustomX509Token#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#5)]
     [!code-vb[c_CustomX509Token#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#5)]  
  
     [!code-csharp[c_CustomX509Token#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#7)]
     [!code-vb[c_CustomX509Token#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#7)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.SecurityKey>
- <xref:System.Security.Cryptography.AsymmetricAlgorithm>
- <xref:System.Security.Cryptography.HashAlgorithm>
- <xref:System.Security.Cryptography.AsymmetricSignatureFormatter>
- [逐步解說：建立自訂用戶端與服務認證](walkthrough-creating-custom-client-and-service-credentials.md)
- [作法：建立自訂安全性權杖驗證器](how-to-create-a-custom-security-token-authenticator.md)
- [作法：建立自訂安全性權杖提供者](how-to-create-a-custom-security-token-provider.md)
- [作法：建立自訂權杖](how-to-create-a-custom-token.md)

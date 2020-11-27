---
title: 作法：建立自訂安全性權杖提供者
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], providing credentials
ms.assetid: db8cb478-aa43-478b-bf97-c6489ad7c7fd
ms.openlocfilehash: 94de506b16d97ec82b84ec6eed34111e99f62977
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249263"
---
# <a name="how-to-create-a-custom-security-token-provider"></a>作法：建立自訂安全性權杖提供者

這個主題會說明如何以自訂安全性權杖提供者建立新的權杖型別，以及如何整合提供者和自訂安全性權杖管理員。  
  
> [!NOTE]
> 如果在 <xref:System.IdentityModel.Tokens> 命名空間中，所找到的系統提供之權杖不符合您的需求，請建立自訂權杖提供者。  
  
 安全性權杖提供者會根據用戶端或服務認證中的資訊，建立安全性權杖表示。 若要在 Windows Communication Foundation 中使用自訂安全性權杖提供者 (WCF) 安全性，您必須建立自訂認證和安全性權杖管理員的建立。  
  
 如需自訂認證和安全性權杖管理員的詳細資訊，請參閱 [逐步解說：建立自訂用戶端和服務認證](walkthrough-creating-custom-client-and-service-credentials.md)。  
  
### <a name="to-create-a-custom-security-token-provider"></a>建立自訂安全性權杖提供者  
  
1. 定義衍生自 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 類別的新類別。  
  
2. 實作 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 方法。 這個方法會負責建立和傳回安全性權杖的執行個體。 下列範例會建立名稱為 `MySecurityTokenProvider` 的類別，並覆寫 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 方法以傳回 <xref:System.IdentityModel.Tokens.X509SecurityToken> 類別的執行個體。 類別建構函式需要 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 類別的執行個體。  
  
     [!code-csharp[c_CustomTokenProvider#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#1)]
     [!code-vb[c_CustomTokenProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#1)]  
  
### <a name="to-integrate-a-custom-security-token-provider-with-a-custom-security-token-manager"></a>整合自訂安全性權杖提供者和自訂安全性權杖管理員  
  
1. 定義衍生自 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 類別的新類別。 (以下範例衍生自 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 類別，而這個類別則衍生自 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 類別)。  
  
2. 如果尚未覆寫 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 方法，請覆寫之。  
  
     <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29>方法負責傳回類別的實例，此 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 類別適用于 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> WCF 安全性架構傳遞給方法的參數。 使用適當的安全性權杖參數呼叫方法時，請修改方法以傳回自訂安全性權杖提供者實作 (在之前的程序中建立此實作)。 如需安全性權杖管理員的詳細資訊，請參閱 [逐步解說：建立自訂用戶端和服務認證](walkthrough-creating-custom-client-and-service-credentials.md)。  
  
3. 將自訂邏輯新增至方法，讓方法可以根據 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 參數傳回自訂安全性權杖提供者。 下列範例會在符合權杖需求時，傳回自訂安全性權杖提供者。 這些需求包括 X.509 安全性權杖和訊息方向 (當權杖用於訊息輸出時)。 在其他情況下，程式碼會呼叫基底類別，以針對其他安全性權杖需求維護系統提供的行為。  
  
 [!code-csharp[c_CustomTokenProvider#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#2)]
 [!code-vb[c_CustomTokenProvider#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#2)]  
  
## <a name="example"></a>範例  

 下列範例會顯示完整 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 實作以及相對應的 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 實作。  
  
 [!code-csharp[c_CustomTokenProvider#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#0)]
 [!code-vb[c_CustomTokenProvider#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#0)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IdentityModel.Selectors.SecurityTokenProvider>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.IdentityModel.Tokens.X509SecurityToken>
- [逐步解說：建立自訂用戶端與服務認證](walkthrough-creating-custom-client-and-service-credentials.md)
- [作法：建立自訂安全性權杖驗證器](how-to-create-a-custom-security-token-authenticator.md)

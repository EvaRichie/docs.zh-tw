---
title: <claimTypeRequirements> 項目
ms.date: 03/30/2017
ms.assetid: a26efe73-4bad-4731-8cad-27f00d54354b
ms.openlocfilehash: b4d8479dd9a24774afbd0549caf9e261f55fa147
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "69926150"
---
# <a name="claimtyperequirements-element"></a>\<claimTypeRequirements> 項目
指定必要宣告型別的集合。  
  
 在聯合案例中，服務會聲明對傳入認證的需求。 例如，傳入認證必須處理特定的一組宣告型別。 這個集合中的每一個子項目都會指定要顯示在聯合認證中的必要和選擇性宣告型別。  
  
 宣告型別需求包含核發之權杖中所要求的宣告型別 URI，以及表示在核發之權杖中宣告型別是必要還是選擇性的布林參數。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ClaimTypeElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [服務身分識別和驗證](../../../wcf/feature-details/service-identity-and-authentication.md)
- [聯合與發行的權杖](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [自訂繫結的安全性功能](../../../wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [聯合與發行的權杖](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [\<add>](add-of-claimtyperequirements.md)
- [繫結](../../../wcf/bindings.md)
- [擴充繫結](../../../wcf/extending/extending-bindings.md)
- [自訂繫結](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [HOW TO：使用 SecurityBindingElement 建立自訂繫結](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [自訂繫結安全性](../../../wcf/samples/custom-binding-security.md)

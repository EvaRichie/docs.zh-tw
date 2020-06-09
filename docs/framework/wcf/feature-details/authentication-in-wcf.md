---
title: WCF 的驗證
ms.date: 03/30/2017
helpviewer_keywords:
- authentication [WCF]
- security [WCF], authentication
ms.assetid: 9254d873-843d-4c6e-bea4-8184ac3e44f4
ms.openlocfilehash: b513c9713bd2c04e125915d1a0a87c86ce249666
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597640"
---
# <a name="authentication-in-wcf"></a>WCF 的驗證
下列主題顯示 Windows Communication Foundation （WCF）中提供驗證的各種不同機制，例如 Windows 驗證、x.509 憑證，以及使用者名稱和密碼。  
  
## <a name="in-this-section"></a>本節內容  
 [如何：使用 ASP.NET 成員資格提供者](how-to-use-the-aspnet-membership-provider.md)  
 ASP.NET 功能包括成員資格及角色提供者、用來儲存驗證時比對的使用者名稱/密碼組合之資料庫，以及供授權的使用者角色。 本主題說明 WCF 服務如何使用相同的資料庫來驗證和授權使用者。  
  
 [如何：使用自訂使用者名稱與密碼驗證程式](how-to-use-a-custom-user-name-and-password-validator.md)  
 示範如何整合自訂使用者名稱與密碼驗證程式。  
  
 [服務身分識別和驗證](service-identity-and-authentication.md)  
 作為額外的保護措施，用戶端可以藉由指定預期的服務身分*識別*來驗證服務。 若預期識別與服務傳回的識別不符，則驗證失敗。  
  
 [安全性交涉與逾時](security-negotiation-and-timeouts.md)  
 說明如何使用 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> 類別中的 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 屬性。  
  
 [偵錯 Windows 驗證錯誤](debugging-windows-authentication-errors.md)  
 焦點放在使用 Windows 驗證時，經常遇見的問題。  
  
## <a name="reference"></a>參考  
 <xref:System.ServiceModel>  
  
## <a name="related-sections"></a>相關章節  
 [常見的安全性案例](common-security-scenarios.md)  
  
## <a name="see-also"></a>請參閱

- [安全性總覽](security-overview.md)
- [Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))

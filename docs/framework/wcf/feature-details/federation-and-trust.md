---
title: 聯合與信任
ms.date: 03/30/2017
helpviewer_keywords:
- federation [WCF], and trust
ms.assetid: 4bdec4f2-f8a2-4512-bdcf-14ef54b5877a
ms.openlocfilehash: 8b924a4aeb9c667592e99d65666cd8f048d34c22
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595475"
---
# <a name="federation-and-trust"></a>聯合與信任
本主題涵蓋與同盟應用程式相關的各種層面、信任界限和設定，以及在 Windows Communication Foundation （WCF）中使用已發行權杖的方式。  
  
## <a name="services-security-token-services-and-trust"></a>服務、安全性權杖服務和信任  
 公開聯合端點的服務，通常會預期用戶端使用特定簽發者所提供的權杖進行驗證。 以正確的簽發者認證設定服務是很重要的，否則該服務將無法確認發行權杖上的簽章，而用戶端將無法與服務通訊。 如需有關在服務上設定簽發者認證的詳細資訊，請參閱 how [to： Configure 認證 on a 同盟服務](how-to-configure-credentials-on-a-federation-service.md)。  
  
 同樣地，在使用對稱金鑰時，由於該金鑰會為目標服務而加密，因此您必須為目標服務以正確的憑證設定安全性權杖服務，否則將無法為目標服務加密金鑰，而因此用戶端將無法與服務通訊。  
  
 WCF 服務會使用 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> [SecurityBindingElement](../diagnostics/wmi/securitybindingelement.md)上的屬性值，以允許用戶端和服務之間的時鐘誤差。 在聯合中，`MaxClockSkew` 設定會從用戶端取得的發行權杖，套用至用戶端和安全性權杖服務間的時鐘誤差。 因此，在設定發行權杖的有效性和到期時間時，安全性權杖服務不需要設定時鐘誤差的上限。  
  
> [!NOTE]
> 時鐘誤差的重要性隨著發行權杖的存留時間縮短而增加。 在大多數的情況下，如果權杖的存留時間為 30 分鐘 (含) 以上，則時鐘誤差就不是個嚴重的問題。 存留時間較短或需要精確驗證權杖時間的案例中，則請務必在設計時考量到時鐘誤差的問題。  
  
## <a name="federated-endpoints-and-time-outs"></a>聯合端點和逾時  
 當用戶端與聯合端點通訊時，必須先從安全性權杖服務取得適當的權杖。 如果安全性權杖服務公開了一個聯合端點，則用戶端必須先從該端點的簽發者取得權杖。 每個權杖的擷取都需要時間，而這些時間會隨著傳送實際訊息至最終端點的整個逾時而變動。  
  
 例如，用戶端通道上的逾時設定為 30 秒。 此時需要呼叫兩個權杖簽發者，以便在傳送訊息至最終端點之前擷取權杖，而每次發行權杖的時間需要 15 秒。 在此例中，此嘗試將會失敗，並會擲回 <xref:System.TimeoutException>。 因此，您必須將用戶端通道上的 <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 值，設定為足以擷取所有發行權杖所需的時間。 在沒有為 <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 屬性指定值的情形下，需要將 <xref:System.ServiceModel.Channels.Binding.OpenTimeout%2A> 屬性或 <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A> 屬性 (或兩者同時) 的值設定為足以擷取所有發行權杖所需的時間。  
  
## <a name="token-lifetime-and-renewal"></a>權杖存留時間和更新  
 對服務提出初始要求時，WCF 用戶端不會檢查發行的權杖。  相反地，WCF 會信任 Security Token Service 來發出具有適當有效和到期時間的權杖。 如果用戶端快取了權杖並重複使用，則會在隨後要求時檢查權杖存留時間，而用戶端則會視需要自動更新權杖。 如需權杖快取的詳細資訊，請參閱[如何：建立同盟用戶端](how-to-create-a-federated-client.md)。  
  
 針對發行的權杖或安全性內容權杖，指定短存留期（以30秒或更少的順序），可能會導致在要求發行的權杖或協商或更新安全性內容權杖時，WCF 用戶端擲回的協商超時或其他例外狀況。  
  
## <a name="issued-tokens-and-inclusionmode"></a>發行的權杖和 InclusionMode  
 從用戶端傳送至聯合端點的訊息中，其發行的權杖是否已序列化是由設定 <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InclusionMode%2A> 類別的 <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> 屬性所控制。 這個屬性可以設定為 <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode> 列舉值的其中一個值，但是這在大部分的聯合案例中沒有作用。 `SecurityTokenInclusionMode.Never` 和 `SecurityTokenInclusionMode.AlwaysToInitiator` 值會使用戶端將權杖參考，傳送給安全性權杖服務所發行給信賴憑證者的權杖。 除非信賴憑證者持有發行權杖的複本，否則驗證將會因為無法解析權杖參考而失敗。 WCF 會 `SecurityTokenInclusionMode.Once` 將視為相當於 `SecurityTokenInclusionMode.AlwaysToRecipient` 。  
  
## <a name="see-also"></a>請參閱

- <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>
- [如何：建立同盟用戶端](how-to-create-a-federated-client.md)
- [HOW TO：設定聯合服務的認證](how-to-configure-credentials-on-a-federation-service.md)
- [如何：建立 WSFederationHttpBinding](how-to-create-a-wsfederationhttpbinding.md)

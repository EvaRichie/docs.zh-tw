---
title: 權限提高
ms.date: 03/30/2017
helpviewer_keywords:
- elevation of privilege [WCF]
- security [WCF], elevation of privilege
ms.assetid: 146e1c66-2a76-4ed3-98a5-fd77851a06d9
ms.openlocfilehash: 9c62e11eedaa3fa194522695a33bccf210d390df
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254216"
---
# <a name="elevation-of-privilege"></a>權限提高

提高 *許可權的* 結果，是授與攻擊者授權許可權，但不超過最初授與的許可權。 例如，具有「唯讀」權限的攻擊者以不明方式將權限提高為「讀取和寫入」。  
  
## <a name="trusted-sts-should-sign-saml-token-claims"></a>受信任的 STS 應該簽署 SAML 權杖宣告  

 安全性判斷提示標記語言 (SAML) 權杖是一種泛型 XML 權杖，同時也是預設的發行權杖類型。 在典型的交換中，結尾 Web 服務所信任的安全性權杖服務 (STS) 可以建構 SAML 權杖。 SAML 權杖會在陳述式中包含宣告。 攻擊者可從有效權杖中複製宣告、建立新的 SAML 權杖，然後使用不同的簽發者進行簽署。 其目的就是判斷伺服器是否正在驗證簽發者，如果不是的話，會運用弱點來建構 SAML 權杖，針對受信任 STS 原先要賦予的權限賦予更多的權限。  
  
 <xref:System.IdentityModel.Tokens.SamlAssertion> 類別會驗證 SAML 權杖中包含的數位簽章，而預設的 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 則要求當 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> 類別的 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> 設為 <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust> 時，必須使用有效的 X.509 憑證來簽署 SAML 權杖。 單是 `ChainTrust` 模式還不足以判斷 SAML 權杖的簽發者是否受信任。 需要更細微信任模型的服務可以使用授權與強制執行原則來檢查由已發行權杖驗證所產生的宣告集之簽發者，或是使用 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> 上的 X.509 驗證設定來限制允許的簽署憑證集。 如需詳細資訊，請參閱使用身分識別模型和[同盟和發行的權杖](federation-and-issued-tokens.md)來[管理宣告與授權](managing-claims-and-authorization-with-the-identity-model.md)。  
  
## <a name="switching-identity-without-a-security-context"></a>切換不含安全性內容的身分識別  

 以下僅適用于 WinFX。  
  
 當用戶端與伺服器之間建立連線時，用戶端的身分識別不會變更，但在下列情況下：開啟 WCF 用戶端之後，如果下列所有條件都成立的話：  
  
- 建立安全性內容 (使用傳輸安全性會話或訊息安全性會話的程式) 關閉 (<xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 屬性會設定為， `false` 以防訊息安全性或傳輸無法建立安全性會話時，會在傳輸安全性案例中使用。 HTTPS 即是此類傳輸的範例之一)。  
  
- 您目前使用 Windows 驗證。  
  
- 您未明確設定認證。  
  
- 您在模擬的安全性內容中呼叫服務。  
  
 如果這些條件成立，用來向服務驗證用戶端的身分識別可能會變更 (可能不是模擬的身分識別，但在開啟 WCF 用戶端之後，仍) 進程身分識別。 這是因為用來向服務驗證用戶端的 Windows 認證會隨著每個訊息一併傳輸，而用來驗證的認證則是從目前執行緒的 Windows 識別取得。 如果目前執行緒的 Windows 識別變更 (例如，藉由模擬不同的呼叫者)，則附加至訊息並用來向服務驗證用戶端的認證可能會一併變更。  
  
 如果您希望在合併使用 Windows 驗證與模擬機制時擁有決定性行為，則您需要明確地設定 Windows 認證，或是需要建立服務的安全性內容。 若要這麼做，請使用訊息安全性工作階段或傳輸安全性工作階段。 例如，net.tcp 傳輸可以提供傳輸安全性工作階段。 此外，在呼叫服務時，只能使用同步版本的用戶端作業。 如果您建立訊息安全性內容，那麼與服務保持連線的時間不應該比設定的工作階段更新期間還長，因為身分識別也會在工作階段更新處理期間變更。  
  
### <a name="credentials-capture"></a>認證擷取  

 以下適用于 .NET Framework 3.5 和後續版本。  
  
 用戶端或服務所使用的認證，係依據目前的內容執行緒而定。 認證會在呼叫用戶端或服務的 `Open` 方法時取得，如果是非同步呼叫 (Asynchronous Call)，則是在呼叫 `BeginOpen` 方法時取得。 對於 <xref:System.ServiceModel.ServiceHost> 和 <xref:System.ServiceModel.ClientBase%601> 類別而言，`Open` 和 `BeginOpen` 方法是繼承自 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 類別的 <xref:System.ServiceModel.Channels.CommunicationObject.BeginOpen%2A> 和 <xref:System.ServiceModel.Channels.CommunicationObject> 方法。  
  
> [!NOTE]
> 使用 `BeginOpen` 方法時，所擷取的認證無法保證一定是呼叫該方法的處理序認證。  
  
## <a name="token-caches-allow-replay-using-obsolete-data"></a>權杖快取允許重新執行使用已過時資料  

 WCF 會使用本地安全機構 (LSA) `LogonUser` 函數，依使用者名稱和密碼來驗證使用者。 因為登入函式是成本高昂的作業，所以 WCF 可讓您快取代表已驗證使用者的權杖，以提升效能。 快取機制可儲存 `LogonUser` 的結果以供後續使用。 此機制預設為停用;若要啟用它，請將 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CacheLogonTokens%2A> 屬性設定為 `true` ，或使用的 `cacheLogonTokens` 屬性 [\<userNameAuthentication>](../../configure-apps/file-schema/wcf/usernameauthentication.md) 。  
  
 您可以將 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CachedLogonTokenLifetime%2A> 屬性 (Property) 設為 <xref:System.TimeSpan>，或是使用 `cachedLogonTokenLifetime` 項目的 `userNameAuthentication` 屬性 (Attribute) 為快取權杖設定存留時間 (TTL)；預設時間為 15 分鐘。 請注意，一旦快取了權杖，任何使用相同使用者名稱與密碼的用戶端都可以使用該權杖，就算使用者帳戶已從 Windows 中刪除，或當其密碼已經變更也是一樣。 在 TTL 到期且權杖從快取中移除之前，WCF 可讓 (可能是惡意的) 使用者進行驗證。  
  
 若要緩解這個情況：請將 `cachedLogonTokenLifetime` 值設為使用者所需的最短時間範圍來減少可能遭受攻擊的時間範圍。  
  
## <a name="issued-token-authorization-expiration-reset-to-large-value"></a>發行的權杖授權：到期日重設為較大值  

 在特定情況下，<xref:System.IdentityModel.Policy.AuthorizationContext.ExpirationTime%2A> 的 <xref:System.IdentityModel.Policy.AuthorizationContext> 屬性可以設為超出預期的較大值 (<xref:System.DateTime.MaxValue> 欄位值減掉一天，或是 9999 年 12 月 20 日)。  
  
 當您使用 <xref:System.ServiceModel.WSFederationHttpBinding> 以及任何將已發行權杖當成用戶端認證類型來使用的系統提供繫結時，就會發生這種情況。  
  
 當您使用下列其中一種方法來建立自訂繫結時，也會發生這種情況：  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A>  
  
 若要緩解這個情況，授權原則必須檢查每個授權原則的動作與到期時間。  
  
## <a name="the-service-uses-a-different-certificate-than-the-client-intended"></a>服務使用的憑證不同於用戶端原先想要的憑證  

 在特定情況下，用戶端可以使用 X.509 憑證來數位簽署訊息，並讓服務擷取與原先不同的憑證。  
  
 在下列狀況下可能會發生這種情形：  
  
- 用戶端使用 X.509 憑證來數位簽署訊息，而且未將 X.509 憑證附加至訊息，只有使用其主體金鑰識別碼來參照憑證。  
  
- 服務的電腦包含兩個以上的憑證具有相同的公開金鑰，但是憑證中包含不同的資訊。  
  
- 服務擷取的憑證符合主體主鑰識別碼，但不是用戶端原先想要使用的那組憑證。 當 WCF 接收訊息並驗證簽章時，WCF 會將非預期的 x.509 憑證中的資訊對應到一組不同的宣告，而且可能會從用戶端預期的許可權提升。  
  
 若要緩解這個情況，請以另一種方式來參照 X.509 憑證，例如使用 <xref:System.ServiceModel.Security.Tokens.X509KeyIdentifierClauseType.IssuerSerial>。  
  
## <a name="see-also"></a>另請參閱

- [安全性考量](security-considerations-in-wcf.md)
- [洩露資訊](information-disclosure.md)
- [拒絕服務](denial-of-service.md)
- [重新執行攻擊](replay-attacks.md)
- [竄改](tampering.md)
- [不支援的案例](unsupported-scenarios.md)

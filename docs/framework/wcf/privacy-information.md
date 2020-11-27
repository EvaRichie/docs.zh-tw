---
title: Windows Communication Foundation 隱私權資訊
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, privacy information
- WCF, privacy information
- privacy information [WCF]
ms.assetid: c9553724-f3e7-45cb-9ea5-450a22d309d9
ms.openlocfilehash: 5ecd1c39a4ad6a146c734aab8349c5caa4212662
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249939"
---
# <a name="windows-communication-foundation-privacy-information"></a>Windows Communication Foundation 隱私權資訊

Microsoft 致力於保護終端使用者隱私權。 當您使用 Windows Communication Foundation (WCF) 3.0 版來建立應用程式時，您的應用程式可能會影響使用者的隱私權。 例如，應用程式可能會明確收集使用者的連絡資訊，或者透過網際網路向您的網站要求資訊或傳送資訊至網站。 如果您在應用程式中內嵌 Microsoft 技術，則該技術可能帶有會影響隱私權的行為。 WCF 不會從您的應用程式將任何資訊傳送給 Microsoft，除非您或使用者選擇將它傳送給我們。  
  
## <a name="wcf-in-brief"></a>WCF 簡介  

 WCF 是使用 Microsoft .NET Framework 的分散式訊息架構，可讓開發人員建立分散式應用程式。 而在兩個應用程式之間通訊的訊息則包含標頭和本文資訊。  
  
 根據應用程式使用的服務而定，標頭可能包含訊息路由、安全性資訊、異動及其他項目。 根據預設，訊息通常會經過加密。 唯一的例外為使用 `BasicHttpBinding` 時，此項原本就設計用於不受安全保護的舊式 Web 服務。 身為應用程式設計師，您要負責做好最後的設計。 SOAP 主體中的訊息包含應用程式特定的資料;不過，這類資料（例如應用程式定義的個人資訊）可以使用 WCF 加密或機密性功能來保護。 下列章節將描述可能影響隱私權的功能。  
  
## <a name="messaging"></a>訊息傳送  

 每個 WCF 訊息都有位址標頭，可指定訊息目的地，以及回復應移至的位置。  
  
 端點位址的位址元件則是可識別端點的統一資源識別元 (URI)。 此位址可以是網路位址或邏輯位址。 位址也可能包含電腦名稱 (主機名稱，完整網域名稱) 和 IP 位址。 端點位址也可能包含全域唯一識別元 (GUID)，或者包含可用於分辨每個位址之暫存定址的 GUID 集合。 每則訊息中都包含屬於 GUID 的訊息識別碼。 另外，此功能會遵循 WS-Addressing 參照標準。  
  
 WCF 訊息層不會將任何個人資訊寫入本機電腦。 不過，如果服務開發人員建立了會公開這類資訊的服務 (例如，在端點名稱中使用某個人的名稱，或者在端點的 Web 服務描述語言中加入個人資訊，可是沒有要求用戶端使用 https 來存取 WSDL)，則該訊息層可能在網路層級中傳播個人資訊。 此外，如果開發人員在公開個人資訊的端點上執行 [內容] [中繼資料公用程式工具 ( # A0) ](servicemodel-metadata-utility-tool-svcutil-exe.md) 工具，則工具的輸出可能會包含該資訊，而且輸出檔會寫入本機硬碟。  
  
## <a name="hosting"></a>裝載  

 WCF 中的裝載功能可讓應用程式視需要啟動，或在多個應用程式之間啟用埠共用。 WCF 應用程式可裝載于 Internet Information Services 的 (IIS) ，類似于 ASP.NET。  
  
 裝載時並不會在網路上公開任何特定資訊，而且也不會保存電腦上的資料。  
  
## <a name="message-security"></a>訊息安全性  

 WCF 安全性提供訊息應用程式的安全性功能。 所提供的安全性功能包含驗證和授權。  
  
 驗證的作法是在用戶端和服務之間傳遞認證。 您可以透過傳輸層級安全性或 SOAP 訊息層級安全性來進行驗證，如下所示：  
  
- 在 SOAP 訊息安全性中，可以透過使用者名稱/密碼、X.509 憑證、Kerberos 票證和 SAML 語彙基元這類認證來執行驗證，而視簽發者而定，這些認證中可能含有個人資訊。  
  
- 使用傳輸安全性時，則可藉由 HTTP 驗證配置 (Basic、Digest、Negotiate、Integrated Windows Authorization、NTLM、None 和 Anonymous) 這種傳統傳輸驗證機制和表單驗證，來處理驗證動作。  
  
 執行驗證之後，會在進行通訊的端點之間建立安全工作階段。 這個工作階段是由會在安全性工作階段的存留期間持續活動的 GUID 所識別。 下表會顯示所保留的項目的位置。  
  
|資料|儲存體|  
|----------|-------------|  
|展示認證，例如使用者名稱、X.509 憑證、Kerberos 語彙基元和認證的各種參照。|標準 Windows 認證管理機制，例如 Windows 憑證存放庫。|  
|使用者成員資格資訊，例如使用者名稱和密碼。|ASP.NET 成員資格提供者。|  
|身分識別服務的相關資訊，此服務是用來驗證用戶端的服務。|服務的端點位址。|  
|呼叫端資訊。|稽核記錄。|  
  
## <a name="auditing"></a>稽核  

 稽核會記錄驗證和授權事件的成功與失敗。 稽核記錄中則包含下列資料：服務 URI、動作 URI 和呼叫端的識別。  
  
 稽核也會記錄系統管理員修改訊息記錄組態 (開啟或關閉) 的時間，這是因為訊息記錄可能會在標頭和本文中記錄應用程式特定的資料。 若為 Windows XP，記錄會記錄在應用程式事件記錄檔中。 在 Windows Vista 和 Windows Server 2003 中，記錄會記錄在安全性事件記錄檔中。  
  
## <a name="transactions"></a>交易  

 交易功能會將交易式服務提供給 WCF 應用程式。  
  
 交易傳播中使用的交易標頭可能包含屬於 GUID 的交易識別碼或登記識別碼。  
  
 異動功能會使用 Microsoft Distributed Transaction Coordinator (MSDTC) 的異動管理員 (一種 Windows 元件) 來管理異動狀態。 根據預設，系統會加密異動管理員之間的通訊。 交易管理員可能會記錄端點參照、交易識別碼和登記識別碼，作為其長期狀態的一部分。 這個狀態的存留期則是由異動管理員的記錄檔存留期所決定。 MSDTC 服務則擁有並維護此記錄。  
  
 異動功能會實作 WS-Coordination 和 WS-Atomic 異動標準。  
  
## <a name="reliable-sessions"></a>可靠工作階段  

 WCF 中的可靠會話可在發生傳輸或媒介失敗時，提供訊息的傳輸。 即使中斷基礎傳輸 (例如，無線網路上的 TCP 連線) 或遺失訊息 (HTTP Proxy 捨棄了傳出或傳入的訊息)，這些可靠的工作階段仍可確實傳送一次訊息。 可靠的工作階段也會復原重新排列順序後的訊息 (在多路徑路由時可能會發生)，保留訊息傳送的順序。  
  
 您可以使用 WS-ReliableMessaging (WS-RM) 通訊協定來實作可靠的工作階段。 這些工作階段會新增其中包含工作階段資訊的 WS-RM 標頭，而您可以使用此資訊來識別與特定可靠的工作階段相關聯的所有訊息。 每個 WS-RM 工作階段都有識別碼，也就是 GUID。  
  
 終端使用者的電腦上不會保留任何個人資訊。  
  
## <a name="queued-channels"></a>佇列通道  

 佇列可代表接收應用程式，存放來自傳送應用程式的訊息，並在稍後將這些訊息轉寄至接收應用程式。 例如，接收應用程式為暫時性時，使用佇列將協助確保訊息的傳輸，從傳送應用程式至接收應用程式。 WCF 提供使用 Microsoft Message Queuing (MSMQ) 做為傳輸的佇列支援。  
  
 佇列通道功能不會將標頭新增至訊息。 該功能會以適當的 [訊息佇列] 訊息屬性設定，來建立 [訊息佇列] 的訊息，並叫用 [訊息佇列] 方法以將訊息放置在 [訊息佇列] 的佇列中。 [訊息佇列] 是隨附於 Windows 的選用元件。  
  
 佇列通道功能不會在終端使用者的電腦上保留任何資訊，因為它會使用訊息佇列作為佇列基礎結構。  
  
## <a name="com-integration"></a>COM+ 整合  

 這項功能會包裝現有的 COM 和 COM + 功能，以建立與 WCF 服務相容的服務。 這項功能不會使用特定標頭，也不會在終端使用者的電腦上保留資料。  
  
## <a name="com-service-moniker"></a>COM 服務 Moniker  

 這會提供標準 WCF 用戶端的非受控包裝函式。 這項功能在網路上沒有特定的標頭，也不會在電腦上保留任何資料。  
  
## <a name="peer-channel"></a>對等通道  

 對等通道可讓您使用 WCF 進行多方應用程式的開發。 多方通訊會以網狀結構的脈絡發生。 [網狀結構] 是依照各節點可加入的名稱所識別。 對等通道中的每個節點都會在使用者指定的連接埠上建立 TCP 接聽項，並與網狀結構中的其他節點建立連線以確保擁有回復性。 若要連線至網狀結構中的其他節點，節點也必須與網狀結構中的其他節點交換資料，包括接聽項位址和電腦的 IP 位址。 在網狀結構中來回傳送的訊息會包含專屬於傳送者的安全性資訊，因此可防止發生訊息詐騙和竄改。  
  
 終端使用者的電腦上不會儲存任何個人資訊。  
  
## <a name="it-professional-experience"></a>IT 專業人員的體驗  
  
### <a name="tracing"></a>追蹤  

 WCF 基礎結構的診斷功能會記錄透過傳輸和服務模型層所傳遞的訊息，以及與這些訊息相關聯的活動和事件。 此功能預設為關閉。 您可以使用應用程式的設定檔來啟用此功能，而且可能會在執行時間使用 WCF WMI 提供者修改追蹤行為。 啟用此功能時，追蹤基礎結構會將包含訊息、活動和處理事件的診斷追蹤，發送至已設定的接聽項。 輸出的格式和位置是由系統管理員的接聽程式組態選項來決定，不過通常會是 XML 格式的檔案。 系統管理員要負責設定追蹤檔上的存取控制清單 (ACL)。 由 Windows Activation System (WAS) 裝載時，系統管理員更應該確定在非必須的情況下，不是從公開的虛擬根目錄使用檔案。  
  
 追蹤的類型有兩種：訊息記錄和服務模型診斷追蹤，分別會在下節中描述。 這兩個類型的追蹤也可透過本身的追蹤來源進行設定：<xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A> 和 <xref:System.ServiceModel>。 這些記錄追蹤來源都會擷取對應用程式而言為本機的資料。  
  
### <a name="message-logging"></a>訊息記錄  

 訊息記錄追蹤來源 (<xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>) 可讓系統管理員記錄在系統來回傳送的訊息。 透過組態，使用者可以決定要記錄整個訊息或僅記錄訊息標頭、是否要在傳輸層及 (或) 服務模型層記錄，以及是否包含格式不正確的訊息。 此外，使用者也可以設定篩選以限制要記錄的訊息。  
  
 根據預設，訊息記錄呈停用狀態。 而本機電腦的系統管理員可以防止應用程式層級的管理員開啟訊息記錄功能。  
  
#### <a name="encrypted-and-decrypted-message-logging"></a>加密和解密的訊息記錄  

 系統會對訊息進行記錄、加密或解密，如下列詞彙所述。  
  
 傳輸記錄  
 記錄在傳輸層級接收和傳送的訊息。 這些訊息包含所有標頭，而且可能會在網路上傳送前和收到訊息時加密。  
  
 如果訊息是在網路上傳送之前以及收到時進行加密，那麼這些訊息也會以加密記錄。 使用安全性通訊協定 (https) 則為例外：即使在網路上加密這些訊息，仍會在傳送之前和接收之後，以解密記錄。  
  
 服務記錄  
 記錄在服務模型層級、發生通道標頭處理之後以及輸入使用者程式碼之前與之後所接收或傳送的訊息。  
  
 在此層級記錄的訊息即使已安全保護並且在網路上加密，仍會進行解密。  
  
 格式不正確的訊息記錄  
 記錄 WCF 基礎結構無法瞭解或處理的訊息。  
  
 會以現狀記錄訊息，也就是加密或未加密的狀態。  
  
 以解密或未加密形式記錄訊息時，WCF 預設會在記錄訊息之前，先從訊息移除安全性金鑰和可能的個人資訊。 下面章節會描述要移除的資訊以及移除的時機。 電腦的系統管理員和應用程式開發人員都必須採取特定的組態動作，才能變更行為以記錄金鑰和可能的個人資訊。  
  
#### <a name="information-removed-from-message-headers-when-logging-decryptedunencrypted-messages"></a>記錄解密/未加密訊息時，從訊息標頭中移除的資訊  

 以解密/未加密形式記錄訊息時，在記錄訊息之前，預設會從訊息標頭和訊息本文中移除安全性金鑰和可能會有的個人資訊。 下列清單顯示 WCF 會將金鑰和可能的個人資訊列入考慮。  
  
 移除的金鑰：  
  
 \- 若為 xmlns： wst = " http://schemas.xmlsoap.org/ws/2004/04/trust " 和 xmlns： wst = " http://schemas.xmlsoap.org/ws/2005/02/trust "  
  
 wst:BinarySecret  
  
 wst:Entropy  
  
 \- 若為 xmlns： wsse = " http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.1.xsd " 和 xmlns： wsse = " http://docs.oasis-open.org/wss/2005/xx/oasis-2005xx-wss-wssecurity-secext-1.1.xsd "  
  
 wsse:Password  
  
 wsse:Nonce  
  
 移除的可能個人資訊：  
  
 \- 若為 xmlns： wsse = " http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.1.xsd " 和 xmlns： wsse = " http://docs.oasis-open.org/wss/2005/xx/oasis-2005xx-wss-wssecurity-secext-1.1.xsd "  
  
 wsse:Username  
  
 wsse:BinarySecurityToken  
  
 \- 若為 xmlns： saml = "urn： oasis： names： tc： SAML：1.0： assertion"，則會移除以下) 中的專案（粗體 (）：  
  
 \<斷言  
  
 MajorVersion="1"  
  
 MinorVersion="1"  
  
 AssertionId="[ID]"  
  
 Issuer="[string]"  
  
 IssueInstant="[dateTime]"  
  
 >  
  
 \<Conditions NotBefore="[dateTime]" NotOnOrAfter="[dateTime]">  
  
 \<AudienceRestrictionCondition>  
  
 \<Audience>url\</Audience>+  
  
 \</AudienceRestrictionCondition>*  
  
 \<DoNotCacheCondition />*  
  
 <\!--抽象基底類型  
  
 \<Condition />*  
  
 -->  
  
 \</Conditions>?  
  
 \<Advice>  
  
 \<AssertionIDReference>識別碼\</AssertionIDReference>*  
  
 \<Assertion>assertion\</Assertion>*  
  
 [any]*  
  
 \</Advice>?  
  
 <\!--抽象基底類型  
  
 \<Statement />*  
  
 \<SubjectStatement>  
  
 \<Subject>  
  
 `<NameIdentifier`  
  
 `NameQualifier="[string]"?`  
  
 `Format="[uri]"?`  
  
 `>`  
  
 `[string]`  
  
 `</NameIdentifier>?`  
  
 \<SubjectConfirmation>  
  
 \<ConfirmationMethod>AnyUri\</ConfirmationMethod>+  
  
 \<SubjectConfirmationData>[任何] \</SubjectConfirmationData> ？  
  
 \<ds:KeyInfo>...\</ds:KeyInfo>?  
  
 \</SubjectConfirmation>?  
  
 \</Subject>  
  
 \</SubjectStatement>*  
  
 -->  
  
 \<AuthenticationStatement  
  
 AuthenticationMethod="[uri]"  
  
 AuthenticationInstant="[dateTime]"  
  
 >  
  
 [主旨]  
  
 `<SubjectLocality`  
  
 `IPAddress="[string]"?`  
  
 `DNSAddress="[string]"?`  
  
 `/>?`  
  
 <AuthorityBinding  
  
 AuthorityKind="[QName]"  
  
 Location="[uri]"  
  
 Binding="[uri]"  
  
 />*  
  
 \</AuthenticationStatement>*  
  
 \<AttributeStatement>  
  
 [主旨]  
  
 \<屬性  
  
 AttributeName="[string]"  
  
 AttributeNamespace="[uri]"  
  
 >  
  
 `<AttributeValue>[any]</AttributeValue>+`  
  
 \</Attribute>+  
  
 \</AttributeStatement>*  
  
 \<AuthorizationDecisionStatement  
  
 Resource="[uri]"  
  
 決策 = "[允許&#124;拒絕&#124;不定]]  
  
 >  
  
 [主旨]  
  
 \<Action Namespace="[uri]">字串\</Action>+  
  
 \<Evidence>  
  
 \<AssertionIDReference>識別碼\</AssertionIDReference>+  
  
 \<Assertion>assertion\</Assertion>+  
  
 \</Evidence>?  
  
 \</AuthorizationDecisionStatement>*  
  
 \</Assertion>  
  
#### <a name="information-removed-from-message-bodies-when-logging-decryptedunencrypted-messages"></a>記錄解密/未加密訊息時，從訊息本文中移除的資訊  

 如先前所述，WCF 會從訊息標頭移除金鑰和已知的可能個人資訊，以取得已記錄的解密/未加密訊息。 此外，WCF 也會從訊息內文中移除主體專案的訊息主體和已知的潛在個人資訊，以描述與金鑰交換相關的安全性訊息。  
  
 若為下列命名空間：  
  
 xmlns： wst = " http://schemas.xmlsoap.org/ws/2004/04/trust " 和 xmlns： wst = " http://schemas.xmlsoap.org/ws/2005/02/trust " (例如，如果沒有可用的動作)   
  
 將移除這些本文項目的資訊，而這些本文項目牽涉到金鑰交換：  
  
 wst:RequestSecurityToken  
  
 wst:RequestSecurityTokenResponse  
  
 wst:RequestSecurityTokenResponseCollection  
  
 也會移除下列每個動作的資訊：  
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Issue`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Issue`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Validate`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Validate`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Amend`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Amend`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RST/SCT`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RSTR/SCT`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RST/SCT-Amend`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RSTR/SCT-Amend`
  
#### <a name="no-information-is-removed-from-application-specific-headers-and-body-data"></a>不會從應用程式特定標頭和本文資料中移除資訊  

 WCF 不會追蹤應用程式特定標頭中的個人資訊 (例如，查詢字串) 或主體資料 (例如) 的信用卡號碼。  
  
 訊息記錄啟用時，也許可以在記錄中看見應用程式特定標頭和本文資訊中的個人資訊。 因此，應用程式部署者應負責設定組態和記錄檔的 ACL。 如果他們不想要顯示記錄，也可以關閉記錄功能，或是在記錄檔中篩選出這些資訊。  
  
### <a name="service-model-tracing"></a>服務模型追蹤  

 服務模型追蹤來源 (<xref:System.ServiceModel>) 會啟用與訊息處理相關的活動和事件追蹤。 這個功能會從 <xref:System.Diagnostics> 使用 .NET Framework 的診斷功能。 在搭配 <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A> 屬性時，使用者可以使用 .NET Framework 應用程式組態檔來設定位置和 ACL。 使用訊息記錄時，只要系統管理員啟用追蹤就一定會設定檔案位置，這表示系統管理員控制了 ACL。  
  
 當訊息在範圍內時，追蹤就包含訊息標頭。 有關上一節所提及之隱藏訊息標頭中的潛在個人資訊，其對應的相同規則也適用：預設會從追蹤中的標頭移除先前所識別的個人資訊。 電腦系統管理員和應用程式部署者都必須修改組態，才能記錄可能的個人資訊。 不過，應用程式特定標頭所含的個人資訊則會記錄在追蹤中。 應用程式部署者應負責設定組態和追蹤檔的 ACL。 它們也可以關閉追蹤，以隱藏此資訊，或在記錄追蹤檔案之後篩選出這些資訊。  
  
 在進行 ServiceModel 追蹤時，當訊息在基礎結構的不同部分傳遞時，唯一識別碼 (又稱為活動識別碼，而且通常為 GUID) 就會將不同的活動連結起來。  
  
#### <a name="custom-trace-listeners"></a>自訂追蹤接聽項  

 您可以對訊息記錄和追蹤設定自訂追蹤接聽項，這樣就可在網路上傳送追蹤和訊息 (例如，傳送至遠端資料庫)。 應用程式部署者負責設定自訂接聽項或讓使用者進行自訂。 它們也會負責在遠端位置公開的任何個人資訊，並適當地將 Acl 套用到這個位置。  
  
### <a name="other-features-for-it-professionals"></a>IT 專業人員可用的其他功能  

 WCF 有一個 WMI 提供者，可透過 Windows) 隨附的 WMI (公開 WCF 基礎結構設定資訊。 根據預設，系統管理員將可使用 WMI 介面。  
  
 WCF 設定會使用 .NET Framework 設定機制。 而這些組態檔會存放在電腦上。 應用程式開發人員和系統管理員會針對每項應用程式需求而建立組態檔和 ACL。 組態檔中包含了一些端點位址和連結，可連接到憑證存放區的憑證。 您可以使用憑證來提供應用程式資料，進而可設定應用程式所使用的各種功能屬性。  
  
 WCF 也會藉由呼叫方法來使用 .NET Framework 進程傾印功能 <xref:System.Environment.FailFast%2A> 。  
  
### <a name="it-pro-tools"></a>IT 專業人員工具  

 WCF 也提供下列 IT 專業工具，其隨附于 Windows SDK。  
  
#### <a name="svctraceviewerexe"></a>SvcTraceViewer.exe  

 檢視器會顯示 WCF 追蹤檔。 也會顯示追蹤內所含的任何資訊。  
  
#### <a name="svcconfigeditorexe"></a>SvcConfigEditor.exe  

 編輯器允許使用者建立和編輯 WCF 設定檔。 這個編輯器還會顯示組態檔中所含的任何資訊。 使用文字編輯器也可完成同樣的工作。  
  
#### <a name="servicemodel_reg"></a>ServiceModel_Reg  

 這個工具可讓使用者管理電腦上的 ServiceModel 安裝。 工具執行時，此工具會在主控台視窗中顯示狀態訊息，而在此程式中，可能會顯示 WCF 安裝設定的相關資訊。  
  
#### <a name="wsatconfigexe-and-wsatuidll"></a>WSATConfig.exe 和 WSATUI.dll  

 這些工具可讓 IT 專業人員在 WCF 中設定可互通的 WS-AtomicTransaction 網路支援。 這些工具會顯示存放在登錄的最常用 WS-AtomicTransaction 設定值，也可讓使用者變更這些值。  
  
## <a name="cross-cutting-features"></a>跨領域功能  

 下列功能為跨領域功能。 也就是說，可以使用前面提及的任何功能來組成不同的功能。  
  
### <a name="service-framework"></a>服務架構  

 標頭中可含執行個體識別碼，這是會使訊息與 CLR 類別的執行個體產生關聯的 GUID。  
  
 Web 服務描述語言 (WSDL) 中包含了連接埠定義。 每個連接埠都有端點位址，以及表示應用程式所使用服務的繫結。 您可以透過組態決定是否公開 WSDL。 在電腦上不會保留任何資訊。  
  
## <a name="see-also"></a>另請參閱

- [Windows Communication Foundation](index.md)
- [安全性](./feature-details/security.md)

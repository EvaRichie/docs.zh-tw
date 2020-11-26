---
title: 保護服務的安全
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [WCF], securing services
- WCF security
- WCF, security
ms.assetid: f0ecc6f7-f4b5-42a4-9cb1-b02e28e26620
ms.openlocfilehash: f2a8e10aaf9c1dbe3065344963fcc712776cd2db
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242223"
---
# <a name="securing-services"></a>保護服務的安全

Windows Communication Foundation (WCF) 服務的安全性是由兩個主要需求所組成：傳輸安全性和授權。  (第三個需求，安全性事件的審核會在 [審核](./feature-details/auditing-security-events.md)中說明。 ) 簡單的說，傳輸安全性包含驗證 (驗證服務和用戶端) 的身分識別、機密性 (訊息加密) 和完整性 (數位簽章來偵測篡改) 。 授權會控制存取資源，例如，只允許有權限的使用者讀取檔案。 使用 WCF 的功能，可輕鬆地執行這兩個主要需求。  
  
 除了 <xref:System.ServiceModel.BasicHttpBinding> 類別 (或設定 [\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md)) 中的元素之外，所有預先定義的系結預設都會啟用傳輸安全性。 本節中的主題涵蓋兩個基本案例：在裝載於 Internet Information Services (IIS) 的內部網路服務上實作傳輸安全性和授權，以及在裝載於 IIS 的服務上實作傳輸安全性和授權。  
  
> [!NOTE]
> Windows XP Home 不支援 Windows 驗證。 因此，您不應該在該系統上執行服務。  
  
## <a name="security-basics"></a>安全性基本概念  

 安全性仰賴「 *認證*」(Credential)。 認證會證明實體如其宣告所言  (*實體* 可以是個人、軟體程式、公司，或任何可獲得授權的。 ) 例如，服務的用戶端 *會建立身分**識別* 的宣告，而認證會以某種方式證明該宣告。 在一般情況下，會發生認證交換。 首先，服務會宣告其身分識別，並使用認證，向用戶端證明它自己。 反之，用戶端會宣告身分識別，並向服務出示認證。 如果雙方信任對方的認證，則會建立「 *安全內容* 」(Secure Context)，其中的所有訊息都會以機密方式交換，而且所有訊息也都會簽署以保護其完整性。 當服務建立用戶端的身分識別之後，就可以將認證中的宣告與群組中的「 *角色* 」(Role) 或「 *成員資格* 」(Membership) 比對。 在這兩種情況下，服務會使用用戶端所屬的角色或群組，根據角色或群組權限「 *授權* 」(Authorize) 用戶端執行一組受限制的作業。  
  
## <a name="windows-security-mechanisms"></a>Windows 安全性機制  

 如果用戶端和服務電腦都位在要求兩者登入網路的 Windows 網域上，Windows 基礎結構會提供認證。 在這種情況下，當電腦使用者登入網路時，會建立認證。 網路上的每個使用者和每台電腦都必須經驗證為屬於受信任的使用者和電腦集合。 在 Windows 系統上，這類使用者和電腦也稱為「 *安全性主體*」(Security Principal)。  
  
 在 *Kerberos* 控制器支援的 Windows 網域上，Kerberos 控制器會使用對每個安全性主體授與票證的配置。 系統中其他票證授與者都會信任控制器所授與的票證。 當實體嘗試執行特定作業或存取「 *資源* 」(Resource) (例如電腦上的檔案或目錄) 時，會檢查票證有效性，如果通過，則會授與主體另一個用於作業的票證。 授與票證的方法比起在每個作業驗證主體的方法更有效率。  
  
 Windows 網域上較不安全的舊型機制是 NT LAN Manager (NTLM)。 在無法使用 Kerberos (通常是在 Windows 網域之外，例如工作群組) 的情況下，NTLM 可以做為替代方法。 NTLM 也是 IIS 的安全性選項。  
  
 在 Windows 系統上，授權的運作方式是，將每台電腦和每個使用者指派至一組角色和群組。 例如，每台 Windows 電腦都必須由身為「 *系統管理員*」(Administrator) 角色的人員 (或一群人) 來設定和控制。 另一個角色是「 *使用者*」(User)，他有一組更加受限制的權限。 除了角色之外，使用者也可以指派至群組。 群組可讓多個使用者以相同角色執行。 因此，在實務上，Windows 電腦的管理方式是將使用者指派至群組。 例如，數個使用者可以指派至電腦的使用者群組，而極少數使用者則可以指派至系統管理員群組。 在本機電腦上，系統管理員也可以建立新群組，並將其他使用者 (或甚至其他群組) 指派至該群組。  
  
 在執行 Windows 的電腦上，目錄中的每個資料夾都會受到保護。 也就是說，您可以選取資料夾並控制誰能存取檔案，以及使用者是否可以複製檔案，或 (在最高權限的情況下) 變更檔案、刪除檔案或將檔案加入至資料夾。 這也稱為存取控制，其機制稱為存取控制清單 (ACL)。 在建立 ACL 時，您可以將存取權限指派至任何一或多個群組，以及網域的個別成員。  
  
 WCF 基礎結構是設計來使用這些 Windows 安全性機制。 因此，如果要建立將會部署在內部網路上的服務，而且服務用戶端限制在 Windows 網域的成員，即可輕鬆實作安全性。 只有有效的使用者才能登入網域。 當使用者登入之後，Kerberos 控制器會讓每個使用者與其他電腦或應用程式建立安全內容。 在本機電腦上，可以輕鬆建立群組。若要保護特定資料夾，這些群組就可以用於電腦上指派存取權限。  
  
## <a name="implementing-windows-security-on-intranet-services"></a>在內部網路服務上實作 Windows 安全性  

 若要保護只在 Windows 網域上執行的應用程式，您可以使用 <xref:System.ServiceModel.WSHttpBinding> 或 <xref:System.ServiceModel.NetTcpBinding> 繫結的預設安全性設定。 依預設，相同 Windows 網域上的任何人都可以存取 WCF 服務。 因為這些使用者已經登入網路，所以他們都是受信任的。 服務和用戶端之間的訊息會為了機密性而加密，且為了完整性而簽署。 如需有關如何建立使用 Windows 安全性之服務的詳細資訊，請參閱 [如何：使用 Windows 認證保護服務](how-to-secure-a-service-with-windows-credentials.md)。  
  
### <a name="authorization-using-the-principalpermissionattribute-class"></a>使用 PrincipalPermissionAttribute 類別的授權  

 如果您必須限制存取電腦上的資源，最簡單的方式是使用 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 類別。 這個屬性可藉由要求使用者應為指定的 Windows 群組或角色或特定使用者，來限制服務作業的引動過程。 如需詳細資訊，請參閱 [如何：使用 PrincipalPermissionAttribute 類別來限制存取](how-to-restrict-access-with-the-principalpermissionattribute-class.md)。  
  
### <a name="impersonation"></a>模擬  

 模擬是另一個可用來控制存取資源的機制。 根據預設，由 IIS 裝載的服務必須在 ASPNET 帳戶的身分識別下執行。 ASPNET 帳戶只能存取它有權限的資源。 不過，也可以將資料夾的 ACL 設定為排除 ASPNET 服務帳戶，但允許某些其他身分識別來存取資料夾。 接下來的問題是，如果不允許 ASPNET 帳戶存取資料夾，如何允許其他使用者存取資料夾。 答案是使用模擬，藉此讓服務能使用用戶端的認證來存取特定資源。 另一個範例是當存取只有某些使用者有權限的 SQL Server 資料庫。 如需使用模擬的詳細資訊，請參閱 [如何：在服務上模擬用戶端](how-to-impersonate-a-client-on-a-service.md) 和 [委派和](./feature-details/delegation-and-impersonation-with-wcf.md)模擬。  
  
## <a name="security-on-the-internet"></a>網際網路上的安全性  

 網際網路上的安全性和內部網路上的安全性有相同需求。 服務必須出示其認證，以證明其真實性，而用戶端則必須向服務證明其身分識別。 一旦證明用戶端的身分識別，服務就可以控制用戶端對資源的存取權限。 不過，由於網際網路的異質性，所出示的認證與 Windows 網域上所使用的並不相同。 在網域上，Kerberos 控制器會使用認證的票證來處理使用者驗證，但在網際網路上，服務和用戶端則仰賴多個不同方式來出示認證。 不過，本主題的目標是要提供一個共同的方法，讓您能夠建立可在網際網路上存取的 WCF 服務。  
  
### <a name="using-iis-and-aspnet"></a>使用 IIS 和 ASP.NET  

 網際網路安全性的需求以及解決這些問題的機制並不陌生。 IIS 是 Microsoft 在網際網路上的 Web 服務器，而且有許多可解決這些問題的安全性功能;此外，ASP.NET 還包含 WCF 服務可以使用的安全性功能。 若要利用這些安全性功能，請在 IIS 上裝載 WCF 服務。  
  
#### <a name="using-aspnet-membership-and-role-providers"></a>使用 ASP.NET 成員資格和角色提供者  

 ASP.NET 包含成員資格和角色提供者。 提供者是用來驗證呼叫者，內含使用者名稱/密碼組的資料庫，也可讓您指定每個呼叫者的存取權限。 使用 WCF 時，您可以透過設定輕鬆地使用既有的成員資格和角色提供者。 如需示範這個用法的範例應用程式，請參閱 [Membership and Role Provider](./samples/membership-and-role-provider.md) 範例。  
  
### <a name="credentials-used-by-iis"></a>IIS 使用的認證  

 不同於 Kerberos 控制器所支援的 Windows 網域，在網際網路的環境中，沒有單一控制器來管理任何時候數以百萬計的登入使用者。 取而代之的是網際網路上最常見的 X.509 憑證 (也稱為 Secure Sockets Layer (SSL) 憑證)。 這些憑證通常是由「 *憑證授權單位*」(Certificate Authority) 發行，這是保證憑證和發給對象真實性的第三方公司。 若要在網際網路上公開服務，您也必須提供這類受信任的憑證來驗證服務。  
  
 這時產生一個問題：如何取得這類憑證？ 當您準備好部署服務及購買服務憑證時，一個來源是第三方憑證授權單位，例如 Authenticode 或 VeriSign。 但是，如果您是在具有 WCF 的開發階段，但尚未準備好要購買憑證，則有一些工具和技巧可用來建立可用於模擬生產部署的 x.509 憑證。 如需詳細資訊，請參閱 [使用憑證](./feature-details/working-with-certificates.md)。  
  
## <a name="security-modes"></a>安全性模式  

 WCF 安全性程式設計需要幾個重要的決策點。 最基本的是「 *安全性模式*」(Security Mode) 的選擇。 兩個主要安全性模式是「 *傳輸模式* 」(Transport Mode) 和「 *訊息模式*」(Message Mode)。  
  
 第三個模式是「 *使用訊息認證的傳輸模式*」(Transport With Message Credentials Mode)，此模式會結合這兩個主要模式的語意。  
  
 安全性模式決定如何保護訊息，每個選項互有利弊，說明如下。 如需設定安全性模式的詳細資訊，請參閱 [如何：設定安全性模式](how-to-set-the-security-mode.md)。  
  
#### <a name="transport-mode"></a>傳輸模式  

 在網路和應用程式之間有多個層次。 其中一個是 *傳輸* 層 *，* 可管理端點之間的訊息傳輸。 基於目前的目的，您只需要瞭解 WCF 會使用數個傳輸通訊協定，而每個通訊協定都可以保護訊息的傳輸。  (如需傳輸的詳細資訊，請參閱 [傳輸](./feature-details/transports.md)。 )   
  
 常用的通訊協定包含 HTTP 和 TCP。 每個這些通訊協定都會藉由通訊協定特定的 (一或多個) 機制來保護訊息傳輸。 例如，HTTP 通訊協定使用 SSL over HTTP (通常縮寫為 "HTTPS") 而受到保護。 因此，當您選取安全性的傳輸模式時，會依照通訊協定規定來選擇使用機制。 例如，如果您選取 <xref:System.ServiceModel.WSHttpBinding> 類別，並將其安全性模式設定為 Transport，同時會選取 SSL over HTTP (HTTPS) 做為安全性機制。 傳輸模式的優點是比訊息模式更有效率，因為安全性是整合在相當低的層級。 使用傳輸模式時，安全性機制必須依照傳輸規格來實作，因此只有在點對點傳輸時訊息才能安全流動。  
  
#### <a name="message-mode"></a>訊息模式  

 相對之下，訊息模式是藉由包含安全性資料做為每個訊息的一部分，來提供安全性。 使用 XML 和 SOAP 安全性標頭，為確保訊息完整性和機密性所需的認證和其他資料會包含在每個訊息中。 每個訊息包含安全性資料且必須個別處理，因此會影響效能  (在傳輸模式中，一旦傳輸層受到保護，所有訊息都可自由流動 ) 。不過，訊息安全性有一個優於傳輸安全性的優點：它比較有彈性。 也就是說，安全性需求不是由傳輸決定的。 您可以使用任何類型的用戶端認證來保護訊息 (在傳輸模式中，傳輸通訊協定會決定可使用的用戶端認證類型)。  
  
#### <a name="transport-with-message-credentials"></a>使用訊息認證的傳輸  

 第三個模式結合傳輸和訊息安全性兩者的優點。 在這個模式中，傳輸安全性會用來有效確保每個訊息的機密性和完整性。 同時，每個訊息包含它自己的認證資料，以便驗證訊息。 使用驗證時，也可以實作授權。 藉由驗證傳送者，可以依照傳送者的身分識別來授與 (或拒絕) 資源的存取權限。  
  
## <a name="specifying-the-client-credential-type-and-credential-value"></a>指定用戶端認證類型和認證值  

 選取安全性模式之後，您也可以指定用戶端認證類型。 用戶端認證類型會指定用戶端必須用來向伺服器驗證自身的類型。  
  
 但並不是所有狀況都需要用戶端認證類型。 使用 SSL over HTTP (HTTPS) 時，服務會向用戶端驗證自身。 在這個驗證過程中，服務的憑證會在一個名為「 *交涉*」(Negotiation) 的處理序中傳送至用戶端。 SSL 安全傳輸會確保所有訊息都是機密的。  
  
 如果建立的服務需要驗證用戶端，則用戶端認證類型的選擇取決於選取的傳輸和安全性模式。 例如，使用 HTTP 傳輸且選擇傳輸模式時，有數個選項，例如「基本」、「摘要」等  (如需這些認證類型的詳細資訊，請參閱 [瞭解 HTTP 驗證](./feature-details/understanding-http-authentication.md)。 )   
  
 如果在 Windows 網域上建立的服務只提供給該網路的其他使用者使用，最簡單的方法是 Windows 用戶端認證類型。 不過，您可能也要提供憑證給服務。 在 [How to: Specify Client Credential Values](how-to-specify-client-credential-values.md)中，會示範這個用法。  
  
#### <a name="credential-values"></a>認證值  

 「 *認證值* 」(Credential Value) 是服務使用的實際認證。 一旦指定認證類型，您可能也要使用實際認證來設定服務。 如果已選取 Windows (而且服務將在 Windows 網域上執行)，則不需要指定實際認證值。  
  
## <a name="identity"></a>身分識別  

 在 WCF 中，身分 *識別* 對於伺服器和用戶端具有不同的意義。 簡言之，當執行服務時，識別是在驗證後指派至安全性內容。 若要檢視實際識別，請檢查 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 類別的 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> 和 <xref:System.ServiceModel.ServiceSecurityContext> 屬性。 如需詳細資訊，請參閱 [如何：檢查安全性內容](how-to-examine-the-security-context.md)。  
  
 相對之下，在用戶端，識別是用來驗證服務。 在設計階段，用戶端開發人員可以將 [\<identity>](../configure-apps/file-schema/wcf/identity.md) 元素設定為從服務取得的值。 在執行階段，用戶端會比對服務的實際識別，來檢查項目的值。 如果檢查失敗，用戶端會結束通訊。 如果服務在特定使用者的識別下執行，此值可以是使用者主要名稱 (UPN)，如果服務在電腦帳戶下執行，則為服務主要名稱 (SPN)。 如需詳細資訊，請參閱 [服務身分識別和驗證](./feature-details/service-identity-and-authentication.md)。 認證也可以是憑證，或是憑證上識別憑證的欄位。  
  
## <a name="protection-levels"></a>保護等級  

 `ProtectionLevel` 屬性 (Property) 會出現在多個屬性 (Attribute) 類別 (例如 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 類別)。 保護層級是一個值，會指定支援服務的訊息 (或訊息部分) 為經過簽署、經過簽署且加密，或是已傳送但未包含簽章或加密。 如需屬性的詳細資訊，請參閱 [瞭解保護層級](understanding-protection-level.md)和程式設計範例，請參閱 [如何：設定 ProtectionLevel 屬性](how-to-set-the-protectionlevel-property.md)。 如需使用內容設計服務合約的詳細資訊 `ProtectionLevel` ，請參閱 [設計服務](designing-service-contracts.md)合約。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [服務身分識別和驗證](./feature-details/service-identity-and-authentication.md)
- [了解保護層級](understanding-protection-level.md)
- [委派和模擬](./feature-details/delegation-and-impersonation-with-wcf.md)
- [設計服務合約](designing-service-contracts.md)
- [安全性](./feature-details/security.md)
- [安全性概觀](./feature-details/security-overview.md)
- [作法：設定 ProtectionLevel 屬性](how-to-set-the-protectionlevel-property.md)
- [作法：使用 Windows 認證來確保服務安全](how-to-secure-a-service-with-windows-credentials.md)
- [作法：設定安全性模式](how-to-set-the-security-mode.md)
- [作法：指定用戶端認證類型](how-to-specify-the-client-credential-type.md)
- [作法：使用 PrincipalPermissionAttribute 類別來限制存取](how-to-restrict-access-with-the-principalpermissionattribute-class.md)
- [作法：在服務上模擬用戶端](how-to-impersonate-a-client-on-a-service.md)
- [作法：檢查資訊安全內容](how-to-examine-the-security-context.md)

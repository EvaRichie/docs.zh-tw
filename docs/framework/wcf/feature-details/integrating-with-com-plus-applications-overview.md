---
title: 整合 COM+ 應用程式概觀
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, COM+ integration
- WCF, COM+ integration
ms.assetid: e481e48f-7096-40eb-9f20-7f0098412941
ms.openlocfilehash: 1b9b7e57760c2aba0a8e9eadd53ca8e72529b787
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96248964"
---
# <a name="integrating-with-com-applications-overview"></a>整合 COM+ 應用程式概觀

Windows Communication Foundation (WCF) 可提供豐富的環境來建立分散式應用程式。 如果您已經使用裝載于 COM + 中的元件架構應用程式邏輯，則可以使用 WCF 來擴充現有的邏輯，而不必重新撰寫它。 一個常見案例就是當您要透過 Web 服務，公開現有的 COM+ 或 Enterprise Services 商務邏輯之時。  
  
 當 COM+ 元件上的介面公開為 Web 服務時，這些服務的規格和合約就會由在應用程式初始化時所執行的自動對映來決定。 下列清單會顯示這個對應的概念模型：  
  
- 對每個公開的 COM 類別定義一個服務。  
  
- 服務的合約是直接衍生自選取之元件的介面定義而得，且組態中可能已定義方法排除。  
  
- 該合約中的作業直接衍生自元件之介面定義上的方法。  
  
- 那些作業的參數則直接衍生自 COM 互通性型別，而此型別會對應至元件的方法參數。  
  
 在服務組態檔中提供服務的預設位址和傳輸繫結，不過可依需求重新設定這些項目。  
  
> [!NOTE]
> 只要 COM+ 介面和組態保持不變，已公開的 Web 服務合約就會保持不變。 對有些介面的修改並不會自動更新可用的服務，並且需要重新執行 COM+ 服務模型組態工具 (ComSvcConfig.exe)。  
  
 以 Web 服務使用時，會繼續強制執行 COM+ 應用程式與其元件的驗證和授權需求。  
  
 如果呼叫端初始化 Web 服務交易，則標示為可交易的元件就會在該交易範圍內登記。  
  
 下列為將 COM+ 元件的介面公開為 Web 服務、而不用修改元件的必要步驟：  
  
1. 判斷 COM+ 元件的介面是否可以公開為 Web 服務。  
  
2. 選取適當的裝載模式。  
  
3. 使用 COM+ 服務模型組態工具 (ComSvcConfig.exe) 以新增介面的 Web 服務。 如需如何使用 ComSvcConfig.exe 的詳細資訊，請參閱 [如何：使用 COM + 服務模型設定工具](how-to-use-the-com-service-model-configuration-tool.md)。  
  
4. 在應用程式組態檔中進行其他服務設定。 如需如何設定元件的詳細資訊，請參閱 [如何：設定 COM + 服務設定](how-to-configure-com-service-settings.md)。  
  
## <a name="supported-interfaces"></a>支援的介面  

 對於可公開為 Web 服務之介面的型別，有一些限制存在。 不支援下列介面型別：  
  
- 將物件參考做為參數進行傳遞的介面：將會在＜限制的物件參考支援＞這一節描述下列限制的物件參考方法。  
  
- 傳遞與 .NET Framework COM 互通性轉換不相容之類型的介面。  
  
- 應用程式的介面，該介面由 COM+ 裝載時，會啟用應用程式共用。  
  
- 元件的介面，這些介面已對應用程式標示為私用。  
  
- COM+ 基礎結構介面。  
  
- 來自系統應用程式的介面。  
  
- 來自 Enterprise Services 元件的介面，這些元件尚未加入至全域組件快取。  
  
### <a name="limited-object-reference-support"></a>限制的物件參考支援  

 由於一些已部署的 COM+ 元件確實會依參考參數而使用物件 (例如，傳回 ADO 資料錄集 (Recordset) 物件)，因此 COM+ 整合中就包括物件參考參數的限制支援。 支援會受限於實作 `IPersistStream` COM 介面的物件。 其中包括 ADO 資料錄集物件，並且可針對特定於應用程式的 COM 物件來實作。  
  
 為了啟用此支援，ComSvcConfig.exe 工具會提供停用一般方法簽章參數的 **allowreferences** 參數，並檢查工具是否執行，以確保不會使用物件參考參數。 此外，您以參數傳遞的物件型別必須在 <`persistableTypes`> 設定元素（<> 專案的子系）中命名和識別 `comContract` 。  
  
 使用這個功能時，COM+ 整合服務會使用 `IPersistStream` 介面來序列化或還原序列化物件執行個體。 如果物件執行個體不支援 `IPersistStream`，就會擲回例外狀況。  
  
 在用戶端應用程式中，您可以使用 <xref:System.ServiceModel.ComIntegration.PersistStreamTypeWrapper> 物件上的方法，將物件傳遞至服務並以類似方法接收物件。  
  
> [!NOTE]
> 由於序列化方法的自訂和平臺特定的本質，因此最適合用於 WCF 用戶端與 WCF 服務。  
  
## <a name="selecting-the-hosting-mode"></a>選取主控模式  

 COM+ 會以下列其中一個主控模式公開 Web 服務：  
  
- COM+ 主控  
  
     會在應用程式的專用 COM+ 伺服器處理序 (Dllhost.exe) 內主控 Web 服務。 使用這個模式時，需要先明確的啟動應用程式，它才可以接收 Web 服務要求。 可以使用 COM+ [以 NT 服務執行] 或 [當閒置時仍繼續執行] 選項，防止應用程式與其服務因閒置而導致關機。 這個模式會對伺服器應用程式提供 Web 服務和 DCOM 存取。  
  
- Web 主控  
  
     Web 服務會在 Web 伺服器工作處理序內主控。 這個模式在接收初始化要求時，不需要使用 COM+。 如果收到這個要求時應用程式不在使用中，會在處理要求之前自動啟動該應用程式。 這個模式也會對伺服器應用程式提供 Web 服務和 DCOM 存取，但會對 Web 服務要求造成處理序躍點。 通常會需要用戶端啟用模擬。 在 WCF 中，這可以透過類別的屬性來完成，該 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> <xref:System.ServiceModel.Security.WindowsClientCredential> 類別是以泛型類別的屬性來存取 <xref:System.ServiceModel.ChannelFactory%601> ，也可以是 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> 列舉值。  
  
- Web 主控同處理序  
  
     會在 Web 伺服器工作處理序內主控 Web 服務和 COM+ 應用程式邏輯。 如此可自動啟動 Web 主控模式，而不會對 Web 服務要求造成處理序躍點。 缺點則為無法透過 DCOM 存取伺服器應用程式。  
  
### <a name="security-considerations"></a>安全性考量  

 就像其他 WCF 服務一樣，公開服務的安全性設定也是透過 WCF 通道的設定來管理。 但不會強制執行傳統 DCOM 安全性設定，例如 DCOM 全機器的權限設定。 若要強制執行 COM+ 應用程式角色，則必須對元件啟用「元件層級存取檢查」授權。  
  
 使用未受保護的繫結時，通訊就會因開放而遭到竄改或導致資訊洩漏。 若要避免發生這個情況，建議您使用受到保護的繫結。  
  
 針對 COM+ 主控和 Web 主控的模式，用戶端應用程式必須讓伺服器處理序可模擬用戶端使用者。 您可以藉由將模擬等級設定為，在 WCF 用戶端中完成這項操作 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> 。  
  
 使用 Internet Information Services (IIS) 或 Windows Process Activation Service (WAS) 搭配 HTTP 傳輸時，就可以使用 Httpcfg.exe 工具來保留傳輸端點位址。 在其他組態中，保護不受充當為預期服務之惡意服務的攻擊可說是相當重要。 若要防止在目的端點上啟動惡意服務，可以將合法的服務設定為以 NT 服務來執行。 這樣可讓合法服務在任何惡意服務之前，先宣告端點位址。  
  
 使用已設定的 COM + 角色作為 Web 裝載服務來公開 COM + 應用程式時，必須將「啟動 IIS 進程帳戶」新增至其中一個應用程式的角色。 必須新增這個帳戶 (其名稱通常為 IWAM_machinename)，才能在使用之後讓物件正常關機。 這個帳戶不應該授與任何其他的權限。  
  
 在整合應用程式上無法使用 COM+ 處理序回收功能。 如果應用程式是設定為使用處理序回收，而且是在 COM+ 主控的處理序中執行元件，將無法啟動服務。 這項需求不包括使用 Web 主控同處理序模式的服務，因為這個服務中未套用處理序回收設定。  
  
## <a name="see-also"></a>另請參閱

- [整合 COM 應用程式概觀](integrating-with-com-applications-overview.md)

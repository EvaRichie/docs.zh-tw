---
title: HOW TO：稽核 Windows Communication Foundation 安全性事件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], auditing events
ms.assetid: e71e9587-3336-46a2-9a9e-d72a1743ecec
ms.openlocfilehash: 67ab5d4a4592a8b772cfdd70befe32f339062b8c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96257557"
---
# <a name="how-to-audit-windows-communication-foundation-security-events"></a>HOW TO：稽核 Windows Communication Foundation 安全性事件

Windows Communication Foundation (WCF) 可讓您將安全性事件記錄至 Windows 事件記錄檔，您可以使用 Windows 事件檢視器來查看這些事件。 這個主題會說明如何將應用程式設定為會記錄安全性事件。 如需 WCF 審核的詳細資訊，請參閱「 [審核](auditing-security-events.md)」。  
  
### <a name="to-audit-security-events-in-code"></a>若要在程式碼中稽核安全性事件  
  
1. 指定稽核記錄檔位置。 若要這樣做，請將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A> 類別的 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 屬性設定為其中一個 <xref:System.ServiceModel.AuditLogLocation> 列舉值，如下列程式碼所示。  
  
     [!code-csharp[AuditingSecurityEvents#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#2)]
     [!code-vb[AuditingSecurityEvents#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#2)]  
  
     <xref:System.ServiceModel.AuditLogLocation>列舉有三個值： `Application` 、 `Security` 或 `Default` 。 該值會指定可在事件檢視器中看見安全性記錄檔或應用程式記錄檔。 如果使用 `Default` 值，實際的記錄檔將會取決於正在執行應用程式的作業系統。 如果已啟用稽核，但未指定記錄檔位置，則支援寫入至安全性記錄檔的平台會預設使用 `Security` 記錄檔，不支援這個動作的平台則會寫入至 `Application` 記錄檔。 依預設，只有 Windows Server 2003 和 Windows Vista 支援寫入至安全性記錄檔。  
  
2. 設定要稽核的事件類型。 您可以同時稽核服務層級事件或訊息層級的授權事件。 若要這樣做，請將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A> 屬性或 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A> 屬性設定為其中一個 <xref:System.ServiceModel.AuditLevel> 列舉值，如下列程式碼所示。  
  
     [!code-csharp[AuditingSecurityEvents#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#3)]
     [!code-vb[AuditingSecurityEvents#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#3)]  
  
3. 指定是否要對與記錄稽核事件相關的應用程式隱藏或公開錯誤。 將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 屬性設定為 `true` 或 `false`，如下列程式碼所示。  
  
     [!code-csharp[AuditingSecurityEvents#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#4)]
     [!code-vb[AuditingSecurityEvents#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#4)]  
  
     預設 `SuppressAuditFailure` 屬性為 `true`，因此稽核錯誤不至於影響應用程式。 否則，會擲回例外狀況。 任何成功稽核的詳細資訊追蹤都會予以寫入， 而任何稽核失敗的追蹤則會在「錯誤」層級寫入。  
  
4. 從 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 的描述中出現的行為集合，刪除現有的 <xref:System.ServiceModel.ServiceHost>。 該行為集合是由 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 屬性存取，接下來則是從 <xref:System.ServiceModel.ServiceHostBase.Description%2A> 屬性存取。 接著將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 新增至相同的集合，如下列程式碼所示。  
  
     [!code-csharp[AuditingSecurityEvents#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#5)]
     [!code-vb[AuditingSecurityEvents#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#5)]  
  
### <a name="to-set-up-auditing-in-configuration"></a>若要使用組態設定稽核  
  
1. 若要在設定中設定審核，請將專案新增 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 至 web.config 檔案的 [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) 區段。 然後新增 [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md) 元素並設定各種屬性，如下列範例所示。  
  
    ```xml  
    <behaviors>  
       <behavior name="myAuditBehavior">  
          <serviceSecurityAudit auditLogLocation="Application"  
                suppressAuditFailure="false"
                serviceAuthorizationAuditLevel="None"
                messageAuthenticationAuditLevel="SuccessOrFailure" />  
          </behavior>  
    </behaviors>  
    ```  
  
2. 您必須指定服務的行為，如下列範例所示。  
  
    ```xml  
    <services>  
        <service type="WCS.Samples.Service.Echo"
        behaviorConfiguration=" myAuditBehavior">  
           <endpoint address=""  
                    binding="wsHttpBinding"  
                    bindingConfiguration="CertificateDefault"
                    contract="WCS.Samples.Service.IEcho" />  
        </service>  
    </services>  
    ```  
  
## <a name="example"></a>範例  

 下列程式碼會建立 <xref:System.ServiceModel.ServiceHost> 類別的執行個體，並且將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 新增至其行為集合。  
  
 [!code-csharp[AuditingSecurityEvents#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#1)]
 [!code-vb[AuditingSecurityEvents#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#1)]  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  

 如果將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 屬性設定為 `true`，就會隱藏產生安全性稽核時的失敗 (如果設定為 `false`，就會擲回例外狀況)。 但是，如果您啟用下列 [Windows **本機安全性設定** ] 屬性，產生 audit 事件的失敗將導致 Windows 立即關機：  
  
 **稽核：當無法記錄安全性稽核時，系統立即關機**  
  
 若要設定屬性，請開啟 [ **本機安全性設定** ] 對話方塊。 在 [ **安全性設定**] 底下，按一下 [ **本機原則**]。 然後按一下 [ **安全性選項**]。  
  
 如果 <xref:System.ServiceModel.AuditLogLocation> 屬性設定為 <xref:System.ServiceModel.AuditLogLocation.Security> ，且未在 **本機安全性原則** 中設定 **audit 物件存取**，則不會將 audit 事件寫入安全性記錄檔。 請注意，這時不會傳回任何失敗，但是稽核項目也不會寫入安全性記錄檔中。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A>
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
- <xref:System.ServiceModel.AuditLogLocation>
- [稽核](auditing-security-events.md)

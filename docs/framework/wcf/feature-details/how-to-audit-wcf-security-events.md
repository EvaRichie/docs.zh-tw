---
title: HOW TO：稽核 Windows Communication Foundation 安全性事件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], auditing events
ms.assetid: e71e9587-3336-46a2-9a9e-d72a1743ecec
ms.openlocfilehash: 186dd4a7fc2beae848e5cbd167a204352ee6ed4e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601292"
---
# <a name="how-to-audit-windows-communication-foundation-security-events"></a><span data-ttu-id="bef53-102">HOW TO：稽核 Windows Communication Foundation 安全性事件</span><span class="sxs-lookup"><span data-stu-id="bef53-102">How to: Audit Windows Communication Foundation Security Events</span></span>
<span data-ttu-id="bef53-103">Windows Communication Foundation （WCF）可讓您將安全性事件記錄到 Windows 事件記錄檔，您可以使用 Windows 事件檢視器來加以查看。</span><span class="sxs-lookup"><span data-stu-id="bef53-103">Windows Communication Foundation (WCF) allows you to log security events to the Windows event log, which can be viewed using the Windows Event Viewer.</span></span> <span data-ttu-id="bef53-104">這個主題會說明如何將應用程式設定為會記錄安全性事件。</span><span class="sxs-lookup"><span data-stu-id="bef53-104">This topic explains how to set up an application so that it logs security events.</span></span> <span data-ttu-id="bef53-105">如需 WCF 審核的詳細資訊，請參閱「[審核](auditing-security-events.md)」。</span><span class="sxs-lookup"><span data-stu-id="bef53-105">For more information about WCF auditing, see [Auditing](auditing-security-events.md).</span></span>  
  
### <a name="to-audit-security-events-in-code"></a><span data-ttu-id="bef53-106">若要在程式碼中稽核安全性事件</span><span class="sxs-lookup"><span data-stu-id="bef53-106">To audit security events in code</span></span>  
  
1. <span data-ttu-id="bef53-107">指定稽核記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="bef53-107">Specify the audit log location.</span></span> <span data-ttu-id="bef53-108">若要這樣做，請將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A> 類別的 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 屬性設定為其中一個 <xref:System.ServiceModel.AuditLogLocation> 列舉值，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-108">To do this, set the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A> property of the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> class to one of the <xref:System.ServiceModel.AuditLogLocation> enumeration values, as shown in the following code.</span></span>  
  
     [!code-csharp[AuditingSecurityEvents#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#2)]
     [!code-vb[AuditingSecurityEvents#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#2)]  
  
     <span data-ttu-id="bef53-109"><xref:System.ServiceModel.AuditLogLocation>列舉有三個值： `Application` 、 `Security` 或 `Default` 。</span><span class="sxs-lookup"><span data-stu-id="bef53-109">The <xref:System.ServiceModel.AuditLogLocation> enumeration has three values: `Application`, `Security`, or `Default`.</span></span> <span data-ttu-id="bef53-110">該值會指定可在事件檢視器中看見安全性記錄檔或應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bef53-110">The value specifies one of the logs visible in the Event Viewer, either the Security log or the Application log.</span></span> <span data-ttu-id="bef53-111">如果使用 `Default` 值，實際的記錄檔將會取決於正在執行應用程式的作業系統。</span><span class="sxs-lookup"><span data-stu-id="bef53-111">If you use the `Default` value, the actual log will depend on the operating system the application is running on.</span></span> <span data-ttu-id="bef53-112">如果已啟用稽核，但未指定記錄檔位置，則支援寫入至安全性記錄檔的平台會預設使用 `Security` 記錄檔，不支援這個動作的平台則會寫入至 `Application` 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bef53-112">If auditing is enabled and the log location is not specified, the default is the `Security` log for platforms that support writing to the Security log; otherwise, it will write to the `Application` log.</span></span> <span data-ttu-id="bef53-113">根據預設，只有 Windows Server 2003 和 Windows Vista 支援寫入安全性記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bef53-113">Only Windows Server 2003 and Windows Vista support writing to the Security log by default.</span></span>  
  
2. <span data-ttu-id="bef53-114">設定要稽核的事件類型。</span><span class="sxs-lookup"><span data-stu-id="bef53-114">Set up the types of events to audit.</span></span> <span data-ttu-id="bef53-115">您可以同時稽核服務層級事件或訊息層級的授權事件。</span><span class="sxs-lookup"><span data-stu-id="bef53-115">You can simultaneously audit service-level events or message-level authorization events.</span></span> <span data-ttu-id="bef53-116">若要這樣做，請將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A> 屬性或 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A> 屬性設定為其中一個 <xref:System.ServiceModel.AuditLevel> 列舉值，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-116">To do this, set the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A> property or the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A> property to one of the <xref:System.ServiceModel.AuditLevel> enumeration values, as shown in the following code.</span></span>  
  
     [!code-csharp[AuditingSecurityEvents#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#3)]
     [!code-vb[AuditingSecurityEvents#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#3)]  
  
3. <span data-ttu-id="bef53-117">指定是否要對與記錄稽核事件相關的應用程式隱藏或公開錯誤。</span><span class="sxs-lookup"><span data-stu-id="bef53-117">Specify whether to suppress or expose failures to the application regarding log audit events.</span></span> <span data-ttu-id="bef53-118">將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 屬性設定為 `true` 或 `false`，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-118">Set the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> property to either `true` or `false`, as shown in the following code.</span></span>  
  
     [!code-csharp[AuditingSecurityEvents#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#4)]
     [!code-vb[AuditingSecurityEvents#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#4)]  
  
     <span data-ttu-id="bef53-119">預設 `SuppressAuditFailure` 屬性為 `true`，因此稽核錯誤不至於影響應用程式。</span><span class="sxs-lookup"><span data-stu-id="bef53-119">The default `SuppressAuditFailure` property is `true`, so that the failure to audit does not affect the application.</span></span> <span data-ttu-id="bef53-120">否則，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="bef53-120">Otherwise, an exception is thrown.</span></span> <span data-ttu-id="bef53-121">任何成功稽核的詳細資訊追蹤都會予以寫入，</span><span class="sxs-lookup"><span data-stu-id="bef53-121">For any successful audit, a verbose trace is written.</span></span> <span data-ttu-id="bef53-122">而任何稽核失敗的追蹤則會在「錯誤」層級寫入。</span><span class="sxs-lookup"><span data-stu-id="bef53-122">For any failure to audit, the trace is written at the Error level.</span></span>  
  
4. <span data-ttu-id="bef53-123">從 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 的描述中出現的行為集合，刪除現有的 <xref:System.ServiceModel.ServiceHost>。</span><span class="sxs-lookup"><span data-stu-id="bef53-123">Delete the existing <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> from the collection of behaviors found in the description of a <xref:System.ServiceModel.ServiceHost>.</span></span> <span data-ttu-id="bef53-124">該行為集合是由 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 屬性存取，接下來則是從 <xref:System.ServiceModel.ServiceHostBase.Description%2A> 屬性存取。</span><span class="sxs-lookup"><span data-stu-id="bef53-124">The behavior collection is accessed by the <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> property, which in turn is accessed from the <xref:System.ServiceModel.ServiceHostBase.Description%2A> property.</span></span> <span data-ttu-id="bef53-125">接著將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 新增至相同的集合，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-125">Then add the new <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> to the same collection, as shown in the following code.</span></span>  
  
     [!code-csharp[AuditingSecurityEvents#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#5)]
     [!code-vb[AuditingSecurityEvents#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#5)]  
  
### <a name="to-set-up-auditing-in-configuration"></a><span data-ttu-id="bef53-126">若要使用組態設定稽核</span><span class="sxs-lookup"><span data-stu-id="bef53-126">To set up auditing in configuration</span></span>  
  
1. <span data-ttu-id="bef53-127">若要設定 configuration 中的 [審核]，請將專案新增至 web.config 檔案 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 的 [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) 區段。</span><span class="sxs-lookup"><span data-stu-id="bef53-127">To set up auditing in configuration, add a [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) element to the [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) section of the web.config file.</span></span> <span data-ttu-id="bef53-128">然後，新增 [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md) 元素並設定各種屬性，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-128">Then add a [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md) element and set the various attributes, as shown in the following example.</span></span>  
  
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
  
2. <span data-ttu-id="bef53-129">您必須指定服務的行為，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="bef53-129">You must specify the behavior for the service, as shown in the following example.</span></span>  
  
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
  
## <a name="example"></a><span data-ttu-id="bef53-130">範例</span><span class="sxs-lookup"><span data-stu-id="bef53-130">Example</span></span>  
 <span data-ttu-id="bef53-131">下列程式碼會建立 <xref:System.ServiceModel.ServiceHost> 類別的執行個體，並且將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 新增至其行為集合。</span><span class="sxs-lookup"><span data-stu-id="bef53-131">The following code creates an instance of the <xref:System.ServiceModel.ServiceHost> class and adds a new <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> to its collection of behaviors.</span></span>  
  
 [!code-csharp[AuditingSecurityEvents#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#1)]
 [!code-vb[AuditingSecurityEvents#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#1)]  
  
## <a name="net-framework-security"></a><span data-ttu-id="bef53-132">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="bef53-132">.NET Framework Security</span></span>  
 <span data-ttu-id="bef53-133">如果將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 屬性設定為 `true`，就會隱藏產生安全性稽核時的失敗 (如果設定為 `false`，就會擲回例外狀況)。</span><span class="sxs-lookup"><span data-stu-id="bef53-133">Setting the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> property to `true`, suppresses any failure to generate security audits (if set to `false`, an exception is thrown).</span></span> <span data-ttu-id="bef53-134">不過，如果您啟用下列 Windows**本機安全性設定**屬性，則無法產生 audit 事件會導致 Windows 立即關閉：</span><span class="sxs-lookup"><span data-stu-id="bef53-134">However, if you enable the following Windows **Local Security Setting** property, a failure to generate audit events will cause Windows to shut down immediately:</span></span>  
  
 <span data-ttu-id="bef53-135">**稽核：當無法記錄安全性稽核時，系統立即關機**</span><span class="sxs-lookup"><span data-stu-id="bef53-135">**Audit: Shut down system immediately if unable to log security audits**</span></span>  
  
 <span data-ttu-id="bef53-136">若要設定屬性，請開啟 [**本機安全性設定**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bef53-136">To set the property, open the **Local Security Settings** dialog box.</span></span> <span data-ttu-id="bef53-137">在 [**安全性設定**] 底下，按一下 [**本機原則**]。</span><span class="sxs-lookup"><span data-stu-id="bef53-137">Under **Security Settings**, click **Local Policies**.</span></span> <span data-ttu-id="bef53-138">然後按一下 [**安全性選項**]。</span><span class="sxs-lookup"><span data-stu-id="bef53-138">Then click **Security Options**.</span></span>  
  
 <span data-ttu-id="bef53-139">如果 <xref:System.ServiceModel.AuditLogLocation> 屬性設定為 <xref:System.ServiceModel.AuditLogLocation.Security> ，而且**本機安全性原則**中未設定**audit 物件存取**，則 Audit 事件將不會寫入安全性記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="bef53-139">If the <xref:System.ServiceModel.AuditLogLocation> property is set to <xref:System.ServiceModel.AuditLogLocation.Security> and **Audit Object Access** is not set in the **Local Security Policy**, audit events will not be written to the Security log.</span></span> <span data-ttu-id="bef53-140">請注意，這時不會傳回任何失敗，但是稽核項目也不會寫入安全性記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="bef53-140">Note that no failure is returned, but audit entries are not written to the Security log.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bef53-141">請參閱</span><span class="sxs-lookup"><span data-stu-id="bef53-141">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A>
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
- <xref:System.ServiceModel.AuditLogLocation>
- [<span data-ttu-id="bef53-142">稽核</span><span class="sxs-lookup"><span data-stu-id="bef53-142">Auditing</span></span>](auditing-security-events.md)

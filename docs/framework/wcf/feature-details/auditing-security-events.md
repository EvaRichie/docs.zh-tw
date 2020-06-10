---
title: 稽核安全性事件
ms.date: 03/30/2017
helpviewer_keywords:
- auditing security events [WCF]
ms.assetid: 5633f61c-a3c9-40dd-8070-1c373b66a716
ms.openlocfilehash: b130ed57ba086535122c8c8795c42863348870d0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597653"
---
# <a name="auditing-security-events"></a><span data-ttu-id="87642-102">稽核安全性事件</span><span class="sxs-lookup"><span data-stu-id="87642-102">Auditing Security Events</span></span>
<span data-ttu-id="87642-103">使用 Windows Communication Foundation （WCF）建立的應用程式可以使用「審核功能」來記錄安全性事件（不論是成功、失敗或兩者）。</span><span class="sxs-lookup"><span data-stu-id="87642-103">Applications created with Windows Communication Foundation (WCF) can log security events (either success, failure, or both) with the auditing feature.</span></span> <span data-ttu-id="87642-104">事件會寫入至 Windows 系統事件記錄檔，並且可以使用 [事件檢視器] 加以檢查。</span><span class="sxs-lookup"><span data-stu-id="87642-104">The events are written to the Windows system event log and can be examined using the Event Viewer.</span></span>  
  
 <span data-ttu-id="87642-105">稽核為系統管理員提供了一種方法，可偵測已發生或正在進行的攻擊。</span><span class="sxs-lookup"><span data-stu-id="87642-105">Auditing provides a way for an administrator to detect an attack that has already occurred or is in progress.</span></span> <span data-ttu-id="87642-106">此外，稽核可以協助開發人員偵錯安全性相關的問題。</span><span class="sxs-lookup"><span data-stu-id="87642-106">In addition, auditing can help a developer to debug security-related problems.</span></span> <span data-ttu-id="87642-107">例如，若授權的組態中出現錯誤，或是在檢查原則時不小心拒絕了某個授權使用者的存取，則開發人員可以藉由檢查事件日誌，快速地探索及隔離導致這個錯誤的原因。</span><span class="sxs-lookup"><span data-stu-id="87642-107">For example, if an error in the configuration of the authorization or checking policy accidentally denies access to an authorized user, a developer can quickly discover and isolate the cause of this error by examining the event log.</span></span>  
  
 <span data-ttu-id="87642-108">如需 WCF 安全性的詳細資訊，請參閱[安全性總覽](security-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="87642-108">For more information about WCF security, see [Security Overview](security-overview.md).</span></span> <span data-ttu-id="87642-109">如需 WCF 程式設計的詳細資訊，請參閱[基本 wcf 程式設計](../basic-wcf-programming.md)。</span><span class="sxs-lookup"><span data-stu-id="87642-109">For more information about programming WCF, see [Basic WCF Programming](../basic-wcf-programming.md).</span></span>  
  
## <a name="audit-level-and-behavior"></a><span data-ttu-id="87642-110">稽核層級和行為</span><span class="sxs-lookup"><span data-stu-id="87642-110">Audit Level and Behavior</span></span>  
 <span data-ttu-id="87642-111">安全性稽核目前有兩種層級：</span><span class="sxs-lookup"><span data-stu-id="87642-111">Two levels of security audits exist:</span></span>  
  
- <span data-ttu-id="87642-112">服務授權層級，其中呼叫者已獲得授權。</span><span class="sxs-lookup"><span data-stu-id="87642-112">Service authorization level, in which a caller is authorized.</span></span>  
  
- <span data-ttu-id="87642-113">訊息層級，WCF 會在其中檢查訊息有效性，並驗證呼叫端。</span><span class="sxs-lookup"><span data-stu-id="87642-113">Message level, in which WCF checks for message validity and authenticates the caller.</span></span>  
  
 <span data-ttu-id="87642-114">您可以檢查成功或失敗的兩個審核層級，也就是所謂的「 *audit 行為*」。</span><span class="sxs-lookup"><span data-stu-id="87642-114">You can check both audit levels for success or failure, which is known as the *audit behavior*.</span></span>  
  
## <a name="audit-log-location"></a><span data-ttu-id="87642-115">稽核記錄檔的位置</span><span class="sxs-lookup"><span data-stu-id="87642-115">Audit Log Location</span></span>  
 <span data-ttu-id="87642-116">決定稽核層級和行為後，您 (或系統管理員) 就可以指定稽核記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="87642-116">Once you determine an audit level and behavior, you (or an administrator) can specify a location for the audit log.</span></span> <span data-ttu-id="87642-117">您有三種選擇，包括：預設、應用程式和安全性。</span><span class="sxs-lookup"><span data-stu-id="87642-117">The three choices include: Default, Application, and Security.</span></span> <span data-ttu-id="87642-118">指定為 [預設] 時，實際的記錄檔取決於您所使用的系統，以及該系統是否支援寫入至安全性記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87642-118">When you specify Default, the actual log depends on which system you are using and whether the system supports writing to the security log.</span></span> <span data-ttu-id="87642-119">如需詳細資訊，請參閱本主題稍後的「作業系統」一節。</span><span class="sxs-lookup"><span data-stu-id="87642-119">For more information, see the "Operating System" section later in this topic.</span></span>  
  
 <span data-ttu-id="87642-120">若要寫入安全性記錄檔，您必須具備 `SeAuditPrivilege`。</span><span class="sxs-lookup"><span data-stu-id="87642-120">To write to the Security log requires the `SeAuditPrivilege`.</span></span> <span data-ttu-id="87642-121">根據預設，只有本機系統帳戶和網路服務帳戶具有此權限。</span><span class="sxs-lookup"><span data-stu-id="87642-121">By default, only Local System and Network Service accounts have this privilege.</span></span> <span data-ttu-id="87642-122">若要管理安全性記錄函式 `read` 和 `delete`，您必須具備 `SeSecurityPrivilege`。</span><span class="sxs-lookup"><span data-stu-id="87642-122">To manage the Security log functions `read` and `delete` requires the `SeSecurityPrivilege`.</span></span> <span data-ttu-id="87642-123">根據預設，只有系統管理員具有此權限。</span><span class="sxs-lookup"><span data-stu-id="87642-123">By default, only administrators have this privilege.</span></span>  
  
 <span data-ttu-id="87642-124">相反地，通過驗證的使用者可以讀取及寫入應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87642-124">In contrast, authenticated users can read and write to the Application log.</span></span> <span data-ttu-id="87642-125">根據預設，Windows XP 會將 audit 事件寫入應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87642-125">Windows XP writes audit events to the Application log by default.</span></span> <span data-ttu-id="87642-126">記錄檔也可以包含個人資訊，所有通過驗證的使用者都可以檢視這些資訊。</span><span class="sxs-lookup"><span data-stu-id="87642-126">The log can also contain personal information that is visible to all authenticated users.</span></span>  
  
## <a name="suppressing-audit-failures"></a><span data-ttu-id="87642-127">隱藏稽核失敗</span><span class="sxs-lookup"><span data-stu-id="87642-127">Suppressing Audit Failures</span></span>  
 <span data-ttu-id="87642-128">稽核期間可以使用的另一個選項為是否要隱藏任何稽核失敗。</span><span class="sxs-lookup"><span data-stu-id="87642-128">Another option during auditing is whether to suppress any audit failure.</span></span> <span data-ttu-id="87642-129">根據預設，稽核失敗不會影響到應用程式。</span><span class="sxs-lookup"><span data-stu-id="87642-129">By default, an audit failure does not affect an application.</span></span> <span data-ttu-id="87642-130">不過，如果需要的話，您可以將選項設定為 `false`，如此便會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="87642-130">If required, however, you can set the option to `false`, which causes an exception to be thrown.</span></span>  
  
## <a name="programming-auditing"></a><span data-ttu-id="87642-131">程式設計稽核</span><span class="sxs-lookup"><span data-stu-id="87642-131">Programming Auditing</span></span>  
 <span data-ttu-id="87642-132">您可以使用程式設計的方式或透過組態的方式指定稽核行為。</span><span class="sxs-lookup"><span data-stu-id="87642-132">You can specify auditing behavior either programmatically or through configuration.</span></span>  
  
### <a name="auditing-classes"></a><span data-ttu-id="87642-133">稽核類別</span><span class="sxs-lookup"><span data-stu-id="87642-133">Auditing Classes</span></span>  
 <span data-ttu-id="87642-134">下表描述用來程式設計稽核行為的類別和屬性。</span><span class="sxs-lookup"><span data-stu-id="87642-134">The following table describes the classes and properties used to program auditing behavior.</span></span>  
  
|<span data-ttu-id="87642-135">類別</span><span class="sxs-lookup"><span data-stu-id="87642-135">Class</span></span>|<span data-ttu-id="87642-136">描述</span><span class="sxs-lookup"><span data-stu-id="87642-136">Description</span></span>|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>|<span data-ttu-id="87642-137">將稽核的設定選項啟用為服務行為。</span><span class="sxs-lookup"><span data-stu-id="87642-137">Enables setting options for auditing as a service behavior.</span></span>|  
|<xref:System.ServiceModel.AuditLogLocation>|<span data-ttu-id="87642-138">用於指定寫入哪個記錄檔的列舉。</span><span class="sxs-lookup"><span data-stu-id="87642-138">Enumeration to specify which log to write to.</span></span> <span data-ttu-id="87642-139">可能的值為 [預設]、[應用程式] 和 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="87642-139">The possible values are Default, Application, and Security.</span></span> <span data-ttu-id="87642-140">當您選取 [預設] 時，作業系統會判斷實際的記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="87642-140">When you select Default, the operating system determines the actual log location.</span></span> <span data-ttu-id="87642-141">如需詳細資訊，請參閱本主題稍後「應用程式或安全性事件記錄檔選擇」一節的說明。</span><span class="sxs-lookup"><span data-stu-id="87642-141">See the "Application or Security Event Log Choice" section later in this topic.</span></span>|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A>|<span data-ttu-id="87642-142">指定要在訊息層級上稽核哪種訊息驗證事件的類型。</span><span class="sxs-lookup"><span data-stu-id="87642-142">Specifies which types of message authentication events are audited at the message level.</span></span> <span data-ttu-id="87642-143">這些選擇有 `None`、`Failure`、`Success` 和 `SuccessOrFailure`。</span><span class="sxs-lookup"><span data-stu-id="87642-143">The choices are `None`, `Failure`, `Success`, and `SuccessOrFailure`.</span></span>|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A>|<span data-ttu-id="87642-144">指定要在服務層級上稽核哪種服務授權事件的類型。</span><span class="sxs-lookup"><span data-stu-id="87642-144">Specifies which types of service authorization events are audited at the service level.</span></span> <span data-ttu-id="87642-145">這些選擇有 `None`、`Failure`、`Success` 和 `SuccessOrFailure`。</span><span class="sxs-lookup"><span data-stu-id="87642-145">The choices are `None`, `Failure`, `Success`, and `SuccessOrFailure`.</span></span>|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A>|<span data-ttu-id="87642-146">指定當稽核失敗時，用戶端要求會產生什麼變化。</span><span class="sxs-lookup"><span data-stu-id="87642-146">Specifies what happens to the client request when auditing fails.</span></span> <span data-ttu-id="87642-147">例如，當服務嘗試寫入安全性記錄檔，但不具有 `SeAuditPrivilege` 時。</span><span class="sxs-lookup"><span data-stu-id="87642-147">For example, when the service attempts to write to the security log, but does not have `SeAuditPrivilege`.</span></span> <span data-ttu-id="87642-148">`true` 的預設值表示忽略該失敗，並且正常處理用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="87642-148">The default value of `true` indicates that failures are ignored, and the client request is processed normally.</span></span>|  
  
 <span data-ttu-id="87642-149">如需設定應用程式以記錄 audit 事件的範例，請參閱[如何： Audit Security events](how-to-audit-wcf-security-events.md)。</span><span class="sxs-lookup"><span data-stu-id="87642-149">For an example of setting up an application to log audit events, see [How to: Audit Security Events](how-to-audit-wcf-security-events.md).</span></span>  
  
### <a name="configuration"></a><span data-ttu-id="87642-150">組態</span><span class="sxs-lookup"><span data-stu-id="87642-150">Configuration</span></span>  
 <span data-ttu-id="87642-151">您也可以在底下新增，以使用設定來指定審核行為 [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md) [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) 。</span><span class="sxs-lookup"><span data-stu-id="87642-151">You can also use configuration to specify auditing behavior by adding a [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md) under the [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md).</span></span> <span data-ttu-id="87642-152">您必須在底下加入元素， [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="87642-152">You must add the element under a [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) as shown in the following code.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <behavior>  
        <!-- auditLogLocation="Application" or "Security" -->  
        <serviceSecurityAudit  
                  auditLogLocation="Application"  
                  suppressAuditFailure="true"  
                  serviceAuthorizationAuditLevel="Failure"  
                  messageAuthenticationAuditLevel="SuccessOrFailure" />
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="87642-153">如果已啟用稽核，但未指定 `auditLogLocation`，則支援寫入至安全性記錄檔的平台會使用的預設記錄名稱為「安全性」記錄檔，否則便是「應用程式」記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87642-153">If auditing is enabled and an `auditLogLocation` is not specified, the default log name is "Security" log for the platform supporting writing to the Security log; otherwise, it is "Application" log.</span></span> <span data-ttu-id="87642-154">只有 Windows Server 2003 和 Windows Vista 作業系統支援寫入安全性記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87642-154">Only the Windows Server 2003 and Windows Vista operating systems support writing to the Security log.</span></span> <span data-ttu-id="87642-155">如需詳細資訊，請參閱本主題稍後的「作業系統」一節。</span><span class="sxs-lookup"><span data-stu-id="87642-155">For more information, see the "Operating System" section later in this topic.</span></span>  
  
## <a name="security-considerations"></a><span data-ttu-id="87642-156">安全性考量</span><span class="sxs-lookup"><span data-stu-id="87642-156">Security Considerations</span></span>  
 <span data-ttu-id="87642-157">如果惡意使用者得知已啟用稽核，攻擊者就可以傳送無效的訊息，而造成寫入稽核項目。</span><span class="sxs-lookup"><span data-stu-id="87642-157">If a malicious user knows that auditing is enabled, that attacker can send invalid messages that cause audit entries to be written.</span></span> <span data-ttu-id="87642-158">如果是因為這個方法而填滿稽核記錄檔，稽核系統就會失敗。</span><span class="sxs-lookup"><span data-stu-id="87642-158">If the audit log is filled in this manner, the auditing system fails.</span></span> <span data-ttu-id="87642-159">若要減輕這個威脅，請將 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 屬性設定為 `true`，並使用 [事件檢視器] 的屬性來控制稽核行為。</span><span class="sxs-lookup"><span data-stu-id="87642-159">To mitigate this, set the <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> property to `true` and use the properties of the Event Viewer to control the auditing behavior.</span></span>  
  
 <span data-ttu-id="87642-160">所有已驗證的使用者都可以看到寫入 Windows XP 應用程式記錄檔的 Audit 事件。</span><span class="sxs-lookup"><span data-stu-id="87642-160">Audit events that are written to the Application Log on Windows XP are visible to any authenticated user.</span></span>  
  
## <a name="choosing-between-application-and-security-event-logs"></a><span data-ttu-id="87642-161">在應用程式和安全性事件記錄檔之間選擇</span><span class="sxs-lookup"><span data-stu-id="87642-161">Choosing Between Application and Security Event Logs</span></span>  
 <span data-ttu-id="87642-162">下表提供可協助您選擇要記錄至應用程式或安全性事件記錄檔的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="87642-162">The following tables provide information to help you choose whether to log into the Application or the Security event log.</span></span>  
  
#### <a name="operating-system"></a><span data-ttu-id="87642-163">作業系統</span><span class="sxs-lookup"><span data-stu-id="87642-163">Operating System</span></span>  
  
|<span data-ttu-id="87642-164">系統</span><span class="sxs-lookup"><span data-stu-id="87642-164">System</span></span>|<span data-ttu-id="87642-165">應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="87642-165">Application log</span></span>|<span data-ttu-id="87642-166">安全性記錄檔</span><span class="sxs-lookup"><span data-stu-id="87642-166">Security log</span></span>|  
|------------|---------------------|------------------|  
|<span data-ttu-id="87642-167">Windows XP SP2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="87642-167">Windows XP SP2 or later</span></span>|<span data-ttu-id="87642-168">支援</span><span class="sxs-lookup"><span data-stu-id="87642-168">Supported</span></span>|<span data-ttu-id="87642-169">不支援</span><span class="sxs-lookup"><span data-stu-id="87642-169">Not supported</span></span>|  
|<span data-ttu-id="87642-170">Windows Server 2003 SP1 和 Windows Vista</span><span class="sxs-lookup"><span data-stu-id="87642-170">Windows Server 2003 SP1 and Windows Vista</span></span>|<span data-ttu-id="87642-171">支援</span><span class="sxs-lookup"><span data-stu-id="87642-171">Supported</span></span>|<span data-ttu-id="87642-172">執行緒內容必須擁有 `SeAuditPrivilege`</span><span class="sxs-lookup"><span data-stu-id="87642-172">Thread context must possess `SeAuditPrivilege`</span></span>|  
  
#### <a name="other-factors"></a><span data-ttu-id="87642-173">其他因素</span><span class="sxs-lookup"><span data-stu-id="87642-173">Other Factors</span></span>  
 <span data-ttu-id="87642-174">除了作業系統之外，下表描述其他控制記錄啟用的設定。</span><span class="sxs-lookup"><span data-stu-id="87642-174">In addition to the operating system, the following table describes other settings that control the enablement of logging.</span></span>  
  
|<span data-ttu-id="87642-175">因數</span><span class="sxs-lookup"><span data-stu-id="87642-175">Factor</span></span>|<span data-ttu-id="87642-176">應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="87642-176">Application log</span></span>|<span data-ttu-id="87642-177">安全性記錄檔</span><span class="sxs-lookup"><span data-stu-id="87642-177">Security log</span></span>|  
|------------|---------------------|------------------|  
|<span data-ttu-id="87642-178">稽核原則管理</span><span class="sxs-lookup"><span data-stu-id="87642-178">Audit policy management</span></span>|<span data-ttu-id="87642-179">不適用。</span><span class="sxs-lookup"><span data-stu-id="87642-179">Not applicable.</span></span>|<span data-ttu-id="87642-180">安全性記錄檔也可以藉由本機安全性授權 (LSA) 原則與組態來加以控制。</span><span class="sxs-lookup"><span data-stu-id="87642-180">Along with configuration, the Security log is also controlled by the local security authority (LSA) policy.</span></span> <span data-ttu-id="87642-181">您也必須啟用 [稽核物件存取] 類別。</span><span class="sxs-lookup"><span data-stu-id="87642-181">The "Audit object access" category must also be enabled.</span></span>|  
|<span data-ttu-id="87642-182">預設的使用者經驗</span><span class="sxs-lookup"><span data-stu-id="87642-182">Default user experience</span></span>|<span data-ttu-id="87642-183">所有通過驗證的使用者都可以寫入應用程式記錄檔，因此不需要為應用程式處理序額外執行設定權限的步驟。</span><span class="sxs-lookup"><span data-stu-id="87642-183">All authenticated users can write to the Application log, so no additional permission step is needed for application processes.</span></span>|<span data-ttu-id="87642-184">應用程式處理序 (內容) 必須具有 `SeAuditPrivilege`。</span><span class="sxs-lookup"><span data-stu-id="87642-184">The application process (context) must have `SeAuditPrivilege`.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="87642-185">請參閱</span><span class="sxs-lookup"><span data-stu-id="87642-185">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
- <xref:System.ServiceModel.AuditLogLocation>
- [<span data-ttu-id="87642-186">安全性總覽</span><span class="sxs-lookup"><span data-stu-id="87642-186">Security Overview</span></span>](security-overview.md)
- [<span data-ttu-id="87642-187">基本 WCF 程式設計</span><span class="sxs-lookup"><span data-stu-id="87642-187">Basic WCF Programming</span></span>](../basic-wcf-programming.md)
- [<span data-ttu-id="87642-188">HOW TO：稽核安全性事件</span><span class="sxs-lookup"><span data-stu-id="87642-188">How to: Audit Security Events</span></span>](how-to-audit-wcf-security-events.md)
- [\<serviceSecurityAudit>](../../configure-apps/file-schema/wcf/servicesecurityaudit.md)
- [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md)
- <span data-ttu-id="87642-189">[Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="87642-189">[Security Model for Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span></span>

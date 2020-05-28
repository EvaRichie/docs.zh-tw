---
title: 異動通訊協定 1.0 版
ms.date: 03/30/2017
ms.assetid: 034679af-0002-402e-98a8-ef73dcd71bb6
ms.openlocfilehash: 6063c643be4c60e9830a020d10ac9fbcd236dac2
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144769"
---
# <a name="transaction-protocols-version-10"></a><span data-ttu-id="b309c-102">異動通訊協定 1.0 版</span><span class="sxs-lookup"><span data-stu-id="b309c-102">Transaction Protocols version 1.0</span></span>
<span data-ttu-id="b309c-103">Windows Communication Foundation （WCF）第1版會執行 WS-不可部分完成交易和 WS 協調通訊協定的1.0 版。</span><span class="sxs-lookup"><span data-stu-id="b309c-103">Windows Communication Foundation (WCF) version 1 implements version 1.0 of the WS-Atomic Transaction and WS-Coordination protocols.</span></span> <span data-ttu-id="b309c-104">如需1.1 版的詳細資訊，請參閱[交易通訊協定](../../../../docs/framework/wcf/feature-details/transaction-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="b309c-104">For more information about version 1.1, see [Transaction Protocols](../../../../docs/framework/wcf/feature-details/transaction-protocols.md).</span></span>  
  
|<span data-ttu-id="b309c-105">規格/文件</span><span class="sxs-lookup"><span data-stu-id="b309c-105">Specification/Document</span></span>|<span data-ttu-id="b309c-106">連結</span><span class="sxs-lookup"><span data-stu-id="b309c-106">Link</span></span>|  
|-----------------------------|----------|  
|<span data-ttu-id="b309c-107">WS-Coordination</span><span class="sxs-lookup"><span data-stu-id="b309c-107">WS-Coordination</span></span>|<https://specs.xmlsoap.org/ws/2004/10/wscoor/wscoor.pdf>|  
|<span data-ttu-id="b309c-108">WS-AtomicTransaction</span><span class="sxs-lookup"><span data-stu-id="b309c-108">WS-AtomicTransaction</span></span>|<https://specs.xmlsoap.org/ws/2004/10/wsat/wsat.pdf>|  
  
 <span data-ttu-id="b309c-109">這些通訊協定規格的互通性需要滿足兩個層級：在應用程式之間，以及在異動管理員之間的層級 (請參閱下圖)。</span><span class="sxs-lookup"><span data-stu-id="b309c-109">Interoperability on these protocol specifications is required at two levels: between applications and between transaction managers (see the following figure).</span></span> <span data-ttu-id="b309c-110">規格詳細描述兩種互通性層級的訊息格式和訊息交換。</span><span class="sxs-lookup"><span data-stu-id="b309c-110">Specifications describe in great detail the message formats and message exchange for both interoperability levels.</span></span> <span data-ttu-id="b309c-111">對應用程式之間的交換也會如同針對標準應用程式交換一樣，套用特定安全性、可靠性和編碼。</span><span class="sxs-lookup"><span data-stu-id="b309c-111">Certain security, reliability, and encodings for application-to-application exchange apply as they do for regular application exchange.</span></span> <span data-ttu-id="b309c-112">但是，交易管理員之間若要成功地達成互通性，便需要有一致的特定繫結，因為使用者通常不會設定它。</span><span class="sxs-lookup"><span data-stu-id="b309c-112">However, successful interoperability between transaction managers requires agreement on the particular binding, because it is usually not configured by the user.</span></span>  
  
 <span data-ttu-id="b309c-113">此主題描述 WS-Atomic 異動 (WS-AT) 安全性規格的組成，並且描述使用在異動管理員之間通訊的安全繫結程序。</span><span class="sxs-lookup"><span data-stu-id="b309c-113">This topic describes a composition of the WS-Atomic Transaction (WS-AT) specification with security and describes the secure binding used for communication between transaction managers.</span></span> <span data-ttu-id="b309c-114">本文件中描述的方法已經使用 WS-AT 和 WS-Coordination 的其他實作成功通過測試，其中包含 IBM、IONA、Sun Microsystems 和其他實作。</span><span class="sxs-lookup"><span data-stu-id="b309c-114">The approach described in this document has been successfully tested with other implementations of WS-AT and WS-Coordination including IBM, IONA, Sun Microsystems, and others.</span></span>  
  
 <span data-ttu-id="b309c-115">下圖說明兩個交易管理員、交易管理員1和交易管理員2之間的互通性，以及應用程式1和應用程式2這兩個應用程式：</span><span class="sxs-lookup"><span data-stu-id="b309c-115">The following figure depicts the interoperability between two transaction managers, Transaction Manager 1 and Transaction Manager 2, and two applications, Application 1 and Application 2:</span></span>  
  
 ![顯示交易管理員之間互動的螢幕擷取畫面。](./media/transaction-protocols/transaction-managers-flow.gif)  
  
 <span data-ttu-id="b309c-117">使用一個啟動器 (I) 和一個參與者 (P) 考量一般的 WS-Coordination/WS-Atomic Transaction 案例。</span><span class="sxs-lookup"><span data-stu-id="b309c-117">Consider a typical WS-Coordination/WS-Atomic Transaction scenario with one Initiator (I) and one Participant (P).</span></span> <span data-ttu-id="b309c-118">啟動器和參與者都有異動管理員 (分別是 ITM 和 PTM)。</span><span class="sxs-lookup"><span data-stu-id="b309c-118">Both Initiator and Participant have Transaction Managers, (ITM and PTM, respectively).</span></span> <span data-ttu-id="b309c-119">在此主題中，兩階段交易認可會稱為 2PC。</span><span class="sxs-lookup"><span data-stu-id="b309c-119">Two-phase commit is referred to as 2PC in this topic.</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="b309c-120">1. CreateCoordinationCoNtext</span><span class="sxs-lookup"><span data-stu-id="b309c-120">1. CreateCoordinationContext</span></span>|<span data-ttu-id="b309c-121">12. 應用程式訊息回應</span><span class="sxs-lookup"><span data-stu-id="b309c-121">12. Application Message Response</span></span>|  
|<span data-ttu-id="b309c-122">2. CreateCoordinationCoNtextResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-122">2. CreateCoordinationContextResponse</span></span>|<span data-ttu-id="b309c-123">13. Commit （完成）</span><span class="sxs-lookup"><span data-stu-id="b309c-123">13. Commit (Completion)</span></span>|  
|<span data-ttu-id="b309c-124">3. 註冊（完成）</span><span class="sxs-lookup"><span data-stu-id="b309c-124">3. Register (Completion)</span></span>|<span data-ttu-id="b309c-125">14. 準備（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-125">14. Prepare (2PC)</span></span>|  
|<span data-ttu-id="b309c-126">4. RegisterResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-126">4. RegisterResponse</span></span>|<span data-ttu-id="b309c-127">15. 準備（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-127">15. Prepare (2PC)</span></span>|  
|<span data-ttu-id="b309c-128">5. 應用程式訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-128">5. Application Message</span></span>|<span data-ttu-id="b309c-129">16. 備妥（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-129">16. Prepared (2PC)</span></span>|  
|<span data-ttu-id="b309c-130">6. CreateCoordinationCoNtext 與內容</span><span class="sxs-lookup"><span data-stu-id="b309c-130">6. CreateCoordinationContext with Context</span></span>|<span data-ttu-id="b309c-131">17. 準備（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-131">17. Prepared (2PC)</span></span>|  
|<span data-ttu-id="b309c-132">7. Register （耐用）</span><span class="sxs-lookup"><span data-stu-id="b309c-132">7. Register (Durable)</span></span>|<span data-ttu-id="b309c-133">18. 已認可（完成）</span><span class="sxs-lookup"><span data-stu-id="b309c-133">18. Committed (Completion)</span></span>|  
|<span data-ttu-id="b309c-134">8. RegisterResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-134">8. RegisterResponse</span></span>|<span data-ttu-id="b309c-135">19. 認可（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-135">19. Commit (2PC)</span></span>|  
|<span data-ttu-id="b309c-136">9. CreateCoordinationCoNtextResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-136">9. CreateCoordinationContextResponse</span></span>|<span data-ttu-id="b309c-137">20. 認可（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-137">20. Commit (2PC)</span></span>|  
|<span data-ttu-id="b309c-138">10. Register （耐用）</span><span class="sxs-lookup"><span data-stu-id="b309c-138">10. Register (Durable)</span></span>|<span data-ttu-id="b309c-139">21. 已認可（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-139">21. Committed (2PC)</span></span>|  
|<span data-ttu-id="b309c-140">11. RegisterResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-140">11. RegisterResponse</span></span>|<span data-ttu-id="b309c-141">22. 已認可（2PC）</span><span class="sxs-lookup"><span data-stu-id="b309c-141">22. Committed (2PC)</span></span>|  
  
 <span data-ttu-id="b309c-142">此文件描述 WS-AtomicTransaction 安全性規格的組成，並且描述使用在異動管理員之間通訊的安全繫結程序。</span><span class="sxs-lookup"><span data-stu-id="b309c-142">This document describes a composition of the WS-AtomicTransaction specification with security and describes the secure binding used for communication between transaction managers.</span></span> <span data-ttu-id="b309c-143">本文件中描述的方法已經使用 WS-AT 和 WS-Coordination 的其他實作成功通過測試。</span><span class="sxs-lookup"><span data-stu-id="b309c-143">The approach described in this document has been successfully tested with other implementations of WS-AT and WS-Coordination.</span></span>  
  
 <span data-ttu-id="b309c-144">圖形與表格會從安全性觀點顯示四種訊息類別：</span><span class="sxs-lookup"><span data-stu-id="b309c-144">The figure and table illustrate four classes of messages from the viewpoint of security:</span></span>  
  
- <span data-ttu-id="b309c-145">啟動訊息 (CreateCoordinationContext 和 CreateCoordinationContextResponse)。</span><span class="sxs-lookup"><span data-stu-id="b309c-145">Activation messages (CreateCoordinationContext and CreateCoordinationContextResponse).</span></span>  
  
- <span data-ttu-id="b309c-146">登錄訊息 (Register 和 RegisterResponse)</span><span class="sxs-lookup"><span data-stu-id="b309c-146">Registration messages (Register and RegisterResponse)</span></span>  
  
- <span data-ttu-id="b309c-147">通訊協定訊息 (準備、復原、認可和中止等等)。</span><span class="sxs-lookup"><span data-stu-id="b309c-147">Protocol messages (Prepare, Rollback, Commit, Aborted, and so on).</span></span>  
  
- <span data-ttu-id="b309c-148">應用程式訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-148">Application messages.</span></span>  
  
 <span data-ttu-id="b309c-149">前三個訊息類別會視為異動管理員訊息，並且在此主題稍後的「應用程式訊息交換」中會描述其繫結程序組態。</span><span class="sxs-lookup"><span data-stu-id="b309c-149">The first three message classes are considered Transaction Manager messages and their binding configuration is described in the "Application Message Exchange" later in this topic.</span></span> <span data-ttu-id="b309c-150">第四個訊息類別是應用程式對應用程式訊息，並且在此主題稍後的「訊息範例」一節中會描述。</span><span class="sxs-lookup"><span data-stu-id="b309c-150">The fourth class of message is application to application messages and is described in the "Message Examples" section later in this topic.</span></span> <span data-ttu-id="b309c-151">本節說明 WCF 每個類別所使用的通訊協定系結。</span><span class="sxs-lookup"><span data-stu-id="b309c-151">This section describes the protocol bindings used for each of these classes by WCF.</span></span>  
  
 <span data-ttu-id="b309c-152">下列 XML 命名空間與關聯的前置詞會使用在整份文件中。</span><span class="sxs-lookup"><span data-stu-id="b309c-152">The following XML Namespaces and associated prefixes are used throughout this document.</span></span>  
  
|<span data-ttu-id="b309c-153">前置詞</span><span class="sxs-lookup"><span data-stu-id="b309c-153">Prefix</span></span>|<span data-ttu-id="b309c-154">命名空間 URI</span><span class="sxs-lookup"><span data-stu-id="b309c-154">Namespace URI</span></span>|  
|------------|-------------------|  
|<span data-ttu-id="b309c-155">s11</span><span class="sxs-lookup"><span data-stu-id="b309c-155">s11</span></span>|`http://schemas.xmlsoap.org/soap/envelope`|  
|<span data-ttu-id="b309c-156">wsa</span><span class="sxs-lookup"><span data-stu-id="b309c-156">wsa</span></span>|`http://www.w3.org/2004/08/addressing`|  
|<span data-ttu-id="b309c-157">wscoor</span><span class="sxs-lookup"><span data-stu-id="b309c-157">wscoor</span></span>|`http://schemas.xmlsoap.org/ws/2004/10/wscoor`|  
|<span data-ttu-id="b309c-158">wsat</span><span class="sxs-lookup"><span data-stu-id="b309c-158">wsat</span></span>|`http://schemas.xmlsoap.org/ws/2004/10/wsat`|  
|<span data-ttu-id="b309c-159">t</span><span class="sxs-lookup"><span data-stu-id="b309c-159">t</span></span>|`http://schemas.xmlsoap.org/ws/2005/02/trust`|  
|<span data-ttu-id="b309c-160">o</span><span class="sxs-lookup"><span data-stu-id="b309c-160">o</span></span>|`http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd`|  
|<span data-ttu-id="b309c-161">xsd</span><span class="sxs-lookup"><span data-stu-id="b309c-161">xsd</span></span>|`http://www.w3.org/2001/XMLSchema`|  
  
## <a name="transaction-manager-bindings"></a><span data-ttu-id="b309c-162">異動管理員繫結程序</span><span class="sxs-lookup"><span data-stu-id="b309c-162">Transaction Manager Bindings</span></span>  
 <span data-ttu-id="b309c-163">R1001：異動管理員必須使用 SOAP 1.1 和 WS-Addressing 2004/08 以便交換 WS-Atomic 異動和 WS-Coordination 訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-163">R1001: Transaction Managers must use SOAP 1.1 and WS-Addressing 2004/08 for WS-Atomic Transaction and WS-Coordination message exchanges.</span></span>  
  
 <span data-ttu-id="b309c-164">應用程式訊息並不限於這些繫結，並且會在稍後描述。</span><span class="sxs-lookup"><span data-stu-id="b309c-164">Application messages are not constrained to these bindings and are described later.</span></span>  
  
### <a name="transaction-manager-https-binding"></a><span data-ttu-id="b309c-165">異動管理員 HTTPS 繫結程序</span><span class="sxs-lookup"><span data-stu-id="b309c-165">Transaction Manager HTTPS Binding</span></span>  
 <span data-ttu-id="b309c-166">異動管理員 HTTPS 繫結程序僅依賴傳輸安全性來達到安全性，並且在異動樹狀中的每個傳送者與接收者組之間建立信任。</span><span class="sxs-lookup"><span data-stu-id="b309c-166">The transaction manager HTTPS binding relies solely on transport security to achieve security and establish trust between each sender-receiver pair in the transaction tree.</span></span>  
  
#### <a name="https-transport-configuration"></a><span data-ttu-id="b309c-167">HTTPS 傳輸組態</span><span class="sxs-lookup"><span data-stu-id="b309c-167">HTTPS Transport Configuration</span></span>  
 <span data-ttu-id="b309c-168">X.509 憑證會用來建立交易管理員身分識別。</span><span class="sxs-lookup"><span data-stu-id="b309c-168">X.509 certificates are used to establish Transaction Manager Identity.</span></span> <span data-ttu-id="b309c-169">需要用戶端/伺服器驗證，而用戶端/伺服器授權則留待實作詳細資料中說明：</span><span class="sxs-lookup"><span data-stu-id="b309c-169">Client/server authentication is required, and client/server authorization is left as an implementation detail:</span></span>  
  
- <span data-ttu-id="b309c-170">R1111：透過網路提供的 X.509 憑證必須有符合起始電腦之完整網域名稱 (FQDN) 的主體名稱。</span><span class="sxs-lookup"><span data-stu-id="b309c-170">R1111: X.509 certificates presented over the wire must have a subject name that matches the fully qualified domain name (FQDN) of the originating machine.</span></span>  
  
- <span data-ttu-id="b309c-171">B1112：在系統中每個傳送者與接收者組之間的 DNS 都必須正常運作，X.509 主體名稱檢查才會成功。</span><span class="sxs-lookup"><span data-stu-id="b309c-171">B1112: DNS must be functional between each sender-receiver pair in the system for X.509 subject name checks to succeed.</span></span>  
  
#### <a name="activation-and-registration-binding-configuration"></a><span data-ttu-id="b309c-172">啟動和登錄繫結組態</span><span class="sxs-lookup"><span data-stu-id="b309c-172">Activation and Registration Binding Configuration</span></span>  
 <span data-ttu-id="b309c-173">WCF 需要透過 HTTPS 相互關聯的要求/回復雙工系結。</span><span class="sxs-lookup"><span data-stu-id="b309c-173">WCF requires request/reply duplex binding with correlation over HTTPS.</span></span> <span data-ttu-id="b309c-174">(如需有關相互關聯與要求/回覆訊息交換模式描述的詳細資訊，請參閱第 8 節的「WS-Atomic 交易」)。</span><span class="sxs-lookup"><span data-stu-id="b309c-174">(For more information about correlation and descriptions of the request/reply message exchange patterns, see WS-Atomic Transaction, Section 8.)</span></span>  
  
#### <a name="2pc-protocol-binding-configuration"></a><span data-ttu-id="b309c-175">2PC 通訊協定繫結組態</span><span class="sxs-lookup"><span data-stu-id="b309c-175">2PC Protocol Binding Configuration</span></span>  
 <span data-ttu-id="b309c-176">WCF 支援透過 HTTPS 的單向（資料包）訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-176">WCF supports one-way (datagram) messages over HTTPS.</span></span> <span data-ttu-id="b309c-177">訊息間的相互關聯則留待實作詳細資料中說明。</span><span class="sxs-lookup"><span data-stu-id="b309c-177">Correlation among the messages is left as an implementation detail.</span></span>  
  
 <span data-ttu-id="b309c-178">B2131：執行程式必須 `wsa:ReferenceParameters` 如 ws-addressing 中所述支援，以達成 WCF 的2pc 訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b309c-178">B2131: Implementations must support `wsa:ReferenceParameters` as described in WS-Addressing to achieve correlation of WCF’s 2PC messages.</span></span>  
  
### <a name="transaction-manager-mixed-security-binding"></a><span data-ttu-id="b309c-179">異動管理員混合安全性繫結程序</span><span class="sxs-lookup"><span data-stu-id="b309c-179">Transaction Manager Mixed Security Binding</span></span>  
 <span data-ttu-id="b309c-180">這是替代的（混合模式）系結，它會針對身分識別的建立使用傳輸安全性，並結合 WS-協調發行的權杖模型。</span><span class="sxs-lookup"><span data-stu-id="b309c-180">This is an alternate (mixed mode) binding that uses transport security combined with the  WS-Coordination Issued Token model for identity establishment purposes.</span></span>  <span data-ttu-id="b309c-181">啟動與登錄是兩個繫結之間唯一不同的項目。</span><span class="sxs-lookup"><span data-stu-id="b309c-181">Activation and Registration are the only elements that differ between the two bindings.</span></span>  
  
#### <a name="https-transport-configuration"></a><span data-ttu-id="b309c-182">HTTPS 傳輸組態</span><span class="sxs-lookup"><span data-stu-id="b309c-182">HTTPS Transport Configuration</span></span>  
 <span data-ttu-id="b309c-183">X.509 憑證會用來建立交易管理員身分識別。</span><span class="sxs-lookup"><span data-stu-id="b309c-183">X.509 certificates are used to establish Transaction Manager Identity.</span></span> <span data-ttu-id="b309c-184">需要用戶端/伺服器驗證，而用戶端/伺服器授權則留待實作詳細資料中說明。</span><span class="sxs-lookup"><span data-stu-id="b309c-184">Client/Server authentication is required, and client/server authorization is left as an implementation detail.</span></span>  
  
#### <a name="activation-message-binding-configuration"></a><span data-ttu-id="b309c-185">啟動訊息繫結組態</span><span class="sxs-lookup"><span data-stu-id="b309c-185">Activation Message Binding Configuration</span></span>  
 <span data-ttu-id="b309c-186">啟動訊息通常不會參與互通性，因為啟動訊息一般會發生在應用程式與其本機異動管理員之間。</span><span class="sxs-lookup"><span data-stu-id="b309c-186">Activation Messages usually do not participate in interoperability because they typically occur between an application and its local Transaction Manager.</span></span>  
  
 <span data-ttu-id="b309c-187">B1221： WCF 使用雙工 HTTPS 系結（如[訊息通訊協定](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)中所述）來啟用訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-187">B1221: WCF uses duplex HTTPS binding (described in [Messaging Protocols](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)) for Activation messages.</span></span> <span data-ttu-id="b309c-188">要求與回覆訊息會使用 WS-Addressing 2004/08 來相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b309c-188">Request and Reply messages are correlated using WS-Addressing 2004/08.</span></span>  
  
 <span data-ttu-id="b309c-189">第 8 節的 WS-Atomic 異動規格進一步描述有關相互關聯與訊息交換模式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b309c-189">WS-Atomic Transaction specification, Section 8, describes further details about correlation and the message exchange patterns.</span></span>  
  
- <span data-ttu-id="b309c-190">R1222：在接收到 `CreateCoordinationContext` 後，協調器必須使用關聯的密碼 `SecurityContextToken` 發行 `STx`。</span><span class="sxs-lookup"><span data-stu-id="b309c-190">R1222: Upon receiving a `CreateCoordinationContext`, the Coordinator must issue a `SecurityContextToken` with associated secret `STx`.</span></span> <span data-ttu-id="b309c-191">在符合 WS-Trust 規格的 `t:IssuedTokens` 標頭中會傳回這個權杖。</span><span class="sxs-lookup"><span data-stu-id="b309c-191">This token is returned inside a `t:IssuedTokens` header following WS-Trust specification.</span></span>  
  
- <span data-ttu-id="b309c-192">R1223：如果啟動發生在現有的協調內容中，則使用與現有內容關聯之 `t:IssuedTokens` 的 `SecurityContextToken` 標頭就必須在 `CreateCoordinationContext` 訊息上流通。</span><span class="sxs-lookup"><span data-stu-id="b309c-192">R1223: If Activation occurs within an existing Coordination Context, the `t:IssuedTokens` header with the `SecurityContextToken` associated with existing Context must flow on the `CreateCoordinationContext` message.</span></span>  
  
 <span data-ttu-id="b309c-193">`t:IssuedTokens`應產生新的標頭，以附加至外寄 `wscoor:CreateCoordinationContextResponse` 訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-193">A new `t:IssuedTokens` header should be generated for attaching to the outgoing `wscoor:CreateCoordinationContextResponse` message.</span></span>  
  
#### <a name="registration-message-binding-configuration"></a><span data-ttu-id="b309c-194">登錄訊息繫結組態</span><span class="sxs-lookup"><span data-stu-id="b309c-194">Registration Message Binding Configuration</span></span>  
 <span data-ttu-id="b309c-195">B1231： WCF 使用雙工 HTTPS 系結（如[訊息通訊協定](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)中所述）。</span><span class="sxs-lookup"><span data-stu-id="b309c-195">B1231: WCF uses duplex HTTPS binding (described in [Messaging Protocols](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)).</span></span> <span data-ttu-id="b309c-196">要求與回覆訊息會使用 WS-Addressing 2004/08 來相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b309c-196">Request and Reply messages are correlated using WS-Addressing 2004/08.</span></span>  
  
 <span data-ttu-id="b309c-197">第 8 節的 WS-AtomicTransaction 進一步描述有關相互關聯與訊息交換模式描述的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b309c-197">WS-AtomicTransaction, Section 8, describes further details about correlation and descriptions of the message exchange patterns.</span></span>  
  
 <span data-ttu-id="b309c-198">R1232：外寄 `wscoor:Register` 訊息必須使用 `IssuedTokenOverTransport` [安全性通訊協定](../../../../docs/framework/wcf/feature-details/security-protocols.md)中所述的驗證模式。</span><span class="sxs-lookup"><span data-stu-id="b309c-198">R1232: Outgoing `wscoor:Register` messages must use the `IssuedTokenOverTransport` authentication mode described in [Security Protocols](../../../../docs/framework/wcf/feature-details/security-protocols.md).</span></span>  
  
 <span data-ttu-id="b309c-199">`wsse:Timestamp`必須使用發出的來簽署元素 `SecurityContextToken STx` 。</span><span class="sxs-lookup"><span data-stu-id="b309c-199">The `wsse:Timestamp` element must be signed using the `SecurityContextToken STx` issued.</span></span> <span data-ttu-id="b309c-200">這個簽章是證明與特定異動關聯之權杖的所有權，並且用來驗證異動中登錄的參與者。</span><span class="sxs-lookup"><span data-stu-id="b309c-200">This signature is a proof of possession of the token associated with particular transaction and is used to authenticate a participant enlisting in the transaction.</span></span> <span data-ttu-id="b309c-201">RegistrationResponse 訊息會透過 HTTPS 傳回。</span><span class="sxs-lookup"><span data-stu-id="b309c-201">The RegistrationResponse message is sent back over HTTPS.</span></span>  
  
#### <a name="2pc-protocol-binding-configuration"></a><span data-ttu-id="b309c-202">2PC 通訊協定繫結組態</span><span class="sxs-lookup"><span data-stu-id="b309c-202">2PC Protocol Binding Configuration</span></span>  
 <span data-ttu-id="b309c-203">WCF 支援透過 HTTPS 的單向（資料包）訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-203">WCF supports one-way (datagram) messages over HTTPS.</span></span> <span data-ttu-id="b309c-204">訊息間的相互關聯則留待實作詳細資料中說明。</span><span class="sxs-lookup"><span data-stu-id="b309c-204">Correlation among the messages is left as an implementation detail.</span></span>  
  
 <span data-ttu-id="b309c-205">B2131：執行程式必須 `wsa:ReferenceParameters` 如 ws-addressing 中所述支援，以達成 WCF 的2pc 訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b309c-205">B2131: Implementations must support `wsa:ReferenceParameters` as described in WS-Addressing to achieve correlation of WCF’s 2PC messages.</span></span>  
  
## <a name="application-message-exchange"></a><span data-ttu-id="b309c-206">應用程式訊息交換</span><span class="sxs-lookup"><span data-stu-id="b309c-206">Application Message Exchange</span></span>  
 <span data-ttu-id="b309c-207">應用程式可以隨意使用應用程式之間訊息的任何特定繫結程序，只要繫結程序符合下列安全性需求：</span><span class="sxs-lookup"><span data-stu-id="b309c-207">Applications are free to use any particular binding for application-to-application messages, as long as the binding meets the following security requirements:</span></span>  
  
- <span data-ttu-id="b309c-208">R2001：應用程式之間的訊息必須將 `t:IssuedTokens` 標頭與訊息標頭中的 `CoordinationContext` 一起流通。</span><span class="sxs-lookup"><span data-stu-id="b309c-208">R2001: Application-to-application messages must flow the `t:IssuedTokens` header along with the `CoordinationContext` in the header of the message.</span></span>  
  
- <span data-ttu-id="b309c-209">R2002：必須提供 `t:IssuedToken` 的完整性與機密性。</span><span class="sxs-lookup"><span data-stu-id="b309c-209">R2002: Integrity and confidentiality of `t:IssuedToken` must be provided.</span></span>  
  
 <span data-ttu-id="b309c-210">`CoordinationContext` 標頭包含 `wscoor:Identifier`。</span><span class="sxs-lookup"><span data-stu-id="b309c-210">The `CoordinationContext` header contains `wscoor:Identifier`.</span></span> <span data-ttu-id="b309c-211">雖然的定義 `xsd:AnyURI` 允許同時使用絕對和相對 uri，但 WCF 僅支援 `wscoor:Identifiers` ，其為絕對 uri。</span><span class="sxs-lookup"><span data-stu-id="b309c-211">While the definition of `xsd:AnyURI` allows the use of both absolute and relative URIs, WCF supports only `wscoor:Identifiers`, which are absolute URIs.</span></span>  
  
 <span data-ttu-id="b309c-212">如果的 `wscoor:Identifier` `wscoor:CoordinationContext` 是相對 URI，則會從交易式 WCF 服務傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="b309c-212">If the `wscoor:Identifier` of the `wscoor:CoordinationContext` is a relative URI, faults will be returned from transactional WCF services.</span></span>  
  
## <a name="message-examples"></a><span data-ttu-id="b309c-213">訊息範例</span><span class="sxs-lookup"><span data-stu-id="b309c-213">Message Examples</span></span>  
  
### <a name="createcoordinationcontext-requestresponse-messages"></a><span data-ttu-id="b309c-214">CreateCoordinationContext 要求/回應訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-214">CreateCoordinationContext Request/Response Messages</span></span>  
 <span data-ttu-id="b309c-215">下列訊息會遵循要求/回應模式。</span><span class="sxs-lookup"><span data-stu-id="b309c-215">The following messages follow a request/response pattern.</span></span>  
  
#### <a name="createcoordinationcontext"></a><span data-ttu-id="b309c-216">CreateCoordinationContext</span><span class="sxs-lookup"><span data-stu-id="b309c-216">CreateCoordinationContext</span></span>  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://.../ws/2004/10/wscoor/CreateCoordinationContext</Action>  
    <a:MessageID>urn:uuid:069f5104-fd88-4264-9f99-60032a82854e</MessageID>  
    <a:ReplyTo>  
      <Address>https://...</a:Address>  
    </a:ReplyTo>  
    <a:To>https://...</a:To>  
    <wsse:Security>  
      <u:Timestamp>  
        <wsu:Created>2005-12-15T23:36:09.921Z</wsu:Created>  
        <wsu:Expires>2005-12-15T23:41:09.921Z</wsu:Expires>  
      </u:Timestamp>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:CreateCoordinationContext>  
      <wscoor:CoordinationType>...</wscoor:CoordinationType>  
    </wscoor:CreateCoordinationContext>  
  </s:Body>  
</s11:Envelope>  
```  
  
#### <a name="createcoordinationcontextresponse"></a><span data-ttu-id="b309c-217">CreateCoordinationContextResponse</span><span class="sxs-lookup"><span data-stu-id="b309c-217">CreateCoordinationContextResponse</span></span>  
  
```xml  
<s:Envelope>  
  <!-- Data below is shown in the clear for  
       illustration purposes only. -->  
  <s:Header>  
    <a:Action>./ws/2004/10/wscoor/CreateCoordinationContextResponse </a:Action>  
    <a:RelatesTo>urn:uuid:069f5104-fd88-4264-9f99-60032a82854e</a:RelatesTo>  
    <a:To s:mustUnderstand="1">https://... </a:To>  
    <t:IssuedTokens>  
 <wst:RequestSecurityTokenResponse
    xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
    xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd"
    xmlns:wst="http://schemas.xmlsoap.org/ws/2005/02/trust"  
    xmlns:wsc="http://schemas.xmlsoap.org/ws/2005/02/sc"  
    xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">  
    <wst:TokenType>http://schemas.xmlsoap.org/ws/2005/02/sc/sct</wst:TokenType>  
    <wst:RequestedSecurityToken>  
      <wsc:SecurityContextToken>  
        <wssu:Identifier>  
          http://fabrikam123.com/SCTi  
        </wssu:Identifier>  
      </wsc:SecurityContextToken>
    </wst:RequestedSecurityToken>  
    <wsp:AppliesTo>  
        http://fabrikam123.com/CCi  
    </wsp:AppliesTo>
    <wst:RequestedAttachedReference>  
      <wsse:SecurityTokenReference >  
        <wsse:Reference
           ValueType="http://schemas.xmlsoap.org/ws/2005/02/sc/sct"  
           URI="http://fabrikam123.com/SCTi"/>  
      </wsse:SecurityTokenReference>  
    </wst:RequestedAttachedReference>  
    <wst:RequestedUnattachedReference>  
      <wsse:SecurityTokenReference>  
        <wsse:Reference
          ValueType="http://schemas.xmlsoap.org/ws/2005/02/sc/sct"  
          URI="http://fabrikam123.com/SCTi"/>  
      </wsse:SecurityTokenReference>  
    </wst:RequestedUnattachedReference>  
    <wst:RequestedProofToken>  
      <wst:BinarySecret
        Type="http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey">  
        <!-- base64 encoded value -->  
      </wst:BinarySecret>  
    </wst:RequestedProofToken>  
    <wst:Lifetime>  
      <wssu:Created>2005-10-24T20:19:26.526Z</wssu:Created>  
      <wssu:Expires>2005-10-25T06:24:26.526Z</wssu:Expires>  
    </wst:Lifetime>  
    <wst:KeySize>256</wst:KeySize>  
</wst:RequestSecurityTokenResponse>  
    </t:IssuedTokens>  
    <o:Security xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="_0">  
        <u:Created>2005-12-15T23:36:12.015Z</u:Created>  
        <u:Expires>2005-12-15T23:41:12.015Z</u:Expires>  
      </u:Timestamp>  
    </o:Security>  
  </s:Header>  
  <s:Body>  
    <wscoor:CreateCoordinationContextResponse>  
      <wscoor:CoordinationContext>  
        <wscoor:Identifier>  
     http://fabrikam123.com/CCi  
      </wscoor:Identifier>  
        <wscoor:Expires>...</wscoor:Expires>  
        <wscoor:CoordinationType>...</wscoor:CoordinationType>  
        <wscoor:RegistrationService>  
          <a:Address>https://...</a:Address>  
          <a:ReferenceParameters>  
             ...  
          </a:ReferenceParameters>  
        </wscoor:RegistrationService>  
      </wscoor:CoordinationContext>  
    </wscoor:CreateCoordinationContextResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="registration-messages"></a><span data-ttu-id="b309c-218">登錄訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-218">Registration Messages</span></span>  
 <span data-ttu-id="b309c-219">下列訊息是登錄訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-219">The following messages are registration messages.</span></span>  
  
#### <a name="register"></a><span data-ttu-id="b309c-220">註冊</span><span class="sxs-lookup"><span data-stu-id="b309c-220">Register</span></span>  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://schemas.xmlsoap.org/ws/2004/10/wscoor/Register</a:Action>  
    <a:MessageID>urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088e</a:MessageID>  
    <a:ReplyTo>  
      <a:Address>https://...</a:Address>
    </a:ReplyTo>  
    <a:To>https://...</a:To>  
    <wsse:Security
      s:mustUnderstand="1"
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp wssu:Id="_0" >  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
      <wsc:SecurityContextToken>  
      <wssu:Identifier>  
          http://fabrikam123.com/SCTi  
      </wssu:Identifier>  
      </wsc:SecurityContextToken>  
      <!-- supporting signature over the timestamp -->  
      <wsse:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">  
        <ds:SignedInfo>  
          <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
          <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#hmac-sha1"/>  
          <ds:Reference URI="#_0">  
            <ds:Transforms>  
              <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
            </ds:Transforms>  
            <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>  
            <ds:DigestValue>  
              alRzyhjLgoUOYoh8cx4n75eTcUk=  
            </ds:DigestValue>  
          </ds:Reference>  
        </ds:SignedInfo>  
        <ds:SignatureValue>YZYjnVvSOVasAQqQxaaviTSWtqI=</ds:SignatureValue>  
        <ds:KeyInfo>  
          <wsse:SecurityTokenReference  
            xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
            <wsse:Reference
              URI="http://fabrikam123.com/SCTi"/>  
          </wsse:SecurityTokenReference>  
        </ds:KeyInfo>  
      </wsse:Signature>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:Register>  
      <wscoor:ProtocolIdentifier>...</wscoor:ProtocolIdentifier>  
      <wscoor:ParticipantProtocolService>  
        <a:Address>https://... </a:Address>  
      </wscoor:ParticipantProtocolService>  
    </wscoor:Register>  
  </s:Body>  
</s:Envelope>  
```  
  
#### <a name="register-response"></a><span data-ttu-id="b309c-221">註冊回應</span><span class="sxs-lookup"><span data-stu-id="b309c-221">Register Response</span></span>  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>  
      http://schemas.xmlsoap.org/ws/2004/10/wscoor/RegisterResponse  
    </a:Action>  
    <a:MessageID>urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088d</a:MessageID>  
    <a:RelatesTo>  
      urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088e
    </a:RelatesTo>  
    <a:To>https://...</a:To>  
    <wsse:Security
      s:mustUnderstand="1"
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp>  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:RegisterResponse>  
      <wscoor:CoordinatorProtocolService>  
        <a:Address>https://...</a:Address>  
        <a:ReferenceParameters>  
          ...  
        </a:ReferenceParameters>  
      </wscoor:CoordinatorProtocolService>  
    </wscoor:RegisterResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="two-phase-commit-protocol-messages"></a><span data-ttu-id="b309c-222">兩階段交易認可通訊協定訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-222">Two Phase Commit Protocol Messages</span></span>  
 <span data-ttu-id="b309c-223">下列訊息與兩階段交易認可 (2PC) 通訊協定有關。</span><span class="sxs-lookup"><span data-stu-id="b309c-223">The following message relates to the two-phase commit (2PC) protocol.</span></span>  
  
#### <a name="commit"></a><span data-ttu-id="b309c-224">Commit</span><span class="sxs-lookup"><span data-stu-id="b309c-224">Commit</span></span>  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://.../ws/2004/10/wsat/Commit</a:Action>  
    <a:To>https://...</a:To>  
    <wsse:Security
      s:mustUnderstand="1"
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp wssu:Id="_0" >  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
   </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wsat:Commit />  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="application-messages"></a><span data-ttu-id="b309c-225">應用程式訊息</span><span class="sxs-lookup"><span data-stu-id="b309c-225">Application Messages</span></span>  
 <span data-ttu-id="b309c-226">下列訊息是應用程式訊息。</span><span class="sxs-lookup"><span data-stu-id="b309c-226">The following messages are application messages.</span></span>  
  
#### <a name="application-message-request"></a><span data-ttu-id="b309c-227">應用程式訊息要求</span><span class="sxs-lookup"><span data-stu-id="b309c-227">Application message-Request</span></span>  
  
```xml  
<s:Envelope>  
  <s:Header>  
<!-- Addressing headers, all signed-->  
    <wsse:Security s:mustUnderstand="1">  
      <wssu:Timestamp wssu:Id="timestamp">
        <wssu:Created>2005-10-25T06:29:18.703Z</wssu:Created>  
        <wssu:Expires>2005-10-25T06:34:18.703Z</wssu:Expires>  
      </wssu:Timestamp>  
      <wsse:BinarySecurityToken
          wssu:Id="IA_Certificate"
          ValueType="...#X509v3"
          EncodingType="...#Base64Binary">  
        <!-- IA certificate -->  
      </wsse:BinarySecurityToken>  
      <e:EncryptedKey Id="encrypted_key">  
            <!-- ephemeral key encrypted for PA certificate -->
        <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
          <e:DataReference URI="#encrypted_body"/>  
          <e:DataReference URI="#encrypted_CCi"/>  
          <e:DataReference URI="#encrypted_issuedtokens"/>  
        </e:ReferenceList>  
      </e:EncryptedKey>  
      <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <!-- signature over Addressing headers, Timestamp, and Body -->  
      </Signature>  
    </wsse:Security>  
    <wsse11:EncryptedHeader>  
     <!-- encrypted wscoor:CoordinationContext header containing CCi -->  
    </wsse11:EncryptedHeader>  
    <wsse11:EncryptedHeader>
      <!-- encrypted wst:IssuedTokens header containing SCTi -->  
      <!-- wst:IssuedTokens header is taken verbatim from message #2 above, omitted for brevity -->  
    </wsse11:EncryptedHeader>  
  </s:Header>  
  <s:Body wssu:Id="body">  
    <!-- encrypted content of the Body element of the application message -->
    <e:EncryptedData Id="encrypted_body"
           Type="http://www.w3.org/2001/04/xmlenc#Content"
           xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
...  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
```

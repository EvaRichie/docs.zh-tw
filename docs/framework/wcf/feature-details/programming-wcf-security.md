---
title: WCF 安全性程式設計
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- message security [WCF], programming overview
ms.assetid: 739ec222-4eda-4cc9-a470-67e64a7a3f10
ms.openlocfilehash: 2b3c96e91c0d6f01fa30b3b617449e7d4a148933
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596769"
---
# <a name="programming-wcf-security"></a><span data-ttu-id="58d2b-102">WCF 安全性程式設計</span><span class="sxs-lookup"><span data-stu-id="58d2b-102">Programming WCF Security</span></span>
<span data-ttu-id="58d2b-103">本主題說明用來建立安全 Windows Communication Foundation （WCF）應用程式的基本程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="58d2b-103">This topic describes the fundamental programming tasks used to create a secure Windows Communication Foundation (WCF) application.</span></span> <span data-ttu-id="58d2b-104">本主題僅涵蓋驗證、機密性和完整性，統稱為*傳輸安全性*。</span><span class="sxs-lookup"><span data-stu-id="58d2b-104">This topic covers only authentication, confidentiality, and integrity, collectively known as *transfer security*.</span></span> <span data-ttu-id="58d2b-105">本主題並未涵蓋授權（控制對資源或服務的存取權）;如需授權的詳細資訊，請參閱[授權](authorization-in-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-105">This topic does not cover authorization (the control of access to resources or services); for information on authorization, see [Authorization](authorization-in-wcf.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="58d2b-106">如需安全性概念的重要簡介（特別是關於 WCF），請參閱 MSDN 上的一組模式和實務教學課程，其中[提供 Web 服務增強功能（WSE）3.0 的案例、模式和執行指引](https://docs.microsoft.com/previous-versions/msp-n-p/ff648183(v=pandp.10))。</span><span class="sxs-lookup"><span data-stu-id="58d2b-106">For a valuable introduction to security concepts, especially in regard to WCF, see the set of patterns and practices tutorials on MSDN at [Scenarios, Patterns, and Implementation Guidance for Web Services Enhancements (WSE) 3.0](https://docs.microsoft.com/previous-versions/msp-n-p/ff648183(v=pandp.10)).</span></span>  
  
 <span data-ttu-id="58d2b-107">WCF 安全性程式設計是以三個步驟為基礎，設定如下：安全性模式、用戶端認證類型和認證值。</span><span class="sxs-lookup"><span data-stu-id="58d2b-107">Programming WCF security is based on three steps setting the following: the security mode, a client credential type, and the credential values.</span></span> <span data-ttu-id="58d2b-108">您可以透過程式碼或組態執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="58d2b-108">You can perform these steps either through code or configuration.</span></span>  
  
## <a name="setting-the-security-mode"></a><span data-ttu-id="58d2b-109">設定安全性模式</span><span class="sxs-lookup"><span data-stu-id="58d2b-109">Setting the Security Mode</span></span>  
 <span data-ttu-id="58d2b-110">以下說明在 WCF 中使用安全性模式進行程式設計的一般步驟：</span><span class="sxs-lookup"><span data-stu-id="58d2b-110">The following explains the general steps for programming with the security mode in WCF:</span></span>  
  
1. <span data-ttu-id="58d2b-111">針對應用程式需求選取一項適合的預先定義繫結程序。</span><span class="sxs-lookup"><span data-stu-id="58d2b-111">Select one of the predefined bindings appropriate to your application requirements.</span></span> <span data-ttu-id="58d2b-112">如需系結選項的清單，請參閱[系統提供](../system-provided-bindings.md)的系結。</span><span class="sxs-lookup"><span data-stu-id="58d2b-112">For a list of the binding choices, see [System-Provided Bindings](../system-provided-bindings.md).</span></span> <span data-ttu-id="58d2b-113">根據預設，幾乎所有的繫結都會啟用安全性。</span><span class="sxs-lookup"><span data-stu-id="58d2b-113">By default, nearly every binding has security enabled.</span></span> <span data-ttu-id="58d2b-114">其中一個例外狀況是 <xref:System.ServiceModel.BasicHttpBinding> 類別（使用設定、 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) ）。</span><span class="sxs-lookup"><span data-stu-id="58d2b-114">The one exception is the <xref:System.ServiceModel.BasicHttpBinding> class (using configuration, the [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md)).</span></span>  
  
     <span data-ttu-id="58d2b-115">您選取的繫結將決定傳輸方式。</span><span class="sxs-lookup"><span data-stu-id="58d2b-115">The binding you select determines the transport.</span></span> <span data-ttu-id="58d2b-116">例如，<xref:System.ServiceModel.WSHttpBinding> 會使用 HTTP 做為傳輸方式；而 <xref:System.ServiceModel.NetTcpBinding> 則使用 TCP。</span><span class="sxs-lookup"><span data-stu-id="58d2b-116">For example, <xref:System.ServiceModel.WSHttpBinding> uses HTTP as the transport; <xref:System.ServiceModel.NetTcpBinding> uses TCP.</span></span>  
  
2. <span data-ttu-id="58d2b-117">選取其中一項安全性模式來進行繫結。</span><span class="sxs-lookup"><span data-stu-id="58d2b-117">Select one of the security modes for the binding.</span></span> <span data-ttu-id="58d2b-118">請注意，您選取的繫結會決定可用的模式選項有哪些。</span><span class="sxs-lookup"><span data-stu-id="58d2b-118">Note that the binding you select determines the available mode choices.</span></span> <span data-ttu-id="58d2b-119">例如，<xref:System.ServiceModel.WSDualHttpBinding> 不允許使用傳輸安全性 (未包含在選項中)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-119">For example, the <xref:System.ServiceModel.WSDualHttpBinding> does not allow transport security (it is not an option).</span></span> <span data-ttu-id="58d2b-120">同樣地，<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 和 <xref:System.ServiceModel.NetNamedPipeBinding> 也都不允許使用訊息安全性。</span><span class="sxs-lookup"><span data-stu-id="58d2b-120">Similarly, neither the <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> nor the <xref:System.ServiceModel.NetNamedPipeBinding> allows message security.</span></span>  
  
     <span data-ttu-id="58d2b-121">您有下列三個選擇：</span><span class="sxs-lookup"><span data-stu-id="58d2b-121">You have three choices:</span></span>  
  
    1. `Transport`  
  
         <span data-ttu-id="58d2b-122">傳輸安全性將視您選取之繫結所使用的機制而定。</span><span class="sxs-lookup"><span data-stu-id="58d2b-122">Transport security depends on the mechanism that the binding you have selected uses.</span></span> <span data-ttu-id="58d2b-123">例如，假使您使用 `WSHttpBinding`，則安全性機制為安全通訊端層 (SSL) (同時也是 HTTPS 通訊協定的機制)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-123">For example, if you are using `WSHttpBinding` then the security mechanism is Secure Sockets Layer (SSL) (also the mechanism for the HTTPS protocol).</span></span> <span data-ttu-id="58d2b-124">一般來說，傳輸安全性的主要優點在於，不管您使用哪種傳輸機制，都能提供良好的輸送量。</span><span class="sxs-lookup"><span data-stu-id="58d2b-124">Generally speaking, the main advantage of transport security is that it delivers good throughput no matter which transport you are using.</span></span> <span data-ttu-id="58d2b-125">但是，它有兩項限制：首先就是傳輸機制會指出用來驗證使用者的認證類型。</span><span class="sxs-lookup"><span data-stu-id="58d2b-125">However, it does have two limitations: The first is that the transport mechanism dictates the credential type used to authenticate a user.</span></span> <span data-ttu-id="58d2b-126">只有當服務需要與其他要求不同認證類型的服務交互操作時，這個限制才會成為缺點。</span><span class="sxs-lookup"><span data-stu-id="58d2b-126">This is a drawback only if a service needs to interoperate with other services that demand different types of credentials.</span></span> <span data-ttu-id="58d2b-127">第二個限制是，由於訊息層級並未套用安全性，所以會以躍點方式 (而不是以端對端方式) 來實作安全性。</span><span class="sxs-lookup"><span data-stu-id="58d2b-127">The second is that, because the security is not applied at the message level, security is implemented in a hop-by-hop manner rather than end-to-end.</span></span> <span data-ttu-id="58d2b-128">只有當用戶端與服務之間的訊息路徑包含媒介時，第二個限制才會成為問題。</span><span class="sxs-lookup"><span data-stu-id="58d2b-128">This latter limitation is an issue only if the message path between client and service includes intermediaries.</span></span> <span data-ttu-id="58d2b-129">如需所要使用之傳輸的詳細資訊，請參閱[選擇傳輸](choosing-a-transport.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-129">For more information about which transport to use, see [Choosing a Transport](choosing-a-transport.md).</span></span> <span data-ttu-id="58d2b-130">如需有關使用傳輸安全性的詳細資訊，請參閱[傳輸安全性總覽](transport-security-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-130">For more information about using transport security, see [Transport Security Overview](transport-security-overview.md).</span></span>  
  
    2. `Message`  
  
         <span data-ttu-id="58d2b-131">訊息安全性表示每則訊息都包含保護訊息安全的必要標頭與資料。</span><span class="sxs-lookup"><span data-stu-id="58d2b-131">Message security means that every message includes the necessary headers and data to keep the message secure.</span></span> <span data-ttu-id="58d2b-132">由於標頭的組成份子各有不同，因此您可以加入任何數量的認證。</span><span class="sxs-lookup"><span data-stu-id="58d2b-132">Because the composition of the headers varies, you can include any number of credentials.</span></span> <span data-ttu-id="58d2b-133">如果您正與其他需要特定認證類型 (但無法適用傳輸機制) 的服務進行交互操作，或是如果訊息必須與一個以上的服務搭配使用，而其中每個服務需要不同的認證類型時，這項特性就會變成一個要件。</span><span class="sxs-lookup"><span data-stu-id="58d2b-133">This becomes a factor if you are interoperating with other services that demand a specific credential type that a transport mechanism can't supply, or if the message must be used with more than one service, where each service demands a different credential type.</span></span>  
  
         <span data-ttu-id="58d2b-134">如需詳細資訊，請參閱[訊息安全性](message-security-in-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-134">For more information, see [Message Security](message-security-in-wcf.md).</span></span>  
  
    3. `TransportWithMessageCredential`  
  
         <span data-ttu-id="58d2b-135">這項選擇使用傳輸層來保護訊息傳輸的安全，而每則訊息則包含其他服務所需的豐富認證。</span><span class="sxs-lookup"><span data-stu-id="58d2b-135">This choice uses the transport layer to secure the message transfer, while every message includes the rich credentials other services need.</span></span> <span data-ttu-id="58d2b-136">這項選擇會將傳輸安全性的效能優點，與訊息安全性的豐富認證優勢加以結合。</span><span class="sxs-lookup"><span data-stu-id="58d2b-136">This combines the performance advantage of transport security with the rich credentials advantage of message security.</span></span> <span data-ttu-id="58d2b-137">您可透過下列繫結來獲得這項優勢：<xref:System.ServiceModel.BasicHttpBinding>、<xref:System.ServiceModel.WSFederationHttpBinding>、<xref:System.ServiceModel.NetPeerTcpBinding> 和 <xref:System.ServiceModel.WSHttpBinding>。</span><span class="sxs-lookup"><span data-stu-id="58d2b-137">This is available with the following bindings: <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WSFederationHttpBinding>, <xref:System.ServiceModel.NetPeerTcpBinding>, and <xref:System.ServiceModel.WSHttpBinding>.</span></span>  
  
3. <span data-ttu-id="58d2b-138">如果您決定在 HTTP 上使用傳輸安全性 (亦即，HTTPS)，必須同時使用 SSL 憑證來設定主機，並啟用連接埠上的 SSL。</span><span class="sxs-lookup"><span data-stu-id="58d2b-138">If you decide to use transport security for HTTP (in other words, HTTPS), you must also configure the host with an SSL certificate and enable SSL on a port.</span></span> <span data-ttu-id="58d2b-139">如需詳細資訊，請參閱[HTTP 傳輸安全性](http-transport-security.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-139">For more information, see [HTTP Transport Security](http-transport-security.md).</span></span>  
  
4. <span data-ttu-id="58d2b-140">如果您正在使用 <xref:System.ServiceModel.WSHttpBinding> 而且不需要建立安全工作階段，請將 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 屬性設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="58d2b-140">If you are using the <xref:System.ServiceModel.WSHttpBinding> and do not need to establish a secure session, set the <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> property to `false`.</span></span>  
  
     <span data-ttu-id="58d2b-141">當用戶端與服務透過對稱金鑰來建立通道時，就會產生安全工作階段 (用戶端與伺服器都會在對話期間全程使用相同的金鑰，直到對話結束為止)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-141">A secure session occurs when a client and service create a channel using a symmetric key (both client and server use the same key for the length of a conversation, until the dialog is closed).</span></span>  
  
## <a name="setting-the-client-credential-type"></a><span data-ttu-id="58d2b-142">設定用戶端認證類型</span><span class="sxs-lookup"><span data-stu-id="58d2b-142">Setting the Client Credential Type</span></span>  
 <span data-ttu-id="58d2b-143">視需要選取用戶端認證類型。</span><span class="sxs-lookup"><span data-stu-id="58d2b-143">Select a client credential type as appropriate.</span></span> <span data-ttu-id="58d2b-144">如需詳細資訊，請參閱[選取認證類型](selecting-a-credential-type.md)。</span><span class="sxs-lookup"><span data-stu-id="58d2b-144">For more information, see [Selecting a Credential Type](selecting-a-credential-type.md).</span></span> <span data-ttu-id="58d2b-145">下列為可用的用戶端認證類型：</span><span class="sxs-lookup"><span data-stu-id="58d2b-145">The following client credential types are available:</span></span>  
  
- `Windows`  
  
- `Certificate`  
  
- `Digest`  
  
- `Basic`  
  
- `UserName`  
  
- `NTLM`  
  
- `IssuedToken`  
  
 <span data-ttu-id="58d2b-146">視模式的設定方式而定，您必須設定認證類型。</span><span class="sxs-lookup"><span data-stu-id="58d2b-146">Depending on how you set the mode, you must set the credential type.</span></span> <span data-ttu-id="58d2b-147">例如，如果您選取了 `wsHttpBinding`，並將模式設為 [訊息]，則也可以將 Message 項目的 `clientCredentialType` 屬性設為下列其中一個值：`None`、`Windows`、`UserName`、`Certificate` 和 `IssuedToken`，如下列組態範例所示。</span><span class="sxs-lookup"><span data-stu-id="58d2b-147">For example, if you have selected the `wsHttpBinding`, and have set the mode to "Message," then you can also set the `clientCredentialType` attribute of the Message element to one of the following values: `None`, `Windows`, `UserName`, `Certificate`, and `IssuedToken`, as shown in the following configuration example.</span></span>  
  
```xml  
<system.serviceModel>  
<bindings>  
  <wsHttpBinding>  
    <binding name="myBinding">  
      <security mode="Message"/>  
      <message clientCredentialType="Windows"/>  
    </binding>
  </wsHttpBinding>
</bindings>  
</system.serviceModel>  
```  
  
 <span data-ttu-id="58d2b-148">或在程式碼中：</span><span class="sxs-lookup"><span data-stu-id="58d2b-148">Or in code:</span></span>  
  
 [!code-csharp[c_WsHttpService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wshttpservice/cs/source.cs#1)]
 [!code-vb[c_WsHttpService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wshttpservice/vb/source.vb#1)]  
  
## <a name="setting-service-credential-values"></a><span data-ttu-id="58d2b-149">設定服務認證值</span><span class="sxs-lookup"><span data-stu-id="58d2b-149">Setting Service Credential Values</span></span>  
 <span data-ttu-id="58d2b-150">一旦您選取了用戶端認證類型，就必須設定實際認證以供服務與用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="58d2b-150">Once you select a client credential type, you must set the actual credentials for the service and client to use.</span></span> <span data-ttu-id="58d2b-151">在服務上，認證需透過 <xref:System.ServiceModel.Description.ServiceCredentials> 類別來加以設定，並由 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 類別的 <xref:System.ServiceModel.ServiceHostBase> 屬性傳回。</span><span class="sxs-lookup"><span data-stu-id="58d2b-151">On the service, credentials are set using the <xref:System.ServiceModel.Description.ServiceCredentials> class and returned by the <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> property of the <xref:System.ServiceModel.ServiceHostBase> class.</span></span> <span data-ttu-id="58d2b-152">使用中的繫結意指服務認證類型、選擇的安全性模式，以及用戶端認證類型。</span><span class="sxs-lookup"><span data-stu-id="58d2b-152">The binding in use implies the service credential type, the security mode chosen, and the type of the client credential.</span></span> <span data-ttu-id="58d2b-153">下列程式碼將為服務認證設定憑證。</span><span class="sxs-lookup"><span data-stu-id="58d2b-153">The following code sets a certificate for a service credential.</span></span>  
  
 [!code-csharp[c_tcpService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_tcpservice/cs/source.cs#3)]
 [!code-vb[c_tcpService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_tcpservice/vb/source.vb#3)]  
  
## <a name="setting-client-credential-values"></a><span data-ttu-id="58d2b-154">設定用戶端認證值</span><span class="sxs-lookup"><span data-stu-id="58d2b-154">Setting Client Credential Values</span></span>  
 <span data-ttu-id="58d2b-155">在用戶端上，用戶端認證值是使用 <xref:System.ServiceModel.Description.ClientCredentials> 類別進行設定，並由 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 類別的 <xref:System.ServiceModel.ClientBase%601> 屬性傳回。</span><span class="sxs-lookup"><span data-stu-id="58d2b-155">On the client, set client credential values using the <xref:System.ServiceModel.Description.ClientCredentials> class and returned by the <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> property of the <xref:System.ServiceModel.ClientBase%601> class.</span></span> <span data-ttu-id="58d2b-156">下列程式碼將透過 TCP 通訊協定在用戶端上將憑證設為認證。</span><span class="sxs-lookup"><span data-stu-id="58d2b-156">The following code sets a certificate as a credential on a client using the TCP protocol.</span></span>  
  
 [!code-csharp[c_TcpClient#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_tcpclient/cs/source.cs#1)]
 [!code-vb[c_TcpClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_tcpclient/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="58d2b-157">請參閱</span><span class="sxs-lookup"><span data-stu-id="58d2b-157">See also</span></span>

- [<span data-ttu-id="58d2b-158">基本 WCF 程式設計</span><span class="sxs-lookup"><span data-stu-id="58d2b-158">Basic WCF Programming</span></span>](../basic-wcf-programming.md)
- [<span data-ttu-id="58d2b-159">常見的安全性案例</span><span class="sxs-lookup"><span data-stu-id="58d2b-159">Common Security Scenarios</span></span>](common-security-scenarios.md)

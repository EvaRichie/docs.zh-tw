---
title: 確保用戶端的安全
ms.date: 03/30/2017
helpviewer_keywords:
- clients [WCF], security considerations
ms.assetid: 44c8578c-9a5b-4acd-8168-1c30a027c4c5
ms.openlocfilehash: b7f720b83a858c8739d2f7b9bf63d29c54b914e0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242249"
---
# <a name="securing-clients"></a><span data-ttu-id="789df-102">確保用戶端的安全</span><span class="sxs-lookup"><span data-stu-id="789df-102">Securing Clients</span></span>

<span data-ttu-id="789df-103">在 Windows Communication Foundation (WCF) 中，此服務會指定用戶端的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="789df-103">In Windows Communication Foundation (WCF), the service dictates the security requirements for clients.</span></span> <span data-ttu-id="789df-104">也就是說，服務會指定使用哪一個安全性模式，以及用戶端是否必須提供認證。</span><span class="sxs-lookup"><span data-stu-id="789df-104">That is, the service specifies what security mode to use, and whether or not the client must provide a credential.</span></span> <span data-ttu-id="789df-105">因此，保護用戶端安全的程序便十分簡單，只要使用從服務 (如果已發行) 取得的中繼資料並建立用戶端即可。</span><span class="sxs-lookup"><span data-stu-id="789df-105">The process of securing a client, therefore, is simple: use the metadata obtained from the service (if it is published) and build a client.</span></span> <span data-ttu-id="789df-106">中繼資料指定如何設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="789df-106">The metadata specifies how to configure the client.</span></span> <span data-ttu-id="789df-107">如果服務要求用戶端提供認證，則您必須取得符合要求的認證。</span><span class="sxs-lookup"><span data-stu-id="789df-107">If the service requires that the client supply a credential, then you must obtain a credential that fits the requirement.</span></span> <span data-ttu-id="789df-108">本主題將進一步探討此程序。</span><span class="sxs-lookup"><span data-stu-id="789df-108">This topic discusses the process in further detail.</span></span> <span data-ttu-id="789df-109">如需有關建立安全服務的詳細資訊，請參閱 [保護服務](securing-services.md)。</span><span class="sxs-lookup"><span data-stu-id="789df-109">For more information about creating a secure service, see [Securing Services](securing-services.md).</span></span>  
  
## <a name="the-service-specifies-security"></a><span data-ttu-id="789df-110">指定安全性的服務</span><span class="sxs-lookup"><span data-stu-id="789df-110">The Service Specifies Security</span></span>  

 <span data-ttu-id="789df-111">根據預設，WCF 系結已啟用安全性功能。</span><span class="sxs-lookup"><span data-stu-id="789df-111">By default, WCF bindings have security features enabled.</span></span> <span data-ttu-id="789df-112"> (例外狀況是 <xref:System.ServiceModel.BasicHttpBinding> 。 ) 因此，如果服務是使用 WCF 建立的，就會有更多機會執行安全性，以確保驗證、機密性和完整性。</span><span class="sxs-lookup"><span data-stu-id="789df-112">(The exception is the <xref:System.ServiceModel.BasicHttpBinding>.) Therefore, if the service was created using WCF, there is a greater chance that it will implement security to ensure authentication, confidentiality, and integrity.</span></span> <span data-ttu-id="789df-113">在該情況下，服務提供的中繼資料將指示它需要什麼來建立安全的通訊通道。</span><span class="sxs-lookup"><span data-stu-id="789df-113">In that case, the metadata the service provides will indicate what it requires to establish a secure communication channel.</span></span> <span data-ttu-id="789df-114">如果服務中繼資料沒有任何安全性需要，那麼就沒有方法強制服務採用安全性配置 (例如透過 HTTP 的 Secure Sockets Layer (SSL))。</span><span class="sxs-lookup"><span data-stu-id="789df-114">If the service metadata does not include any security requirements, there is no way to impose a security scheme, such as Secure Sockets Layer (SSL) over HTTP, on a service.</span></span> <span data-ttu-id="789df-115">如果服務要求用戶端提供認證，則用戶端開發人員、部署人員或管理員必須提供用戶端用來向服務驗證的實際認證。</span><span class="sxs-lookup"><span data-stu-id="789df-115">If, however, the service requires the client to supply a credential, then the client developer, deployer, or administrator must supply the actual credential that the client will use to authenticate itself to the service.</span></span>  
  
## <a name="obtaining-metadata"></a><span data-ttu-id="789df-116">取得中繼資料</span><span class="sxs-lookup"><span data-stu-id="789df-116">Obtaining Metadata</span></span>  

 <span data-ttu-id="789df-117">建立用戶端時，第一個步驟是取得與用戶端通訊的服務中繼資料。</span><span class="sxs-lookup"><span data-stu-id="789df-117">When creating a client, the first step is to obtain the metadata for the service that the client will communicate with.</span></span> <span data-ttu-id="789df-118">有兩種方法可以達到這個目的：</span><span class="sxs-lookup"><span data-stu-id="789df-118">This can be done in two ways.</span></span> <span data-ttu-id="789df-119">首先，如果服務將 (MEX 的中繼資料交換發佈) 端點，或透過 HTTP 或 HTTPS 提供它的中繼資料，您可以使用 [配置 [中繼資料公用程式] 工具 ( # A0) ](servicemodel-metadata-utility-tool-svcutil-exe.md)來下載中繼資料，這會同時產生用戶端的程式碼檔案，以及設定檔。</span><span class="sxs-lookup"><span data-stu-id="789df-119">First, if the service publishes a metadata exchange (MEX) endpoint or makes its metadata available over HTTP or HTTPS, you can download the metadata using the [ServiceModel Metadata Utility Tool (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), which generates both code files for a client as well as a configuration file.</span></span> <span data-ttu-id="789df-120"> (如需使用此工具的詳細資訊，請參閱 [使用 WCF 用戶端存取服務](accessing-services-using-a-wcf-client.md)。 ) 如果服務未發佈 MEX 端點，而且也未透過 HTTP 或 HTTPS 提供其中繼資料，您必須洽詢服務建立者，以取得描述安全性需求和中繼資料的檔。</span><span class="sxs-lookup"><span data-stu-id="789df-120">(For more information about using the tool, see [Accessing Services Using a WCF Client](accessing-services-using-a-wcf-client.md).) If the service does not publish a MEX endpoint and also does not make its metadata available over HTTP or HTTPS, you must contact the service creator for documentation that describes the security requirements and the metadata.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="789df-121">建議使用來自受信任來源且不可竄改的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="789df-121">It is recommended that the metadata come from a trusted source and that it not be tampered with.</span></span> <span data-ttu-id="789df-122">使用 HTTP 通訊協定擷取的中繼資料會以純文字傳送出去且可以竄改。</span><span class="sxs-lookup"><span data-stu-id="789df-122">Metadata retrieved using the HTTP protocol is sent in clear text and can be tampered with.</span></span> <span data-ttu-id="789df-123">如果服務使用 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 和 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> 屬性，請以服務建立者提供的 URL 來使用 HTTPS 通訊協定下載資料。</span><span class="sxs-lookup"><span data-stu-id="789df-123">If the service uses the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> and <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> properties, use the URL the service creator supplied to download the data using the HTTPS protocol.</span></span>  
  
## <a name="validating-security"></a><span data-ttu-id="789df-124">驗證安全性</span><span class="sxs-lookup"><span data-stu-id="789df-124">Validating Security</span></span>  

 <span data-ttu-id="789df-125">中繼來源可以區分成兩大類別：信任來源與不受信任的來源。</span><span class="sxs-lookup"><span data-stu-id="789df-125">Metadata sources can be divided into two broad categories: trust sources and untrusted sources.</span></span> <span data-ttu-id="789df-126">如果您信任來源，而且已從該來源的安全 MEX 端點下載用戶端程式碼和其他中繼資料，那麼您可以建立用戶端，提供用戶端正確的認證，並且毫無後顧之憂地執行它。</span><span class="sxs-lookup"><span data-stu-id="789df-126">If you trust a source and have downloaded the client code and other metadata from that source's secure MEX endpoint, then you can build the client, supply it with the right credentials, and run it with no other concerns.</span></span>  
  
 <span data-ttu-id="789df-127">如果您選擇從您對它幾乎一無所知的來源下載用戶端和中繼資料，請務必驗證程式碼使用的安全性措施。</span><span class="sxs-lookup"><span data-stu-id="789df-127">However, if you elect to download a client and metadata from a source that you know little about, be sure to validate the security measures the code uses.</span></span> <span data-ttu-id="789df-128">例如，您不可以只建立傳送您的個人資料或財務資料到服務的用戶端，除非該服務僅要求機密性和完整性。</span><span class="sxs-lookup"><span data-stu-id="789df-128">For example, you must not simply create a client that sends your personal or financial information to a service unless the service demands confidentiality and integrity (at the very least).</span></span> <span data-ttu-id="789df-129">您應該將服務的擁有者信任至您願意洩漏這類資訊的範圍，因為這些資訊將會顯示給他們。</span><span class="sxs-lookup"><span data-stu-id="789df-129">You should trust the owner of the service to the extent that you are willing to disclose such information, because such information will be visible to them.</span></span>  
  
 <span data-ttu-id="789df-130">因此，通常在使用來自不受信任來源的程式碼和中繼資料時，請檢查程式碼和中繼資料，以確保其符合您要求的安全性等級。</span><span class="sxs-lookup"><span data-stu-id="789df-130">As a rule, therefore, when using code and metadata from an untrusted source, check the code and metadata to ensure that it meets the security level that you require.</span></span>  
  
## <a name="setting-a-client-credential"></a><span data-ttu-id="789df-131">設定用戶端認證</span><span class="sxs-lookup"><span data-stu-id="789df-131">Setting a Client Credential</span></span>  

 <span data-ttu-id="789df-132">在用戶端上設定用戶端認證是由兩個步驟所組成：</span><span class="sxs-lookup"><span data-stu-id="789df-132">Setting a client credential on a client consists of two steps:</span></span>  
  
1. <span data-ttu-id="789df-133">判斷服務需要的 *用戶端認證類型* 。</span><span class="sxs-lookup"><span data-stu-id="789df-133">Determine the *client credential type* the service requires.</span></span> <span data-ttu-id="789df-134">這可以由兩個方法的其中之一完成。</span><span class="sxs-lookup"><span data-stu-id="789df-134">This is accomplished by one of two methods.</span></span> <span data-ttu-id="789df-135">首先，如果您有來自服務建立者的文件，文件中應指出服務需要的用戶端認證類型 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="789df-135">First, if you have documentation from the service creator, it should specify the client credential type (if any) the service requires.</span></span> <span data-ttu-id="789df-136">再者，如果您只有 Svcutil.exe 工具產生的組態檔，您可以檢查個別的繫結來判斷需要哪一種認證類型。</span><span class="sxs-lookup"><span data-stu-id="789df-136">Second, if you have only a configuration file generated by the Svcutil.exe tool, you can examine the individual bindings to determine what credential type is required.</span></span>  
  
2. <span data-ttu-id="789df-137">指定實際的用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="789df-137">Specify an actual client credential.</span></span> <span data-ttu-id="789df-138">實際的用戶端認證稱為 *用戶端認證值* ，可區別其與類型。</span><span class="sxs-lookup"><span data-stu-id="789df-138">The actual client credential is called a *client credential value* to distinguish it from the type.</span></span> <span data-ttu-id="789df-139">例如，如果用戶端認證類型指定憑證，您必須提供由服務信任的憑證授權單位核發的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-139">For example, if the client credential type specifies a certificate, you must supply an X.509 certificate that is issued by a certification authority the service trusts.</span></span>  
  
### <a name="determining-the-client-credential-type"></a><span data-ttu-id="789df-140">判斷用戶端認證類型</span><span class="sxs-lookup"><span data-stu-id="789df-140">Determining the Client Credential Type</span></span>  

 <span data-ttu-id="789df-141">如果您有 Svcutil.exe 工具產生的設定檔，請檢查 [\<bindings>](../configure-apps/file-schema/wcf/bindings.md) 區段以判斷所需的用戶端認證類型。</span><span class="sxs-lookup"><span data-stu-id="789df-141">If you have the configuration file the Svcutil.exe tool generated, examine the [\<bindings>](../configure-apps/file-schema/wcf/bindings.md) section to determine what client credential type is required.</span></span> <span data-ttu-id="789df-142">在該部分內有指定安全性需要的繫結項目。</span><span class="sxs-lookup"><span data-stu-id="789df-142">Within the section are binding elements that specify the security requirements.</span></span> <span data-ttu-id="789df-143">具體而言，請檢查每個系結的 \<security> 元素。</span><span class="sxs-lookup"><span data-stu-id="789df-143">Specifically, examine the \<security> Element of each binding.</span></span> <span data-ttu-id="789df-144">該項目包括 `mode` 屬性，您可以將該屬性設定為三個可能值 (`Message`、`Transport` 或 `TransportWithMessageCredential`) 的其中之一。</span><span class="sxs-lookup"><span data-stu-id="789df-144">That element includes the `mode` attribute, which you can set to one of three possible values (`Message`, `Transport`, or `TransportWithMessageCredential`).</span></span> <span data-ttu-id="789df-145">屬性的值決定模式，而模式決定哪一個子項目是重要的。</span><span class="sxs-lookup"><span data-stu-id="789df-145">The value of the attribute determines the mode, and the mode determines which of the child elements is significant.</span></span>  
  
 <span data-ttu-id="789df-146">`<security>`元素可以包含 `<transport>` 或專案 `<message>` ，或兩者都包含。</span><span class="sxs-lookup"><span data-stu-id="789df-146">The `<security>` element can contain either a `<transport>` or `<message>` element, or both.</span></span> <span data-ttu-id="789df-147">重要的項目就是符合安全性模式的項目。</span><span class="sxs-lookup"><span data-stu-id="789df-147">The significant element is the one that matches the security mode.</span></span> <span data-ttu-id="789df-148">例如，下列程式碼指定安全性模式為 `"Message"`，而且 `<message>` 項目的用戶端認證類型是 `"Certificate"`。</span><span class="sxs-lookup"><span data-stu-id="789df-148">For example, the following code specifies that the security mode is `"Message"`, and the client credential type for the `<message>` element is `"Certificate"`.</span></span> <span data-ttu-id="789df-149">在這個情況中，可以忽略 `<transport>` 項目。</span><span class="sxs-lookup"><span data-stu-id="789df-149">In this case, the `<transport>` element can be ignored.</span></span> <span data-ttu-id="789df-150">但 `<message>` 項目指定必須提供 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-150">However, the `<message>` element specifies that an X.509 certificate must be supplied.</span></span>  

```xml  
<wsHttpBinding>  
    <binding name="WSHttpBinding_ICalculator">  
       <security mode="Message">  
           <transport clientCredentialType="Windows"
                      realm="" />  
           <message clientCredentialType="Certificate"
                    negotiateServiceCredential="true"  
                    algorithmSuite="Default"
                    establishSecurityContext="true" />  
       </security>  
    </binding>  
</wsHttpBinding>  
```  

 <span data-ttu-id="789df-151">請注意，如果 `clientCredentialType` 屬性已設定為 `"Windows"`，如下列範例所示，您不需要提供實際的認證值。</span><span class="sxs-lookup"><span data-stu-id="789df-151">Note that if the `clientCredentialType` attribute is set to `"Windows"`, as shown in the following example, you do not need to supply an actual credential value.</span></span> <span data-ttu-id="789df-152">這是因為 Windows 整合式安全性已提供執行用戶端之人員的實際認證 (Kerberos 權杖)。</span><span class="sxs-lookup"><span data-stu-id="789df-152">This is because the Windows integrated security provides the actual credential (a Kerberos token) of the person who is running the client.</span></span>  
  
```xml  
<security mode="Message">  
    <transport clientCredentialType="Windows "
        realm="" />  
</security>  
```  
  
### <a name="setting-the-client-credential-value"></a><span data-ttu-id="789df-153">設定用戶端認證值</span><span class="sxs-lookup"><span data-stu-id="789df-153">Setting the Client Credential Value</span></span>  

 <span data-ttu-id="789df-154">如果用戶端必須提供認證，請使用適當方法設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="789df-154">If it is determined that the client must supply a credential, use the appropriate method to configure the client.</span></span> <span data-ttu-id="789df-155">例如，使用 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 方法設定用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-155">For example, to set a client certificate, use the <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> method.</span></span>  
  
 <span data-ttu-id="789df-156">常見的認證形式是 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-156">A common form of credential is the X.509 certificate.</span></span> <span data-ttu-id="789df-157">您可以用兩種方式提供認證：</span><span class="sxs-lookup"><span data-stu-id="789df-157">You can supply the credential in two ways:</span></span>  
  
- <span data-ttu-id="789df-158">以程式設計方式將它編寫在您的用戶端程式碼中 (使用 `SetCertificate` 方法)。</span><span class="sxs-lookup"><span data-stu-id="789df-158">By programming it in your client code (using the `SetCertificate` method).</span></span>  
  
 <span data-ttu-id="789df-159">藉由 [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md) 為用戶端新增設定檔的區段，並使用 `clientCredentials` 元素 (如下所示) 。</span><span class="sxs-lookup"><span data-stu-id="789df-159">By adding a [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md) section of the configuration file for the client and using the `clientCredentials` element (shown below).</span></span>  
  
#### <a name="setting-a-clientcredentials-value-in-code"></a><span data-ttu-id="789df-160">在程式 \<clientCredentials> 代碼中設定值</span><span class="sxs-lookup"><span data-stu-id="789df-160">Setting a \<clientCredentials> Value in Code</span></span>  

 <span data-ttu-id="789df-161">若要 [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) 在程式碼中設定值，您必須存取 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 類別的屬性 <xref:System.ServiceModel.ClientBase%601> 。</span><span class="sxs-lookup"><span data-stu-id="789df-161">To set a [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) value in code, you must access the <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> property of the <xref:System.ServiceModel.ClientBase%601> class.</span></span> <span data-ttu-id="789df-162">該屬性傳回允許存取各種認證類型的 <xref:System.ServiceModel.Description.ClientCredentials> 物件，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="789df-162">The property returns a <xref:System.ServiceModel.Description.ClientCredentials> object that allows access to various credential types, as shown in the following table.</span></span>  
  
|<span data-ttu-id="789df-163">ClientCredential 屬性</span><span class="sxs-lookup"><span data-stu-id="789df-163">ClientCredential Property</span></span>|<span data-ttu-id="789df-164">描述</span><span class="sxs-lookup"><span data-stu-id="789df-164">Description</span></span>|<span data-ttu-id="789df-165">附註</span><span class="sxs-lookup"><span data-stu-id="789df-165">Notes</span></span>|  
|-------------------------------|-----------------|-----------|  
|<xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>|<span data-ttu-id="789df-166">傳回 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-166">Returns an <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential></span></span>|<span data-ttu-id="789df-167">代表用戶端向服務進行驗證時提供的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-167">Represents an X.509 certificate provided by the client to authenticate itself to the service.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>|<span data-ttu-id="789df-168">傳回 <xref:System.ServiceModel.Security.HttpDigestClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-168">Returns an <xref:System.ServiceModel.Security.HttpDigestClientCredential></span></span>|<span data-ttu-id="789df-169">代表 HTTP 摘要式認證。</span><span class="sxs-lookup"><span data-stu-id="789df-169">Represents an HTTP digest credential.</span></span> <span data-ttu-id="789df-170">此認證是使用者名稱與密碼的雜湊。</span><span class="sxs-lookup"><span data-stu-id="789df-170">The credential is a hash of the user name and password.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>|<span data-ttu-id="789df-171">傳回 <xref:System.ServiceModel.Security.IssuedTokenClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-171">Returns an <xref:System.ServiceModel.Security.IssuedTokenClientCredential></span></span>|<span data-ttu-id="789df-172">代表安全性權杖服務核發的自訂安全性權杖，常使用於聯合案例中。</span><span class="sxs-lookup"><span data-stu-id="789df-172">Represents a custom security token issued by a Security Token Service, commonly used in federation scenarios.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.Peer%2A>|<span data-ttu-id="789df-173">傳回 <xref:System.ServiceModel.Security.PeerCredential></span><span class="sxs-lookup"><span data-stu-id="789df-173">Returns a <xref:System.ServiceModel.Security.PeerCredential></span></span>|<span data-ttu-id="789df-174">代表用在 Windows 網域上參與對等網狀結構的對等認證。</span><span class="sxs-lookup"><span data-stu-id="789df-174">Represents a Peer credential for participation in a Peer mesh on a Windows domain.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>|<span data-ttu-id="789df-175">傳回 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-175">Returns an <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential></span></span>|<span data-ttu-id="789df-176">代表超出範圍交涉中的服務所提供的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="789df-176">Represents an X.509 certificate provided by the service in an out-of-band negotiation.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.UserName%2A>|<span data-ttu-id="789df-177">傳回 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-177">Returns a <xref:System.ServiceModel.Security.UserNamePasswordClientCredential></span></span>|<span data-ttu-id="789df-178">代表使用者名稱和密碼組。</span><span class="sxs-lookup"><span data-stu-id="789df-178">Represents a user name and password pair.</span></span>|  
|<xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>|<span data-ttu-id="789df-179">傳回 <xref:System.ServiceModel.Security.WindowsClientCredential></span><span class="sxs-lookup"><span data-stu-id="789df-179">Returns a <xref:System.ServiceModel.Security.WindowsClientCredential></span></span>|<span data-ttu-id="789df-180">代表 Windows 用戶端認證 (Kerberos 認證)。</span><span class="sxs-lookup"><span data-stu-id="789df-180">Represents a Windows client credential (a Kerberos credential).</span></span> <span data-ttu-id="789df-181">類別的屬性是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="789df-181">The properties of the class are read-only.</span></span>|  
  
#### <a name="setting-a-clientcredentials-value-in-configuration"></a><span data-ttu-id="789df-182">設定 \<clientCredentials> Configuration 中的值</span><span class="sxs-lookup"><span data-stu-id="789df-182">Setting a \<clientCredentials> Value in Configuration</span></span>  

 <span data-ttu-id="789df-183">認證值的指定方式是使用端點行為作為元素的子項目 [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) 。</span><span class="sxs-lookup"><span data-stu-id="789df-183">Credential values are specified by using an endpoint behavior as child elements of the [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) element.</span></span> <span data-ttu-id="789df-184">使用的項目視用戶端認證類型而定。</span><span class="sxs-lookup"><span data-stu-id="789df-184">The element used depends on the client credential type.</span></span> <span data-ttu-id="789df-185">例如，下列範例顯示使用 <設定 x.509 憑證的設定 [\<clientCertificate>](../configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md) 。</span><span class="sxs-lookup"><span data-stu-id="789df-185">For example, the following example shows the configuration to set an X.509 certificate using the <[\<clientCertificate>](../configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md).</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>
        <behavior name="myEndpointBehavior">  
          <clientCredentials>  
            <clientCertificate findvalue="myMachineName"
            storeLocation="Current" X509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>
      </endpointBehaviors>
    </behaviors>
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="789df-186">若要在設定中設定用戶端認證，請將 [\<endpointBehaviors>](../configure-apps/file-schema/wcf/endpointbehaviors.md) 元素新增至設定檔。</span><span class="sxs-lookup"><span data-stu-id="789df-186">To set the client credential in configuration, add an [\<endpointBehaviors>](../configure-apps/file-schema/wcf/endpointbehaviors.md) element to the configuration file.</span></span> <span data-ttu-id="789df-187">此外，新增的行為專案必須使用專案的 `behaviorConfiguration` 屬性（attribute [ \<endpoint> \<client> ](../configure-apps/file-schema/wcf/endpoint-of-client.md) ）連結至服務的端點，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="789df-187">Additionally, the added behavior element must be linked to the service's endpoint using the `behaviorConfiguration` attribute of the [\<endpoint> of \<client>](../configure-apps/file-schema/wcf/endpoint-of-client.md) element as shown in the following example.</span></span> <span data-ttu-id="789df-188">`behaviorConfiguration` 屬性的值必須與 `name` 屬性的值相符。</span><span class="sxs-lookup"><span data-stu-id="789df-188">The value of the `behaviorConfiguration` attribute must match the value of the behavior `name` attribute.</span></span>  

```xml
<configuration>
  <system.serviceModel>
    <client>
      <endpoint address="http://localhost/servicemodelsamples/service.svc"
                binding="wsHttpBinding"
                bindingConfiguration="Binding1"
                behaviorConfiguration="myEndpointBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </client>
  </system.serviceModel>
</configuration>
```
  
> [!NOTE]
> <span data-ttu-id="789df-189">使用應用程式組態檔無法設定某些用戶端認證值，例如使用者名稱和密碼，或者 Windows 使用者和密碼值。</span><span class="sxs-lookup"><span data-stu-id="789df-189">Some of the client credential values cannot be set using application configuration files, for example, user name and password, or Windows user and password values.</span></span> <span data-ttu-id="789df-190">這類認證值只能在程式碼中指定。</span><span class="sxs-lookup"><span data-stu-id="789df-190">Such credential values can be specified only in code.</span></span>  
  
 <span data-ttu-id="789df-191">如需設定用戶端認證的詳細資訊，請參閱 [如何：指定用戶端認證值](how-to-specify-client-credential-values.md)。</span><span class="sxs-lookup"><span data-stu-id="789df-191">For more information about setting the client credential, see [How to: Specify Client Credential Values](how-to-specify-client-credential-values.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="789df-192">`ClientCredentialType` 設定為 `SecurityMode` 時，會忽略 `"TransportWithMessageCredential",`，如下列範例組態所示。</span><span class="sxs-lookup"><span data-stu-id="789df-192">`ClientCredentialType` is ignored when `SecurityMode` is set to `"TransportWithMessageCredential",` as shown in the following sample configuration.</span></span>  
  
```xml  
<wsHttpBinding>  
    <binding name="PingBinding">  
        <security mode="TransportWithMessageCredential"  >  
           <message  clientCredentialType="UserName"
               establishSecurityContext="false"
               negotiateServiceCredential="false" />  
           <transport clientCredentialType="Certificate"  />  
         </security>  
    </binding>  
</wsHttpBinding>  
```  
  
## <a name="see-also"></a><span data-ttu-id="789df-193">另請參閱</span><span class="sxs-lookup"><span data-stu-id="789df-193">See also</span></span>

- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>
- <xref:System.ServiceModel.ClientBase%601>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>
- [\<bindings>](../configure-apps/file-schema/wcf/bindings.md)
- [<span data-ttu-id="789df-194">組態編輯器工具 (SvcConfigEditor.exe)</span><span class="sxs-lookup"><span data-stu-id="789df-194">Configuration Editor Tool (SvcConfigEditor.exe)</span></span>](configuration-editor-tool-svcconfigeditor-exe.md)
- [<span data-ttu-id="789df-195">保護服務的安全</span><span class="sxs-lookup"><span data-stu-id="789df-195">Securing Services</span></span>](securing-services.md)
- [<span data-ttu-id="789df-196">使用 WCF 用戶端存取服務</span><span class="sxs-lookup"><span data-stu-id="789df-196">Accessing Services Using a WCF Client</span></span>](accessing-services-using-a-wcf-client.md)
- [<span data-ttu-id="789df-197">作法：指定用戶端認證值</span><span class="sxs-lookup"><span data-stu-id="789df-197">How to: Specify Client Credential Values</span></span>](how-to-specify-client-credential-values.md)
- [<span data-ttu-id="789df-198">ServiceModel 中繼資料公用程式工具 (Svcutil.exe)</span><span class="sxs-lookup"><span data-stu-id="789df-198">ServiceModel Metadata Utility Tool (Svcutil.exe)</span></span>](servicemodel-metadata-utility-tool-svcutil-exe.md)
- [<span data-ttu-id="789df-199">作法：指定用戶端認證類型</span><span class="sxs-lookup"><span data-stu-id="789df-199">How to: Specify the Client Credential Type</span></span>](how-to-specify-the-client-credential-type.md)

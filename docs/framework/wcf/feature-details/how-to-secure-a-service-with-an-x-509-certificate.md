---
title: 作法：使用 X.509 憑證來確保服務安全
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
ms.openlocfilehash: bf498ee373f2d637a7a93fbc36225a38ff7744c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293893"
---
# <a name="how-to-secure-a-service-with-an-x509-certificate"></a><span data-ttu-id="456bb-102">作法：使用 X.509 憑證來確保服務安全</span><span class="sxs-lookup"><span data-stu-id="456bb-102">How to: Secure a Service with an X.509 Certificate</span></span>

<span data-ttu-id="456bb-103">使用 x.509 憑證保護服務是 Windows Communication Foundation (WCF) 使用的基本技術。</span><span class="sxs-lookup"><span data-stu-id="456bb-103">Securing a service with an X.509 certificate is a basic technique that most bindings in Windows Communication Foundation (WCF) use.</span></span> <span data-ttu-id="456bb-104">此主題會介紹使用 X.509 憑證設定自我主控服務的步驟。</span><span class="sxs-lookup"><span data-stu-id="456bb-104">This topic walks through the steps of configuring a self-hosted service with an X.509 certificate.</span></span>  
  
 <span data-ttu-id="456bb-105">必要條件是能夠用來驗證伺服器的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="456bb-105">A prerequisite is a valid certificate that can be used to authenticate the server.</span></span> <span data-ttu-id="456bb-106">憑證必須透過受信任的憑證授權單位發行至伺服器。</span><span class="sxs-lookup"><span data-stu-id="456bb-106">The certificate must be issued to the server by a trusted certificate authority.</span></span> <span data-ttu-id="456bb-107">如果憑證無效，任何嘗試使用服務的用戶端都不會信任該服務，因此無法建立連線。</span><span class="sxs-lookup"><span data-stu-id="456bb-107">If the certificate is not valid, any client trying to use the service will not trust the service, and consequently no connection will be made.</span></span> <span data-ttu-id="456bb-108">如需使用憑證的詳細資訊，請參閱使用 [憑證](working-with-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="456bb-108">For more information about using certificates, see [Working with Certificates](working-with-certificates.md).</span></span>  
  
### <a name="to-configure-a-service-with-a-certificate-using-code"></a><span data-ttu-id="456bb-109">使用程式碼搭配憑證設定服務</span><span class="sxs-lookup"><span data-stu-id="456bb-109">To configure a service with a certificate using code</span></span>  
  
1. <span data-ttu-id="456bb-110">建立服務合約以及實作的服務。</span><span class="sxs-lookup"><span data-stu-id="456bb-110">Create the service contract and the implemented service.</span></span> <span data-ttu-id="456bb-111">如需詳細資訊，請參閱 [設計和執行服務](../designing-and-implementing-services.md)。</span><span class="sxs-lookup"><span data-stu-id="456bb-111">For more information, see [Designing and Implementing Services](../designing-and-implementing-services.md).</span></span>  
  
2. <span data-ttu-id="456bb-112">建立 <xref:System.ServiceModel.WSHttpBinding> 類別的執行個體，並將其安全性模式設定為 <xref:System.ServiceModel.SecurityMode.Message>，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="456bb-112">Create an instance of the <xref:System.ServiceModel.WSHttpBinding> class and set its security mode to <xref:System.ServiceModel.SecurityMode.Message>, as shown in the following code.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3. <span data-ttu-id="456bb-113">建立兩個 <xref:System.Type> 變數，分別指派給合約類型以及已實作合約，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="456bb-113">Create two <xref:System.Type> variables, one each for the contract type and the implemented contract, as shown in the following code.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4. <span data-ttu-id="456bb-114">建立服務基底位址之 <xref:System.Uri> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="456bb-114">Create an instance of the <xref:System.Uri> class for the base address of the service.</span></span> <span data-ttu-id="456bb-115">因為 `WSHttpBinding` 使用 HTTP 傳輸，所以 (URI) 的統一資源識別項必須以該架構開頭，或 Windows Communication Foundation (WCF) 會在開啟服務時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="456bb-115">Because the `WSHttpBinding` uses the HTTP transport, the Uniform Resource Identifier (URI) must begin with that schema, or Windows Communication Foundation (WCF) will throw an exception when the service is opened.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5. <span data-ttu-id="456bb-116">使用已實作之合約類型變數與 URI 建立 <xref:System.ServiceModel.ServiceHost> 類別的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="456bb-116">Create a new instance of the <xref:System.ServiceModel.ServiceHost> class with the implemented contract type variable and the URI.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6. <span data-ttu-id="456bb-117">使用 <xref:System.ServiceModel.Description.ServiceEndpoint> 方法將 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 新增至服務。</span><span class="sxs-lookup"><span data-stu-id="456bb-117">Add a <xref:System.ServiceModel.Description.ServiceEndpoint> to the service using the <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> method.</span></span> <span data-ttu-id="456bb-118">將合約、繫結，以及端點位址傳遞給建構函式，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="456bb-118">Pass the contract, binding, and an endpoint address to the constructor, as shown in the following code.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7. <span data-ttu-id="456bb-119">選擇性。</span><span class="sxs-lookup"><span data-stu-id="456bb-119">Optional.</span></span> <span data-ttu-id="456bb-120">若要從服務擷取中繼資料，請建立新的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 物件並將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="456bb-120">To retrieve metadata from the service, create a new <xref:System.ServiceModel.Description.ServiceMetadataBehavior> object and set the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> property to `true`.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8. <span data-ttu-id="456bb-121">請使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 類別的 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 方法，將有效憑證新增至服務。</span><span class="sxs-lookup"><span data-stu-id="456bb-121">Use the <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> method of the <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> class to add the valid certificate to the service.</span></span> <span data-ttu-id="456bb-122">方法就可以使用其中一種方法尋找憑證。</span><span class="sxs-lookup"><span data-stu-id="456bb-122">The method can use one of several methods to find a certificate.</span></span> <span data-ttu-id="456bb-123">這個範例會使用 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectName> 列舉。</span><span class="sxs-lookup"><span data-stu-id="456bb-123">This example uses the <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectName> enumeration.</span></span> <span data-ttu-id="456bb-124">列舉會指定所提供的值，是憑證所發行至該實體的名稱。</span><span class="sxs-lookup"><span data-stu-id="456bb-124">The enumeration specifies that the supplied value is the name of the entity that the certificate was issued to.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. <span data-ttu-id="456bb-125">呼叫 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 方法啟動服務接聽。</span><span class="sxs-lookup"><span data-stu-id="456bb-125">Call the <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> method to start the service listening.</span></span> <span data-ttu-id="456bb-126">如果您建立主控台應用程式，請呼叫 <xref:System.Console.ReadLine%2A> 方法讓服務保持在接聽狀態。</span><span class="sxs-lookup"><span data-stu-id="456bb-126">If you are creating a console application, call the <xref:System.Console.ReadLine%2A> method to keep the service in the listening state.</span></span>  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="456bb-127">範例</span><span class="sxs-lookup"><span data-stu-id="456bb-127">Example</span></span>  

 <span data-ttu-id="456bb-128">下列程式碼範例會使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 方法，使用 X.509 憑證設定服務。</span><span class="sxs-lookup"><span data-stu-id="456bb-128">The following example uses the <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> method to configure a service with an X.509 certificate.</span></span>  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="456bb-129">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="456bb-129">Compiling the Code</span></span>  

 <span data-ttu-id="456bb-130">要編譯程式碼時，必須有下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="456bb-130">The following namespaces are required to compile the code:</span></span>  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.Web.Services.Description>  
  
- <xref:System.Security.Cryptography.X509Certificates>  
  
- <xref:System.Runtime.Serialization>  
  
## <a name="see-also"></a><span data-ttu-id="456bb-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="456bb-131">See also</span></span>

- [<span data-ttu-id="456bb-132">使用憑證</span><span class="sxs-lookup"><span data-stu-id="456bb-132">Working with Certificates</span></span>](working-with-certificates.md)

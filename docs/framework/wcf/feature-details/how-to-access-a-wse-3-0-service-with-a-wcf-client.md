---
title: HOW TO：使用 WCF 用戶端來存取 WSE 3.0 服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
ms.openlocfilehash: 179591c272685771fbde12e161cb38b1bd969052
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597198"
---
# <a name="how-to-access-a-wse-30-service-with-a-wcf-client"></a><span data-ttu-id="00eef-102">HOW TO：使用 WCF 用戶端來存取 WSE 3.0 服務</span><span class="sxs-lookup"><span data-stu-id="00eef-102">How to: Access a WSE 3.0 Service with a WCF Client</span></span>
<span data-ttu-id="00eef-103">在 WCF 用戶端設定為使用 WS-ADDRESSING 規格的8月2004版時，Windows Communication Foundation （WCF）用戶端的連線層級與適用于 Microsoft .NET 服務的 Web 服務增強功能（WSE）3.0 相容。</span><span class="sxs-lookup"><span data-stu-id="00eef-103">Windows Communication Foundation (WCF) clients are wire-level compatible with Web Services Enhancements (WSE) 3.0 for Microsoft .NET services when WCF clients are configured to use the August 2004 version of the WS-Addressing specification.</span></span> <span data-ttu-id="00eef-104">不過，WSE 3.0 服務不支援中繼資料交換（MEX）通訊協定，因此當您使用[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)來建立 wcf 用戶端類別時，安全性設定並不會套用至所產生的 wcf 用戶端。</span><span class="sxs-lookup"><span data-stu-id="00eef-104">However, WSE 3.0 services do not support the metadata exchange (MEX) protocol, so when you use the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to create a WCF client class, the security settings are not applied to the generated WCF client.</span></span> <span data-ttu-id="00eef-105">因此，在產生 WCF 用戶端之後，您必須指定 WSE 3.0 服務所需的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="00eef-105">Therefore, you must specify the security settings that the WSE 3.0 service requires after the WCF client is generated.</span></span>  
  
 <span data-ttu-id="00eef-106">您可以使用自訂系結來套用這些安全性設定，以將 wse 3.0 服務的需求，以及 WSE 3.0 服務和 WCF 用戶端之間的互通需求納入考慮。</span><span class="sxs-lookup"><span data-stu-id="00eef-106">You can apply these security settings by using a custom binding to take into account the WSE 3.0 service's requirements and the interoperable requirements between a WSE 3.0 service and a WCF client.</span></span> <span data-ttu-id="00eef-107">這些互通性需求包含上述的 WS-Addressing August 2004 規格使用和 WSE 3.0 預設訊息保護 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt>。</span><span class="sxs-lookup"><span data-stu-id="00eef-107">These interoperability requirements include the aforementioned use of the August 2004 WS-Addressing specification and the  WSE 3.0default message protection of <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt>.</span></span> <span data-ttu-id="00eef-108">WCF 的預設訊息保護是 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature> 。</span><span class="sxs-lookup"><span data-stu-id="00eef-108">The default message protection for WCF is <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature>.</span></span> <span data-ttu-id="00eef-109">本主題詳細說明如何建立與 WSE 3.0 服務互通的 WCF 系結。</span><span class="sxs-lookup"><span data-stu-id="00eef-109">This topic details how to create a WCF binding that interoperates with a WSE 3.0 service.</span></span> <span data-ttu-id="00eef-110">WCF 也提供併入此系結的範例。</span><span class="sxs-lookup"><span data-stu-id="00eef-110">WCF also provides a sample that incorporates this binding.</span></span> <span data-ttu-id="00eef-111">如需此範例的詳細資訊，請參閱[與 .Asmx Web 服務互](../samples/interoperating-with-asmx-web-services.md)操作。</span><span class="sxs-lookup"><span data-stu-id="00eef-111">For more information about this sample, see [Interoperating with ASMX Web Services](../samples/interoperating-with-asmx-web-services.md).</span></span>  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a><span data-ttu-id="00eef-112">若要使用 WCF 用戶端來存取 WSE 3.0 Web 服務</span><span class="sxs-lookup"><span data-stu-id="00eef-112">To access a WSE 3.0 Web service with a WCF client</span></span>  
  
1. <span data-ttu-id="00eef-113">執行[System.servicemodel 中繼資料公用程式工具（Svcutil .exe）](../servicemodel-metadata-utility-tool-svcutil-exe.md) ，為 WSE 3.0 Web 服務建立 WCF 用戶端。</span><span class="sxs-lookup"><span data-stu-id="00eef-113">Run the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to create a WCF client for the WSE 3.0 Web service.</span></span>  
  
     <span data-ttu-id="00eef-114">若為 WSE 3.0 Web 服務，則會建立 WCF 用戶端。</span><span class="sxs-lookup"><span data-stu-id="00eef-114">For a WSE 3.0 Web service, a WCF client is created.</span></span> <span data-ttu-id="00eef-115">因為 WSE 3.0 不支援 MEX 通訊協定，所以您無法使用此工具擷取 Web 服務的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="00eef-115">Because WSE 3.0 does not support the MEX protocol, you cannot use the tool to retrieve the security requirements for the Web service.</span></span> <span data-ttu-id="00eef-116">應用程式開發人員必須為用戶端加入安全性設定。</span><span class="sxs-lookup"><span data-stu-id="00eef-116">The application developer must add the security settings for the client.</span></span>  
  
     <span data-ttu-id="00eef-117">如需建立 WCF 用戶端的詳細資訊，請參閱[如何：建立用戶端](../how-to-create-a-wcf-client.md)。</span><span class="sxs-lookup"><span data-stu-id="00eef-117">For more information about creating a WCF client, see the [How to: Create a Client](../how-to-create-a-wcf-client.md).</span></span>  
  
2. <span data-ttu-id="00eef-118">建立類別，表示可與 WSE 3.0 Web 服務通訊的繫結。</span><span class="sxs-lookup"><span data-stu-id="00eef-118">Create a class that represents a binding that can communicate with WSE 3.0 Web services.</span></span>  
  
     <span data-ttu-id="00eef-119">下列類別是[與 WSE 互](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)操作的一部分：</span><span class="sxs-lookup"><span data-stu-id="00eef-119">The following class is part of the [Interoperating with WSE](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29) sample:</span></span>  
  
    1. <span data-ttu-id="00eef-120">建立從 <xref:System.ServiceModel.Channels.Binding> 類別衍生的類別。</span><span class="sxs-lookup"><span data-stu-id="00eef-120">Create a class that derives from the <xref:System.ServiceModel.Channels.Binding> class.</span></span>  
  
         <span data-ttu-id="00eef-121">下列程式碼範例會建立一個名為 `WseHttpBinding` 的類別，此類別衍生自 <xref:System.ServiceModel.Channels.Binding> 類別。</span><span class="sxs-lookup"><span data-stu-id="00eef-121">The following code example creates a class named `WseHttpBinding` that derives from the <xref:System.ServiceModel.Channels.Binding> class.</span></span>  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2. <span data-ttu-id="00eef-122">將屬性加入至類別，這些屬性會指定 WSE 服務所使用的 WSE 通行判斷提示 (Turnkey Assertion)、是否需要衍生金鑰、是否使用安全工作階段、是否需要簽章確認，以及訊息保護設定。</span><span class="sxs-lookup"><span data-stu-id="00eef-122">Add properties to the class that specify the WSE turnkey assertion used by the WSE service, whether derived keys are required, whether secure sessions are used, whether signature confirmations are required, and the message protection settings.</span></span> <span data-ttu-id="00eef-123">在 WSE 3.0 中，通行判斷提示會指定用戶端或 Web 服務的安全性需求，類似于 WCF 中的系結驗證模式。</span><span class="sxs-lookup"><span data-stu-id="00eef-123">In WSE 3.0, a turnkey assertion specifies the security requirements for a client or Web service—similar to the authentication mode of a binding in WCF.</span></span>  
  
         <span data-ttu-id="00eef-124">下列程式碼範例會定義 `SecurityAssertion`、`RequireDerivedKeys`、`EstablishSecurityContext` 和 `MessageProtectionOrder` 屬性，這些屬性會分別指定 WSE 通行判斷提示、是否需要衍生金鑰、是否使用安全工作階段、是否需要簽章確認，以及訊息保護設定。</span><span class="sxs-lookup"><span data-stu-id="00eef-124">The following code example defines the `SecurityAssertion`, `RequireDerivedKeys`, `EstablishSecurityContext`, and `MessageProtectionOrder` properties that specify the WSE turnkey assertion, whether derived keys are required, whether secure sessions are used, whether signature confirmations are required, and the message protection settings, respectively.</span></span>  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3. <span data-ttu-id="00eef-125">覆寫 <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> 方法來設定繫結屬性。</span><span class="sxs-lookup"><span data-stu-id="00eef-125">Override the <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> method to set the binding properties.</span></span>  
  
         <span data-ttu-id="00eef-126">下列程式碼範例會藉由取得 `SecurityAssertion` 和 `MessageProtectionOrder` 屬性的值，指定傳輸、訊息編碼和訊息保護設定。</span><span class="sxs-lookup"><span data-stu-id="00eef-126">The following code example specifies the transport, message encoding, and message protection settings by getting the values of the `SecurityAssertion` and `MessageProtectionOrder` properties.</span></span>  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3. <span data-ttu-id="00eef-127">在用戶端應用程式程式碼中，加入程式碼以設定繫結屬性。</span><span class="sxs-lookup"><span data-stu-id="00eef-127">In the client application code, add code to set the binding properties.</span></span>  
  
     <span data-ttu-id="00eef-128">下列程式碼範例會指定 WCF 用戶端必須使用訊息保護和驗證，如 WSE 3.0 通行安全性判斷提示所定義 `AnonymousForCertificate` 。</span><span class="sxs-lookup"><span data-stu-id="00eef-128">The following code example specifies that the WCF client must use message protection and authentication as defined by the WSE 3.0 `AnonymousForCertificate` turnkey security assertion.</span></span> <span data-ttu-id="00eef-129">此外，也需要安全工作階段和衍生金鑰。</span><span class="sxs-lookup"><span data-stu-id="00eef-129">Additionally, secure sessions and derived keys are required.</span></span>  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a><span data-ttu-id="00eef-130">範例</span><span class="sxs-lookup"><span data-stu-id="00eef-130">Example</span></span>  
 <span data-ttu-id="00eef-131">下列程式碼範例會定義自訂的繫結，此繫結會公開 WSE 3.0 通行安全性判斷提示屬性的對應屬性。</span><span class="sxs-lookup"><span data-stu-id="00eef-131">The following code example defines a custom binding that exposes properties that correspond to the properties of a WSE 3.0 turnkey security assertion.</span></span> <span data-ttu-id="00eef-132">該自訂系結（名為 `WseHttpBinding` ）接著會用來指定與 WSSECURITYANONYMOUS WSE 3.0 快速入門範例通訊之 WCF 用戶端的系結屬性。</span><span class="sxs-lookup"><span data-stu-id="00eef-132">That custom binding, which is named `WseHttpBinding`, is then used to specify the binding properties for a WCF client that communicates with the WSSecurityAnonymous WSE 3.0 QuickStart sample.</span></span>  

## <a name="see-also"></a><span data-ttu-id="00eef-133">請參閱</span><span class="sxs-lookup"><span data-stu-id="00eef-133">See also</span></span>

- <xref:System.ServiceModel.Channels.Binding>
- [<span data-ttu-id="00eef-134">與 WSE 交互操作</span><span class="sxs-lookup"><span data-stu-id="00eef-134">Interoperating with WSE</span></span>](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)

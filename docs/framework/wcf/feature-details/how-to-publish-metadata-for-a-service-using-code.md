---
title: HOW TO：使用程式碼發行服務的中繼資料
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 51407e6d-4d87-42d5-be7c-9887b8652006
ms.openlocfilehash: db6bca8728789879f9bfea40904bfc80352d1dbe
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144912"
---
# <a name="how-to-publish-metadata-for-a-service-using-code"></a><span data-ttu-id="8d637-102">HOW TO：使用程式碼發行服務的中繼資料</span><span class="sxs-lookup"><span data-stu-id="8d637-102">How to: Publish Metadata for a Service Using Code</span></span>
<span data-ttu-id="8d637-103">這是討論 Windows Communication Foundation （WCF）服務發行中繼資料的兩個 how to 主題之一。</span><span class="sxs-lookup"><span data-stu-id="8d637-103">This is one of two how-to topics that discuss publishing metadata for a Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="8d637-104">有兩種方法可以指定服務發行中繼資料的方式，分別是使用組態檔和使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d637-104">There are two ways to specify how a service should publish metadata, using a configuration file and using code.</span></span> <span data-ttu-id="8d637-105">本主題說明如何使用程式碼發行服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-105">This topic shows how to publish metadata for a service using a code.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="8d637-106">本主題將示範以不安全的方法發行中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-106">This topic shows how to publish metadata in an unsecure manner.</span></span> <span data-ttu-id="8d637-107">任何用戶端都能從服務擷取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-107">Any client can retrieve the metadata from the service.</span></span> <span data-ttu-id="8d637-108">若您的服務需要以安全的方法發行中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-108">If you require your service to publish metadata in a secure manner.</span></span> <span data-ttu-id="8d637-109">請參閱[自訂安全中繼資料端點](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="8d637-109">see [Custom Secure Metadata Endpoint](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md).</span></span>  
  
 <span data-ttu-id="8d637-110">如需在設定檔案中發行中繼資料的詳細資訊，請參閱[如何：使用設定檔發行服務的中繼資料](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="8d637-110">For more information about publishing metadata in a configuration file, see [How to: Publish Metadata for a Service Using a Configuration File](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md).</span></span> <span data-ttu-id="8d637-111">發行中繼資料可讓用戶端透過 WS-Transfer GET 要求，或是透過使用 `?wsdl` 查詢字串的 HTTP/GET 要求來擷取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-111">Publishing metadata allows clients to retrieve the metadata using a WS-Transfer GET request or an HTTP/GET request using the `?wsdl` query string.</span></span> <span data-ttu-id="8d637-112">若要確定程式碼可以運作，您必須建立基本的 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="8d637-112">To be sure that the code is working you must create a basic WCF service.</span></span> <span data-ttu-id="8d637-113">下列程式碼提供您基本的自我裝載服務。</span><span class="sxs-lookup"><span data-stu-id="8d637-113">A basic self-hosted service is provided in the following code.</span></span>  
  
 [!code-csharp[htPublishMetadataCode#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#0)]
 [!code-vb[htPublishMetadataCode#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#0)]  
  
### <a name="to-publish-metadata-in-code"></a><span data-ttu-id="8d637-114">若要透過程式碼發行中繼資料</span><span class="sxs-lookup"><span data-stu-id="8d637-114">To publish metadata in code</span></span>  
  
1. <span data-ttu-id="8d637-115">在主控台應用程式的 main 方法中，傳入服務類型與基底位址來產生 <xref:System.ServiceModel.ServiceHost> 物件。</span><span class="sxs-lookup"><span data-stu-id="8d637-115">Within the main method of a console application, instantiate a <xref:System.ServiceModel.ServiceHost> object by passing in the service type and the base address.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#1)]
     [!code-vb[htPublishMetadataCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#1)]  
  
2. <span data-ttu-id="8d637-116">在步驟 1 的程式碼底下，立即建立 try 區塊，以便在執行服務時，攔截任何擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8d637-116">Create a try block immediately below the code for step 1, this catches any exceptions that get thrown while the service is running.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#2)]
     [!code-vb[htPublishMetadataCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#2)]  
  
     [!code-csharp[htPublishMetadataCode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#3)]
     [!code-vb[htPublishMetadataCode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#3)]  
  
3. <span data-ttu-id="8d637-117">檢查服務主機是否已包含 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>，如果沒有的話，建立新的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8d637-117">Check to see whether the service host already contains a <xref:System.ServiceModel.Description.ServiceMetadataBehavior>, if not, create a new <xref:System.ServiceModel.Description.ServiceMetadataBehavior> instance.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#4)]
     [!code-vb[htPublishMetadataCode#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#4)]  
  
4. <span data-ttu-id="8d637-118">將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 屬性設定為 `true.`</span><span class="sxs-lookup"><span data-stu-id="8d637-118">Set the <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> property to `true.`</span></span>  
  
     [!code-csharp[htPublishMetadataCode#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#5)]
     [!code-vb[htPublishMetadataCode#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#5)]  
  
5. <span data-ttu-id="8d637-119"><xref:System.ServiceModel.Description.ServiceMetadataBehavior> 會包含 <xref:System.ServiceModel.Description.MetadataExporter> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d637-119">The <xref:System.ServiceModel.Description.ServiceMetadataBehavior> contains a <xref:System.ServiceModel.Description.MetadataExporter> property.</span></span> <span data-ttu-id="8d637-120"><xref:System.ServiceModel.Description.MetadataExporter> 會包含 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d637-120">The <xref:System.ServiceModel.Description.MetadataExporter> contains a <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> property.</span></span> <span data-ttu-id="8d637-121">將 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性值設定為 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>。</span><span class="sxs-lookup"><span data-stu-id="8d637-121">Set the value of the <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> property to <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>.</span></span> <span data-ttu-id="8d637-122"><xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性也可以設為 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>。</span><span class="sxs-lookup"><span data-stu-id="8d637-122">The <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> property can also be set to <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>.</span></span> <span data-ttu-id="8d637-123">當設定為時 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> ，中繼資料匯出工具會使用「符合 WS-原則1.5」的中繼資料來產生原則資訊。</span><span class="sxs-lookup"><span data-stu-id="8d637-123">When set to <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> the metadata exporter generates policy information with the metadata that" conforms to WS-Policy 1.5.</span></span> <span data-ttu-id="8d637-124">一旦設為 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>，中繼資料匯出工具會產生符合 WS-Policy 1.2 的原則資訊。</span><span class="sxs-lookup"><span data-stu-id="8d637-124">When set to <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A> the metadata exporter generates policy information that conforms to WS-Policy 1.2.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#6)]
     [!code-vb[htPublishMetadataCode#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#6)]  
  
6. <span data-ttu-id="8d637-125">將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 執行個體新增至服務主機的行為集合中。</span><span class="sxs-lookup"><span data-stu-id="8d637-125">Add the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> instance to the service host's behaviors collection.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#7)]
     [!code-vb[htPublishMetadataCode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#7)]  
  
7. <span data-ttu-id="8d637-126">將中繼資料交換端點新增至服務主機。</span><span class="sxs-lookup"><span data-stu-id="8d637-126">Add the metadata exchange endpoint to the service host.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#8)]
     [!code-vb[htPublishMetadataCode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#8)]  
  
8. <span data-ttu-id="8d637-127">將應用程式端點新增至服務主機。</span><span class="sxs-lookup"><span data-stu-id="8d637-127">Add an application endpoint to the service host.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#9)]
     [!code-vb[htPublishMetadataCode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#9)]  
  
    > [!NOTE]
    > <span data-ttu-id="8d637-128">如果您沒有將任何端點加入至服務中，執行階段會為您加入預設端點。</span><span class="sxs-lookup"><span data-stu-id="8d637-128">If you do not add any endpoints to the service, the runtime adds default endpoints for you.</span></span> <span data-ttu-id="8d637-129">在這個範例中，由於服務將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 設定為 `true`，表示服務已啟用中繼資料發行。</span><span class="sxs-lookup"><span data-stu-id="8d637-129">In this example, because the service has a <xref:System.ServiceModel.Description.ServiceMetadataBehavior> set to `true`, the service has publishing metadata enabled.</span></span> <span data-ttu-id="8d637-130">如需預設端點的詳細資訊，請參閱[簡化](../../../../docs/framework/wcf/simplified-configuration.md)的設定和[WCF 服務的簡化](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)設定。</span><span class="sxs-lookup"><span data-stu-id="8d637-130">For more information about default endpoints, see [Simplified Configuration](../../../../docs/framework/wcf/simplified-configuration.md) and [Simplified Configuration for WCF Services](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).</span></span>  
  
9. <span data-ttu-id="8d637-131">開啟服務主機並等候傳入呼叫。</span><span class="sxs-lookup"><span data-stu-id="8d637-131">Open the service host and wait for incoming calls.</span></span> <span data-ttu-id="8d637-132">當使用者按下 ENTER 鍵時，關閉服務主機。</span><span class="sxs-lookup"><span data-stu-id="8d637-132">When the user presses ENTER, close the service host.</span></span>  
  
     [!code-csharp[htPublishMetadataCode#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#10)]
     [!code-vb[htPublishMetadataCode#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#10)]  
  
10. <span data-ttu-id="8d637-133">建置並執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d637-133">Build and run the console application.</span></span>  
  
11. <span data-ttu-id="8d637-134">使用 Internet Explorer 流覽至服務的基底位址（ `http://localhost:8001/MetadataSample` 在此範例中為），並確認已開啟中繼資料發佈。</span><span class="sxs-lookup"><span data-stu-id="8d637-134">Use Internet Explorer to browse to the base address of the service (`http://localhost:8001/MetadataSample` in this sample) and verify that the metadata publishing is turned on.</span></span> <span data-ttu-id="8d637-135">您應該會看到頁面上方標示「簡易服務」，且在其下跟著「您已建立服務」的網頁。</span><span class="sxs-lookup"><span data-stu-id="8d637-135">You should see a Web page displayed that says "Simple Service" at the top and immediately below "You have created a service."</span></span> <span data-ttu-id="8d637-136">如果沒有的話，結果頁面上方應該會顯示：「為此服務發行的中繼資料目前停用」。</span><span class="sxs-lookup"><span data-stu-id="8d637-136">If not, a message at the top of the resulting page displays: "Metadata publishing for this service is currently disabled."</span></span>  
  
## <a name="example"></a><span data-ttu-id="8d637-137">範例</span><span class="sxs-lookup"><span data-stu-id="8d637-137">Example</span></span>  
 <span data-ttu-id="8d637-138">下列程式碼範例示範如何執行基本 WCF 服務，以在程式碼中發行服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8d637-138">The following code example shows the implementation of a basic WCF service that publishes metadata for the service in code.</span></span>  
  
 [!code-csharp[htPublishMetadataCode#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#11)]
 [!code-vb[htPublishMetadataCode#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#11)]  
  
## <a name="see-also"></a><span data-ttu-id="8d637-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8d637-139">See also</span></span>

- [<span data-ttu-id="8d637-140">如何：於受管理的應用程式中裝載 WCF 服務</span><span class="sxs-lookup"><span data-stu-id="8d637-140">How to: Host a WCF Service in a Managed Application</span></span>](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)
- [<span data-ttu-id="8d637-141">自我裝載</span><span class="sxs-lookup"><span data-stu-id="8d637-141">Self-Host</span></span>](../../../../docs/framework/wcf/samples/self-host.md)
- [<span data-ttu-id="8d637-142">中繼資料架構概觀</span><span class="sxs-lookup"><span data-stu-id="8d637-142">Metadata Architecture Overview</span></span>](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
- [<span data-ttu-id="8d637-143">使用中繼資料</span><span class="sxs-lookup"><span data-stu-id="8d637-143">Using Metadata</span></span>](../../../../docs/framework/wcf/feature-details/using-metadata.md)
- [<span data-ttu-id="8d637-144">HOW TO：使用組態檔發行服務的中繼資料</span><span class="sxs-lookup"><span data-stu-id="8d637-144">How to: Publish Metadata for a Service Using a Configuration File</span></span>](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)

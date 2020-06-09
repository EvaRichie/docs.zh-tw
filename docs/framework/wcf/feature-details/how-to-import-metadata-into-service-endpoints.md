---
title: HOW TO：將中繼資料匯入服務端點
ms.date: 03/30/2017
ms.assetid: b69dbe20-92a1-4911-89d8-ffbc3dad4663
ms.openlocfilehash: 1de316b8e91739d5e3e24ff960e2cdfb33cc7fab
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597055"
---
# <a name="how-to-import-metadata-into-service-endpoints"></a><span data-ttu-id="0f1c5-102">HOW TO：將中繼資料匯入服務端點</span><span class="sxs-lookup"><span data-stu-id="0f1c5-102">How to: Import Metadata into Service Endpoints</span></span>
<span data-ttu-id="0f1c5-103">本主題說明如何將中繼資料匯入服務端點的集合，並使用在[消費者入門](../samples/getting-started-sample.md)中定義的服務。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-103">This topic explains how to import metadata into a collection of service endpoints and use the service defined in the [Getting Started](../samples/getting-started-sample.md).</span></span> <span data-ttu-id="0f1c5-104">本主題將示範如何建立用戶端應用程式，從服務匯入中繼資料，然後在服務上呼叫 `Add` 方法。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-104">This topic show how to create a client application that imports metadata from the service and then calls the `Add` method on the service.</span></span>  
  
### <a name="to-import-metadata-into-service-endpoints"></a><span data-ttu-id="0f1c5-105">將中繼資料匯入服務端點</span><span class="sxs-lookup"><span data-stu-id="0f1c5-105">To import metadata into service endpoints</span></span>  
  
1. <span data-ttu-id="0f1c5-106">請宣告 <xref:System.ServiceModel.EndpointAddress> 物件，並使用服務之中繼資料交換 (MEX) 位址的統一資源識別元 (URI) 來初始化該物件。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-106">Declare an <xref:System.ServiceModel.EndpointAddress> object and initialize it with the Uniform Resource Identifier (URI) for the metadata exchange (MEX) address of the service.</span></span>  
  
     [!code-csharp[UE_ImportMetadata#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#0)]  
  
2. <span data-ttu-id="0f1c5-107">建立 <xref:System.ServiceModel.Description.MetadataExchangeClient>，在 MEX 位址中傳遞，然後呼叫 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-107">Create a <xref:System.ServiceModel.Description.MetadataExchangeClient>, passing in the MEX address, and call <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>.</span></span> <span data-ttu-id="0f1c5-108">這會從服務擷取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-108">This retrieves the metadata from the service.</span></span>  
  
     [!code-csharp[UE_ImportMetadata#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#1)]  
  
3. <span data-ttu-id="0f1c5-109">建立 <xref:System.ServiceModel.Description.WsdlImporter>，在先前擷取的中繼資料中傳遞，然後呼叫 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-109">Create a <xref:System.ServiceModel.Description.WsdlImporter>, passing in the metadata previously retrieved, and call <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>.</span></span> <span data-ttu-id="0f1c5-110">這會產生 <xref:System.ServiceModel.Description.ContractDescription> 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-110">This generates a collection of <xref:System.ServiceModel.Description.ContractDescription> objects.</span></span> <span data-ttu-id="0f1c5-111">您也可以呼叫 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A> 或 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>，視您的需要而定。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-111">You could also call <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A> or <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>, depending upon your needs.</span></span>  
  
     [!code-csharp[UE_ImportMetadata#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#2)]  
  
    > [!NOTE]
    > <span data-ttu-id="0f1c5-112">在您匯入中繼資料之後，將無法建立用戶端通道或匯出中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-112">After you have imported the metadata, you will not be able to create a client channel or export the metadata.</span></span> <span data-ttu-id="0f1c5-113">這是因為此時沒有可用的型別資訊。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-113">This is because no type information is available at this point.</span></span> <span data-ttu-id="0f1c5-114">實際與服務互動或匯出中繼資料需要型別資訊。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-114">Type information is required to actually interact with the service or export metadata.</span></span> <span data-ttu-id="0f1c5-115">如果要產生型別資訊，您需要產生程式碼，如步驟 4 和 5 中所示。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-115">To generate the type information, you need to generate code, shown in steps 4 and 5.</span></span> <span data-ttu-id="0f1c5-116">或者，您可以使用 <xref:System.ServiceModel.Description.MetadataResolver> 協助程式類別。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-116">Alternatively, you could use the <xref:System.ServiceModel.Description.MetadataResolver> helper class.</span></span> <span data-ttu-id="0f1c5-117">如需詳細資訊，請參閱[如何：使用 MetadataResolver 來動態取得系結中繼資料](how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-117">For more information, see [How to: Use MetadataResolver to Obtain Binding Metadata Dynamically](how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md).</span></span>  
  
4. <span data-ttu-id="0f1c5-118">產生各個合約的型別資訊。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-118">Generate type information for each contract.</span></span>  
  
     [!code-csharp[UE_ImportMetadata#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#3)]  
  
5. <span data-ttu-id="0f1c5-119">現在您可以使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-119">Now you can use this information.</span></span> <span data-ttu-id="0f1c5-120">下列範例會產生 C# 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="0f1c5-120">The following sample generates C# source code.</span></span>  
  
     [!code-csharp[UE_ImportMetadata#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#4)]  
  
## <a name="see-also"></a><span data-ttu-id="0f1c5-121">請參閱</span><span class="sxs-lookup"><span data-stu-id="0f1c5-121">See also</span></span>

- [<span data-ttu-id="0f1c5-122">中繼資料</span><span class="sxs-lookup"><span data-stu-id="0f1c5-122">Metadata</span></span>](metadata.md)
- [<span data-ttu-id="0f1c5-123">快速入門</span><span class="sxs-lookup"><span data-stu-id="0f1c5-123">Getting Started</span></span>](../samples/getting-started-sample.md)

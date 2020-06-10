---
title: HOW TO：使用程式碼發行服務的中繼資料
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 51407e6d-4d87-42d5-be7c-9887b8652006
ms.openlocfilehash: 9239e8bd9b85986d41006c4b2a21b6f2304e8275
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601227"
---
# <a name="how-to-publish-metadata-for-a-service-using-code"></a>HOW TO：使用程式碼發行服務的中繼資料
這是討論 Windows Communication Foundation （WCF）服務發行中繼資料的兩個 how to 主題之一。 有兩種方法可以指定服務發行中繼資料的方式，分別是使用組態檔和使用程式碼。 本主題說明如何使用程式碼發行服務的中繼資料。  
  
> [!CAUTION]
> 本主題將示範以不安全的方法發行中繼資料。 任何用戶端都能從服務擷取中繼資料。 若您的服務需要以安全的方法發行中繼資料。 請參閱[自訂安全中繼資料端點](../samples/custom-secure-metadata-endpoint.md)。  
  
 如需在設定檔案中發行中繼資料的詳細資訊，請參閱[如何：使用設定檔發行服務的中繼資料](how-to-publish-metadata-for-a-service-using-a-configuration-file.md)。 發行中繼資料可讓用戶端透過 WS-Transfer GET 要求，或是透過使用 `?wsdl` 查詢字串的 HTTP/GET 要求來擷取中繼資料。 若要確定程式碼可以運作，您必須建立基本的 WCF 服務。 下列程式碼提供您基本的自我裝載服務。  
  
 [!code-csharp[htPublishMetadataCode#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#0)]
 [!code-vb[htPublishMetadataCode#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#0)]  
  
### <a name="to-publish-metadata-in-code"></a>若要透過程式碼發行中繼資料  
  
1. 在主控台應用程式的 main 方法中，傳入服務類型與基底位址來產生 <xref:System.ServiceModel.ServiceHost> 物件。  
  
     [!code-csharp[htPublishMetadataCode#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#1)]
     [!code-vb[htPublishMetadataCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#1)]  
  
2. 在步驟 1 的程式碼底下，立即建立 try 區塊，以便在執行服務時，攔截任何擲回的例外狀況。  
  
     [!code-csharp[htPublishMetadataCode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#2)]
     [!code-vb[htPublishMetadataCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#2)]  
  
     [!code-csharp[htPublishMetadataCode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#3)]
     [!code-vb[htPublishMetadataCode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#3)]  
  
3. 檢查服務主機是否已包含 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>，如果沒有的話，建立新的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 執行個體。  
  
     [!code-csharp[htPublishMetadataCode#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#4)]
     [!code-vb[htPublishMetadataCode#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#4)]  
  
4. 將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 屬性設定為 `true.`  
  
     [!code-csharp[htPublishMetadataCode#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#5)]
     [!code-vb[htPublishMetadataCode#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#5)]  
  
5. <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 會包含 <xref:System.ServiceModel.Description.MetadataExporter> 屬性。 <xref:System.ServiceModel.Description.MetadataExporter> 會包含 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性。 將 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性值設定為 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>。 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 屬性也可以設為 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>。 當設定為時 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> ，中繼資料匯出工具會使用「符合 WS-原則1.5」的中繼資料來產生原則資訊。 一旦設為 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>，中繼資料匯出工具會產生符合 WS-Policy 1.2 的原則資訊。  
  
     [!code-csharp[htPublishMetadataCode#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#6)]
     [!code-vb[htPublishMetadataCode#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#6)]  
  
6. 將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 執行個體新增至服務主機的行為集合中。  
  
     [!code-csharp[htPublishMetadataCode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#7)]
     [!code-vb[htPublishMetadataCode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#7)]  
  
7. 將中繼資料交換端點新增至服務主機。  
  
     [!code-csharp[htPublishMetadataCode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#8)]
     [!code-vb[htPublishMetadataCode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#8)]  
  
8. 將應用程式端點新增至服務主機。  
  
     [!code-csharp[htPublishMetadataCode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#9)]
     [!code-vb[htPublishMetadataCode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#9)]  
  
    > [!NOTE]
    > 如果您沒有將任何端點加入至服務中，執行階段會為您加入預設端點。 在這個範例中，由於服務將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 設定為 `true`，表示服務已啟用中繼資料發行。 如需預設端點的詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定和[WCF 服務的簡化](../samples/simplified-configuration-for-wcf-services.md)設定。  
  
9. 開啟服務主機並等候傳入呼叫。 當使用者按下 ENTER 鍵時，關閉服務主機。  
  
     [!code-csharp[htPublishMetadataCode#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#10)]
     [!code-vb[htPublishMetadataCode#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#10)]  
  
10. 建置並執行主控台應用程式。  
  
11. 使用 Internet Explorer 流覽至服務的基底位址（ `http://localhost:8001/MetadataSample` 在此範例中為），並確認已開啟中繼資料發佈。 您應該會看到頁面上方標示「簡易服務」，且在其下跟著「您已建立服務」的網頁。 如果沒有的話，結果頁面上方應該會顯示：「為此服務發行的中繼資料目前停用」。  
  
## <a name="example"></a>範例  
 下列程式碼範例示範如何執行基本 WCF 服務，以在程式碼中發行服務的中繼資料。  
  
 [!code-csharp[htPublishMetadataCode#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#11)]
 [!code-vb[htPublishMetadataCode#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#11)]  
  
## <a name="see-also"></a>請參閱

- [如何：於受管理的應用程式中裝載 WCF 服務](../how-to-host-a-wcf-service-in-a-managed-application.md)
- [自我裝載](../samples/self-host.md)
- [中繼資料架構概觀](metadata-architecture-overview.md)
- [使用中繼資料](using-metadata.md)
- [HOW TO：使用組態檔發行服務的中繼資料](how-to-publish-metadata-for-a-service-using-a-configuration-file.md)

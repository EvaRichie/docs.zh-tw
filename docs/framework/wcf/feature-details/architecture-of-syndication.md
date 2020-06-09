---
title: 新聞訂閱架構
ms.date: 03/30/2017
ms.assetid: ed4ca86e-e3d8-4acb-87aa-1921fbc353be
ms.openlocfilehash: 718778993a953ae819a2bee5a4a050a81d3a4b84
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587517"
---
# <a name="architecture-of-syndication"></a>新聞訂閱架構
新聞訂閱 API 主要是提供格式中性的程式設計模型，以便在網路上透過各種格式來撰寫新聞訂閱內容。 抽象資料模型包含下列類別：  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 這些類別可緊密地對應至 Atom 1.0 規格中所定義的建構 (儘管其中有些名稱不同)。  
  
 在 Windows Communication Foundation （WCF）中，新聞訂閱摘要會模型化為另一種服務作業類型，其中傳回類型是的其中一個衍生類別 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 。 摘要的擷取會被模型化為要求-回應訊息交換。 用戶端會將要求傳送至服務，並由服務回應。 要求訊息是在基礎結構通訊協定 (例如，原始 HTTP) 上設置，而回應訊息則包含常用新聞訂閱格式 (RSS 2.0 或 Atom 1.0) 的承載。 可實作這些訊息交換的服務，稱為新聞訂閱服務。  
  
 新聞訂閱服務合約包含一組可傳回 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 類別執行個體的作業。 下列範例示範新聞訂閱服務的介面宣告。  
  
 [!code-csharp[S_UE_SyndicationBoth#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_syndicationboth/cs/service.cs#0)]  
  
 新聞訂閱支援是以 WCF REST 程式設計模型為基礎，它會定義系結，此系結 <xref:System.ServiceModel.WebHttpBinding> 會與搭配使用， <xref:System.ServiceModel.Description.WebHttpBehavior> 以提供可做為服務的摘要。 如需 WCF REST 程式設計模型的詳細資訊，請參閱[Wcf WEB HTTP 程式設計模型總覽](wcf-web-http-programming-model-overview.md)。  
  
> [!NOTE]
> Atom 1.0 規格允許在其任何日期建構中指定小數秒數。 序列化和還原序列化 WCF 執行時，會忽略小數秒數。  
  
## <a name="object-model"></a>物件模型  
 新聞訂閱的物件模型包含下表中的類別群組。  
  
 格式化類別：  
  
|類別|描述|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationFeed> 執行個體序列化為 Atom 1.0 格式。|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationFeed> 衍生類別序列化為 Atom 1.0 格式。|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationItem> 執行個體序列化為 Atom 1.0 格式。|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationItem> 衍生類別序列化為 Atom 1.0 格式。|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationFeed> 執行個體序列化為 RSS 2.0 格式。|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationFeed> 衍生類別序列化為 RSS 2.0 格式。|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationItem> 執行個體序列化為 RSS 2.0 格式。|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>|此類別可將 <xref:System.ServiceModel.Syndication.SyndicationItem> 衍生類別序列化為 RSS 2.0 格式。|  
  
 物件模型類別：  
  
|類別|描述|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.SyndicationCategory>|表示新聞訂閱摘要分類的類別。|  
|<xref:System.ServiceModel.Syndication.SyndicationContent>|表示新聞訂閱內容的基底類別。|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtension>|表示新聞訂閱項目延伸的類別。|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection>|<xref:System.ServiceModel.Syndication.SyndicationElementExtension> 物件的集合。|  
|<xref:System.ServiceModel.Syndication.SyndicationFeed>|表示最上層摘要物件的類別。|  
|<xref:System.ServiceModel.Syndication.SyndicationItem>|表示摘要項目的類別。|  
|<xref:System.ServiceModel.Syndication.SyndicationLink>|類別，表示新聞訂閱摘要內的連結或項目內的連結。|  
|<xref:System.ServiceModel.Syndication.SyndicationPerson>|類別，表示 Atom Person 建構。|  
|<xref:System.ServiceModel.Syndication.SyndicationVersions>|類別，表示支援的新聞訂閱通訊協定版本。|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContent>|類別，表示要對終端使用者顯示的任何 <xref:System.ServiceModel.Syndication.SyndicationItem> 內容。|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContentKind>|列舉，表示支援的不同文字新聞訂閱內容型別。|  
|<xref:System.ServiceModel.Syndication.UrlSyndicationContent>|類別，表示包含另一個資源 URL 的新聞訂閱內容。|  
|<xref:System.ServiceModel.Syndication.XmlSyndicationContent>|類別，表示不會在瀏覽器中顯示的新聞訂閱內容。|  
  
 物件模型中的核心資料抽象概念為「摘要」和「項目」，兩者分別對應至 <xref:System.ServiceModel.Syndication.SyndicationFeed> 和 <xref:System.ServiceModel.Syndication.SyndicationItem> 類別。 「摘要」會公開一些摘要層級的中繼資料 (例如，Title、Description 和 Author)、儲存未知延伸的位置，以及組成摘要其餘資訊內容的項目集合。 「項目」會提供一些項目層級的中繼資料 (例如，Title、Summary 和 PublicationDate)、儲存未知延伸的位置，以及包含項目其餘資訊內容的內容項目。 「摘要」和「項目」的核心抽象概念是由代表 Atom 1.0 和 RSS 規格所提及之一般資料建構的其他類別支援。  
  
 「摘要」執行個體中的資訊可以轉換為各種不同的 XML 格式。 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 類別負責管理與 XML 間的轉換過程。 此類別是抽象的，而提供給 Atom 1.0 和 RSS 2.0 的具體實作分別為 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> 和 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>。 若要使用衍生的摘要類別，請使用 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601> 或 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>，因為它們允許您指定衍生摘要類別。 若要使用衍生項目類別，請使用 <xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601> 或 <xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>，因為它們允許您指定衍生的項目類別。協力廠商可衍生自己的 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 實作來支援各種不同的新聞訂閱格式。  
  
## <a name="extensibility"></a>擴充性  
  
- 擴充性是新聞訂閱通訊協定的一項重要功能。 Atom 1.0 和 RSS 2.0 都可讓您將屬性與項目新增至規格中未定義的新聞訂閱摘要。 WCF 新聞訂閱程式設計模型提供兩種使用自訂屬性和延伸模組的方式：衍生新的類別和鬆散類型的存取。 如需詳細資訊，[請參閱新聞](syndication-extensibility.md)訂閱擴充性。  
  
## <a name="see-also"></a>請參閱

- [WCF 新聞訂閱概觀](wcf-syndication-overview.md)
- [WCF 新聞訂閱物件模型對應到 Atom 和 RSS 的方式](how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)
- [WCF Web HTTP 程式設計模型](wcf-web-http-programming-model.md)

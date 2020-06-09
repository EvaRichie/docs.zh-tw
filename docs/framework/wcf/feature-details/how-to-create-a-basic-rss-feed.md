---
title: HOW TO：建立基本 RSS 摘要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 431879b8-a5f8-4947-ad1e-4768c726aca8
ms.openlocfilehash: 872fe325a6705e79d026cd7f6e1f7cfef5145307
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599018"
---
# <a name="how-to-create-a-basic-rss-feed"></a>HOW TO：建立基本 RSS 摘要
Windows Communication Foundation （WCF）可讓您建立公開新聞訂閱摘要的服務。 本主題討論如何建立可公開 RSS 新聞訂閱摘要的新聞訂閱服務。  
  
### <a name="to-create-a-basic-syndication-service"></a>若要建立基本新聞訂閱服務  
  
1. 使用以 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性標記的介面來定義服務合約。 每個公開為新聞訂閱摘要的作業都應該傳回 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> 物件。  
  
     [!code-csharp[htRssBasic#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#0)]
     [!code-vb[htRssBasic#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#0)]  
  
    > [!NOTE]
    > 所有套用 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性的服務作業都會對應至 HTTP GET 要求。 若要將您的作業對應至不同的 HTTP 方法，請改用 <xref:System.ServiceModel.Web.WebInvokeAttribute>。 如需詳細資訊，請參閱[如何：建立基本 WCF WEB HTTP 服務](how-to-create-a-basic-wcf-web-http-service.md)。  
  
2. 實作服務合約。  
  
     [!code-csharp[htRssBasic#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#1)]
     [!code-vb[htRssBasic#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#1)]  
  
3. 建立 <xref:System.ServiceModel.Syndication.SyndicationFeed> 物件並新增作者、分類和描述。  
  
     [!code-csharp[htRssBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#2)]
     [!code-vb[htRssBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#2)]  
  
4. 建立幾個 <xref:System.ServiceModel.Syndication.SyndicationItem> 物件。  
  
     [!code-csharp[htRssBasic#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#3)]
     [!code-vb[htRssBasic#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#3)]  
  
5. 將 <xref:System.ServiceModel.Syndication.SyndicationItem> 加入至摘要。  
  
     [!code-csharp[htRssBasic#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#4)]
     [!code-vb[htRssBasic#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#4)]  
  
6. 傳回摘要。  
  
     [!code-csharp[htRssBasic#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#5)]
     [!code-vb[htRssBasic#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#5)]  
  
### <a name="to-host-a-service"></a>若要裝載服務  
  
1. 建立 <xref:System.ServiceModel.Web.WebServiceHost> 物件。  
  
     [!code-csharp[htRssBasic#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#6)]
     [!code-vb[htRssBasic#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#6)]  
  
2. 開啟服務主機並等候使用者按下 ENTER。  
  
     [!code-csharp[htRssBasic#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#8)]
     [!code-vb[htRssBasic#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#8)]  
  
### <a name="to-call-getblog-with-an-http-get"></a>若要使用 HTTP GET 呼叫 GetBlog()  
  
1. 開啟 Internet Explorer，輸入下列 URL，然後按 ENTER： `http://localhost:8000/BlogService/GetBlog` 。 URL 包含服務的基底位址（ `http://localhost:8000/BlogService` ）、端點的相對位址，以及要呼叫的服務作業。  
  
### <a name="to-call-getblog-from-code"></a>若要從程式碼呼叫 GetBlog()  
  
1. 使用基底位址與您要呼叫的方法建立 <xref:System.Xml.XmlReader>。  
  
     [!code-csharp[htRssBasic#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#9)]
     [!code-vb[htRssBasic#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#9)]  
  
2. 呼叫靜態 <xref:System.ServiceModel.Syndication.SyndicationFeed.Load%28System.Xml.XmlReader%29> 方法，傳入剛才建立的 <xref:System.Xml.XmlReader>。  
  
     [!code-csharp[htRssBasic#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#10)]
     [!code-vb[htRssBasic#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#10)]  
  
     這會叫用服務作業，並在新的 <xref:System.ServiceModel.Syndication.SyndicationFeed> 中填入服務作業所傳回的格式器。  
  
3. 存取摘要物件。  
  
     [!code-csharp[htRssBasic#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#11)]
     [!code-vb[htRssBasic#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#11)]  
  
## <a name="example"></a>範例  
 以下是這個範例的完整程式碼清單。  
  
 [!code-csharp[htRssBasic#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#12)]
 [!code-vb[htRssBasic#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#12)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 在編譯先前的程式碼時，請參考 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>

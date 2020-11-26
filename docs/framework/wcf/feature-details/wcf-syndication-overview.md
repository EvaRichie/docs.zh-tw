---
title: WCF 新聞訂閱概觀
ms.date: 03/30/2017
ms.assetid: af6d4c39-e5e8-4099-aee6-5261feff9107
ms.openlocfilehash: 8ffc42987ff03b074e35f594491a0ca5a3adbe46
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239051"
---
# <a name="wcf-syndication-overview"></a>WCF 新聞訂閱概觀

Windows Communication Foundation (WCF) 提供從 WCF 服務公開新聞訂閱摘要的支援。 新聞訂閱是一種應用程式整合機制，可讓伺服器透過稱為摘要的互通格式來公開一些應用程式資料。 摘要是一種應用程式資料的集合，內含一些摘要層級的中繼資料 (標題、作者、URL 與其他中繼資料) 以及一系列的摘要項目。 摘要中的項目通常會依照時間順序，從距今最近的時間往回排列。 摘要項目包含一組標準的項目層級中繼資料 (標題、URL、建立日期、分類，與其他項目層級的中繼資料) 以及任意數量的特定應用程式資料。 最常見的新聞訂閱摘要類型是 (RSS) 2.0 和 Atom 1.0 的簡單新聞訂閱，這兩者都是由 WCF 支援。  
  
## <a name="object-model"></a>物件模型  

 WCF 會定義一組新聞訂閱專屬類別，可讓您使用與格式無關的方式來處理摘要、摘要專案和相關的中繼資料： <xref:System.ServiceModel.Syndication.SyndicationFeed> 、 <xref:System.ServiceModel.Syndication.SyndicationItem> 、 <xref:System.ServiceModel.Syndication.SyndicationPerson> 、 <xref:System.ServiceModel.Syndication.SyndicationLink> 和其他新聞訂閱特定類別。 WCF 也會定義以 WCF REST 程式設計模型為基礎的基礎結構類別，以提供摘要整合支援，包括： <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> 和  <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> 。 摘要格式器類別支援在 RSS 2.0 和 Atom 1.0 格式之間來回序列化物件模型。  
  
## <a name="scenarios"></a>案例  

 今日最常見的新聞訂閱應用就是網誌，也就是網誌作者會定期發行一些資訊。 這些內容可以是文字、影像、聲音，或其他類型的資訊。 許多報紙與雜誌也會透過新聞訂閱方式來發行新聞報導或文章。 只要訂閱這類摘要，使用者就可以隨時取得這些網站的最新資訊。 儘管新聞訂閱最常與網誌和出版社產生關聯，它還可以和其他用來公開大量資訊的應用程式搭配使用，例如，使用新聞訂閱摘要來公開 Bug 資料庫。 您可以建立一個 WCF 服務，以公開稱為的作業 `CodeDefects` 。 這項作業所採用的參數能夠針對您要擷取 Bug 的人員指定其電子郵件地址。 用戶端可以使用下列 URL 來呼叫作業： `http://someserver/bugDatabase/CodeDefects?user=johndoe` 。  
  
## <a name="syndication-formats"></a>新聞訂閱格式  

 WCF 摘要整合平臺支援 RSS 2.0 和 Atom 1.0。  
  
## <a name="see-also"></a>另請參閱

- [WCF Web HTTP 程式設計模型](wcf-web-http-programming-model.md)

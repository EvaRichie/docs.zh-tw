---
title: 如何：自訂搭配反映提供者使用的摘要 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, customizing feeds
ms.assetid: 00c23dcf-9bb8-459a-a012-6c4d9bcad7e9
ms.openlocfilehash: fb22e87569a8e243813b3186232b6989abeb2a5e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91161304"
---
# <a name="how-to-customize-feeds-with-the-reflection-provider-wcf-data-services"></a>如何：自訂搭配反映提供者使用的摘要 (WCF 資料服務)

WCF Data Services 可讓您自訂資料服務回應中的 Atom 序列化，讓實體的屬性可以對應至 AtomPub 通訊協定中定義的未使用元素。 本主題說明如何針對資料模型中的實體類型 (經由使用反映提供者定義) 定義對應的屬性。 如需詳細資訊，請參閱摘要 [自訂](feed-customization-wcf-data-services.md)。  
  
 此範例的資料模型定義于 how [to：使用反映提供者建立資料服務](create-a-data-service-using-rp-wcf-data-services.md)中的主題。  
  
## <a name="example"></a>範例  

 在下列範例中，`Order` 類型的兩個屬性都對應至現有的元素項目。 `Product` 類型的 `Item` 屬性會對應至不同命名空間中的自訂摘要屬性。  
  
 [!code-csharp[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_custom_feeds/cs/orderitems.svc.cs#customiqueryablefeeds)]
 [!code-vb[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_custom_feeds/vb/orderitems.svc.vb#customiqueryablefeeds)]  
  
## <a name="example"></a>範例  

 上一個範例會傳回以下 URI `http://myservice/OrderItems.svc/Orders(0)?$expand=Items` 的結果。  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResultInline](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/iqueryablefeedresultinline.xml#iqueryablefeedresultinline)]  
  
## <a name="see-also"></a>另請參閱

- [反映提供者](reflection-provider-wcf-data-services.md)

---
title: Entity Framework 提供者 (WCF 資料服務)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 650b5eb6-c71d-4dc1-8b64-b6beaf752114
ms.openlocfilehash: cb7bd7e793f73fc34057150ee5217dba6653237e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172641"
---
# <a name="entity-framework-provider-wcf-data-services"></a>Entity Framework 提供者 (WCF 資料服務)

如同 WCF Data Services，ADO.NET Entity Framework 是以實體資料模型為基礎，也就是實體關聯性模型的型別。 Entity Framework 會實體資料模型針對資料來源將作業（稱為 *概念模型*）轉譯為對等作業。 這會使 Entity Framework 是以關聯式資料為基礎之資料服務的理想提供者，而任何具有支援 Entity Framework 之資料提供者的資料庫都可以搭配 WCF Data Services 使用。 如需目前支援 Entity Framework 的資料來源清單，請參閱 [Entity Framework 提供者](/ef/ef6/fundamentals/providers/)。
  
 在概念模型中，實體容器是服務的根。 您必須先在 Entity Framework 中定義概念模型，資料服務才能公開資料。 如需詳細資訊，請參閱 [如何：使用 ADO.NET Entity Framework 資料來源建立資料服務](create-a-data-service-using-an-adonet-ef-data-wcf.md)。  
  
 WCF Data Services 藉由讓您定義實體的並行存取權杖，來支援開放式平行存取模型。 這個並行語彙基元包含實體的一個或多個屬性，資料服務會使用它來判斷正在要求、更新或刪除的資料中是否已經發生變更。 當取自要求中 eTag 的語彙基元值與目前實體的值不同時，資料服務就會引發例外狀況。 若要指出屬性是並行存取權杖的一部分，您必須將屬性套用至 `ConcurrencyMode="Fixed"` Entity Framework 提供者所定義的資料模型中。 並行語彙基元不得包含索引鍵屬性或導覽屬性。 如需詳細資訊，請參閱 [更新資料服務](updating-the-data-service-wcf-data-services.md)。  
  
 若要深入瞭解 Entity Framework，請參閱 [Entity Framework 總覽](../adonet/ef/overview.md)。  
  
## <a name="see-also"></a>另請參閱

- [資料服務提供者](data-services-providers-wcf-data-services.md)
- [反映提供者](reflection-provider-wcf-data-services.md)
- [實體資料模型](../adonet/entity-data-model.md)

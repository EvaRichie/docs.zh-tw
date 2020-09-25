---
title: 實體集
ms.date: 03/30/2017
ms.assetid: 59ec6ab0-88e5-4d25-b112-7a4eccbe61f0
ms.openlocfilehash: 6286d3707a8506e7a389359a5aa361c152e75212
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194787"
---
# <a name="entity-set"></a>實體集

*實體集*是[實體類型](entity-type.md)實例的邏輯容器，以及衍生自該實體類型之任何類型的實例。  (如需衍生類型的詳細資訊，請參閱 [實體資料模型：繼承](entity-data-model-inheritance.md)。 ) 實體類型和實體集之間的關聯性，類似于關係資料庫中的資料列和資料表之間的關聯性：像是資料列、實體型別描述資料結構，以及像資料表一樣，實體集包含給定結構的實例。 實體集不是資料模型建構，也就是說，它不會描述資料結構。 反之，實體集會提供建構，讓裝載或儲存環境 (例如 Common Language Runtime 或 SQL Server 資料庫) 群組實體類型執行個體，以將其對應至資料存放區。  
  
 實體集是在 [實體容器](entity-container.md)中定義的，而實體容器是實體集和 [關聯集](association-set.md)的邏輯群組。  
  
 實體類型執行個體若要存在於實體集中，下列條件必須為 true：  
  
- 執行個體的類型必須與該實體集所依據的實體類型相同，或者執行個體的型別為該實體類型的子類型。  
  
- 實例的 [實體索引鍵](entity-key.md) 在實體集內是唯一的。  
  
- 執行個體不存在於任何其他實體集中。  
  
    > [!NOTE]
    > 您可以使用相同的實體類型定義多個實體集，但指定實體類型的執行個體只能存在於一個實體集中。  
  
 您不需定義概念模型中每個實體類型的實體集。  
  
## <a name="example"></a>範例  

 下圖顯示包含三種實體類型 (`Book`、`Publisher` 和 `Author`) 的概念模型。  
  
 ![包含三種實體類型的範例模型](./media/entity-set/example-model-three-entity-types.gif)  
  
 下圖顯示以前述概念模型為基礎的兩個實體集 (`Books` 和 `Publishers`)，以及一個關聯集 `PublishedBy`)。 `Books`實體集中的 Bi 代表 `Book` 執行時間的實體型別實例。 同樣地，Pj `Publisher` 則代表 `Publishers` 實體集中的實例。 BiPj 代表 `PublishedBy` 關聯集中關聯的實例 `PublishedBy` 。  
  
 ![顯示集合範例的螢幕擷取畫面。](./media/entity-set/sets-example-association.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。 下列 CSDL 定義實體容器，上述概念模型中的每個實體類型皆具有一個實體集。 請注意，每個實體集名稱和實體類型都是使用 XML 屬性定義的。  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 您可以定義每個類型的多重實體集 (MEST)。 下列 CSDL 所定義的實體容體具有兩個 `Book` 實體類型的實體集：  
  
 [!code-xml[EDM_Example_Model#MESTExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#mestexample)]  
  
## <a name="see-also"></a>另請參閱

- [實體資料模型索引鍵概念](entity-data-model-key-concepts.md)
- [實體資料模型](entity-data-model.md)

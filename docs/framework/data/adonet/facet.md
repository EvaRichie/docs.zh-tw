---
title: facet
ms.date: 03/30/2017
ms.assetid: 91c4e6aa-3e54-4b6c-a38a-abf27808cc85
ms.openlocfilehash: b9ef2276f988923fe83cefce910e8c3685cb9da9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156442"
---
# <a name="facet"></a>facet

*Facet*用來將詳細資料新增至基本類型屬性定義。 [屬性](property.md)定義包含屬性類型的相關資訊，但通常需要更多詳細資料。 例如，概念模型中的實體類型可能會有 `String` 型別的屬性，其值不可設為 null。 Facet 可讓您指定此詳細層級。  
  
 下表描述 EDM 中支援的 Facet。  
  
> [!NOTE]
> 確切的 Facet 值和行為取決於使用 EDM 實作的執行階段環境。  
  
|Facet|描述|適用於|  
|-----------|-----------------|----------------|  
|`Collation`|在執行比較和排序屬性值的作業時，指定要使用的定序順序 (或排序順序)。|`String`|  
|`ConcurrencyMode`|表示屬性值應用於開放式並行存取檢查。|所有基底類型屬性|  
|`Default`|執行個體化時如果沒有提供值，請指定屬性的預設值。|所有基底類型屬性|  
|`FixedLength`|指定屬性值的長度是否可以變更。|`Binary`, `String`|  
|`MaxLength`|指定屬性值的最大長度。|`Binary`, `String`|  
|`Nullable`|指定屬性是否可以有 null 值。|所有基底類型屬性|  
|`Precision`|針對型別 `Decimal` 的屬性，指定屬性值可以擁有的位數。 針對型別 `Time`、`DateTime` 和 `DateTimeOffset` 的屬性，指定屬性值秒數之小數點後的位數。|`DateTime`, `DateTimeOffset`, `Decimal`, `Time`,|  
|`Scale`|指定屬性值小數點右邊的位數。|Decimal|  
|`Unicode`|指出屬性值是否儲存為 Unicode。|`String`|  
  
## <a name="example"></a>範例  

 [ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。 下列 CSDL 定義 `Book` 實體類型。 請注意，Facet 會實作為 XML 屬性。 Facet 值表示不可將任何屬性設為 null，且 `Scale` 屬性的 `Precision` 和 `Revision` 皆分別設為 29。  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## <a name="see-also"></a>另請參閱

- [實體資料模型索引鍵概念](entity-data-model-key-concepts.md)
- [實體資料模型](entity-data-model.md)

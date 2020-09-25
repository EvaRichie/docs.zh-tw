---
title: 實體索引鍵
ms.date: 03/30/2017
ms.assetid: 0d447a6d-fa7a-4db0-8e7a-fd45e385fca0
ms.openlocfilehash: b2692faf2f8bea27c8a5d6cdc52689ca186d3194
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200780"
---
# <a name="entity-key"></a><span data-ttu-id="b5424-102">實體索引鍵</span><span class="sxs-lookup"><span data-stu-id="b5424-102">entity key</span></span>

<span data-ttu-id="b5424-103">*實體索引鍵*是[實體類型](entity-type.md)的[屬性](property.md)或一組屬性，用來判斷身分識別。</span><span class="sxs-lookup"><span data-stu-id="b5424-103">An *entity key* is a [property](property.md) or a set of properties of an [entity type](entity-type.md) that are used to determine identity.</span></span> <span data-ttu-id="b5424-104">構成實體索引鍵的屬性是在設計階段選取的。</span><span class="sxs-lookup"><span data-stu-id="b5424-104">The properties that make up an entity key are chosen at design time.</span></span> <span data-ttu-id="b5424-105">實體索引鍵屬性的值必須在執行時間，唯一識別 [實體集](entity-set.md) 內的實體類型實例。</span><span class="sxs-lookup"><span data-stu-id="b5424-105">The values of entity key properties must uniquely identify an entity type instance within an [entity set](entity-set.md) at run time.</span></span> <span data-ttu-id="b5424-106">您應選取構成實體索引鍵的屬性，以保證執行個體在實體集中的唯一性。</span><span class="sxs-lookup"><span data-stu-id="b5424-106">The properties that make up an entity key should be chosen to guarantee uniqueness of instances in an entity set.</span></span>  
  
 <span data-ttu-id="b5424-107">屬性集若要成為實體索引鍵，需求如下：</span><span class="sxs-lookup"><span data-stu-id="b5424-107">The following are the requirements for a set of properties to be an entity key:</span></span>  
  
- <span data-ttu-id="b5424-108">實體集中的任兩個實體索引鍵均不可完全相同。</span><span class="sxs-lookup"><span data-stu-id="b5424-108">No two entity keys within an entity set can be identical.</span></span> <span data-ttu-id="b5424-109">也就是說，以實體集中任兩個實體來說，構成索引鍵的所有屬性的值不可完全相同。</span><span class="sxs-lookup"><span data-stu-id="b5424-109">That is, for any two entities within an entity set, the values for all of the properties that constitute a key cannot be the same.</span></span> <span data-ttu-id="b5424-110">不過，構成實體索引鍵的部分 (非所有) 值可以相同。</span><span class="sxs-lookup"><span data-stu-id="b5424-110">However, some (but not all) of the values that make up an entity key can be the same.</span></span>  
  
- <span data-ttu-id="b5424-111">實體索引鍵必須由一組不可為 null 且不可變的 [基本類型屬性](entity-data-model-primitive-data-types.md)所組成。</span><span class="sxs-lookup"><span data-stu-id="b5424-111">An entity key must consist of a set of non-nullable, immutable, [primitive type properties](entity-data-model-primitive-data-types.md).</span></span>  
  
- <span data-ttu-id="b5424-112">構成指定實體類型之實體索引鍵的屬性不可變更。</span><span class="sxs-lookup"><span data-stu-id="b5424-112">The properties that make up an entity key for a given entity type cannot change.</span></span> <span data-ttu-id="b5424-113">您不能允許指定的實體類型擁有多個可能的實體索引鍵，不支援 Surrogate 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b5424-113">You cannot allow more than one possible entity key for a given entity type; surrogate keys are not supported.</span></span>  
  
- <span data-ttu-id="b5424-114">實體與繼承階層相關時，根實體必須包含構成實體索引鍵的所有屬性，而且必須在根實體類型定義該實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b5424-114">When an entity is involved in an inheritance hierarchy, the root entity must contain all the properties that make up the entity key, and the entity key must be defined on the root entity type.</span></span> <span data-ttu-id="b5424-115">如需詳細資訊，請參閱 [實體資料模型：繼承](entity-data-model-inheritance.md)。</span><span class="sxs-lookup"><span data-stu-id="b5424-115">For more information, see [Entity Data Model: Inheritance](entity-data-model-inheritance.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="b5424-116">範例</span><span class="sxs-lookup"><span data-stu-id="b5424-116">Example</span></span>  

 <span data-ttu-id="b5424-117">下圖顯示包含三種實體類型 (`Book`、`Publisher` 和 `Author`) 的概念模型。</span><span class="sxs-lookup"><span data-stu-id="b5424-117">The diagram below shows a conceptual model with three entity types: `Book`, `Publisher`, and `Author`.</span></span> <span data-ttu-id="b5424-118">構成實體索引鍵之每個實體類型的屬性皆加註「(索引鍵)」。</span><span class="sxs-lookup"><span data-stu-id="b5424-118">The properties of each entity type that make up its entity key are denoted with "(Key)".</span></span> <span data-ttu-id="b5424-119">請注意，`Author` 實體類型的實體索引鍵包含兩個屬性：`Name` 和 `Address`。</span><span class="sxs-lookup"><span data-stu-id="b5424-119">Note that the `Author` entity type has an entity key that consists of two properties, `Name` and `Address`.</span></span>  
  
 ![包含三種實體類型的範例模型](./media/entity-key/example-model-three-entity-types.gif)  
  
 <span data-ttu-id="b5424-121">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="b5424-121">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="b5424-122">下列的 CSDL 會定義上圖顯示的 `Book` 實體類型。</span><span class="sxs-lookup"><span data-stu-id="b5424-122">The CSDL below defines the `Book` entity type shown in the diagram above.</span></span> <span data-ttu-id="b5424-123">請注意，實體索引鍵是藉由參考實體類型的 `ISBN` 屬性而定義的。</span><span class="sxs-lookup"><span data-stu-id="b5424-123">Note that the entity key is defined by referencing the `ISBN` property of the entity type.</span></span>  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 <span data-ttu-id="b5424-124">`ISBN` 屬性是實體索引鍵的最佳選擇，因為國際標準書號 (International Standard Book Number，ISBN) 可明確識別一本書。</span><span class="sxs-lookup"><span data-stu-id="b5424-124">The `ISBN` property is a good choice for the entity key because an International Standard Book Number (ISBN) uniquely identifies a book.</span></span>  
  
 <span data-ttu-id="b5424-125">下列的 CSDL 會定義上圖顯示的 `Author` 實體類型。</span><span class="sxs-lookup"><span data-stu-id="b5424-125">The CSDL below defines the `Author` entity type shown in the diagram above.</span></span> <span data-ttu-id="b5424-126">請注意，實體索引鍵包含兩個屬性：`Name` 和 `Address`。</span><span class="sxs-lookup"><span data-stu-id="b5424-126">Note that the entity key consists of two properties, `Name` and `Address`.</span></span>  
  
 [!code-xml[EDM_Example_Model#CompositeKeyExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#compositekeyexample)]  
  
 <span data-ttu-id="b5424-127">針對實體索引鍵使用 `Name` 和 `Address` 是合理的選擇，因為相同名稱的兩位作者不太可能住在同一個地址。</span><span class="sxs-lookup"><span data-stu-id="b5424-127">Using `Name` and `Address` for the entity key is a reasonable choice, because two authors of the same name are unlikely to live at the same address.</span></span> <span data-ttu-id="b5424-128">不過，針對實體索引鍵所做的這個選擇不能絕對保證實體集中的唯一實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b5424-128">However, this choice for an entity key does not absolutely guarantee unique entity keys in an entity set.</span></span> <span data-ttu-id="b5424-129">在這種情況下，建議您加入一個屬性，例如 `AuthorId`，可用於明確識別作者。</span><span class="sxs-lookup"><span data-stu-id="b5424-129">Adding a property, such as `AuthorId`, that could be used to uniquely identify an author would be recommended in this case.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b5424-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b5424-130">See also</span></span>

- [<span data-ttu-id="b5424-131">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="b5424-131">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="b5424-132">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="b5424-132">Entity Data Model</span></span>](entity-data-model.md)

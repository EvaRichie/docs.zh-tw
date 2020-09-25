---
title: 參考完整性條件約束
description: 瞭解實體資料模型中的參考完整性條件約束，確保實體類型之間一律存在有效的關聯。
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: 6ade9d0155a6915757c7f47c5cb3ab0a51dbd437
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172732"
---
# <a name="referential-integrity-constraint"></a><span data-ttu-id="bc3a8-103">參考完整性條件約束</span><span class="sxs-lookup"><span data-stu-id="bc3a8-103">referential integrity constraint</span></span>

<span data-ttu-id="bc3a8-104">實體資料模型 (EDM) 中的 *參考完整性條件約束* 類似于關係資料庫中的參考完整性條件約束。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-104">A *referential integrity constraint* in the Entity Data Model (EDM) is similar to a referential integrity constraint in a relational database.</span></span> <span data-ttu-id="bc3a8-105">與資料行 (或從資料庫資料表) 的資料行相同的方式可以參考另一個資料表的主鍵，而[實體類型](entity-type.md)) 的 ([屬性（property](property.md) ）可以參考另一個實體類型的[實體索引鍵](entity-key.md)。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-105">In the same way that a column (or columns) from a database table can reference the primary key of another table, a [property](property.md) (or properties) of an [entity type](entity-type.md) can reference the [entity key](entity-key.md) of another entity type.</span></span> <span data-ttu-id="bc3a8-106">參考的實體類型稱為條件約束的 *主要端點* 。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-106">The entity type that is referenced is called the *principal end* of the constraint.</span></span> <span data-ttu-id="bc3a8-107">參考主體端的實體類型稱為條件約束的 *相依端點* 。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-107">The entity type that references the principal end is called the *dependent end* of the constraint.</span></span>  
  
 <span data-ttu-id="bc3a8-108">參考完整性條件約束定義為兩個實體類型之間 [關聯](association-type.md) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-108">A referential integrity constraint is defined as part of an [association](association-type.md) between two entity types.</span></span> <span data-ttu-id="bc3a8-109">參考完整性條件約束的定義指定下列資訊：</span><span class="sxs-lookup"><span data-stu-id="bc3a8-109">The definition for a referential integrity constraint specifies the following information:</span></span>  
  
- <span data-ttu-id="bc3a8-110">條件約束的主要端點。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-110">The principal end of the constraint.</span></span> <span data-ttu-id="bc3a8-111">(實體類型，相依端點會參考其實體索引鍵。)</span><span class="sxs-lookup"><span data-stu-id="bc3a8-111">(An entity type whose entity key is referenced by the dependent end.)</span></span>  
  
- <span data-ttu-id="bc3a8-112">主要端點的實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-112">The entity key of the principal end.</span></span>  
  
- <span data-ttu-id="bc3a8-113">條件約束的相依端點。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-113">The dependent end of the constraint.</span></span> <span data-ttu-id="bc3a8-114">(實體類型，具有參考主要端點之實體索引鍵的屬性。)</span><span class="sxs-lookup"><span data-stu-id="bc3a8-114">(An entity type that has a property or properties that reference the entity key of the principal end.)</span></span>  
  
- <span data-ttu-id="bc3a8-115">相依端點的參考屬性。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-115">The referencing property or properties of the dependent end.</span></span>  
  
 <span data-ttu-id="bc3a8-116">在 EDM 中，參考完整性條件約束的目的在於確保有效的關聯永遠存在。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-116">The purpose of referential integrity constraints in the EDM is to ensure that valid associations always exist.</span></span> <span data-ttu-id="bc3a8-117">如需詳細資訊，請參閱 [外鍵屬性](foreign-key-property.md)。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-117">For more information, see [foreign key property](foreign-key-property.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="bc3a8-118">範例</span><span class="sxs-lookup"><span data-stu-id="bc3a8-118">Example</span></span>  

 <span data-ttu-id="bc3a8-119">下圖顯示包含兩個關聯 (`WrittenBy` 和 `PublishedBy`) 的概念模型。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-119">The diagram below shows a conceptual model with two associations: `WrittenBy` and `PublishedBy`.</span></span> <span data-ttu-id="bc3a8-120">`Book` 實體類型具有屬性 `PublisherId`，當您定義 `Publisher` 關聯的參考完整性條件約束時，此屬性會參考 `PublishedBy` 實體類型的實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-120">The `Book` entity type has a property, `PublisherId`, that references the entity key of the `Publisher` entity type when you define a referential integrity constraint on the `PublishedBy` association.</span></span>  
  
 <span data-ttu-id="bc3a8-121">![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "參考條件約束模型的範例")</span><span class="sxs-lookup"><span data-stu-id="bc3a8-121">![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "Example of a referential constraint model")</span></span>  
  
 <span data-ttu-id="bc3a8-122">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-122">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="bc3a8-123">下列 CSDL 會對上述概念模型中的 `PublishedBy` 關聯定義參考完整性條件約束。</span><span class="sxs-lookup"><span data-stu-id="bc3a8-123">The following CSDL defines a referential integrity constraint on the `PublishedBy` association shown in the conceptual model above.</span></span>  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a><span data-ttu-id="bc3a8-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bc3a8-124">See also</span></span>

- [<span data-ttu-id="bc3a8-125">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="bc3a8-125">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="bc3a8-126">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="bc3a8-126">Entity Data Model</span></span>](entity-data-model.md)

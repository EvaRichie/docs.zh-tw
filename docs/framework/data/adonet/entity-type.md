---
title: Entity Type - 實體類型
ms.date: 03/30/2017
ms.assetid: a6dee9ab-9e4a-48f2-a169-3f79cc15821c
ms.openlocfilehash: 3f99667a06d8aa439232802d4909290dfe9db97c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194774"
---
# <a name="entity-type"></a><span data-ttu-id="98466-102">Entity Type - 實體類型</span><span class="sxs-lookup"><span data-stu-id="98466-102">entity type</span></span>

<span data-ttu-id="98466-103">*實體類型*是用來描述實體資料模型 (EDM) 之資料結構的基本組建區塊。</span><span class="sxs-lookup"><span data-stu-id="98466-103">The *entity type* is the fundamental building block for describing the structure of data with the Entity Data Model (EDM).</span></span> <span data-ttu-id="98466-104">在概念模型中，實體類型代表最上層概念的結構，例如客戶或訂單。</span><span class="sxs-lookup"><span data-stu-id="98466-104">In a conceptual model, an entity type represents the structure of top-level concepts, such as customers or orders.</span></span> <span data-ttu-id="98466-105">實體類型是實體類型執行個體的範本。</span><span class="sxs-lookup"><span data-stu-id="98466-105">An entity type is a template for entity type instances.</span></span> <span data-ttu-id="98466-106">每個範本包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="98466-106">Each template contains the following information:</span></span>  
  
- <span data-ttu-id="98466-107">唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="98466-107">A unique name.</span></span> <span data-ttu-id="98466-108">(必要項。)</span><span class="sxs-lookup"><span data-stu-id="98466-108">(Required.)</span></span>  
  
- <span data-ttu-id="98466-109">由一或多個屬性定義的 [實體索引鍵](entity-key.md) 。</span><span class="sxs-lookup"><span data-stu-id="98466-109">An [entity key](entity-key.md) defined by one or more properties.</span></span> <span data-ttu-id="98466-110">(必要項。)</span><span class="sxs-lookup"><span data-stu-id="98466-110">(Required.)</span></span>  
  
- <span data-ttu-id="98466-111">[屬性](property.md)形式的資料。</span><span class="sxs-lookup"><span data-stu-id="98466-111">Data in the form of [properties](property.md).</span></span> <span data-ttu-id="98466-112">(選擇性。)</span><span class="sxs-lookup"><span data-stu-id="98466-112">(Optional.)</span></span>  
  
- <span data-ttu-id="98466-113">允許從[關聯](association-type.md)[的一端導覽](association-end.md)至另一端的[導覽屬性](navigation-property.md)。</span><span class="sxs-lookup"><span data-stu-id="98466-113">[Navigation properties](navigation-property.md) that allow for navigation from one [end](association-end.md) of an [association](association-type.md) to the other end.</span></span> <span data-ttu-id="98466-114">(選用)</span><span class="sxs-lookup"><span data-stu-id="98466-114">(Optional)</span></span>  
  
 <span data-ttu-id="98466-115">在應用程式中，實體類型的執行個體代表特定的物件 (例如特定的客戶或訂單)。</span><span class="sxs-lookup"><span data-stu-id="98466-115">In an application, an instance of an entity type represents a specific object (such as a specific customer or order).</span></span> <span data-ttu-id="98466-116">實體類型的每個實例在[實體集](entity-set.md)內都必須有唯一的[實體索引鍵](entity-key.md)。</span><span class="sxs-lookup"><span data-stu-id="98466-116">Each instance of an entity type must have a unique [entity key](entity-key.md) within an [entity set](entity-set.md).</span></span>  
  
 <span data-ttu-id="98466-117">如果兩個實體類型執行個體屬於相同類型，而且索引鍵的值也相同，則會將這兩個執行個體視為相等。</span><span class="sxs-lookup"><span data-stu-id="98466-117">Two entity type instances are considered equal only if they are of the same type and the values of their entity keys are the same.</span></span>  
  
## <a name="example"></a><span data-ttu-id="98466-118">範例</span><span class="sxs-lookup"><span data-stu-id="98466-118">Example</span></span>  

 <span data-ttu-id="98466-119">下圖顯示包含三種實體類型 (`Book`、`Publisher` 和 `Author`) 的概念模型：</span><span class="sxs-lookup"><span data-stu-id="98466-119">The diagram below shows a conceptual model with three entity types: `Book`, `Publisher`, and `Author`:</span></span>  
  
 ![包含三種實體類型的範例模型](./media/entity-type/example-model-three-entity-types.gif)  
  
 <span data-ttu-id="98466-121">請注意，構成實體索引鍵的每個實體類型屬性皆加註「(索引鍵)」。</span><span class="sxs-lookup"><span data-stu-id="98466-121">Note that the properties of each entity type that make up its entity key are denoted with "(Key)".</span></span>  
  
 <span data-ttu-id="98466-122">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="98466-122">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="98466-123">下列 CSDL 定義上圖所顯示的 `Book` 實體類型：</span><span class="sxs-lookup"><span data-stu-id="98466-123">The following CSDL defines the `Book` entity type shown in the diagram above:</span></span>  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## <a name="see-also"></a><span data-ttu-id="98466-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98466-124">See also</span></span>

- [<span data-ttu-id="98466-125">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="98466-125">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="98466-126">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="98466-126">Entity Data Model</span></span>](entity-data-model.md)
- [<span data-ttu-id="98466-127">方面</span><span class="sxs-lookup"><span data-stu-id="98466-127">facet</span></span>](facet.md)

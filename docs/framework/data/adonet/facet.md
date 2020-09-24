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
# <a name="facet"></a><span data-ttu-id="219ed-102">facet</span><span class="sxs-lookup"><span data-stu-id="219ed-102">facet</span></span>

<span data-ttu-id="219ed-103">*Facet*用來將詳細資料新增至基本類型屬性定義。</span><span class="sxs-lookup"><span data-stu-id="219ed-103">A *facet* is used to add detail to a primitive type property definition.</span></span> <span data-ttu-id="219ed-104">[屬性](property.md)定義包含屬性類型的相關資訊，但通常需要更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="219ed-104">A [property](property.md) definition contains information about the property type, but often more detail is necessary.</span></span> <span data-ttu-id="219ed-105">例如，概念模型中的實體類型可能會有 `String` 型別的屬性，其值不可設為 null。</span><span class="sxs-lookup"><span data-stu-id="219ed-105">For example, an entity type in a conceptual model might have a property of type `String` whose value cannot be set to null.</span></span> <span data-ttu-id="219ed-106">Facet 可讓您指定此詳細層級。</span><span class="sxs-lookup"><span data-stu-id="219ed-106">Facets allow you to specify this level of detail.</span></span>  
  
 <span data-ttu-id="219ed-107">下表描述 EDM 中支援的 Facet。</span><span class="sxs-lookup"><span data-stu-id="219ed-107">The table below describes the facets that are supported in the EDM.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="219ed-108">確切的 Facet 值和行為取決於使用 EDM 實作的執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="219ed-108">The exact values and behaviors of facets are determined by the run-time environment that uses an EDM implementation.</span></span>  
  
|<span data-ttu-id="219ed-109">Facet</span><span class="sxs-lookup"><span data-stu-id="219ed-109">Facet</span></span>|<span data-ttu-id="219ed-110">描述</span><span class="sxs-lookup"><span data-stu-id="219ed-110">Description</span></span>|<span data-ttu-id="219ed-111">適用於</span><span class="sxs-lookup"><span data-stu-id="219ed-111">Applies to</span></span>|  
|-----------|-----------------|----------------|  
|`Collation`|<span data-ttu-id="219ed-112">在執行比較和排序屬性值的作業時，指定要使用的定序順序 (或排序順序)。</span><span class="sxs-lookup"><span data-stu-id="219ed-112">Specifies the collating sequence (or sorting sequence) to be used when performing comparison and ordering operations on values of the property.</span></span>|`String`|  
|`ConcurrencyMode`|<span data-ttu-id="219ed-113">表示屬性值應用於開放式並行存取檢查。</span><span class="sxs-lookup"><span data-stu-id="219ed-113">Indicates that the value of the property should be used for optimistic concurrency checks.</span></span>|<span data-ttu-id="219ed-114">所有基底類型屬性</span><span class="sxs-lookup"><span data-stu-id="219ed-114">All primitive type properties</span></span>|  
|`Default`|<span data-ttu-id="219ed-115">執行個體化時如果沒有提供值，請指定屬性的預設值。</span><span class="sxs-lookup"><span data-stu-id="219ed-115">Specifies the default value of the property if no value is supplied upon instantiation.</span></span>|<span data-ttu-id="219ed-116">所有基底類型屬性</span><span class="sxs-lookup"><span data-stu-id="219ed-116">All primitive type properties</span></span>|  
|`FixedLength`|<span data-ttu-id="219ed-117">指定屬性值的長度是否可以變更。</span><span class="sxs-lookup"><span data-stu-id="219ed-117">Specifies whether the length of the property value can vary.</span></span>|<span data-ttu-id="219ed-118">`Binary`, `String`</span><span class="sxs-lookup"><span data-stu-id="219ed-118">`Binary`, `String`</span></span>|  
|`MaxLength`|<span data-ttu-id="219ed-119">指定屬性值的最大長度。</span><span class="sxs-lookup"><span data-stu-id="219ed-119">Specifies the maximum length of the property value.</span></span>|<span data-ttu-id="219ed-120">`Binary`, `String`</span><span class="sxs-lookup"><span data-stu-id="219ed-120">`Binary`, `String`</span></span>|  
|`Nullable`|<span data-ttu-id="219ed-121">指定屬性是否可以有 null 值。</span><span class="sxs-lookup"><span data-stu-id="219ed-121">Specifies whether the property can have a null value.</span></span>|<span data-ttu-id="219ed-122">所有基底類型屬性</span><span class="sxs-lookup"><span data-stu-id="219ed-122">All primitive type properties</span></span>|  
|`Precision`|<span data-ttu-id="219ed-123">針對型別 `Decimal` 的屬性，指定屬性值可以擁有的位數。</span><span class="sxs-lookup"><span data-stu-id="219ed-123">For properties of type `Decimal`, specifies the number of digits a property value can have.</span></span> <span data-ttu-id="219ed-124">針對型別 `Time`、`DateTime` 和 `DateTimeOffset` 的屬性，指定屬性值秒數之小數點後的位數。</span><span class="sxs-lookup"><span data-stu-id="219ed-124">For properties of type `Time`, `DateTime`, and `DateTimeOffset`, specifies the number of digits for the fractional part of seconds of the property value.</span></span>|<span data-ttu-id="219ed-125">`DateTime`, `DateTimeOffset`, `Decimal`, `Time`,</span><span class="sxs-lookup"><span data-stu-id="219ed-125">`DateTime`, `DateTimeOffset`, `Decimal`, `Time`,</span></span>|  
|`Scale`|<span data-ttu-id="219ed-126">指定屬性值小數點右邊的位數。</span><span class="sxs-lookup"><span data-stu-id="219ed-126">Specifies the number of digits to the right of the decimal point for the property value.</span></span>|<span data-ttu-id="219ed-127">Decimal</span><span class="sxs-lookup"><span data-stu-id="219ed-127">Decimal</span></span>|  
|`Unicode`|<span data-ttu-id="219ed-128">指出屬性值是否儲存為 Unicode。</span><span class="sxs-lookup"><span data-stu-id="219ed-128">Indicates whether the property value is stored as Unicode.</span></span>|`String`|  
  
## <a name="example"></a><span data-ttu-id="219ed-129">範例</span><span class="sxs-lookup"><span data-stu-id="219ed-129">Example</span></span>  

 <span data-ttu-id="219ed-130">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="219ed-130">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="219ed-131">下列 CSDL 定義 `Book` 實體類型。</span><span class="sxs-lookup"><span data-stu-id="219ed-131">The following CSDL defines a `Book` entity type.</span></span> <span data-ttu-id="219ed-132">請注意，Facet 會實作為 XML 屬性。</span><span class="sxs-lookup"><span data-stu-id="219ed-132">Note that facets are implemented as XML attributes.</span></span> <span data-ttu-id="219ed-133">Facet 值表示不可將任何屬性設為 null，且 `Scale` 屬性的 `Precision` 和 `Revision` 皆分別設為 29。</span><span class="sxs-lookup"><span data-stu-id="219ed-133">The facet values indicate that no property can be set to null, and that the `Scale` and `Precision` of the `Revision` property are each set to 29.</span></span>  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## <a name="see-also"></a><span data-ttu-id="219ed-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="219ed-134">See also</span></span>

- [<span data-ttu-id="219ed-135">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="219ed-135">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="219ed-136">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="219ed-136">Entity Data Model</span></span>](entity-data-model.md)

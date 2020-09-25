---
title: 實體資料模型：命名空間
ms.date: 03/30/2017
ms.assetid: 98ab4226-bb9f-44e7-af46-61a9b1a4e47c
ms.openlocfilehash: 1e5f9527ec208c5650c68fe35bb758e0850b7700
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194826"
---
# <a name="entity-data-model-namespaces"></a><span data-ttu-id="49b05-102">實體資料模型：命名空間</span><span class="sxs-lookup"><span data-stu-id="49b05-102">Entity Data Model: Namespaces</span></span>

<span data-ttu-id="49b05-103">實體資料模型 (EDM) 中的命名空間是 [實體類型](entity-type.md)、 [複雜類型](complex-type.md)和 [關聯](association-type.md)的抽象容器。</span><span class="sxs-lookup"><span data-stu-id="49b05-103">A namespace in the Entity Data Model (EDM) is an abstract container for [entity types](entity-type.md), [complex types](complex-type.md), and [associations](association-type.md).</span></span> <span data-ttu-id="49b05-104">EDM 中的命名空間類似於程式設計語言中的命名空間：針對它們所包含的物件提供內容，並且提供方法讓名稱相同 (但包含在不同命名空間中) 的物件意義清楚。</span><span class="sxs-lookup"><span data-stu-id="49b05-104">Namespaces in the EDM are similar to namespaces in a programming language: they provide context for the objects that they contain and they provide a way to disambiguate objects that have the same name (but are contained in different namespaces).</span></span>  
  
## <a name="example"></a><span data-ttu-id="49b05-105">範例</span><span class="sxs-lookup"><span data-stu-id="49b05-105">Example</span></span>  

 <span data-ttu-id="49b05-106">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="49b05-106">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="49b05-107">下列 CSDL 程式碼使用命名空間來識別在不同概念模型中定義的型別。</span><span class="sxs-lookup"><span data-stu-id="49b05-107">The following CSDL code uses a namespace to identify a type that is defined in a different conceptual model.</span></span> <span data-ttu-id="49b05-108">此範例定義的實體類型 (`Publisher`) 具有從 `Address` 命名空間匯入的複雜類型屬性 (`ExtendedBooksModel`)。</span><span class="sxs-lookup"><span data-stu-id="49b05-108">The example defines an entity type (`Publisher`) that has a complex type property (`Address`) that is imported from the `ExtendedBooksModel` namespace.</span></span> <span data-ttu-id="49b05-109">請注意，`Using` 項目代表已匯入命名空間。</span><span class="sxs-lookup"><span data-stu-id="49b05-109">Note that the `Using` element indicates that a namespace has been imported.</span></span> <span data-ttu-id="49b05-110">亦請注意，`Address` 屬性的型別是利用其完整名稱 (`ExtendedBooksModel.Address`) 來定義，表示此型別是在 `ExtendedBooksModel` 命名空間中定義的。</span><span class="sxs-lookup"><span data-stu-id="49b05-110">Also note that the type of the `Address` property is defined by using its fully qualified name (`ExtendedBooksModel.Address`), indicating that this type is defined in the `ExtendedBooksModel` namespace.</span></span>  
  
 [!code-xml[EDM_Example_Model#ImportedNamespace](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books6.edmx#importednamespace)]  
  
## <a name="see-also"></a><span data-ttu-id="49b05-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49b05-111">See also</span></span>

- [<span data-ttu-id="49b05-112">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="49b05-112">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="49b05-113">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="49b05-113">Entity Data Model</span></span>](entity-data-model.md)

---
title: 模型宣告函式
ms.date: 03/30/2017
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
ms.openlocfilehash: fb30dd86c29d6a7fff6f2c71d5fd892326e1fda4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147849"
---
# <a name="model-declared-function"></a><span data-ttu-id="c584b-102">模型宣告函式</span><span class="sxs-lookup"><span data-stu-id="c584b-102">model-declared function</span></span>

<span data-ttu-id="c584b-103">模型宣告函式是在概念模型中宣告的函 *式* ，但不是在該概念模型中定義的函數。</span><span class="sxs-lookup"><span data-stu-id="c584b-103">A *model-declared function* is a function that is declared in a conceptual model, but is not defined in that conceptual model.</span></span> <span data-ttu-id="c584b-104">該函式可能是在裝載或儲存環境中定義的。</span><span class="sxs-lookup"><span data-stu-id="c584b-104">The function might be defined in the hosting or storage environment.</span></span> <span data-ttu-id="c584b-105">例如，模型宣告函式可能對應到在資料庫中定義的函式，因而在概念模型中公開伺服器端的功能。</span><span class="sxs-lookup"><span data-stu-id="c584b-105">For example, a model-declared function might be mapped to a function that is defined in a database, thus exposing server-side functionality in the conceptual model.</span></span>  
  
 <span data-ttu-id="c584b-106">模型宣告函式的宣告包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c584b-106">The declaration of a model-declared function contains the following information:</span></span>  
  
- <span data-ttu-id="c584b-107">函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c584b-107">The name of the function.</span></span> <span data-ttu-id="c584b-108">(必要)</span><span class="sxs-lookup"><span data-stu-id="c584b-108">(Required)</span></span>  
  
- <span data-ttu-id="c584b-109">傳回值的型別。</span><span class="sxs-lookup"><span data-stu-id="c584b-109">The type of the return value.</span></span> <span data-ttu-id="c584b-110">(選用)</span><span class="sxs-lookup"><span data-stu-id="c584b-110">(Optional)</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c584b-111">若未指定任何傳回值，則傳回型別為 void。</span><span class="sxs-lookup"><span data-stu-id="c584b-111">If no return value is specified, the return type is void.</span></span>  
  
- <span data-ttu-id="c584b-112">參數資訊，包括參數名稱和型別。</span><span class="sxs-lookup"><span data-stu-id="c584b-112">Parameter information, including parameter name and type.</span></span> <span data-ttu-id="c584b-113">(選用)</span><span class="sxs-lookup"><span data-stu-id="c584b-113">(Optional)</span></span>  
  
## <a name="example"></a><span data-ttu-id="c584b-114">範例</span><span class="sxs-lookup"><span data-stu-id="c584b-114">Example</span></span>  

 <span data-ttu-id="c584b-115">[ADO.NET Entity Framework](./ef/index.md)會使用 (DSL) 稱為概念結構定義語言 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) 來定義概念模型的特定領域語言。</span><span class="sxs-lookup"><span data-stu-id="c584b-115">The [ADO.NET Entity Framework](./ef/index.md) uses a domain-specific language (DSL) called conceptual schema definition language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) to define conceptual models.</span></span> <span data-ttu-id="c584b-116">在 CSDL 中，模型宣告函式的其中一個實作為函式匯入 (使用 [FunctionImport 元素](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#functionimport-element-csdl)) 。</span><span class="sxs-lookup"><span data-stu-id="c584b-116">In CSDL, one implementation of a model-declared function is a function import (using the [FunctionImport element](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#functionimport-element-csdl)).</span></span> <span data-ttu-id="c584b-117">下列 CSDL 定義具有函式匯入定義的實體容器。</span><span class="sxs-lookup"><span data-stu-id="c584b-117">The following CSDL defines an entity container with a function import definition.</span></span> <span data-ttu-id="c584b-118">請注意，由於沒有指定傳回型別，因此該函式的傳回型別為 void。</span><span class="sxs-lookup"><span data-stu-id="c584b-118">Note that the return type for the function is void since no return type is specified.</span></span>  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## <a name="see-also"></a><span data-ttu-id="c584b-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c584b-119">See also</span></span>

- [<span data-ttu-id="c584b-120">實體資料模型索引鍵概念</span><span class="sxs-lookup"><span data-stu-id="c584b-120">Entity Data Model Key Concepts</span></span>](entity-data-model-key-concepts.md)
- [<span data-ttu-id="c584b-121">實體資料模型</span><span class="sxs-lookup"><span data-stu-id="c584b-121">Entity Data Model</span></span>](entity-data-model.md)

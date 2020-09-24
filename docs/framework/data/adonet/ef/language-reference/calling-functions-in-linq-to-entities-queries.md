---
title: 在 LINQ to Entities 查詢中呼叫函式
description: 使用這些文章來查看 EntityFunctions 和 SqlFunctions 類別如何提供標準和資料庫函式的存取權，做為 Entity Framework 的一部分。
ms.date: 03/30/2017
ms.assetid: 12a525a9-727c-4464-a0c7-71a0ef541792
ms.openlocfilehash: 8c771c93e0c3ed82f3ad550613dd855fd06b6f48
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177484"
---
# <a name="calling-functions-in-linq-to-entities-queries"></a><span data-ttu-id="f0a1a-103">在 LINQ to Entities 查詢中呼叫函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-103">Calling Functions in LINQ to Entities Queries</span></span>

<span data-ttu-id="f0a1a-104">本章節的主題描述如何使用呼叫 LINQ to Entities 查詢中的函式。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-104">The topics in this section describe how to call functions in LINQ to Entities queries.</span></span>  
  
 <span data-ttu-id="f0a1a-105"><xref:System.Data.Objects.EntityFunctions> 與 <xref:System.Data.Objects.SqlClient.SqlFunctions> 類別可讓您存取標準函式與資料庫函式，這些函式是 Entity Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-105">The <xref:System.Data.Objects.EntityFunctions> and <xref:System.Data.Objects.SqlClient.SqlFunctions> classes provide access to canonical and database functions as part of the Entity Framework.</span></span> <span data-ttu-id="f0a1a-106">如需詳細資訊，請參閱 [如何：呼叫標準](how-to-call-canonical-functions.md) 函式和 [如何：呼叫資料庫](how-to-call-database-functions.md)函式。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-106">For more information, see [How to: Call Canonical Functions](how-to-call-canonical-functions.md) and [How to: Call Database Functions](how-to-call-database-functions.md).</span></span>  
  
 <span data-ttu-id="f0a1a-107">呼叫自訂函式的程序需要三個基本步驟：</span><span class="sxs-lookup"><span data-stu-id="f0a1a-107">The process for calling a custom function requires three basic steps:</span></span>  
  
1. <span data-ttu-id="f0a1a-108">定義概念模型中的函式或宣告儲存模型中的函式。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-108">Define a function in your conceptual model or declare a function in your storage model.</span></span>  
  
2. <span data-ttu-id="f0a1a-109">使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 將方法加入至應用程式，並將它對應至模型中的函式。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-109">Add a method to your application and map it to the function in the model with an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>.</span></span>  
  
3. <span data-ttu-id="f0a1a-110">呼叫 LINQ to Entities 查詢中的函式。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-110">Call the function in a LINQ to Entities query.</span></span>  
  
 <span data-ttu-id="f0a1a-111">如需詳細資料，請參閱本節中的主題。</span><span class="sxs-lookup"><span data-stu-id="f0a1a-111">For more information, see the topics in this section.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="f0a1a-112">本節內容</span><span class="sxs-lookup"><span data-stu-id="f0a1a-112">In This Section</span></span>  

 [<span data-ttu-id="f0a1a-113">如何：呼叫標準函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-113">How to: Call Canonical Functions</span></span>](how-to-call-canonical-functions.md)  
  
 [<span data-ttu-id="f0a1a-114">如何：呼叫資料庫函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-114">How to: Call Database Functions</span></span>](how-to-call-database-functions.md)  
  
 [<span data-ttu-id="f0a1a-115">如何：呼叫自訂資料庫函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-115">How to: Call Custom Database Functions</span></span>](how-to-call-custom-database-functions.md)  
  
 [<span data-ttu-id="f0a1a-116">如何：在查詢中呼叫模型定義函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-116">How to: Call Model-Defined Functions in Queries</span></span>](how-to-call-model-defined-functions-in-queries.md)  
  
 [<span data-ttu-id="f0a1a-117">如何：將模型定義函式當做物件方法來呼叫</span><span class="sxs-lookup"><span data-stu-id="f0a1a-117">How to: Call Model-Defined Functions as Object Methods</span></span>](how-to-call-model-defined-functions-as-object-methods.md)  
  
## <a name="see-also"></a><span data-ttu-id="f0a1a-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f0a1a-118">See also</span></span>

- [<span data-ttu-id="f0a1a-119">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="f0a1a-119">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
- [<span data-ttu-id="f0a1a-120">標準函式</span><span class="sxs-lookup"><span data-stu-id="f0a1a-120">Canonical Functions</span></span>](canonical-functions.md)
- <span data-ttu-id="f0a1a-121">[.edmx 檔概觀](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="f0a1a-121">[.edmx File Overview](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span></span>
- <span data-ttu-id="f0a1a-122">[HOW TO：在概念模型中定義自訂函式](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="f0a1a-122">[How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))</span></span>

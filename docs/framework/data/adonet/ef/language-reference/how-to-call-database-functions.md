---
title: 如何：呼叫資料庫函式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 79038efa-15bf-464a-83e2-35fe145252ce
ms.openlocfilehash: a4cf77000af56ed2a6445beaef2d7856486b85db
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173662"
---
# <a name="how-to-call-database-functions"></a><span data-ttu-id="646fd-102">如何：呼叫資料庫函式</span><span class="sxs-lookup"><span data-stu-id="646fd-102">How to: Call Database Functions</span></span>

<span data-ttu-id="646fd-103"><xref:System.Data.Objects.SqlClient.SqlFunctions> 類別包含公開 SQL Server 函式以用於 LINQ to Entities 查詢的方法。</span><span class="sxs-lookup"><span data-stu-id="646fd-103">The <xref:System.Data.Objects.SqlClient.SqlFunctions> class contains methods that expose SQL Server functions to use in LINQ to Entities queries.</span></span> <span data-ttu-id="646fd-104">使用 LINQ to Entities 中的 <xref:System.Data.Objects.SqlClient.SqlFunctions> 方法時，對應的資料庫函式會在資料庫中執行。</span><span class="sxs-lookup"><span data-stu-id="646fd-104">When you use <xref:System.Data.Objects.SqlClient.SqlFunctions> methods in LINQ to Entities queries, the corresponding database functions are executed in the database.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="646fd-105">可直接叫用的資料庫函式，會執行值集的計算，然後傳回單一值 (亦稱為彙總資料庫函式)。</span><span class="sxs-lookup"><span data-stu-id="646fd-105">Database functions that perform a calculation on a set of values and return a single value (also known as aggregate database functions) can be directly invoked.</span></span> <span data-ttu-id="646fd-106">呼叫的其他標準函式則做為 LINQ to Entities 查詢的一部份。</span><span class="sxs-lookup"><span data-stu-id="646fd-106">Other canonical functions can only be called as part of a LINQ to Entities query.</span></span> <span data-ttu-id="646fd-107">若要直接呼叫彙總函式，您必須將 <xref:System.Data.Objects.ObjectQuery%601> 傳遞至函式。</span><span class="sxs-lookup"><span data-stu-id="646fd-107">To call an aggregate function directly, you must pass an <xref:System.Data.Objects.ObjectQuery%601> to the function.</span></span> <span data-ttu-id="646fd-108">如需詳細資訊，請參閱下列第二個範例。</span><span class="sxs-lookup"><span data-stu-id="646fd-108">For more information, see the second example below.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="646fd-109"><xref:System.Data.Objects.SqlClient.SqlFunctions> 類別中的方法專屬於 SQL Server 函式。</span><span class="sxs-lookup"><span data-stu-id="646fd-109">The methods in the <xref:System.Data.Objects.SqlClient.SqlFunctions> class are specific to SQL Server functions.</span></span> <span data-ttu-id="646fd-110">公開資料庫函式的類似類別可透過其他提供者提供。</span><span class="sxs-lookup"><span data-stu-id="646fd-110">Similar classes that expose database functions may be available through other providers.</span></span>  
  
## <a name="example"></a><span data-ttu-id="646fd-111">範例</span><span class="sxs-lookup"><span data-stu-id="646fd-111">Example</span></span>  

 <span data-ttu-id="646fd-112">下列範例會使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。</span><span class="sxs-lookup"><span data-stu-id="646fd-112">The following example uses the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).</span></span> <span data-ttu-id="646fd-113">範例執行 LINQ to Entities 查詢時，會使用 <xref:System.Data.Objects.SqlClient.SqlFunctions.CharIndex%2A> 方法，傳回姓氏以 "Si" 為開頭的所有連絡人：</span><span class="sxs-lookup"><span data-stu-id="646fd-113">The example executes a LINQ to Entities query that uses the <xref:System.Data.Objects.SqlClient.SqlFunctions.CharIndex%2A> method to return all contacts whose last name starts with "Si":</span></span>  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#3)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#3)]  
  
## <a name="example"></a><span data-ttu-id="646fd-114">範例</span><span class="sxs-lookup"><span data-stu-id="646fd-114">Example</span></span>  

 <span data-ttu-id="646fd-115">下列範例會使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。</span><span class="sxs-lookup"><span data-stu-id="646fd-115">The following example uses the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).</span></span> <span data-ttu-id="646fd-116">範例直接呼叫彙總 <xref:System.Data.Objects.SqlClient.SqlFunctions.ChecksumAggregate%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="646fd-116">The example calls the aggregate <xref:System.Data.Objects.SqlClient.SqlFunctions.ChecksumAggregate%2A> method directly.</span></span> <span data-ttu-id="646fd-117">請注意，<xref:System.Data.Objects.ObjectQuery%601> 已傳遞至函式，函式允許其接受呼叫時，不必成為 LINQ to Entities 查詢的一部份。</span><span class="sxs-lookup"><span data-stu-id="646fd-117">Note that an <xref:System.Data.Objects.ObjectQuery%601> is passed to the function, which allows it to be called without being part of a LINQ to Entities query.</span></span>  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#4)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="646fd-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="646fd-118">See also</span></span>

- [<span data-ttu-id="646fd-119">在 LINQ to Entities 查詢中呼叫函式</span><span class="sxs-lookup"><span data-stu-id="646fd-119">Calling Functions in LINQ to Entities Queries</span></span>](calling-functions-in-linq-to-entities-queries.md)
- [<span data-ttu-id="646fd-120">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="646fd-120">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)

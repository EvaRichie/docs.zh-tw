---
title: 以方法為基礎的查詢語法範例：項目運算子 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eedf2fbd-f407-4f62-bb1a-c00eb001b1dd
ms.openlocfilehash: 669c6a34d1179caf4ec40eb8db559bdfdc9fc7f5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91189275"
---
# <a name="method-based-query-syntax-examples-element-operators-linq-to-dataset"></a><span data-ttu-id="8450d-102">以方法為基礎的查詢語法範例：項目運算子 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="8450d-102">Method-Based Query Syntax Examples: Element Operators (LINQ to DataSet)</span></span>

<span data-ttu-id="8450d-103">此主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.First%2A> 和 <xref:System.Linq.Enumerable.ElementAt%2A> 方法並搭配查詢運算式語法來取得 <xref:System.Data.DataRow> 中的 <xref:System.Data.DataSet> 項目。</span><span class="sxs-lookup"><span data-stu-id="8450d-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.First%2A> and <xref:System.Linq.Enumerable.ElementAt%2A> methods to get <xref:System.Data.DataRow> elements from a <xref:System.Data.DataSet> using the query expression syntax.</span></span>  
  
 <span data-ttu-id="8450d-104">`FillDataSet`這些範例中使用的方法是在將[資料載入資料集](loading-data-into-a-dataset.md)時指定。</span><span class="sxs-lookup"><span data-stu-id="8450d-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="8450d-105">此主題中的範例將使用 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="8450d-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="8450d-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="8450d-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
[!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
[!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]

 <span data-ttu-id="8450d-107">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 LINQ to DataSet 專案](how-to-create-a-linq-to-dataset-project-in-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="8450d-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="elementat"></a><span data-ttu-id="8450d-108">ElementAt</span><span class="sxs-lookup"><span data-stu-id="8450d-108">ElementAt</span></span>  
  
### <a name="example"></a><span data-ttu-id="8450d-109">範例</span><span class="sxs-lookup"><span data-stu-id="8450d-109">Example</span></span>  

 <span data-ttu-id="8450d-110">這則範例會使用 <xref:System.Linq.Enumerable.ElementAt%2A> 方法來擷取 `PostalCode` == "M4B 1V7" 的第五筆地址。</span><span class="sxs-lookup"><span data-stu-id="8450d-110">This example uses the <xref:System.Linq.Enumerable.ElementAt%2A> method to retrieve the fifth address where `PostalCode` == "M4B 1V7".</span></span>  
  
[!code-csharp[DP LINQ to DataSet Examples#ElementAt](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#elementat)]
[!code-vb[DP LINQ to DataSet Examples#ElementAt](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#elementat)]
  
## <a name="first"></a><span data-ttu-id="8450d-111">First</span><span class="sxs-lookup"><span data-stu-id="8450d-111">First</span></span>  
  
### <a name="example"></a><span data-ttu-id="8450d-112">範例</span><span class="sxs-lookup"><span data-stu-id="8450d-112">Example</span></span>  

 <span data-ttu-id="8450d-113">這則範例會使用 <xref:System.Linq.Enumerable.First%2A> 方法來傳回名字為 'Brooke' 的第一位連絡人。</span><span class="sxs-lookup"><span data-stu-id="8450d-113">This example uses the <xref:System.Linq.Enumerable.First%2A> method to return the first contact whose first name is 'Brooke'.</span></span>  
  
[!code-csharp[DP LINQ to DataSet Examples#FirstSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#firstsimple)]
[!code-vb[DP LINQ to DataSet Examples#FirstSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#firstsimple)]
  
## <a name="see-also"></a><span data-ttu-id="8450d-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8450d-114">See also</span></span>

- [<span data-ttu-id="8450d-115">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="8450d-115">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="8450d-116">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="8450d-116">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="8450d-117">標準查詢運算子概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="8450d-117">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="8450d-118">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8450d-118">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)

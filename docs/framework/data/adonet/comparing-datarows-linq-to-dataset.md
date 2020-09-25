---
title: 比較 DataRow (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8fe0eadf-297b-487c-8d4b-7816753c2883
ms.openlocfilehash: 8cce52734c83e42312d71806d4151ef21e4df0ba
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203796"
---
# <a name="comparing-datarows-linq-to-dataset"></a><span data-ttu-id="c1cc5-102">比較 DataRow (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="c1cc5-102">Comparing DataRows (LINQ to DataSet)</span></span>

<span data-ttu-id="c1cc5-103"> (LINQ) 的語言整合式查詢定義了不同的集合運算子，以比較來源元素來查看它們是否相等。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-103">Language-Integrated Query (LINQ) defines various set operators to compare source elements to see if they are equal.</span></span> <span data-ttu-id="c1cc5-104">LINQ 提供下列 set 運算子：</span><span class="sxs-lookup"><span data-stu-id="c1cc5-104">LINQ provides the following set operators:</span></span>  
  
- <xref:System.Linq.Enumerable.Distinct%2A>  
  
- <xref:System.Linq.Enumerable.Union%2A>  
  
- <xref:System.Linq.Enumerable.Intersect%2A>  
  
- <xref:System.Linq.Enumerable.Except%2A>  
  
 <span data-ttu-id="c1cc5-105">這些運算子會針對每個項目集合呼叫 <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> 和 <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> 方法，藉以比較來源項目。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-105">These operators compare source elements by calling the <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> and <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> methods on each collection of elements.</span></span> <span data-ttu-id="c1cc5-106">在 <xref:System.Data.DataRow> 的情況中，這些運算子會執行參考比較，但是這通常不是表格式資料之設定作業的理想行為。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-106">In the case of a <xref:System.Data.DataRow>, these operators perform a reference comparison, which is generally not the ideal behavior for set operations over tabular data.</span></span> <span data-ttu-id="c1cc5-107">若為設定作業，您通常會想要判斷項目值是否相等，而非項目參考。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-107">For set operations, you usually want to determine whether the element values are equal and not the element references.</span></span> <span data-ttu-id="c1cc5-108">因此， <xref:System.Data.DataRowComparer> 類別已新增至 LINQ to DataSet。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-108">Therefore, the <xref:System.Data.DataRowComparer> class has been added to LINQ to DataSet.</span></span> <span data-ttu-id="c1cc5-109">這個類別可用來比較資料列值。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-109">This class can be used to compare row values.</span></span>  
  
 <span data-ttu-id="c1cc5-110"><xref:System.Data.DataRowComparer> 類別包含 <xref:System.Data.DataRow> 的值比較實作 (Implementation)，所以這個類別可用於 <xref:System.Linq.Enumerable.Distinct%2A> 等設定作業。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-110">The <xref:System.Data.DataRowComparer> class contains a value comparison implementation for <xref:System.Data.DataRow>, so this class can be used for set operations such as <xref:System.Linq.Enumerable.Distinct%2A>.</span></span> <span data-ttu-id="c1cc5-111">您無法直接具現化 (Instantiated) 這個類別，而必須使用 <xref:System.Data.DataRowComparer.Default%2A> 屬性來傳回 <xref:System.Data.DataRowComparer%601> 的執行個體 (Instance)。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-111">This class cannot be directly instantiated; instead, the <xref:System.Data.DataRowComparer.Default%2A> property must be used to return an instance of the <xref:System.Data.DataRowComparer%601>.</span></span> <span data-ttu-id="c1cc5-112">然後，系統會呼叫 <xref:System.Data.DataRowComparer%601.Equals%2A> 方法並將要比較的兩個 <xref:System.Data.DataRow> 物件當做輸入參數傳入。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-112">The <xref:System.Data.DataRowComparer%601.Equals%2A> method is then called and the two <xref:System.Data.DataRow> objects to be compared are passed in as input parameters.</span></span> <span data-ttu-id="c1cc5-113">如果這兩個 <xref:System.Data.DataRowComparer%601.Equals%2A> 物件中的已排序資料行值組相等，`true` 方法就會傳回 <xref:System.Data.DataRow>，否則它會傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-113">The <xref:System.Data.DataRowComparer%601.Equals%2A> method returns `true` if the ordered set of column values in both <xref:System.Data.DataRow> objects are equal; otherwise, `false`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c1cc5-114">範例</span><span class="sxs-lookup"><span data-stu-id="c1cc5-114">Example</span></span>  

 <span data-ttu-id="c1cc5-115">這則範例會使用 `Intersect` 來傳回在這兩份資料表中都出現的連絡人。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-115">This example uses `Intersect` to return contacts that appear in both tables.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#intersect2)]
 [!code-vb[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#intersect2)]  
  
### <a name="example"></a><span data-ttu-id="c1cc5-116">範例</span><span class="sxs-lookup"><span data-stu-id="c1cc5-116">Example</span></span>  

 <span data-ttu-id="c1cc5-117">下列範例會比較兩個資料列並取得其雜湊程式碼。</span><span class="sxs-lookup"><span data-stu-id="c1cc5-117">The following example compares two rows and gets their hash codes.</span></span>  
  
 [!code-vb[DP LINQ to DataSet Examples#CompareDifferentRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#comparedifferentrows)]  
  
## <a name="see-also"></a><span data-ttu-id="c1cc5-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c1cc5-118">See also</span></span>

- <xref:System.Data.DataRowComparer>
- [<span data-ttu-id="c1cc5-119">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="c1cc5-119">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="c1cc5-120">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="c1cc5-120">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)

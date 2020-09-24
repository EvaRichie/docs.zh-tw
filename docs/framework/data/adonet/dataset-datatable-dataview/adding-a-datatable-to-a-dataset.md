---
title: 將 DataTable 加入至資料集
description: 請參閱此範例程式碼，以瞭解如何建立 DataTable 物件，並將它們加入至 ADO.NET 中的現有資料集。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 556d29a3-8fc9-4e38-b3ee-c188f7e7b155
ms.openlocfilehash: 6a5e3a89870b3959a6ac042b93414694e8a6cc1c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164892"
---
# <a name="adding-a-datatable-to-a-dataset"></a><span data-ttu-id="4d671-103">將 DataTable 加入至資料集</span><span class="sxs-lookup"><span data-stu-id="4d671-103">Adding a DataTable to a DataSet</span></span>

<span data-ttu-id="4d671-104">ADO.NET 可讓您建立 <xref:System.Data.DataTable> 物件，並將它們加入現有的 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="4d671-104">ADO.NET enables you to create <xref:System.Data.DataTable> objects and add them to an existing <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="4d671-105">您可以使用 <xref:System.Data.DataTable> 和 <xref:System.Data.DataTable.PrimaryKey%2A> 屬性，為 <xref:System.Data.DataColumn.Unique%2A> 設定條件約束 (Constraint) 資訊。</span><span class="sxs-lookup"><span data-stu-id="4d671-105">You can set constraint information for a <xref:System.Data.DataTable> by using the <xref:System.Data.DataTable.PrimaryKey%2A> and <xref:System.Data.DataColumn.Unique%2A> properties.</span></span>  
  
## <a name="example"></a><span data-ttu-id="4d671-106">範例</span><span class="sxs-lookup"><span data-stu-id="4d671-106">Example</span></span>  

 <span data-ttu-id="4d671-107">下列範例會建構 <xref:System.Data.DataSet>、將新的 <xref:System.Data.DataTable> 物件加入至 <xref:System.Data.DataSet>，然後再將三個 <xref:System.Data.DataColumn> 物件加入至資料表。</span><span class="sxs-lookup"><span data-stu-id="4d671-107">The following example constructs a <xref:System.Data.DataSet>, adds a new <xref:System.Data.DataTable> object to the <xref:System.Data.DataSet>, and then adds three <xref:System.Data.DataColumn> objects to the table.</span></span> <span data-ttu-id="4d671-108">最後，程式碼會將一個資料行設定為主索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="4d671-108">Finally, the code sets one column as the primary key column.</span></span>  
  
 [!code-csharp[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/VB/source.vb#1)]  
  
## <a name="case-sensitivity"></a><span data-ttu-id="4d671-109">區分大小寫</span><span class="sxs-lookup"><span data-stu-id="4d671-109">Case Sensitivity</span></span>  

 <span data-ttu-id="4d671-110"><xref:System.Data.DataSet> 中可能有兩個或兩個以上具有相同名稱，但不同大小寫的資料表或關聯。</span><span class="sxs-lookup"><span data-stu-id="4d671-110">Two or more tables or relations with the same name, but different casing, can exist in a <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="4d671-111">在這種情況下，按照資料表和關聯名稱進行參考時是區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="4d671-111">In such cases, references by name to tables and relations are case sensitive.</span></span> <span data-ttu-id="4d671-112">例如，如果 <xref:System.Data.DataSet> **資料集** 包含資料表 **Table1** 和 **table1**，您會依名稱將 **table1** 參考為 **資料集。資料表 ["Table1"]** 和 **table1** 做為 **資料集。資料表 ["table1"]**。</span><span class="sxs-lookup"><span data-stu-id="4d671-112">For example, if the <xref:System.Data.DataSet> **dataSet** contains tables **Table1** and **table1**, you would reference **Table1** by name as **dataSet.Tables["Table1"]**, and **table1** as **dataSet.Tables["table1"]**.</span></span> <span data-ttu-id="4d671-113">嘗試參考其中一個資料表做為 **資料集。資料表 ["TABLE1"]** 會產生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4d671-113">Attempting to reference either of the tables as **dataSet.Tables["TABLE1"]** would generate an exception.</span></span>  
  
 <span data-ttu-id="4d671-114">如果只有一個具有特定名稱的資料表或關聯，則不適用區分大小寫規則。</span><span class="sxs-lookup"><span data-stu-id="4d671-114">The case-sensitivity behavior does not apply if only one table or relation has a particular name.</span></span> <span data-ttu-id="4d671-115">例如，如果 <xref:System.Data.DataSet> 只有 **Table1**，您可以使用資料集來參考它 **。資料表 ["Table1"]**。</span><span class="sxs-lookup"><span data-stu-id="4d671-115">For example, if the <xref:System.Data.DataSet> has only **Table1**, you can reference it using **dataSet.Tables["TABLE1"]**.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4d671-116"><xref:System.Data.DataSet.CaseSensitive%2A> 的 <xref:System.Data.DataSet> 屬性不會影響這項行為。</span><span class="sxs-lookup"><span data-stu-id="4d671-116">The <xref:System.Data.DataSet.CaseSensitive%2A> property of the <xref:System.Data.DataSet> does not affect this behavior.</span></span> <span data-ttu-id="4d671-117"><xref:System.Data.DataSet.CaseSensitive%2A> 屬性會套用至 <xref:System.Data.DataSet> 內的資料，並影響排序、搜尋、篩選、強制執行條件約束等方面。</span><span class="sxs-lookup"><span data-stu-id="4d671-117">The <xref:System.Data.DataSet.CaseSensitive%2A> property applies to the data in the <xref:System.Data.DataSet> and affects sorting, searching, filtering, enforcing constraints, and so on.</span></span>  
  
## <a name="namespace-support"></a><span data-ttu-id="4d671-118">命名空間支援 </span><span class="sxs-lookup"><span data-stu-id="4d671-118">Namespace Support</span></span>  

 <span data-ttu-id="4d671-119">在 2.0 之前的 ADO.NET 版本中，兩個資料表不能有相同的名稱，即使它們在不同的命名空間也一樣。</span><span class="sxs-lookup"><span data-stu-id="4d671-119">In versions of ADO.NET earlier than 2.0, two tables could not have the same name, even if they were in different namespaces.</span></span> <span data-ttu-id="4d671-120">ADO.NET 2.0 已移除這項限制。</span><span class="sxs-lookup"><span data-stu-id="4d671-120">This limitation was removed in ADO.NET 2.0.</span></span> <span data-ttu-id="4d671-121"><xref:System.Data.DataSet> 可能會包含兩個 <xref:System.Data.DataTable.TableName%2A> 屬性值相同，但 <xref:System.Data.DataTable.Namespace%2A> 屬性值不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="4d671-121">A <xref:System.Data.DataSet> can contain two tables that have the same <xref:System.Data.DataTable.TableName%2A> property value but different <xref:System.Data.DataTable.Namespace%2A> property values.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4d671-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4d671-122">See also</span></span>

- [<span data-ttu-id="4d671-123">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="4d671-123">DataSets, DataTables, and DataViews</span></span>](index.md)
- <span data-ttu-id="4d671-124">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="4d671-124">[ADO.NET Overview](../ado-net-overview.md)</span></span>

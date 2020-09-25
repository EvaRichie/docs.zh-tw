---
title: 查詢 DataView 中的 DataRowView 集合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b9070a12-1094-44d6-bb87-a23b50bcb0af
ms.openlocfilehash: 5757079bbc0ef8c498ea1db1a88f6b356ab0409e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172745"
---
# <a name="querying-the-datarowview-collection-in-a-dataview"></a><span data-ttu-id="4e8ad-102">查詢 DataView 中的 DataRowView 集合</span><span class="sxs-lookup"><span data-stu-id="4e8ad-102">Querying the DataRowView Collection in a DataView</span></span>

<span data-ttu-id="4e8ad-103"><xref:System.Data.DataView> 公開可列舉之 <xref:System.Data.DataRowView> 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-103">The <xref:System.Data.DataView> exposes an enumerable collection of <xref:System.Data.DataRowView> objects.</span></span> <span data-ttu-id="4e8ad-104"><xref:System.Data.DataRowView> 代表 <xref:System.Data.DataRow> 的自訂檢視並會在控制項中顯示該 <xref:System.Data.DataRow> 的特定版本。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-104"><xref:System.Data.DataRowView> represents a customized view of a <xref:System.Data.DataRow> and displays a specific version of that <xref:System.Data.DataRow> in a control.</span></span> <span data-ttu-id="4e8ad-105">只有一個 <xref:System.Data.DataRow> 的版本能透過控制項顯示，例如 <xref:System.Windows.Forms.DataGridView>。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-105">Only one version of a <xref:System.Data.DataRow> can be displayed through a control, such as a <xref:System.Windows.Forms.DataGridView>.</span></span> <span data-ttu-id="4e8ad-106">您可以透過 <xref:System.Data.DataRow> 的 <xref:System.Data.DataRowView> 屬性，存取 <xref:System.Data.DataRowView.Row%2A> 公開的 <xref:System.Data.DataRowView>。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-106">You can access the <xref:System.Data.DataRow> that is exposed by the <xref:System.Data.DataRowView> through the <xref:System.Data.DataRowView.Row%2A> property of the <xref:System.Data.DataRowView>.</span></span> <span data-ttu-id="4e8ad-107">使用 <xref:System.Data.DataRowView> 檢視值時，<xref:System.Data.DataView.RowStateFilter%2A> 屬性會判斷要公開的是哪一個基礎 <xref:System.Data.DataRow> 的資料列版本。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-107">When you view values by using a <xref:System.Data.DataRowView>, the <xref:System.Data.DataView.RowStateFilter%2A> property determines which row version of the underlying <xref:System.Data.DataRow> is exposed.</span></span> <span data-ttu-id="4e8ad-108">如需使用存取不同資料列版本的詳細資訊 <xref:System.Data.DataRow> ，請參閱資料 [列狀態和資料列版本](./dataset-datatable-dataview/row-states-and-row-versions.md)。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-108">For information about accessing different row versions using a <xref:System.Data.DataRow>, see [Row States and Row Versions](./dataset-datatable-dataview/row-states-and-row-versions.md).</span></span> <span data-ttu-id="4e8ad-109">因為 <xref:System.Data.DataRowView> 公開的物件集合是可列舉的，所以 <xref:System.Data.DataView> 您可以使用 LINQ to DataSet 來進行查詢。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-109">Because the collection of <xref:System.Data.DataRowView> objects exposed by the <xref:System.Data.DataView> is enumerable, you can use LINQ to DataSet to query over it.</span></span>  
  
 <span data-ttu-id="4e8ad-110">下列範例會查詢 `Product` 資料表中以紅色顯示的產品並根據該查詢建立資料表。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-110">The following example queries the `Product` table for red-colored products and creates a table from that query.</span></span> <span data-ttu-id="4e8ad-111"><xref:System.Data.DataView> 會根據資料表建立並且 <xref:System.Data.DataView.RowStateFilter%2A> 屬性會設為在刪除和修改的資料行進行篩選。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-111">A <xref:System.Data.DataView> is created from the table and the <xref:System.Data.DataView.RowStateFilter%2A> property is set to filter on deleted and modified rows.</span></span> <span data-ttu-id="4e8ad-112">接著就會使用 <xref:System.Data.DataView> 做為 LINQ 查詢中的來源，而已經修改和刪除的 <xref:System.Data.DataRowView> 物件會繫結至 <xref:System.Windows.Forms.DataGridView> 控制項。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-112">The <xref:System.Data.DataView> is then used as a source in a LINQ query, and the <xref:System.Data.DataRowView> objects that have been modified and deleted are bound to a <xref:System.Windows.Forms.DataGridView> control.</span></span>  
  
 [!code-csharp[DP DataView Samples#QueryDataView2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview2)]
 [!code-vb[DP DataView Samples#QueryDataView2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview2)]  
  
 <span data-ttu-id="4e8ad-113">下列範例會從繫結至 <xref:System.Windows.Forms.DataGridView> 控制項的檢視建立產品資料表。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-113">The following example creates a table of products from a view that is bound to a <xref:System.Windows.Forms.DataGridView> control.</span></span> <span data-ttu-id="4e8ad-114">針對以紅色顯示的產品查詢會在 <xref:System.Data.DataView> 中進行，並且排序後的結果會繫結至 <xref:System.Windows.Forms.DataGridView> 控制項。</span><span class="sxs-lookup"><span data-stu-id="4e8ad-114">The <xref:System.Data.DataView> is queried for red-colored products and the ordered results are bound to a <xref:System.Windows.Forms.DataGridView> control.</span></span>  
  
 [!code-csharp[DP DataView Samples#QueryDataView1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview1)]
 [!code-vb[DP DataView Samples#QueryDataView1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview1)]  
  
## <a name="see-also"></a><span data-ttu-id="4e8ad-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4e8ad-115">See also</span></span>

- [<span data-ttu-id="4e8ad-116">資料繫結和 LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="4e8ad-116">Data Binding and LINQ to DataSet</span></span>](data-binding-and-linq-to-dataset.md)

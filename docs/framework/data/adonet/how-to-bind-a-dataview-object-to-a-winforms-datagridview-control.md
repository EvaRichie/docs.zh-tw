---
title: 作法：將 DataView 物件繫結至 Windows Forms DataGridView 控制項
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2b73d60a-6049-446a-85a7-3e5a68b183e2
ms.openlocfilehash: cbae5453be485896e27a5039ece20bb3bcec9913
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556976"
---
# <a name="how-to-bind-a-dataview-object-to-a-windows-forms-datagridview-control"></a><span data-ttu-id="3094e-102">作法：將 DataView 物件繫結至 Windows Forms DataGridView 控制項</span><span class="sxs-lookup"><span data-stu-id="3094e-102">How to: Bind a DataView Object to a Windows Forms DataGridView Control</span></span>
<span data-ttu-id="3094e-103"><xref:System.Windows.Forms.DataGridView> 控制項以表格式顯示資料，是一項功能強大、有彈性的方式。</span><span class="sxs-lookup"><span data-stu-id="3094e-103">The <xref:System.Windows.Forms.DataGridView> control provides a powerful and flexible way to display data in a tabular format.</span></span> <span data-ttu-id="3094e-104"><xref:System.Windows.Forms.DataGridView> 控制項支援標準的 Windows Form 資料繫結模型，因此它將繫結至 <xref:System.Data.DataView> 和各種其他資料來源。</span><span class="sxs-lookup"><span data-stu-id="3094e-104">The <xref:System.Windows.Forms.DataGridView> control supports the standard Windows Forms data binding model, so it will bind to <xref:System.Data.DataView> and a variety of other data sources.</span></span> <span data-ttu-id="3094e-105">不過，在大部分情況下，您會繫結至 <xref:System.Windows.Forms.BindingSource> 元件，以便管理與資料來源互動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3094e-105">In most situations, however, you will bind to a <xref:System.Windows.Forms.BindingSource> component that will manage the details of interacting with the data source.</span></span>  
  
 <span data-ttu-id="3094e-106">如需控制項的詳細資訊 <xref:System.Windows.Forms.DataGridView> ，請參閱 [DataGridView 控制項總覽](/dotnet/desktop/winforms/controls/datagridview-control-overview-windows-forms)。</span><span class="sxs-lookup"><span data-stu-id="3094e-106">For more information about the <xref:System.Windows.Forms.DataGridView> control, see [DataGridView Control Overview](/dotnet/desktop/winforms/controls/datagridview-control-overview-windows-forms).</span></span>  
  
### <a name="to-connect-a-datagridview-control-to-a-dataview"></a><span data-ttu-id="3094e-107">若要將 DataGridView 控制項連接至 DataView</span><span class="sxs-lookup"><span data-stu-id="3094e-107">To connect a DataGridView control to a DataView</span></span>  
  
1. <span data-ttu-id="3094e-108">實作一種方法來處理從資料庫中擷取資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3094e-108">Implement a method to handle the details of retrieving data from a database.</span></span> <span data-ttu-id="3094e-109">下列程式碼範例會實作 `GetData` 方法，而此方法會初始化 <xref:System.Data.SqlClient.SqlDataAdapter> 元件並用它來填入 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="3094e-109">The following code example implements a `GetData` method that initializes a <xref:System.Data.SqlClient.SqlDataAdapter> component and uses it to fill a <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="3094e-110">請務必將 `connectionString` 變數設定為適用於您資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="3094e-110">Be sure to set the `connectionString` variable to a value that is appropriate for your database.</span></span> <span data-ttu-id="3094e-111">您將需要已安裝 AdventureWorks SQL Server 範例資料庫之伺服器的存取權。</span><span class="sxs-lookup"><span data-stu-id="3094e-111">You will need access to a server with the AdventureWorks SQL Server sample database installed.</span></span>  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1getdata)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1getdata)]  
  
2. <span data-ttu-id="3094e-112">在表單的 <xref:System.Windows.Forms.Form.Load> 事件處理常式中，將 <xref:System.Windows.Forms.DataGridView> 控制項繫結至 <xref:System.Windows.Forms.BindingSource> 元件並呼叫 `GetData` 方法，以便從資料庫中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="3094e-112">In the <xref:System.Windows.Forms.Form.Load> event handler of your form, bind the <xref:System.Windows.Forms.DataGridView> control to the <xref:System.Windows.Forms.BindingSource> component and call the `GetData` method to retrieve the data from the database.</span></span> <span data-ttu-id="3094e-113"><xref:System.Data.DataView>會透過連絡人的 LINQ to DataSet 查詢建立，然後系結 <xref:System.Data.DataTable> 至 <xref:System.Windows.Forms.BindingSource> 元件。</span><span class="sxs-lookup"><span data-stu-id="3094e-113">The <xref:System.Data.DataView> is created from a LINQ to DataSet query over the Contact <xref:System.Data.DataTable> and is then bound to the <xref:System.Windows.Forms.BindingSource> component.</span></span>  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1formload)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1formload)]  
  
## <a name="see-also"></a><span data-ttu-id="3094e-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3094e-114">See also</span></span>

- [<span data-ttu-id="3094e-115">資料繫結和 LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="3094e-115">Data Binding and LINQ to DataSet</span></span>](data-binding-and-linq-to-dataset.md)

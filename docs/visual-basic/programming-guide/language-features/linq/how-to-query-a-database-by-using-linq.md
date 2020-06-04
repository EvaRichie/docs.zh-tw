---
title: 如何：使用 LINQ 查詢資料庫
ms.date: 07/20/2015
helpviewer_keywords:
- query samples [LINQ]
- database querying [LINQ]
- queries [LINQ in Visual Basic], database querying
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: bcf5e9c3-a236-4399-9a7f-3991eca7cf56
ms.openlocfilehash: ad4744e1734fd968f610ec02b60814eadd3ebe9a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404961"
---
# <a name="how-to-query-a-database-by-using-linq-visual-basic"></a><span data-ttu-id="7b4bf-102">如何：使用 LINQ 查詢資料庫 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7b4bf-102">How to: Query a Database by Using LINQ (Visual Basic)</span></span>
<span data-ttu-id="7b4bf-103">語言整合式查詢（LINQ）可讓您輕鬆地存取資料庫資訊並執行查詢。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-103">Language-Integrated Query (LINQ) makes it easy to access database information and execute queries.</span></span>  
  
 <span data-ttu-id="7b4bf-104">下列範例示範如何建立新的應用程式，以對 SQL Server 資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-104">The following example shows how to create a new application that performs queries against a SQL Server database.</span></span>  
  
 <span data-ttu-id="7b4bf-105">本主題中的範例會使用 Northwind 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-105">The examples in this topic use the Northwind sample database.</span></span> <span data-ttu-id="7b4bf-106">如果您的開發電腦上沒有這個資料庫，則可以從 Microsoft 下載中心下載。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-106">If you do not have this database on your development computer, you can download it from the Microsoft Download Center.</span></span> <span data-ttu-id="7b4bf-107">如需指示，請參閱[下載範例資料庫](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-107">For instructions, see [Downloading Sample Databases](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).</span></span>  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-create-a-connection-to-a-database"></a><span data-ttu-id="7b4bf-108">建立資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="7b4bf-108">To create a connection to a database</span></span>  
  
1. <span data-ttu-id="7b4bf-109">在 Visual Studio 中， **Server Explorer** / **Database Explorer**按一下**Server Explorer** / [ **View** ] 功能表上的 [伺服器總管**資料庫總管**] 來開啟伺服器總管資料庫總管。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-109">In Visual Studio, open **Server Explorer**/**Database Explorer** by clicking **Server Explorer**/**Database Explorer** on the **View** menu.</span></span>  
  
2. <span data-ttu-id="7b4bf-110">以滑鼠右鍵按一下**伺服器總管**資料庫總管中的 [**資料連線**] / **Database Explorer** ，然後按一下 [**新增連接**]。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-110">Right-click **Data Connections** in **Server Explorer**/**Database Explorer** and then click **Add Connection**.</span></span>  
  
3. <span data-ttu-id="7b4bf-111">請指定與 Northwind 範例資料庫的有效連接。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-111">Specify a valid connection to the Northwind sample database.</span></span>  
  
## <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a><span data-ttu-id="7b4bf-112">若要加入包含 LINQ to SQL 檔案的專案</span><span class="sxs-lookup"><span data-stu-id="7b4bf-112">To add a project that contains a LINQ to SQL file</span></span>  
  
1. <span data-ttu-id="7b4bf-113">**在 Visual Studio 的 [檔案**] 功能表上，指向 [**新增**]，然後按一下 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-113">In Visual Studio, on the **File** menu, point to **New** and then click **Project**.</span></span> <span data-ttu-id="7b4bf-114">選取 [Visual Basic **Windows Forms 應用程式**] 做為 [專案類型]。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-114">Select Visual Basic **Windows Forms Application** as the project type.</span></span>  
  
2. <span data-ttu-id="7b4bf-115">在 [專案]\*\*\*\* 功能表上，按一下 [加入新項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-115">On the **Project** menu, click **Add New Item**.</span></span> <span data-ttu-id="7b4bf-116">選取 [ **LINQ to SQL 類別**] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-116">Select the **LINQ to SQL Classes** item template.</span></span>  
  
3. <span data-ttu-id="7b4bf-117">將檔案命名為 `northwind.dbml`。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-117">Name the file `northwind.dbml`.</span></span> <span data-ttu-id="7b4bf-118">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-118">Click **Add**.</span></span> <span data-ttu-id="7b4bf-119">[物件關聯式設計工具（O/R 設計工具）] 會針對 northwind .dbml 檔案開啟。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-119">The Object Relational Designer (O/R Designer) is opened for the northwind.dbml file.</span></span>  
  
## <a name="to-add-tables-to-query-to-the-or-designer"></a><span data-ttu-id="7b4bf-120">若要將資料表加入至 O/R 設計工具以進行查詢</span><span class="sxs-lookup"><span data-stu-id="7b4bf-120">To add tables to query to the O/R Designer</span></span>  
  
1. <span data-ttu-id="7b4bf-121">在**伺服器總管** / **資料庫總管**中，展開 Northwind 資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-121">In **Server Explorer**/**Database Explorer**, expand the connection to the Northwind database.</span></span> <span data-ttu-id="7b4bf-122">展開 **[資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-122">Expand the **Tables** folder.</span></span>  
  
     <span data-ttu-id="7b4bf-123">如果您已經關閉 O/R 設計工具，可以按兩下先前加入的 northwind 檔案來重新開啟它。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-123">If you have closed the O/R Designer, you can reopen it by double-clicking the northwind.dbml file that you added earlier.</span></span>  
  
2. <span data-ttu-id="7b4bf-124">按一下 [Customers] 資料表，並將它拖曳至設計工具的左窗格。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-124">Click the Customers table and drag it to the left pane of the designer.</span></span> <span data-ttu-id="7b4bf-125">按一下 [Orders] 資料表，並將它拖曳至設計工具的左窗格。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-125">Click the Orders table and drag it to the left pane of the designer.</span></span>  
  
     <span data-ttu-id="7b4bf-126">設計工具會 `Customer` `Order` 為您的專案建立新的和物件。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-126">The designer creates new `Customer` and `Order` objects for your project.</span></span> <span data-ttu-id="7b4bf-127">請注意，設計工具會自動偵測資料表之間的關聯性，並建立相關物件的子屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-127">Notice that the designer automatically detects relationships between the tables and creates child properties for related objects.</span></span> <span data-ttu-id="7b4bf-128">例如，IntelliSense 會顯示 `Customer` 物件具有與 `Orders` 該客戶相關之所有訂單的屬性。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-128">For example, IntelliSense will show that the `Customer` object has an `Orders` property for all orders related to that customer.</span></span>  
  
3. <span data-ttu-id="7b4bf-129">儲存您的變更並關閉設計工具。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-129">Save your changes and close the designer.</span></span>  
  
4. <span data-ttu-id="7b4bf-130">儲存您的專案。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-130">Save your project.</span></span>  
  
## <a name="to-add-code-to-query-the-database-and-display-the-results"></a><span data-ttu-id="7b4bf-131">若要加入程式碼以查詢資料庫並顯示結果</span><span class="sxs-lookup"><span data-stu-id="7b4bf-131">To add code to query the database and display the results</span></span>  
  
1. <span data-ttu-id="7b4bf-132">從 [**工具箱**] 中，將 <xref:System.Windows.Forms.DataGridView> 控制項拖曳至專案的預設 Windows Form （Form1）。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-132">From the **Toolbox**, drag a <xref:System.Windows.Forms.DataGridView> control onto the default Windows Form for your project, Form1.</span></span>  
  
2. <span data-ttu-id="7b4bf-133">按兩下 [Form1]，將程式碼加入 `Load` 表單的事件中。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-133">Double-click Form1 to add code to the `Load` event of the form.</span></span>  
  
3. <span data-ttu-id="7b4bf-134">當您將資料表加入至 O/R 設計工具時，設計工具會 <xref:System.Data.Linq.DataContext> 為您的專案加入物件。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-134">When you added tables to the O/R Designer, the designer added a <xref:System.Data.Linq.DataContext> object for your project.</span></span> <span data-ttu-id="7b4bf-135">除了每個資料表的個別物件和集合之外，此物件還包含存取這些資料表所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-135">This object contains the code that you must have to access those tables, in addition to individual objects and collections for each table.</span></span> <span data-ttu-id="7b4bf-136"><xref:System.Data.Linq.DataContext>專案的物件會根據 .dbml 檔案的名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-136">The <xref:System.Data.Linq.DataContext> object for your project is named based on the name of your .dbml file.</span></span> <span data-ttu-id="7b4bf-137">針對此專案， <xref:System.Data.Linq.DataContext> 物件的名稱為 `northwindDataContext` 。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-137">For this project, the <xref:System.Data.Linq.DataContext> object is named `northwindDataContext`.</span></span>  
  
     <span data-ttu-id="7b4bf-138">您可以 <xref:System.Data.Linq.DataContext> 在程式碼中建立的實例，並查詢 O/R 設計工具所指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-138">You can create an instance of the <xref:System.Data.Linq.DataContext> in your code and query the tables specified by the O/R Designer.</span></span>  
  
     <span data-ttu-id="7b4bf-139">將下列程式碼加入至 `Load` 事件，以查詢公開為數據內容屬性的資料表。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-139">Add the following code to the `Load` event to query the tables that are exposed as properties of your data context.</span></span>  
  
     [!code-vb[VbLINQToSQLHowTos#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form2.vb#3)]  
  
4. <span data-ttu-id="7b4bf-140">按 F5 執行您的專案並查看結果。</span><span class="sxs-lookup"><span data-stu-id="7b4bf-140">Press F5 to run your project and view the results.</span></span>  
  
5. <span data-ttu-id="7b4bf-141">以下是一些您可以嘗試的其他查詢：</span><span class="sxs-lookup"><span data-stu-id="7b4bf-141">Following are some additional queries that you can try:</span></span>  
  
     [!code-vb[VbLINQToSQLHowTos#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form2.vb#4)]  
    [!code-vb[VbLINQToSQLHowTos#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form2.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="7b4bf-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7b4bf-142">See also</span></span>

- [<span data-ttu-id="7b4bf-143">LINQ</span><span class="sxs-lookup"><span data-stu-id="7b4bf-143">LINQ</span></span>](index.md)
- [<span data-ttu-id="7b4bf-144">查詢</span><span class="sxs-lookup"><span data-stu-id="7b4bf-144">Queries</span></span>](../../../language-reference/queries/index.md)
- [<span data-ttu-id="7b4bf-145">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="7b4bf-145">LINQ to SQL</span></span>](../../../../framework/data/adonet/sql/linq/index.md)
- [<span data-ttu-id="7b4bf-146">DataCoNtext 方法（O/R 設計工具）</span><span class="sxs-lookup"><span data-stu-id="7b4bf-146">DataContext Methods (O/R Designer)</span></span>](/visualstudio/data-tools/datacontext-methods-o-r-designer)

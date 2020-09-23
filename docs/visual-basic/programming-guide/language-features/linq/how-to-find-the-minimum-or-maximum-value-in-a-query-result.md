---
title: 如何：使用 LINQ 尋找查詢結果中的最小或最大值
ms.date: 07/20/2015
helpviewer_keywords:
- max operator [LINQ in Visual Basic]
- aggregate operator [LINQ in Visual Basic]
- aggregate queries
- minimum values [LINQ in Visual Basic]
- min operator [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], minimum and maximum values
- Max property
- maximum values [LINQ in Visual Basic]
- Aggregate clause [Visual Basic]
- queries [LINQ in Visual Basic], aggregate queries
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 238b763b-7dcd-4b14-8050-b65500a4f71c
ms.openlocfilehash: e397ccd6fe21caaeb9d56ff3b0cc1ce16032639a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91084004"
---
# <a name="how-to-find-the-minimum-or-maximum-value-in-a-query-result-by-using-linq-visual-basic"></a><span data-ttu-id="6714b-102">如何：使用 LINQ 尋找查詢結果中的最小或最大值 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6714b-102">How to: Find the Minimum or Maximum Value in a Query Result by Using LINQ (Visual Basic)</span></span>

<span data-ttu-id="6714b-103"> (LINQ) 的語言整合式查詢，可讓您輕鬆地存取資料庫資訊和執行查詢。</span><span class="sxs-lookup"><span data-stu-id="6714b-103">Language-Integrated Query (LINQ) makes it easy to access database information and execute queries.</span></span>  
  
 <span data-ttu-id="6714b-104">下列範例示範如何建立新的應用程式，以針對 SQL Server 資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="6714b-104">The following example shows how to create a new application that performs queries against a SQL Server database.</span></span> <span data-ttu-id="6714b-105">此範例會使用和子句來決定結果的最小值和最大值 `Aggregate` `Group By` 。</span><span class="sxs-lookup"><span data-stu-id="6714b-105">The sample determines the minimum and maximum values for the results by using the `Aggregate` and `Group By` clauses.</span></span> <span data-ttu-id="6714b-106">如需詳細資訊，請參閱 [Aggregate 子句](../../../language-reference/queries/aggregate-clause.md) 和 [group by 子句](../../../language-reference/queries/group-by-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="6714b-106">For more information, see [Aggregate Clause](../../../language-reference/queries/aggregate-clause.md) and [Group By Clause](../../../language-reference/queries/group-by-clause.md).</span></span>  
  
 <span data-ttu-id="6714b-107">本主題中的範例會使用 Northwind 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="6714b-107">The examples in this topic use the Northwind sample database.</span></span> <span data-ttu-id="6714b-108">如果您的開發電腦上沒有這個資料庫，則可以從 Microsoft 下載中心下載。</span><span class="sxs-lookup"><span data-stu-id="6714b-108">If you do not have this database on your development computer, you can download it from the Microsoft Download Center.</span></span> <span data-ttu-id="6714b-109">如需相關指示，請參閱 [下載範例資料庫](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="6714b-109">For instructions, see [Downloading Sample Databases](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).</span></span>  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="create-a-connection-to-a-database"></a><span data-ttu-id="6714b-110">建立與資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="6714b-110">Create a connection to a database</span></span>  
  
1. <span data-ttu-id="6714b-111">在 Visual Studio 中， **Server Explorer** / 按一下 [View] 功能表上的 [**伺服器總管**資料庫總管來開啟伺服器總管**資料庫總管** / **Database Explorer** 。 **View**</span><span class="sxs-lookup"><span data-stu-id="6714b-111">In Visual Studio, open **Server Explorer**/**Database Explorer** by clicking **Server Explorer**/**Database Explorer** on the **View** menu.</span></span>  
  
2. <span data-ttu-id="6714b-112">以滑鼠右鍵按一下**伺服器總管**資料庫總管中的 [**資料連線**] / **Database Explorer** ，然後按一下 [**加入連接**]。</span><span class="sxs-lookup"><span data-stu-id="6714b-112">Right-click **Data Connections** in **Server Explorer**/**Database Explorer** and then click **Add Connection**.</span></span>  
  
3. <span data-ttu-id="6714b-113">請指定與 Northwind 範例資料庫的有效連接。</span><span class="sxs-lookup"><span data-stu-id="6714b-113">Specify a valid connection to the Northwind sample database.</span></span>  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a><span data-ttu-id="6714b-114">若要加入包含 LINQ to SQL 檔案的專案</span><span class="sxs-lookup"><span data-stu-id="6714b-114">To add a project that contains a LINQ to SQL file</span></span>  
  
1. <span data-ttu-id="6714b-115">在 Visual Studio **的 [檔案** ] 功能表上，指向 [ **新增** ]，然後按一下 [ **專案**]。</span><span class="sxs-lookup"><span data-stu-id="6714b-115">In Visual Studio, on the **File** menu, point to **New** and then click **Project**.</span></span> <span data-ttu-id="6714b-116">選取 Visual Basic **Windows Forms 應用程式** 做為專案類型。</span><span class="sxs-lookup"><span data-stu-id="6714b-116">Select Visual Basic **Windows Forms Application** as the project type.</span></span>  
  
2. <span data-ttu-id="6714b-117">在 [專案]\*\*\*\* 功能表上，按一下 [加入新項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6714b-117">On the **Project** menu, click **Add New Item**.</span></span> <span data-ttu-id="6714b-118">選取 [ **LINQ to SQL 類別** ] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="6714b-118">Select the **LINQ to SQL Classes** item template.</span></span>  
  
3. <span data-ttu-id="6714b-119">將檔案命名為 `northwind.dbml`。</span><span class="sxs-lookup"><span data-stu-id="6714b-119">Name the file `northwind.dbml`.</span></span> <span data-ttu-id="6714b-120">按一下 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="6714b-120">Click **Add**.</span></span> <span data-ttu-id="6714b-121">物件關聯式設計工具的 (O/R 設計工具) 會針對 northwind 檔案開啟。</span><span class="sxs-lookup"><span data-stu-id="6714b-121">The Object Relational Designer (O/R Designer) is opened for the northwind.dbml file.</span></span>  
  
## <a name="add-tables-to-query-to-the-or-designer"></a><span data-ttu-id="6714b-122">將資料表加入至 O/R 設計工具的查詢</span><span class="sxs-lookup"><span data-stu-id="6714b-122">Add tables to query to the O/R Designer</span></span>  
  
1. <span data-ttu-id="6714b-123">在**伺服器總管** / **資料庫總管**中，展開 Northwind 資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="6714b-123">In **Server Explorer**/**Database Explorer**, expand the connection to the Northwind database.</span></span> <span data-ttu-id="6714b-124">展開 **[資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6714b-124">Expand the **Tables** folder.</span></span>  
  
     <span data-ttu-id="6714b-125">如果您已關閉 O/R 設計工具，您可以按兩下先前加入的 northwind 檔案來重新開啟它。</span><span class="sxs-lookup"><span data-stu-id="6714b-125">If you have closed the O/R Designer, you can reopen it by double-clicking the northwind.dbml file that you added earlier.</span></span>  
  
2. <span data-ttu-id="6714b-126">按一下 [Customers] 資料表，然後將它拖曳至設計工具的左窗格。</span><span class="sxs-lookup"><span data-stu-id="6714b-126">Click the Customers table and drag it to the left pane of the designer.</span></span> <span data-ttu-id="6714b-127">按一下 [Orders] 資料表，然後將它拖曳至設計工具的左窗格。</span><span class="sxs-lookup"><span data-stu-id="6714b-127">Click the Orders table and drag it to the left pane of the designer.</span></span>  
  
     <span data-ttu-id="6714b-128">設計工具會 `Customer` `Order` 為您的專案建立新的和物件。</span><span class="sxs-lookup"><span data-stu-id="6714b-128">The designer creates new `Customer` and `Order` objects for your project.</span></span> <span data-ttu-id="6714b-129">請注意，設計工具會自動偵測資料表之間的關聯性，並建立相關物件的子屬性。</span><span class="sxs-lookup"><span data-stu-id="6714b-129">Notice that the designer automatically detects relationships between the tables and creates child properties for related objects.</span></span> <span data-ttu-id="6714b-130">例如，IntelliSense 會顯示 `Customer` 物件具有與 `Orders` 該客戶相關之所有訂單的屬性。</span><span class="sxs-lookup"><span data-stu-id="6714b-130">For example, IntelliSense will show that the `Customer` object has an `Orders` property for all orders related to that customer.</span></span>  
  
3. <span data-ttu-id="6714b-131">儲存您的變更並關閉設計工具。</span><span class="sxs-lookup"><span data-stu-id="6714b-131">Save your changes and close the designer.</span></span>  
  
4. <span data-ttu-id="6714b-132">儲存您的專案。</span><span class="sxs-lookup"><span data-stu-id="6714b-132">Save your project.</span></span>  
  
## <a name="add-code-to-query-the-database-and-display-the-results"></a><span data-ttu-id="6714b-133">加入程式碼以查詢資料庫並顯示結果</span><span class="sxs-lookup"><span data-stu-id="6714b-133">Add code to query the database and display the results</span></span>  
  
1. <span data-ttu-id="6714b-134">從 [ **工具箱**] 中，將 <xref:System.Windows.Forms.DataGridView> 控制項拖曳至專案的預設 Windows 表單（Form1）。</span><span class="sxs-lookup"><span data-stu-id="6714b-134">From the **Toolbox**, drag a <xref:System.Windows.Forms.DataGridView> control onto the default Windows Form for your project, Form1.</span></span>  
  
2. <span data-ttu-id="6714b-135">按兩下 [Form1]，將程式碼加入 `Load` 表單的事件中。</span><span class="sxs-lookup"><span data-stu-id="6714b-135">Double-click Form1 to add code to the `Load` event of the form.</span></span>  
  
3. <span data-ttu-id="6714b-136">當您將資料表加入至 O/R 設計工具時，設計工具會 <xref:System.Data.Linq.DataContext> 為您的專案新增物件。</span><span class="sxs-lookup"><span data-stu-id="6714b-136">When you added tables to the O/R Designer, the designer added a <xref:System.Data.Linq.DataContext> object for your project.</span></span> <span data-ttu-id="6714b-137">除了每個資料表的個別物件和集合之外，此物件還包含存取這些資料表所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6714b-137">This object contains the code that you must have to access those tables, in addition to individual objects and collections for each table.</span></span> <span data-ttu-id="6714b-138"><xref:System.Data.Linq.DataContext>專案的物件是根據您 .dbml 檔的名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="6714b-138">The <xref:System.Data.Linq.DataContext> object for your project is named based on the name of your .dbml file.</span></span> <span data-ttu-id="6714b-139">針對此專案， <xref:System.Data.Linq.DataContext> 會將物件命名為 `northwindDataContext` 。</span><span class="sxs-lookup"><span data-stu-id="6714b-139">For this project, the <xref:System.Data.Linq.DataContext> object is named `northwindDataContext`.</span></span>  
  
     <span data-ttu-id="6714b-140">您可以 <xref:System.Data.Linq.DataContext> 在程式碼中建立的實例，並查詢 O/R 設計工具所指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="6714b-140">You can create an instance of the <xref:System.Data.Linq.DataContext> in your code and query the tables specified by the O/R Designer.</span></span>  
  
     <span data-ttu-id="6714b-141">將下列程式碼加入至 `Load` 事件。</span><span class="sxs-lookup"><span data-stu-id="6714b-141">Add the following code to the `Load` event.</span></span> <span data-ttu-id="6714b-142">這段程式碼會查詢公開為您資料內容屬性的資料表，並決定結果的最小值和最大值。</span><span class="sxs-lookup"><span data-stu-id="6714b-142">This code queries the tables that are exposed as properties of your data context and determines the minimum and maximum values for the results.</span></span> <span data-ttu-id="6714b-143">此範例會使用 `Aggregate` 子句來查詢單一結果，以及使用 `Group By` 子句來顯示群組結果的平均值。</span><span class="sxs-lookup"><span data-stu-id="6714b-143">The sample uses the `Aggregate` clause to query for a single result, and the `Group By` clause to show an average for grouped results.</span></span>  
  
     [!code-vb[VbLINQToSQLHowTos#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form7.vb#14)]  
  
4. <span data-ttu-id="6714b-144">按 **F5** 執行您的專案，並查看結果。</span><span class="sxs-lookup"><span data-stu-id="6714b-144">Press **F5** to run your project and view the results.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6714b-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6714b-145">See also</span></span>

- [<span data-ttu-id="6714b-146">LINQ</span><span class="sxs-lookup"><span data-stu-id="6714b-146">LINQ</span></span>](index.md)
- [<span data-ttu-id="6714b-147">查詢</span><span class="sxs-lookup"><span data-stu-id="6714b-147">Queries</span></span>](../../../language-reference/queries/index.md)
- [<span data-ttu-id="6714b-148">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="6714b-148">LINQ to SQL</span></span>](../../../../framework/data/adonet/sql/linq/index.md)
- [<span data-ttu-id="6714b-149">DataContext 方法 (O/R 設計工具)</span><span class="sxs-lookup"><span data-stu-id="6714b-149">DataContext Methods (O/R Designer)</span></span>](/visualstudio/data-tools/datacontext-methods-o-r-designer)

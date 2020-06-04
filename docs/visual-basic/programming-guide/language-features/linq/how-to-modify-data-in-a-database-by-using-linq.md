---
title: 如何：使用 LINQ 修改資料庫中的資料
ms.date: 07/20/2015
helpviewer_keywords:
- inserting rows [LINQ to SQL]
- deleting rows [LINQ to SQL]
- updating rows [LINQ to SQL]
- inserting data [Visual Basic]
- deleting data
- data [Visual Basic], updating
- updating data [LINQ]
- queries [LINQ in Visual Basic], data changes in database
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: cf52635f-0c1b-46c3-aff1-bdf181cf19b1
ms.openlocfilehash: eb076d9156fa66858f2e560422eef0dc61ba22b5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403481"
---
# <a name="how-to-modify-data-in-a-database-by-using-linq-visual-basic"></a><span data-ttu-id="fb41c-102">如何：使用 LINQ 修改資料庫中的資料 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="fb41c-102">How to: Modify Data in a Database by Using LINQ (Visual Basic)</span></span>

<span data-ttu-id="fb41c-103">語言整合式查詢（LINQ）查詢可讓您輕鬆地存取資料庫資訊並修改資料庫中的值。</span><span class="sxs-lookup"><span data-stu-id="fb41c-103">Language-Integrated Query (LINQ) queries make it easy to access database information and modify values in the database.</span></span>

<span data-ttu-id="fb41c-104">下列範例示範如何建立新的應用程式，以抓取和更新 SQL Server 資料庫中的資訊。</span><span class="sxs-lookup"><span data-stu-id="fb41c-104">The following example shows how to create a new application that retrieves and updates information in a SQL Server database.</span></span>

<span data-ttu-id="fb41c-105">本主題中的範例會使用 Northwind 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="fb41c-105">The examples in this topic use the Northwind sample database.</span></span> <span data-ttu-id="fb41c-106">如果您的開發電腦上沒有這個資料庫，則可以從 Microsoft 下載中心下載。</span><span class="sxs-lookup"><span data-stu-id="fb41c-106">If you do not have this database on your development computer, you can download it from the Microsoft Download Center.</span></span> <span data-ttu-id="fb41c-107">如需指示，請參閱[下載範例資料庫](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="fb41c-107">For instructions, see [Downloading Sample Databases](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).</span></span>

### <a name="to-create-a-connection-to-a-database"></a><span data-ttu-id="fb41c-108">建立資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="fb41c-108">To create a connection to a database</span></span>

1. <span data-ttu-id="fb41c-109">在 Visual Studio 中， **Server Explorer** / 按一下 [ **View** ] 功能表以開啟伺服器總管**資料庫總管**，然後選取 [**伺服器總管** / **資料庫總管**]。</span><span class="sxs-lookup"><span data-stu-id="fb41c-109">In Visual Studio, open **Server Explorer**/**Database Explorer** by clicking the **View** menu, and then select **Server Explorer**/**Database Explorer**.</span></span>

2. <span data-ttu-id="fb41c-110">以滑鼠右鍵按一下**伺服器總管**資料庫總管中的 [**資料連線**] / \*\* **，然後按一下 [**新增連接\*\*]。</span><span class="sxs-lookup"><span data-stu-id="fb41c-110">Right-click **Data Connections** in **Server Explorer**/**Database Explorer**, and click **Add Connection**.</span></span>

3. <span data-ttu-id="fb41c-111">請指定與 Northwind 範例資料庫的有效連接。</span><span class="sxs-lookup"><span data-stu-id="fb41c-111">Specify a valid connection to the Northwind sample database.</span></span>

### <a name="to-add-a-project-with-a-linq-to-sql-file"></a><span data-ttu-id="fb41c-112">若要加入具有 LINQ to SQL 檔案的專案</span><span class="sxs-lookup"><span data-stu-id="fb41c-112">To add a Project with a LINQ to SQL file</span></span>

1. <span data-ttu-id="fb41c-113">**在 Visual Studio 的 [檔案**] 功能表上，指向 [**新增**]，然後按一下 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="fb41c-113">In Visual Studio, on the **File** menu, point to **New** and then click **Project**.</span></span> <span data-ttu-id="fb41c-114">選取 [Visual Basic **Windows Forms 應用程式**] 做為 [專案類型]。</span><span class="sxs-lookup"><span data-stu-id="fb41c-114">Select Visual Basic **Windows Forms Application** as the project type.</span></span>

2. <span data-ttu-id="fb41c-115">在 [專案]\*\*\*\* 功能表上，按一下 [加入新項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="fb41c-115">On the **Project** menu, click **Add New Item**.</span></span> <span data-ttu-id="fb41c-116">選取 [ **LINQ to SQL 類別**] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="fb41c-116">Select the **LINQ to SQL Classes** item template.</span></span>

3. <span data-ttu-id="fb41c-117">將檔案命名為 `northwind.dbml`。</span><span class="sxs-lookup"><span data-stu-id="fb41c-117">Name the file `northwind.dbml`.</span></span> <span data-ttu-id="fb41c-118">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-118">Click **Add**.</span></span> <span data-ttu-id="fb41c-119">隨即開啟檔案的物件關聯式設計工具（O/R 設計工具） `northwind.dbml` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-119">The Object Relational Designer (O/R Designer) is opened for the `northwind.dbml` file.</span></span>

### <a name="to-add-tables-to-query-and-modify-to-the-designer"></a><span data-ttu-id="fb41c-120">若要將資料表加入至設計工具並進行查詢和修改</span><span class="sxs-lookup"><span data-stu-id="fb41c-120">To add tables to query and modify to the designer</span></span>

1. <span data-ttu-id="fb41c-121">在**伺服器總管** / **資料庫總管**中，展開 Northwind 資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="fb41c-121">In **Server Explorer**/**Database Explorer**, expand the connection to the Northwind database.</span></span> <span data-ttu-id="fb41c-122">展開 **[資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb41c-122">Expand the **Tables** folder.</span></span>

     <span data-ttu-id="fb41c-123">如果您已經關閉 O/R 設計工具，可以按兩下先前加入的檔案來重新開啟它 `northwind.dbml` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-123">If you have closed the O/R Designer, you can reopen it by double-clicking the `northwind.dbml` file that you added earlier.</span></span>

2. <span data-ttu-id="fb41c-124">按一下 [Customers] 資料表，並將它拖曳至設計工具的左窗格。</span><span class="sxs-lookup"><span data-stu-id="fb41c-124">Click the Customers table and drag it to the left pane of the designer.</span></span>

     <span data-ttu-id="fb41c-125">設計工具會為您的專案建立新的 Customer 物件。</span><span class="sxs-lookup"><span data-stu-id="fb41c-125">The designer creates a new Customer object for your project.</span></span>

3. <span data-ttu-id="fb41c-126">儲存您的變更並關閉設計工具。</span><span class="sxs-lookup"><span data-stu-id="fb41c-126">Save your changes and close the designer.</span></span>

4. <span data-ttu-id="fb41c-127">儲存您的專案。</span><span class="sxs-lookup"><span data-stu-id="fb41c-127">Save your project.</span></span>

### <a name="to-add-code-to-modify-the-database-and-display-the-results"></a><span data-ttu-id="fb41c-128">若要加入程式碼來修改資料庫並顯示結果</span><span class="sxs-lookup"><span data-stu-id="fb41c-128">To add code to modify the database and display the results</span></span>

1. <span data-ttu-id="fb41c-129">從 [**工具箱**] 中，將 <xref:System.Windows.Forms.DataGridView> 控制項拖曳至專案的預設 Windows Form （Form1）。</span><span class="sxs-lookup"><span data-stu-id="fb41c-129">From the **Toolbox**, drag a <xref:System.Windows.Forms.DataGridView> control onto the default Windows Form for your project, Form1.</span></span>

2. <span data-ttu-id="fb41c-130">當您將資料表加入至 O/R 設計工具時，設計工具會將 <xref:System.Data.Linq.DataContext> 物件加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="fb41c-130">When you added tables to the O/R Designer, the designer added a <xref:System.Data.Linq.DataContext> object to your project.</span></span> <span data-ttu-id="fb41c-131">此物件包含您可以用來存取 Customers 資料表的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb41c-131">This object contains code that you can use to access the Customers table.</span></span> <span data-ttu-id="fb41c-132">它也包含定義本機 Customer 物件和資料表之 Customers 集合的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb41c-132">It also contains code that defines  a local Customer object and a Customers collection for the table.</span></span> <span data-ttu-id="fb41c-133"><xref:System.Data.Linq.DataContext>專案的物件會根據 .dbml 檔案的名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="fb41c-133">The <xref:System.Data.Linq.DataContext> object for your project is named based on the name of your .dbml file.</span></span> <span data-ttu-id="fb41c-134">針對此專案， <xref:System.Data.Linq.DataContext> 物件的名稱為 `northwindDataContext` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-134">For this project, the <xref:System.Data.Linq.DataContext> object is named `northwindDataContext`.</span></span>

     <span data-ttu-id="fb41c-135">您可以 <xref:System.Data.Linq.DataContext> 在程式碼中建立物件的實例，並查詢和修改 O/R 設計工具所指定的 Customers 集合。</span><span class="sxs-lookup"><span data-stu-id="fb41c-135">You can create an instance of the <xref:System.Data.Linq.DataContext> object in your code and query and modify the Customers collection specified by the O/R Designer.</span></span> <span data-ttu-id="fb41c-136">您對 Customers 集合所做的變更不會反映在資料庫中，直到您藉由呼叫物件的方法來提交為止 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> <xref:System.Data.Linq.DataContext> 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-136">Changes that you make to the Customers collection are not reflected in the database until you submit them by calling the <xref:System.Data.Linq.DataContext.SubmitChanges%2A> method of the <xref:System.Data.Linq.DataContext> object.</span></span>

     <span data-ttu-id="fb41c-137">按兩下 Windows Form Form1，將程式碼加入至 <xref:System.Windows.Forms.Form.Load> 事件，以查詢公開為之屬性的 Customers 資料表 <xref:System.Data.Linq.DataContext> 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-137">Double-click the Windows Form, Form1, to add code to the <xref:System.Windows.Forms.Form.Load> event to query the Customers table that is exposed as a property of your <xref:System.Data.Linq.DataContext>.</span></span> <span data-ttu-id="fb41c-138">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fb41c-138">Add the following code:</span></span>

    ```vb
    Private db As northwindDataContext

    Private Sub Form1_Load(ByVal sender As System.Object,
                           ByVal e As System.EventArgs
                          ) Handles MyBase.Load
      db = New northwindDataContext()

      RefreshData()
    End Sub

    Private Sub RefreshData()
      Dim customers = From cust In db.Customers
                      Where cust.City(0) = "W"
                      Select cust

      DataGridView1.DataSource = customers
    End Sub
    ```

3. <span data-ttu-id="fb41c-139">從 [**工具箱**] 將三個 <xref:System.Windows.Forms.Button> 控制項拖曳至表單上。</span><span class="sxs-lookup"><span data-stu-id="fb41c-139">From the **Toolbox**, drag three <xref:System.Windows.Forms.Button> controls onto the form.</span></span> <span data-ttu-id="fb41c-140">選取第一個 `Button` 控制項。</span><span class="sxs-lookup"><span data-stu-id="fb41c-140">Select the first `Button` control.</span></span> <span data-ttu-id="fb41c-141">在 [**屬性**] 視窗中，將控制項的設定 `Name` `Button` 為 `AddButton` ，並將設 `Text` 為 `Add` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-141">In the **Properties** window, set the `Name` of the `Button` control to `AddButton` and the `Text` to `Add`.</span></span> <span data-ttu-id="fb41c-142">選取第二個按鈕，並將 `Name` 屬性設為 `UpdateButton` ，並將屬性設定 `Text` 為 `Update` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-142">Select the second button and set the `Name` property to `UpdateButton` and the `Text` property to `Update`.</span></span> <span data-ttu-id="fb41c-143">選取第三個按鈕，並將屬性設 `Name` 為 `DeleteButton` ，並將 `Text` 屬性設定為 `Delete` 。</span><span class="sxs-lookup"><span data-stu-id="fb41c-143">Select the third button and set the `Name` property to `DeleteButton` and the `Text` property to `Delete`.</span></span>

4. <span data-ttu-id="fb41c-144">按兩下 [**新增**] 按鈕，將程式碼新增至其 `Click` 事件。</span><span class="sxs-lookup"><span data-stu-id="fb41c-144">Double-click the **Add** button to add code to its `Click` event.</span></span> <span data-ttu-id="fb41c-145">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fb41c-145">Add the following code:</span></span>

    ```vb
    Private Sub AddButton_Click(ByVal sender As System.Object,
                                ByVal e As System.EventArgs
                               ) Handles AddButton.Click
      Dim cust As New Customer With {
        .City = "Wellington",
        .CompanyName = "Blue Yonder Airlines",
        .ContactName = "Jill Frank",
        .Country = "New Zealand",
        .CustomerID = "JILLF"}

      db.Customers.InsertOnSubmit(cust)

      Try
        db.SubmitChanges()
      Catch
        ' Handle exception.
      End Try

      RefreshData()
    End Sub
    ```

5. <span data-ttu-id="fb41c-146">按兩下 [**更新**] 按鈕，將程式碼新增至其 `Click` 事件。</span><span class="sxs-lookup"><span data-stu-id="fb41c-146">Double-click the **Update** button to add code to its `Click` event.</span></span> <span data-ttu-id="fb41c-147">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fb41c-147">Add the following code:</span></span>

    ```vb
    Private Sub UpdateButton_Click(ByVal sender As System.Object, _
                                   ByVal e As System.EventArgs
                                  ) Handles UpdateButton.Click
      Dim updateCust = (From cust In db.Customers
                        Where cust.CustomerID = "JILLF").ToList()(0)

      updateCust.ContactName = "Jill Shrader"
      updateCust.Country = "Wales"
      updateCust.CompanyName = "Red Yonder Airlines"
      updateCust.City = "Cardiff"

      Try
        db.SubmitChanges()
      Catch
        ' Handle exception.
      End Try

      RefreshData()
    End Sub
    ```

6. <span data-ttu-id="fb41c-148">按兩下 [**刪除**] 按鈕，將程式碼新增至其 `Click` 事件。</span><span class="sxs-lookup"><span data-stu-id="fb41c-148">Double-click the **Delete** button to add code to its `Click` event.</span></span> <span data-ttu-id="fb41c-149">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fb41c-149">Add the following code:</span></span>

    ```vb
    Private Sub DeleteButton_Click(ByVal sender As System.Object, _
                                   ByVal e As System.EventArgs
                                  ) Handles DeleteButton.Click
      Dim deleteCust = (From cust In db.Customers
                        Where cust.CustomerID = "JILLF").ToList()(0)

      db.Customers.DeleteOnSubmit(deleteCust)

      Try
        db.SubmitChanges()
      Catch
        ' Handle exception.
      End Try

      RefreshData()
    End Sub
    ```

7. <span data-ttu-id="fb41c-150">請按 F5 執行您的專案。</span><span class="sxs-lookup"><span data-stu-id="fb41c-150">Press F5 to run your project.</span></span> <span data-ttu-id="fb41c-151">按一下 **[新增]** 以新增記錄。</span><span class="sxs-lookup"><span data-stu-id="fb41c-151">Click **Add** to add a new record.</span></span> <span data-ttu-id="fb41c-152">按一下 [**更新**] 以修改新的記錄。</span><span class="sxs-lookup"><span data-stu-id="fb41c-152">Click **Update** to modify the new record.</span></span> <span data-ttu-id="fb41c-153">按一下 [**刪除**] 以刪除新的記錄。</span><span class="sxs-lookup"><span data-stu-id="fb41c-153">Click **Delete** to delete the new record.</span></span>

## <a name="see-also"></a><span data-ttu-id="fb41c-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fb41c-154">See also</span></span>

- [<span data-ttu-id="fb41c-155">LINQ</span><span class="sxs-lookup"><span data-stu-id="fb41c-155">LINQ</span></span>](index.md)
- [<span data-ttu-id="fb41c-156">查詢</span><span class="sxs-lookup"><span data-stu-id="fb41c-156">Queries</span></span>](../../../language-reference/queries/index.md)
- [<span data-ttu-id="fb41c-157">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="fb41c-157">LINQ to SQL</span></span>](../../../../framework/data/adonet/sql/linq/index.md)
- [<span data-ttu-id="fb41c-158">DataCoNtext 方法（O/R 設計工具）</span><span class="sxs-lookup"><span data-stu-id="fb41c-158">DataContext Methods (O/R Designer)</span></span>](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [<span data-ttu-id="fb41c-159">如何：指派用來執行更新、插入和刪除的預存程序 (O/R 設計工具)</span><span class="sxs-lookup"><span data-stu-id="fb41c-159">How to: Assign stored procedures to perform updates, inserts, and deletes (O/R Designer)</span></span>](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)

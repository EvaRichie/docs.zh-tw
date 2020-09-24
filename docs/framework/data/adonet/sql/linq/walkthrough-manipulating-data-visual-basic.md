---
title: 逐步解說：操作資料 (Visual Basic)
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 1f6a54f6-ec33-452a-a37d-48122207bf14
ms.openlocfilehash: dbf18273e69ff0977f5d16ff179b8659865ef696
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164047"
---
# <a name="walkthrough-manipulating-data-visual-basic"></a><span data-ttu-id="d1aca-102">逐步解說：操作資料 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d1aca-102">Walkthrough: Manipulating Data (Visual Basic)</span></span>

<span data-ttu-id="d1aca-103">本逐步解說針對加入、修改和刪除資料庫中的資料，提供基本的端對端 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 案例。</span><span class="sxs-lookup"><span data-stu-id="d1aca-103">This walkthrough provides a fundamental end-to-end [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] scenario for adding, modifying, and deleting data in a database.</span></span> <span data-ttu-id="d1aca-104">您將使用範例 Northwind 資料庫的複本來加入客戶、變更客戶名稱，以及刪除訂單。</span><span class="sxs-lookup"><span data-stu-id="d1aca-104">You will use a copy of the sample Northwind database to add a customer, change the name of a customer, and delete an order.</span></span>  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 <span data-ttu-id="d1aca-105">這個逐步解說是使用 Visual Basic 開發設定所撰寫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-105">This walkthrough was written by using Visual Basic Development Settings.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d1aca-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="d1aca-106">Prerequisites</span></span>  

 <span data-ttu-id="d1aca-107">本逐步解說需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d1aca-107">This walkthrough requires the following:</span></span>  
  
- <span data-ttu-id="d1aca-108">本逐步解說會使用專用資料夾 ("c:\linqtest2") 來保存檔案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-108">This walkthrough uses a dedicated folder ("c:\linqtest2") to hold files.</span></span> <span data-ttu-id="d1aca-109">請先建立這個資料夾，再開始逐步解說。</span><span class="sxs-lookup"><span data-stu-id="d1aca-109">Create this folder before you begin the walkthrough.</span></span>  
  
- <span data-ttu-id="d1aca-110">Northwind 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-110">The Northwind sample database.</span></span>  
  
     <span data-ttu-id="d1aca-111">如果您的開發電腦上沒有這個資料庫，則可以從 Microsoft 下載網站下載。</span><span class="sxs-lookup"><span data-stu-id="d1aca-111">If you do not have this database on your development computer, you can download it from the Microsoft download site.</span></span> <span data-ttu-id="d1aca-112">如需相關指示，請參閱 [下載範例資料庫](downloading-sample-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="d1aca-112">For instructions, see [Downloading Sample Databases](downloading-sample-databases.md).</span></span> <span data-ttu-id="d1aca-113">下載資料庫之後，請將 northwnd.mdf 檔案複製至 c:\linqtest2 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d1aca-113">After you have downloaded the database, copy the northwnd.mdf file to the c:\linqtest2 folder.</span></span>  
  
- <span data-ttu-id="d1aca-114">從 Northwind 資料庫產生的 Visual Basic 程式碼檔。</span><span class="sxs-lookup"><span data-stu-id="d1aca-114">A Visual Basic code file generated from the Northwind database.</span></span>  
  
     <span data-ttu-id="d1aca-115">您可以使用物件關聯式設計工具或 SQLMetal 工具來產生此檔案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-115">You can generate this file by using either the Object Relational Designer or the SQLMetal tool.</span></span> <span data-ttu-id="d1aca-116">本逐步解說是使用 SQLMetal 工具，以下列命令列所撰寫：</span><span class="sxs-lookup"><span data-stu-id="d1aca-116">This walkthrough was written by using the SQLMetal tool with the following command line:</span></span>  
  
     <span data-ttu-id="d1aca-117">**sqlmetal /code:"c:\linqtest2\northwind.vb" /language:vb "C:\linqtest2\northwnd.mdf" /pluralize**</span><span class="sxs-lookup"><span data-stu-id="d1aca-117">**sqlmetal /code:"c:\linqtest2\northwind.vb" /language:vb "C:\linqtest2\northwnd.mdf" /pluralize**</span></span>  
  
     <span data-ttu-id="d1aca-118">如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../tools/sqlmetal-exe-code-generation-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="d1aca-118">For more information, see [SqlMetal.exe (Code Generation Tool)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span></span>  
  
## <a name="overview"></a><span data-ttu-id="d1aca-119">概觀</span><span class="sxs-lookup"><span data-stu-id="d1aca-119">Overview</span></span>  

 <span data-ttu-id="d1aca-120">此逐步解說包含六個主要工作：</span><span class="sxs-lookup"><span data-stu-id="d1aca-120">This walkthrough consists of six main tasks:</span></span>  
  
- <span data-ttu-id="d1aca-121">[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]在 Visual Studio 中建立方案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-121">Creating the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] solution in Visual Studio.</span></span>  
  
- <span data-ttu-id="d1aca-122">將資料庫程式碼檔案加入至專案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-122">Adding the database code file to the project.</span></span>  
  
- <span data-ttu-id="d1aca-123">建立新的客戶物件。</span><span class="sxs-lookup"><span data-stu-id="d1aca-123">Creating a new customer object.</span></span>  
  
- <span data-ttu-id="d1aca-124">修改客戶的連絡人名稱。</span><span class="sxs-lookup"><span data-stu-id="d1aca-124">Modifying the contact name of a customer.</span></span>  
  
- <span data-ttu-id="d1aca-125">刪除訂單。</span><span class="sxs-lookup"><span data-stu-id="d1aca-125">Deleting an order.</span></span>  
  
- <span data-ttu-id="d1aca-126">將這些變更送出至 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-126">Submitting these changes to the Northwind database.</span></span>  
  
## <a name="creating-a-linq-to-sql-solution"></a><span data-ttu-id="d1aca-127">建立 LINQ to SQL 方案</span><span class="sxs-lookup"><span data-stu-id="d1aca-127">Creating a LINQ to SQL Solution</span></span>  

 <span data-ttu-id="d1aca-128">在第一個工作中，您會建立 Visual Studio 方案，其中包含建立和執行專案所需的參考 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="d1aca-128">In this first task, you create a Visual Studio solution that contains the necessary references to build and run a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] project.</span></span>  
  
#### <a name="to-create-a-linq-to-sql-solution"></a><span data-ttu-id="d1aca-129">若要建立 LINQ to SQL 方案</span><span class="sxs-lookup"><span data-stu-id="d1aca-129">To create a LINQ to SQL solution</span></span>  
  
1. <span data-ttu-id="d1aca-130">在 Visual Studio 的 [檔案] \*\*\*\* 功能表上，按一下 [新增專案] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d1aca-130">On the Visual Studio **File** menu, click **New Project**.</span></span>  
  
2. <span data-ttu-id="d1aca-131">在 [**新增專案**] 對話方塊的 [**專案類型**] 窗格中，按一下 [ **Visual Basic**]。</span><span class="sxs-lookup"><span data-stu-id="d1aca-131">In the **Project types** pane in the **New Project** dialog box, click **Visual Basic**.</span></span>  
  
3. <span data-ttu-id="d1aca-132">按一下 [範本]\*\*\*\* 窗格中的 [主控台應用程式]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d1aca-132">In the **Templates** pane, click **Console Application**.</span></span>  
  
4. <span data-ttu-id="d1aca-133">在 [ **名稱** ] 方塊中，輸入 **LinqDataManipulationApp**。</span><span class="sxs-lookup"><span data-stu-id="d1aca-133">In the **Name** box, type **LinqDataManipulationApp**.</span></span>  
  
5. <span data-ttu-id="d1aca-134">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="d1aca-134">Click **OK**.</span></span>  
  
## <a name="adding-linq-references-and-directives"></a><span data-ttu-id="d1aca-135">加入 LINQ 參考和指示詞</span><span class="sxs-lookup"><span data-stu-id="d1aca-135">Adding LINQ References and Directives</span></span>  

 <span data-ttu-id="d1aca-136">本逐步解說使用的組件，可能在您的專案中預設為不安裝。</span><span class="sxs-lookup"><span data-stu-id="d1aca-136">This walkthrough uses assemblies that might not be installed by default in your project.</span></span> <span data-ttu-id="d1aca-137">如果未 `System.Data.Linq` 在專案中列為參考 (按一下 [顯示**方案總管**中的**所有**檔案]，然後展開 [**參考**] 節點) ，將其加入，如下列步驟所述。</span><span class="sxs-lookup"><span data-stu-id="d1aca-137">If `System.Data.Linq` is not listed as a reference in your project (click **Show All Files** in **Solution Explorer** and expand the **References** node), add it, as explained in the following steps.</span></span>  
  
#### <a name="to-add-systemdatalinq"></a><span data-ttu-id="d1aca-138">若要加入 System.Data.Linq</span><span class="sxs-lookup"><span data-stu-id="d1aca-138">To add System.Data.Linq</span></span>  
  
1. <span data-ttu-id="d1aca-139">在 **方案總管**中，以滑鼠右鍵按一下 [ **參考**]，然後按一下 [ **加入參考**]。</span><span class="sxs-lookup"><span data-stu-id="d1aca-139">In **Solution Explorer**, right-click **References**, and then click **Add Reference**.</span></span>  
  
2. <span data-ttu-id="d1aca-140">在 [ **加入參考** ] 對話方塊中，按一下 [ **.net**]，按一下 [system.string] 元件，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="d1aca-140">In the **Add Reference** dialog box, click **.NET**, click the System.Data.Linq assembly, and then click **OK**.</span></span>  
  
     <span data-ttu-id="d1aca-141">組件隨即加入至專案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-141">The assembly is added to the project.</span></span>  
  
3. <span data-ttu-id="d1aca-142">在 [程式碼編輯器] 中，將下列指示詞加入至 [ **Module1**] 上方：</span><span class="sxs-lookup"><span data-stu-id="d1aca-142">In the code editor, add the following directives above **Module1**:</span></span>  
  
     [!code-vb[DLinqWalk3VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a><span data-ttu-id="d1aca-143">將 Northwind 程式碼檔案加入至專案</span><span class="sxs-lookup"><span data-stu-id="d1aca-143">Adding the Northwind Code File to the Project</span></span>  

 <span data-ttu-id="d1aca-144">這些步驟假設您已使用 SQLMetal 工具，從 Northwind 範例資料庫產生程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-144">These steps assume that you have used the SQLMetal tool to generate a code file from the Northwind sample database.</span></span> <span data-ttu-id="d1aca-145">如需詳細資訊，請參閱本逐步解說稍早的「必要條件」一節。</span><span class="sxs-lookup"><span data-stu-id="d1aca-145">For more information, see the Prerequisites section earlier in this walkthrough.</span></span>  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a><span data-ttu-id="d1aca-146">若要將 Northwind 程式碼檔案加入至專案</span><span class="sxs-lookup"><span data-stu-id="d1aca-146">To add the northwind code file to the project</span></span>  
  
1. <span data-ttu-id="d1aca-147">在 [專案]\*\*\*\* 功能表上，按一下 [新增現有項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d1aca-147">On the **Project** menu, click **Add Existing Item**.</span></span>  
  
2. <span data-ttu-id="d1aca-148">在 [ **加入現有專案** ] 對話方塊中，流覽至 [c:\linqtest2\northwind.vb]，然後按一下 [ **加入**]。</span><span class="sxs-lookup"><span data-stu-id="d1aca-148">In the **Add Existing Item** dialog box, navigate to c:\linqtest2\northwind.vb, and then click **Add**.</span></span>  
  
     <span data-ttu-id="d1aca-149">northwind.vb file 隨即加入至專案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-149">The northwind.vb file is added to the project.</span></span>  
  
## <a name="setting-up-the-database-connection"></a><span data-ttu-id="d1aca-150">設定資料庫連接</span><span class="sxs-lookup"><span data-stu-id="d1aca-150">Setting Up the Database Connection</span></span>  

 <span data-ttu-id="d1aca-151">請先測試與資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="d1aca-151">First, test your connection to the database.</span></span> <span data-ttu-id="d1aca-152">請特別注意，資料庫的名稱 (Northwnd) 沒有字母 i。</span><span class="sxs-lookup"><span data-stu-id="d1aca-152">Note especially that the name of the database, Northwnd, has no i character.</span></span> <span data-ttu-id="d1aca-153">如果在後續步驟發生錯誤，則請檢閱 northwind.vb 檔案，以判斷 Northwind 部分類別的拼法。</span><span class="sxs-lookup"><span data-stu-id="d1aca-153">If you generate errors in the next steps, review the northwind.vb file to determine how the Northwind partial class is spelled.</span></span>  
  
#### <a name="to-set-up-and-test-the-database-connection"></a><span data-ttu-id="d1aca-154">若要設定和測試資料庫連接</span><span class="sxs-lookup"><span data-stu-id="d1aca-154">To set up and test the database connection</span></span>  
  
1. <span data-ttu-id="d1aca-155">在 `Sub Main` 中輸入或貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="d1aca-155">Type or paste the following code into `Sub Main`:</span></span>  
  
     [!code-vb[DLinqWalk3VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#2)]  
  
2. <span data-ttu-id="d1aca-156">按 F5，立即測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1aca-156">Press F5 to test the application at this point.</span></span>  
  
     <span data-ttu-id="d1aca-157">**主控台**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d1aca-157">A **Console** window opens.</span></span>  
  
     <span data-ttu-id="d1aca-158">在**主控台**視窗中按 enter 鍵，或按一下 [Visual Studio **Debug** ] 功能表上的 [**停止調試**程式]，以關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1aca-158">Close the application by pressing Enter in the **Console** window, or by clicking **Stop Debugging** on the Visual Studio **Debug** menu.</span></span>  
  
## <a name="creating-a-new-entity"></a><span data-ttu-id="d1aca-159">建立新的實體</span><span class="sxs-lookup"><span data-stu-id="d1aca-159">Creating a New Entity</span></span>  

 <span data-ttu-id="d1aca-160">建立新的實體十分簡單。</span><span class="sxs-lookup"><span data-stu-id="d1aca-160">Creating a new entity is straightforward.</span></span> <span data-ttu-id="d1aca-161">您可以使用 `Customer` 關鍵字，建立物件 (如 `New`)。</span><span class="sxs-lookup"><span data-stu-id="d1aca-161">You can create objects (such as `Customer`) by using the `New` keyword.</span></span>  
  
 <span data-ttu-id="d1aca-162">在本節和下列各節中，您變更的只是本機快取。</span><span class="sxs-lookup"><span data-stu-id="d1aca-162">In this and the following sections, you are making changes only to the local cache.</span></span> <span data-ttu-id="d1aca-163">在本逐步解說最後呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 之前，都不會將變更傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-163">No changes are sent to the database until you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> toward the end of this walkthrough.</span></span>  
  
#### <a name="to-add-a-new-customer-entity-object"></a><span data-ttu-id="d1aca-164">若要加入新的 Customer 實體物件</span><span class="sxs-lookup"><span data-stu-id="d1aca-164">To add a new Customer entity object</span></span>  
  
1. <span data-ttu-id="d1aca-165">在 `Customer` 中的 `Console.ReadLine` 之前加入下列程式碼，以建立新的 `Sub Main`：</span><span class="sxs-lookup"><span data-stu-id="d1aca-165">Create a new `Customer` by adding the following code before `Console.ReadLine` in `Sub Main`:</span></span>  
  
     [!code-vb[DLinqWalk3VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#3)]  
  
2. <span data-ttu-id="d1aca-166">按 F5 對方案進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="d1aca-166">Press F5 to debug the solution.</span></span>  
  
     <span data-ttu-id="d1aca-167">主控台視窗中顯示的結果如下：</span><span class="sxs-lookup"><span data-stu-id="d1aca-167">The results that are shown in the console window are as follows:</span></span>  
  
     `Customers matching CA before insert:`  
  
     `Customer ID: CACTU`  
  
     `Customer ID: RICAR`  
  
     <span data-ttu-id="d1aca-168">請注意，新的資料列不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="d1aca-168">Note that the new row does not appear in the results.</span></span> <span data-ttu-id="d1aca-169">新的資料尚未送出至資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-169">The new data has not yet been submitted to the database.</span></span>  
  
3. <span data-ttu-id="d1aca-170">在 **主控台** 視窗中按 enter 鍵，以停止調試。</span><span class="sxs-lookup"><span data-stu-id="d1aca-170">Press Enter in the **Console** window to stop debugging.</span></span>  
  
## <a name="updating-an-entity"></a><span data-ttu-id="d1aca-171">更新實體</span><span class="sxs-lookup"><span data-stu-id="d1aca-171">Updating an Entity</span></span>  

 <span data-ttu-id="d1aca-172">在下列步驟中，您會擷取 `Customer` 物件，並修改它的其中一個屬性。</span><span class="sxs-lookup"><span data-stu-id="d1aca-172">In the following steps, you will retrieve a `Customer` object and modify one of its properties.</span></span>  
  
#### <a name="to-change-the-name-of-a-customer"></a><span data-ttu-id="d1aca-173">若要變更 Customer 的名稱</span><span class="sxs-lookup"><span data-stu-id="d1aca-173">To change the name of a Customer</span></span>  
  
- <span data-ttu-id="d1aca-174">將下列程式碼加入至 `Console.ReadLine()` 的上方：</span><span class="sxs-lookup"><span data-stu-id="d1aca-174">Add the following code above `Console.ReadLine()`:</span></span>  
  
     [!code-vb[DLinqWalk3VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#4)]  
  
## <a name="deleting-an-entity"></a><span data-ttu-id="d1aca-175">刪除實體</span><span class="sxs-lookup"><span data-stu-id="d1aca-175">Deleting an Entity</span></span>  

 <span data-ttu-id="d1aca-176">您可以使用同一個客戶物件，刪除第一份訂單。</span><span class="sxs-lookup"><span data-stu-id="d1aca-176">Using the same customer object, you can delete the first order.</span></span>  
  
 <span data-ttu-id="d1aca-177">在下列程式碼中，會示範如何中斷資料列之間的關聯性 (Relationship)，以及如何刪除資料庫中的資料列。</span><span class="sxs-lookup"><span data-stu-id="d1aca-177">The following code demonstrates how to sever relationships between rows, and how to delete a row from the database.</span></span>  
  
#### <a name="to-delete-a-row"></a><span data-ttu-id="d1aca-178">若要刪除資料列</span><span class="sxs-lookup"><span data-stu-id="d1aca-178">To delete a row</span></span>  
  
- <span data-ttu-id="d1aca-179">將下列程式碼加入至 `Console.ReadLine()` 的正上方：</span><span class="sxs-lookup"><span data-stu-id="d1aca-179">Add the following code just above `Console.ReadLine()`:</span></span>  
  
     [!code-vb[DLinqWalk3VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#5)]  
  
## <a name="submitting-changes-to-the-database"></a><span data-ttu-id="d1aca-180">將變更送出至資料庫</span><span class="sxs-lookup"><span data-stu-id="d1aca-180">Submitting Changes to the Database</span></span>  

 <span data-ttu-id="d1aca-181">建立、更新和刪除物件所需的最後一個步驟是實際將變更送出至資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1aca-181">The final step required for creating, updating, and deleting objects is to actually submit the changes to the database.</span></span> <span data-ttu-id="d1aca-182">沒有這個步驟，所進行的變更只是針對本機，並不會出現在查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="d1aca-182">Without this step, your changes are only local and will not appear in query results.</span></span>  
  
#### <a name="to-submit-changes-to-the-database"></a><span data-ttu-id="d1aca-183">若要將變更送出至資料庫</span><span class="sxs-lookup"><span data-stu-id="d1aca-183">To submit changes to the database</span></span>  
  
1. <span data-ttu-id="d1aca-184">將下列程式碼插入至 `Console.ReadLine` 的正上方：</span><span class="sxs-lookup"><span data-stu-id="d1aca-184">Insert the following code just above `Console.ReadLine`:</span></span>  
  
     [!code-vb[DLinqWalk3VB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#6)]  
  
2. <span data-ttu-id="d1aca-185">將下列程式碼插入至 `SubmitChanges` 的後面，以顯示送出變更之前和之後的效果：</span><span class="sxs-lookup"><span data-stu-id="d1aca-185">Insert the following code (after `SubmitChanges`) to show the before and after effects of submitting the changes:</span></span>  
  
     [!code-vb[DLinqWalk3VB#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#7)]  
  
3. <span data-ttu-id="d1aca-186">按 F5 對方案進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="d1aca-186">Press F5 to debug the solution.</span></span>  
  
     <span data-ttu-id="d1aca-187">主控台視窗隨即出現如下內容：</span><span class="sxs-lookup"><span data-stu-id="d1aca-187">The console window appears as follows:</span></span>  
  
    ```console
    Customers matching CA before update:  
    Customer ID: CACTU  
    Customer ID: RICAR  
  
    The Order Detail to be deleted is: OrderID = 10643  
  
    Customers matching CA after update:  
    Customer ID: A3VCA  
    Customer ID: CACTU  
    Customer ID: RICAR  
    ```  
  
4. <span data-ttu-id="d1aca-188">在 **主控台** 視窗中按 enter 鍵，以停止調試。</span><span class="sxs-lookup"><span data-stu-id="d1aca-188">Press Enter in the **Console** window to stop debugging.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d1aca-189">送出變更以加入新的客戶之後，因為您無法再原樣加入同一位客戶，所以無法再原樣執行這個方案。</span><span class="sxs-lookup"><span data-stu-id="d1aca-189">After you have added the new customer by submitting the changes, you cannot execute this solution again as is, because you cannot add the same customer again as is.</span></span> <span data-ttu-id="d1aca-190">若要再執行一次這個方案，請變更要加入的客戶 ID 值。</span><span class="sxs-lookup"><span data-stu-id="d1aca-190">To execute the solution again, change the value of the customer ID to be added.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d1aca-191">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d1aca-191">See also</span></span>

- [<span data-ttu-id="d1aca-192">依逐步解說學習</span><span class="sxs-lookup"><span data-stu-id="d1aca-192">Learning by Walkthroughs</span></span>](learning-by-walkthroughs.md)

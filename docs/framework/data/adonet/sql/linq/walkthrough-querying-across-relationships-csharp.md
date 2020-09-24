---
title: 逐步解說：跨關聯性查詢 (C#)
ms.date: 03/30/2017
ms.assetid: 552abeb1-18f2-4e93-a9c6-ef7b2db30c32
ms.openlocfilehash: 9dfe34136f2d0a14a12f72e22a96d1882ddbce49
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164008"
---
# <a name="walkthrough-querying-across-relationships-c"></a><span data-ttu-id="fcc5f-102">逐步解說：跨關聯性查詢 (C#)</span><span class="sxs-lookup"><span data-stu-id="fcc5f-102">Walkthrough: Querying Across Relationships (C#)</span></span>

<span data-ttu-id="fcc5f-103">本逐步解說示範如何使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *關聯* 來表示資料庫中的外鍵關聯性。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-103">This walkthrough demonstrates the use of [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *associations* to represent foreign-key relationships in the database.</span></span>  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 <span data-ttu-id="fcc5f-104">本逐步解說的內容是依據 Visual C# 開發設定所撰寫的。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-104">This walkthrough was written by using Visual C# Development Settings.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="fcc5f-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="fcc5f-105">Prerequisites</span></span>  

 <span data-ttu-id="fcc5f-106">您必須已完成 [逐步解說：簡單的物件模型和查詢 (c # ) ](walkthrough-simple-object-model-and-query-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-106">You must have completed [Walkthrough: Simple Object Model and Query (C#)](walkthrough-simple-object-model-and-query-csharp.md).</span></span> <span data-ttu-id="fcc5f-107">此逐步解說建立於該逐步解說之上，其中包含出現在 c:\linqtest5 中的 northwnd.mdf 檔。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-107">This walkthrough builds on that one, including the presence of the northwnd.mdf file in c:\linqtest5.</span></span>  
  
## <a name="overview"></a><span data-ttu-id="fcc5f-108">概觀</span><span class="sxs-lookup"><span data-stu-id="fcc5f-108">Overview</span></span>  

 <span data-ttu-id="fcc5f-109">此逐步解說包含三項主要工作：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-109">This walkthrough consists of three main tasks:</span></span>  
  
- <span data-ttu-id="fcc5f-110">加入實體類別，以表示 Northwind 範例資料庫中的 Orders 資料表。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-110">Adding an entity class to represent the Orders table in the sample Northwind database.</span></span>  
  
- <span data-ttu-id="fcc5f-111">補充 `Customer` 類別的附註，以加強 `Customer` 和 `Order` 類別之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-111">Supplementing annotations to the `Customer` class to enhance the relationship between the `Customer` and `Order` classes.</span></span>  
  
- <span data-ttu-id="fcc5f-112">建立和執行查詢，以測試使用 `Order` 類別取得 `Customer` 資訊。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-112">Creating and running a query to test obtaining `Order` information by using the `Customer` class.</span></span>  
  
## <a name="mapping-relationships-across-tables"></a><span data-ttu-id="fcc5f-113">跨資料表對應關聯性</span><span class="sxs-lookup"><span data-stu-id="fcc5f-113">Mapping Relationships Across Tables</span></span>  

 <span data-ttu-id="fcc5f-114">在 `Customer` 類別定義之後，建立包含下列程式碼的 `Order` 實體類別定義，這表示 `Order.Customer` 為 `Customer.CustomerID` 的外部索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-114">After the `Customer` class definition, create the `Order` entity class definition that includes the following code, which indicates that `Order.Customer` relates as a foreign key to `Customer.CustomerID`.</span></span>  
  
### <a name="to-add-the-order-entity-class"></a><span data-ttu-id="fcc5f-115">若要加入 Order 實體類別</span><span class="sxs-lookup"><span data-stu-id="fcc5f-115">To add the Order entity class</span></span>  
  
- <span data-ttu-id="fcc5f-116">在 `Customer` 類別之後輸入或貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-116">Type or paste the following code after the `Customer` class:</span></span>  
  
     [!code-csharp[DLinqWalk2CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#1)]  
  
## <a name="annotating-the-customer-class"></a><span data-ttu-id="fcc5f-117">加入 Customer 類別的附註</span><span class="sxs-lookup"><span data-stu-id="fcc5f-117">Annotating the Customer Class</span></span>  

 <span data-ttu-id="fcc5f-118">在這個步驟中，您會加入 `Customer` 類別的附註，指出其與 `Order` 類別的關聯性</span><span class="sxs-lookup"><span data-stu-id="fcc5f-118">In this step, you annotate the `Customer` class to indicate its relationship to the `Order` class.</span></span> <span data-ttu-id="fcc5f-119">(此加入動作並非絕對必要，因為定義任一方向的關聯性就足以建立連結。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-119">(This addition is not strictly necessary, because defining the relationship in either direction is sufficient to create the link.</span></span> <span data-ttu-id="fcc5f-120">但加入此附註確實可讓您輕易地以任一方向巡覽物件)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-120">But adding this annotation does enable you to easily navigate objects in either direction.)</span></span>  
  
### <a name="to-annotate-the-customer-class"></a><span data-ttu-id="fcc5f-121">若要標註 Customer 類別</span><span class="sxs-lookup"><span data-stu-id="fcc5f-121">To annotate the Customer class</span></span>  
  
- <span data-ttu-id="fcc5f-122">將下列程式碼輸入或貼到 `Customer` 類別中：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-122">Type or paste the following code into the `Customer` class:</span></span>  
  
     [!code-csharp[DLinqWalk2CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a><span data-ttu-id="fcc5f-123">建立和執行客戶-訂單關聯性的查詢</span><span class="sxs-lookup"><span data-stu-id="fcc5f-123">Creating and Running a Query Across the Customer-Order Relationship</span></span>  

 <span data-ttu-id="fcc5f-124">您現在可以直接從 `Order` 物件存取 `Customer` 物件，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-124">You can now access `Order` objects directly from the `Customer` objects, or in the opposite order.</span></span> <span data-ttu-id="fcc5f-125">客戶與訂單之間不需要明確的 *聯結* 。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-125">You do not need an explicit *join* between customers and orders.</span></span>  
  
### <a name="to-access-order-objects-by-using-customer-objects"></a><span data-ttu-id="fcc5f-126">若要使用 Customer 物件存取 Order 物件</span><span class="sxs-lookup"><span data-stu-id="fcc5f-126">To access Order objects by using Customer objects</span></span>  
  
1. <span data-ttu-id="fcc5f-127">將下列程式碼輸入或貼到 `Main` 方法，進而修改此方法：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-127">Modify the `Main` method by typing or pasting the following code into the method:</span></span>  
  
     [!code-csharp[DLinqWalk2CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#3)]  
  
2. <span data-ttu-id="fcc5f-128">按 F5 對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-128">Press F5 to debug your application.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="fcc5f-129">您可以將 `db.Log = Console.Out;` 標記為註解，以便在主控台視窗中排除 SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-129">You can eliminate the SQL code in the Console window by commenting out `db.Log = Console.Out;`.</span></span>  
  
3. <span data-ttu-id="fcc5f-130">在主控台視窗中按 Enter 鍵，以停止偵錯。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-130">Press Enter in the Console window to stop debugging.</span></span>  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a><span data-ttu-id="fcc5f-131">建立資料庫的強型別檢視</span><span class="sxs-lookup"><span data-stu-id="fcc5f-131">Creating a Strongly Typed View of Your Database</span></span>  

 <span data-ttu-id="fcc5f-132">從資料庫的強型別檢視著手會容易許多。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-132">It is much easier to start with a strongly typed view of your database.</span></span> <span data-ttu-id="fcc5f-133">透過建立強型別 <xref:System.Data.Linq.DataContext> 物件，您就不需要呼叫 <xref:System.Data.Linq.DataContext.GetTable%2A>。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-133">By strongly typing the <xref:System.Data.Linq.DataContext> object, you do not need calls to <xref:System.Data.Linq.DataContext.GetTable%2A>.</span></span> <span data-ttu-id="fcc5f-134">當您使用強型別 <xref:System.Data.Linq.DataContext> 物件時，可以在所有查詢中使用強型別資料表。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-134">You can use strongly typed tables in all your queries when you use the strongly typed <xref:System.Data.Linq.DataContext> object.</span></span>  
  
 <span data-ttu-id="fcc5f-135">在下列步驟中，您會將 `Customers` 建立為強型別資料表，以對應資料庫中的 Customers 資料表。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-135">In the following steps, you will create `Customers` as a strongly typed table that maps to the Customers table in the database.</span></span>  
  
### <a name="to-strongly-type-the-datacontext-object"></a><span data-ttu-id="fcc5f-136">若要建立強型別 DataContext 物件</span><span class="sxs-lookup"><span data-stu-id="fcc5f-136">To strongly type the DataContext object</span></span>  
  
1. <span data-ttu-id="fcc5f-137">在 `Customer` 類別宣告之上加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-137">Add the following code above the `Customer` class declaration.</span></span>  
  
     [!code-csharp[DLinqWalk2CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#4)]  
  
2. <span data-ttu-id="fcc5f-138">修改 `Main` 方法以使用強型別 <xref:System.Data.Linq.DataContext>，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-138">Modify the `Main` method to use the strongly typed <xref:System.Data.Linq.DataContext> as follows:</span></span>  
  
     [!code-csharp[DLinqWalk2CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#5)]  
  
3. <span data-ttu-id="fcc5f-139">按 F5 對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-139">Press F5 to debug your application.</span></span>  
  
     <span data-ttu-id="fcc5f-140">主控台視窗輸出為：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-140">The Console window output is:</span></span>  
  
     `ID=WHITC`  
  
4. <span data-ttu-id="fcc5f-141">在主控台視窗中按 Enter 鍵，以停止偵錯。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-141">Press Enter in the console window to stop debugging.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="fcc5f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcc5f-142">Next Steps</span></span>  

 <span data-ttu-id="fcc5f-143">下一個逐步解說 ([逐步解說：運算元據 (c # ) ](walkthrough-manipulating-data-csharp.md)) 示範如何運算元據。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-143">The next walkthrough ([Walkthrough: Manipulating Data (C#)](walkthrough-manipulating-data-csharp.md)) demonstrates how to manipulate data.</span></span> <span data-ttu-id="fcc5f-144">該逐步解說並不要求您儲存這系列中已完成的兩個逐步解說。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-144">That walkthrough does not require that you save the two walkthroughs in this series that you have already completed.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fcc5f-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fcc5f-145">See also</span></span>

- [<span data-ttu-id="fcc5f-146">依逐步解說學習</span><span class="sxs-lookup"><span data-stu-id="fcc5f-146">Learning by Walkthroughs</span></span>](learning-by-walkthroughs.md)

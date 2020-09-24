---
title: LINQ to SQL 的功能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 061d98b2-baa7-4336-8ad2-c14de8134d91
ms.openlocfilehash: a2e65cb558eec3cec21ea0efbcc66bb8c56ec7b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91163917"
---
# <a name="what-you-can-do-with-linq-to-sql"></a><span data-ttu-id="af491-102">LINQ to SQL 的功能</span><span class="sxs-lookup"><span data-stu-id="af491-102">What You Can Do With LINQ to SQL</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="af491-103">支援 SQL 開發人員需要的所有重要功能。</span><span class="sxs-lookup"><span data-stu-id="af491-103">supports all the key capabilities you would expect as a SQL developer.</span></span> <span data-ttu-id="af491-104">您可以查詢資訊，以及在資料表中插入、更新和刪除資訊。</span><span class="sxs-lookup"><span data-stu-id="af491-104">You can query for information, and insert, update, and delete information from tables.</span></span>  
  
## <a name="selecting"></a><span data-ttu-id="af491-105">選取</span><span class="sxs-lookup"><span data-stu-id="af491-105">Selecting</span></span>  

 <span data-ttu-id="af491-106">只要以自己的程式設計語言撰寫 LINQ 查詢，然後執行該查詢來取得結果，就可以選取 (*投射*) 。</span><span class="sxs-lookup"><span data-stu-id="af491-106">Selecting (*projection*) is achieved by just writing a LINQ query in your own programming language, and then executing that query to retrieve the results.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="af491-107">會將所有必要的作業轉譯成熟悉的 SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="af491-107">itself translates all the necessary operations into the necessary SQL operations that you are familiar with.</span></span> <span data-ttu-id="af491-108">如需詳細資訊，請參閱 [LINQ to SQL](index.md)。</span><span class="sxs-lookup"><span data-stu-id="af491-108">For more information, see [LINQ to SQL](index.md).</span></span>  
  
 <span data-ttu-id="af491-109">在下列範例中，會擷取 London 客戶的公司名稱，並將它們顯示在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="af491-109">In the following example, the company names of customers from London are retrieved and displayed in the console window.</span></span>  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## <a name="inserting"></a><span data-ttu-id="af491-110">插入</span><span class="sxs-lookup"><span data-stu-id="af491-110">Inserting</span></span>  

 <span data-ttu-id="af491-111">若要執行 SQL `Insert`，只要將物件加入至所建立的物件模型，並在 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 上呼叫 <xref:System.Data.Linq.DataContext>即可。</span><span class="sxs-lookup"><span data-stu-id="af491-111">To execute a SQL `Insert`, just add objects to the object model you have created, and call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> on the <xref:System.Data.Linq.DataContext>.</span></span>  
  
 <span data-ttu-id="af491-112">在下列範例中，會使用 `Customers` 將新的客戶與該客戶的相關資訊加入至 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>資料表。</span><span class="sxs-lookup"><span data-stu-id="af491-112">In the following example, a new customer and information about the customer is added to the `Customers` table by using <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>.</span></span>  
  
 [!code-csharp[DLinqGettingStarted#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#2)]
 [!code-vb[DLinqGettingStarted#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#2)]  
  
## <a name="updating"></a><span data-ttu-id="af491-113">更新</span><span class="sxs-lookup"><span data-stu-id="af491-113">Updating</span></span>  

 <span data-ttu-id="af491-114">若要更新 ( `Update` ) 資料庫項目，請先擷取該項目，然後直接在物件模型中編輯該項目。</span><span class="sxs-lookup"><span data-stu-id="af491-114">To `Update` a database entry, first retrieve the item and edit it directly in the object model.</span></span> <span data-ttu-id="af491-115">修改物件之後，再於 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 上呼叫 <xref:System.Data.Linq.DataContext> 以更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="af491-115">After you have modified the object, call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> on the <xref:System.Data.Linq.DataContext> to update the database.</span></span>  
  
 <span data-ttu-id="af491-116">在下列範例中，會擷取所有來自 London 的客戶，</span><span class="sxs-lookup"><span data-stu-id="af491-116">In the following example, all customers who are from London are retrieved.</span></span> <span data-ttu-id="af491-117">然後將城市的名稱從 "London" 變更為 "London - Metro"。</span><span class="sxs-lookup"><span data-stu-id="af491-117">Then the name of the city is changed from "London" to "London - Metro".</span></span> <span data-ttu-id="af491-118">最後，會呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ，以將變更傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="af491-118">Finally, <xref:System.Data.Linq.DataContext.SubmitChanges%2A> is called to send the changes to the database.</span></span>  
  
 [!code-csharp[DLinqGettingStarted#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#3)]
 [!code-vb[DLinqGettingStarted#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#3)]  
  
## <a name="deleting"></a><span data-ttu-id="af491-119">刪除</span><span class="sxs-lookup"><span data-stu-id="af491-119">Deleting</span></span>  

 <span data-ttu-id="af491-120">若要刪除 ( `Delete` ) 項目，請從項目所屬的集合中移除該項目，然後在 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 上呼叫 <xref:System.Data.Linq.DataContext> ，以認可變更。</span><span class="sxs-lookup"><span data-stu-id="af491-120">To `Delete` an item, remove the item from the collection to which it belongs, and then call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> on the <xref:System.Data.Linq.DataContext> to commit the change.</span></span>  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="af491-121">無法辨識串聯刪除作業。</span><span class="sxs-lookup"><span data-stu-id="af491-121">does not recognize cascade-delete operations.</span></span> <span data-ttu-id="af491-122">如果您想要刪除有條件約束之資料表中的資料列，請參閱 [如何：從資料庫刪除資料列](how-to-delete-rows-from-the-database.md)。</span><span class="sxs-lookup"><span data-stu-id="af491-122">If you want to delete a row in a table that has constraints against it, see [How to: Delete Rows From the Database](how-to-delete-rows-from-the-database.md).</span></span>  
  
 <span data-ttu-id="af491-123">在下列範例中，會從資料庫中擷取 `CustomerID` 為 `98128` 的客戶。</span><span class="sxs-lookup"><span data-stu-id="af491-123">In the following example, the customer who has `CustomerID` of `98128` is retrieved from the database.</span></span> <span data-ttu-id="af491-124">然後會在確認已擷取該客戶的資料列之後，呼叫 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> ，以從集合中移除該物件。</span><span class="sxs-lookup"><span data-stu-id="af491-124">Then, after confirming that the customer row was retrieved, <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> is called to remove that object from the collection.</span></span> <span data-ttu-id="af491-125">最後，會呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ，以將刪除轉送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="af491-125">Finally, <xref:System.Data.Linq.DataContext.SubmitChanges%2A> is called to forward the deletion to the database.</span></span>  
  
 [!code-csharp[DLinqGettingStarted#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#4)]
 [!code-vb[DLinqGettingStarted#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="af491-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af491-126">See also</span></span>

- [<span data-ttu-id="af491-127">程式設計指南</span><span class="sxs-lookup"><span data-stu-id="af491-127">Programming Guide</span></span>](programming-guide.md)
- [<span data-ttu-id="af491-128">LINQ to SQL 物件模型</span><span class="sxs-lookup"><span data-stu-id="af491-128">The LINQ to SQL Object Model</span></span>](the-linq-to-sql-object-model.md)
- [<span data-ttu-id="af491-129">快速入門</span><span class="sxs-lookup"><span data-stu-id="af491-129">Getting Started</span></span>](getting-started.md)

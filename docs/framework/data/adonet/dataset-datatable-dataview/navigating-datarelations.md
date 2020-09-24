---
title: 導覽 DataRelation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 5eb2ee16712be5ccd5e9aa0af4dde22dcaaeea09
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148382"
---
# <a name="navigating-datarelations"></a><span data-ttu-id="cf27b-102">導覽 DataRelation</span><span class="sxs-lookup"><span data-stu-id="cf27b-102">Navigating DataRelations</span></span>

<span data-ttu-id="cf27b-103"><xref:System.Data.DataRelation> 的其中一個主要功能，是讓您可以從 <xref:System.Data.DataTable> 內的某個 <xref:System.Data.DataSet> 巡覽至另一個。</span><span class="sxs-lookup"><span data-stu-id="cf27b-103">One of the primary functions of a <xref:System.Data.DataRelation> is to allow navigation from one <xref:System.Data.DataTable> to another within a <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="cf27b-104">這可讓您在 <xref:System.Data.DataRow> 指定來自相關**datatable**的單一**DataRow**時，從一個**datatable**中取出所有相關物件。</span><span class="sxs-lookup"><span data-stu-id="cf27b-104">This allows you to retrieve all the related <xref:System.Data.DataRow> objects in one **DataTable** when given a single **DataRow** from a related **DataTable**.</span></span> <span data-ttu-id="cf27b-105">例如，在客戶資料表與訂單資料表之間建立 **DataRelation** 之後，您就可以使用 **GetChildRows**抓取特定客戶資料列的所有訂單資料列。</span><span class="sxs-lookup"><span data-stu-id="cf27b-105">For example, after establishing a **DataRelation** between a table of customers and a table of orders, you can retrieve all the order rows for a particular customer row using **GetChildRows**.</span></span>  
  
 <span data-ttu-id="cf27b-106">下列程式碼範例會在**Customers**資料表和**資料集**的**orders**資料表之間建立**DataRelation** ，並傳回每個客戶的所有訂單。</span><span class="sxs-lookup"><span data-stu-id="cf27b-106">The following code example creates a **DataRelation** between the **Customers** table and the **Orders** table of a **DataSet** and returns all the orders for each customer.</span></span>  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 <span data-ttu-id="cf27b-107">下一個範例則是以前述範例為基礎，在四個資料表之間建立關聯，並巡覽其中的關聯性。</span><span class="sxs-lookup"><span data-stu-id="cf27b-107">The next example builds on the preceding example, relating four tables together and navigating those relationships.</span></span> <span data-ttu-id="cf27b-108">如同上述範例， **CustomerID** 會將 **Customers** 資料表與 **Orders** 資料表產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cf27b-108">As in the previous example, **CustomerID** relates the **Customers** table to the **Orders** table.</span></span> <span data-ttu-id="cf27b-109">針對**Customers**資料表中的每個客戶，會決定**orders**資料表中的所有子資料列，以便傳回特定客戶擁有的訂單**數目及其訂單值。**</span><span class="sxs-lookup"><span data-stu-id="cf27b-109">For each customer in the **Customers** table, all the child rows in the **Orders** table are determined, in order to return the number of orders a particular customer has and their **OrderID** values.</span></span>  
  
 <span data-ttu-id="cf27b-110">展開的範例也會傳回來自 **OrderDetails** 和 **Products** 資料表的值。</span><span class="sxs-lookup"><span data-stu-id="cf27b-110">The expanded example also returns the values from the **OrderDetails** and **Products** tables.</span></span> <span data-ttu-id="cf27b-111">**Orders**資料表**與使用「訂單表**」的**OrderDetails**資料表相關，以決定每個客戶訂單的訂購產品和數量。</span><span class="sxs-lookup"><span data-stu-id="cf27b-111">The **Orders** table is related to the **OrderDetails** table using **OrderID** to determine, for each customer order, what products and quantities were ordered.</span></span> <span data-ttu-id="cf27b-112">因為**OrderDetails**資料表只包含已訂購產品的**Productid** ，所以**OrderDetails**會與使用**ProductID**的**產品**相關，以便傳回**ProductName**。</span><span class="sxs-lookup"><span data-stu-id="cf27b-112">Because the **OrderDetails** table only contains the **ProductID** of an ordered product, **OrderDetails** is related to **Products** using **ProductID** in order to return the **ProductName**.</span></span> <span data-ttu-id="cf27b-113">在這種關聯性中， **Products** 資料表是父系，而 **Order Details** 資料表則是子系。</span><span class="sxs-lookup"><span data-stu-id="cf27b-113">In this relation, the **Products** table is the parent and the **Order Details** table is the child.</span></span> <span data-ttu-id="cf27b-114">因此，逐一查看 **OrderDetails** 資料表時，會呼叫 **GetParentRow** 以抓取相關的 **ProductName** 值。</span><span class="sxs-lookup"><span data-stu-id="cf27b-114">As a result, when iterating through the **OrderDetails** table, **GetParentRow** is called to retrieve the related **ProductName** value.</span></span>  
  
 <span data-ttu-id="cf27b-115">請注意，為**Customers**和**Orders**資料表建立**DataRelation**時，不會為**createConstraints**旗標指定值 (預設值為**true**) 。</span><span class="sxs-lookup"><span data-stu-id="cf27b-115">Notice that when the **DataRelation** is created for the **Customers** and **Orders** tables, no value is specified for the **createConstraints** flag (the default is **true**).</span></span> <span data-ttu-id="cf27b-116">這會假設 **Orders** 資料表中的所有資料列都有一個 **CustomerID** 值存在於父 **Customers** 資料表中。</span><span class="sxs-lookup"><span data-stu-id="cf27b-116">This assumes that all the rows in the **Orders** table have a **CustomerID** value that exists in the parent **Customers** table.</span></span> <span data-ttu-id="cf27b-117">如果**Orders**資料表中沒有**CustomerID**存在於**Customers**資料表中，則會擲回例外狀況 <xref:System.Data.ForeignKeyConstraint> 。</span><span class="sxs-lookup"><span data-stu-id="cf27b-117">If a **CustomerID** exists in the **Orders** table that does not exist in the **Customers** table, a <xref:System.Data.ForeignKeyConstraint> causes an exception to be thrown.</span></span>  
  
 <span data-ttu-id="cf27b-118">當子資料行可能包含父資料行不包含的值時，請在加入**DataRelation**時將**createConstraints**旗標設定為**false** 。</span><span class="sxs-lookup"><span data-stu-id="cf27b-118">When the child column might contain values that the parent column does not contain, set the **createConstraints** flag to **false** when adding the **DataRelation**.</span></span> <span data-ttu-id="cf27b-119">在此範例中， **Orders**資料表和**OrderDetails**資料表之間的**DataRelation** **createConstraints**旗標設為**false** 。</span><span class="sxs-lookup"><span data-stu-id="cf27b-119">In the example, the **createConstraints** flag is set to **false** for the **DataRelation** between the **Orders** table and the **OrderDetails** table.</span></span> <span data-ttu-id="cf27b-120">這可讓應用程式從 **OrderDetails** 資料表傳回所有記錄，而不會產生執行時間例外狀況，只傳回 **Orders** 資料表中的記錄子集。</span><span class="sxs-lookup"><span data-stu-id="cf27b-120">This enables the application to return all the records from the **OrderDetails** table and only a subset of records from the **Orders** table without generating a run-time exception.</span></span> <span data-ttu-id="cf27b-121">展開範例會產生下列格式的輸出。</span><span class="sxs-lookup"><span data-stu-id="cf27b-121">The expanded sample generates output in the following format.</span></span>  
  
```output  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 <span data-ttu-id="cf27b-122">下列程式碼範例是展開的範例，其中會傳回來自 **OrderDetails** 和 **Products** 資料表的值，其中只會傳回 **Orders** 資料表中的記錄子集。</span><span class="sxs-lookup"><span data-stu-id="cf27b-122">The following code example is an expanded sample where the values from the **OrderDetails** and **Products** tables are returned, with only a subset of the records in the **Orders** table being returned.</span></span>  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="cf27b-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cf27b-123">See also</span></span>

- [<span data-ttu-id="cf27b-124">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="cf27b-124">DataSets, DataTables, and DataViews</span></span>](index.md)
- <span data-ttu-id="cf27b-125">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="cf27b-125">[ADO.NET Overview](../ado-net-overview.md)</span></span>

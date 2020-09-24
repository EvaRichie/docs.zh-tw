---
title: 使用預存程序修改資料
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.openlocfilehash: 65116a48533fd6ce86894c6a4522929285f8e1f0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150748"
---
# <a name="modifying-data-with-stored-procedures"></a><span data-ttu-id="f23ac-102">使用預存程序修改資料</span><span class="sxs-lookup"><span data-stu-id="f23ac-102">Modifying Data with Stored Procedures</span></span>

<span data-ttu-id="f23ac-103">預存程序 (Stored Procedure) 可以接受資料做為輸入參數，也可以將資料以輸出參數、結果集 (Result Set) 或傳回值的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="f23ac-103">Stored procedures can accept data as input parameters and can return data as output parameters, result sets, or return values.</span></span> <span data-ttu-id="f23ac-104">下列範例說明 ADO.NET 如何傳送及接收輸入參數、輸出參數和傳回值。</span><span class="sxs-lookup"><span data-stu-id="f23ac-104">The sample below illustrates how ADO.NET sends and receives input parameters, output parameters, and return values.</span></span> <span data-ttu-id="f23ac-105">此範例會將新記錄插入資料表 (該資料表的主索引鍵資料行是 SQL Server 資料庫中的識別欄位)。</span><span class="sxs-lookup"><span data-stu-id="f23ac-105">The example inserts a new record into a table where the primary key column is an identity column in a SQL Server database.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f23ac-106">如果您要使用 SQL Server 預存程序搭配 <xref:System.Data.SqlClient.SqlDataAdapter> 來編輯或刪除資料，請務必不要在預存程序定義中使用 SET NOCOUNT ON。</span><span class="sxs-lookup"><span data-stu-id="f23ac-106">If you are using SQL Server stored procedures to edit or delete data using a <xref:System.Data.SqlClient.SqlDataAdapter>, make sure that you do not use SET NOCOUNT ON in the stored procedure definition.</span></span> <span data-ttu-id="f23ac-107">因為這樣會讓傳回的受影響資料列計數成為零，而 `DataAdapter` 會將它解譯為並行衝突。</span><span class="sxs-lookup"><span data-stu-id="f23ac-107">This causes the rows affected count returned to be zero, which the `DataAdapter` interprets as a concurrency conflict.</span></span> <span data-ttu-id="f23ac-108">在此事件中，系統會擲回 <xref:System.Data.DBConcurrencyException>。</span><span class="sxs-lookup"><span data-stu-id="f23ac-108">In this event, a <xref:System.Data.DBConcurrencyException> will be thrown.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f23ac-109">範例</span><span class="sxs-lookup"><span data-stu-id="f23ac-109">Example</span></span>  

 <span data-ttu-id="f23ac-110">此範例會使用下列預存程式，將新的分類插入 **Northwind** **分類** 資料表中。</span><span class="sxs-lookup"><span data-stu-id="f23ac-110">The sample uses the following stored procedure to insert a new category into the **Northwind** **Categories** table.</span></span> <span data-ttu-id="f23ac-111">預存程式會採用 [ **類別名稱** ] 資料行中的值做為輸入參數，並使用 SCOPE_IDENTITY ( # A1 函式來抓取識別欄位的新值，並將其設為 [ **類別**名稱]，並在輸出參數中傳回。</span><span class="sxs-lookup"><span data-stu-id="f23ac-111">The stored procedure takes the value in the **CategoryName** column as an input parameter and uses the SCOPE_IDENTITY() function to retrieve the new value of the identity field, **CategoryID**, and return it in an output parameter.</span></span> <span data-ttu-id="f23ac-112">RETURN 語句會使用 @ @ROWCOUNT 函數來傳回插入的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="f23ac-112">The RETURN statement uses the @@ROWCOUNT function to return the number of rows inserted.</span></span>  
  
```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  
  
 <span data-ttu-id="f23ac-113">下列程式碼範例使用以上所示的 `InsertCategory` 預存程序做為 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 的 <xref:System.Data.SqlClient.SqlDataAdapter> 的來源。</span><span class="sxs-lookup"><span data-stu-id="f23ac-113">The following code example uses the `InsertCategory` stored procedure shown above as the source for the <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> of the <xref:System.Data.SqlClient.SqlDataAdapter>.</span></span> <span data-ttu-id="f23ac-114">在呼叫 `@Identity` 的 <xref:System.Data.DataSet> 方法而將記錄插入至資料庫之後，`Update` 輸出參數將反映在 <xref:System.Data.SqlClient.SqlDataAdapter> 中。</span><span class="sxs-lookup"><span data-stu-id="f23ac-114">The `@Identity` output parameter will be reflected in the <xref:System.Data.DataSet> after the record has been inserted into the database when the `Update` method of the <xref:System.Data.SqlClient.SqlDataAdapter> is called.</span></span> <span data-ttu-id="f23ac-115">程式碼也會擷取傳回值。</span><span class="sxs-lookup"><span data-stu-id="f23ac-115">The code also retrieves the return value.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f23ac-116">使用時 <xref:System.Data.OleDb.OleDbDataAdapter> ，您必須在 <xref:System.Data.ParameterDirection> 其他參數之前指定具有 **ReturnValue** 的參數。</span><span class="sxs-lookup"><span data-stu-id="f23ac-116">When using the <xref:System.Data.OleDb.OleDbDataAdapter>, you must specify parameters with a <xref:System.Data.ParameterDirection> of **ReturnValue** before the other parameters.</span></span>  
  
 [!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/VB/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="f23ac-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f23ac-117">See also</span></span>

- [<span data-ttu-id="f23ac-118">在 ADO.NET 中傳送和修改資料</span><span class="sxs-lookup"><span data-stu-id="f23ac-118">Retrieving and Modifying Data in ADO.NET</span></span>](retrieving-and-modifying-data.md)
- [<span data-ttu-id="f23ac-119">DataAdapter 和 DataReader</span><span class="sxs-lookup"><span data-stu-id="f23ac-119">DataAdapters and DataReaders</span></span>](dataadapters-and-datareaders.md)
- [<span data-ttu-id="f23ac-120">執行命令</span><span class="sxs-lookup"><span data-stu-id="f23ac-120">Executing a Command</span></span>](executing-a-command.md)
- <span data-ttu-id="f23ac-121">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="f23ac-121">[ADO.NET Overview](ado-net-overview.md)</span></span>

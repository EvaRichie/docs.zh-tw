---
title: GetSchema 和結構描述集合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab93b89-1221-427c-84ad-04803b3c64b4
ms.openlocfilehash: cea9deb7fe019fea189a87fc08468d010929db9a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177445"
---
# <a name="getschema-and-schema-collections"></a><span data-ttu-id="15ce6-102">GetSchema 和結構描述集合</span><span class="sxs-lookup"><span data-stu-id="15ce6-102">GetSchema and Schema Collections</span></span>

<span data-ttu-id="15ce6-103">每個 .NET Framework managed 提供者中的 **連接** 類別都會採用 **GetSchema** 方法，此方法可用來取得目前連接之資料庫的架構資訊，而從 **GetSchema** 方法傳回的架構資訊則會以的形式呈現 <xref:System.Data.DataTable> 。</span><span class="sxs-lookup"><span data-stu-id="15ce6-103">The **Connection** classes in each of the .NET Framework managed providers implement a **GetSchema** method which is used to retrieve schema information about the database that is currently connected, and the schema information returned from the **GetSchema** method comes in the form of a <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="15ce6-104">**GetSchema**方法是一種多載方法，可提供選擇性參數來指定要傳回的架構集合，以及限制傳回的資訊量。</span><span class="sxs-lookup"><span data-stu-id="15ce6-104">The **GetSchema** method is an overloaded method that provides optional parameters for specifying the schema collection to return, and restricting the amount of information returned.</span></span>  
  
## <a name="specifying-the-schema-collections"></a><span data-ttu-id="15ce6-105">指定結構描述集合</span><span class="sxs-lookup"><span data-stu-id="15ce6-105">Specifying the Schema Collections</span></span>  

 <span data-ttu-id="15ce6-106">**GetSchema**方法的第一個選擇性參數是指定為字串的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="15ce6-106">The first optional parameter of the **GetSchema** method is the collection name which is specified as a string.</span></span> <span data-ttu-id="15ce6-107">結構描述集合有兩種型別：通用於所有提供者的通用結構描述集合與每個提供者特有的特定結構描述集合。</span><span class="sxs-lookup"><span data-stu-id="15ce6-107">There are two types of schema collections: common schema collections that are common to all providers, and specific schema collections which are specific to each provider.</span></span>  
  
 <span data-ttu-id="15ce6-108">您可以藉由呼叫 **GetSchema** 方法（不含引數）或架構集合名稱 ">metadatacollections" 來查詢 .NET Framework 的 managed 提供者，以判斷支援的架構集合清單。</span><span class="sxs-lookup"><span data-stu-id="15ce6-108">You can query a .NET Framework managed provider to determine the list of supported schema collections by calling the **GetSchema** method with no arguments, or with the schema collection name "MetaDataCollections".</span></span> <span data-ttu-id="15ce6-109">這會傳回 <xref:System.Data.DataTable>，包括支援的結構描述集合清單、每個集合所支援的限制數目，以及集合所使用之識別項部分的數目。</span><span class="sxs-lookup"><span data-stu-id="15ce6-109">This will return a <xref:System.Data.DataTable> with a list of the supported schema collections, the number of restrictions that they each support, and the number of identifier parts that they use.</span></span>  
  
### <a name="retrieving-schema-collections-example"></a><span data-ttu-id="15ce6-110">擷取結構描述集合範例</span><span class="sxs-lookup"><span data-stu-id="15ce6-110">Retrieving Schema Collections Example</span></span>  

 <span data-ttu-id="15ce6-111">下列範例示範如何使用 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> SQL Server 類別 .NET Framework Data Provider 的方法 <xref:System.Data.SqlClient.SqlConnection> ，來取得 **AdventureWorks** 範例資料庫中包含之所有資料表的架構資訊：</span><span class="sxs-lookup"><span data-stu-id="15ce6-111">The following examples demonstrate how to use the <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> method of the .NET Framework Data Provider for the SQL Server <xref:System.Data.SqlClient.SqlConnection> class to retrieve schema information about all of the tables contained in the **AdventureWorks** sample database:</span></span>  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
   Sub Main()  
      Dim connectionString As String = GetConnectionString()  
      Using connection As New SqlConnection(connectionString)  
         'Connect to the database then retrieve the schema information.  
         connection.Open()  
         Dim table As DataTable = connection.GetSchema("Tables")  
  
         ' Display the contents of the table.  
         DisplayData(table)  
         Console.WriteLine("Press any key to continue.")  
         Console.ReadKey()  
      End Using  
   End Sub  
  
   Private Function GetConnectionString() As String  
      ' To avoid storing the connection string in your code,
      ' you can retrieve it from a configuration file.  
      Return "Data Source=(local);Database=AdventureWorks;" _  
         & "Integrated Security=true;"  
   End Function  
  
   Private Sub DisplayData(ByVal table As DataTable)  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
   End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
  string connectionString = GetConnectionString();  
  using (SqlConnection connection = new SqlConnection(connectionString))  
  {  
   // Connect to the database then retrieve the schema information.  
   connection.Open();  
   DataTable table = connection.GetSchema("Tables");  
  
   // Display the contents of the table.  
   DisplayData(table);  
   Console.WriteLine("Press any key to continue.");  
   Console.ReadKey();  
   }  
 }  
  
  private static string GetConnectionString()  
  {  
   // To avoid storing the connection string in your code,  
   // you can retrieve it from a configuration file.  
   return "Data Source=(local);Database=AdventureWorks;" +  
      "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="15ce6-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="15ce6-112">See also</span></span>

- [<span data-ttu-id="15ce6-113">擷取資料庫結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="15ce6-113">Retrieving Database Schema Information</span></span>](retrieving-database-schema-information.md)
- <span data-ttu-id="15ce6-114">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="15ce6-114">[ADO.NET Overview](ado-net-overview.md)</span></span>

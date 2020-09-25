---
title: 從 DataView 建立 DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2d45cf41-d8ae-4409-af3e-a96a7e476d85
ms.openlocfilehash: 42843ec40f4f7271526e341dc53bdbc2ef11db38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198726"
---
# <a name="creating-a-datatable-from-a-dataview"></a><span data-ttu-id="89e79-102">從 DataView 建立 DataTable</span><span class="sxs-lookup"><span data-stu-id="89e79-102">Creating a DataTable from a DataView</span></span>

<span data-ttu-id="89e79-103">從資料來源擷取資料並將資料填入 <xref:System.Data.DataTable> 後，您可能想要排序、篩選，或限制所傳回的資料，而不想再次擷取該資料。</span><span class="sxs-lookup"><span data-stu-id="89e79-103">Once you have retrieved data from a data source, and have filled a <xref:System.Data.DataTable> with the data, you may want to sort, filter, or otherwise limit the returned data without retrieving it again.</span></span> <span data-ttu-id="89e79-104"><xref:System.Data.DataView> 類別使這成為可行。</span><span class="sxs-lookup"><span data-stu-id="89e79-104">The <xref:System.Data.DataView> class makes this possible.</span></span> <span data-ttu-id="89e79-105">此外，如果您需要從建立新的 <xref:System.Data.DataTable> <xref:System.Data.DataView> ，您可以使用方法，將 <xref:System.Data.DataView.ToTable%2A> 所有資料列和資料行或資料的子集複製到新的 <xref:System.Data.DataTable> 。</span><span class="sxs-lookup"><span data-stu-id="89e79-105">In addition, if you need to create a new <xref:System.Data.DataTable> from the <xref:System.Data.DataView>, you can use the <xref:System.Data.DataView.ToTable%2A> method to copy all the rows and columns, or a subset of the data into a new <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="89e79-106"><xref:System.Data.DataView.ToTable%2A> 方法提供多載，以進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="89e79-106">The <xref:System.Data.DataView.ToTable%2A> method provides overloads to:</span></span>  
  
- <span data-ttu-id="89e79-107">建立含有資料行的 <xref:System.Data.DataTable>，其中的資料行是 <xref:System.Data.DataView> 之資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="89e79-107">Create a <xref:System.Data.DataTable> containing columns that are a subset of the columns in the <xref:System.Data.DataView>.</span></span>  
  
- <span data-ttu-id="89e79-108">建立 <xref:System.Data.DataTable> 只包含不同資料列的 <xref:System.Data.DataView> ，類似至 transact-sql 中的 distinct 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="89e79-108">Create a <xref:System.Data.DataTable> that includes only distinct rows from the <xref:System.Data.DataView>, analogously to the DISTINCT keyword in Transact-SQL.</span></span>  
  
## <a name="example"></a><span data-ttu-id="89e79-109">範例</span><span class="sxs-lookup"><span data-stu-id="89e79-109">Example</span></span>  

 <span data-ttu-id="89e79-110">下列主控台應用程式範例會建立 <xref:System.Data.DataTable> ，其中包含**AdventureWorks**範例資料庫中**Person**資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="89e79-110">The following console application example creates a <xref:System.Data.DataTable> that contains data from the **Person.Contact** table in the **AdventureWorks** sample database.</span></span> <span data-ttu-id="89e79-111">接下來，此範例會根據，建立已排序和已篩選的 <xref:System.Data.DataView> <xref:System.Data.DataTable> 。</span><span class="sxs-lookup"><span data-stu-id="89e79-111">Next, the example creates a sorted and filtered <xref:System.Data.DataView> based on the <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="89e79-112">顯示 <xref:System.Data.DataTable> 和的內容之後 <xref:System.Data.DataView> ，此範例會藉 <xref:System.Data.DataTable> <xref:System.Data.DataView> 由呼叫方法來從建立新的，並 <xref:System.Data.DataView.ToTable%2A> 只選取可用資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="89e79-112">After displaying the contents of the <xref:System.Data.DataTable> and the <xref:System.Data.DataView>, the example creates a new <xref:System.Data.DataTable> from the <xref:System.Data.DataView> by calling the <xref:System.Data.DataView.ToTable%2A> method, selecting only a subset of the available columns.</span></span> <span data-ttu-id="89e79-113">最後，此範例會顯示新 <xref:System.Data.DataTable> 的內容。</span><span class="sxs-lookup"><span data-stu-id="89e79-113">Finally, the example displays the contents of the new <xref:System.Data.DataTable>.</span></span>  
  
```vb  
Private Sub DemonstrateDataView()  
    ' Retrieve a DataTable from the AdventureWorks sample database.  
    ' connectionString is assumed to be a valid connection string.  
    Dim adapter As New SqlDataAdapter( _  
       "SELECT FirstName, LastName, EmailAddress FROM Person.Contact WHERE FirstName LIKE 'Mich%'", connectionString)  
    Dim table As New DataTable  
  
    adapter.Fill(table)  
    Console.WriteLine("Original table name: " & table.TableName)  
    ' Print current table values.  
    PrintTableOrView(table, "Current Values in Table")  
  
    ' Now create a DataView based on the DataTable.  
    ' Sort and filter the data.  
    Dim view As DataView = table.DefaultView  
    view.Sort = "LastName, FirstName"  
    view.RowFilter = "LastName > 'M'"  
    PrintTableOrView(view, "Current Values in View")  
  
    ' Create a new DataTable based on the DataView,  
    ' requesting only two columns with distinct values  
    ' in the columns.  
    Dim newTable As DataTable = view.ToTable("UniqueLastNames", True, "FirstName", "LastName")  
    PrintTableOrView(newTable, "Table created from DataView")  
    Console.WriteLine("New table name: " & newTable.TableName)  
  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
    End Sub  
  
Private Sub PrintTableOrView(ByVal dv As DataView, ByVal label As String)  
    Dim sw As System.IO.StringWriter  
    Dim output As String  
    Dim table As DataTable = dv.Table  
  
    Console.WriteLine(label)  
  
    ' Loop through each row in the view.  
    For Each rowView As DataRowView In dv  
        sw = New System.IO.StringWriter  
  
        ' Loop through each column.  
        For Each col As DataColumn In table.Columns  
            ' Output the value of each column's data.  
            sw.Write(rowView(col.ColumnName).ToString() & ", ")  
        Next  
        output = sw.ToString  
        ' Trim off the trailing ", ", so the output looks correct.  
        If output.Length > 2 Then  
            output = output.Substring(0, output.Length - 2)  
        End If  
        ' Display the row in the console window.  
        Console.WriteLine(output)  
    Next  
    Console.WriteLine()  
End Sub  
  
Private Sub PrintTableOrView(ByVal table As DataTable, ByVal label As String)  
    Dim sw As System.IO.StringWriter  
    Dim output As String  
  
    Console.WriteLine(label)  
  
    ' Loop through each row in the table.  
    For Each row As DataRow In table.Rows  
        sw = New System.IO.StringWriter  
        ' Loop through each column.  
        For Each col As DataColumn In table.Columns  
            ' Output the value of each column's data.  
            sw.Write(row(col).ToString() & ", ")  
        Next  
        output = sw.ToString  
        ' Trim off the trailing ", ", so the output looks correct.  
        If output.Length > 2 Then  
            output = output.Substring(0, output.Length - 2)  
        End If  
        ' Display the row in the console window.  
        Console.WriteLine(output)  
    Next  
    Console.WriteLine()  
    End Sub  
End Module  
```  
  
```csharp  
private static void DemonstrateDataView()  
{  
// Retrieve a DataTable from the AdventureWorks sample database.  
// connectionString is assumed to be a valid connection string.  
SqlDataAdapter adapter = new SqlDataAdapter(  
    "SELECT FirstName, LastName, EmailAddress " +  
    "FROM Person.Contact WHERE FirstName LIKE 'Mich%'",
       GetConnectionString());  
DataTable table = new DataTable();  
  
adapter.Fill(table);  
Console.WriteLine("Original table name: " + table.TableName);  
// Print current table values.  
PrintTableOrView(table, "Current Values in Table");  
  
// Now create a DataView based on the DataTable.  
// Sort and filter the data.  
DataView view = table.DefaultView;  
view.Sort = "LastName, FirstName";  
view.RowFilter = "LastName > 'M'";  
PrintTableOrView(view, "Current Values in View");  
  
// Create a new DataTable based on the DataView,  
// requesting only two columns with distinct values  
// in the columns.  
DataTable newTable = view.ToTable("UniqueLastNames",  
     true, "FirstName", "LastName");  
PrintTableOrView(newTable, "Table created from DataView");  
Console.WriteLine("New table name: " + newTable.TableName);  
  
Console.WriteLine("Press any key to continue.");  
Console.ReadKey();  
}  
  
private static void PrintTableOrView(DataView dv, string label)  
{  
System.IO.StringWriter sw;  
string output;  
DataTable table = dv.Table;  
  
Console.WriteLine(label);  
  
// Loop through each row in the view.  
foreach (DataRowView rowView in dv)  
{  
    sw = new System.IO.StringWriter();  
  
    // Loop through each column.  
    foreach (DataColumn col in table.Columns)  
    {  
        // Output the value of each column's data.  
        sw.Write(rowView[col.ColumnName].ToString() + ", ");  
    }  
    output = sw.ToString();  
    // Trim off the trailing ", ", so the output looks correct.  
    if (output.Length > 2)  
    {  
        output = output.Substring(0, output.Length - 2);  
    }  
    // Display the row in the console window.  
    Console.WriteLine(output);  
}  
Console.WriteLine();  
}  
  
private static void PrintTableOrView(DataTable table, string label)  
{  
System.IO.StringWriter sw;  
string output;  
  
Console.WriteLine(label);  
  
// Loop through each row in the table.  
foreach (DataRow row in table.Rows)  
{  
    sw = new System.IO.StringWriter();  
    // Loop through each column.  
    foreach (DataColumn col in table.Columns)  
    {  
        // Output the value of each column's data.  
        sw.Write(row[col].ToString() + ", ");  
    }  
    output = sw.ToString();  
    // Trim off the trailing ", ", so the output looks correct.  
    if (output.Length > 2)  
    {  
        output = output.Substring(0, output.Length - 2);  
    }  
    // Display the row in the console window.  
    Console.WriteLine(output);  
} //  
Console.WriteLine();  
}  
```  
  
 <span data-ttu-id="89e79-114">}</span><span class="sxs-lookup"><span data-stu-id="89e79-114">}</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="89e79-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="89e79-115">See also</span></span>

- <xref:System.Data.DataView.ToTable%2A>
- [<span data-ttu-id="89e79-116">DataView</span><span class="sxs-lookup"><span data-stu-id="89e79-116">DataViews</span></span>](dataviews.md)
- <span data-ttu-id="89e79-117">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="89e79-117">[ADO.NET Overview](../ado-net-overview.md)</span></span>

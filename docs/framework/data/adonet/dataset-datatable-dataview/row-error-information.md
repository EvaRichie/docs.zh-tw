---
title: 資料列錯誤資訊
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8b1f9070-d032-48c7-b030-bd8fbb2ca59a
ms.openlocfilehash: 8673b7fbc2e4238f7047698376c53af991de9f1b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91181163"
---
# <a name="row-error-information"></a>資料列錯誤資訊

編輯 <xref:System.Data.DataTable> 中的值時，若要避免必須在每次發生資料列錯誤時都回應，則可以將錯誤資訊加入至資料列中，供日後使用。 針對這項用途，<xref:System.Data.DataRow> 物件會為每個資料列提供 <xref:System.Data.DataRow.RowError%2A> 屬性。 將資料加入至**datarow**的**RowError**屬性時，會將 <xref:System.Data.DataRow.HasErrors%2A> **DataRow**的屬性設定為**true**。 如果 **datarow** 是 **DataTable**的一部分，且 **HasErrors** 為 **true**，則 **DataTable. HasErrors** 屬性也是 **true**。 這也適用于**DataTable**所屬的**資料集**。 測試錯誤時，您可以檢查 **HasErrors** 屬性，以判斷是否已將錯誤資訊加入至任何資料列。 如果 **HasErrors** 為 **true**，您可以使用 <xref:System.Data.DataTable.GetErrors%2A> **DataTable** 的方法來傳回和檢查具有錯誤的資料列，如下列範例所示。  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
workTable.Columns.Add("CustID", Type.GetType("System.Int32"))  
workTable.Columns.Add("Total", Type.GetType("System.Double"))  
  
AddHandler workTable.RowChanged, New DataRowChangeEventHandler(AddressOf OnRowChanged)  
  
Dim i  As Int32  
  
For i  = 0 To 10  
  workTable.Rows.Add(New Object() {i , i *100})  
Next  
  
If workTable.HasErrors Then  
  Console.WriteLine("Errors in Table " & workTable.TableName)  
  
  Dim myRow As DataRow  
  
  For Each myRow In workTable.GetErrors()  
    Console.WriteLine("CustID = " & myRow("CustID").ToString())  
    Console.WriteLine(" Error = " & myRow.RowError & vbCrLf)  
  Next  
End If  
  
Private Shared Sub OnRowChanged( _  
    sender As Object, args As DataRowChangeEventArgs)  
  ' Check for zero values.  
  If CDbl(args.Row("Total")) = 0 Then args.Row.RowError = _  
      "Total cannot be 0."  
End Sub  
```  
  
```csharp  
DataTable  workTable = new DataTable("Customers");  
workTable.Columns.Add("CustID", typeof(Int32));  
workTable.Columns.Add("Total", typeof(Double));  
  
workTable.RowChanged += new DataRowChangeEventHandler(OnRowChanged);  
  
for (int i = 0; i < 10; i++)  
  workTable.Rows.Add(new Object[] {i, i*100});  
  
if (workTable.HasErrors)  
{  
  Console.WriteLine("Errors in Table " + workTable.TableName);  
  
  foreach (DataRow myRow in workTable.GetErrors())  
  {  
    Console.WriteLine("CustID = " + myRow["CustID"]);  
    Console.WriteLine(" Error = " + myRow.RowError + "\n");  
  }  
}  
  
protected static void OnRowChanged(  
    Object sender, DataRowChangeEventArgs args)  
{  
  // Check for zero values.  
  if (args.Row["Total"].Equals(0D))  
    args.Row.RowError = "Total cannot be 0.";  
}  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataRow>
- <xref:System.Data.DataTable>
- [在 DataTable 中操作資料](manipulating-data-in-a-datatable.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)

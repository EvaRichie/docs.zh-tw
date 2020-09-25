---
title: AcceptChanges 和 RejectChanges
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e2d1a6fe-31f9-4b83-9728-06c406a3394e
ms.openlocfilehash: e29d2404d6d593b9a5b905206af3cdd3bc1a3e51
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177588"
---
# <a name="acceptchanges-and-rejectchanges"></a>AcceptChanges 和 RejectChanges

在確認對中的資料所做之變更的精確度之後， <xref:System.Data.DataTable> 您可以使用、或的方法接受變更， <xref:System.Data.DataRow.AcceptChanges%2A> <xref:System.Data.DataRow> <xref:System.Data.DataTable> <xref:System.Data.DataSet> 這會將 **目前** 的資料列值設定為 **原始** 值，並將 **RowState** 屬性設定為 **未**變更。 接受或拒絕變更會清除任何 **RowError** 資訊，並將 **HasErrors** 屬性設定為 **false**。 接受或拒絕變更也會影響資料來源中的資料更新。 如需詳細資訊，請參閱 [使用 Dataadapter 更新資料來源](../updating-data-sources-with-dataadapters.md)。  
  
 如果**DataTable**上有 foreign key 條件約束，則使用**AcceptChanges**和**RejectChanges**來接受或拒絕的變更會根據**ForeignKeyConstraint**傳播到**DataRow**的子資料列。 如需詳細資訊，請參閱 [DataTable 條件約束](datatable-constraints.md)。  
  
 下列範例會檢查發生錯誤的資料列、適當地解決錯誤，並且在無法解決錯誤時拒絕資料列。 請注意，針對已解決的錯誤， **RowError** 值會重設為空字串，而導致 **HasErrors** 屬性設定為 **false**。 當所有具有錯誤的資料列都已解決或遭到拒絕時，會呼叫 **AcceptChanges** 以接受整個 **DataTable**的所有變更。  
  
```vb  
If workTable.HasErrors Then  
  Dim errRow As DataRow  
  
  For Each errRow in workTable.GetErrors()  
  
    If errRow.RowError = "Total cannot exceed 1000." Then  
      errRow("Total") = 1000  
      errRow.RowError = ""    ' Clear the error.  
    Else  
      errRow.RejectChanges()  
    End If  
  Next  
End If  
  
workTable.AcceptChanges()  
```  
  
```csharp  
if (workTable.HasErrors)  
{  
  
  foreach (DataRow errRow in workTable.GetErrors())  
  {  
    if (errRow.RowError == "Total cannot exceed 1000.")  
    {  
      errRow["Total"] = 1000;  
      errRow.RowError = "";    // Clear the error.  
    }  
    else  
      errRow.RejectChanges();  
  }  
}  
  
workTable.AcceptChanges();  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- [在 DataTable 中操作資料](manipulating-data-in-a-datatable.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)

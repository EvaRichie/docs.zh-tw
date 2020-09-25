---
title: 建立資料集
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 57629d8f-393e-4677-8b83-29ffde27f5fc
ms.openlocfilehash: cbf652cc3742cb880fe060743dcc2615e6283ca7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202353"
---
# <a name="creating-a-dataset"></a>建立資料集

您可呼叫 <xref:System.Data.DataSet> 建構函式 (Constructor) 來建立 <xref:System.Data.DataSet> 的執行個體 (Instance)。 選擇性地指定名稱引數。 如果您不指定 <xref:System.Data.DataSet> 的名稱，則名稱會設定為 "NewDataSet"。  
  
 您也可以根據現有的 <xref:System.Data.DataSet> 建立新的 <xref:System.Data.DataSet>。 新的 <xref:System.Data.DataSet> 可以是：現有 <xref:System.Data.DataSet> 的完整複本；<xref:System.Data.DataSet> 的複製，該項目複製關聯式架構或結構描述，但是不包含任何來自現有 <xref:System.Data.DataSet> 的資料；或 <xref:System.Data.DataSet> 的子集，其中只包含來自現有的 <xref:System.Data.DataSet> 且使用 <xref:System.Data.DataSet.GetChanges%2A> 方法修改過的資料列。 如需詳細資訊，請參閱 [複製資料集內容](copying-dataset-contents.md)。  
  
 下列程式碼範例示範如何建構 <xref:System.Data.DataSet> 的執行個體。  
  
```vb  
Dim customerOrders As DataSet = New DataSet("CustomerOrders")  
```  
  
```csharp  
DataSet customerOrders = new DataSet("CustomerOrders");  
```  
  
## <a name="see-also"></a>另請參閱

- [從 DataAdapter 填入資料集](../populating-a-dataset-from-a-dataadapter.md)
- [DataSet、DataTable 和 DataView](index.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)

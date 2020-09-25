---
title: 比較 DataRow (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8fe0eadf-297b-487c-8d4b-7816753c2883
ms.openlocfilehash: 8cce52734c83e42312d71806d4151ef21e4df0ba
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203796"
---
# <a name="comparing-datarows-linq-to-dataset"></a>比較 DataRow (LINQ to DataSet)

 (LINQ) 的語言整合式查詢定義了不同的集合運算子，以比較來源元素來查看它們是否相等。 LINQ 提供下列 set 運算子：  
  
- <xref:System.Linq.Enumerable.Distinct%2A>  
  
- <xref:System.Linq.Enumerable.Union%2A>  
  
- <xref:System.Linq.Enumerable.Intersect%2A>  
  
- <xref:System.Linq.Enumerable.Except%2A>  
  
 這些運算子會針對每個項目集合呼叫 <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> 和 <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> 方法，藉以比較來源項目。 在 <xref:System.Data.DataRow> 的情況中，這些運算子會執行參考比較，但是這通常不是表格式資料之設定作業的理想行為。 若為設定作業，您通常會想要判斷項目值是否相等，而非項目參考。 因此， <xref:System.Data.DataRowComparer> 類別已新增至 LINQ to DataSet。 這個類別可用來比較資料列值。  
  
 <xref:System.Data.DataRowComparer> 類別包含 <xref:System.Data.DataRow> 的值比較實作 (Implementation)，所以這個類別可用於 <xref:System.Linq.Enumerable.Distinct%2A> 等設定作業。 您無法直接具現化 (Instantiated) 這個類別，而必須使用 <xref:System.Data.DataRowComparer.Default%2A> 屬性來傳回 <xref:System.Data.DataRowComparer%601> 的執行個體 (Instance)。 然後，系統會呼叫 <xref:System.Data.DataRowComparer%601.Equals%2A> 方法並將要比較的兩個 <xref:System.Data.DataRow> 物件當做輸入參數傳入。 如果這兩個 <xref:System.Data.DataRowComparer%601.Equals%2A> 物件中的已排序資料行值組相等，`true` 方法就會傳回 <xref:System.Data.DataRow>，否則它會傳回 `false`。  
  
## <a name="example"></a>範例  

 這則範例會使用 `Intersect` 來傳回在這兩份資料表中都出現的連絡人。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#intersect2)]
 [!code-vb[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#intersect2)]  
  
### <a name="example"></a>範例  

 下列範例會比較兩個資料列並取得其雜湊程式碼。  
  
 [!code-vb[DP LINQ to DataSet Examples#CompareDifferentRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#comparedifferentrows)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Data.DataRowComparer>
- [將資料載入至資料集](loading-data-into-a-dataset.md)
- [LINQ to DataSet 範例](linq-to-dataset-examples.md)

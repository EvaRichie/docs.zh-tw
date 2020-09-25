---
title: 作法：使用有參數的預存程序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b935fd84-cb9c-4205-8c48-658d5db2ec93
ms.openlocfilehash: a54e2ee553629179022b68658d44cbcb02ab590f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91184959"
---
# <a name="how-to-use-stored-procedures-that-take-parameters"></a>作法：使用有參數的預存程序

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會將輸出參數對應至參考參數，而且會針對實值型別 (Value Type)，將參數宣告為可為 Null。  
  
 如需如何在傳回資料列集的查詢中使用輸入參數的範例，請參閱 [如何：](how-to-return-rowsets.md)傳回資料列集。  
  
## <a name="example"></a>範例  

 下列範例取用單一輸入參數 (客戶 ID)，並傳回輸出參數 (該客戶的總銷售量)。  
  
```sql
CREATE PROCEDURE [dbo].[CustOrderTotal]
@CustomerID nchar(5),  
@TotalSales money OUTPUT  
AS  
SELECT @TotalSales = SUM(OD.UNITPRICE*(1-OD.DISCOUNT) * OD.QUANTITY)  
FROM ORDERS O, "ORDER DETAILS" OD  
where O.CUSTOMERID = @CustomerID AND O.ORDERID = OD.ORDERID  
```  
  
 [!code-csharp[DLinqSprox#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#2)]
 [!code-vb[DLinqSprox#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#2)]  
  
## <a name="example"></a>範例  

 您可如下呼叫這個預存程序 (Stored Procedure)：  
  
 [!code-csharp[DLinqSprox#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#3)]
 [!code-vb[DLinqSprox#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>另請參閱

- [預存程序](stored-procedures.md)
- [下載範例資料庫](downloading-sample-databases.md)
- [可為 null 的實數值型別 (c # ) ](../../../../../csharp/language-reference/builtin-types/nullable-value-types.md)
- [可為 Null 的實值類型 (Visual Basic)](../../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)

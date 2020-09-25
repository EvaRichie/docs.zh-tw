---
title: 從方法傳回查詢
description: 如何傳回查詢。
ms.date: 11/30/2016
ms.assetid: db220f79-c35b-41f2-886c-cd068672d42d
ms.openlocfilehash: 646e771d637aa242231e3fe216d4a856bb156649
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203328"
---
# <a name="how-to-return-a-query-from-a-method-c-programming-guide"></a>如何從方法傳回查詢 (c # 程式設計手冊) 

這個範例示範如何以傳回值和 `out` 參數形式從方法中傳回查詢。  
  
 查詢物件是可編寫的，這表示您可以從方法傳回查詢。 代表查詢的物件不會儲存所產生的集合，而是在必要時產生結果的步驟。 從方法傳回查詢物件的優點，在於可以進一步編寫或修改它們。 因此，傳回查詢的方法的任何傳回值或 `out` 參數也必須具有該類型。 如果方法將查詢具體化到具體 <xref:System.Collections.Generic.List%601> 或 <xref:System.Array> 類型，則會視為傳回查詢結果，而不是查詢本身。 從方法傳回的查詢變數仍然可以進行編寫或修改。  
  
## <a name="example"></a>範例  

 在下列範例中，第一個方法會以傳回值形式傳回查詢，第二個方法會以 `out` 參數形式傳回查詢。 請注意，在這兩種情況下，它是傳回的查詢，而不是查詢結果。  
  
 [!code-csharp[csProgGuideLINQ#80](~/samples/snippets/csharp/concepts/linq/how-to-return-a-query-from-a-method_1.cs)]  

## <a name="see-also"></a>另請參閱

- [Language Integrated Query (LINQ)](index.md)

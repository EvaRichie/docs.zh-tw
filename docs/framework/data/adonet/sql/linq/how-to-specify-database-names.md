---
title: 作法：指定資料庫名稱
ms.date: 03/30/2017
ms.assetid: b80f0fd2-7f75-45fe-9e12-496f80f183df
ms.openlocfilehash: 82cb3f8f31af433b0299b4fec742b548d61921e4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197153"
---
# <a name="how-to-specify-database-names"></a>作法：指定資料庫名稱

在 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 屬性 (Attribute) 上使用 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 屬性 (Property)，可在連接未提供名稱時指定資料庫名稱。  
  
 如需程式碼範例，請參閱 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>。  
  
### <a name="to-specify-the-name-of-the-database"></a>若要指定資料庫的名稱  
  
1. 將 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 屬性 (Attribute) 加入至資料庫的類別宣告。  
  
2. 將 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 屬性 (Property) 加入至 <xref:System.Data.Linq.Mapping.DatabaseAttribute> 屬性 (Attribute)。  
  
3. 將 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 屬性 (Property) 值設定為想要指定的名稱。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)
- [作法：使用程式碼編輯器自訂實體類別](how-to-customize-entity-classes-by-using-the-code-editor.md)

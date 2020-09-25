---
title: LINQ 和泛型類型 (C#)
description: '深入瞭解 c # 中支援查詢的泛型型別基本概念。  LINQ 查詢是以泛型型別為基礎。'
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], generic types
- generic types [LINQ]
- generics [LINQ]
ms.assetid: 660e3799-25ca-462c-8c4a-8bce04fbb031
ms.openlocfilehash: a71957eabea788fb06195df1ef026390947f013d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91170463"
---
# <a name="linq-and-generic-types-c"></a>LINQ 和泛型類型 (C#)

LINQ 查詢是以 .NET Framework 2.0 版中引進的泛型型別為基礎。 您不需要深入了解泛型，就可以開始撰寫查詢。 不過，您可能需要了解兩個基本概念：  
  
1. 建立泛型集合類別 (例如 <xref:System.Collections.Generic.List%601>) 的執行個體時，請將 "T" 取代為清單中會包含之物件的類型。 例如，字串的清單是以 `List<string>` 表示，而 `Customer` 物件的清單則是以 `List<Customer>` 表示。 泛型清單是強型別，而且優點多於以 <xref:System.Object> 形式儲存項目的集合。 如果您嘗試將 `Customer` 新增至 `List<string>`，則會在編譯時收到錯誤。 由於不需要執行執行階段類型轉換，因此您可以輕鬆使用泛型集合。  
  
2. <xref:System.Collections.Generic.IEnumerable%601> 介面藉由使用 `foreach` 陳述式來列舉泛型集合類別。 泛型集合類別支援 <xref:System.Collections.Generic.IEnumerable%601>，就像 <xref:System.Collections.ArrayList> 這類非泛型集合類別支援 <xref:System.Collections.IEnumerable>。  
  
 如需泛型的詳細資訊，請參閱[泛型](../../generics/index.md)。  
  
## <a name="ienumerablet-variables-in-linq-queries"></a>LINQ 查詢中的 IEnumerable<T\> 變數  

 LINQ 查詢變數的類型為 <xref:System.Collections.Generic.IEnumerable%601> 或衍生類型，例如 <xref:System.Linq.IQueryable%601> 。 當您看到類型為 `IEnumerable<Customer>` 的查詢變數時，只表示查詢在執行時會產生由零個以上的 `Customer` 物件所組成的序列。  
  
 [!code-csharp[csLINQGettingStarted#34](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#34)]  
  
 如需詳細資訊，請參閱 [LINQ 查詢作業中的類型關聯性](./type-relationships-in-linq-query-operations.md)。  
  
## <a name="letting-the-compiler-handle-generic-type-declarations"></a>讓編譯器處理泛型型別宣告  

 如果您想要，也可以使用 [var](../../../language-reference/keywords/var.md) 關鍵字避免使用泛型語法。 `var` 關鍵字會指示編譯器查看 `from` 子句中指定的資料來源，來推斷查詢變數的類型。 下列範例會產生與上一個範例相同的已編譯程式碼：  
  
 [!code-csharp[csLINQGettingStarted#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#35)]  
  
 當變數的類型很明顯，或不需要明確指定巢狀泛型型別 (例如群組查詢所產生的巢狀泛型型別) 時，`var` 關鍵字會很有用。 一般而言，如果使用 `var`，建議您考慮到它會讓其他人更難看懂您的程式碼。 如需詳細資訊，請參閱[隱含型別區域變數](../../classes-and-structs/implicitly-typed-local-variables.md)。  
  
## <a name="see-also"></a>另請參閱

- [泛型](../../generics/index.md)

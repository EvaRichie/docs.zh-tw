---
title: '如何在查詢中使用 lambda 運算式-c # 程式設計手冊'
description: 瞭解如何在查詢中使用 lambda 運算式。 請參閱程式碼範例，並查看其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], in LINQ
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
ms.openlocfilehash: 501e67011707e2d165a3b9c1ff9f206db7f55448
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381628"
---
# <a name="how-to-use-lambda-expressions-in-a-query-c-programming-guide"></a>如何在查詢中使用 lambda 運算式（c # 程式設計手冊）
您不會在查詢語法中直接使用 Lambda 運算式，而是在方法呼叫中使用它們，因此查詢運算式可以包含方法呼叫。 事實上，某些查詢作業只能以方法語法來表示。 如需查詢語法與方法語法之間差異的詳細資訊，請參閱 [LINQ 中的查詢語法及方法語法](../concepts/linq/query-syntax-and-method-syntax-in-linq.md)。  
  
## <a name="example"></a>範例  
 下列範例示範如何透過 <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType> 標準查詢運算子，在以方法為基礎的查詢中使用 Lambda 運算式。 請注意，此範例中的 <xref:System.Linq.Enumerable.Where%2A> 方法具有委派類型 <xref:System.Func%602> 的輸入參數，而且該委派會接受整數作為輸入並傳回布林值。 Lambda 運算式可轉換成該委派。 如果這是使用 <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType> 方法的 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 查詢，參數類型就會是 `Expression<Func<int,bool>>`，但 Lambda 運算式看起來會完全相同。 如需運算式類型的詳細資訊，請參閱 <xref:System.Linq.Expressions.Expression?displayProperty=nameWithType>。  
  
 [!code-csharp[csProgGuideLINQ#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#1)]  
  
## <a name="example"></a>範例  
 下列範例示範如何在查詢運算式的方法呼叫中使用 Lambda 運算式。 因為無法使用查詢語法來叫用 <xref:System.Linq.Enumerable.Sum%2A> 標準查詢運算子，所以需要此 Lambda。  
  
 此查詢會先根據學生的年級 (已定義於 `GradeLevel` 列舉) 來進行分組。 接著會針對每一組加總計算每個學生的總分數。 這需要兩個 `Sum` 運算。 內部的 `Sum` 會計算每個學生的總分數，而外部的 `Sum` 會不斷執行，以加總該群組中所有學生的總分數。  
  
 [!code-csharp[csProgGuideLINQ#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#2)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 若要執行此程式碼，請將方法複製並貼到 `StudentClass` [查詢物件集合](../../linq/query-a-collection-of-objects.md)中所提供的，並從方法呼叫它 `Main` 。
  
## <a name="see-also"></a>另請參閱

- [Lambda 運算式](./lambda-expressions.md)
- [運算式樹狀架構 (C#)](../concepts/expression-trees/index.md)

---
title: '如何使用運算式樹狀架構建立動態查詢 (c # ) '
description: 瞭解如何使用運算式樹狀架構建立動態 LINQ 查詢。 當查詢的詳細資訊在編譯時間未知時，這些查詢會很有用。
ms.date: 07/20/2015
ms.assetid: 52cd44dd-a3ec-441e-b93a-4eca388119c7
ms.openlocfilehash: 284e7fa4534d1648c8e2bd6f4feaa62796ca60d8
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202587"
---
# <a name="how-to-use-expression-trees-to-build-dynamic-queries-c"></a>如何使用運算式樹狀架構建立動態查詢 (c # ) 

在 LINQ 中，您可以使用運算式樹狀架構，來代表以實作 <xref:System.Linq.IQueryable%601> 的資料來源為目標的結構化查詢。 例如，LINQ 提供者會實作 <xref:System.Linq.IQueryable%601> 介面，來查詢關聯式資料存放區。 C# 編譯器會將以這類資料來源為目標的查詢編譯為程式碼，以在執行階段建立運算式樹狀架構。 查詢提供者可接著周遊運算式樹狀架構資料結構，並將它轉譯成適用於資料來源的查詢語言。  
  
 您也可以在 LINQ 中使用運算式樹狀架構，來代表指派給 <xref:System.Linq.Expressions.Expression%601> 類型變數的 Lambda 運算式。  
  
 本主題描述如何使用運算式樹狀架構建立動態 LINQ 查詢。 如果在編譯時不知道查詢的詳細資料，動態查詢會很有用。 例如，應用程式可能會提供一個使用者介面，讓終端使用者指定一或多個述詞來篩選資料。 若要使用 LINQ 進行查詢，這類應用程式必須使用運算式樹狀架構在執行階段建立 LINQ 查詢。  
  
## <a name="example"></a>範例  

 下列範例示範如何使用運算式樹狀架構，對 `IQueryable` 資料來源建構並接著執行查詢。 程式碼會建立運算式樹狀架構來代表下列查詢：  
  
 ```csharp
 companies.Where(company => (company.ToLower() == "coho winery" || company.Length > 16))
          .OrderBy(company => company)
 ```
  
 <xref:System.Linq.Expressions> 命名空間中的 Factory 方法可用於建立運算式樹狀架構，來代表組成整體查詢的運算式。 代表標準查詢運算子方法呼叫的運算式會參考這些方法的 <xref:System.Linq.Queryable> 實作。 最後一個運算式樹狀結構會傳遞至 `IQueryable` 資料來源之提供者的 <xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29> 實作，以建立類型為 `IQueryable` 的可執行查詢。 藉由列舉查詢變數可取得結果。  
  
```csharp  
// Add a using directive for System.Linq.Expressions.  
  
string[] companies = { "Consolidated Messenger", "Alpine Ski House", "Southridge Video", "City Power & Light",  
                   "Coho Winery", "Wide World Importers", "Graphic Design Institute", "Adventure Works",  
                   "Humongous Insurance", "Woodgrove Bank", "Margie's Travel", "Northwind Traders",  
                   "Blue Yonder Airlines", "Trey Research", "The Phone Company",  
                   "Wingtip Toys", "Lucerne Publishing", "Fourth Coffee" };  
  
// The IQueryable data to query.  
IQueryable<String> queryableData = companies.AsQueryable<string>();  
  
// Compose the expression tree that represents the parameter to the predicate.  
ParameterExpression pe = Expression.Parameter(typeof(string), "company");  
  
// ***** Where(company => (company.ToLower() == "coho winery" || company.Length > 16)) *****  
// Create an expression tree that represents the expression 'company.ToLower() == "coho winery"'.  
Expression left = Expression.Call(pe, typeof(string).GetMethod("ToLower", System.Type.EmptyTypes));  
Expression right = Expression.Constant("coho winery");  
Expression e1 = Expression.Equal(left, right);  
  
// Create an expression tree that represents the expression 'company.Length > 16'.  
left = Expression.Property(pe, typeof(string).GetProperty("Length"));  
right = Expression.Constant(16, typeof(int));  
Expression e2 = Expression.GreaterThan(left, right);  
  
// Combine the expression trees to create an expression tree that represents the  
// expression '(company.ToLower() == "coho winery" || company.Length > 16)'.  
Expression predicateBody = Expression.OrElse(e1, e2);  
  
// Create an expression tree that represents the expression  
// 'queryableData.Where(company => (company.ToLower() == "coho winery" || company.Length > 16))'  
MethodCallExpression whereCallExpression = Expression.Call(  
    typeof(Queryable),  
    "Where",  
    new Type[] { queryableData.ElementType },  
    queryableData.Expression,  
    Expression.Lambda<Func<string, bool>>(predicateBody, new ParameterExpression[] { pe }));  
// ***** End Where *****  
  
// ***** OrderBy(company => company) *****  
// Create an expression tree that represents the expression  
// 'whereCallExpression.OrderBy(company => company)'  
MethodCallExpression orderByCallExpression = Expression.Call(  
    typeof(Queryable),  
    "OrderBy",  
    new Type[] { queryableData.ElementType, queryableData.ElementType },  
    whereCallExpression,  
    Expression.Lambda<Func<string, string>>(pe, new ParameterExpression[] { pe }));  
// ***** End OrderBy *****  
  
// Create an executable query from the expression tree.  
IQueryable<string> results = queryableData.Provider.CreateQuery<string>(orderByCallExpression);  
  
// Enumerate the results.  
foreach (string company in results)  
    Console.WriteLine(company);  
  
/*  This code produces the following output:  
  
    Blue Yonder Airlines  
    City Power & Light  
    Coho Winery  
    Consolidated Messenger  
    Graphic Design Institute  
    Humongous Insurance  
    Lucerne Publishing  
    Northwind Traders  
    The Phone Company  
    Wide World Importers  
*/  
```  
  
 此程式碼在傳遞至 `Queryable.Where` 方法的述詞中，使用固定數目的運算式。 不過，您可以撰寫一個應用程式，以根據使用者輸入合併可變數目的述詞運算式。 您也可以根據使用者輸入，更改查詢中所呼叫的標準查詢運算子。  
  
## <a name="compiling-the-code"></a>編譯程式碼  
  
- 加入 System.Linq.Expressions 命名空間。  
  
## <a name="see-also"></a>另請參閱

- [運算式樹狀架構 (C#)](./index.md)
- [如何執行運算式樹狀架構 (c # ) ](./how-to-execute-expression-trees.md)
- [在執行階段動態指定述詞篩選](../../../linq/dynamically-specify-predicate-filters-at-runtime.md)

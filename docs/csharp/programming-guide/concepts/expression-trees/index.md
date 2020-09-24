---
title: 運算式樹狀架構 (C#)
description: 深入瞭解運算式樹狀架構。 請參閱如何編譯和執行這些資料結構所代表的程式碼，其中每個節點都是運算式。
ms.date: 07/20/2015
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
ms.openlocfilehash: 04b5486b6d3c54f0dfd3914eacbda5cffe15890a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167635"
---
# <a name="expression-trees-c"></a>運算式樹狀架構 (C#)

運算式樹狀架構代表類似樹狀目錄之資料結構中的程式碼，其中，每個節點都是一個運算式，例如，方法呼叫或二進位運算 (如 `x < y`)。  
  
 您可以編譯和執行運算式樹狀架構所代表的程式碼。 這會啟用動態修改可執行程式碼、在各種資料庫中執行 LINQ 查詢，以及建立動態查詢。 如需 LINQ 中運算式樹狀架構的詳細資訊，請參閱 [如何使用運算式樹狀架構建立動態查詢 (c # ) ](./how-to-use-expression-trees-to-build-dynamic-queries.md)。
  
 動態語言執行時間也會使用運算式樹狀架構 (DLR) 來提供動態語言與 .NET 之間的互通性，並讓編譯器寫入器發出運算式樹狀架構，而不是 Microsoft 中繼語言 (MSIL) 。 如需 DLR 的詳細資訊，請參閱 [Dynamic Language Runtime 概觀](../../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)。  
  
 您可以根據匿名 Lambda 運算式讓 C# 或 Visual Basic 編譯器建立運算式樹狀架構，也可以使用 <xref:System.Linq.Expressions> 命名空間以手動建立運算式樹狀架構。  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>從 Lambda 運算式建立運算式樹狀架構  

 將 Lambda 運算式指派給類型為 <xref:System.Linq.Expressions.Expression%601> 的變數時，編譯器會發出程式碼，以建置代表 Lambda 運算式的運算式樹狀架構。  
  
 C# 編譯器只能從運算式 Lambda (或單行 Lambda) 產生運算式樹狀架構。 它無法剖析陳述式 Lambda (或多行 Lambda)。 如需 C# 中之 Lambda 運算式的詳細資訊，請參閱 [Lambda 運算式](../../../language-reference/operators/lambda-expressions.md)。  
  
 下列程式碼範例示範如何讓 C# 編譯器建立代表 Lambda 運算式 `num => num < 5` 的運算式樹狀架構。  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>使用 API 建立運算式樹狀架構  

 若要使用 API 建立運算式樹狀架構，請使用 <xref:System.Linq.Expressions.Expression> 類別。 這個類別包含可建立之特定類型運算式樹狀架構節點的靜態 factory 方法，例如，<xref:System.Linq.Expressions.ParameterExpression> (代表變數或參數) 或 <xref:System.Linq.Expressions.MethodCallExpression> (代表方法呼叫)。 <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression> 和其他運算式特定類型也定義在 <xref:System.Linq.Expressions> 命名空間中。 這些類型衍生自抽象類型 <xref:System.Linq.Expressions.Expression>。  
  
 下列程式碼範例示範如何使用 API 建立代表 Lambda 運算式 `num => num < 5` 的運算式樹狀架構。  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 在.NET Framework 4 或更新版中，運算式樹狀架構 API 也可用於指派及控制流程運算式，例如迴圈、條件式區塊及 `try-catch` 區塊。 使用 API 建立的運算式樹狀架構，可以比使用 C# 編譯器從 Lambda 運算式建立的運算式樹狀架構更加複雜。 下列範例示範如何建立可計算數字階乘的運算式樹狀架構。  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

如需詳細資訊，請參閱[在 Visual Studio 2010 中使用運算式樹狀架構產生動態方法 (英文)](https://devblogs.microsoft.com/csharpfaq/generating-dynamic-methods-with-expression-trees-in-visual-studio-2010/)，這也適用於更新版本的 Visual Studio。
  
## <a name="parsing-expression-trees"></a>剖析運算式樹狀架構  

 下列程式碼範例示範如何將代表 Lambda 運算式 `num => num < 5` 的運算式樹狀架構分解成各部組件。  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>運算式樹狀架構的不變性  

 運算式樹狀架構應該是不變的。 這表示，如果您要修改運算式樹狀架構，則必須複製現有運算式樹狀架構，並取代其中的節點，以建構新的運算式樹狀架構。 您可以使用運算式樹狀架構訪問項來周遊現有運算式樹狀架構。 如需詳細資訊，請參閱 [如何修改運算式樹狀架構 (c # ) ](./how-to-modify-expression-trees.md)。
  
## <a name="compiling-expression-trees"></a>編譯運算式樹狀架構  

 <xref:System.Linq.Expressions.Expression%601> 類型提供 <xref:System.Linq.Expressions.Expression%601.Compile%2A> 方法，以將運算式樹狀架構所代表的程式碼編譯為可執行委派。  
  
 下列程式碼範例示範如何編譯運算式樹狀架構，並執行產生的程式碼。  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 如需詳細資訊，請參閱 [如何執行運算式樹狀架構 (c # ) ](./how-to-execute-expression-trees.md)。
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq.Expressions>
- [如何執行運算式樹狀架構 (c # ) ](./how-to-execute-expression-trees.md)
- [如何修改運算式樹狀架構 (c # ) ](./how-to-modify-expression-trees.md)
- [Lambda 運算式](../../../language-reference/operators/lambda-expressions.md)
- [動態語言執行時間總覽](../../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)
- [程式設計概念 (C#)](../index.md)

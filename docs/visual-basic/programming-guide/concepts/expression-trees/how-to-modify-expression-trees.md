---
title: 如何：修改運算式樹狀架構
ms.date: 07/20/2015
ms.assetid: d1309fff-28bd-4d8e-a2cf-75725999e8f2
ms.openlocfilehash: 1f052120a2e7e12f5a985adce3ae193afec0e9af
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410988"
---
# <a name="how-to-modify-expression-trees-visual-basic"></a>如何：修改運算式樹狀結構 (Visual Basic)

本主題示範如何修改運算式樹狀架構。 運算式樹狀架構為不可變，這表示無法直接對其進行修改。 若要變更運算式樹狀架構，您必須建立現有運算式樹狀架構的複本，並且在建立複本時進行必要的變更。 您可以使用 <xref:System.Linq.Expressions.ExpressionVisitor> 類別周遊現有的運算式樹狀架構，並複製每個瀏覽的節點。

## <a name="to-modify-an-expression-tree"></a>修改運算式樹狀架構

1. 建立新的**主控台應用程式**專案。

2. 將 `Imports` 語句加入至命名空間的檔案 `System.Linq.Expressions` 。

3. 將 `AndAlsoModifier` 類別新增至專案。

    ```vb
    Public Class AndAlsoModifier
        Inherits ExpressionVisitor

        Public Function Modify(ByVal expr As Expression) As Expression
            Return Visit(expr)
        End Function

        Protected Overrides Function VisitBinary(ByVal b As BinaryExpression) As Expression
            If b.NodeType = ExpressionType.AndAlso Then
                Dim left = Me.Visit(b.Left)
                Dim right = Me.Visit(b.Right)

                ' Make this binary expression an OrElse operation instead
                ' of an AndAlso operation.
                Return Expression.MakeBinary(ExpressionType.OrElse, left, right, _
                                             b.IsLiftedToNull, b.Method)
            End If

            Return MyBase.VisitBinary(b)
        End Function
    End Class
    ```

    此類別會繼承 <xref:System.Linq.Expressions.ExpressionVisitor> 類別，並針對代表 `AND` 條件運算的運算式進行修改。 它會將這些運算從 `AND` 條件運算變更為 `OR` 條件運算。 為了執行這項操作，此類別會覆寫基底類型的 <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> 方法，因為 `AND` 條件運算式會以二元運算式來表示。 在 `VisitBinary` 方法中，如果傳遞給它的運算式代表 `AND` 條件運算，程式碼會建構新的運算式，以包含 `OR` 條件運算子來取代 `AND` 條件運算子。 如果傳遞給 `VisitBinary` 的運算式不代表 `AND` 條件運算，此方法會延後到基底類別實作。 基底類別方法會建構類似傳入之運算式樹狀架構的節點，但這些節點的樹狀子目錄會由造訪者以遞迴方式產生的運算式樹狀架構來取代。

4. 將 `Imports` 語句加入至命名空間的檔案 `System.Linq.Expressions` 。

5. 將程式碼加入至 `Main` Module1 檔案中的方法，以建立運算式樹狀架構，並將它傳遞給將會修改它的方法。

    ```vb
    Dim expr As Expression(Of Func(Of String, Boolean)) = _
        Function(name) name.Length > 10 AndAlso name.StartsWith("G")

    Console.WriteLine(expr)

    Dim modifier As New AndAlsoModifier()
    Dim modifiedExpr = modifier.Modify(CType(expr, Expression))

    Console.WriteLine(modifiedExpr)

    ' This code produces the following output:
    ' name => ((name.Length > 10) && name.StartsWith("G"))
    ' name => ((name.Length > 10) || name.StartsWith("G"))
    ```

    此程式碼會建立包含 `AND` 條件運算的運算式。 然後建立 `AndAlsoModifier` 類別的執行個體，並將運算式傳遞給此類別的 `Modify` 的方法。 此時會輸出原始和修改後的運算式樹狀架構，以顯示變更的情形。

6. 編譯並執行應用程式。

## <a name="see-also"></a>另請參閱

- [如何：執行運算式樹狀結構 (Visual Basic)](how-to-execute-expression-trees.md)
- [運算式樹狀結構 (Visual Basic)](index.md)

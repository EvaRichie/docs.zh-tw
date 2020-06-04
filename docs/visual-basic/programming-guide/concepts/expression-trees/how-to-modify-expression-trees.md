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
# <a name="how-to-modify-expression-trees-visual-basic"></a><span data-ttu-id="f77ed-102">如何：修改運算式樹狀結構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f77ed-102">How to: Modify Expression Trees (Visual Basic)</span></span>

<span data-ttu-id="f77ed-103">本主題示範如何修改運算式樹狀架構。</span><span class="sxs-lookup"><span data-stu-id="f77ed-103">This topic shows you how to modify an expression tree.</span></span> <span data-ttu-id="f77ed-104">運算式樹狀架構為不可變，這表示無法直接對其進行修改。</span><span class="sxs-lookup"><span data-stu-id="f77ed-104">Expression trees are immutable, which means that they cannot be modified directly.</span></span> <span data-ttu-id="f77ed-105">若要變更運算式樹狀架構，您必須建立現有運算式樹狀架構的複本，並且在建立複本時進行必要的變更。</span><span class="sxs-lookup"><span data-stu-id="f77ed-105">To change an expression tree, you must create a copy of an existing expression tree and when you create the copy, make the required changes.</span></span> <span data-ttu-id="f77ed-106">您可以使用 <xref:System.Linq.Expressions.ExpressionVisitor> 類別周遊現有的運算式樹狀架構，並複製每個瀏覽的節點。</span><span class="sxs-lookup"><span data-stu-id="f77ed-106">You can use the <xref:System.Linq.Expressions.ExpressionVisitor> class to traverse an existing expression tree and to copy each node that it visits.</span></span>

## <a name="to-modify-an-expression-tree"></a><span data-ttu-id="f77ed-107">修改運算式樹狀架構</span><span class="sxs-lookup"><span data-stu-id="f77ed-107">To modify an expression tree</span></span>

1. <span data-ttu-id="f77ed-108">建立新的**主控台應用程式**專案。</span><span class="sxs-lookup"><span data-stu-id="f77ed-108">Create a new **Console Application** project.</span></span>

2. <span data-ttu-id="f77ed-109">將 `Imports` 語句加入至命名空間的檔案 `System.Linq.Expressions` 。</span><span class="sxs-lookup"><span data-stu-id="f77ed-109">Add an `Imports` statement to the file for the `System.Linq.Expressions` namespace.</span></span>

3. <span data-ttu-id="f77ed-110">將 `AndAlsoModifier` 類別新增至專案。</span><span class="sxs-lookup"><span data-stu-id="f77ed-110">Add the `AndAlsoModifier` class to your project.</span></span>

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

    <span data-ttu-id="f77ed-111">此類別會繼承 <xref:System.Linq.Expressions.ExpressionVisitor> 類別，並針對代表 `AND` 條件運算的運算式進行修改。</span><span class="sxs-lookup"><span data-stu-id="f77ed-111">This class inherits the <xref:System.Linq.Expressions.ExpressionVisitor> class and is specialized to modify expressions that represent conditional `AND` operations.</span></span> <span data-ttu-id="f77ed-112">它會將這些運算從 `AND` 條件運算變更為 `OR` 條件運算。</span><span class="sxs-lookup"><span data-stu-id="f77ed-112">It changes these operations from a conditional `AND` to a conditional `OR`.</span></span> <span data-ttu-id="f77ed-113">為了執行這項操作，此類別會覆寫基底類型的 <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> 方法，因為 `AND` 條件運算式會以二元運算式來表示。</span><span class="sxs-lookup"><span data-stu-id="f77ed-113">To do this, the class overrides the <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> method of the base type, because conditional `AND` expressions are represented as binary expressions.</span></span> <span data-ttu-id="f77ed-114">在 `VisitBinary` 方法中，如果傳遞給它的運算式代表 `AND` 條件運算，程式碼會建構新的運算式，以包含 `OR` 條件運算子來取代 `AND` 條件運算子。</span><span class="sxs-lookup"><span data-stu-id="f77ed-114">In the `VisitBinary` method, if the expression that is passed to it represents a conditional `AND` operation, the code constructs a new expression that contains the conditional `OR` operator instead of the conditional `AND` operator.</span></span> <span data-ttu-id="f77ed-115">如果傳遞給 `VisitBinary` 的運算式不代表 `AND` 條件運算，此方法會延後到基底類別實作。</span><span class="sxs-lookup"><span data-stu-id="f77ed-115">If the expression that is passed to `VisitBinary` does not represent a conditional `AND` operation, the method defers to the base class implementation.</span></span> <span data-ttu-id="f77ed-116">基底類別方法會建構類似傳入之運算式樹狀架構的節點，但這些節點的樹狀子目錄會由造訪者以遞迴方式產生的運算式樹狀架構來取代。</span><span class="sxs-lookup"><span data-stu-id="f77ed-116">The base class methods construct nodes that are like the expression trees that are passed in, but the nodes have their sub trees replaced with the expression trees that are produced recursively by the visitor.</span></span>

4. <span data-ttu-id="f77ed-117">將 `Imports` 語句加入至命名空間的檔案 `System.Linq.Expressions` 。</span><span class="sxs-lookup"><span data-stu-id="f77ed-117">Add an `Imports` statement to the file for the `System.Linq.Expressions` namespace.</span></span>

5. <span data-ttu-id="f77ed-118">將程式碼加入至 `Main` Module1 檔案中的方法，以建立運算式樹狀架構，並將它傳遞給將會修改它的方法。</span><span class="sxs-lookup"><span data-stu-id="f77ed-118">Add code to the `Main` method in the Module1.vb file to create an expression tree and pass it to the method that will modify it.</span></span>

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

    <span data-ttu-id="f77ed-119">此程式碼會建立包含 `AND` 條件運算的運算式。</span><span class="sxs-lookup"><span data-stu-id="f77ed-119">The code creates an expression that contains a conditional `AND` operation.</span></span> <span data-ttu-id="f77ed-120">然後建立 `AndAlsoModifier` 類別的執行個體，並將運算式傳遞給此類別的 `Modify` 的方法。</span><span class="sxs-lookup"><span data-stu-id="f77ed-120">It then creates an instance of the `AndAlsoModifier` class and passes the expression to the `Modify` method of this class.</span></span> <span data-ttu-id="f77ed-121">此時會輸出原始和修改後的運算式樹狀架構，以顯示變更的情形。</span><span class="sxs-lookup"><span data-stu-id="f77ed-121">Both the original and the modified expression trees are outputted to show the change.</span></span>

6. <span data-ttu-id="f77ed-122">編譯並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f77ed-122">Compile and run the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="f77ed-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f77ed-123">See also</span></span>

- [<span data-ttu-id="f77ed-124">如何：執行運算式樹狀結構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f77ed-124">How to: Execute Expression Trees (Visual Basic)</span></span>](how-to-execute-expression-trees.md)
- [<span data-ttu-id="f77ed-125">運算式樹狀結構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f77ed-125">Expression Trees (Visual Basic)</span></span>](index.md)

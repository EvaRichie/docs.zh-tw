---
title: 命名空間
ms.date: 07/20/2015
f1_keywords:
- vb.global
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- name collisions
- Global keyword [Visual Basic]
- namespace pollution
- names [Visual Basic], avoiding conflicts
- naming conflicts [Visual Basic], namespaces
- namespaces [Visual Basic], assemblies
- Visual Basic code, namespaces
- fully qualified names [Visual Basic]
- naming conventions [Visual Basic], naming conflicts
- namespaces
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
ms.openlocfilehash: 087c6f02e1fca9cf2664ca76581c08a9b1a5e447
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398353"
---
# <a name="namespaces-in-visual-basic"></a><span data-ttu-id="32a7a-102">Visual Basic 中的命名空間</span><span class="sxs-lookup"><span data-stu-id="32a7a-102">Namespaces in Visual Basic</span></span>
<span data-ttu-id="32a7a-103">命名空間可組織組件中定義的物件。</span><span class="sxs-lookup"><span data-stu-id="32a7a-103">Namespaces organize the objects defined in an assembly.</span></span> <span data-ttu-id="32a7a-104">組件可包含多個命名空間，而命名空間也可包含其他命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-104">Assemblies can contain multiple namespaces, which can in turn contain other namespaces.</span></span> <span data-ttu-id="32a7a-105">在使用類別庫等大型物件群組時，命名空間可避免語意模糊並簡化參考。</span><span class="sxs-lookup"><span data-stu-id="32a7a-105">Namespaces prevent ambiguity and simplify references when using large groups of objects such as class libraries.</span></span>  
  
 <span data-ttu-id="32a7a-106">例如，.NET Framework 會 <xref:System.Windows.Forms.ListBox> 在命名空間中定義類別 <xref:System.Windows.Forms?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="32a7a-106">For example, the .NET Framework defines the <xref:System.Windows.Forms.ListBox> class in the <xref:System.Windows.Forms?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="32a7a-107">下列程式碼片段示範如何使用這個類別的完整名稱來宣告變數：</span><span class="sxs-lookup"><span data-stu-id="32a7a-107">The following code fragment shows how to declare a variable using the fully qualified name for this class:</span></span>  
  
 [!code-vb[VbVbalrApplication#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#6)]  
  
## <a name="avoiding-name-collisions"></a><span data-ttu-id="32a7a-108">避免名稱衝突</span><span class="sxs-lookup"><span data-stu-id="32a7a-108">Avoiding Name Collisions</span></span>  
 <span data-ttu-id="32a7a-109">.NET Framework 命名空間會解決問題，有時稱為*命名空間污染*，其中類別庫的開發人員會在另一個程式庫中使用類似的名稱而受到阻礙。</span><span class="sxs-lookup"><span data-stu-id="32a7a-109">.NET Framework namespaces address a problem sometimes called *namespace pollution*, in which the developer of a class library is hampered by the use of similar names in another library.</span></span> <span data-ttu-id="32a7a-110">這些與現有元件的衝突有時稱為 *「名稱衝突」*(name collision)。</span><span class="sxs-lookup"><span data-stu-id="32a7a-110">These conflicts with existing components are sometimes called *name collisions*.</span></span>  
  
 <span data-ttu-id="32a7a-111">例如，如果您建立了一個名為 `ListBox`的新類別，您不需提供完整名稱就可以在專案內使用它。</span><span class="sxs-lookup"><span data-stu-id="32a7a-111">For example, if you create a new class named `ListBox`, you can use it inside your project without qualification.</span></span> <span data-ttu-id="32a7a-112">不過，如果您想要 <xref:System.Windows.Forms.ListBox> 在相同的專案中使用 .NET Framework 類別，則必須使用完整參考，讓參考成為唯一的。</span><span class="sxs-lookup"><span data-stu-id="32a7a-112">However, if you want to use the .NET Framework <xref:System.Windows.Forms.ListBox> class in the same project, you must use a fully qualified reference to make the reference unique.</span></span> <span data-ttu-id="32a7a-113">如果參考不是唯一的，Visual Basic 會產生錯誤，指出名稱不明確。</span><span class="sxs-lookup"><span data-stu-id="32a7a-113">If the reference is not unique, Visual Basic produces an error stating that the name is ambiguous.</span></span> <span data-ttu-id="32a7a-114">下列程式碼範例示範如何宣告這些物件：</span><span class="sxs-lookup"><span data-stu-id="32a7a-114">The following code example demonstrates how to declare these objects:</span></span>  
  
 [!code-vb[VbVbalrApplication#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#7)]  
  
 <span data-ttu-id="32a7a-115">下圖顯示兩個命名空間階層，兩者都包含名為的物件 `ListBox` ：</span><span class="sxs-lookup"><span data-stu-id="32a7a-115">The following illustration shows two namespace hierarchies, both containing an object named `ListBox`:</span></span>  
  
 ![顯示兩個命名空間階層的螢幕擷取畫面。](./media/namespaces/visual-basic-namespace-hierarchy.gif)  
  
 <span data-ttu-id="32a7a-117">根據預設，您使用 Visual Basic 建立的每個可執行檔，都會包含一個與專案同名的命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-117">By default, every executable file you create with Visual Basic contains a namespace with the same name as your project.</span></span> <span data-ttu-id="32a7a-118">例如，如果您在名為 `ListBoxProject`的專案中定義物件，則可執行檔 ListBoxProject.exe 會包含一個稱為 `ListBoxProject`的命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-118">For example, if you define an object within a project named `ListBoxProject`, the executable file ListBoxProject.exe contains a namespace called `ListBoxProject`.</span></span>  
  
 <span data-ttu-id="32a7a-119">多個組件可以使用相同的命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-119">Multiple assemblies can use the same namespace.</span></span> <span data-ttu-id="32a7a-120">Visual Basic 會將它們視為一組名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-120">Visual Basic treats them as a single set of names.</span></span> <span data-ttu-id="32a7a-121">例如，您可以在名為 `SomeNameSpace` 的組件中為稱為 `Assemb1`的命名空間定義類別，並自一個名為 `Assemb2`的組件中為相同的命名空間定義其他類別。</span><span class="sxs-lookup"><span data-stu-id="32a7a-121">For example, you can define classes for a namespace called `SomeNameSpace` in an assembly named `Assemb1`, and define additional classes for the same namespace from an assembly named `Assemb2`.</span></span>  
  
## <a name="fully-qualified-names"></a><span data-ttu-id="32a7a-122">完整名稱</span><span class="sxs-lookup"><span data-stu-id="32a7a-122">Fully Qualified Names</span></span>  
 <span data-ttu-id="32a7a-123">完整名稱是物件參考，前面會加上定義物件之命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-123">Fully qualified names are object references that are prefixed with the name of the namespace in which the object is defined.</span></span> <span data-ttu-id="32a7a-124">如果您建立類別的參考 (在 [專案] \*\*\*\* 功能表中選擇 [加入參考] \*\*\*\* )，就可以使用其他專案中所定義的物件，並且在程式碼中使用該物件的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-124">You can use objects defined in other projects if you create a reference to the class (by choosing **Add Reference** from the **Project** menu) and then use the fully qualified name for the object in your code.</span></span> <span data-ttu-id="32a7a-125">下列程式碼片段示範如何使用另一個專案命名空間之物件的完整名稱：</span><span class="sxs-lookup"><span data-stu-id="32a7a-125">The following code fragment shows how to use the fully qualified name for an object from another project's namespace:</span></span>  
  
 [!code-vb[VbVbalrApplication#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#8)]  
  
 <span data-ttu-id="32a7a-126">完整名稱可防止命名衝突，因為完整名稱讓編譯器能夠判斷正在使用哪一個物件。</span><span class="sxs-lookup"><span data-stu-id="32a7a-126">Fully qualified names prevent naming conflicts because they make it possible for the compiler to determine which object is being used.</span></span> <span data-ttu-id="32a7a-127">不過，名稱本身可能既長又累贅。</span><span class="sxs-lookup"><span data-stu-id="32a7a-127">However, the names themselves can get long and cumbersome.</span></span> <span data-ttu-id="32a7a-128">若要解決這個問題，您可以使用 `Imports` 陳述式定義一個 *「別名」*(alias)，也就是可用於取代完整名稱的縮寫名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-128">To get around this, you can use the `Imports` statement to define an *alias*—an abbreviated name you can use in place of a fully qualified name.</span></span> <span data-ttu-id="32a7a-129">例如，下列程式碼範例會建立兩個完整名稱的別名，並使用這些別名定義兩個物件。</span><span class="sxs-lookup"><span data-stu-id="32a7a-129">For example, the following code example creates aliases for two fully qualified names, and uses these aliases to define two objects.</span></span>  
  
 [!code-vb[VbVbalrApplication#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#9)]  
  
 [!code-vb[VbVbalrApplication#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#10)]  
  
 <span data-ttu-id="32a7a-130">如果您使用沒有別名的 `Imports` 陳述式，則不需要提供完整名稱就可以使用該命名空間中的所有名稱，但前提是這些名稱對於專案而言是唯一的。</span><span class="sxs-lookup"><span data-stu-id="32a7a-130">If you use the `Imports` statement without an alias, you can use all the names in that namespace without qualification, provided they are unique to the project.</span></span> <span data-ttu-id="32a7a-131">如果您的專案所包含的 `Imports` 陳述式與命名空間內的項目有相同名稱，您必須在使用時提供完整名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-131">If your project contains `Imports` statements for namespaces that contain items with the same name, you must fully qualify that name when you use it.</span></span> <span data-ttu-id="32a7a-132">例如，假設您的專案含有下列兩個 `Imports` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="32a7a-132">Suppose, for example, your project contained the following two `Imports` statements:</span></span>  
  
 [!code-vb[VbVbalrApplication#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#11)]  
  
 <span data-ttu-id="32a7a-133">如果您嘗試在 `Class1` 沒有完整限定的情況下使用，Visual Basic 會產生錯誤，指出名稱 `Class1` 不明確。</span><span class="sxs-lookup"><span data-stu-id="32a7a-133">If you attempt to use `Class1` without fully qualifying it, Visual Basic produces an error stating that the name `Class1` is ambiguous.</span></span>  
  
## <a name="namespace-level-statements"></a><span data-ttu-id="32a7a-134">命名空間層級陳述式</span><span class="sxs-lookup"><span data-stu-id="32a7a-134">Namespace Level Statements</span></span>  
 <span data-ttu-id="32a7a-135">在命名空間中，您可以定義模組、介面、類別、委派、列舉、結構和其他命名空間等項目。</span><span class="sxs-lookup"><span data-stu-id="32a7a-135">Within a namespace, you can define items such as modules, interfaces, classes, delegates, enumerations, structures, and other namespaces.</span></span> <span data-ttu-id="32a7a-136">您無法在命名空間層級定義屬性、程序、變數和事件等項目。</span><span class="sxs-lookup"><span data-stu-id="32a7a-136">You cannot define items such as properties, procedures, variables and events at the namespace level.</span></span> <span data-ttu-id="32a7a-137">這些項目必須在模組、結構或類別等容器內宣告。</span><span class="sxs-lookup"><span data-stu-id="32a7a-137">These items must be declared within containers such as modules, structures, or classes.</span></span>  
  
## <a name="global-keyword-in-fully-qualified-names"></a><span data-ttu-id="32a7a-138">完整名稱中的 Global 關鍵字</span><span class="sxs-lookup"><span data-stu-id="32a7a-138">Global Keyword in Fully Qualified Names</span></span>  
 <span data-ttu-id="32a7a-139">如果您已定義巢狀的命名空間階層，則可能會封鎖該階層內程式碼存取 .NET Framework 的 <xref:System?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-139">If you have defined a nested hierarchy of namespaces, code inside that hierarchy might be blocked from accessing the <xref:System?displayProperty=nameWithType> namespace of the .NET Framework.</span></span> <span data-ttu-id="32a7a-140">下列範例說明 `SpecialSpace.System` 命名空間會封鎖存取 <xref:System?displayProperty=nameWithType>的階層。</span><span class="sxs-lookup"><span data-stu-id="32a7a-140">The following example illustrates a hierarchy in which the `SpecialSpace.System` namespace blocks access to <xref:System?displayProperty=nameWithType>.</span></span>  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 <span data-ttu-id="32a7a-141">因此，Visual Basic 編譯器無法順利解析 <xref:System.Int32?displayProperty=nameWithType>的參考，因為 `SpecialSpace.System` 未定義 `Int32`。</span><span class="sxs-lookup"><span data-stu-id="32a7a-141">As a result, the Visual Basic compiler cannot successfully resolve the reference to <xref:System.Int32?displayProperty=nameWithType>, because `SpecialSpace.System` does not define `Int32`.</span></span> <span data-ttu-id="32a7a-142">您可以使用 `Global` 關鍵字，在 .NET Framework 類別庫的最外層啟動限定性鏈結。</span><span class="sxs-lookup"><span data-stu-id="32a7a-142">You can use the `Global` keyword to start the qualification chain at the outermost level of the .NET Framework class library.</span></span> <span data-ttu-id="32a7a-143">這樣做可讓您指定類別庫中的 <xref:System?displayProperty=nameWithType> 命名空間或任何其他命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-143">This allows you to specify the <xref:System?displayProperty=nameWithType> namespace or any other namespace in the class library.</span></span> <span data-ttu-id="32a7a-144">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="32a7a-144">The following example illustrates this.</span></span>  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 <span data-ttu-id="32a7a-145">您可以使用 `Global` ，存取其他根層級命名空間 (例如 <xref:Microsoft.VisualBasic?displayProperty=nameWithType>) 和任何與專案相關聯的命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-145">You can use `Global` to access other root-level namespaces, such as <xref:Microsoft.VisualBasic?displayProperty=nameWithType>, and any namespace associated with your project.</span></span>  
  
## <a name="global-keyword-in-namespace-statements"></a><span data-ttu-id="32a7a-146">Namespace 陳述式中的 Global 關鍵字</span><span class="sxs-lookup"><span data-stu-id="32a7a-146">Global Keyword in Namespace Statements</span></span>  
 <span data-ttu-id="32a7a-147">您也可以在 `Global` 中使用 [Global](../../language-reference/statements/namespace-statement.md)(name collision)。</span><span class="sxs-lookup"><span data-stu-id="32a7a-147">You can also use the `Global` keyword in a [Namespace Statement](../../language-reference/statements/namespace-statement.md).</span></span> <span data-ttu-id="32a7a-148">這可讓您從專案的根命名空間定義一個命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-148">This lets you define a namespace out of the root namespace of your project.</span></span>  
  
 <span data-ttu-id="32a7a-149">專案中的所有命名空間都會以專案的根命名空間為基礎。</span><span class="sxs-lookup"><span data-stu-id="32a7a-149">All namespaces in your project are based on the root namespace for the project.</span></span>  <span data-ttu-id="32a7a-150">Visual Studio 會針對專案中的所有程式碼，將專案名稱指派為預設根命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-150">Visual Studio assigns your project name as the default root namespace for all code in your project.</span></span> <span data-ttu-id="32a7a-151">例如，如果專案已命名為 `ConsoleApplication1`，其程式設計項目會屬於命名空間 `ConsoleApplication1`。</span><span class="sxs-lookup"><span data-stu-id="32a7a-151">For example, if your project is named `ConsoleApplication1`, its programming elements belong to namespace `ConsoleApplication1`.</span></span> <span data-ttu-id="32a7a-152">如果您宣告 `Namespace Magnetosphere`，專案中的 `Magnetosphere` 參考可存取 `ConsoleApplication1.Magnetosphere`。</span><span class="sxs-lookup"><span data-stu-id="32a7a-152">If you declare `Namespace Magnetosphere`, references to `Magnetosphere` in the project will access `ConsoleApplication1.Magnetosphere`.</span></span>  
  
 <span data-ttu-id="32a7a-153">下列範例使用 `Global` 關鍵字，從專案的根命名空間宣告一個命名空間。</span><span class="sxs-lookup"><span data-stu-id="32a7a-153">The following examples use the `Global` keyword to declare a namespace out of the root namespace for the project.</span></span>  
  
 [!code-vb[VbVbalrApplication#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/module1.vb#22)]  
  
 <span data-ttu-id="32a7a-154">在命名空間宣告中， `Global` 不能以巢狀方式放在另一個命名空間中。</span><span class="sxs-lookup"><span data-stu-id="32a7a-154">In a namespace declaration, `Global` cannot be nested in another namespace.</span></span>  
  
 <span data-ttu-id="32a7a-155">您可以使用 [Application Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic) 來檢視及修改專案的 [根命名空間] \*\*\*\* 。</span><span class="sxs-lookup"><span data-stu-id="32a7a-155">You can use the [Application Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic) to view and modify the **Root Namespace** of the project.</span></span>  <span data-ttu-id="32a7a-156">若是新專案，[根命名空間] \*\*\*\* 預設為專案名稱。</span><span class="sxs-lookup"><span data-stu-id="32a7a-156">For new projects, the **Root Namespace** defaults to the project name.</span></span> <span data-ttu-id="32a7a-157">若要使 `Global` 成為最上層命名空間，您可以清除 [根命名空間] \*\*\*\* 項目讓方塊空白。</span><span class="sxs-lookup"><span data-stu-id="32a7a-157">To cause `Global` to be the top-level namespace, you can clear the **Root Namespace** entry so that the box is empty.</span></span> <span data-ttu-id="32a7a-158">清除 [根命名空間] \*\*\*\* 就不再需要命名空間宣告中的 `Global` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="32a7a-158">Clearing **Root Namespace** removes the need for the `Global` keyword in namespace declarations.</span></span>  
  
 <span data-ttu-id="32a7a-159">如果 `Namespace` 陳述式所宣告的名稱也是 .NET Framework 中的命名空間，當完整名稱中未使用 `Global` 關鍵字時，.NET Framework 命名空間會變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="32a7a-159">If a `Namespace` statement declares a name that is also a namespace in the .NET Framework, the .NET Framework namespace becomes unavailable if the `Global` keyword is not used in a fully qualified name.</span></span> <span data-ttu-id="32a7a-160">若要允許在不使用 `Global` 關鍵字的情況下存取該 .NET Framework 命名空間，您可以在 `Global` 陳述式中包含 `Namespace` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="32a7a-160">To enable access to that .NET Framework namespace without using the `Global` keyword, you can include the `Global` keyword in the `Namespace` statement.</span></span>  
  
 <span data-ttu-id="32a7a-161">下列範例在 `Global` 命名空間宣告中有 `System.Text` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="32a7a-161">The following example has the `Global` keyword in the `System.Text` namespace declaration.</span></span>  
  
 <span data-ttu-id="32a7a-162">如果 `Global` 關鍵字不在命名空間宣告中，則必須指定 <xref:System.Text.StringBuilder> 才能存取 `Global.System.Text.StringBuilder`。</span><span class="sxs-lookup"><span data-stu-id="32a7a-162">If the `Global` keyword was not present in the namespace declaration, <xref:System.Text.StringBuilder> could not be accessed without specifying `Global.System.Text.StringBuilder`.</span></span> <span data-ttu-id="32a7a-163">針對名為 `ConsoleApplication1`的專案，如果未使用 `System.Text` 關鍵字， `ConsoleApplication1.System.Text` 的參考會存取 `Global` 。</span><span class="sxs-lookup"><span data-stu-id="32a7a-163">For a project named `ConsoleApplication1`, references to `System.Text` would access `ConsoleApplication1.System.Text` if the `Global` keyword was not used.</span></span>  
  
 [!code-vb[VbVbalrApplication#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/module1.vb#21)]  
  
## <a name="see-also"></a><span data-ttu-id="32a7a-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="32a7a-164">See also</span></span>

- <xref:System.Windows.Forms.ListBox>
- <xref:System.Windows.Forms?displayProperty=nameWithType>
- [<span data-ttu-id="32a7a-165">.NET 中的組件</span><span class="sxs-lookup"><span data-stu-id="32a7a-165">Assemblies in .NET</span></span>](../../../standard/assembly/index.md)
- [<span data-ttu-id="32a7a-166">References 與 Imports 陳述式</span><span class="sxs-lookup"><span data-stu-id="32a7a-166">References and the Imports Statement</span></span>](references-and-the-imports-statement.md)
- [<span data-ttu-id="32a7a-167">Imports 陳述式 (.NET 命名空間和類型)</span><span class="sxs-lookup"><span data-stu-id="32a7a-167">Imports Statement (.NET Namespace and Type)</span></span>](../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [<span data-ttu-id="32a7a-168">撰寫 Office 方案中的程式碼</span><span class="sxs-lookup"><span data-stu-id="32a7a-168">Writing Code in Office Solutions</span></span>](/visualstudio/vsto/writing-code-in-office-solutions)

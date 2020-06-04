---
title: 如何：宣告及呼叫預設屬性
ms.date: 07/20/2015
helpviewer_keywords:
- defaults [Visual Basic], properties
- properties [Visual Basic], default
- procedures [Visual Basic], defining
- default properties [Visual Basic], in Visual Basic
- Visual Basic code, procedures
- Visual Basic code, properties
- default properties
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
ms.openlocfilehash: 4de5d94a94e764d1fc543ffae41b00a9bb729c94
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388150"
---
# <a name="how-to-declare-and-call-a-default-property-in-visual-basic"></a><span data-ttu-id="f7d36-102">如何：在 Visual Basic 中宣告及呼叫預設屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-102">How to: Declare and Call a Default Property in Visual Basic</span></span>
<span data-ttu-id="f7d36-103">*預設屬性*是您的程式碼可以存取而不需要指定的類別或結構屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-103">A *default property* is a class or structure property that your code can access without specifying it.</span></span> <span data-ttu-id="f7d36-104">呼叫程式碼時，會將類別或結構命名為，而不是屬性，而內容則允許存取屬性，Visual Basic 解析對該類別或結構的預設屬性的存取（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="f7d36-104">When calling code names a class or structure but not a property, and the context allows access to a property, Visual Basic resolves the access to that class or structure's default property if one exists.</span></span>  
  
 <span data-ttu-id="f7d36-105">類別或結構最多隻能有一個預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-105">A class or structure can have at most one default property.</span></span> <span data-ttu-id="f7d36-106">不過，您可以多載預設屬性，並擁有一個以上的版本。</span><span class="sxs-lookup"><span data-stu-id="f7d36-106">However, you can overload a default property and have more than one version of it.</span></span>  
  
 <span data-ttu-id="f7d36-107">如需詳細資訊，請參閱[Default](../../../language-reference/modifiers/default.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d36-107">For more information, see [Default](../../../language-reference/modifiers/default.md).</span></span>  
  
### <a name="to-declare-a-default-property"></a><span data-ttu-id="f7d36-108">若要宣告預設屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-108">To declare a default property</span></span>  
  
1. <span data-ttu-id="f7d36-109">以一般方式宣告屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-109">Declare the property in the normal way.</span></span> <span data-ttu-id="f7d36-110">請勿指定 `Shared` 或 `Private` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="f7d36-110">Do not specify the `Shared` or `Private` keyword.</span></span>  
  
2. <span data-ttu-id="f7d36-111">`Default`在屬性宣告中包含關鍵字。</span><span class="sxs-lookup"><span data-stu-id="f7d36-111">Include the `Default` keyword in the property declaration.</span></span>  
  
3. <span data-ttu-id="f7d36-112">請為屬性指定至少一個參數。</span><span class="sxs-lookup"><span data-stu-id="f7d36-112">Specify at least one parameter for the property.</span></span> <span data-ttu-id="f7d36-113">您不能定義不接受至少一個引數的預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-113">You cannot define a default property that does not take at least one argument.</span></span>  
  
     [!code-vb[VbVbcnProcedures#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#17)]  
  
### <a name="to-call-a-default-property"></a><span data-ttu-id="f7d36-114">呼叫預設屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-114">To call a default property</span></span>  
  
1. <span data-ttu-id="f7d36-115">宣告包含類別或結構類型的變數。</span><span class="sxs-lookup"><span data-stu-id="f7d36-115">Declare a variable of the containing class or structure type.</span></span>  
  
     [!code-vb[VbVbcnProcedures#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#16)]  
  
2. <span data-ttu-id="f7d36-116">在通常會包含屬性名稱的運算式中單獨使用變數名稱。</span><span class="sxs-lookup"><span data-stu-id="f7d36-116">Use the variable name alone in an expression where you would normally include the property name.</span></span>  
  
     [!code-vb[VbVbcnProcedures#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#21)]  
  
3. <span data-ttu-id="f7d36-117">請在括弧中的變數名稱後面加上引數清單。</span><span class="sxs-lookup"><span data-stu-id="f7d36-117">Follow the variable name with an argument list in parentheses.</span></span> <span data-ttu-id="f7d36-118">預設屬性至少必須接受一個引數。</span><span class="sxs-lookup"><span data-stu-id="f7d36-118">A default property must take at least one argument.</span></span>  
  
     [!code-vb[VbVbcnProcedures#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#20)]  
  
4. <span data-ttu-id="f7d36-119">若要抓取預設屬性值，請在運算式中使用變數名稱，並以引數清單或在指派語句中後面接著等 `=` 號（）。</span><span class="sxs-lookup"><span data-stu-id="f7d36-119">To retrieve the default property value, use the variable name, with an argument list, in an expression or following the equal (`=`) sign in an assignment statement.</span></span>  
  
     [!code-vb[VbVbcnProcedures#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#15)]  
  
5. <span data-ttu-id="f7d36-120">若要設定預設屬性值，請在指派語句的左邊使用變數名稱，以及引數清單。</span><span class="sxs-lookup"><span data-stu-id="f7d36-120">To set the default property value, use the variable name, with an argument list, on the left side of an assignment statement.</span></span>  
  
     [!code-vb[VbVbcnProcedures#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#14)]  
  
6. <span data-ttu-id="f7d36-121">您一律可以將預設屬性名稱與變數名稱一起指定，就像存取任何其他屬性一樣。</span><span class="sxs-lookup"><span data-stu-id="f7d36-121">You can always specify the default property name together with the variable name, just as you would do to access any other property.</span></span>  
  
     [!code-vb[VbVbcnProcedures#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#19)]  
  
## <a name="example"></a><span data-ttu-id="f7d36-122">範例</span><span class="sxs-lookup"><span data-stu-id="f7d36-122">Example</span></span>  
 <span data-ttu-id="f7d36-123">下列範例會宣告類別的預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-123">The following example declares a default property on a class.</span></span>  
  
 [!code-vb[VbVbcnProcedures#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#12)]  
  
## <a name="example"></a><span data-ttu-id="f7d36-124">範例</span><span class="sxs-lookup"><span data-stu-id="f7d36-124">Example</span></span>  
 <span data-ttu-id="f7d36-125">下列範例示範如何呼叫類別上的預設屬性 `myProperty` `class1` 。</span><span class="sxs-lookup"><span data-stu-id="f7d36-125">The following example demonstrates how to call the default property `myProperty` on class `class1`.</span></span> <span data-ttu-id="f7d36-126">這三個指派語句會將值儲存在中 `myProperty` ，而呼叫則會 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 讀取這些值。</span><span class="sxs-lookup"><span data-stu-id="f7d36-126">The three assignment statements store values in `myProperty`, and the <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> call reads the values.</span></span>  
  
 [!code-vb[VbVbcnProcedures#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#13)]  
  
 <span data-ttu-id="f7d36-127">預設屬性的最常見用法是 <xref:Microsoft.VisualBasic.Collection.Item%2A> 各種集合類別上的屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-127">The most common use of a default property is the <xref:Microsoft.VisualBasic.Collection.Item%2A> property on various collection classes.</span></span>  
  
## <a name="robust-programming"></a><span data-ttu-id="f7d36-128">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="f7d36-128">Robust Programming</span></span>  
 <span data-ttu-id="f7d36-129">預設屬性可能會減少原始碼字元數，但它們可能會使您的程式碼更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="f7d36-129">Default properties can result in a small reduction in source code-characters, but they can make your code more difficult to read.</span></span> <span data-ttu-id="f7d36-130">如果呼叫程式碼不熟悉您的類別或結構，當它對類別或結構名稱進行參考時，就無法確定該參考是要存取類別或結構本身，還是預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-130">If the calling code is not familiar with your class or structure, when it makes a reference to the class or structure name it cannot be certain whether that reference accesses the class or structure itself, or a default property.</span></span> <span data-ttu-id="f7d36-131">這可能會導致編譯器錯誤或細微的執行時間邏輯錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7d36-131">This can lead to compiler errors or subtle run-time logic errors.</span></span>  
  
 <span data-ttu-id="f7d36-132">您可以藉由一律使用[Option Strict 語句](../../../language-reference/statements/option-strict-statement.md)將編譯器類型檢查設定為，來減少預設屬性錯誤的機率 `On` 。</span><span class="sxs-lookup"><span data-stu-id="f7d36-132">You can somewhat reduce the chance of default property errors by always using the [Option Strict Statement](../../../language-reference/statements/option-strict-statement.md) to set compiler type checking to `On`.</span></span>  
  
 <span data-ttu-id="f7d36-133">如果您打算在程式碼中使用預先定義的類別或結構，就必須判斷它是否有預設屬性，如果是，它的名稱為何。</span><span class="sxs-lookup"><span data-stu-id="f7d36-133">If you are planning to use a predefined class or structure in your code, you must determine whether it has a default property, and if so, what its name is.</span></span>  
  
 <span data-ttu-id="f7d36-134">由於這些缺點，您應該考慮不要定義預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-134">Because of these disadvantages, you should consider not defining default properties.</span></span> <span data-ttu-id="f7d36-135">為了讓程式碼更容易閱讀，您也應該考慮明確參考所有屬性，甚至是預設屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d36-135">For code readability, you should also consider always referring to all properties explicitly, even default properties.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7d36-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f7d36-136">See also</span></span>

- [<span data-ttu-id="f7d36-137">屬性程序</span><span class="sxs-lookup"><span data-stu-id="f7d36-137">Property Procedures</span></span>](./property-procedures.md)
- [<span data-ttu-id="f7d36-138">程序參數和引數</span><span class="sxs-lookup"><span data-stu-id="f7d36-138">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="f7d36-139">Property Statement</span><span class="sxs-lookup"><span data-stu-id="f7d36-139">Property Statement</span></span>](../../../language-reference/statements/property-statement.md)
- [<span data-ttu-id="f7d36-140">預設值</span><span class="sxs-lookup"><span data-stu-id="f7d36-140">Default</span></span>](../../../language-reference/modifiers/default.md)
- [<span data-ttu-id="f7d36-141">Visual Basic 中屬性和變數的差異</span><span class="sxs-lookup"><span data-stu-id="f7d36-141">Differences Between Properties and Variables in Visual Basic</span></span>](./differences-between-properties-and-variables.md)
- [<span data-ttu-id="f7d36-142">如何：建立屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-142">How to: Create a Property</span></span>](./how-to-create-a-property.md)
- [<span data-ttu-id="f7d36-143">如何：宣告混合存取層級的屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-143">How to: Declare a Property with Mixed Access Levels</span></span>](./how-to-declare-a-property-with-mixed-access-levels.md)
- [<span data-ttu-id="f7d36-144">如何：呼叫屬性程序</span><span class="sxs-lookup"><span data-stu-id="f7d36-144">How to: Call a Property Procedure</span></span>](./how-to-call-a-property-procedure.md)
- [<span data-ttu-id="f7d36-145">如何：將值置入屬性</span><span class="sxs-lookup"><span data-stu-id="f7d36-145">How to: Put a Value in a Property</span></span>](./how-to-put-a-value-in-a-property.md)
- [<span data-ttu-id="f7d36-146">如何：取得屬性值</span><span class="sxs-lookup"><span data-stu-id="f7d36-146">How to: Get a Value from a Property</span></span>](./how-to-get-a-value-from-a-property.md)

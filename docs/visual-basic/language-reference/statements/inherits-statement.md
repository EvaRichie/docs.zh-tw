---
title: Inherits Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Inherits
- Inherits
helpviewer_keywords:
- Inherits statement [Visual Basic]
- Inherits statement [Visual Basic], syntax
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
ms.openlocfilehash: 5d88a01f90bc91a88229d19aa2368f8c71075b2f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404495"
---
# <a name="inherits-statement"></a><span data-ttu-id="ebece-102">Inherits Statement</span><span class="sxs-lookup"><span data-stu-id="ebece-102">Inherits Statement</span></span>
<span data-ttu-id="ebece-103">導致目前的類別或介面繼承另一個類別或一組介面的屬性、變數、屬性、程式和事件。</span><span class="sxs-lookup"><span data-stu-id="ebece-103">Causes the current class or interface to inherit the attributes, variables, properties, procedures, and events from another class or set of interfaces.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ebece-104">語法</span><span class="sxs-lookup"><span data-stu-id="ebece-104">Syntax</span></span>  
  
```vb  
Inherits basetypenames  
```  
  
## <a name="parts"></a><span data-ttu-id="ebece-105">組件</span><span class="sxs-lookup"><span data-stu-id="ebece-105">Parts</span></span>  
  
|<span data-ttu-id="ebece-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="ebece-106">Term</span></span>|<span data-ttu-id="ebece-107">定義</span><span class="sxs-lookup"><span data-stu-id="ebece-107">Definition</span></span>|  
|---|---|  
|`basetypenames`|<span data-ttu-id="ebece-108">必要。</span><span class="sxs-lookup"><span data-stu-id="ebece-108">Required.</span></span> <span data-ttu-id="ebece-109">這個類別衍生來源的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="ebece-109">The name of the class from which this class derives.</span></span><br /><br /> <span data-ttu-id="ebece-110">-或-</span><span class="sxs-lookup"><span data-stu-id="ebece-110">-or-</span></span><br /><br /> <span data-ttu-id="ebece-111">這個介面衍生自的介面名稱。</span><span class="sxs-lookup"><span data-stu-id="ebece-111">The names of the interfaces from which this interface derives.</span></span> <span data-ttu-id="ebece-112">使用逗號來分隔多個名稱。</span><span class="sxs-lookup"><span data-stu-id="ebece-112">Use commas to separate multiple names.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ebece-113">備註</span><span class="sxs-lookup"><span data-stu-id="ebece-113">Remarks</span></span>  
 <span data-ttu-id="ebece-114">如果使用，則 `Inherits` 語句必須是類別或介面定義中第一個非空白的非批註行。</span><span class="sxs-lookup"><span data-stu-id="ebece-114">If used, the `Inherits` statement must be the first non-blank, non-comment line in a class or interface definition.</span></span> <span data-ttu-id="ebece-115">它應該緊接在 `Class` 或 `Interface` 語句之後。</span><span class="sxs-lookup"><span data-stu-id="ebece-115">It should immediately follow the `Class` or `Interface` statement.</span></span>  
  
 <span data-ttu-id="ebece-116">您 `Inherits` 只能在類別或介面中使用。</span><span class="sxs-lookup"><span data-stu-id="ebece-116">You can use `Inherits` only in a class or interface.</span></span> <span data-ttu-id="ebece-117">這表示繼承的宣告內容不能是原始程式檔、命名空間、結構、模組、程式或區塊。</span><span class="sxs-lookup"><span data-stu-id="ebece-117">This means the declaration context for an inheritance cannot be a source file, namespace, structure, module, procedure, or block.</span></span>  
  
## <a name="rules"></a><span data-ttu-id="ebece-118">規則</span><span class="sxs-lookup"><span data-stu-id="ebece-118">Rules</span></span>  
  
- <span data-ttu-id="ebece-119">**類別繼承。**</span><span class="sxs-lookup"><span data-stu-id="ebece-119">**Class Inheritance.**</span></span> <span data-ttu-id="ebece-120">如果類別使用 `Inherits` 語句，您只能指定一個基類。</span><span class="sxs-lookup"><span data-stu-id="ebece-120">If a class uses the `Inherits` statement, you can specify only one base class.</span></span>  
  
     <span data-ttu-id="ebece-121">類別無法繼承自其內嵌套的類別。</span><span class="sxs-lookup"><span data-stu-id="ebece-121">A class cannot inherit from a class nested within it.</span></span>  
  
- <span data-ttu-id="ebece-122">**介面繼承。**</span><span class="sxs-lookup"><span data-stu-id="ebece-122">**Interface Inheritance.**</span></span> <span data-ttu-id="ebece-123">如果介面使用 `Inherits` 語句，您可以指定一或多個基底介面。</span><span class="sxs-lookup"><span data-stu-id="ebece-123">If an interface uses the `Inherits` statement, you can specify one or more base interfaces.</span></span> <span data-ttu-id="ebece-124">您可以從兩個介面繼承，即使它們各自訂具有相同名稱的成員。</span><span class="sxs-lookup"><span data-stu-id="ebece-124">You can inherit from two interfaces even if they each define a member with the same name.</span></span> <span data-ttu-id="ebece-125">如果您這樣做，則執行程式碼必須使用名稱限定性來指定它所要執行的成員。</span><span class="sxs-lookup"><span data-stu-id="ebece-125">If you do so, the implementing code must use name qualification to specify which member it is implementing.</span></span>  
  
     <span data-ttu-id="ebece-126">介面無法繼承自具有更嚴格存取層級的另一個介面。</span><span class="sxs-lookup"><span data-stu-id="ebece-126">An interface cannot inherit from another interface with a more restrictive access level.</span></span> <span data-ttu-id="ebece-127">例如， `Public` 介面無法繼承自 `Friend` 介面。</span><span class="sxs-lookup"><span data-stu-id="ebece-127">For example, a `Public` interface cannot inherit from a `Friend` interface.</span></span>  
  
     <span data-ttu-id="ebece-128">介面無法繼承自其內所嵌套的介面。</span><span class="sxs-lookup"><span data-stu-id="ebece-128">An interface cannot inherit from an interface nested within it.</span></span>  
  
 <span data-ttu-id="ebece-129">.NET Framework 中類別繼承的範例 <xref:System.ArgumentException> ，是繼承自類別的類別 <xref:System.SystemException> 。</span><span class="sxs-lookup"><span data-stu-id="ebece-129">An example of class inheritance in the .NET Framework is the <xref:System.ArgumentException> class, which inherits from the <xref:System.SystemException> class.</span></span> <span data-ttu-id="ebece-130">這會提供給 <xref:System.ArgumentException> 系統例外狀況所需的所有預先定義屬性和程式，例如 <xref:System.Exception.Message%2A> 屬性和 <xref:System.Exception.ToString%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="ebece-130">This provides to <xref:System.ArgumentException> all the predefined properties and procedures required by system exceptions, such as the <xref:System.Exception.Message%2A> property and the <xref:System.Exception.ToString%2A> method.</span></span>  
  
 <span data-ttu-id="ebece-131">.NET Framework 中的介面繼承範例是 <xref:System.Collections.ICollection> 介面，它會繼承自 <xref:System.Collections.IEnumerable> 介面。</span><span class="sxs-lookup"><span data-stu-id="ebece-131">An example of interface inheritance in the .NET Framework is the <xref:System.Collections.ICollection> interface, which inherits from the <xref:System.Collections.IEnumerable> interface.</span></span> <span data-ttu-id="ebece-132">這會導致 <xref:System.Collections.ICollection> 繼承集合所需的列舉值定義。</span><span class="sxs-lookup"><span data-stu-id="ebece-132">This causes <xref:System.Collections.ICollection> to inherit the definition of the enumerator required to traverse a collection.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ebece-133">範例</span><span class="sxs-lookup"><span data-stu-id="ebece-133">Example</span></span>  
 <span data-ttu-id="ebece-134">下列範例 `Inherits` 會使用語句來顯示名稱為的類別如何 `thisClass` 繼承名為之基類的所有成員 `anotherClass` 。</span><span class="sxs-lookup"><span data-stu-id="ebece-134">The following example uses the `Inherits` statement to show how a class named `thisClass` can inherit all the members of a base class named `anotherClass`.</span></span>  
  
 [!code-vb[VbVbalrStatements#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#37)]  
  
## <a name="example"></a><span data-ttu-id="ebece-135">範例</span><span class="sxs-lookup"><span data-stu-id="ebece-135">Example</span></span>  
 <span data-ttu-id="ebece-136">下列範例會顯示多個介面的繼承。</span><span class="sxs-lookup"><span data-stu-id="ebece-136">The following example shows inheritance of multiple interfaces.</span></span>  
  
 [!code-vb[VbVbalrStatements#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#38)]  
  
 <span data-ttu-id="ebece-137">名為的介面 `thisInterface` 現在包含、和介面中的所有定義，而 <xref:System.IComparable> 繼承的成員會 <xref:System.IDisposable> <xref:System.IFormattable> 分別提供兩個物件的類型特定比較、釋放已配置的資源，以及將物件的值表示為 `String` 。</span><span class="sxs-lookup"><span data-stu-id="ebece-137">The interface named `thisInterface` now includes all the definitions in the <xref:System.IComparable>, <xref:System.IDisposable>, and <xref:System.IFormattable> interfaces The inherited members provide respectively for type-specific comparison of two objects, releasing allocated resources, and expressing the value of an object as a `String`.</span></span> <span data-ttu-id="ebece-138">執行的類別 `thisInterface` 必須實作為每一個基底介面的每個成員。</span><span class="sxs-lookup"><span data-stu-id="ebece-138">A class that implements `thisInterface` must implement every member of every base interface.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ebece-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ebece-139">See also</span></span>

- [<span data-ttu-id="ebece-140">MustInherit</span><span class="sxs-lookup"><span data-stu-id="ebece-140">MustInherit</span></span>](../modifiers/mustinherit.md)
- [<span data-ttu-id="ebece-141">NotInheritable</span><span class="sxs-lookup"><span data-stu-id="ebece-141">NotInheritable</span></span>](../modifiers/notinheritable.md)
- [<span data-ttu-id="ebece-142">物件和類別</span><span class="sxs-lookup"><span data-stu-id="ebece-142">Objects and Classes</span></span>](../../programming-guide/language-features/objects-and-classes/index.md)
- [<span data-ttu-id="ebece-143">繼承基本概念</span><span class="sxs-lookup"><span data-stu-id="ebece-143">Inheritance Basics</span></span>](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [<span data-ttu-id="ebece-144">介面</span><span class="sxs-lookup"><span data-stu-id="ebece-144">Interfaces</span></span>](../../programming-guide/language-features/interfaces/index.md)

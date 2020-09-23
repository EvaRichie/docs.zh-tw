---
title: 作法：使用泛型類別
ms.date: 07/20/2015
helpviewer_keywords:
- type parameters [Visual Basic], defining
- data type arguments [Visual Basic], defining
- arguments [Visual Basic], data types
- Of keyword [Visual Basic], using
- generic parameters
- data type parameters
- generics [Visual Basic], about generics
- data types [Visual Basic], as parameters
- data types [Visual Basic], as arguments
- parameters [Visual Basic], type
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- generics [Visual Basic], creating generic types
- data type arguments
- parameters [Visual Basic], data type
- data type parameters [Visual Basic], defining
- type arguments [Visual Basic], defining
- arguments [Visual Basic], type
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
ms.openlocfilehash: 87ba5132afe9f5a7cd6fb33d716c670f4812c7e2
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91077107"
---
# <a name="how-to-use-a-generic-class-visual-basic"></a><span data-ttu-id="16f17-102">如何：使用泛型類別 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="16f17-102">How to: Use a Generic Class (Visual Basic)</span></span>

<span data-ttu-id="16f17-103">採用 *「類型參數」* (type parameter) 的類別稱為 *「泛型類別」*(generic class)。</span><span class="sxs-lookup"><span data-stu-id="16f17-103">A class that takes *type parameters* is called a *generic class*.</span></span> <span data-ttu-id="16f17-104">如果您使用泛型類別，則可以透過它產生 *「建構類別」* (constructed class)，方法是提供所有這些參數的 *「類型引數」* (type argument)。</span><span class="sxs-lookup"><span data-stu-id="16f17-104">If you are using a generic class, you can generate a *constructed class* from it by supplying a *type argument* for each of these parameters.</span></span> <span data-ttu-id="16f17-105">您接著可以宣告所建構類別類型的變數，而且可以建立所建構類別的執行個體，並將它指派給該變數。</span><span class="sxs-lookup"><span data-stu-id="16f17-105">You can then declare a variable of the constructed class type, and you can create an instance of the constructed class and assign it to that variable.</span></span>  
  
 <span data-ttu-id="16f17-106">除了類別之外，您還可以定義和使用泛型結構、介面、程序和委派。</span><span class="sxs-lookup"><span data-stu-id="16f17-106">In addition to classes, you can also define and use generic structures, interfaces, procedures, and delegates.</span></span>  
  
 <span data-ttu-id="16f17-107">下列程式會採用 .NET Framework 中定義的泛型類別，並從它建立實例。</span><span class="sxs-lookup"><span data-stu-id="16f17-107">The following procedure takes a generic class defined in the .NET Framework and creates an instance from it.</span></span>  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a><span data-ttu-id="16f17-108">使用採用類型參數的類別</span><span class="sxs-lookup"><span data-stu-id="16f17-108">To use a class that takes a type parameter</span></span>  
  
1. <span data-ttu-id="16f17-109">在原始程式檔的開頭，包含 [Imports 語句 ( .Net 命名空間，並輸入) ](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) 匯入 <xref:System.Collections.Generic?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="16f17-109">At the beginning of your source file, include an [Imports Statement (.NET Namespace and Type)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) to import the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="16f17-110">這可讓您參考 <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> 類別，而不需要完整限定它就區分它與其他佇列類別 (例如 <xref:System.Collections.Queue?displayProperty=nameWithType>)。</span><span class="sxs-lookup"><span data-stu-id="16f17-110">This allows you to refer to the <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> class without having to fully qualify it to differentiate it from other queue classes such as <xref:System.Collections.Queue?displayProperty=nameWithType>.</span></span>  
  
2. <span data-ttu-id="16f17-111">以一般方式建立物件，但是在類別名稱之後立即新增 `(Of type)` 。</span><span class="sxs-lookup"><span data-stu-id="16f17-111">Create the object in the normal way, but add `(Of type)` immediately after the class name.</span></span>  
  
     <span data-ttu-id="16f17-112">下列範例使用相同的類別 (<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>) 來建立保留不同資料類型之項目的兩個佇列物件。</span><span class="sxs-lookup"><span data-stu-id="16f17-112">The following example uses the same class (<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>) to create two queue objects that hold items of different data types.</span></span> <span data-ttu-id="16f17-113">它會將項目新增至每個佇列的結尾，然後移除，並顯示每個佇列前端的項目。</span><span class="sxs-lookup"><span data-stu-id="16f17-113">It adds items to the end of each queue and then removes and displays items from the front of each queue.</span></span>  
  
     [!code-vb[VbVbalrDataTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#9)]  
  
## <a name="see-also"></a><span data-ttu-id="16f17-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16f17-114">See also</span></span>

- [<span data-ttu-id="16f17-115">Data types (資料類型)</span><span class="sxs-lookup"><span data-stu-id="16f17-115">Data Types</span></span>](index.md)
- [<span data-ttu-id="16f17-116">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="16f17-116">Generic Types in Visual Basic</span></span>](generic-types.md)
- [<span data-ttu-id="16f17-117">語言獨立性以及與語言無關的元件</span><span class="sxs-lookup"><span data-stu-id="16f17-117">Language Independence and Language-Independent Components</span></span>](../../../../standard/language-independence-and-language-independent-components.md)
- [<span data-ttu-id="16f17-118">次數</span><span class="sxs-lookup"><span data-stu-id="16f17-118">Of</span></span>](../../../language-reference/statements/of-clause.md)
- [<span data-ttu-id="16f17-119">Imports 陳述式 (.NET 命名空間和類型)</span><span class="sxs-lookup"><span data-stu-id="16f17-119">Imports Statement (.NET Namespace and Type)</span></span>](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [<span data-ttu-id="16f17-120">作法：定義可以為不同資料類型提供相同功能的類別</span><span class="sxs-lookup"><span data-stu-id="16f17-120">How to: Define a Class That Can Provide Identical Functionality on Different Data Types</span></span>](how-to-define-a-class-that-can-provide-identical-functionality.md)
- [<span data-ttu-id="16f17-121">迭代器</span><span class="sxs-lookup"><span data-stu-id="16f17-121">Iterators</span></span>](../../concepts/iterators.md)

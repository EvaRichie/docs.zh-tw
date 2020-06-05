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
ms.openlocfilehash: 01f1f7ef5963feeb3fe2b5390244e4e516773bad
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393840"
---
# <a name="how-to-use-a-generic-class-visual-basic"></a><span data-ttu-id="21468-102">如何：使用泛型類別 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="21468-102">How to: Use a Generic Class (Visual Basic)</span></span>
<span data-ttu-id="21468-103">採用 *「類型參數」* (type parameter) 的類別稱為 *「泛型類別」*(generic class)。</span><span class="sxs-lookup"><span data-stu-id="21468-103">A class that takes *type parameters* is called a *generic class*.</span></span> <span data-ttu-id="21468-104">如果您使用泛型類別，則可以透過它產生 *「建構類別」* (constructed class)，方法是提供所有這些參數的 *「類型引數」* (type argument)。</span><span class="sxs-lookup"><span data-stu-id="21468-104">If you are using a generic class, you can generate a *constructed class* from it by supplying a *type argument* for each of these parameters.</span></span> <span data-ttu-id="21468-105">您接著可以宣告所建構類別類型的變數，而且可以建立所建構類別的執行個體，並將它指派給該變數。</span><span class="sxs-lookup"><span data-stu-id="21468-105">You can then declare a variable of the constructed class type, and you can create an instance of the constructed class and assign it to that variable.</span></span>  
  
 <span data-ttu-id="21468-106">除了類別之外，您還可以定義和使用泛型結構、介面、程序和委派。</span><span class="sxs-lookup"><span data-stu-id="21468-106">In addition to classes, you can also define and use generic structures, interfaces, procedures, and delegates.</span></span>  
  
 <span data-ttu-id="21468-107">下列程式會採用在 .NET Framework 中定義的泛型類別，並從中建立實例。</span><span class="sxs-lookup"><span data-stu-id="21468-107">The following procedure takes a generic class defined in the .NET Framework and creates an instance from it.</span></span>  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a><span data-ttu-id="21468-108">使用採用類型參數的類別</span><span class="sxs-lookup"><span data-stu-id="21468-108">To use a class that takes a type parameter</span></span>  
  
1. <span data-ttu-id="21468-109">在原始程式檔的開頭，加入[Imports 語句（.Net 命名空間和類型）](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)來匯入 <xref:System.Collections.Generic?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="21468-109">At the beginning of your source file, include an [Imports Statement (.NET Namespace and Type)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) to import the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="21468-110">這可讓您參考 <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> 類別，而不需要完整限定它就區分它與其他佇列類別 (例如 <xref:System.Collections.Queue?displayProperty=nameWithType>)。</span><span class="sxs-lookup"><span data-stu-id="21468-110">This allows you to refer to the <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> class without having to fully qualify it to differentiate it from other queue classes such as <xref:System.Collections.Queue?displayProperty=nameWithType>.</span></span>  
  
2. <span data-ttu-id="21468-111">以一般方式建立物件，但是在類別名稱之後立即新增 `(Of type)` 。</span><span class="sxs-lookup"><span data-stu-id="21468-111">Create the object in the normal way, but add `(Of type)` immediately after the class name.</span></span>  
  
     <span data-ttu-id="21468-112">下列範例使用相同的類別 (<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>) 來建立保留不同資料類型之項目的兩個佇列物件。</span><span class="sxs-lookup"><span data-stu-id="21468-112">The following example uses the same class (<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>) to create two queue objects that hold items of different data types.</span></span> <span data-ttu-id="21468-113">它會將項目新增至每個佇列的結尾，然後移除，並顯示每個佇列前端的項目。</span><span class="sxs-lookup"><span data-stu-id="21468-113">It adds items to the end of each queue and then removes and displays items from the front of each queue.</span></span>  
  
     [!code-vb[VbVbalrDataTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#9)]  
  
## <a name="see-also"></a><span data-ttu-id="21468-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="21468-114">See also</span></span>

- [<span data-ttu-id="21468-115">資料類型</span><span class="sxs-lookup"><span data-stu-id="21468-115">Data Types</span></span>](index.md)
- [<span data-ttu-id="21468-116">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="21468-116">Generic Types in Visual Basic</span></span>](generic-types.md)
- [<span data-ttu-id="21468-117">語言獨立性以及與語言無關的元件</span><span class="sxs-lookup"><span data-stu-id="21468-117">Language Independence and Language-Independent Components</span></span>](../../../../standard/language-independence-and-language-independent-components.md)
- [<span data-ttu-id="21468-118">的</span><span class="sxs-lookup"><span data-stu-id="21468-118">Of</span></span>](../../../language-reference/statements/of-clause.md)
- [<span data-ttu-id="21468-119">Imports 陳述式 (.NET 命名空間和類型)</span><span class="sxs-lookup"><span data-stu-id="21468-119">Imports Statement (.NET Namespace and Type)</span></span>](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [<span data-ttu-id="21468-120">作法：定義可以為不同資料類型提供相同功能的類別</span><span class="sxs-lookup"><span data-stu-id="21468-120">How to: Define a Class That Can Provide Identical Functionality on Different Data Types</span></span>](how-to-define-a-class-that-can-provide-identical-functionality.md)
- [<span data-ttu-id="21468-121">迭代器</span><span class="sxs-lookup"><span data-stu-id="21468-121">Iterators</span></span>](../../concepts/iterators.md)

---
title: "'<expression>' 不能當做類型條件約束使用"
ms.date: 07/20/2015
f1_keywords:
- bc32061
- vbc32061
helpviewer_keywords:
- BC32061
ms.assetid: b17821b7-fa14-4397-a211-6e2a14079f09
ms.openlocfilehash: 4f1db6bdbe6f25d0362b55acd95e716fbc2417ed
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874272"
---
# <a name="expression-cannot-be-used-as-a-type-constraint"></a><span data-ttu-id="6ab58-102">'\<expression>' 不能當做類型條件約束使用</span><span class="sxs-lookup"><span data-stu-id="6ab58-102">'\<expression>' cannot be used as a type constraint</span></span>

<span data-ttu-id="6ab58-103">條件約束清單包含運算式，此運算式不表示類型參數上有效的條件約束。</span><span class="sxs-lookup"><span data-stu-id="6ab58-103">A constraint list includes an expression that does not represent a valid constraint on a type parameter.</span></span>  
  
 <span data-ttu-id="6ab58-104">條件約束清單會對傳遞至類型參數的類型引數強制一些必要需求。</span><span class="sxs-lookup"><span data-stu-id="6ab58-104">A constraint list imposes requirements on the type argument passed to the type parameter.</span></span> <span data-ttu-id="6ab58-105">您可以利用任意組合指定下列需求：</span><span class="sxs-lookup"><span data-stu-id="6ab58-105">You can specify the following requirements in any combination:</span></span>  
  
- <span data-ttu-id="6ab58-106">類型引數必須實作一或多個介面</span><span class="sxs-lookup"><span data-stu-id="6ab58-106">The type argument must implement one or more interfaces</span></span>  
  
- <span data-ttu-id="6ab58-107">類型引數最多只能繼承自一個類別</span><span class="sxs-lookup"><span data-stu-id="6ab58-107">The type argument must inherit from at most one class</span></span>  
  
- <span data-ttu-id="6ab58-108">類型引數必須公開建立程式碼可以存取的無參數建構函式 (包含 `New` 條件約束)</span><span class="sxs-lookup"><span data-stu-id="6ab58-108">The type argument must expose a parameterless constructor that the creating code can access (include the `New` constraint)</span></span>  
  
 <span data-ttu-id="6ab58-109">如果您未在條件約束清單中包含任何特定類別或介面，則可以指定下列其中一項以強制更一般的需求：</span><span class="sxs-lookup"><span data-stu-id="6ab58-109">If you do not include any specific class or interface in the constraint list, you can impose a more general requirement by specifying one of the following:</span></span>  
  
- <span data-ttu-id="6ab58-110">類型引數必須是實值類型 (包含 `Structure` 條件約束)</span><span class="sxs-lookup"><span data-stu-id="6ab58-110">The type argument must be a value type (include the `Structure` constraint)</span></span>  
  
- <span data-ttu-id="6ab58-111">類型引數必須是參考類型 (包含 `Class` 條件約束)</span><span class="sxs-lookup"><span data-stu-id="6ab58-111">The type argument must be a reference type (include the `Class` constraint)</span></span>  
  
 <span data-ttu-id="6ab58-112">您無法針對相同的類型參數同時指定 `Structure` 和 `Class` ，並且無法多次指定其中一個。</span><span class="sxs-lookup"><span data-stu-id="6ab58-112">You cannot specify both `Structure` and `Class` for the same type parameter, and you cannot specify either one more than once.</span></span>  
  
 <span data-ttu-id="6ab58-113">**錯誤識別碼：** BC32061</span><span class="sxs-lookup"><span data-stu-id="6ab58-113">**Error ID:** BC32061</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="6ab58-114">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="6ab58-114">To correct this error</span></span>  
  
- <span data-ttu-id="6ab58-115">驗證是否有正確拼寫運算式與它的項目。</span><span class="sxs-lookup"><span data-stu-id="6ab58-115">Verify that the expression and its elements are spelled correctly.</span></span>  
  
- <span data-ttu-id="6ab58-116">如果運算式不符合上述的需求清單，請將它從條件約束清單中移除。</span><span class="sxs-lookup"><span data-stu-id="6ab58-116">If the expression does not qualify for the preceding list of requirements, remove it from the constraint list.</span></span>  
  
- <span data-ttu-id="6ab58-117">如果運算式參考介面或類別，請驗證編譯器是否有權存取該介面或類別。</span><span class="sxs-lookup"><span data-stu-id="6ab58-117">If the expression refers to an interface or class, verify that the compiler has access to that interface or class.</span></span> <span data-ttu-id="6ab58-118">您可能需要限定其名稱，而且也可能需要將參考加入專案中。</span><span class="sxs-lookup"><span data-stu-id="6ab58-118">You might need to qualify its name, and you might need to add a reference to your project.</span></span> <span data-ttu-id="6ab58-119">如需詳細資訊，請參閱宣告 [元素參考](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)中的「專案參考」。</span><span class="sxs-lookup"><span data-stu-id="6ab58-119">For more information, see "References to Projects" in [References to Declared Elements](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6ab58-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6ab58-120">See also</span></span>

- [<span data-ttu-id="6ab58-121">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="6ab58-121">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
- [<span data-ttu-id="6ab58-122">Value Types and Reference Types</span><span class="sxs-lookup"><span data-stu-id="6ab58-122">Value Types and Reference Types</span></span>](../../programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [<span data-ttu-id="6ab58-123">References to Declared Elements</span><span class="sxs-lookup"><span data-stu-id="6ab58-123">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)

---
title: Private
ms.date: 07/20/2015
f1_keywords:
- vb.Private
helpviewer_keywords:
- Private keyword [Visual Basic]
- Private keyword [Visual Basic], syntax
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
ms.openlocfilehash: 59f1c1666ce38923a2861244fb377007cd0fa992
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874974"
---
# <a name="private-visual-basic"></a><span data-ttu-id="2a4a6-102">Private (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2a4a6-102">Private (Visual Basic)</span></span>

<span data-ttu-id="2a4a6-103">指定一或多個宣告的程式設計專案只能從其宣告內容（包括從任何包含的型別內）存取。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-103">Specifies that one or more declared programming elements are accessible only from within their declaration context, including from within any contained types.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2a4a6-104">備註</span><span class="sxs-lookup"><span data-stu-id="2a4a6-104">Remarks</span></span>  

 <span data-ttu-id="2a4a6-105">如果程式設計項目代表專屬的功能，或包含機密資料，您通常會想要盡可能嚴格地限制其存取權。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-105">If a programming element represents proprietary functionality, or contains confidential data, you usually want to limit access to it as strictly as possible.</span></span> <span data-ttu-id="2a4a6-106">您只允許定義它來存取它的模組、類別或結構，以達到最大限制。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-106">You achieve the maximum limitation by allowing only the module, class, or structure that defines it to access it.</span></span> <span data-ttu-id="2a4a6-107">若要以這種方式限制對專案的存取，您可以使用來宣告專案 `Private` 。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-107">To limit access to an element in this way, you can declare it with `Private`.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a4a6-108">您也可以使用 [私用受保護](private-protected.md) 的存取修飾詞，讓成員可以從該類別記憶體取，也可以從位於其包含元件中的衍生類別存取。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-108">You can also use the [Private Protected](private-protected.md) access modifier, which makes a member accessible from within that class and from derived classes located in its containing assembly.</span></span>

## <a name="rules"></a><span data-ttu-id="2a4a6-109">規則</span><span class="sxs-lookup"><span data-stu-id="2a4a6-109">Rules</span></span>  

- <span data-ttu-id="2a4a6-110">**宣告內容。**</span><span class="sxs-lookup"><span data-stu-id="2a4a6-110">**Declaration Context.**</span></span> <span data-ttu-id="2a4a6-111">您只能在模組層級使用 `Private`。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-111">You can use `Private` only at module level.</span></span> <span data-ttu-id="2a4a6-112">這表示元素的宣告內容 `Private` 必須是模組、類別或結構，而且不能是原始程式檔、命名空間、介面或程式。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-112">This means the declaration context for a `Private` element must be a module, class, or structure, and cannot be a source file, namespace, interface, or procedure.</span></span>  
  
## <a name="behavior"></a><span data-ttu-id="2a4a6-113">行為</span><span class="sxs-lookup"><span data-stu-id="2a4a6-113">Behavior</span></span>  
  
- <span data-ttu-id="2a4a6-114">**存取層級。**</span><span class="sxs-lookup"><span data-stu-id="2a4a6-114">**Access Level.**</span></span> <span data-ttu-id="2a4a6-115">宣告內容中的所有程式碼都可以存取其 `Private` 元素。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-115">All code within a declaration context can access its `Private` elements.</span></span> <span data-ttu-id="2a4a6-116">這包括包含型別內的程式碼，例如嵌套類別或列舉中的指派運算式。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-116">This includes code within a contained type, such as a nested class or an assignment expression in an enumeration.</span></span> <span data-ttu-id="2a4a6-117">宣告內容之外的任何程式碼都不能存取其 `Private` 元素。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-117">No code outside of the declaration context can access its `Private` elements.</span></span>  
  
- <span data-ttu-id="2a4a6-118">**存取修飾詞。**</span><span class="sxs-lookup"><span data-stu-id="2a4a6-118">**Access Modifiers.**</span></span> <span data-ttu-id="2a4a6-119">指定存取層級的關鍵字稱為 *存取*修飾詞。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-119">The keywords that specify access level are called *access modifiers*.</span></span> <span data-ttu-id="2a4a6-120">如需存取修飾詞的比較，請參閱 [Visual Basic 中的存取層級](../../programming-guide/language-features/declared-elements/access-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="2a4a6-120">For a comparison of the access modifiers, see [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).</span></span>  
  
 <span data-ttu-id="2a4a6-121">`Private` 修飾詞可用於以下內容：</span><span class="sxs-lookup"><span data-stu-id="2a4a6-121">The `Private` modifier can be used in these contexts:</span></span>  
  
 [<span data-ttu-id="2a4a6-122">Class 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-122">Class Statement</span></span>](../statements/class-statement.md)  
  
 [<span data-ttu-id="2a4a6-123">Const 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-123">Const Statement</span></span>](../statements/const-statement.md)  
  
 [<span data-ttu-id="2a4a6-124">Declare Statement</span><span class="sxs-lookup"><span data-stu-id="2a4a6-124">Declare Statement</span></span>](../statements/declare-statement.md)  
  
 [<span data-ttu-id="2a4a6-125">Delegate 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-125">Delegate Statement</span></span>](../statements/delegate-statement.md)  
  
 [<span data-ttu-id="2a4a6-126">Dim 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-126">Dim Statement</span></span>](../statements/dim-statement.md)  
  
 [<span data-ttu-id="2a4a6-127">End 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-127">Enum Statement</span></span>](../statements/enum-statement.md)  
  
 [<span data-ttu-id="2a4a6-128">Event 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-128">Event Statement</span></span>](../statements/event-statement.md)  
  
 [<span data-ttu-id="2a4a6-129">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-129">Function Statement</span></span>](../statements/function-statement.md)  
  
 [<span data-ttu-id="2a4a6-130">Interface 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-130">Interface Statement</span></span>](../statements/interface-statement.md)  
  
 [<span data-ttu-id="2a4a6-131">Property Statement</span><span class="sxs-lookup"><span data-stu-id="2a4a6-131">Property Statement</span></span>](../statements/property-statement.md)  
  
 [<span data-ttu-id="2a4a6-132">Structure 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-132">Structure Statement</span></span>](../statements/structure-statement.md)  
  
 [<span data-ttu-id="2a4a6-133">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="2a4a6-133">Sub Statement</span></span>](../statements/sub-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="2a4a6-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2a4a6-134">See also</span></span>

- [<span data-ttu-id="2a4a6-135">公開</span><span class="sxs-lookup"><span data-stu-id="2a4a6-135">Public</span></span>](public.md)
- [<span data-ttu-id="2a4a6-136">保護</span><span class="sxs-lookup"><span data-stu-id="2a4a6-136">Protected</span></span>](protected.md)
- [<span data-ttu-id="2a4a6-137">Friend</span><span class="sxs-lookup"><span data-stu-id="2a4a6-137">Friend</span></span>](friend.md)
- [<span data-ttu-id="2a4a6-138">私用保護</span><span class="sxs-lookup"><span data-stu-id="2a4a6-138">Private Protected</span></span>](./private-protected.md)
- [<span data-ttu-id="2a4a6-139">Protected Friend</span><span class="sxs-lookup"><span data-stu-id="2a4a6-139">Protected Friend</span></span>](./protected-friend.md)
- [<span data-ttu-id="2a4a6-140">Visual Basic 中的存取層級</span><span class="sxs-lookup"><span data-stu-id="2a4a6-140">Access levels in Visual Basic</span></span>](../../programming-guide/language-features/declared-elements/access-levels.md)
- [<span data-ttu-id="2a4a6-141">程序</span><span class="sxs-lookup"><span data-stu-id="2a4a6-141">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
- [<span data-ttu-id="2a4a6-142">結構</span><span class="sxs-lookup"><span data-stu-id="2a4a6-142">Structures</span></span>](../../programming-guide/language-features/data-types/structures.md)
- [<span data-ttu-id="2a4a6-143">物件和類別</span><span class="sxs-lookup"><span data-stu-id="2a4a6-143">Objects and Classes</span></span>](../../programming-guide/language-features/objects-and-classes/index.md)

---
title: Shadows
ms.date: 07/20/2015
f1_keywords:
- vb.Shadows
- shadows
helpviewer_keywords:
- shadowing
- duplicate names [Visual Basic]
- scope [Visual Basic], shadowing
- Shadows keyword [Visual Basic]
- names [Visual Basic], shadowing
ms.assetid: 6bf687cd-0544-4797-b51b-911125ec57c6
ms.openlocfilehash: 7aed6bec21bd484cca019b061bd5915de13a9eb8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402703"
---
# <a name="shadows-visual-basic"></a><span data-ttu-id="24c23-102">Shadows (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="24c23-102">Shadows (Visual Basic)</span></span>

<span data-ttu-id="24c23-103">指定宣告的程式設計專案會在基類中重新宣告並隱藏具有相同名稱的專案或多載元素的集合。</span><span class="sxs-lookup"><span data-stu-id="24c23-103">Specifies that a declared programming element redeclares and hides an identically named element, or set of overloaded elements, in a base class.</span></span>

## <a name="remarks"></a><span data-ttu-id="24c23-104">備註</span><span class="sxs-lookup"><span data-stu-id="24c23-104">Remarks</span></span>

<span data-ttu-id="24c23-105">遮蔽的主要目的（也稱為「*依名稱隱藏*」）是保留類別成員的定義。</span><span class="sxs-lookup"><span data-stu-id="24c23-105">The main purpose of shadowing (which is also known as *hiding by name*) is to preserve the definition of your class members.</span></span> <span data-ttu-id="24c23-106">基類可能會進行一項變更，以建立一個與您已定義的專案名稱相同的元素。</span><span class="sxs-lookup"><span data-stu-id="24c23-106">The base class might undergo a change that creates an element with the same name as one you have already defined.</span></span> <span data-ttu-id="24c23-107">如果發生這種情況， `Shadows` 修飾詞會強制透過類別的參考解析成您所定義的成員，而不是新的基類元素。</span><span class="sxs-lookup"><span data-stu-id="24c23-107">If this happens, the `Shadows` modifier forces references through your class to be resolved to the member you defined, instead of to the new base class element.</span></span>

<span data-ttu-id="24c23-108">遮蔽和覆寫都會重新定義繼承的項目，但這兩種方法之間有顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="24c23-108">Both shadowing and overriding redefine an inherited element, but there are significant differences between the two approaches.</span></span> <span data-ttu-id="24c23-109">如需詳細資訊，請參閱[Visual Basic 中的陰影](../../programming-guide/language-features/declared-elements/shadowing.md)。</span><span class="sxs-lookup"><span data-stu-id="24c23-109">For more information, see [Shadowing in Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md).</span></span>

## <a name="rules"></a><span data-ttu-id="24c23-110">規則</span><span class="sxs-lookup"><span data-stu-id="24c23-110">Rules</span></span>

- <span data-ttu-id="24c23-111">**宣告內容。**</span><span class="sxs-lookup"><span data-stu-id="24c23-111">**Declaration Context.**</span></span> <span data-ttu-id="24c23-112">您 `Shadows` 只能在類別層級使用。</span><span class="sxs-lookup"><span data-stu-id="24c23-112">You can use `Shadows` only at class level.</span></span> <span data-ttu-id="24c23-113">這表示元素的宣告內容 `Shadows` 必須是類別，而且不能是原始程式檔、命名空間、介面、模組、結構或程式。</span><span class="sxs-lookup"><span data-stu-id="24c23-113">This means the declaration context for a `Shadows` element must be a class, and cannot be a source file, namespace, interface, module, structure, or procedure.</span></span>

  <span data-ttu-id="24c23-114">您只能在單一宣告語句中宣告一個遮蔽元素。</span><span class="sxs-lookup"><span data-stu-id="24c23-114">You can declare only one shadowing element in a single declaration statement.</span></span>

- <span data-ttu-id="24c23-115">**結合的修飾詞。**</span><span class="sxs-lookup"><span data-stu-id="24c23-115">**Combined Modifiers.**</span></span> <span data-ttu-id="24c23-116">您不能 `Shadows` `Overloads` `Overrides` 在相同的宣告中，搭配、或來指定 `Static` 。</span><span class="sxs-lookup"><span data-stu-id="24c23-116">You cannot specify `Shadows` together with `Overloads`, `Overrides`, or `Static` in the same declaration.</span></span>

- <span data-ttu-id="24c23-117">**元素類型。**</span><span class="sxs-lookup"><span data-stu-id="24c23-117">**Element Types.**</span></span> <span data-ttu-id="24c23-118">您可以使用任何其他類型遮蔽任何一種已宣告的項目。</span><span class="sxs-lookup"><span data-stu-id="24c23-118">You can shadow any kind of declared element with any other kind.</span></span> <span data-ttu-id="24c23-119">如果您使用另一個屬性或程式來遮蔽屬性或程式，參數和傳回型別就不需要與基類屬性或程式中的相同。</span><span class="sxs-lookup"><span data-stu-id="24c23-119">If you shadow a property or procedure with another property or procedure, the parameters and the return type do not have to match those in the base class property or procedure.</span></span>

- <span data-ttu-id="24c23-120">**正在.**</span><span class="sxs-lookup"><span data-stu-id="24c23-120">**Accessing.**</span></span> <span data-ttu-id="24c23-121">基類中的陰影元素通常無法從遮蔽它的衍生類別中使用。</span><span class="sxs-lookup"><span data-stu-id="24c23-121">The shadowed element in the base class is normally unavailable from within the derived class that shadows it.</span></span> <span data-ttu-id="24c23-122">不過，下列考慮適用于。</span><span class="sxs-lookup"><span data-stu-id="24c23-122">However, the following considerations apply.</span></span>

  - <span data-ttu-id="24c23-123">如果無法從參考的程式碼存取遮蔽專案，則會將參考解析為陰影專案。</span><span class="sxs-lookup"><span data-stu-id="24c23-123">If the shadowing element is not accessible from the code referring to it, the reference is resolved to the shadowed element.</span></span> <span data-ttu-id="24c23-124">例如，如果專案 `Private` 遮蔽基類元素，則沒有許可權存取專案的程式碼會改為存取 `Private` 基類元素。</span><span class="sxs-lookup"><span data-stu-id="24c23-124">For example, if a `Private` element shadows a base class element, code that does not have permission to access the `Private` element accesses the base class element instead.</span></span>

  - <span data-ttu-id="24c23-125">如果您遮蔽某個元素，仍然可以透過以基類類型宣告的物件來存取陰影元素。</span><span class="sxs-lookup"><span data-stu-id="24c23-125">If you shadow an element, you can still access the shadowed element through an object declared with the type of the base class.</span></span> <span data-ttu-id="24c23-126">您也可以透過來存取它 `MyBase` 。</span><span class="sxs-lookup"><span data-stu-id="24c23-126">You can also access it through `MyBase`.</span></span>

<span data-ttu-id="24c23-127">`Shadows` 修飾詞可用於以下內容：</span><span class="sxs-lookup"><span data-stu-id="24c23-127">The `Shadows` modifier can be used in these contexts:</span></span>

- [<span data-ttu-id="24c23-128">Class 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-128">Class Statement</span></span>](../statements/class-statement.md)

- [<span data-ttu-id="24c23-129">Const 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-129">Const Statement</span></span>](../statements/const-statement.md)

- [<span data-ttu-id="24c23-130">Declare Statement</span><span class="sxs-lookup"><span data-stu-id="24c23-130">Declare Statement</span></span>](../statements/declare-statement.md)

- [<span data-ttu-id="24c23-131">Delegate 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-131">Delegate Statement</span></span>](../statements/delegate-statement.md)

- [<span data-ttu-id="24c23-132">Dim 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-132">Dim Statement</span></span>](../statements/dim-statement.md)

- [<span data-ttu-id="24c23-133">End 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-133">Enum Statement</span></span>](../statements/enum-statement.md)

- [<span data-ttu-id="24c23-134">Event 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-134">Event Statement</span></span>](../statements/event-statement.md)

- [<span data-ttu-id="24c23-135">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-135">Function Statement</span></span>](../statements/function-statement.md)

- [<span data-ttu-id="24c23-136">Interface 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-136">Interface Statement</span></span>](../statements/interface-statement.md)

- [<span data-ttu-id="24c23-137">Property Statement</span><span class="sxs-lookup"><span data-stu-id="24c23-137">Property Statement</span></span>](../statements/property-statement.md)

- [<span data-ttu-id="24c23-138">Structure 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-138">Structure Statement</span></span>](../statements/structure-statement.md)

- [<span data-ttu-id="24c23-139">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="24c23-139">Sub Statement</span></span>](../statements/sub-statement.md)

## <a name="see-also"></a><span data-ttu-id="24c23-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="24c23-140">See also</span></span>

- <span data-ttu-id="24c23-141">[共用][](shared.md)</span><span class="sxs-lookup"><span data-stu-id="24c23-141">[Shared](shared.md)</span></span>
- [<span data-ttu-id="24c23-142">靜態</span><span class="sxs-lookup"><span data-stu-id="24c23-142">Static</span></span>](static.md)
- [<span data-ttu-id="24c23-143">私用</span><span class="sxs-lookup"><span data-stu-id="24c23-143">Private</span></span>](private.md)
- [<span data-ttu-id="24c23-144">Me、My、MyBase 及 MyClass</span><span class="sxs-lookup"><span data-stu-id="24c23-144">Me, My, MyBase, and MyClass</span></span>](../../programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [<span data-ttu-id="24c23-145">繼承基本概念</span><span class="sxs-lookup"><span data-stu-id="24c23-145">Inheritance Basics</span></span>](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [<span data-ttu-id="24c23-146">New</span><span class="sxs-lookup"><span data-stu-id="24c23-146">MustOverride</span></span>](mustoverride.md)
- [<span data-ttu-id="24c23-147">NotOverridable</span><span class="sxs-lookup"><span data-stu-id="24c23-147">NotOverridable</span></span>](notoverridable.md)
- [<span data-ttu-id="24c23-148">多載</span><span class="sxs-lookup"><span data-stu-id="24c23-148">Overloads</span></span>](overloads.md)
- [<span data-ttu-id="24c23-149">Overrides</span><span class="sxs-lookup"><span data-stu-id="24c23-149">Overridable</span></span>](overridable.md)
- [<span data-ttu-id="24c23-150">覆寫</span><span class="sxs-lookup"><span data-stu-id="24c23-150">Overrides</span></span>](overrides.md)
- [<span data-ttu-id="24c23-151">Visual Basic 中的遮蔽功能</span><span class="sxs-lookup"><span data-stu-id="24c23-151">Shadowing in Visual Basic</span></span>](../../programming-guide/language-features/declared-elements/shadowing.md)

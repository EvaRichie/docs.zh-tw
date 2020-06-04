---
title: New
ms.date: 07/20/2015
f1_keywords:
- vb.MustOverride
- MustOverride
helpviewer_keywords:
- virtual elements [Visual Basic], pure
- elements [Visual Basic], pure virtual
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- overriding, MustOverride keyword
- procedures [Visual Basic], redefining
- pure virtual elements [Visual Basic]
- MustOverride keyword [Visual Basic]
- properties [Visual Basic], overriding
ms.assetid: 6e9d9ad6-bb64-433f-b32b-3ef84293bf96
ms.openlocfilehash: 1b20108a2d42e82c0af7598fde8d60a08fea28ec
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396190"
---
# <a name="mustoverride-visual-basic"></a><span data-ttu-id="b514a-102">MustOverride (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b514a-102">MustOverride (Visual Basic)</span></span>
<span data-ttu-id="b514a-103">指定在這個類別中不會實作為屬性或程式，而且必須在衍生類別中加以覆寫，才可以使用它。</span><span class="sxs-lookup"><span data-stu-id="b514a-103">Specifies that a property or procedure is not implemented in this class and must be overridden in a derived class before it can be used.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b514a-104">備註</span><span class="sxs-lookup"><span data-stu-id="b514a-104">Remarks</span></span>  
 <span data-ttu-id="b514a-105">您 `MustOverride` 只能在屬性或程式宣告語句中使用。</span><span class="sxs-lookup"><span data-stu-id="b514a-105">You can use `MustOverride` only in a property or procedure declaration statement.</span></span> <span data-ttu-id="b514a-106">指定的屬性或程式 `MustOverride` 必須是類別的成員，而且類別必須標記為[MustInherit](mustinherit.md)。</span><span class="sxs-lookup"><span data-stu-id="b514a-106">The property or procedure that specifies `MustOverride` must be a member of a class, and the class must be marked [MustInherit](mustinherit.md).</span></span>  
  
## <a name="rules"></a><span data-ttu-id="b514a-107">規則</span><span class="sxs-lookup"><span data-stu-id="b514a-107">Rules</span></span>  
  
- <span data-ttu-id="b514a-108">**不完整的宣告。**</span><span class="sxs-lookup"><span data-stu-id="b514a-108">**Incomplete Declaration.**</span></span> <span data-ttu-id="b514a-109">當您指定時，不會 `MustOverride` 為屬性或程式提供任何額外的程式程式碼，甚至不會提供 `End Function` 、 `End Property` 或 `End Sub` 語句。</span><span class="sxs-lookup"><span data-stu-id="b514a-109">When you specify `MustOverride`, you do not supply any additional lines of code for the property or procedure, not even the `End Function`, `End Property`, or `End Sub` statement.</span></span>  
  
- <span data-ttu-id="b514a-110">**結合的修飾詞。**</span><span class="sxs-lookup"><span data-stu-id="b514a-110">**Combined Modifiers.**</span></span> <span data-ttu-id="b514a-111">您不能 `MustOverride` `NotOverridable` `Overridable` 在相同的宣告中，搭配、或來指定 `Shared` 。</span><span class="sxs-lookup"><span data-stu-id="b514a-111">You cannot specify `MustOverride` together with `NotOverridable`, `Overridable`, or `Shared` in the same declaration.</span></span>  
  
- <span data-ttu-id="b514a-112">**遮蔽和覆寫。**</span><span class="sxs-lookup"><span data-stu-id="b514a-112">**Shadowing and Overriding.**</span></span> <span data-ttu-id="b514a-113">遮蔽和覆寫都會重新定義繼承的項目，但這兩種方法之間有顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="b514a-113">Both shadowing and overriding redefine an inherited element, but there are significant differences between the two approaches.</span></span> <span data-ttu-id="b514a-114">如需詳細資訊，請參閱[Visual Basic 中的陰影](../../programming-guide/language-features/declared-elements/shadowing.md)。</span><span class="sxs-lookup"><span data-stu-id="b514a-114">For more information, see [Shadowing in Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md).</span></span>  
  
- <span data-ttu-id="b514a-115">**替代詞彙。**</span><span class="sxs-lookup"><span data-stu-id="b514a-115">**Alternate Terms.**</span></span> <span data-ttu-id="b514a-116">除非在覆寫中，否則無法使用的元素，有時稱為*純虛擬*元素。</span><span class="sxs-lookup"><span data-stu-id="b514a-116">An element that cannot be used except in an override is sometimes called a *pure virtual* element.</span></span>  
  
 <span data-ttu-id="b514a-117">`MustOverride` 修飾詞可用於以下內容：</span><span class="sxs-lookup"><span data-stu-id="b514a-117">The `MustOverride` modifier can be used in these contexts:</span></span>  
  
 [<span data-ttu-id="b514a-118">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="b514a-118">Function Statement</span></span>](../statements/function-statement.md)  
  
 [<span data-ttu-id="b514a-119">Property Statement</span><span class="sxs-lookup"><span data-stu-id="b514a-119">Property Statement</span></span>](../statements/property-statement.md)  
  
 [<span data-ttu-id="b514a-120">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="b514a-120">Sub Statement</span></span>](../statements/sub-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="b514a-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b514a-121">See also</span></span>

- [<span data-ttu-id="b514a-122">NotOverridable</span><span class="sxs-lookup"><span data-stu-id="b514a-122">NotOverridable</span></span>](notoverridable.md)
- [<span data-ttu-id="b514a-123">Overrides</span><span class="sxs-lookup"><span data-stu-id="b514a-123">Overridable</span></span>](overridable.md)
- [<span data-ttu-id="b514a-124">覆寫</span><span class="sxs-lookup"><span data-stu-id="b514a-124">Overrides</span></span>](overrides.md)
- [<span data-ttu-id="b514a-125">MustInherit</span><span class="sxs-lookup"><span data-stu-id="b514a-125">MustInherit</span></span>](mustinherit.md)
- [<span data-ttu-id="b514a-126">關鍵字</span><span class="sxs-lookup"><span data-stu-id="b514a-126">Keywords</span></span>](../keywords/index.md)
- [<span data-ttu-id="b514a-127">Visual Basic 中的遮蔽功能</span><span class="sxs-lookup"><span data-stu-id="b514a-127">Shadowing in Visual Basic</span></span>](../../programming-guide/language-features/declared-elements/shadowing.md)

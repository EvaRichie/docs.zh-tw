---
title: Protected Friend
ms.date: 05/10/2018
f1_keywords:
- vb.ProtectedFriend
helpviewer_keywords:
- Protected Friend keyword [Visual Basic]
- Protected Friend keyword [Visual Basic], syntax
ms.openlocfilehash: 27fc993ca0b94d406261d5e6275de8cd619eb6a8
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303448"
---
# <a name="protected-friend-visual-basic"></a><span data-ttu-id="37ebd-102">受保護的 Friend （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="37ebd-102">Protected Friend (Visual Basic)</span></span>

<span data-ttu-id="37ebd-103">`Protected Friend` 關鍵字組合是成員存取修飾詞。</span><span class="sxs-lookup"><span data-stu-id="37ebd-103">The `Protected Friend` keyword combination is a member access modifier.</span></span> <span data-ttu-id="37ebd-104">它會在宣告的元素上授[Friend](friend.md)存取和[受保護](protected.md)的存取，因此可以從相同元件中的任何位置、從其本身的類別，以及從衍生類別存取。</span><span class="sxs-lookup"><span data-stu-id="37ebd-104">It confers both [Friend](friend.md) access and [Protected](protected.md) access on the declared elements, so they are accessible from anywhere in the same assembly, from their own class, and from derived classes.</span></span> <span data-ttu-id="37ebd-105">您 `Protected Friend` 只能在類別的成員上指定，因為無法繼承結構，所以無法套用 `Protected Friend` 到結構的成員。</span><span class="sxs-lookup"><span data-stu-id="37ebd-105">You can specify `Protected Friend` only on members of classes; you cannot apply `Protected Friend` to members of a structure because structures cannot be inherited.</span></span>

> [!NOTE]
> <span data-ttu-id="37ebd-106">在 Visual Studio 中，選取 [F1 `protected friend` 說明] 會提供[受保護](protected.md)或[friend](friend.md)的協助。</span><span class="sxs-lookup"><span data-stu-id="37ebd-106">In Visual Studio, selecting F1 help on `protected friend` provides help for either [protected](protected.md) or [friend](friend.md).</span></span> <span data-ttu-id="37ebd-107">IDE 會挑選游標下的單一 token，而不是複合字組。</span><span class="sxs-lookup"><span data-stu-id="37ebd-107">The IDE picks the single token under the cursor rather than the compound word.</span></span>

## <a name="rules"></a><span data-ttu-id="37ebd-108">規則</span><span class="sxs-lookup"><span data-stu-id="37ebd-108">Rules</span></span>

<span data-ttu-id="37ebd-109">**宣告內容。**</span><span class="sxs-lookup"><span data-stu-id="37ebd-109">**Declaration Context.**</span></span> <span data-ttu-id="37ebd-110">您 `Protected Friend` 只能在類別層級使用。</span><span class="sxs-lookup"><span data-stu-id="37ebd-110">You can use `Protected Friend` only at the class level.</span></span> <span data-ttu-id="37ebd-111">這表示元素的宣告內容 `Protected` 必須是類別，而且不能是原始程式檔、命名空間、介面、模組、結構或程式。</span><span class="sxs-lookup"><span data-stu-id="37ebd-111">This means the declaration context for a `Protected` element must be a class, and cannot be a source file, namespace, interface, module, structure, or procedure.</span></span>

## <a name="see-also"></a><span data-ttu-id="37ebd-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="37ebd-112">See also</span></span>

- [<span data-ttu-id="37ebd-113">公開</span><span class="sxs-lookup"><span data-stu-id="37ebd-113">Public</span></span>](public.md)
- [<span data-ttu-id="37ebd-114">免受</span><span class="sxs-lookup"><span data-stu-id="37ebd-114">Protected</span></span>](protected.md)
- [<span data-ttu-id="37ebd-115">給</span><span class="sxs-lookup"><span data-stu-id="37ebd-115">Friend</span></span>](friend.md)
- [<span data-ttu-id="37ebd-116">私用</span><span class="sxs-lookup"><span data-stu-id="37ebd-116">Private</span></span>](private.md)
- [<span data-ttu-id="37ebd-117">私用保護</span><span class="sxs-lookup"><span data-stu-id="37ebd-117">Private Protected</span></span>](./private-protected.md)
- [<span data-ttu-id="37ebd-118">Visual Basic 中的存取層級</span><span class="sxs-lookup"><span data-stu-id="37ebd-118">Access levels in Visual Basic</span></span>](../../programming-guide/language-features/declared-elements/access-levels.md)
- [<span data-ttu-id="37ebd-119">程序</span><span class="sxs-lookup"><span data-stu-id="37ebd-119">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
- [<span data-ttu-id="37ebd-120">結構</span><span class="sxs-lookup"><span data-stu-id="37ebd-120">Structures</span></span>](../../programming-guide/language-features/data-types/structures.md)
- [<span data-ttu-id="37ebd-121">物件和類別</span><span class="sxs-lookup"><span data-stu-id="37ebd-121">Objects and Classes</span></span>](../../programming-guide/language-features/objects-and-classes/index.md)

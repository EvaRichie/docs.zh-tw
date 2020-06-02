---
title: 虛擬成員
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- overridable members
- virtual members
- members [.NET Framework], virtual
ms.assetid: 8ff4eb97-0364-43ec-8a02-934b5cd94d19
ms.openlocfilehash: 9eb6cbef969e51dee1a72d402c124d06f08fe5c4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288494"
---
# <a name="virtual-members"></a><span data-ttu-id="82743-102">虛擬成員</span><span class="sxs-lookup"><span data-stu-id="82743-102">Virtual Members</span></span>
<span data-ttu-id="82743-103">可以覆寫虛擬成員，因此變更子類別的行為。</span><span class="sxs-lookup"><span data-stu-id="82743-103">Virtual members can be overridden, thus changing the behavior of the subclass.</span></span> <span data-ttu-id="82743-104">它們在其提供的擴充性方面相當類似回呼，但它們在執行效能和記憶體耗用量方面比較好。</span><span class="sxs-lookup"><span data-stu-id="82743-104">They are quite similar to callbacks in terms of the extensibility they provide, but they are better in terms of execution performance and memory consumption.</span></span> <span data-ttu-id="82743-105">此外，在需要建立一種特殊類型（特製化）的案例中，虛擬成員的外觀更為自然。</span><span class="sxs-lookup"><span data-stu-id="82743-105">Also, virtual members feel more natural in scenarios that require creating a special kind of an existing type (specialization).</span></span>

 <span data-ttu-id="82743-106">虛擬成員的執行效果優於回呼和事件，但不會比非虛擬方法執行得好。</span><span class="sxs-lookup"><span data-stu-id="82743-106">Virtual members perform better than callbacks and events, but do not perform better than non-virtual methods.</span></span>

 <span data-ttu-id="82743-107">虛擬成員的主要缺點在於，虛擬成員的行為只能在編譯時進行修改。</span><span class="sxs-lookup"><span data-stu-id="82743-107">The main disadvantage of virtual members is that the behavior of a virtual member can only be modified at the time of compilation.</span></span> <span data-ttu-id="82743-108">您可以在執行時間修改回呼的行為。</span><span class="sxs-lookup"><span data-stu-id="82743-108">The behavior of a callback can be modified at run time.</span></span>

 <span data-ttu-id="82743-109">像回呼（也可能是回呼）等虛擬成員的設計、測試和維護成本高昂，因為對虛擬成員的任何呼叫都可以在無法預期的情況下遭到覆寫，而且可以執行任意程式碼。</span><span class="sxs-lookup"><span data-stu-id="82743-109">Virtual members, like callbacks (and maybe more than callbacks), are costly to design, test, and maintain because any call to a virtual member can be overridden in unpredictable ways and can execute arbitrary code.</span></span> <span data-ttu-id="82743-110">此外，通常需要更多的工作來清楚定義虛擬成員的合約，因此設計和記錄它們的成本會更高。</span><span class="sxs-lookup"><span data-stu-id="82743-110">Also, much more effort is usually required to clearly define the contract of virtual members, so the cost of designing and documenting them is higher.</span></span>

 <span data-ttu-id="82743-111">❌除非您有很好的理由要這麼做，否則請不要將成員設為虛擬，而且您會瞭解與設計、測試和維護虛擬成員相關的所有成本。</span><span class="sxs-lookup"><span data-stu-id="82743-111">❌ DO NOT make members virtual unless you have a good reason to do so and you are aware of all the costs related to designing, testing, and maintaining virtual members.</span></span>

 <span data-ttu-id="82743-112">在不中斷相容性的情況下，虛擬成員可以對其進行變更，而不會有太大的容許。</span><span class="sxs-lookup"><span data-stu-id="82743-112">Virtual members are less forgiving in terms of changes that can be made to them without breaking compatibility.</span></span> <span data-ttu-id="82743-113">此外，它們的速度會比非虛擬成員慢，主要是因為不會內嵌對虛擬成員的呼叫。</span><span class="sxs-lookup"><span data-stu-id="82743-113">Also, they are slower than non-virtual members, mostly because calls to virtual members are not inlined.</span></span>

 <span data-ttu-id="82743-114">✔️考慮限制只有絕對必要的擴充性。</span><span class="sxs-lookup"><span data-stu-id="82743-114">✔️ CONSIDER limiting extensibility to only what is absolutely necessary.</span></span>

 <span data-ttu-id="82743-115">✔️偏好透過虛擬成員的公用存取範圍來保護存取範圍。</span><span class="sxs-lookup"><span data-stu-id="82743-115">✔️ DO prefer protected accessibility over public accessibility for virtual members.</span></span> <span data-ttu-id="82743-116">公用成員應該藉由呼叫受保護的虛擬成員來提供擴充性（如有需要）。</span><span class="sxs-lookup"><span data-stu-id="82743-116">Public members should provide extensibility (if required) by calling into a protected virtual member.</span></span>

 <span data-ttu-id="82743-117">類別的公用成員應該為該類別的直接取用者提供正確的功能集。</span><span class="sxs-lookup"><span data-stu-id="82743-117">The public members of a class should provide the right set of functionality for direct consumers of that class.</span></span> <span data-ttu-id="82743-118">虛擬成員是設計用來在子類別中覆寫，而受保護的存取範圍是將所有虛擬擴充點限定于其使用位置的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="82743-118">Virtual members are designed to be overridden in subclasses, and protected accessibility is a great way to scope all virtual extensibility points to where they can be used.</span></span>

 <span data-ttu-id="82743-119">*部分©2005、2009 Microsoft Corporation。已保留擁有權限。*</span><span class="sxs-lookup"><span data-stu-id="82743-119">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="82743-120">獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 節錄。\*\*</span><span class="sxs-lookup"><span data-stu-id="82743-120">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="82743-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="82743-121">See also</span></span>

- [<span data-ttu-id="82743-122">架構設計方針</span><span class="sxs-lookup"><span data-stu-id="82743-122">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="82743-123">擴充性設計</span><span class="sxs-lookup"><span data-stu-id="82743-123">Designing for Extensibility</span></span>](designing-for-extensibility.md)

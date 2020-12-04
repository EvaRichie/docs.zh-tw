---
title: " (程式碼分析) 的命名規則"
description: 瞭解程式碼分析命名規則。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis rules, naming rules
- naming rules
- rules, naming
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 88e7ec6bc1051fa98c46696b2193a5d5912eb111
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "96585235"
---
# <a name="naming-rules"></a><span data-ttu-id="72d10-103">命名規則</span><span class="sxs-lookup"><span data-stu-id="72d10-103">Naming rules</span></span>

<span data-ttu-id="72d10-104">命名規則支援遵守 .NET 設計指導方針的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="72d10-104">Naming rules support adherence to the naming conventions of the .NET Design Guidelines.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="72d10-105">本節內容</span><span class="sxs-lookup"><span data-stu-id="72d10-105">In this section</span></span>

|<span data-ttu-id="72d10-106">規則</span><span class="sxs-lookup"><span data-stu-id="72d10-106">Rule</span></span>|<span data-ttu-id="72d10-107">描述</span><span class="sxs-lookup"><span data-stu-id="72d10-107">Description</span></span>|
|----------|-----------------|
|[<span data-ttu-id="72d10-108">CA1700:不要在列舉值名稱中包含 'Reserved'</span><span class="sxs-lookup"><span data-stu-id="72d10-108">CA1700: Do not name enum values 'Reserved'</span></span>](ca1700.md)|<span data-ttu-id="72d10-109">這項規則假設名稱中包含 "reserved" 的列舉成員目前並未使用，但是在未來版本會是重新命名或移除的替代符號 (Placeholder)。</span><span class="sxs-lookup"><span data-stu-id="72d10-109">This rule assumes that an enumeration member that has a name that contains "reserved" is not currently used but is a placeholder to be renamed or removed in a future version.</span></span> <span data-ttu-id="72d10-110">重新命名或移除成員是中斷變更。</span><span class="sxs-lookup"><span data-stu-id="72d10-110">Renaming or removing a member is a breaking change.</span></span>|
|[<span data-ttu-id="72d10-111">CA1707:識別項名稱不應該包含底線</span><span class="sxs-lookup"><span data-stu-id="72d10-111">CA1707: Identifiers should not contain underscores</span></span>](ca1707.md)|<span data-ttu-id="72d10-112">根據慣例，識別項名稱不包含底線 (_) 字元。</span><span class="sxs-lookup"><span data-stu-id="72d10-112">By convention, identifier names do not contain the underscore (_) character.</span></span> <span data-ttu-id="72d10-113">此規則會檢查命名空間、類型、成員和參數。</span><span class="sxs-lookup"><span data-stu-id="72d10-113">This rule checks namespaces, types, members, and parameters.</span></span>|
|[<span data-ttu-id="72d10-114">CA1708:識別項名稱不應該只靠大小寫區別</span><span class="sxs-lookup"><span data-stu-id="72d10-114">CA1708: Identifiers should differ by more than case</span></span>](ca1708.md)|<span data-ttu-id="72d10-115">因為以通用語言執行平台為目標的語言不需要區分大小寫，因此，命名空間、類型、成員和參數的識別項不能只有大小寫的不同。</span><span class="sxs-lookup"><span data-stu-id="72d10-115">Identifiers for namespaces, types, members, and parameters cannot differ only by case because languages that target the common language runtime are not required to be case-sensitive.</span></span>|
|[<span data-ttu-id="72d10-116">CA1710:識別項應該使用正確的後置字元</span><span class="sxs-lookup"><span data-stu-id="72d10-116">CA1710: Identifiers should have correct suffix</span></span>](ca1710.md)|<span data-ttu-id="72d10-117">依照慣例，擴充特定基底類型或實作為某些介面的類型名稱，或是從這些類型衍生的類型，其後綴會與基底類型或介面相關聯。</span><span class="sxs-lookup"><span data-stu-id="72d10-117">By convention, the names of types that extend certain base types or that implement certain interfaces, or types derived from these types, have a suffix that is associated with the base type or interface.</span></span>|
|[<span data-ttu-id="72d10-118">CA1711:識別項名稱不應該使用不正確的後置字元</span><span class="sxs-lookup"><span data-stu-id="72d10-118">CA1711: Identifiers should not have incorrect suffix</span></span>](ca1711.md)|<span data-ttu-id="72d10-119">依照慣例，只有擴充特定基底類型或實作特定介面的類型名稱，或是從這些類型衍生的類型名稱，應以特定保留的後置字元結尾。</span><span class="sxs-lookup"><span data-stu-id="72d10-119">By convention, only the names of types that extend certain base types or that implement certain interfaces, or types that are derived from these types, should end with specific reserved suffixes.</span></span> <span data-ttu-id="72d10-120">其他類型名稱不得使用這些保留的後置字元。</span><span class="sxs-lookup"><span data-stu-id="72d10-120">Other type names should not use these reserved suffixes.</span></span>|
|[<span data-ttu-id="72d10-121">CA1712:不要使用類型名稱作為列舉值的前置字元</span><span class="sxs-lookup"><span data-stu-id="72d10-121">CA1712: Do not prefix enum values with type name</span></span>](ca1712.md)|<span data-ttu-id="72d10-122">列舉成員的名稱不會加上類型名稱的前置詞，因為開發工具預期會提供類型資訊。</span><span class="sxs-lookup"><span data-stu-id="72d10-122">Names of enumeration members are not prefixed with the type name because type information is expected to be provided by development tools.</span></span>|
|[<span data-ttu-id="72d10-123">CA1713:事件不應該有 before 或 after 前置字元</span><span class="sxs-lookup"><span data-stu-id="72d10-123">CA1713: Events should not have before or after prefix</span></span>](ca1713.md)|<span data-ttu-id="72d10-124">事件的名稱會以 "Before" 或 "After" 為開頭。</span><span class="sxs-lookup"><span data-stu-id="72d10-124">The name of an event starts with "Before" or "After".</span></span> <span data-ttu-id="72d10-125">若要命名在特定序列 (Sequence) 中引發的相關事件，請使用現在式或過去式表示動作序列相對的位置。</span><span class="sxs-lookup"><span data-stu-id="72d10-125">To name related events that are raised in a specific sequence, use the present or past tense to indicate the relative position in the sequence of actions.</span></span>|
|[<span data-ttu-id="72d10-126">CA1714:旗標列舉應該使用複數名稱</span><span class="sxs-lookup"><span data-stu-id="72d10-126">CA1714: Flags enums should have plural names</span></span>](ca1714.md)|<span data-ttu-id="72d10-127">公用列舉具有 FlagsAttribute 屬性，而且其名稱結尾不是 "s"。</span><span class="sxs-lookup"><span data-stu-id="72d10-127">A public enumeration has the System.FlagsAttribute attribute and its name does not end in "s".</span></span> <span data-ttu-id="72d10-128">標記為 FlagsAttribute 的類型具有複數名稱，因為屬性工作表示可以指定多個值。</span><span class="sxs-lookup"><span data-stu-id="72d10-128">Types that are marked with FlagsAttribute have names that are plural because the attribute indicates that more than one value can be specified.</span></span>|
|[<span data-ttu-id="72d10-129">CA1715:識別項名稱應該使用正確的前置字元</span><span class="sxs-lookup"><span data-stu-id="72d10-129">CA1715: Identifiers should have correct prefix</span></span>](ca1715.md)|<span data-ttu-id="72d10-130">外部可見介面的名稱不是以大寫 "I" 開頭。</span><span class="sxs-lookup"><span data-stu-id="72d10-130">The name of an externally visible interface does not start with a capital "I".</span></span>  <span data-ttu-id="72d10-131">外部可見類型或方法上泛型型別參數的名稱不是以大寫 "T" 開頭。</span><span class="sxs-lookup"><span data-stu-id="72d10-131">The name of a generic type parameter on an externally visible type or method does not start with a capital "T".</span></span>|
|[<span data-ttu-id="72d10-132">CA1716:識別項名稱不應該和關鍵字相符</span><span class="sxs-lookup"><span data-stu-id="72d10-132">CA1716: Identifiers should not match keywords</span></span>](ca1716.md)|<span data-ttu-id="72d10-133">命名空間 (Namespace) 名稱或類型名稱符合程式語言中的保留關鍵字。</span><span class="sxs-lookup"><span data-stu-id="72d10-133">A namespace name or a type name matches a reserved keyword in a programming language.</span></span> <span data-ttu-id="72d10-134">命名空間和類型的識別項不應該符合語言所定義的關鍵字，而這些語言的目標為 Common Language Runtime。</span><span class="sxs-lookup"><span data-stu-id="72d10-134">Identifiers for namespaces and types should not match keywords that are defined by languages that target the common language runtime.</span></span>|
|[<span data-ttu-id="72d10-135">CA1717:只有 FlagsAttribute 列舉應該使用複數名稱</span><span class="sxs-lookup"><span data-stu-id="72d10-135">CA1717: Only FlagsAttribute enums should have plural names</span></span>](ca1717.md)|<span data-ttu-id="72d10-136">依照命名規範的要求，列舉的複數名稱代表可以同時指定多個列舉值。</span><span class="sxs-lookup"><span data-stu-id="72d10-136">Naming conventions dictate that a plural name for an enumeration indicates that more than one value of the enumeration can be specified at the same time.</span></span>|
|[<span data-ttu-id="72d10-137">CA1720:識別項名稱不應該包含類型名稱</span><span class="sxs-lookup"><span data-stu-id="72d10-137">CA1720: Identifiers should not contain type names</span></span>](ca1720.md)|<span data-ttu-id="72d10-138">外部可見成員中的參數名稱包含資料類型名稱，或外部可見成員的名稱包含語言特定的資料類型名稱。</span><span class="sxs-lookup"><span data-stu-id="72d10-138">The name of a parameter in an externally visible member contains a data type name, or the name of an externally visible member contains a language-specific data type name.</span></span>|
|[<span data-ttu-id="72d10-139">CA1721:屬性名稱不應該和其中有 get 的方法名稱相符</span><span class="sxs-lookup"><span data-stu-id="72d10-139">CA1721: Property names should not match get methods</span></span>](ca1721.md)|<span data-ttu-id="72d10-140">公用或保護之成員的名稱是以 "Get" 開頭，否則需符合公用或保護之屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="72d10-140">The name of a public or protected member starts with "Get" and otherwise matches the name of a public or protected property.</span></span> <span data-ttu-id="72d10-141">"Get" 方法和屬性的名稱應該清楚區別其功能。</span><span class="sxs-lookup"><span data-stu-id="72d10-141">"Get" methods and properties should have names that clearly distinguish their function.</span></span>|
|[<span data-ttu-id="72d10-142">CA1724:類型名稱不應該和命名空間相符</span><span class="sxs-lookup"><span data-stu-id="72d10-142">CA1724: Type Names Should Not Match Namespaces</span></span>](ca1724.md)|<span data-ttu-id="72d10-143">類型名稱不應與 .NET 命名空間的名稱相符。</span><span class="sxs-lookup"><span data-stu-id="72d10-143">Type names should not match the names of .NET namespaces.</span></span> <span data-ttu-id="72d10-144">違規此規則可能會降低程式庫的可用性。</span><span class="sxs-lookup"><span data-stu-id="72d10-144">Violation of this rule can reduce the usability of the library.</span></span>|
|[<span data-ttu-id="72d10-145">CA1725:參數名稱應該符合基底類型的宣告</span><span class="sxs-lookup"><span data-stu-id="72d10-145">CA1725: Parameter names should match base declaration</span></span>](ca1725.md)|<span data-ttu-id="72d10-146">在覆寫階層架構中一致的參數命名方式，會增加方法覆寫的可用性。</span><span class="sxs-lookup"><span data-stu-id="72d10-146">Consistent naming of parameters in an override hierarchy increases the usability of the method overrides.</span></span> <span data-ttu-id="72d10-147">與基底宣告中的名稱不同之衍生方法中的參數名稱，可能會造成方法為基底方法的覆寫或為方法的新多載而混淆。</span><span class="sxs-lookup"><span data-stu-id="72d10-147">A parameter name in a derived method that differs from the name in the base declaration can cause confusion about whether the method is an override of the base method or a new overload of the method.</span></span>|
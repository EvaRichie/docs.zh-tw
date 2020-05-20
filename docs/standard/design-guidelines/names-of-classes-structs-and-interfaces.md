---
title: 類別、結構和介面的名稱
description: 使用這些指導方針來命名類別、結構和介面，作為設計延伸和互動 .NET 程式庫的指引的一部分。
ms.date: 10/22/2008
helpviewer_keywords:
- type names, guidelines
- classes [.NET Framework], names
- enumerations [.NET Framework], names
- names [.NET Framework], interfaces
- common type names
- names [.NET Framework], type names
- names [.NET Framework], classes
- interfaces [.NET Framework], names
- generic type parameters
ms.assetid: 87a4b0da-ed64-43b1-ac43-968576c444ce
ms.openlocfilehash: e7eee414c5bf5c69f63543ef240e50a4d2d948a3
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419079"
---
# <a name="names-of-classes-structs-and-interfaces"></a><span data-ttu-id="06ce2-103">類別、結構和介面的名稱</span><span class="sxs-lookup"><span data-stu-id="06ce2-103">Names of Classes, Structs, and Interfaces</span></span>
<span data-ttu-id="06ce2-104">後面的命名指導方針適用于一般類型命名。</span><span class="sxs-lookup"><span data-stu-id="06ce2-104">The naming guidelines that follow apply to general type naming.</span></span>

 <span data-ttu-id="06ce2-105">✔️使用 PascalCasing 來命名具有名詞或名詞片語的類別和結構。</span><span class="sxs-lookup"><span data-stu-id="06ce2-105">✔️ DO name classes and structs with nouns or noun phrases, using PascalCasing.</span></span>

 <span data-ttu-id="06ce2-106">這會區分方法中的型別名稱，其以動詞片語命名。</span><span class="sxs-lookup"><span data-stu-id="06ce2-106">This distinguishes type names from methods, which are named with verb phrases.</span></span>

 <span data-ttu-id="06ce2-107">✔️使用形容詞片語，或偶爾使用名詞或名詞片語來命名介面。</span><span class="sxs-lookup"><span data-stu-id="06ce2-107">✔️ DO name interfaces with adjective phrases, or occasionally with nouns or noun phrases.</span></span>

 <span data-ttu-id="06ce2-108">名詞和名詞片語應該很少使用，而且可能表示該類型應該是抽象類別，而不是介面。</span><span class="sxs-lookup"><span data-stu-id="06ce2-108">Nouns and noun phrases should be used rarely and they might indicate that the type should be an abstract class, and not an interface.</span></span>

 <span data-ttu-id="06ce2-109">❌不要為類別名稱提供前置詞（例如 "C"）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-109">❌ DO NOT give class names a prefix (e.g., "C").</span></span>

 <span data-ttu-id="06ce2-110">✔️考慮使用基類的名稱來結束衍生類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-110">✔️ CONSIDER ending the name of derived classes with the name of the base class.</span></span>

 <span data-ttu-id="06ce2-111">這是非常容易閱讀的，並且清楚地說明關聯性。</span><span class="sxs-lookup"><span data-stu-id="06ce2-111">This is very readable and explains the relationship clearly.</span></span> <span data-ttu-id="06ce2-112">在程式碼中的一些範例是： `ArgumentOutOfRangeException` ，這是一種 `Exception` 、和 `SerializableAttribute` ，這是一種類型 `Attribute` 。</span><span class="sxs-lookup"><span data-stu-id="06ce2-112">Some examples of this in code are: `ArgumentOutOfRangeException`, which is a kind of `Exception`, and `SerializableAttribute`, which is a kind of `Attribute`.</span></span> <span data-ttu-id="06ce2-113">不過，請務必在套用此指導方針時使用合理的判斷。例如， `Button` 類別是一種 `Control` 事件，但 `Control` 不會出現在其名稱中。</span><span class="sxs-lookup"><span data-stu-id="06ce2-113">However, it is important to use reasonable judgment in applying this guideline; for example, the `Button` class is a kind of `Control` event, although `Control` doesn’t appear in its name.</span></span>

 <span data-ttu-id="06ce2-114">✔️在介面名稱前面加上字母 I，表示該類型為介面。</span><span class="sxs-lookup"><span data-stu-id="06ce2-114">✔️ DO prefix interface names with the letter I, to indicate that the type is an interface.</span></span>

 <span data-ttu-id="06ce2-115">例如， `IComponent` （描述性名詞）、 `ICustomAttributeProvider` （名詞片語）和 `IPersistable` （形容詞）是適當的介面名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-115">For example, `IComponent` (descriptive noun), `ICustomAttributeProvider` (noun phrase), and `IPersistable` (adjective) are appropriate interface names.</span></span> <span data-ttu-id="06ce2-116">如同其他類型名稱，請避免使用縮寫。</span><span class="sxs-lookup"><span data-stu-id="06ce2-116">As with other type names, avoid abbreviations.</span></span>

 <span data-ttu-id="06ce2-117">當您定義類別–介面組（其中類別是介面的標準執行）時，✔️確實會確保介面名稱上的 "I" 前置詞只有名稱不同。</span><span class="sxs-lookup"><span data-stu-id="06ce2-117">✔️ DO ensure that the names differ only by the "I" prefix on the interface name when you are defining a class–interface pair where the class is a standard implementation of the interface.</span></span>

## <a name="names-of-generic-type-parameters"></a><span data-ttu-id="06ce2-118">泛型型別參數的名稱</span><span class="sxs-lookup"><span data-stu-id="06ce2-118">Names of Generic Type Parameters</span></span>
 <span data-ttu-id="06ce2-119">泛型已加入至 .NET Framework 2.0。</span><span class="sxs-lookup"><span data-stu-id="06ce2-119">Generics were added to .NET Framework 2.0.</span></span> <span data-ttu-id="06ce2-120">此功能引進了一種稱為「*型別參數*」的新識別碼。</span><span class="sxs-lookup"><span data-stu-id="06ce2-120">The feature introduced a new kind of identifier called *type parameter*.</span></span>

 <span data-ttu-id="06ce2-121">除非單一字母名稱完全一目了然，而且描述性名稱不會加上值，否則✔️ DO 名稱具有描述性名稱的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="06ce2-121">✔️ DO name generic type parameters with descriptive names unless a single-letter name is completely self-explanatory and a descriptive name would not add value.</span></span>

 <span data-ttu-id="06ce2-122">✔️請考慮使用 `T` 做為具有一個單字母類型參數之類型的類型參數名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-122">✔️ CONSIDER using `T` as the type parameter name for types with one single-letter type parameter.</span></span>

```csharp
public int IComparer<T> { ... }
public delegate bool Predicate<T>(T item);
public struct Nullable<T> where T:struct { ... }
```

 <span data-ttu-id="06ce2-123">✔️使用在描述性類型參數名稱前面加上 `T` 。</span><span class="sxs-lookup"><span data-stu-id="06ce2-123">✔️ DO prefix descriptive type parameter names with `T`.</span></span>

```csharp
public interface ISessionChannel<TSession> where TSession : ISession {
    TSession Session { get; }
}
```

 <span data-ttu-id="06ce2-124">✔️，請考慮在參數名稱中指出在類型參數上放置的條件約束。</span><span class="sxs-lookup"><span data-stu-id="06ce2-124">✔️ CONSIDER indicating constraints placed on a type parameter in the name of the parameter.</span></span>

 <span data-ttu-id="06ce2-125">例如，受條件約束的參數 `ISession` 可能會被呼叫 `TSession` 。</span><span class="sxs-lookup"><span data-stu-id="06ce2-125">For example, a parameter constrained to `ISession` might be called `TSession`.</span></span>

## <a name="names-of-common-types"></a><span data-ttu-id="06ce2-126">一般類型的名稱</span><span class="sxs-lookup"><span data-stu-id="06ce2-126">Names of Common Types</span></span>
 <span data-ttu-id="06ce2-127">✔️請遵循下表中所述的指導方針來命名衍生自的型別，或執行特定的 .NET Framework 類型。</span><span class="sxs-lookup"><span data-stu-id="06ce2-127">✔️ DO follow the guidelines described in the following table when naming types derived from or implementing certain .NET Framework types.</span></span>

|<span data-ttu-id="06ce2-128">基底類型</span><span class="sxs-lookup"><span data-stu-id="06ce2-128">Base Type</span></span>|<span data-ttu-id="06ce2-129">衍生/執行類型指導方針</span><span class="sxs-lookup"><span data-stu-id="06ce2-129">Derived/Implementing Type Guideline</span></span>|
|---------------|------------------------------------------|
|`System.Attribute`|<span data-ttu-id="06ce2-130">✔️請將尾碼 "Attribute" 新增至自訂屬性類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-130">✔️ DO add the suffix "Attribute" to names of custom attribute classes.</span></span>|
|`System.Delegate`|<span data-ttu-id="06ce2-131">✔️請將後置詞 "EventHandler" 新增至事件中所使用的委派名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-131">✔️ DO add the suffix "EventHandler" to names of delegates that are used in events.</span></span><br /><br /> <span data-ttu-id="06ce2-132">✔️請將後置詞「回呼」新增至委派的名稱，而非當做事件處理常式使用。</span><span class="sxs-lookup"><span data-stu-id="06ce2-132">✔️ DO add the suffix "Callback" to names of delegates other than those used as event handlers.</span></span><br /><br /> <span data-ttu-id="06ce2-133">❌請勿將後置詞「委派」新增至委派。</span><span class="sxs-lookup"><span data-stu-id="06ce2-133">❌ DO NOT add the suffix "Delegate" to a delegate.</span></span>|
|`System.EventArgs`|<span data-ttu-id="06ce2-134">✔️新增尾碼 "EventArgs"。</span><span class="sxs-lookup"><span data-stu-id="06ce2-134">✔️ DO add the suffix "EventArgs."</span></span>|
|`System.Enum`|<span data-ttu-id="06ce2-135">❌請勿從這個類別衍生;請改用您的語言支援的關鍵字;例如，在 c # 中，使用 `enum` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="06ce2-135">❌ DO NOT derive from this class; use the keyword supported by your language instead; for example, in C#, use the `enum` keyword.</span></span><br /><br /> <span data-ttu-id="06ce2-136">❌請勿新增尾碼 "Enum" 或 "旗標"。</span><span class="sxs-lookup"><span data-stu-id="06ce2-136">❌ DO NOT add the suffix "Enum" or "Flag."</span></span>|
|`System.Exception`|<span data-ttu-id="06ce2-137">✔️新增尾碼 "Exception"。</span><span class="sxs-lookup"><span data-stu-id="06ce2-137">✔️ DO add the suffix "Exception."</span></span>|
|`IDictionary` <br /> `IDictionary<TKey,TValue>`|<span data-ttu-id="06ce2-138">✔️新增尾碼「字典」。</span><span class="sxs-lookup"><span data-stu-id="06ce2-138">✔️ DO add the suffix "Dictionary."</span></span> <span data-ttu-id="06ce2-139">請注意， `IDictionary` 是特定類型的集合，但這項指導方針優先于後面的較一般集合指導方針。</span><span class="sxs-lookup"><span data-stu-id="06ce2-139">Note that `IDictionary` is a specific type of collection, but this guideline takes precedence over the more general collections guideline that follows.</span></span>|
|`IEnumerable` <br /> `ICollection` <br /> `IList` <br /> `IEnumerable<T>` <br /> `ICollection<T>` <br /> `IList<T>`|<span data-ttu-id="06ce2-140">✔️新增尾碼「集合」。</span><span class="sxs-lookup"><span data-stu-id="06ce2-140">✔️ DO add the suffix "Collection."</span></span>|
|`System.IO.Stream`|<span data-ttu-id="06ce2-141">✔️新增尾碼「串流」。</span><span class="sxs-lookup"><span data-stu-id="06ce2-141">✔️ DO add the suffix "Stream."</span></span>|
|`CodeAccessPermission IPermission`|<span data-ttu-id="06ce2-142">✔️新增尾碼「許可權」。</span><span class="sxs-lookup"><span data-stu-id="06ce2-142">✔️ DO add the suffix "Permission."</span></span>|

## <a name="naming-enumerations"></a><span data-ttu-id="06ce2-143">命名列舉</span><span class="sxs-lookup"><span data-stu-id="06ce2-143">Naming Enumerations</span></span>
 <span data-ttu-id="06ce2-144">列舉類型的名稱（也稱為列舉）通常應該遵循標準類型命名規則（PascalCasing 等等）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-144">Names of enumeration types (also called enums) in general should follow the standard type-naming rules (PascalCasing, etc.).</span></span> <span data-ttu-id="06ce2-145">不過，還有其他適用于列舉的指導方針。</span><span class="sxs-lookup"><span data-stu-id="06ce2-145">However, there are additional guidelines that apply specifically to enums.</span></span>

 <span data-ttu-id="06ce2-146">✔️請將單數類型名稱用於列舉，除非其值為位欄位。</span><span class="sxs-lookup"><span data-stu-id="06ce2-146">✔️ DO use a singular type name for an enumeration unless its values are bit fields.</span></span>

 <span data-ttu-id="06ce2-147">✔️確實將複數型別名稱用於具有位欄位做為值（也稱為 flags 列舉）的列舉。</span><span class="sxs-lookup"><span data-stu-id="06ce2-147">✔️ DO use a plural type name for an enumeration with bit fields as values, also called flags enum.</span></span>

 <span data-ttu-id="06ce2-148">❌請不要在列舉型別名稱中使用 "Enum" 尾碼。</span><span class="sxs-lookup"><span data-stu-id="06ce2-148">❌ DO NOT use an "Enum" suffix in enum type names.</span></span>

 <span data-ttu-id="06ce2-149">❌請不要在列舉型別名稱中使用「旗標」或「旗標」尾碼。</span><span class="sxs-lookup"><span data-stu-id="06ce2-149">❌ DO NOT use "Flag" or "Flags" suffixes in enum type names.</span></span>

 <span data-ttu-id="06ce2-150">❌請不要在列舉值名稱上使用前置詞（例如，"ad" 代表 ADO enum，"rtf" 用於豐富文字列舉等等）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-150">❌ DO NOT use a prefix on enumeration value names (e.g., "ad" for ADO enums, "rtf" for rich text enums, etc.).</span></span>

 <span data-ttu-id="06ce2-151">*部分©2005、2009 Microsoft Corporation。已保留擁有權限。*</span><span class="sxs-lookup"><span data-stu-id="06ce2-151">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="06ce2-152">獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 節錄。\*\*</span><span class="sxs-lookup"><span data-stu-id="06ce2-152">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="06ce2-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="06ce2-153">See also</span></span>

- [<span data-ttu-id="06ce2-154">架構設計方針</span><span class="sxs-lookup"><span data-stu-id="06ce2-154">Framework Design Guidelines</span></span>](../../../docs/standard/design-guidelines/index.md)
- [<span data-ttu-id="06ce2-155">命名方針</span><span class="sxs-lookup"><span data-stu-id="06ce2-155">Naming Guidelines</span></span>](../../../docs/standard/design-guidelines/naming-guidelines.md)

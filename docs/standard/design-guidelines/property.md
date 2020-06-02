---
title: 屬性設計
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, properties
- properties [.NET Framework], design guidelines
ms.assetid: 127cbc0c-cbed-48fd-9c89-7c5d4f98f163
ms.openlocfilehash: c49b42ab369ace582c76d7f326da309415e8c45b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291938"
---
# <a name="property-design"></a><span data-ttu-id="aad2a-102">屬性設計</span><span class="sxs-lookup"><span data-stu-id="aad2a-102">Property Design</span></span>
<span data-ttu-id="aad2a-103">雖然屬性的技術與方法非常類似，但它們在使用案例方面的差異很大。</span><span class="sxs-lookup"><span data-stu-id="aad2a-103">Although properties are technically very similar to methods, they are quite different in terms of their usage scenarios.</span></span> <span data-ttu-id="aad2a-104">它們應該會視為智慧型欄位。</span><span class="sxs-lookup"><span data-stu-id="aad2a-104">They should be seen as smart fields.</span></span> <span data-ttu-id="aad2a-105">它們具有欄位的呼叫語法，以及方法的彈性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-105">They have the calling syntax of fields, and the flexibility of methods.</span></span>

 <span data-ttu-id="aad2a-106">如果呼叫端應該無法變更屬性的值，✔️執行 [建立僅限取得] 屬性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-106">✔️ DO create get-only properties if the caller should not be able to change the value of the property.</span></span>

 <span data-ttu-id="aad2a-107">請記住，如果屬性的型別是可變動的參考型別，即使屬性是 get only，屬性值也可以變更。</span><span class="sxs-lookup"><span data-stu-id="aad2a-107">Keep in mind that if the type of the property is a mutable reference type, the property value can be changed even if the property is get-only.</span></span>

 <span data-ttu-id="aad2a-108">❌請不要提供僅限 set 屬性或屬性，其 setter 的存取範圍高於 getter。</span><span class="sxs-lookup"><span data-stu-id="aad2a-108">❌ DO NOT provide set-only properties or properties with the setter having broader accessibility than the getter.</span></span>

 <span data-ttu-id="aad2a-109">例如，請勿使用具有公用 setter 和 protected getter 的屬性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-109">For example, do not use properties with a public setter and a protected getter.</span></span>

 <span data-ttu-id="aad2a-110">如果無法提供屬性 getter，請改為將此功能當做方法來執行。</span><span class="sxs-lookup"><span data-stu-id="aad2a-110">If the property getter cannot be provided, implement the functionality as a method instead.</span></span> <span data-ttu-id="aad2a-111">考慮使用來啟動方法名稱 `Set` ，並遵循您所命名的屬性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-111">Consider starting the method name with `Set` and follow with what you would have named the property.</span></span> <span data-ttu-id="aad2a-112">例如， <xref:System.AppDomain> 有一個稱為的方法， `SetCachePath` 而不是具有稱為的僅限 set 屬性 `CachePath` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-112">For example, <xref:System.AppDomain> has a method called `SetCachePath` instead of having a set-only property called `CachePath`.</span></span>

 <span data-ttu-id="aad2a-113">✔️確實為所有屬性提供合理的預設值，確保預設值不會導致安全性漏洞或驗證效率不佳的程式碼。</span><span class="sxs-lookup"><span data-stu-id="aad2a-113">✔️ DO provide sensible default values for all properties, ensuring that the defaults do not result in a security hole or terribly inefficient code.</span></span>

 <span data-ttu-id="aad2a-114">✔️允許以任何順序設定屬性，即使這會導致物件的暫時無效狀態。</span><span class="sxs-lookup"><span data-stu-id="aad2a-114">✔️ DO allow properties to be set in any order even if this results in a temporary invalid state of the object.</span></span>

 <span data-ttu-id="aad2a-115">兩個或多個屬性通常會相互關聯，因為相同物件上的其他屬性值可能會使某個屬性的某些值無效。</span><span class="sxs-lookup"><span data-stu-id="aad2a-115">It is common for two or more properties to be interrelated to a point where some values of one property might be invalid given the values of other properties on the same object.</span></span> <span data-ttu-id="aad2a-116">在這種情況下，從無效狀態產生的例外狀況應該會延後，直到物件實際使用相互關聯的屬性為止。</span><span class="sxs-lookup"><span data-stu-id="aad2a-116">In such cases, exceptions resulting from the invalid state should be postponed until the interrelated properties are actually used together by the object.</span></span>

 <span data-ttu-id="aad2a-117">如果屬性 setter 擲回例外狀況，✔️確實保留先前的值。</span><span class="sxs-lookup"><span data-stu-id="aad2a-117">✔️ DO preserve the previous value if a property setter throws an exception.</span></span>

 <span data-ttu-id="aad2a-118">❌避免從屬性 getter 擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="aad2a-118">❌ AVOID throwing exceptions from property getters.</span></span>

 <span data-ttu-id="aad2a-119">屬性 getter 應該是簡單的作業，而且不應該有任何前置條件。</span><span class="sxs-lookup"><span data-stu-id="aad2a-119">Property getters should be simple operations and should not have any preconditions.</span></span> <span data-ttu-id="aad2a-120">如果 getter 可能會擲回例外狀況，則可能會重新設計為方法。</span><span class="sxs-lookup"><span data-stu-id="aad2a-120">If a getter can throw an exception, it should probably be redesigned to be a method.</span></span> <span data-ttu-id="aad2a-121">請注意，此規則不適用於索引子，因為驗證引數會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="aad2a-121">Notice that this rule does not apply to indexers, where we do expect exceptions as a result of validating the arguments.</span></span>

### <a name="indexed-property-design"></a><span data-ttu-id="aad2a-122">索引屬性設計</span><span class="sxs-lookup"><span data-stu-id="aad2a-122">Indexed Property Design</span></span>
 <span data-ttu-id="aad2a-123">索引屬性是特殊的屬性，可以具有參數，而且可以使用類似于陣列索引編制的特殊語法來呼叫。</span><span class="sxs-lookup"><span data-stu-id="aad2a-123">An indexed property is a special property that can have parameters and can be called with special syntax similar to array indexing.</span></span>

 <span data-ttu-id="aad2a-124">索引屬性通常稱為索引子。</span><span class="sxs-lookup"><span data-stu-id="aad2a-124">Indexed properties are commonly referred to as indexers.</span></span> <span data-ttu-id="aad2a-125">索引子只能用於提供邏輯集合中專案存取權的 Api。</span><span class="sxs-lookup"><span data-stu-id="aad2a-125">Indexers should be used only in APIs that provide access to items in a logical collection.</span></span> <span data-ttu-id="aad2a-126">例如，字串是字元的集合，而上的索引子 <xref:System.String?displayProperty=nameWithType> 已加入來存取其字元。</span><span class="sxs-lookup"><span data-stu-id="aad2a-126">For example, a string is a collection of characters, and the indexer on <xref:System.String?displayProperty=nameWithType> was added to access its characters.</span></span>

 <span data-ttu-id="aad2a-127">✔️考慮使用索引子來提供內部陣列中所儲存之資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="aad2a-127">✔️ CONSIDER using indexers to provide access to data stored in an internal array.</span></span>

 <span data-ttu-id="aad2a-128">✔️請考慮在代表專案集合的類型上提供索引子。</span><span class="sxs-lookup"><span data-stu-id="aad2a-128">✔️ CONSIDER providing indexers on types representing collections of items.</span></span>

 <span data-ttu-id="aad2a-129">❌避免使用具有一個以上參數的索引屬性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-129">❌ AVOID using indexed properties with more than one parameter.</span></span>

 <span data-ttu-id="aad2a-130">如果設計需要多個參數，請重新考慮屬性是否真的代表邏輯集合的存取子。</span><span class="sxs-lookup"><span data-stu-id="aad2a-130">If the design requires multiple parameters, reconsider whether the property really represents an accessor to a logical collection.</span></span> <span data-ttu-id="aad2a-131">如果不存在，請改用方法。</span><span class="sxs-lookup"><span data-stu-id="aad2a-131">If it does not, use methods instead.</span></span> <span data-ttu-id="aad2a-132">請考慮使用或來啟動方法名稱 `Get` `Set` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-132">Consider starting the method name with `Get` or `Set`.</span></span>

 <span data-ttu-id="aad2a-133">❌請避免使用 <xref:System.Int32?displayProperty=nameWithType> 、 <xref:System.Int64?displayProperty=nameWithType> 、 <xref:System.String?displayProperty=nameWithType> 、或列舉以外參數類型的索引子 <xref:System.Object?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-133">❌ AVOID indexers with parameter types other than <xref:System.Int32?displayProperty=nameWithType>, <xref:System.Int64?displayProperty=nameWithType>, <xref:System.String?displayProperty=nameWithType>, <xref:System.Object?displayProperty=nameWithType>, or an enum.</span></span>

 <span data-ttu-id="aad2a-134">如果設計需要其他類型的參數，請強烈重新評估 API 是否真的代表邏輯集合的存取子。</span><span class="sxs-lookup"><span data-stu-id="aad2a-134">If the design requires other types of parameters, strongly reevaluate whether the API really represents an accessor to a logical collection.</span></span> <span data-ttu-id="aad2a-135">如果不存在，請使用方法。</span><span class="sxs-lookup"><span data-stu-id="aad2a-135">If it does not, use a method.</span></span> <span data-ttu-id="aad2a-136">請考慮使用或來啟動方法名稱 `Get` `Set` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-136">Consider starting the method name with `Get` or `Set`.</span></span>

 <span data-ttu-id="aad2a-137">✔️請使用索引屬性的名稱， `Item` 除非有明顯較好的名稱（例如，請參閱 <xref:System.String.Chars%2A> 上的屬性 `System.String` ）。</span><span class="sxs-lookup"><span data-stu-id="aad2a-137">✔️ DO use the name `Item` for indexed properties unless there is an obviously better name (e.g., see the <xref:System.String.Chars%2A> property on `System.String`).</span></span>

 <span data-ttu-id="aad2a-138">在 c # 中，索引子預設會命名為 Item。</span><span class="sxs-lookup"><span data-stu-id="aad2a-138">In C#, indexers are by default named Item.</span></span> <span data-ttu-id="aad2a-139"><xref:System.Runtime.CompilerServices.IndexerNameAttribute>可以用來自訂此名稱。</span><span class="sxs-lookup"><span data-stu-id="aad2a-139">The <xref:System.Runtime.CompilerServices.IndexerNameAttribute> can be used to customize this name.</span></span>

 <span data-ttu-id="aad2a-140">❌請勿同時提供具有相同語義的索引子和方法。</span><span class="sxs-lookup"><span data-stu-id="aad2a-140">❌ DO NOT provide both an indexer and methods that are semantically equivalent.</span></span>

 <span data-ttu-id="aad2a-141">❌請不要在一種類型中提供一個以上多載的索引子系列。</span><span class="sxs-lookup"><span data-stu-id="aad2a-141">❌ DO NOT provide more than one family of overloaded indexers in one type.</span></span>

 <span data-ttu-id="aad2a-142">這是由 c # 編譯器強制執行。</span><span class="sxs-lookup"><span data-stu-id="aad2a-142">This is enforced by the C# compiler.</span></span>

 <span data-ttu-id="aad2a-143">❌請勿使用非預設的索引屬性。</span><span class="sxs-lookup"><span data-stu-id="aad2a-143">❌ DO NOT use nondefault indexed properties.</span></span>

 <span data-ttu-id="aad2a-144">這是由 c # 編譯器強制執行。</span><span class="sxs-lookup"><span data-stu-id="aad2a-144">This is enforced by the C# compiler.</span></span>

### <a name="property-change-notification-events"></a><span data-ttu-id="aad2a-145">屬性變更通知事件</span><span class="sxs-lookup"><span data-stu-id="aad2a-145">Property Change Notification Events</span></span>
 <span data-ttu-id="aad2a-146">有時候，提供事件通知使用者屬性值的變更會很有用。</span><span class="sxs-lookup"><span data-stu-id="aad2a-146">Sometimes it is useful to provide an event notifying the user of changes in a property value.</span></span> <span data-ttu-id="aad2a-147">例如，會在 `System.Windows.Forms.Control` `TextChanged` 其屬性的值變更後引發事件 `Text` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-147">For example, `System.Windows.Forms.Control` raises a `TextChanged` event after the value of its `Text` property has changed.</span></span>

 <span data-ttu-id="aad2a-148">當高階 Api （通常是設計工具元件）中的屬性值被修改時，✔️考慮引發變更通知事件。</span><span class="sxs-lookup"><span data-stu-id="aad2a-148">✔️ CONSIDER raising change notification events when property values in high-level APIs (usually designer components) are modified.</span></span>

 <span data-ttu-id="aad2a-149">如果有一個很好的案例，讓使用者知道何時會變更物件的屬性，物件應該會引發屬性的變更通知事件。</span><span class="sxs-lookup"><span data-stu-id="aad2a-149">If there is a good scenario for a user to know when a property of an object is changing, the object should raise a change notification event for the property.</span></span>

 <span data-ttu-id="aad2a-150">不過，針對低層級 Api （例如基底類型或集合）引發這類事件的額外負荷不太值得。</span><span class="sxs-lookup"><span data-stu-id="aad2a-150">However, it is unlikely to be worth the overhead to raise such events for low-level APIs such as base types or collections.</span></span> <span data-ttu-id="aad2a-151">例如， <xref:System.Collections.Generic.List%601> 當新專案新增至清單且屬性變更時，不會引發這類事件 `Count` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-151">For example, <xref:System.Collections.Generic.List%601> would not raise such events when a new item is added to the list and the `Count` property changes.</span></span>

 <span data-ttu-id="aad2a-152">✔️考慮當屬性的值透過外部強制變更時，引發變更通知事件。</span><span class="sxs-lookup"><span data-stu-id="aad2a-152">✔️ CONSIDER raising change notification events when the value of a property changes via external forces.</span></span>

 <span data-ttu-id="aad2a-153">如果屬性值透過某些外部強制進行變更（透過在物件上呼叫方法以外的方式），則引發事件會向開發人員指出值已變更且已變更。</span><span class="sxs-lookup"><span data-stu-id="aad2a-153">If a property value changes via some external force (in a way other than by calling methods on the object), raise events indicate to the developer that the value is changing and has changed.</span></span> <span data-ttu-id="aad2a-154">文字方塊控制項的屬性就是一個很好的例子 `Text` 。</span><span class="sxs-lookup"><span data-stu-id="aad2a-154">A good example is the `Text` property of a text box control.</span></span> <span data-ttu-id="aad2a-155">當使用者在中輸入文字時 `TextBox` ，屬性值會自動變更。</span><span class="sxs-lookup"><span data-stu-id="aad2a-155">When the user types text in a `TextBox`, the property value automatically changes.</span></span>

 <span data-ttu-id="aad2a-156">*部分©2005、2009 Microsoft Corporation。已保留擁有權限。*</span><span class="sxs-lookup"><span data-stu-id="aad2a-156">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="aad2a-157">獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 節錄。\*\*</span><span class="sxs-lookup"><span data-stu-id="aad2a-157">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="aad2a-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="aad2a-158">See also</span></span>

- [<span data-ttu-id="aad2a-159">成員設計方針</span><span class="sxs-lookup"><span data-stu-id="aad2a-159">Member Design Guidelines</span></span>](member.md)
- [<span data-ttu-id="aad2a-160">架構設計方針</span><span class="sxs-lookup"><span data-stu-id="aad2a-160">Framework Design Guidelines</span></span>](index.md)

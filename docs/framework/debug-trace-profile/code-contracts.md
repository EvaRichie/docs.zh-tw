---
title: 程式碼合約
description: 探索程式碼合約，這種方法可讓您在 .NET 程式碼中指定前置條件、後置條件和物件不變數。
ms.date: 09/05/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Code contracts
ms.assetid: 84526045-496f-489d-8517-a258cf76f040
ms.openlocfilehash: 60f794373af75bd3f745c224e0a8c7a84192e4c4
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904139"
---
# <a name="code-contracts"></a><span data-ttu-id="09013-103">程式碼合約</span><span class="sxs-lookup"><span data-stu-id="09013-103">Code Contracts</span></span>

<span data-ttu-id="09013-104">程式碼合約可讓您指定程式碼中的前置條件、後置條件和物件非變異值。</span><span class="sxs-lookup"><span data-stu-id="09013-104">Code contracts provide a way to specify preconditions, postconditions, and object invariants in your code.</span></span> <span data-ttu-id="09013-105">前置條件是輸入方法或屬性時，必須符合的需求。</span><span class="sxs-lookup"><span data-stu-id="09013-105">Preconditions are requirements that must be met when entering a method or property.</span></span> <span data-ttu-id="09013-106">後置條件描述在方法或屬性程式碼結束時的期望。</span><span class="sxs-lookup"><span data-stu-id="09013-106">Postconditions describe expectations at the time the method or property code exits.</span></span> <span data-ttu-id="09013-107">物件非變異值描述針對處於良好狀態的類別，所預期的狀態。</span><span class="sxs-lookup"><span data-stu-id="09013-107">Object invariants describe the expected state for a class that is in a good state.</span></span>

<span data-ttu-id="09013-108">程式碼合約包含用來標示程式碼的類別、用來進行編譯時期分析的靜態分析器，以及執行階段分析器。</span><span class="sxs-lookup"><span data-stu-id="09013-108">Code contracts include classes for marking your code, a static analyzer for compile-time analysis, and a runtime analyzer.</span></span> <span data-ttu-id="09013-109">您可以在 <xref:System.Diagnostics.Contracts> 命名空間中找到程式碼合約的類別。</span><span class="sxs-lookup"><span data-stu-id="09013-109">The classes for code contracts can be found in the <xref:System.Diagnostics.Contracts> namespace.</span></span>

<span data-ttu-id="09013-110">程式碼合約的優點包括：</span><span class="sxs-lookup"><span data-stu-id="09013-110">The benefits of code contracts include the following:</span></span>

- <span data-ttu-id="09013-111">改良的測試：程式碼合約提供靜態合約驗證、執行階段檢查，以及文件產生。</span><span class="sxs-lookup"><span data-stu-id="09013-111">Improved testing: Code contracts provide static contract verification, runtime checking, and documentation generation.</span></span>

- <span data-ttu-id="09013-112">自動測試工具：您可以使用程式碼合約來篩選掉不符合前置條件的無意義的測試引數，以產生較有意義的單元測試。</span><span class="sxs-lookup"><span data-stu-id="09013-112">Automatic testing tools: You can use code contracts to generate more meaningful unit tests by filtering out meaningless test arguments that do not satisfy preconditions.</span></span>

- <span data-ttu-id="09013-113">靜態驗證：靜態檢查工具可以決定是否有任何合約違規，而不需要執行程式。</span><span class="sxs-lookup"><span data-stu-id="09013-113">Static verification: The static checker can decide whether there are any contract violations without running the program.</span></span> <span data-ttu-id="09013-114">它會檢查隱含的合約，例如 null 取值和陣列界限，以及明確的合約。</span><span class="sxs-lookup"><span data-stu-id="09013-114">It checks for implicit contracts, such as null dereferences and array bounds, and explicit contracts.</span></span>

- <span data-ttu-id="09013-115">參考文件：文件產生器會使用合約資訊來增強現有的 XML 文件檔案。</span><span class="sxs-lookup"><span data-stu-id="09013-115">Reference documentation: The documentation generator augments existing XML documentation files with contract information.</span></span> <span data-ttu-id="09013-116">此外，還有一些可搭配 [Sandcastle](https://github.com/EWSoftware/SHFB) 使用的樣式表，能夠讓產生的文件頁面具有合約區段。</span><span class="sxs-lookup"><span data-stu-id="09013-116">There are also style sheets that can be used with [Sandcastle](https://github.com/EWSoftware/SHFB) so that the generated documentation pages have contract sections.</span></span>

<span data-ttu-id="09013-117">所有 .NET Framework 語言都可以立即利用合約；您不必撰寫特殊的剖析器或編譯器。</span><span class="sxs-lookup"><span data-stu-id="09013-117">All .NET Framework languages can immediately take advantage of contracts; you do not have to write a special parser or compiler.</span></span> <span data-ttu-id="09013-118">Visual Studio 增益集可讓您指定所要執行之程式碼合約分析的層級。</span><span class="sxs-lookup"><span data-stu-id="09013-118">A Visual Studio add-in lets you specify the level of code contract analysis to be performed.</span></span> <span data-ttu-id="09013-119">分析器可以確認合約語式正確 (類型檢查和名稱解析)，並且可以產生 Microsoft 中繼語言 (MSIL) 格式合約的編譯形式。</span><span class="sxs-lookup"><span data-stu-id="09013-119">The analyzers can confirm that the contracts are well-formed (type checking and name resolution) and can produce a compiled form of the contracts in Microsoft intermediate language (MSIL) format.</span></span> <span data-ttu-id="09013-120">在 Visual Studio 中撰寫合約，可讓您利用該工具所提供的標準 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="09013-120">Authoring contracts in Visual Studio lets you take advantage of the standard IntelliSense provided by the tool.</span></span>

<span data-ttu-id="09013-121">合約類別中的大部分方法都是有條件地編譯；也就是說，唯有當您使用 `#define` 指示詞，來定義特殊符號 CONTRACTS_FULL 時，編譯器才會發出呼叫至這些方法。</span><span class="sxs-lookup"><span data-stu-id="09013-121">Most methods in the contract class are conditionally compiled; that is, the compiler emits calls to these methods only when  you define a special symbol, CONTRACTS_FULL, by using the `#define` directive.</span></span> <span data-ttu-id="09013-122">CONTRACTS_FULL 可讓您在程式碼中撰寫合約，而不需使用 `#ifdef` 指示詞；您可以產生不同的組建，有些有合約，有些則沒有。</span><span class="sxs-lookup"><span data-stu-id="09013-122">CONTRACTS_FULL lets you write contracts in your code without using `#ifdef` directives; you can produce different builds, some with contracts, and some without.</span></span>

<span data-ttu-id="09013-123">如需使用程式碼合約的工具和詳細指示，請參閱 Visual Studio marketplace 網站上的程式[代碼合約](https://marketplace.visualstudio.com/items?itemName=RiSEResearchinSoftwareEngineering.CodeContractsforNET)。</span><span class="sxs-lookup"><span data-stu-id="09013-123">For tools and detailed instructions for using code contracts, see [Code Contracts](https://marketplace.visualstudio.com/items?itemName=RiSEResearchinSoftwareEngineering.CodeContractsforNET) on the Visual Studio marketplace site.</span></span>

## <a name="preconditions"></a><span data-ttu-id="09013-124">先決條件</span><span class="sxs-lookup"><span data-stu-id="09013-124">Preconditions</span></span>

<span data-ttu-id="09013-125">您可以使用 <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=nameWithType> 方法來表示前置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-125">You can express preconditions by using the <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="09013-126">前置條件可指定叫用方法時的狀態。</span><span class="sxs-lookup"><span data-stu-id="09013-126">Preconditions specify state when a method is invoked.</span></span> <span data-ttu-id="09013-127">其通常是用來指定有效的參數值。</span><span class="sxs-lookup"><span data-stu-id="09013-127">They are generally used to specify valid parameter values.</span></span> <span data-ttu-id="09013-128">前置條件中提及之所有成員的可存取性，必須至少與方法本身相同，否則可能無法讓方法的所有呼叫端都了解該前置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-128">All members that are mentioned in preconditions must be at least as accessible as the method itself; otherwise, the precondition might not be understood by all callers of a method.</span></span> <span data-ttu-id="09013-129">該條件必須沒有副作用。</span><span class="sxs-lookup"><span data-stu-id="09013-129">The condition must have no side-effects.</span></span> <span data-ttu-id="09013-130">失敗前置條件的執行階段行為，取決於執行階段分析器。</span><span class="sxs-lookup"><span data-stu-id="09013-130">The run-time behavior of failed preconditions is determined by the runtime analyzer.</span></span>

<span data-ttu-id="09013-131">例如，下列前置條件表示 `x` 參數必須為非 null。</span><span class="sxs-lookup"><span data-stu-id="09013-131">For example, the following precondition expresses that parameter `x` must be non-null.</span></span>

```csharp
Contract.Requires(x != null);
```

<span data-ttu-id="09013-132">如果您的程式碼必須在前置條件失敗時擲回特定例外狀況，您可以使用 <xref:System.Diagnostics.Contracts.Contract.Requires%2A> 的泛型多載，如下所示。</span><span class="sxs-lookup"><span data-stu-id="09013-132">If your code must throw a particular exception on failure of a precondition, you can use the generic overload of <xref:System.Diagnostics.Contracts.Contract.Requires%2A> as follows.</span></span>

```csharp
Contract.Requires<ArgumentNullException>(x != null, "x");
```

### <a name="legacy-requires-statements"></a><span data-ttu-id="09013-133">舊版需要陳述式</span><span class="sxs-lookup"><span data-stu-id="09013-133">Legacy Requires Statements</span></span>

<span data-ttu-id="09013-134">大部分程式碼都包含 `if`-`then`-`throw` 程式碼形式的一些參數驗證。</span><span class="sxs-lookup"><span data-stu-id="09013-134">Most code contains some parameter validation in the form of `if`-`then`-`throw` code.</span></span> <span data-ttu-id="09013-135">在下列情況下，合約工具會將這些陳述式辨識為前置條件：</span><span class="sxs-lookup"><span data-stu-id="09013-135">The contract tools recognize these statements as preconditions in the following cases:</span></span>

- <span data-ttu-id="09013-136">這些陳述式會出現在方法中的任何其他陳述式之前。</span><span class="sxs-lookup"><span data-stu-id="09013-136">The statements appear before any other statements in a method.</span></span>

- <span data-ttu-id="09013-137">這一整組陳述式後面會接著明確的 <xref:System.Diagnostics.Contracts.Contract> 方法呼叫，例如呼叫 <xref:System.Diagnostics.Contracts.Contract.Requires%2A>、<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>、<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A> 或 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="09013-137">The entire set of such statements is followed by an explicit <xref:System.Diagnostics.Contracts.Contract> method call, such as a call to the <xref:System.Diagnostics.Contracts.Contract.Requires%2A>, <xref:System.Diagnostics.Contracts.Contract.Ensures%2A>, <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>, or <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> method.</span></span>

<span data-ttu-id="09013-138">當 `if`-`then`-`throw` 陳述式以這種形式出現時，工具會將其識別為舊版 `requires` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="09013-138">When `if`-`then`-`throw` statements appear in this form, the tools recognize them as legacy `requires` statements.</span></span> <span data-ttu-id="09013-139">如果 `if`-`then`-`throw` 序列後面沒有接著任何其他合約，則以 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A?displayProperty=nameWithType> 方法來結束程式碼。</span><span class="sxs-lookup"><span data-stu-id="09013-139">If no other contracts follow the `if`-`then`-`throw` sequence, end the code with the <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A?displayProperty=nameWithType> method.</span></span>

```csharp
if (x == null) throw new ...
Contract.EndContractBlock(); // All previous "if" checks are preconditions
```

<span data-ttu-id="09013-140">請注意，先前測試中的條件是否定的前置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-140">Note that the condition in the preceding test is a negated precondition.</span></span> <span data-ttu-id="09013-141">（實際的前置條件是 `x != null` 。）否定的前置條件具有高度限制：必須如前一個範例所示加以撰寫。也就是說，它不應包含任何 `else` 子句，而且子句的主體 `then` 必須是單一 `throw` 語句。</span><span class="sxs-lookup"><span data-stu-id="09013-141">(The actual precondition would be `x != null`.) A negated precondition is highly restricted: It must be written as shown in the previous example; that is, it should contain no `else` clauses, and the body of the `then` clause must be a single `throw` statement.</span></span> <span data-ttu-id="09013-142">`if` 測試受限於單純性和可視性規則 (請參閱[使用方式方針](#usage_guidelines))，但是 `throw` 運算式只受限於單純性規則。</span><span class="sxs-lookup"><span data-stu-id="09013-142">The `if` test is subject to both purity and visibility rules (see [Usage Guidelines](#usage_guidelines)), but the `throw` expression is subject only to purity rules.</span></span> <span data-ttu-id="09013-143">不過，所擲回之例外狀況的類型可視性，必須與發生合約的方法相同。</span><span class="sxs-lookup"><span data-stu-id="09013-143">However, the type of the exception thrown must be as visible as the method in which the contract occurs.</span></span>

## <a name="postconditions"></a><span data-ttu-id="09013-144">Postconditions</span><span class="sxs-lookup"><span data-stu-id="09013-144">Postconditions</span></span>

<span data-ttu-id="09013-145">後置條件是當方法終止時的方法狀態合約。</span><span class="sxs-lookup"><span data-stu-id="09013-145">Postconditions are contracts for the state of a method when it terminates.</span></span> <span data-ttu-id="09013-146">在方法臨結束前，才會檢查後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-146">The postcondition is checked just before exiting a method.</span></span> <span data-ttu-id="09013-147">失敗後置條件的執行階段行為，取決於執行階段分析器。</span><span class="sxs-lookup"><span data-stu-id="09013-147">The run-time behavior of failed postconditions is determined by the runtime analyzer.</span></span>

<span data-ttu-id="09013-148">不同於前置條件，後置條件可能會參考可視性較低的成員。</span><span class="sxs-lookup"><span data-stu-id="09013-148">Unlike preconditions, postconditions may reference members with less visibility.</span></span> <span data-ttu-id="09013-149">用戶端可能無法使用私用狀態來了解或利用以後置條件來表示的一些資訊，但這不影響用戶端正確地使用方法的能力。</span><span class="sxs-lookup"><span data-stu-id="09013-149">A client may not be able to understand or make use of some of the information expressed by a postcondition using private state, but this does not affect the client's ability to use the method correctly.</span></span>

### <a name="standard-postconditions"></a><span data-ttu-id="09013-150">標準後置條件</span><span class="sxs-lookup"><span data-stu-id="09013-150">Standard Postconditions</span></span>

<span data-ttu-id="09013-151">您可以使用 <xref:System.Diagnostics.Contracts.Contract.Ensures%2A> 方法來表示後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-151">You can express standard postconditions by using the <xref:System.Diagnostics.Contracts.Contract.Ensures%2A> method.</span></span> <span data-ttu-id="09013-152">後置條件會表示方法正常終止時，必須為 `true` 的條件。</span><span class="sxs-lookup"><span data-stu-id="09013-152">Postconditions express a condition that must be `true` upon normal termination of the method.</span></span>

```csharp
Contract.Ensures(this.F > 0);
```

### <a name="exceptional-postconditions"></a><span data-ttu-id="09013-153">例外後置條件</span><span class="sxs-lookup"><span data-stu-id="09013-153">Exceptional Postconditions</span></span>

<span data-ttu-id="09013-154">例外後置條件是當方法擲回特定例外狀況時，應為 `true` 的後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-154">Exceptional postconditions are postconditions that should be `true` when a particular exception is thrown by a method.</span></span> <span data-ttu-id="09013-155">您可以使用 <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A?displayProperty=nameWithType> 方法來指定這些後置條件，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="09013-155">You can specify these postconditions by using the <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A?displayProperty=nameWithType> method, as the following example shows.</span></span>

```csharp
Contract.EnsuresOnThrow<T>(this.F > 0);
```

<span data-ttu-id="09013-156">此引數是每當擲回的例外狀況是 `T` 的子類型時，必須為 `true` 的條件。</span><span class="sxs-lookup"><span data-stu-id="09013-156">The argument is the condition that must be `true` whenever an exception that is a subtype of `T` is thrown.</span></span>

<span data-ttu-id="09013-157">有些例外狀況類型很難用在例外後置條件中。</span><span class="sxs-lookup"><span data-stu-id="09013-157">There are some exception types that are difficult to use in an exceptional postcondition.</span></span> <span data-ttu-id="09013-158">例如，將類型 <xref:System.Exception> 用於 `T` 時，無論擲回的例外狀況類型為何，即使是堆疊溢位或其他無法控制的例外狀況，該方法都必須保證此條件。</span><span class="sxs-lookup"><span data-stu-id="09013-158">For example, using the type <xref:System.Exception> for `T` requires the method to guarantee the condition regardless of the type of exception that is thrown, even if it is a stack overflow or other impossible-to-control exception.</span></span> <span data-ttu-id="09013-159">例外後置條件應該只限用於呼叫成員時，可能會擲回的特定例外狀況；例如，針對 <xref:System.TimeZoneInfo> 方法呼叫擲回 <xref:System.InvalidTimeZoneException> 時。</span><span class="sxs-lookup"><span data-stu-id="09013-159">You should use exceptional postconditions only for specific exceptions that might be thrown when a member is called, for example, when an <xref:System.InvalidTimeZoneException> is thrown for a <xref:System.TimeZoneInfo> method call.</span></span>

### <a name="special-postconditions"></a><span data-ttu-id="09013-160">特殊後置條件</span><span class="sxs-lookup"><span data-stu-id="09013-160">Special Postconditions</span></span>

<span data-ttu-id="09013-161">下列方法僅限用於後置條件中：</span><span class="sxs-lookup"><span data-stu-id="09013-161">The following methods may be used only within postconditions:</span></span>

- <span data-ttu-id="09013-162">若要參考後置條件中的方法傳回值，您可以使用 `Contract.Result<T>()` 運算式，其中 `T` 要取代為方法的傳回類型。</span><span class="sxs-lookup"><span data-stu-id="09013-162">You can refer to method return values in postconditions by using the expression `Contract.Result<T>()`, where `T` is replaced by the return type of the method.</span></span> <span data-ttu-id="09013-163">當編譯器無法推斷類型時，您必須明確地提供類型。</span><span class="sxs-lookup"><span data-stu-id="09013-163">When the compiler is unable to infer the type, you must explicitly provide it.</span></span> <span data-ttu-id="09013-164">例如，C# 編譯器無法推斷沒有採用任何引數之方法的類型，因此需要下列後置條件：`Contract.Ensures(0 <Contract.Result<int>())` 傳回類型為 `void` 的方法，不能參考其後置條件中的 `Contract.Result<T>()`。</span><span class="sxs-lookup"><span data-stu-id="09013-164">For example, the C# compiler is unable to infer types for methods that do not take any arguments, so it requires the following postcondition: `Contract.Ensures(0 <Contract.Result<int>())` Methods with a return type of `void` cannot refer to `Contract.Result<T>()` in their postconditions.</span></span>

- <span data-ttu-id="09013-165">後置條件中的 prestate 值是指位於方法或屬性開頭之運算式的值。</span><span class="sxs-lookup"><span data-stu-id="09013-165">A prestate value in a postcondition refers to the value of an expression at the start of a method or property.</span></span> <span data-ttu-id="09013-166">它會使用 `Contract.OldValue<T>(e)` 運算式，其中 `T` 是 `e` 的類型。</span><span class="sxs-lookup"><span data-stu-id="09013-166">It uses the expression `Contract.OldValue<T>(e)`, where `T` is the type of `e`.</span></span> <span data-ttu-id="09013-167">只要編譯器能夠推斷其類型，您就可以省略泛型類型引數。</span><span class="sxs-lookup"><span data-stu-id="09013-167">You can omit the generic type argument whenever the compiler is able to infer its type.</span></span> <span data-ttu-id="09013-168">（例如，c # 編譯器一律會推斷類型，因為它接受引數）。有數個限制 `e` ，以及可能出現舊運算式的內容。</span><span class="sxs-lookup"><span data-stu-id="09013-168">(For example, the C# compiler always infers the type because it takes an argument.) There are several restrictions on what can occur in `e` and the contexts in which an old expression may appear.</span></span> <span data-ttu-id="09013-169">舊運算式不能包含另一個舊運算式。</span><span class="sxs-lookup"><span data-stu-id="09013-169">An old expression cannot contain another old expression.</span></span> <span data-ttu-id="09013-170">最重要的是，舊的運算式必須參考存在於方法前置條件狀態中的值。</span><span class="sxs-lookup"><span data-stu-id="09013-170">Most importantly, an old expression must refer to a value that existed in the method's precondition state.</span></span> <span data-ttu-id="09013-171">換句話說，只要方法的前置條件是 `true`，它就必須是可供評估的運算式。</span><span class="sxs-lookup"><span data-stu-id="09013-171">In other words, it must be an expression that can be evaluated as long as the method's precondition is `true`.</span></span> <span data-ttu-id="09013-172">以下是該規則的一些執行個體。</span><span class="sxs-lookup"><span data-stu-id="09013-172">Here are several instances of that rule.</span></span>

  - <span data-ttu-id="09013-173">該值必須存在於方法的前置條件狀態中。</span><span class="sxs-lookup"><span data-stu-id="09013-173">The value must exist in the method's precondition state.</span></span> <span data-ttu-id="09013-174">為了參考物件上的欄位，前置條件必須保證物件一律為非 null。</span><span class="sxs-lookup"><span data-stu-id="09013-174">In order to reference a field on an object, the preconditions must guarantee that the object is always non-null.</span></span>

  - <span data-ttu-id="09013-175">您不能在舊運算式中參考方法的傳回值：</span><span class="sxs-lookup"><span data-stu-id="09013-175">You cannot refer to the method's return value in an old expression:</span></span>

      ```csharp
      Contract.OldValue(Contract.Result<int>() + x) // ERROR
      ```

  - <span data-ttu-id="09013-176">您不能在舊運算式中參考 `out` 參數。</span><span class="sxs-lookup"><span data-stu-id="09013-176">You cannot refer to `out` parameters in an old expression.</span></span>

  - <span data-ttu-id="09013-177">如果數量詞的範圍取決於方法的傳回值，則舊運算式不能取決於數量詞的繫結變數中：</span><span class="sxs-lookup"><span data-stu-id="09013-177">An old expression cannot depend on the bound variable of a quantifier if the range of the quantifier depends on the return value of the method:</span></span>

      ```csharp
      Contract.ForAll(0, Contract.Result<int>(), i => Contract.OldValue(xs[i]) > 3); // ERROR
      ```

  - <span data-ttu-id="09013-178">舊運算式不能參考 <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> 或 <xref:System.Diagnostics.Contracts.Contract.Exists%2A> 呼叫中匿名委派的參數，除非是用來做為方法呼叫的索引子或引數：</span><span class="sxs-lookup"><span data-stu-id="09013-178">An old expression cannot refer to the parameter of the anonymous delegate in a <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> or <xref:System.Diagnostics.Contracts.Contract.Exists%2A> call unless it is used as an indexer or argument to a method call:</span></span>

      ```csharp
      Contract.ForAll(0, xs.Length, i => Contract.OldValue(xs[i]) > 3); // OK
      Contract.ForAll(0, xs.Length, i => Contract.OldValue(i) > 3); // ERROR
      ```

  - <span data-ttu-id="09013-179">如果舊運算式的值取決於匿名委派的任何參數，則舊運算式不能出現在匿名委派的主體中，除非匿名委派是 <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> 或 <xref:System.Diagnostics.Contracts.Contract.Exists%2A> 方法的引數：</span><span class="sxs-lookup"><span data-stu-id="09013-179">An old expression cannot occur in the body of an anonymous delegate if the value of the old expression depends on any of the parameters of the anonymous delegate, unless the anonymous delegate is an argument to the <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> or <xref:System.Diagnostics.Contracts.Contract.Exists%2A> method:</span></span>

      ```csharp
      Method(... (T t) => Contract.OldValue(... t ...) ...); // ERROR
      ```

  - <span data-ttu-id="09013-180">`Out` 參數出現問題，因為合約出現在方法的主體之前，而大部分編譯器不允許參考後置條件中的 `out` 參數。</span><span class="sxs-lookup"><span data-stu-id="09013-180">`Out` parameters present a problem because contracts appear before the body of the method, and most compilers do not allow references to `out` parameters in postconditions.</span></span> <span data-ttu-id="09013-181">為了解決這個問題，<xref:System.Diagnostics.Contracts.Contract> 類別提供了 <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> 方法，可允許以 `out` 參數為基礎的後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-181">To solve this problem, the <xref:System.Diagnostics.Contracts.Contract> class provides the <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> method, which allows a postcondition based on an `out` parameter.</span></span>

      ```csharp
      public void OutParam(out int x)
      {
          Contract.Ensures(Contract.ValueAtReturn(out x) == 3);
          x = 3;
      }
      ```

      <span data-ttu-id="09013-182">如同 <xref:System.Diagnostics.Contracts.Contract.OldValue%2A> 方法，只要編譯器能夠推斷其類型，您就可以省略泛型型別引數。</span><span class="sxs-lookup"><span data-stu-id="09013-182">As with the <xref:System.Diagnostics.Contracts.Contract.OldValue%2A> method, you can omit the generic type parameter whenever the compiler is able to infer its type.</span></span> <span data-ttu-id="09013-183">合約重寫器會將方法呼叫取代為 `out` 參數的值。</span><span class="sxs-lookup"><span data-stu-id="09013-183">The contract rewriter replaces the method call with the value of the `out` parameter.</span></span> <span data-ttu-id="09013-184"><xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> 方法只會出現在後置條件中。</span><span class="sxs-lookup"><span data-stu-id="09013-184">The <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> method may appear only in postconditions.</span></span> <span data-ttu-id="09013-185">方法的引數必須是 `out` 參數，或是結構 `out` 參數的欄位。</span><span class="sxs-lookup"><span data-stu-id="09013-185">The argument to the method must be an `out` parameter or a field of a structure `out` parameter.</span></span> <span data-ttu-id="09013-186">參考結構建構函式後置條件中的欄位時，後者也很有用。</span><span class="sxs-lookup"><span data-stu-id="09013-186">The latter is also useful when referring to fields in the postcondition of a structure constructor.</span></span>

      > [!NOTE]
      > <span data-ttu-id="09013-187">目前，程式碼合約分析工具不會檢查 `out` 參數是否正確初始化，並忽略其於後置條件中的相關記錄。</span><span class="sxs-lookup"><span data-stu-id="09013-187">Currently, the code contract analysis tools do not check whether `out` parameters are initialized properly and disregard their mention in the postcondition.</span></span> <span data-ttu-id="09013-188">因此，在上述範例中，如果合約之後的字行使用 `x` 的值，而不是指派整數給它，則編譯器不會發出正確的錯誤。</span><span class="sxs-lookup"><span data-stu-id="09013-188">Therefore, in the previous example, if the line after the contract had used the value of `x` instead of assigning an integer to it, a compiler would not issue the correct error.</span></span> <span data-ttu-id="09013-189">不過，在未定義 CONTRACTS_FULL 前置處理器符號的組建 (例如 asa 發行組建) 上，編譯器會發出錯誤。</span><span class="sxs-lookup"><span data-stu-id="09013-189">However, on a build where the CONTRACTS_FULL preprocessor symbol is not defined (such asa release build), the compiler will issue an error.</span></span>

## <a name="invariants"></a><span data-ttu-id="09013-190">非變異值</span><span class="sxs-lookup"><span data-stu-id="09013-190">Invariants</span></span>

<span data-ttu-id="09013-191">只要用戶端可以看到該物件，針對類別的每個執行個體，物件非變異值都是應該為 true 的條件。</span><span class="sxs-lookup"><span data-stu-id="09013-191">Object invariants are conditions that should be true for each instance of a class whenever that object is visible to a client.</span></span> <span data-ttu-id="09013-192">在其表示的條件下，物件會被視為正確。</span><span class="sxs-lookup"><span data-stu-id="09013-192">They express the conditions under which the object is considered to be correct.</span></span>

<span data-ttu-id="09013-193">非變異方法會標示 <xref:System.Diagnostics.Contracts.ContractInvariantMethodAttribute> 屬性，以供識別。</span><span class="sxs-lookup"><span data-stu-id="09013-193">The invariant methods are identified by being marked with the <xref:System.Diagnostics.Contracts.ContractInvariantMethodAttribute> attribute.</span></span> <span data-ttu-id="09013-194">非變異方法絕不能包含任何程式碼，但是對 <xref:System.Diagnostics.Contracts.Contract.Invariant%2A> 方法的一連串呼叫除外，其中每個呼叫都會指定一個個別非變異值，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="09013-194">The invariant methods must contain no code except for a sequence of calls to the <xref:System.Diagnostics.Contracts.Contract.Invariant%2A> method, each of which specifies an individual invariant, as shown in the following example.</span></span>

```csharp
[ContractInvariantMethod]
protected void ObjectInvariant ()
{
    Contract.Invariant(this.y >= 0);
    Contract.Invariant(this.x > this.y);
    ...
}
```

<span data-ttu-id="09013-195">CONTRACTS_FULL 前置處理器符號會有條件地定義非變異值。</span><span class="sxs-lookup"><span data-stu-id="09013-195">Invariants are conditionally defined by the CONTRACTS_FULL preprocessor symbol.</span></span> <span data-ttu-id="09013-196">在執行階段檢查期間，會在每個公用方法的結尾檢查非變異值。</span><span class="sxs-lookup"><span data-stu-id="09013-196">During run-time checking, invariants are checked at the end of each public method.</span></span> <span data-ttu-id="09013-197">如果非變異值提及在相同類別中的公用方法，則會停用通常在該公用方法結尾進行的非變異檢查。</span><span class="sxs-lookup"><span data-stu-id="09013-197">If an invariant mentions a public method in the same class, the invariant check that would normally happen at the end of that public method is disabled.</span></span> <span data-ttu-id="09013-198">此檢查反而只會發生在該類別最外層的方法呼叫結尾。</span><span class="sxs-lookup"><span data-stu-id="09013-198">Instead, the check occurs only at the end of the outermost method call to that class.</span></span> <span data-ttu-id="09013-199">如果因為呼叫另一個類別上的方法而重新輸入此類別，也會進行這項檢查。</span><span class="sxs-lookup"><span data-stu-id="09013-199">This also happens if the class is re-entered because of a call to a method on another class.</span></span> <span data-ttu-id="09013-200">不會針對物件完成項和執行檢查不變數 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="09013-200">Invariants are not checked for an object finalizer and an <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementation.</span></span>

<a name="usage_guidelines"></a>

## <a name="usage-guidelines"></a><span data-ttu-id="09013-201">使用方針</span><span class="sxs-lookup"><span data-stu-id="09013-201">Usage Guidelines</span></span>

### <a name="contract-ordering"></a><span data-ttu-id="09013-202">合約排序</span><span class="sxs-lookup"><span data-stu-id="09013-202">Contract Ordering</span></span>

<span data-ttu-id="09013-203">下表顯示當您撰寫方法合約時，應該使用的項目順序。</span><span class="sxs-lookup"><span data-stu-id="09013-203">The following table shows the order of elements you should use when you write method contracts.</span></span>

|`If-then-throw statements`|<span data-ttu-id="09013-204">回溯相容公用前置條件</span><span class="sxs-lookup"><span data-stu-id="09013-204">Backward-compatible public preconditions</span></span>|
|-|-|
|<xref:System.Diagnostics.Contracts.Contract.Requires%2A>|<span data-ttu-id="09013-205">所有公用前置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-205">All public preconditions.</span></span>|
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|<span data-ttu-id="09013-206">所有公用 (一般) 後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-206">All public (normal) postconditions.</span></span>|
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|<span data-ttu-id="09013-207">所有公用例外後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-207">All public exceptional postconditions.</span></span>|
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|<span data-ttu-id="09013-208">所有私用/內部 (一般) 後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-208">All private/internal (normal) postconditions.</span></span>|
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|<span data-ttu-id="09013-209">所有私用/內部 (一般) 例外後置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-209">All private/internal exceptional postconditions.</span></span>|
|<xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A>|<span data-ttu-id="09013-210">如果使用 `if`-`then`-`throw` 樣式前置條件，而沒有搭配任何其他合約，則呼叫 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A>，以指出所有先前的 if 檢查都是前置條件。</span><span class="sxs-lookup"><span data-stu-id="09013-210">If using `if`-`then`-`throw` style preconditions without any other contracts, place a call to <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> to indicate that all previous if checks are preconditions.</span></span>|

<a name="purity"></a>

### <a name="purity"></a><span data-ttu-id="09013-211">單純性</span><span class="sxs-lookup"><span data-stu-id="09013-211">Purity</span></span>

<span data-ttu-id="09013-212">在合約中呼叫的所有方法都必須都是單純的；也就是說，這些方法絕不能更新任何預先存在的狀態。</span><span class="sxs-lookup"><span data-stu-id="09013-212">All methods that are called within a contract must be pure; that is, they must not update any preexisting state.</span></span> <span data-ttu-id="09013-213">單純方法可以修改進入單純方法之後已建立的物件。</span><span class="sxs-lookup"><span data-stu-id="09013-213">A pure method is allowed to modify objects that have been created after entry into the pure method.</span></span>

<span data-ttu-id="09013-214">程式碼合約工具目前假設下列程式碼項目是單純的：</span><span class="sxs-lookup"><span data-stu-id="09013-214">Code contract tools currently assume that the following code elements are pure:</span></span>

- <span data-ttu-id="09013-215">標示 <xref:System.Diagnostics.Contracts.PureAttribute> 的方法。</span><span class="sxs-lookup"><span data-stu-id="09013-215">Methods that are marked with the <xref:System.Diagnostics.Contracts.PureAttribute>.</span></span>

- <span data-ttu-id="09013-216">標示 <xref:System.Diagnostics.Contracts.PureAttribute> 的類型 (此屬性會套用至所有類型的方法)。</span><span class="sxs-lookup"><span data-stu-id="09013-216">Types that are marked with the <xref:System.Diagnostics.Contracts.PureAttribute> (the attribute applies to all the type's methods).</span></span>

- <span data-ttu-id="09013-217">屬性 get 存取子。</span><span class="sxs-lookup"><span data-stu-id="09013-217">Property get accessors.</span></span>

- <span data-ttu-id="09013-218">運算子 (名稱開頭為 "op"，並且有一個或兩個參數以及非 void 傳回型別的靜態方法)。</span><span class="sxs-lookup"><span data-stu-id="09013-218">Operators (static methods whose names start with "op", and that have one or two parameters and a non-void return type).</span></span>

- <span data-ttu-id="09013-219">完整名稱開頭為 "System.Diagnostics.Contracts.Contract"、"System.String"、"System.IO.Path" 或 "System.Type" 的任何方法。</span><span class="sxs-lookup"><span data-stu-id="09013-219">Any method whose fully qualified name begins with "System.Diagnostics.Contracts.Contract", "System.String", "System.IO.Path", or "System.Type".</span></span>

- <span data-ttu-id="09013-220">任何叫用的委派，前提是委派類型本身是以 <xref:System.Diagnostics.Contracts.PureAttribute> 來屬性化。</span><span class="sxs-lookup"><span data-stu-id="09013-220">Any invoked delegate, provided that the delegate type itself is attributed with the <xref:System.Diagnostics.Contracts.PureAttribute>.</span></span> <span data-ttu-id="09013-221">委派類型 <xref:System.Predicate%601?displayProperty=nameWithType> 和 <xref:System.Comparison%601?displayProperty=nameWithType> 會被視為單純。</span><span class="sxs-lookup"><span data-stu-id="09013-221">The delegate types <xref:System.Predicate%601?displayProperty=nameWithType> and <xref:System.Comparison%601?displayProperty=nameWithType> are considered pure.</span></span>

<a name="visibility"></a>

### <a name="visibility"></a><span data-ttu-id="09013-222">可見性</span><span class="sxs-lookup"><span data-stu-id="09013-222">Visibility</span></span>

<span data-ttu-id="09013-223">合約中提及之所有成員的可視性，必須至少與其所在的方法相同。</span><span class="sxs-lookup"><span data-stu-id="09013-223">All members mentioned in a contract must be at least as visible as the method in which they appear.</span></span> <span data-ttu-id="09013-224">例如，針對公用方法，不能在前置條件中提及私用欄位；用戶端無法在呼叫該方法之前，先驗證這類合約。</span><span class="sxs-lookup"><span data-stu-id="09013-224">For example, a private field cannot be mentioned in a precondition for a public method; clients cannot validate such a contract before they call the method.</span></span> <span data-ttu-id="09013-225">不過，如果該欄位標示 <xref:System.Diagnostics.Contracts.ContractPublicPropertyNameAttribute>，則不受限於這些規則。</span><span class="sxs-lookup"><span data-stu-id="09013-225">However, if the field is marked with the <xref:System.Diagnostics.Contracts.ContractPublicPropertyNameAttribute>, it is exempt from these rules.</span></span>

## <a name="example"></a><span data-ttu-id="09013-226">範例</span><span class="sxs-lookup"><span data-stu-id="09013-226">Example</span></span>

<span data-ttu-id="09013-227">下列範例顯示程式碼合約的用法。</span><span class="sxs-lookup"><span data-stu-id="09013-227">The following example shows the use of code contracts.</span></span>

[!code-csharp[ContractExample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/contractexample/cs/program.cs#1)]
[!code-vb[ContractExample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/contractexample/vb/program.vb#1)]

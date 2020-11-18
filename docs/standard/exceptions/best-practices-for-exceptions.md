---
title: 例外狀況的最佳做法 - .NET
description: 瞭解例外狀況的最佳做法，例如使用 try/catch/finally、處理沒有例外狀況的一般情況，以及使用預先定義的 .NET 例外狀況類型。
ms.date: 12/05/2018
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- exceptions, best practices
ms.assetid: f06da765-235b-427a-bfb6-47cd219af539
ms.openlocfilehash: 815dcc81cf41465bffd1515d366a66ff558304fa
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828227"
---
# <a name="best-practices-for-exceptions"></a><span data-ttu-id="37b16-103">例外狀況的最佳做法</span><span class="sxs-lookup"><span data-stu-id="37b16-103">Best practices for exceptions</span></span>

<span data-ttu-id="37b16-104">設計良好的應用程式可處理例外狀況和錯誤，防止應用程式損毀。</span><span class="sxs-lookup"><span data-stu-id="37b16-104">A well-designed app handles exceptions and errors to prevent app crashes.</span></span> <span data-ttu-id="37b16-105">本節說明處理和建立例外狀況的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="37b16-105">This section describes best practices for handling and creating exceptions.</span></span>

## <a name="use-trycatchfinally-blocks-to-recover-from-errors-or-release-resources"></a><span data-ttu-id="37b16-106">使用 try/catch/finally 區塊從錯誤中復原或釋放資源</span><span class="sxs-lookup"><span data-stu-id="37b16-106">Use try/catch/finally blocks to recover from errors or release resources</span></span>

<span data-ttu-id="37b16-107">在可能產生例外狀況的程式碼周圍使用 `try`/`catch` 區塊，「且」您的程式碼即可從該例外狀況復原。</span><span class="sxs-lookup"><span data-stu-id="37b16-107">Use `try`/`catch` blocks around code that can potentially generate an exception ***and*** your code can recover from that exception.</span></span> <span data-ttu-id="37b16-108">在 `catch` 區塊中，一律將例外狀況從最具衍生性的排列到最不具衍生性。</span><span class="sxs-lookup"><span data-stu-id="37b16-108">In `catch` blocks, always order exceptions from the most derived to the least derived.</span></span> <span data-ttu-id="37b16-109">所有例外狀況皆衍生自 <xref:System.Exception>。</span><span class="sxs-lookup"><span data-stu-id="37b16-109">All exceptions derive from <xref:System.Exception>.</span></span> <span data-ttu-id="37b16-110">前有基底例外狀況類別 catch 子句的 catch 子句，不會處理最具衍生性的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-110">More derived exceptions are not handled by a catch clause that is preceded by a catch clause for a base exception class.</span></span> <span data-ttu-id="37b16-111">當您的程式碼無法從例外狀況復原時，請不要攔截該例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-111">When your code cannot recover from an exception, don't catch that exception.</span></span> <span data-ttu-id="37b16-112">如果可能，請啟用方法讓呼叫堆疊盡可能修復。</span><span class="sxs-lookup"><span data-stu-id="37b16-112">Enable methods further up the call stack to recover if possible.</span></span>

<span data-ttu-id="37b16-113">清除配置了 `using` 陳述式或 `finally` 區塊的資源。</span><span class="sxs-lookup"><span data-stu-id="37b16-113">Clean up resources allocated with either `using` statements, or `finally` blocks.</span></span> <span data-ttu-id="37b16-114">擲回例外狀況時，偏好使用 `using` 陳述式來自動清除資源。</span><span class="sxs-lookup"><span data-stu-id="37b16-114">Prefer `using` statements to automatically clean up resources when exceptions are thrown.</span></span> <span data-ttu-id="37b16-115">使用 `finally` 區塊清除不會實作 <xref:System.IDisposable> 的資源。</span><span class="sxs-lookup"><span data-stu-id="37b16-115">Use `finally` blocks to clean up resources that don't implement <xref:System.IDisposable>.</span></span> <span data-ttu-id="37b16-116">就算擲回例外狀況，也一律執行 `finally` 子句中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37b16-116">Code in a `finally` clause is almost always executed even when exceptions are thrown.</span></span>

## <a name="handle-common-conditions-without-throwing-exceptions"></a><span data-ttu-id="37b16-117">處理常見的狀況，而不擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="37b16-117">Handle common conditions without throwing exceptions</span></span>

<span data-ttu-id="37b16-118">針對可能發生但可能會觸發例外狀況的狀況，請考慮以避免例外狀況的方式來處理這些狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-118">For conditions that are likely to occur but might trigger an exception, consider handling them in a way that will avoid the exception.</span></span> <span data-ttu-id="37b16-119">例如，如果您嘗試關閉已關閉的連線，您會得到 `InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="37b16-119">For example, if you try to close a connection that is already closed, you'll get an `InvalidOperationException`.</span></span> <span data-ttu-id="37b16-120">您可以在嘗試關閉之前，使用 `if` 陳述式來檢查連線狀態，以避免此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-120">You can avoid that by using an `if` statement to check the connection state before trying to close it.</span></span>

[!code-cpp[Conceptual.Exception.Handling#2](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#2)]
[!code-csharp[Conceptual.Exception.Handling#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#2)]
[!code-vb[Conceptual.Exception.Handling#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#2)]

<span data-ttu-id="37b16-121">如果您沒有檢查連線狀態就關閉，您可能會攔截到 `InvalidOperationException` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-121">If you don't check connection state before closing, you can catch the `InvalidOperationException` exception.</span></span>

[!code-cpp[Conceptual.Exception.Handling#3](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#3)]
[!code-csharp[Conceptual.Exception.Handling#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#3)]
[!code-vb[Conceptual.Exception.Handling#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#3)]

<span data-ttu-id="37b16-122">選擇的方法取決於您預期事件會發生的頻率。</span><span class="sxs-lookup"><span data-stu-id="37b16-122">The method to choose depends on how often you expect the event to occur.</span></span>

- <span data-ttu-id="37b16-123">如果事件不常發生，也就是說事件真的是例外並且表示錯誤 (例如未預期的檔案結尾)，則使用例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="37b16-123">Use exception handling if the event doesn't occur very often, that is, if the event is truly exceptional and indicates an error (such as an unexpected end-of-file).</span></span> <span data-ttu-id="37b16-124">當您使用例外狀況處理時，在正常情況下會執行較少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37b16-124">When you use exception handling, less code is executed in normal conditions.</span></span>

- <span data-ttu-id="37b16-125">如果事件定期發生而且可視為正常執行的一部分，請檢查程式碼中是否有錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-125">Check for error conditions in code if the event happens routinely and could be considered part of normal execution.</span></span> <span data-ttu-id="37b16-126">當您檢查是否有常見的錯誤狀況時，因為避免例外狀況，所以會執行較少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37b16-126">When you check for common error conditions, less code is executed because you avoid exceptions.</span></span>

## <a name="design-classes-so-that-exceptions-can-be-avoided"></a><span data-ttu-id="37b16-127">設計類別以避免例外狀況</span><span class="sxs-lookup"><span data-stu-id="37b16-127">Design classes so that exceptions can be avoided</span></span>

<span data-ttu-id="37b16-128">類別可提供方法或屬性，讓您避免進行會觸發例外狀況的呼叫。</span><span class="sxs-lookup"><span data-stu-id="37b16-128">A class can provide methods or properties that enable you to avoid making a call that would trigger an exception.</span></span> <span data-ttu-id="37b16-129">例如，<xref:System.IO.FileStream> 類別會提供方法，協助判斷是否已經抵達檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="37b16-129">For example, a <xref:System.IO.FileStream> class provides methods that help determine whether the end of the file has been reached.</span></span> <span data-ttu-id="37b16-130">這些方法或屬性可用來避免萬一您讀取超過檔案結尾時，所擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-130">These can be used to avoid the exception that is thrown if you read past the end of the file.</span></span> <span data-ttu-id="37b16-131">下列範例示範如何讀取至檔案結尾，而不會觸發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-131">The following example shows how to read to the end of a file without triggering an exception.</span></span>

[!code-cpp[Conceptual.Exception.Handling#5](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#5)]
[!code-csharp[Conceptual.Exception.Handling#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#5)]
[!code-vb[Conceptual.Exception.Handling#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#5)]

<span data-ttu-id="37b16-132">另一個避免例外狀況的方法是針對很常見的錯誤案例傳回 Null (或預設值)，而不擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-132">Another way to avoid exceptions is to return null (or default) for extremely common error cases instead of throwing an exception.</span></span> <span data-ttu-id="37b16-133">相當普遍的錯誤案例可視為一般控制流程。</span><span class="sxs-lookup"><span data-stu-id="37b16-133">An extremely common error case can be considered normal flow of control.</span></span> <span data-ttu-id="37b16-134">針對這些案例傳回 Null (或預設值)，就能盡量降低對應用程式效能的影響。</span><span class="sxs-lookup"><span data-stu-id="37b16-134">By returning null (or default) in these cases, you minimize the performance impact to an app.</span></span>

<span data-ttu-id="37b16-135">針對實值型別，無論是要使用 `Nullable<T>` 還是預設值作為您的錯誤指標，都是必須為您的特定應用程式考慮的事項之一。</span><span class="sxs-lookup"><span data-stu-id="37b16-135">For value types, whether to use `Nullable<T>` or default as your error indicator is something to consider for your particular app.</span></span> <span data-ttu-id="37b16-136">透過使用 `Nullable<Guid>`，`default` 會成為 `null`，而非 `Guid.Empty`。</span><span class="sxs-lookup"><span data-stu-id="37b16-136">By using `Nullable<Guid>`, `default` becomes `null` instead of `Guid.Empty`.</span></span> <span data-ttu-id="37b16-137">有時候，當值存在或不存在時，新增 `Nullable<T>` 可讓您清楚了解。</span><span class="sxs-lookup"><span data-stu-id="37b16-137">Some times, adding `Nullable<T>` can make it clearer when a value is present or absent.</span></span> <span data-ttu-id="37b16-138">在其他時候，新增 `Nullable<T>` 會建立不必要的額外案例，而且會產生潛在的錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="37b16-138">Other times, adding `Nullable<T>` can create extra cases to check that aren't necessary, and only serve to create potential sources of errors.</span></span>

## <a name="throw-exceptions-instead-of-returning-an-error-code"></a><span data-ttu-id="37b16-139">擲回例外狀況來代替傳回錯誤碼</span><span class="sxs-lookup"><span data-stu-id="37b16-139">Throw exceptions instead of returning an error code</span></span>

<span data-ttu-id="37b16-140">例外狀況可確保不會發生未通知失敗的情況，因為呼叫程式碼並不會檢查傳回碼。</span><span class="sxs-lookup"><span data-stu-id="37b16-140">Exceptions ensure that failures do not go unnoticed because calling code didn't check a return code.</span></span>

## <a name="use-the-predefined-net-exception-types"></a><span data-ttu-id="37b16-141">使用預先定義的 .NET 例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="37b16-141">Use the predefined .NET exception types</span></span>

<span data-ttu-id="37b16-142">只有在預先定義的類型不適用時，才引進新的例外狀況類別。</span><span class="sxs-lookup"><span data-stu-id="37b16-142">Introduce a new exception class only when a predefined one doesn't apply.</span></span> <span data-ttu-id="37b16-143">例如：</span><span class="sxs-lookup"><span data-stu-id="37b16-143">For example:</span></span>

- <span data-ttu-id="37b16-144">如果屬性集或方法呼叫對於物件的目前狀態而言並不適當，就會擲回 <xref:System.InvalidOperationException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-144">Throw an <xref:System.InvalidOperationException> exception if a property set or method call is not appropriate given the object's current state.</span></span>

- <span data-ttu-id="37b16-145">在傳遞的參數無效時擲回 <xref:System.ArgumentException> 例外狀況，或擲回預先定義之類別中，從 <xref:System.ArgumentException> 衍生而來的類別。</span><span class="sxs-lookup"><span data-stu-id="37b16-145">Throw an <xref:System.ArgumentException> exception or one of the predefined classes that derive from <xref:System.ArgumentException> if invalid parameters are passed.</span></span>

## <a name="end-exception-class-names-with-the-word-exception"></a><span data-ttu-id="37b16-146">使用字組 `Exception` 作為例外狀況類別名稱的結尾</span><span class="sxs-lookup"><span data-stu-id="37b16-146">End exception class names with the word `Exception`</span></span>

<span data-ttu-id="37b16-147">如需自訂例外狀況，請適當地加以命名，並從 <xref:System.Exception>加以衍生。</span><span class="sxs-lookup"><span data-stu-id="37b16-147">When a custom exception is necessary, name it appropriately and derive it from the <xref:System.Exception> class.</span></span> <span data-ttu-id="37b16-148">例如：</span><span class="sxs-lookup"><span data-stu-id="37b16-148">For example:</span></span>

[!code-cpp[Conceptual.Exception.Handling#4](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#4)]
[!code-csharp[Conceptual.Exception.Handling#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#4)]
[!code-vb[Conceptual.Exception.Handling#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#4)]

## <a name="include-three-constructors-in-custom-exception-classes"></a><span data-ttu-id="37b16-149">在自訂例外狀況類別中包含三個建構函式</span><span class="sxs-lookup"><span data-stu-id="37b16-149">Include three constructors in custom exception classes</span></span>

<span data-ttu-id="37b16-150">當您建立自己的例外狀況類別時，請使用至少三個種常見的建構函式：無參數建構函式、採用字串訊息的建構函式，以及採用字串訊息和內部例外狀況的建構函式。</span><span class="sxs-lookup"><span data-stu-id="37b16-150">Use at least the three common constructors when creating your own exception classes: the parameterless constructor, a constructor that takes a string message, and a constructor that takes a string message and an inner exception.</span></span>

- <span data-ttu-id="37b16-151"><xref:System.Exception.%23ctor>，會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="37b16-151"><xref:System.Exception.%23ctor>, which uses default values.</span></span>

- <span data-ttu-id="37b16-152"><xref:System.Exception.%23ctor%28System.String%29>，它會接受字串訊息。</span><span class="sxs-lookup"><span data-stu-id="37b16-152"><xref:System.Exception.%23ctor%28System.String%29>, which accepts a string message.</span></span>

- <span data-ttu-id="37b16-153"><xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>，它會接受字串訊息和內部例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-153"><xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>, which accepts a string message and an inner exception.</span></span>

<span data-ttu-id="37b16-154">如需範例，請參閱[如何：建立使用者定義的例外狀況](how-to-create-user-defined-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="37b16-154">For an example, see [How to: Create User-Defined Exceptions](how-to-create-user-defined-exceptions.md).</span></span>

## <a name="ensure-that-exception-data-is-available-when-code-executes-remotely"></a><span data-ttu-id="37b16-155">確保從遠端執行程式碼時可以使用例外狀況資料</span><span class="sxs-lookup"><span data-stu-id="37b16-155">Ensure that exception data is available when code executes remotely</span></span>

<span data-ttu-id="37b16-156">當您建立使用者定義的例外狀況時，請確保例外狀況的中繼資料可供遠端執行的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="37b16-156">When you create user-defined exceptions, ensure that the metadata for the exceptions is available to code that is executing remotely.</span></span>

<span data-ttu-id="37b16-157">例如，在支援應用程式定義域的 .NET 實作上，例外狀況可能會跨應用程式定義域發生。</span><span class="sxs-lookup"><span data-stu-id="37b16-157">For example, on .NET implementations that support App Domains, exceptions may occur across App domains.</span></span> <span data-ttu-id="37b16-158">假定應用程式定義域 A 建立應用程式定義域 B，它會執行擲回例外狀況的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37b16-158">Suppose App Domain A creates App Domain B, which executes code that throws an exception.</span></span> <span data-ttu-id="37b16-159">為使應用程式定義域 A 能夠正確地攔截及處理例外狀況，其必須能夠尋找含有應用程式定義域 B 所擲回之例外狀況的組件。若應用程式定義域 B 擲回例外狀況，但此例外狀況包含在位於其應用程式基底之下的組件，而不是位於在應用程式定義域 A 的應用程式基底之下的組件，應用程式定義域 A 將無法尋找例外狀況，而且 Common Language Runtime 將會擲回 <xref:System.IO.FileNotFoundException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="37b16-159">For App Domain A to properly catch and handle the exception, it must be able to find the assembly that contains the exception thrown by App Domain B. If App Domain B throws an exception that is contained in an assembly under its application base, but not under App Domain A's application base, App Domain A will not be able to find the exception, and the common language runtime will throw a <xref:System.IO.FileNotFoundException> exception.</span></span> <span data-ttu-id="37b16-160">若要避免這個情形，您可以透過兩種方式部署含有例外狀況資訊的組件：</span><span class="sxs-lookup"><span data-stu-id="37b16-160">To avoid this situation, you can deploy the assembly that contains the exception information in two ways:</span></span>

- <span data-ttu-id="37b16-161">將組件放入這兩個應用程式定義域共用的通用應用程式基底。</span><span class="sxs-lookup"><span data-stu-id="37b16-161">Put the assembly into a common application base shared by both app domains.</span></span>

    <span data-ttu-id="37b16-162">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="37b16-162">\- or -</span></span>

- <span data-ttu-id="37b16-163">如果定義域不共用通用應用程式基底，則以強式名稱簽署含有例外狀況資訊的組件，並將組件部署到全域組件快取中。</span><span class="sxs-lookup"><span data-stu-id="37b16-163">If the domains do not share a common application base, sign the assembly that contains the exception information with a strong name and deploy the assembly into the global assembly cache.</span></span>

## <a name="use-grammatically-correct-error-messages"></a><span data-ttu-id="37b16-164">使用文法正確的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="37b16-164">Use grammatically correct error messages</span></span>

<span data-ttu-id="37b16-165">撰寫清楚的句子並包含結尾標點符號。</span><span class="sxs-lookup"><span data-stu-id="37b16-165">Write clear sentences and include ending punctuation.</span></span> <span data-ttu-id="37b16-166">在每個指派給 <xref:System.Exception.Message?displayProperty=nameWithType> 屬性的字串中之句子，都應以句點結束。</span><span class="sxs-lookup"><span data-stu-id="37b16-166">Each sentence in the string assigned to the <xref:System.Exception.Message?displayProperty=nameWithType> property should end in a period.</span></span> <span data-ttu-id="37b16-167">例如，「記錄資料表已溢位」。</span><span class="sxs-lookup"><span data-stu-id="37b16-167">For example, "The log table has overflowed."</span></span> <span data-ttu-id="37b16-168">就是正確的訊息字串。</span><span class="sxs-lookup"><span data-stu-id="37b16-168">would be an appropriate message string.</span></span>

## <a name="include-a-localized-string-message-in-every-exception"></a><span data-ttu-id="37b16-169">在每個例外狀況中，納入當地語系化的字串訊息</span><span class="sxs-lookup"><span data-stu-id="37b16-169">Include a localized string message in every exception</span></span>

<span data-ttu-id="37b16-170">使用者所看到的錯誤訊息，衍生自擲回的例外狀況之 <xref:System.Exception.Message?displayProperty=nameWithType> 屬性，而並非來自例外狀況類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="37b16-170">The error message that the user sees is derived from the <xref:System.Exception.Message?displayProperty=nameWithType> property of the exception that was thrown, and not from the name of the exception class.</span></span> <span data-ttu-id="37b16-171">一般來說，您要將值指派到 <xref:System.Exception.Message?displayProperty=nameWithType> 屬性，方法是將訊息字串傳遞到[例外狀況建構函式](xref:System.Exception.%23ctor%2A)的 `message` 引數。</span><span class="sxs-lookup"><span data-stu-id="37b16-171">Typically, you assign a value to the <xref:System.Exception.Message?displayProperty=nameWithType>  property by passing the message string to the `message` argument of an [Exception constructor](xref:System.Exception.%23ctor%2A).</span></span>

<span data-ttu-id="37b16-172">若是當地語系化的應用程式，則應對每個應用程式可能會擲回的例外狀況，該提供當地語系化的訊息字串。</span><span class="sxs-lookup"><span data-stu-id="37b16-172">For localized applications, you should provide a localized message string for every exception that your application can throw.</span></span> <span data-ttu-id="37b16-173">您可使用資源檔，提供當地語系化的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="37b16-173">You use resource files to provide localized error messages.</span></span> <span data-ttu-id="37b16-174">如需當地語系化應用程式和取得當地語系化字串的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="37b16-174">For information on localizing applications and retrieving localized strings, see the following articles:</span></span>

- [<span data-ttu-id="37b16-175">如何：使用當地語系化例外狀況訊息來建立使用者定義的例外狀況</span><span class="sxs-lookup"><span data-stu-id="37b16-175">How to: create user-defined exceptions with localized exception messages</span></span>](how-to-create-localized-exception-messages.md)
- [<span data-ttu-id="37b16-176">桌面應用程式中的資源</span><span class="sxs-lookup"><span data-stu-id="37b16-176">Resources in Desktop Apps</span></span>](../../framework/resources/index.md)
- <xref:System.Resources.ResourceManager?displayProperty=nameWithType>

## <a name="in-custom-exceptions-provide-additional-properties-as-needed"></a><span data-ttu-id="37b16-177">在自訂例外狀況中，視需要提供額外的屬性</span><span class="sxs-lookup"><span data-stu-id="37b16-177">In custom exceptions, provide additional properties as needed</span></span>

<span data-ttu-id="37b16-178">只有在其他資訊對某個程式設計案例實用時，才為例外狀況提供其他屬性 (以及自訂訊息字串)。</span><span class="sxs-lookup"><span data-stu-id="37b16-178">Provide additional properties for an exception (in addition to the custom message string) only when there's a programmatic scenario where the additional information is useful.</span></span> <span data-ttu-id="37b16-179">例如，<xref:System.IO.FileNotFoundException> 提供 <xref:System.IO.FileNotFoundException.FileName> 屬性。</span><span class="sxs-lookup"><span data-stu-id="37b16-179">For example, the <xref:System.IO.FileNotFoundException> provides the <xref:System.IO.FileNotFoundException.FileName> property.</span></span>

## <a name="place-throw-statements-so-that-the-stack-trace-will-be-helpful"></a><span data-ttu-id="37b16-180">放置 throw 陳述式讓堆疊追蹤更有用</span><span class="sxs-lookup"><span data-stu-id="37b16-180">Place throw statements so that the stack trace will be helpful</span></span>

<span data-ttu-id="37b16-181">堆疊追蹤會從擲回例外狀況所在的陳述式開始，並在攔截例外狀況的 `catch` 陳述式結束。</span><span class="sxs-lookup"><span data-stu-id="37b16-181">The stack trace begins at the statement where the exception is thrown and ends at the `catch` statement that catches the exception.</span></span>

## <a name="use-exception-builder-methods"></a><span data-ttu-id="37b16-182">使用例外狀況產生器方法</span><span class="sxs-lookup"><span data-stu-id="37b16-182">Use exception builder methods</span></span>

<span data-ttu-id="37b16-183">類別在它的實作中從不同的地方擲回相同的例外狀況是很常見的。</span><span class="sxs-lookup"><span data-stu-id="37b16-183">It is common for a class to throw the same exception from different places in its implementation.</span></span> <span data-ttu-id="37b16-184">若要避免過多的程式碼，請使用 Helper 方法，以建立例外狀況並將它傳回。</span><span class="sxs-lookup"><span data-stu-id="37b16-184">To avoid excessive code, use helper methods that create the exception and return it.</span></span> <span data-ttu-id="37b16-185">例如：</span><span class="sxs-lookup"><span data-stu-id="37b16-185">For example:</span></span>

[!code-cpp[Conceptual.Exception.Handling#6](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#6)]
[!code-csharp[Conceptual.Exception.Handling#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#6)]
[!code-vb[Conceptual.Exception.Handling#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#6)]

<span data-ttu-id="37b16-186">在某些情況下，使用例外狀況的建構函式來建置例外狀況會更適當。</span><span class="sxs-lookup"><span data-stu-id="37b16-186">In some cases, it's more appropriate to use the exception's constructor to build the exception.</span></span> <span data-ttu-id="37b16-187">範例為全域例外狀況類別 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="37b16-187">An example is a global exception class such as <xref:System.ArgumentException>.</span></span>

## <a name="restore-state-when-methods-dont-complete-due-to-exceptions"></a><span data-ttu-id="37b16-188">當方法因為例外狀況而未完成時還原狀態</span><span class="sxs-lookup"><span data-stu-id="37b16-188">Restore state when methods don't complete due to exceptions</span></span>

<span data-ttu-id="37b16-189">呼叫端應該能夠假設，從方法擲回例外狀況時不會產生副作用。</span><span class="sxs-lookup"><span data-stu-id="37b16-189">Callers should be able to assume that there are no side effects when an exception is thrown from a method.</span></span> <span data-ttu-id="37b16-190">例如，如果您有用來轉帳的程式碼，會從某個帳戶提款再存入另一個帳戶，而且在執行存款時擲回例外狀況，則您不想要讓提款仍有效。</span><span class="sxs-lookup"><span data-stu-id="37b16-190">For example, if you have code that transfers money by withdrawing from one account and depositing in another account, and an exception is thrown while executing the deposit, you don't want the withdrawal to remain in effect.</span></span>

```csharp
public void TransferFunds(Account from, Account to, decimal amount)
{
    from.Withdrawal(amount);
    // If the deposit fails, the withdrawal shouldn't remain in effect.
    to.Deposit(amount);
}
```

```vb
Public Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    from.Withdrawal(amount)
    ' If the deposit fails, the withdrawal shouldn't remain in effect.
    [to].Deposit(amount)
End Sub
```

<span data-ttu-id="37b16-191">上述的方法不直接擲回任何例外狀況，但必須以自我防禦的方式寫入，以便存款作業失敗時可以撤銷付款。</span><span class="sxs-lookup"><span data-stu-id="37b16-191">The method above does not directly throw any exceptions, but must be written defensively so that if the deposit operation fails, the withdrawal is reversed.</span></span>

<span data-ttu-id="37b16-192">處理這種情況的一個方式是攔截存款交易所擲回的任何例外狀況，並復原提款。</span><span class="sxs-lookup"><span data-stu-id="37b16-192">One way to handle this situation is to catch any exceptions thrown by the deposit transaction and roll back the withdrawal.</span></span>

```csharp
private static void TransferFunds(Account from, Account to, decimal amount)
{
    string withdrawalTrxID = from.Withdrawal(amount);
    try
    {
        to.Deposit(amount);
    }
    catch
    {
        from.RollbackTransaction(withdrawalTrxID);
        throw;
    }
}
```

```vb
Private Shared Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    Dim withdrawalTrxID As String = from.Withdrawal(amount)
    Try
        [to].Deposit(amount)
    Catch
        from.RollbackTransaction(withdrawalTrxID)
        Throw
    End Try
End Sub
```

<span data-ttu-id="37b16-193">此範例說明如何使用 `throw` 重新擲回原始的例外狀況，以方便呼叫端無須檢視 <xref:System.Exception.InnerException>屬性，就能輕鬆查看問題的實際原因。</span><span class="sxs-lookup"><span data-stu-id="37b16-193">This example illustrates the use of `throw` to re-throw the original exception, which can make it easier for callers to see the real cause of the problem without having to examine the <xref:System.Exception.InnerException> property.</span></span> <span data-ttu-id="37b16-194">另一種做法是擲回新的例外狀況，並包含原始例外狀況作為內部例外狀況：</span><span class="sxs-lookup"><span data-stu-id="37b16-194">An alternative is to throw a new exception and include the original exception as the inner exception:</span></span>

```csharp
catch (Exception ex)
{
    from.RollbackTransaction(withdrawalTrxID);
    throw new TransferFundsException("Withdrawal failed.", innerException: ex)
    {
        From = from,
        To = to,
        Amount = amount
    };
}
```

```vb
Catch ex As Exception
    from.RollbackTransaction(withdrawalTrxID)
    Throw New TransferFundsException("Withdrawal failed.", innerException:=ex) With
    {
        .From = from,
        .[To] = [to],
        .Amount = amount
    }
End Try
```

## <a name="see-also"></a><span data-ttu-id="37b16-195">請參閱</span><span class="sxs-lookup"><span data-stu-id="37b16-195">See also</span></span>

- [<span data-ttu-id="37b16-196">例外狀況</span><span class="sxs-lookup"><span data-stu-id="37b16-196">Exceptions</span></span>](index.md)

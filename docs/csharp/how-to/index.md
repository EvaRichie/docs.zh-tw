---
title: 操作說明文章 (C# 指南)
description: 集結了快速提示與簡要的程式碼範例
ms.date: 12/20/2017
ms.openlocfilehash: 26d3931ff3b4ecfcc052c3ace25a09801f84c505
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537401"
---
# <a name="how-to-c"></a><span data-ttu-id="34a38-103">操作說明 (C#)</span><span class="sxs-lookup"><span data-stu-id="34a38-103">How to (C#)</span></span>

<span data-ttu-id="34a38-104">在 c # 指南的 how to 區段中，您可以找到常見問題的快速解答。</span><span class="sxs-lookup"><span data-stu-id="34a38-104">In the How to section of the C# Guide, you can find quick answers to common questions.</span></span> <span data-ttu-id="34a38-105">在某些形況下，文章可能會列在多個章節內。</span><span class="sxs-lookup"><span data-stu-id="34a38-105">In some cases, articles may be listed in multiple sections.</span></span> <span data-ttu-id="34a38-106">這是因為我們希望使用者能從多個搜尋管道輕鬆找到這些文章。</span><span class="sxs-lookup"><span data-stu-id="34a38-106">We wanted to make them easy to find for multiple search paths.</span></span>

## <a name="general-c-concepts"></a><span data-ttu-id="34a38-107">一般 C# 概念</span><span class="sxs-lookup"><span data-stu-id="34a38-107">General C# concepts</span></span>

<span data-ttu-id="34a38-108">常見的 c # 開發人員作法有幾個秘訣和訣竅：</span><span class="sxs-lookup"><span data-stu-id="34a38-108">There are several tips and tricks that are common C# developer practices:</span></span>

- <span data-ttu-id="34a38-109">[使用物件初始設定式將物件初始化](../programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-109">[Initialize objects using an object initializer](../programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md).</span></span>
- <span data-ttu-id="34a38-110">[了解向方法傳遞結構及類別的不同](../programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-110">[Learn the differences between passing a struct and a class to a method](../programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md).</span></span>
- <span data-ttu-id="34a38-111">[使用運算子多載](../language-reference/operators/operator-overloading.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-111">[Use operator overloading](../language-reference/operators/operator-overloading.md).</span></span>
- <span data-ttu-id="34a38-112">[執行和呼叫自訂擴充方法](../programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-112">[Implement and call a custom extension method](../programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md).</span></span>
- <span data-ttu-id="34a38-113">即使是 c # 程式設計人員也可能想要 [使用 `My` Visual Basic 的命名空間](../programming-guide/namespaces/how-to-use-the-my-namespace.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-113">Even C# programmers may want to [use the `My` namespace from Visual Basic](../programming-guide/namespaces/how-to-use-the-my-namespace.md).</span></span>
- <span data-ttu-id="34a38-114">[使用擴充方法建立 `enum` 類型的新方法](../programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-114">[Create a new method for an `enum` type using extension methods](../programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md).</span></span>

### <a name="class-and-struct-members"></a><span data-ttu-id="34a38-115">類別和結構成員</span><span class="sxs-lookup"><span data-stu-id="34a38-115">Class and struct members</span></span>

<span data-ttu-id="34a38-116">您可以建立類別及結構來實作您的程式。</span><span class="sxs-lookup"><span data-stu-id="34a38-116">You create classes and structs to implement your program.</span></span> <span data-ttu-id="34a38-117">撰寫類別或結構時常會用到這些技術。</span><span class="sxs-lookup"><span data-stu-id="34a38-117">These techniques are commonly used when writing classes or structs.</span></span>

- <span data-ttu-id="34a38-118">[宣告自動實作屬性](../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-118">[Declare auto implemented properties](../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md).</span></span>
- <span data-ttu-id="34a38-119">[宣告和使用 R/W 屬性](../programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-119">[Declare and use read/write properties](../programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties.md).</span></span>
- <span data-ttu-id="34a38-120">[定義常數](../programming-guide/classes-and-structs/how-to-define-constants.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-120">[Define constants](../programming-guide/classes-and-structs/how-to-define-constants.md).</span></span>
- <span data-ttu-id="34a38-121">[覆寫 `ToString` 方法來提供字串輸出](../programming-guide/classes-and-structs/how-to-override-the-tostring-method.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-121">[Override the `ToString` method to provide string output](../programming-guide/classes-and-structs/how-to-override-the-tostring-method.md).</span></span>
- <span data-ttu-id="34a38-122">[定義抽象屬性](../programming-guide/classes-and-structs/how-to-define-abstract-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-122">[Define abstract properties](../programming-guide/classes-and-structs/how-to-define-abstract-properties.md).</span></span>
- <span data-ttu-id="34a38-123">[使用 XML 文件功能來記錄程式碼](../programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-123">[Use the xml documentation features to document your code](../programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md).</span></span>
- <span data-ttu-id="34a38-124">[明確實作介面成員](../programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)讓公用介面保持精簡。</span><span class="sxs-lookup"><span data-stu-id="34a38-124">[Explicitly implement interface members](../programming-guide/interfaces/how-to-explicitly-implement-interface-members.md) to keep your public interface concise.</span></span>
- <span data-ttu-id="34a38-125">[明確實作兩個介面的成員](../programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-125">[Explicitly implement members of two interfaces](../programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md).</span></span>

### <a name="working-with-collections"></a><span data-ttu-id="34a38-126">使用集合</span><span class="sxs-lookup"><span data-stu-id="34a38-126">Working with collections</span></span>

<span data-ttu-id="34a38-127">這些文章有助您使用資料集合。</span><span class="sxs-lookup"><span data-stu-id="34a38-127">These articles help you work with collections of data.</span></span>

- <span data-ttu-id="34a38-128">[使用集合初始設定式將字典初始化](../programming-guide/classes-and-structs/how-to-initialize-a-dictionary-with-a-collection-initializer.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-128">[Initialize a dictionary with a collection initializer](../programming-guide/classes-and-structs/how-to-initialize-a-dictionary-with-a-collection-initializer.md).</span></span>

## <a name="working-with-strings"></a><span data-ttu-id="34a38-129">使用字串</span><span class="sxs-lookup"><span data-stu-id="34a38-129">Working with strings</span></span>

<span data-ttu-id="34a38-130">字串是用來顯示或操作文字的基本資料類型。</span><span class="sxs-lookup"><span data-stu-id="34a38-130">Strings are the fundamental data type used to display or manipulate text.</span></span> <span data-ttu-id="34a38-131">這些文章會示範字串的常見做法。</span><span class="sxs-lookup"><span data-stu-id="34a38-131">These articles demonstrate common practices with strings.</span></span>

- <span data-ttu-id="34a38-132">[比較字串](compare-strings.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-132">[Compare strings](compare-strings.md).</span></span>
- <span data-ttu-id="34a38-133">[修改字串內容](modify-string-contents.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-133">[Modify the contents of a string](modify-string-contents.md).</span></span>
- <span data-ttu-id="34a38-134">[判斷字串是否代表一個數字](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-134">[Determine if a string represents a number](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).</span></span>
- <span data-ttu-id="34a38-135">[使用 `String.Split` 來分隔字串](parse-strings-using-split.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-135">[Use `String.Split` to separate strings](parse-strings-using-split.md).</span></span>
- <span data-ttu-id="34a38-136">[將多個字串合併為一個字串](concatenate-multiple-strings.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-136">[Combine multiple strings into one](concatenate-multiple-strings.md).</span></span>
- <span data-ttu-id="34a38-137">[搜尋字串中的文字](search-strings.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-137">[Search for text in a string](search-strings.md).</span></span>

## <a name="convert-between-types"></a><span data-ttu-id="34a38-138">在類型之間轉換</span><span class="sxs-lookup"><span data-stu-id="34a38-138">Convert between types</span></span>

<span data-ttu-id="34a38-139">您可能需要將物件轉換為不同類型。</span><span class="sxs-lookup"><span data-stu-id="34a38-139">You may need to convert an object to a different type.</span></span>

- <span data-ttu-id="34a38-140">[判斷字串是否代表一個數字](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-140">[Determine if a string represents a number](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).</span></span>
- <span data-ttu-id="34a38-141">[在代表十六進位數字的字串與數字之間轉換](../programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-141">[Convert between strings that represent hexadecimal numbers and the number](../programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).</span></span>
- <span data-ttu-id="34a38-142">[將字串轉換為 `DateTime`](../../standard/base-types/parsing-datetime.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-142">[Convert a string to a `DateTime`](../../standard/base-types/parsing-datetime.md).</span></span>
- <span data-ttu-id="34a38-143">[將位元組陣列轉換為 int](../programming-guide/types/how-to-convert-a-byte-array-to-an-int.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-143">[Convert a byte array to an int](../programming-guide/types/how-to-convert-a-byte-array-to-an-int.md).</span></span>
- <span data-ttu-id="34a38-144">[將字串轉換為數字](../programming-guide/types/how-to-convert-a-string-to-a-number.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-144">[Convert a string to a number](../programming-guide/types/how-to-convert-a-string-to-a-number.md).</span></span>
- <span data-ttu-id="34a38-145">[使用模式比對，以 `as` 和 `is` 運算子安全地轉換至其他類型](safely-cast-using-pattern-matching-is-and-as-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-145">[Use pattern matching, the `as` and `is` operators to safely cast to a different type](safely-cast-using-pattern-matching-is-and-as-operators.md).</span></span>
- <span data-ttu-id="34a38-146">[定義自訂型別轉換](../language-reference/operators/user-defined-conversion-operators.md).</span><span class="sxs-lookup"><span data-stu-id="34a38-146">[Define custom type conversions](../language-reference/operators/user-defined-conversion-operators.md).</span></span>
- <span data-ttu-id="34a38-147">[決定類型是不是可為 Null 的實值型別](../language-reference/builtin-types/nullable-value-types.md#how-to-identify-a-nullable-value-type)。</span><span class="sxs-lookup"><span data-stu-id="34a38-147">[Determine if a type is a nullable value type](../language-reference/builtin-types/nullable-value-types.md#how-to-identify-a-nullable-value-type).</span></span>
- <span data-ttu-id="34a38-148">[在可為 Null 與不可為 Null 的實值型別間轉換](../language-reference/builtin-types/nullable-value-types.md#conversion-from-a-nullable-value-type-to-an-underlying-type)。</span><span class="sxs-lookup"><span data-stu-id="34a38-148">[Convert between nullable and non-nullable value types](../language-reference/builtin-types/nullable-value-types.md#conversion-from-a-nullable-value-type-to-an-underlying-type).</span></span>

## <a name="equality-and-ordering-comparisons"></a><span data-ttu-id="34a38-149">相等和排序比較</span><span class="sxs-lookup"><span data-stu-id="34a38-149">Equality and ordering comparisons</span></span>

<span data-ttu-id="34a38-150">您可以建立定義自身相等規則的類型，或是定義該類型物件的自然順序。</span><span class="sxs-lookup"><span data-stu-id="34a38-150">You may create types that define their own rules for equality or define a natural ordering among objects of that type.</span></span>

- <span data-ttu-id="34a38-151">[測試以參考為依據的相等](../programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-151">[Test for reference-based equality](../programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).</span></span>
- <span data-ttu-id="34a38-152">[定義類型的實值相等](../programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-152">[Define value-based equality for a type](../programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).</span></span>

## <a name="exception-handling"></a><span data-ttu-id="34a38-153">例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="34a38-153">Exception handling</span></span>

<span data-ttu-id="34a38-154">.NET 程式會透過擲回例外狀況，回報方法未成功完成其作業。</span><span class="sxs-lookup"><span data-stu-id="34a38-154">.NET programs report that methods did not successfully complete their work by throwing exceptions.</span></span> <span data-ttu-id="34a38-155">在這些文章中，您會了解如何利用例外狀況。</span><span class="sxs-lookup"><span data-stu-id="34a38-155">In these articles you'll learn to work with exceptions.</span></span>

- <span data-ttu-id="34a38-156">[使用 `try` 與 `catch` 處理例外狀況](../programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-156">[Handle exceptions using `try` and `catch`](../programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md).</span></span>
- <span data-ttu-id="34a38-157">[使用 `finally` 子句清除資源](../programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-157">[Cleanup resources using `finally` clauses](../programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md).</span></span>
- <span data-ttu-id="34a38-158">[從非 CLS (Common Language Specification) 例外狀況復原](../programming-guide/exceptions/how-to-catch-a-non-cls-exception.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-158">[Recover from non-CLS (Common Language Specification) exceptions](../programming-guide/exceptions/how-to-catch-a-non-cls-exception.md).</span></span>

## <a name="delegates-and-events"></a><span data-ttu-id="34a38-159">委派和事件</span><span class="sxs-lookup"><span data-stu-id="34a38-159">Delegates and events</span></span>

<span data-ttu-id="34a38-160">委派和事件會提供有關鬆散結合程式碼區塊的策略功能。</span><span class="sxs-lookup"><span data-stu-id="34a38-160">Delegates and events provide a capability for strategies that involve loosely coupled blocks of code.</span></span>

- <span data-ttu-id="34a38-161">[宣告和使用委派及將其具現化](../programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-161">[Declare, instantiate, and use delegates](../programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md).</span></span>
- <span data-ttu-id="34a38-162">[合併多點傳送委派](../programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-162">[Combine multicast delegates](../programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md).</span></span>

<span data-ttu-id="34a38-163">事件會提供發佈或訂閱通知的機制。</span><span class="sxs-lookup"><span data-stu-id="34a38-163">Events provide a mechanism to publish or subscribe to notifications.</span></span>

- <span data-ttu-id="34a38-164">[訂閱及取消訂閱事件](../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-164">[Subscribe and unsubscribe from events](../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).</span></span>
- <span data-ttu-id="34a38-165">[實作介面中宣告的事件](../programming-guide/events/how-to-implement-interface-events.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-165">[Implement events declared in interfaces](../programming-guide/events/how-to-implement-interface-events.md).</span></span>
- <span data-ttu-id="34a38-166">[當您的程式碼發佈事件時，符合 .net 指導方針](../programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-166">[Conform to .NET guidelines when your code publishes events](../programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).</span></span>
- <span data-ttu-id="34a38-167">[從衍生類別引發在基底類別中定義的事件](../programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-167">[Raise events defined in base classes from derived classes](../programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md).</span></span>
- <span data-ttu-id="34a38-168">[實作自訂事件存取子](../programming-guide/events/how-to-implement-custom-event-accessors.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-168">[Implement custom event accessors](../programming-guide/events/how-to-implement-custom-event-accessors.md).</span></span>

## <a name="linq-practices"></a><span data-ttu-id="34a38-169">LINQ 做法</span><span class="sxs-lookup"><span data-stu-id="34a38-169">LINQ practices</span></span>

<span data-ttu-id="34a38-170">LINQ 可讓您撰寫程式碼，來查詢支援 LINQ 查詢運算式模式的任何資料來源。</span><span class="sxs-lookup"><span data-stu-id="34a38-170">LINQ enables you to write code to query any data source that supports the LINQ query expression pattern.</span></span> <span data-ttu-id="34a38-171">這些文章有助您理解模式，以及如何利用各種資料來源。</span><span class="sxs-lookup"><span data-stu-id="34a38-171">These articles help you understand the pattern and work with different data sources.</span></span>

- <span data-ttu-id="34a38-172">[查詢集合](../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-172">[Query a collection](../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md).</span></span>
- <span data-ttu-id="34a38-173">[在查詢中使用 lambda 運算式](../programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-in-a-query.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-173">[Use lambda expressions in a query](../programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-in-a-query.md).</span></span>
- <span data-ttu-id="34a38-174">[在查詢運算式中使用 `var`](../programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-174">[Use `var` in query expressions](../programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md).</span></span>
- <span data-ttu-id="34a38-175">[從查詢傳回元素屬性的子集](../programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-175">[Return subsets of element properties from a query](../programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md).</span></span>
- <span data-ttu-id="34a38-176">[撰寫具有複雜篩選的查詢](../../standard/linq/write-queries-complex-filtering.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-176">[Write queries with complex filtering](../../standard/linq/write-queries-complex-filtering.md).</span></span>
- <span data-ttu-id="34a38-177">[排序資料來源的元素](../../standard/linq/sort-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-177">[Sort elements of a data source](../../standard/linq/sort-elements.md).</span></span>
- <span data-ttu-id="34a38-178">[排序多個索引鍵的元素](../../standard/linq/sort-elements-multiple-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-178">[Sort elements on multiple keys](../../standard/linq/sort-elements-multiple-keys.md).</span></span>
- <span data-ttu-id="34a38-179">[控制投影的類型](../../standard/linq/control-type-projection.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-179">[Control the type of a projection](../../standard/linq/control-type-projection.md).</span></span>
- <span data-ttu-id="34a38-180">[計算來源序列中值的出現次數](../programming-guide/concepts/linq/how-to-count-occurrences-of-a-word-in-a-string-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-180">[Count occurrences of a value in a source sequence](../programming-guide/concepts/linq/how-to-count-occurrences-of-a-word-in-a-string-linq.md).</span></span>
- <span data-ttu-id="34a38-181">[計算中繼值](../../standard/linq/calculate-intermediate-values.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-181">[Calculate intermediate values](../../standard/linq/calculate-intermediate-values.md).</span></span>
- <span data-ttu-id="34a38-182">[合併多個來源的資料](../programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-182">[Merge data from multiple sources](../programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md).</span></span>
- <span data-ttu-id="34a38-183">[找出兩個序列之間的集合差異](../programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-183">[Find the set difference between two sequences](../programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md).</span></span>
- <span data-ttu-id="34a38-184">[為空白的查詢結果偵錯](../../standard/linq/debug-empty-query-results-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-184">[Debug empty query results](../../standard/linq/debug-empty-query-results-sets.md).</span></span>
- <span data-ttu-id="34a38-185">[將自訂方法新增到 LINQ 查詢](../programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-185">[Add custom methods to LINQ queries](../programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md).</span></span>

## <a name="multiple-threads-and-async-processing"></a><span data-ttu-id="34a38-186">多個執行緒和非同步處理</span><span class="sxs-lookup"><span data-stu-id="34a38-186">Multiple threads and async processing</span></span>

<span data-ttu-id="34a38-187">新式程式常使用非同步作業。</span><span class="sxs-lookup"><span data-stu-id="34a38-187">Modern programs often use asynchronous operations.</span></span> <span data-ttu-id="34a38-188">這些文章會協助您了解如何使用這些技術。</span><span class="sxs-lookup"><span data-stu-id="34a38-188">These articles will help you learn to use these techniques.</span></span>

- <span data-ttu-id="34a38-189">[使用 `System.Threading.Tasks.Task.WhenAll` 改善非同步效能](../programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-189">[Improve async performance using `System.Threading.Tasks.Task.WhenAll`](../programming-guide/concepts/async/index.md).</span></span>
- <span data-ttu-id="34a38-190">[使用 `async` 與 `await` 平行提出多個 Web 要求](../programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-190">[Make multiple web requests in parallel using `async` and `await`](../programming-guide/concepts/async/index.md).</span></span>
- <span data-ttu-id="34a38-191">[使用執行緒集區](../../standard/threading/the-managed-thread-pool.md#using-the-thread-pool)。</span><span class="sxs-lookup"><span data-stu-id="34a38-191">[Use a thread pool](../../standard/threading/the-managed-thread-pool.md#using-the-thread-pool).</span></span>

## <a name="command-line-args-to-your-program"></a><span data-ttu-id="34a38-192">程式的命令列引數</span><span class="sxs-lookup"><span data-stu-id="34a38-192">Command line args to your program</span></span>

<span data-ttu-id="34a38-193">一般來說，C# 程式具有命令列引數。</span><span class="sxs-lookup"><span data-stu-id="34a38-193">Typically, C# programs have command line arguments.</span></span> <span data-ttu-id="34a38-194">這些文章會向您說明如何存取及處理這些命令列引數。</span><span class="sxs-lookup"><span data-stu-id="34a38-194">These articles teach you to access and process those command line arguments.</span></span>

- <span data-ttu-id="34a38-195">[使用 `for` 擷取所有命令列引數](../programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)。</span><span class="sxs-lookup"><span data-stu-id="34a38-195">[Retrieve all command line arguments with `for`](../programming-guide/main-and-command-args/how-to-display-command-line-arguments.md).</span></span>

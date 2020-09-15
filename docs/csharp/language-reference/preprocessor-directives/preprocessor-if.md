---
description: '#if 前置處理器指示詞 - C# 參考'
title: '#if 前置處理器指示詞 - C# 參考'
ms.date: 10/27/2019
f1_keywords:
- '#if'
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
ms.openlocfilehash: dc3e235db49279691203a0db4d124239fb972c69
ms.sourcegitcommit: a69d548f90a03e105ee6701236c38390ecd9ccd1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/14/2020
ms.locfileid: "90065226"
---
# <a name="if-c-reference"></a><span data-ttu-id="d4636-103">#if (c # 參考) </span><span class="sxs-lookup"><span data-stu-id="d4636-103">#if (C# reference)</span></span>

<span data-ttu-id="d4636-104">當 C# 編譯器遇到 `#if` 指示詞，且其後接著 [#endif](preprocessor-endif.md) 指示詞時，只有在定義了指定的符號時，它才會編譯指示詞之間的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4636-104">When the C# compiler encounters an `#if` directive, followed eventually by an [#endif](preprocessor-endif.md) directive, it compiles the code between the directives only if the specified symbol is defined.</span></span> <span data-ttu-id="d4636-105">不同於 C 和 C++，您無法將數值指派給符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-105">Unlike C and C++, you cannot assign a numeric value to a symbol.</span></span> <span data-ttu-id="d4636-106">`#if`C # 中的語句是布林值，而且只會測試是否已定義符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-106">The `#if` statement in C# is Boolean and only tests whether the symbol has been defined or not.</span></span> <span data-ttu-id="d4636-107">例如：</span><span class="sxs-lookup"><span data-stu-id="d4636-107">For example:</span></span>

```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

<span data-ttu-id="d4636-108">您可以使用運算子 [==](../operators/equality-operators.md#equality-operator-) (相等) 和 [！ =](../operators/equality-operators.md#inequality-operator-) (不相等) 僅測試 [bool](../builtin-types/bool.md) 值 `true` 或 `false` 。</span><span class="sxs-lookup"><span data-stu-id="d4636-108">You can use the operators [==](../operators/equality-operators.md#equality-operator-) (equality) and [!=](../operators/equality-operators.md#inequality-operator-) (inequality) only to test for the [bool](../builtin-types/bool.md) values `true` or `false`.</span></span> <span data-ttu-id="d4636-109">`true` 表示已定義符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-109">`true` means the symbol is defined.</span></span> <span data-ttu-id="d4636-110">`#if DEBUG` 陳述式的意義與 `#if (DEBUG == true)` 一樣。</span><span class="sxs-lookup"><span data-stu-id="d4636-110">The statement `#if DEBUG` has the same meaning as `#if (DEBUG == true)`.</span></span> <span data-ttu-id="d4636-111">您可以使用 [&&  (和) ](../operators/boolean-logical-operators.md#conditional-logical-and-operator-)、 [&#124;&#124;  (或) ](../operators/boolean-logical-operators.md#conditional-logical-or-operator-)，以及 [！ (不) ](../operators/boolean-logical-operators.md#logical-negation-operator-) 運算子來評估是否已定義多個符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-111">You can use the [&& (and)](../operators/boolean-logical-operators.md#conditional-logical-and-operator-), [&#124;&#124; (or)](../operators/boolean-logical-operators.md#conditional-logical-or-operator-), and [! (not)](../operators/boolean-logical-operators.md#logical-negation-operator-) operators to evaluate whether multiple symbols have been defined.</span></span> <span data-ttu-id="d4636-112">您也可以使用括弧來將符號和運算子分組。</span><span class="sxs-lookup"><span data-stu-id="d4636-112">You can also group symbols and operators with parentheses.</span></span>

## <a name="remarks"></a><span data-ttu-id="d4636-113">備註</span><span class="sxs-lookup"><span data-stu-id="d4636-113">Remarks</span></span>

<span data-ttu-id="d4636-114">`#if`以及 [#else](preprocessor-else.md)、 [#elif](preprocessor-elif.md)、 [#endif](preprocessor-endif.md)、 [#define](preprocessor-define.md)和 [#undef](preprocessor-undef.md) 指示詞，可讓您根據一或多個符號是否存在來包含或排除程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4636-114">`#if`, along with the [#else](preprocessor-else.md), [#elif](preprocessor-elif.md), [#endif](preprocessor-endif.md), [#define](preprocessor-define.md), and [#undef](preprocessor-undef.md) directives, lets you include or exclude code based on the existence of one or more symbols.</span></span> <span data-ttu-id="d4636-115">在編譯偵錯組建的程式碼時，或是在針對特定組態進行編譯時，這非常實用。</span><span class="sxs-lookup"><span data-stu-id="d4636-115">This can be useful when compiling code for a debug build or when compiling for a specific configuration.</span></span>

<span data-ttu-id="d4636-116">以 `#if` 指示詞開頭的條件式指示詞必須明確地以 `#endif` 指示詞終止。</span><span class="sxs-lookup"><span data-stu-id="d4636-116">A conditional directive beginning with a `#if` directive must explicitly be terminated with a `#endif` directive.</span></span>

<span data-ttu-id="d4636-117">`#define` 可讓您定義符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-117">`#define` lets you define a symbol.</span></span> <span data-ttu-id="d4636-118">屆時，使用該符號作為傳遞到 `#if` 指示詞的運算式，運算式就會評估為 `true`。</span><span class="sxs-lookup"><span data-stu-id="d4636-118">By then using the symbol as the expression passed to the `#if` directive, the expression evaluates to `true`.</span></span>

<span data-ttu-id="d4636-119">您也可以使用 [-define](../compiler-options/define-compiler-option.md) 編譯器選項來定義符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-119">You can also define a symbol with the [-define](../compiler-options/define-compiler-option.md) compiler option.</span></span> <span data-ttu-id="d4636-120">您可以使用 [#undef](preprocessor-undef.md) 來取消定義符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-120">You can undefine a symbol with [#undef](preprocessor-undef.md).</span></span>

<span data-ttu-id="d4636-121">透過 `-define` 或 `#define` 定義的符號不會與相同名稱的變數發生衝突。</span><span class="sxs-lookup"><span data-stu-id="d4636-121">A symbol that you define with `-define` or with `#define` doesn't conflict with a variable of the same name.</span></span> <span data-ttu-id="d4636-122">也就是說，您不應將變數名稱傳遞給前置處理器指示詞，而且符號僅能由前置處理器指示詞來評估。</span><span class="sxs-lookup"><span data-stu-id="d4636-122">That is, a variable name should not be passed to a preprocessor directive, and a symbol can only be evaluated by a preprocessor directive.</span></span>

<span data-ttu-id="d4636-123">使用 `#define` 建立的符號範圍是定義它的檔案。</span><span class="sxs-lookup"><span data-stu-id="d4636-123">The scope of a symbol created with `#define` is the file in which it was defined.</span></span>

<span data-ttu-id="d4636-124">組建系統也會留意表示 SDK 樣式專案中不同 [目標 framework](../../../standard/frameworks.md) 的預先定義預處理器符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-124">The build system is also aware of predefined preprocessor symbols representing different [target frameworks](../../../standard/frameworks.md) in SDK-style projects.</span></span> <span data-ttu-id="d4636-125">當您建立的應用程式可能會以多個 .NET 版本為目標時，它們會很有用。</span><span class="sxs-lookup"><span data-stu-id="d4636-125">They're useful when creating applications that can target more than one .NET version.</span></span>

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

> [!NOTE]
> <span data-ttu-id="d4636-126">針對傳統的非 SDK 樣式專案，您必須透過專案的 [屬性] 頁面，在 Visual Studio 中手動設定不同目標 framework 的條件式編譯符號。</span><span class="sxs-lookup"><span data-stu-id="d4636-126">For traditional, non-SDK-style projects, you have to manually configure the conditional compilation symbols for the different target frameworks in Visual Studio via the project's properties pages.</span></span>

<span data-ttu-id="d4636-127">其他預先定義符號包括 DEBUG 和 TRACE 常數。</span><span class="sxs-lookup"><span data-stu-id="d4636-127">Other predefined symbols include the DEBUG and TRACE constants.</span></span> <span data-ttu-id="d4636-128">您可以使用 `#define` 來覆寫為專案所設定的值。</span><span class="sxs-lookup"><span data-stu-id="d4636-128">You can override the values set for the project using `#define`.</span></span> <span data-ttu-id="d4636-129">例如，DEBUG 符號會根據您的組建組態屬性 ("Debug" 或 "Release" 模式) 而自動設定。</span><span class="sxs-lookup"><span data-stu-id="d4636-129">The DEBUG symbol, for example, is automatically set depending on your build configuration properties ("Debug" or "Release" mode).</span></span>

## <a name="examples"></a><span data-ttu-id="d4636-130">範例</span><span class="sxs-lookup"><span data-stu-id="d4636-130">Examples</span></span>

<span data-ttu-id="d4636-131">以下範例說明如何在檔案上定義 MYTEST 符號，然後測試 MYTEST 和 DEBUG 符號的值。</span><span class="sxs-lookup"><span data-stu-id="d4636-131">The following example shows you how to define a MYTEST symbol on a file and then test the values of the MYTEST and DEBUG symbols.</span></span> <span data-ttu-id="d4636-132">此範例的輸出視您使用 Debug 或 Release 組態模式建置專案而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d4636-132">The output of this example depends on whether you built the project on Debug or Release configuration mode.</span></span>

```csharp
#define MYTEST
using System;
public class MyClass
{
    static void Main()
    {
#if (DEBUG && !MYTEST)
        Console.WriteLine("DEBUG is defined");
#elif (!DEBUG && MYTEST)
        Console.WriteLine("MYTEST is defined");
#elif (DEBUG && MYTEST)
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else
        Console.WriteLine("DEBUG and MYTEST are not defined");
#endif
    }
}
```

<span data-ttu-id="d4636-133">以下範例說明如何測試不同的目標 Framework，讓您可以盡可能使用較新的 API：</span><span class="sxs-lookup"><span data-stu-id="d4636-133">The following example shows you how to test for different target frameworks so you can use newer APIs when possible:</span></span>

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        WebClient _client = new WebClient();
#else
        HttpClient _client = new HttpClient();
#endif
    }
    //...
}
```

## <a name="see-also"></a><span data-ttu-id="d4636-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d4636-134">See also</span></span>

- [<span data-ttu-id="d4636-135">C # 參考</span><span class="sxs-lookup"><span data-stu-id="d4636-135">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="d4636-136">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="d4636-136">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="d4636-137">C # 預處理器指示詞</span><span class="sxs-lookup"><span data-stu-id="d4636-137">C# Preprocessor Directives</span></span>](index.md)
- [<span data-ttu-id="d4636-138">作法：使用追蹤和偵錯進行條件式編譯</span><span class="sxs-lookup"><span data-stu-id="d4636-138">How to: Compile Conditionally with Trace and Debug</span></span>](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)

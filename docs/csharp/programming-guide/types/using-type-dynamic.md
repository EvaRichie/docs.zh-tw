---
title: 使用 dynamic 類型 - C# 程式設計指南
description: 瞭解如何使用動態類型。 動態類型是靜態類型，但是動態物件會略過靜態類型檢查。
ms.date: 07/20/2015
helpviewer_keywords:
- dynamic [C#], about dynamic type
- dynamic type [C#]
ms.assetid: 3828989d-c967-4a51-b948-857ebc8fdf26
ms.openlocfilehash: 9904f0452feca388704067b1fd5432f74d0df86b
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381576"
---
# <a name="using-type-dynamic-c-programming-guide"></a><span data-ttu-id="3c28e-104">使用 dynamic 類型 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="3c28e-104">Using type dynamic (C# Programming Guide)</span></span>

<span data-ttu-id="3c28e-105">C# 4 引進一種新型別 `dynamic`。</span><span class="sxs-lookup"><span data-stu-id="3c28e-105">C# 4 introduces a new type, `dynamic`.</span></span> <span data-ttu-id="3c28e-106">此類型是靜態類型，但 `dynamic` 類型的物件會略過靜態類型檢查。</span><span class="sxs-lookup"><span data-stu-id="3c28e-106">The type is a static type, but an object of type `dynamic` bypasses static type checking.</span></span> <span data-ttu-id="3c28e-107">在大多數情況下，其運作會像是具有 `object` 類型。</span><span class="sxs-lookup"><span data-stu-id="3c28e-107">In most cases, it functions like it has type `object`.</span></span> <span data-ttu-id="3c28e-108">在編譯時期，會假設類型為 `dynamic` 的項目能夠支援所有作業。</span><span class="sxs-lookup"><span data-stu-id="3c28e-108">At compile time, an element that is typed as `dynamic` is assumed to support any operation.</span></span> <span data-ttu-id="3c28e-109">因此，您無須考慮物件是從 COM API、動態語言 (例如 IronPython)、HTML 文件物件模型 (DOM)、反映或是程式其他地方取得其值。</span><span class="sxs-lookup"><span data-stu-id="3c28e-109">Therefore, you do not have to be concerned about whether the object gets its value from a COM API, from a dynamic language such as IronPython, from the HTML Document Object Model (DOM), from reflection, or from somewhere else in the program.</span></span> <span data-ttu-id="3c28e-110">不過，如果程式碼無效，則會在執行階段攔截到錯誤。</span><span class="sxs-lookup"><span data-stu-id="3c28e-110">However, if the code is not valid, errors are caught at run time.</span></span>

<span data-ttu-id="3c28e-111">例如，如果下列程式碼中的執行個體方法 `exampleMethod1` 只有一個參數，則編譯器會將 `ec.exampleMethod1(10, 4)` 方法的第一個呼叫視為無效，因為它包含兩個引數。</span><span class="sxs-lookup"><span data-stu-id="3c28e-111">For example, if instance method `exampleMethod1` in the following code has only one parameter, the compiler recognizes that the first call to the method, `ec.exampleMethod1(10, 4)`, is not valid because it contains two arguments.</span></span> <span data-ttu-id="3c28e-112">呼叫會造成編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="3c28e-112">The call causes a compiler error.</span></span> <span data-ttu-id="3c28e-113">編譯器不會檢查 `dynamic_ec.exampleMethod1(10, 4)` 方法的第二個呼叫，因為 `dynamic_ec` 的類型為 `dynamic`。</span><span class="sxs-lookup"><span data-stu-id="3c28e-113">The second call to the method, `dynamic_ec.exampleMethod1(10, 4)`, is not checked by the compiler because the type of `dynamic_ec` is `dynamic`.</span></span> <span data-ttu-id="3c28e-114">因此，不會報告編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="3c28e-114">Therefore, no compiler error is reported.</span></span> <span data-ttu-id="3c28e-115">不過，這項錯誤並不是永遠不會被發現。</span><span class="sxs-lookup"><span data-stu-id="3c28e-115">However, the error does not escape notice indefinitely.</span></span> <span data-ttu-id="3c28e-116">它會在執行階段被攔截，並造成執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3c28e-116">It is caught at run time and causes a run-time exception.</span></span>

[!code-csharp[CsProgGuideTypes#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#50)]

[!code-csharp[CsProgGuideTypes#56](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#56)]

<span data-ttu-id="3c28e-117">上述範例中的編譯器角色，就是將每個陳述式應該對類型為 `dynamic` 的物件或運算式所進行之動作的相關資訊封裝在一起。</span><span class="sxs-lookup"><span data-stu-id="3c28e-117">The role of the compiler in these examples is to package together information about what each statement is proposing to do to the object or expression that is typed as `dynamic`.</span></span> <span data-ttu-id="3c28e-118">在執行階段，會檢查這些預存資訊，如果有任何陳述式無效，便會造成執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3c28e-118">At run time, the stored information is examined, and any statement that is not valid causes a run-time exception.</span></span>

<span data-ttu-id="3c28e-119">大多數動態作業的結果本身就是 `dynamic`。</span><span class="sxs-lookup"><span data-stu-id="3c28e-119">The result of most dynamic operations is itself `dynamic`.</span></span> <span data-ttu-id="3c28e-120">例如，如果您在下列範例中將滑鼠指標停在 `testSum` 的使用用途上，IntelliSense 會顯示 **(區域變數) dynamic testSum** 類型。</span><span class="sxs-lookup"><span data-stu-id="3c28e-120">For example, if you rest the mouse pointer over the use of `testSum` in the following example, IntelliSense displays the type **(local variable) dynamic testSum**.</span></span>

[!code-csharp[CsProgGuideTypes#51](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#51)]

<span data-ttu-id="3c28e-121">結果不是 `dynamic` 的作業包括：</span><span class="sxs-lookup"><span data-stu-id="3c28e-121">Operations in which the result is not `dynamic` include:</span></span>

* <span data-ttu-id="3c28e-122">從 `dynamic` 轉換成另一種類型。</span><span class="sxs-lookup"><span data-stu-id="3c28e-122">Conversions from `dynamic` to another type.</span></span>
* <span data-ttu-id="3c28e-123">包含 `dynamic` 類型引數的建構函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="3c28e-123">Constructor calls that include arguments of type `dynamic`.</span></span>

<span data-ttu-id="3c28e-124">例如，下列宣告中 `testInstance` 的類型是 `ExampleClass`，而不是 `dynamic`：</span><span class="sxs-lookup"><span data-stu-id="3c28e-124">For example, the type of `testInstance` in the following declaration is `ExampleClass`, not `dynamic`:</span></span>

[!code-csharp[CsProgGuideTypes#52](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#52)]

<span data-ttu-id="3c28e-125">下一節＜轉換＞會顯示轉換範例。</span><span class="sxs-lookup"><span data-stu-id="3c28e-125">Conversion examples are shown in the following section, "Conversions."</span></span>

## <a name="conversions"></a><span data-ttu-id="3c28e-126">轉換</span><span class="sxs-lookup"><span data-stu-id="3c28e-126">Conversions</span></span>

<span data-ttu-id="3c28e-127">動態物件和其他類型間的轉換很簡單。</span><span class="sxs-lookup"><span data-stu-id="3c28e-127">Conversions between dynamic objects and other types are easy.</span></span> <span data-ttu-id="3c28e-128">因此，開發人員可以在動態和非動態行為之間進行切換。</span><span class="sxs-lookup"><span data-stu-id="3c28e-128">This enables the developer to switch between dynamic and non-dynamic behavior.</span></span>

<span data-ttu-id="3c28e-129">所有物件都能隱含轉換成動態類型，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3c28e-129">Any object can be converted to dynamic type implicitly, as shown in the following examples.</span></span>

[!code-csharp[CsProgGuideTypes#53](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#53)]

<span data-ttu-id="3c28e-130">相反地，隱含轉換可以動態套用至 `dynamic` 類型的任何運算式。</span><span class="sxs-lookup"><span data-stu-id="3c28e-130">Conversely, an implicit conversion can be dynamically applied to any expression of type `dynamic`.</span></span>

[!code-csharp[CsProgGuideTypes#54](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#54)]

## <a name="overload-resolution-with-arguments-of-type-dynamic"></a><span data-ttu-id="3c28e-131">dynamic 類型引數的多載解析</span><span class="sxs-lookup"><span data-stu-id="3c28e-131">Overload resolution with arguments of type dynamic</span></span>

<span data-ttu-id="3c28e-132">如果方法呼叫中有一或多個引數的類型為 `dynamic`，或如果方法呼叫的接收端類型為 `dynamic`，則會在執行階段 (而不是編譯時期) 發生多載解析。</span><span class="sxs-lookup"><span data-stu-id="3c28e-132">Overload resolution occurs at run time instead of at compile time if one or more of the arguments in a method call have the type `dynamic`, or if the receiver of the method call is of type `dynamic`.</span></span> <span data-ttu-id="3c28e-133">在下列範例中，如果唯一可存取的 `exampleMethod2` 方法已定義為接受字串引數，則將 `d1` 作為引數傳送不會造成編譯器錯誤，但會造成執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3c28e-133">In the following example, if the only accessible `exampleMethod2` method is defined to take a string argument, sending `d1` as the argument does not cause a compiler error, but it does cause a run-time exception.</span></span> <span data-ttu-id="3c28e-134">多載解析會在執行階段失敗，因為 `d1` 的執行階段類型為 `int`，而 `exampleMethod2` 需要字串。</span><span class="sxs-lookup"><span data-stu-id="3c28e-134">Overload resolution fails at run time because the run-time type of `d1` is `int`, and `exampleMethod2` requires a string.</span></span>

[!code-csharp[CsProgGuideTypes#55](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#55)]

## <a name="dynamic-language-runtime"></a><span data-ttu-id="3c28e-135">Dynamic Language Runtime</span><span class="sxs-lookup"><span data-stu-id="3c28e-135">Dynamic language runtime</span></span>

<span data-ttu-id="3c28e-136">動態語言執行時間（DLR）是在 .NET Framework 4 中引進的 API。</span><span class="sxs-lookup"><span data-stu-id="3c28e-136">The dynamic language runtime (DLR) is an API that was introduced in .NET Framework 4.</span></span> <span data-ttu-id="3c28e-137">它提供的基礎結構支援 C# 中的 `dynamic` 類型，也支援實作 IronPython 和 IronRuby 之類的動態程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="3c28e-137">It provides the infrastructure that supports the `dynamic` type in C#, and also the implementation of dynamic programming languages such as IronPython and IronRuby.</span></span> <span data-ttu-id="3c28e-138">如需 DLR 的詳細資訊，請參閱 [Dynamic Language Runtime 概觀](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3c28e-138">For more information about the DLR, see [Dynamic Language Runtime Overview](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md).</span></span>

## <a name="com-interop"></a><span data-ttu-id="3c28e-139">COM Interop</span><span class="sxs-lookup"><span data-stu-id="3c28e-139">COM interop</span></span>

<span data-ttu-id="3c28e-140">C# 4 包含幾項功能，可改善與 COM API (例如 Office Automation API) 相互操作的體驗。</span><span class="sxs-lookup"><span data-stu-id="3c28e-140">C# 4 includes several features that improve the experience of interoperating with COM APIs such as the Office Automation APIs.</span></span> <span data-ttu-id="3c28e-141">這些改進包括使用 `dynamic` 類型，以及使用[具名和選擇性引數](../classes-and-structs/named-and-optional-arguments.md)。</span><span class="sxs-lookup"><span data-stu-id="3c28e-141">Among the improvements are the use of the `dynamic` type, and of [named and optional arguments](../classes-and-structs/named-and-optional-arguments.md).</span></span>

<span data-ttu-id="3c28e-142">許多 COM 方法允許針對引數類型和傳回型別進行變化，方法是將類型指定為 `object`。</span><span class="sxs-lookup"><span data-stu-id="3c28e-142">Many COM methods allow for variation in argument types and return type by designating the types as `object`.</span></span> <span data-ttu-id="3c28e-143">這需要對值進行明確轉型，才能與 C# 中的強型別變數配合使用。</span><span class="sxs-lookup"><span data-stu-id="3c28e-143">This has necessitated explicit casting of the values to coordinate with strongly typed variables in C#.</span></span> <span data-ttu-id="3c28e-144">如果您使用[-link （c # 編譯器選項）](../../language-reference/compiler-options/link-compiler-option.md)選項進行編譯，則引入型別可 `dynamic` 讓您將 COM 簽章中的出現次數視為 `object` 型別 `dynamic` ，進而避免大部分的轉換。</span><span class="sxs-lookup"><span data-stu-id="3c28e-144">If you compile by using the [-link (C# Compiler Options)](../../language-reference/compiler-options/link-compiler-option.md) option, the introduction of the `dynamic` type enables you to treat the occurrences of `object` in COM signatures as if they were of type `dynamic`, and thereby to avoid much of the casting.</span></span> <span data-ttu-id="3c28e-145">例如，下列陳述式將比較使用 `dynamic` 類型和不使用 `dynamic` 類型存取 Microsoft Office Excel 試算表中儲存格的方式。</span><span class="sxs-lookup"><span data-stu-id="3c28e-145">For example, the following statements contrast how you access a cell in a Microsoft Office Excel spreadsheet with the `dynamic` type and without the `dynamic` type.</span></span>

[!code-csharp[csOfficeWalkthrough#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#12)]

[!code-csharp[csOfficeWalkthrough#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#13)]

## <a name="related-topics"></a><span data-ttu-id="3c28e-146">相關主題</span><span class="sxs-lookup"><span data-stu-id="3c28e-146">Related topics</span></span>

|<span data-ttu-id="3c28e-147">標題</span><span class="sxs-lookup"><span data-stu-id="3c28e-147">Title</span></span>|<span data-ttu-id="3c28e-148">描述</span><span class="sxs-lookup"><span data-stu-id="3c28e-148">Description</span></span>|
|-----------|-----------------|
|[<span data-ttu-id="3c28e-149">動態</span><span class="sxs-lookup"><span data-stu-id="3c28e-149">dynamic</span></span>](../../language-reference/builtin-types/reference-types.md)|<span data-ttu-id="3c28e-150">說明如何使用 `dynamic` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="3c28e-150">Describes the usage of the `dynamic` keyword.</span></span>|
|[<span data-ttu-id="3c28e-151">動態語言執行時間總覽</span><span class="sxs-lookup"><span data-stu-id="3c28e-151">Dynamic Language Runtime Overview</span></span>](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)|<span data-ttu-id="3c28e-152">提供 DLR 概觀，DLR 是在 Common Language Runtime (CLR) 中新增一組動態語言服務的執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="3c28e-152">Provides an overview of the DLR, which is a runtime environment that adds a set of services for dynamic languages to the common language runtime (CLR).</span></span>|
|[<span data-ttu-id="3c28e-153">逐步解說：建立和使用動態物件</span><span class="sxs-lookup"><span data-stu-id="3c28e-153">Walkthrough: Creating and Using Dynamic Objects</span></span>](walkthrough-creating-and-using-dynamic-objects.md)|<span data-ttu-id="3c28e-154">針對建立自訂動態物件及建立存取 `IronPython` 程式庫的專案，提供逐步指示。</span><span class="sxs-lookup"><span data-stu-id="3c28e-154">Provides step-by-step instructions for creating a custom dynamic object and for creating a project that accesses an `IronPython` library.</span></span>|
|[<span data-ttu-id="3c28e-155">如何使用 C# 功能存取 Office Interop 物件</span><span class="sxs-lookup"><span data-stu-id="3c28e-155">How to access Office interop objects by using C# features</span></span>](../interop/how-to-access-office-onterop-objects.md)|<span data-ttu-id="3c28e-156">示範如何建立使用具名和選擇性引數、`dynamic` 類型，以及其他可簡化 Office API 物件存取之增強功能的專案。</span><span class="sxs-lookup"><span data-stu-id="3c28e-156">Demonstrates how to create a project that uses named and optional arguments, the `dynamic` type, and other enhancements that simplify access to Office API objects.</span></span>|

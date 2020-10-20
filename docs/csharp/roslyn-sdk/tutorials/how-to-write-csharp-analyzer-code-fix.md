---
title: 教學課程：撰寫您的第一個分析器和程式碼修正
description: 本教學課程提供 使用 .NET Compiler SDK (Roslyn API) 來建置分析器和程式碼修正的逐步指示。
ms.date: 08/01/2018
ms.custom: mvc
ms.openlocfilehash: 33c00e90d768021e36a7987be0ddd7daec4cfcec
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224045"
---
# <a name="tutorial-write-your-first-analyzer-and-code-fix"></a><span data-ttu-id="bc77b-103">教學課程：撰寫您的第一個分析器和程式碼修正</span><span class="sxs-lookup"><span data-stu-id="bc77b-103">Tutorial: Write your first analyzer and code fix</span></span>

<span data-ttu-id="bc77b-104">.NET Compiler Platform SDK 可為您提供必要的工具，用以建立以 C# 或 Visual Basic 程式碼為目標的自訂警告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-104">The .NET Compiler Platform SDK provides the tools you need to create custom warnings that target C# or Visual Basic code.</span></span> <span data-ttu-id="bc77b-105">您的**分析器**包含可辨識違反規則的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-105">Your **analyzer** contains code that recognizes violations of your rule.</span></span> <span data-ttu-id="bc77b-106">您的**程式碼修正**包含可修正違規的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-106">Your **code fix** contains the code that fixes the violation.</span></span> <span data-ttu-id="bc77b-107">您所實作的規則可以是程式碼結構、編碼樣式、命名慣例等任何項目。</span><span class="sxs-lookup"><span data-stu-id="bc77b-107">The rules you implement can be anything from code structure to coding style to naming conventions and more.</span></span> <span data-ttu-id="bc77b-108">.NET Compiler Platform 可提供開發人員在撰寫程式碼時執行分析所需的架構，以及修正程式碼所需的所有 Visual Studio UI 功能：在編輯器中顯示波浪線、填入 Visual Studio 錯誤清單、建立「燈泡」建議，以及顯示建議修正的各式預覽。</span><span class="sxs-lookup"><span data-stu-id="bc77b-108">The .NET Compiler Platform provides the framework for running analysis as developers are writing code, and all the Visual Studio UI features for fixing code: showing squiggles in the editor, populating the Visual Studio Error List, creating the "light bulb" suggestions and showing the rich preview of the suggested fixes.</span></span>

<span data-ttu-id="bc77b-109">在本教學課程中，您將探索如何使用 Roslyn API 建立**分析器**和隨附的**程式碼修正**。</span><span class="sxs-lookup"><span data-stu-id="bc77b-109">In this tutorial, you'll explore the creation of an **analyzer** and an accompanying **code fix** using the Roslyn APIs.</span></span> <span data-ttu-id="bc77b-110">分析器是執行原始程式碼分析並向使用者報告問題的方式之一。</span><span class="sxs-lookup"><span data-stu-id="bc77b-110">An analyzer is a way to perform source code analysis and report a problem to the user.</span></span> <span data-ttu-id="bc77b-111">分析器也可以選擇性地提供程式碼修正，以顯示對使用者的原始程式碼所做的修改。</span><span class="sxs-lookup"><span data-stu-id="bc77b-111">Optionally, an analyzer can also provide a code fix that represents a modification to the user's source code.</span></span> <span data-ttu-id="bc77b-112">本教學課程所建立的分析器會尋找可使用 `const` 修飾詞來宣告、但並未這麼做的區域變數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-112">This tutorial creates an analyzer that finds local variable declarations that could be declared using the `const` modifier but are not.</span></span> <span data-ttu-id="bc77b-113">隨附的程式碼修正會修改這些宣告，而新增 `const` 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="bc77b-113">The accompanying code fix modifies those declarations to add the `const` modifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc77b-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc77b-114">Prerequisites</span></span>

- <span data-ttu-id="bc77b-115">[Visual Studio 2019](https://www.visualstudio.com/downloads) 16.7 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="bc77b-115">[Visual Studio 2019](https://www.visualstudio.com/downloads) version 16.7 or later</span></span>

<span data-ttu-id="bc77b-116">您必須透過 Visual Studio 安裝程式安裝 **.NET COMPILER PLATFORM SDK** ：</span><span class="sxs-lookup"><span data-stu-id="bc77b-116">You'll need to install the **.NET Compiler Platform SDK** via the Visual Studio Installer:</span></span>

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

<span data-ttu-id="bc77b-117">建立和驗證您的分析器時須執行幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="bc77b-117">There are several steps to creating and validating your analyzer:</span></span>

1. <span data-ttu-id="bc77b-118">建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-118">Create the solution.</span></span>
1. <span data-ttu-id="bc77b-119">註冊的分析器名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="bc77b-119">Register the analyzer name and description.</span></span>
1. <span data-ttu-id="bc77b-120">報告分析器警告和建議。</span><span class="sxs-lookup"><span data-stu-id="bc77b-120">Report analyzer warnings and recommendations.</span></span>
1. <span data-ttu-id="bc77b-121">實作接受建議的程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-121">Implement the code fix to accept recommendations.</span></span>
1. <span data-ttu-id="bc77b-122">透過單元測試來改善分析。</span><span class="sxs-lookup"><span data-stu-id="bc77b-122">Improve the analysis through unit tests.</span></span>

## <a name="explore-the-analyzer-template"></a><span data-ttu-id="bc77b-123">瀏覽分析器範本</span><span class="sxs-lookup"><span data-stu-id="bc77b-123">Explore the analyzer template</span></span>

<span data-ttu-id="bc77b-124">您的分析器會向使用者報告可轉換成區域常數的任何區域變數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-124">Your analyzer reports to the user any local variable declarations that can be converted to local constants.</span></span> <span data-ttu-id="bc77b-125">例如，請參考下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bc77b-125">For example, consider the following code:</span></span>

```csharp
int x = 0;
Console.WriteLine(x);
```

<span data-ttu-id="bc77b-126">在上述程式碼中，會為 `x` 指派常數值，且一律不會修改。</span><span class="sxs-lookup"><span data-stu-id="bc77b-126">In the code above, `x` is assigned a constant value and is never modified.</span></span> <span data-ttu-id="bc77b-127">此值可使用 `const` 修飾詞來宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-127">It can be declared using the `const` modifier:</span></span>

```csharp
const int x = 0;
Console.WriteLine(x);
```

<span data-ttu-id="bc77b-128">其中涉及用以判斷變數是否可設為常數的分析，這需要進行語法分析、初始設定式運算式的常數分析，和資料流程分析，以確保一律不會寫入變數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-128">The analysis to determine whether a variable can be made constant is involved, requiring syntactic analysis, constant analysis of the initializer expression and dataflow analysis to ensure that the variable is never written to.</span></span> <span data-ttu-id="bc77b-129">.NET Compiler Platform 所提供的 API 可讓您更輕鬆地執行這項分析。</span><span class="sxs-lookup"><span data-stu-id="bc77b-129">The .NET Compiler Platform provides APIs that make it easier to perform this analysis.</span></span> <span data-ttu-id="bc77b-130">第一個步驟是建立新的 C# **具有程式碼修正的分析器**專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-130">The first step is to create a new C# **Analyzer with code fix** project.</span></span>

- <span data-ttu-id="bc77b-131">在 Visual Studio 中選擇 [檔案] > [新增] > [專案...]\*\*\*\*，以顯示 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bc77b-131">In Visual Studio, choose **File > New > Project...** to display the New Project dialog.</span></span>
- <span data-ttu-id="bc77b-132">在 [Visual C# > 擴充性]\*\*\*\* 下方，選擇 [具有程式碼修正的分析器 (.NET Standard)]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="bc77b-132">Under **Visual C# > Extensibility**, choose **Analyzer with code fix (.NET Standard)**.</span></span>
- <span data-ttu-id="bc77b-133">將您的專案命名為 "**MakeConst**"，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bc77b-133">Name your project "**MakeConst**" and click OK.</span></span>

<span data-ttu-id="bc77b-134">具有程式碼修正範本的分析器會建立三個專案：一個包含分析器和程式碼修正，第二個是單元測試專案，第三個則是 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-134">The analyzer with code fix template creates three projects: one contains the analyzer and code fix, the second is a unit test project, and the third is the VSIX project.</span></span> <span data-ttu-id="bc77b-135">預設啟始專案為 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-135">The default startup project is the VSIX project.</span></span> <span data-ttu-id="bc77b-136">按 <kbd>F5</kbd> 以啟動 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-136">Press <kbd>F5</kbd> to start the VSIX project.</span></span> <span data-ttu-id="bc77b-137">這會啟動已載入新分析器的第二個 Visual Studio 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bc77b-137">This starts a second instance of Visual Studio that has loaded your new analyzer.</span></span>

> [!TIP]
> <span data-ttu-id="bc77b-138">當您執行分析器時，您會啟動 Visual Studio 的第二個複本。</span><span class="sxs-lookup"><span data-stu-id="bc77b-138">When you run your analyzer, you start a second copy of Visual Studio.</span></span> <span data-ttu-id="bc77b-139">此複本會使用不同的登錄區來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="bc77b-139">This second copy uses a different registry hive to store settings.</span></span> <span data-ttu-id="bc77b-140">這可讓您區分兩個 Visual Studio 複本中的的視覺化設定。</span><span class="sxs-lookup"><span data-stu-id="bc77b-140">That enables you to differentiate the visual settings in the two copies of Visual Studio.</span></span> <span data-ttu-id="bc77b-141">您可以挑選不同的佈景主題，用於 Visual Studio 的實驗性執行。</span><span class="sxs-lookup"><span data-stu-id="bc77b-141">You can pick a different theme for the experimental run of Visual Studio.</span></span> <span data-ttu-id="bc77b-142">此外，請勿使用 Visual Studio 的實驗性執行漫遊您的設定或登入 Visual Studio 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc77b-142">In addition, don't roam your settings or login to your Visual Studio account using the experimental run of Visual Studio.</span></span> <span data-ttu-id="bc77b-143">設定會因此而不同。</span><span class="sxs-lookup"><span data-stu-id="bc77b-143">That keeps the settings different.</span></span>

<span data-ttu-id="bc77b-144">在您剛開始 Visual Studio 的第二個實例中，建立新的 c # 主控台應用程式專案 (.NET Core 或 .NET Framework 專案可運作--分析器可在來源層級運作。 ) 將滑鼠停留在標記上的波浪底線，並顯示分析器所提供的警告文字。</span><span class="sxs-lookup"><span data-stu-id="bc77b-144">In the second Visual Studio instance that you just started, create a new C# Console Application project (either .NET Core or .NET Framework project will work -- analyzers work at the source level.) Hover over the token with a wavy underline, and the warning text provided by an analyzer appears.</span></span>

<span data-ttu-id="bc77b-145">範本會建立分析器，以針對每個在類型名稱中包含小寫字母的類型宣告回報警告，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-145">The template creates an analyzer that reports a warning on each type declaration where the type name contains lowercase letters, as shown in the following figure:</span></span>

![報告警告的分析器](media/how-to-write-csharp-analyzer-code-fix/report-warning.png)

<span data-ttu-id="bc77b-147">範本也會提供程式碼修正，以將任何包含小寫字元的類型名稱全部變更為大寫。</span><span class="sxs-lookup"><span data-stu-id="bc77b-147">The template also provides a code fix that changes any type name containing lower case characters to all upper case.</span></span> <span data-ttu-id="bc77b-148">您可以按一下隨警告顯示的燈泡，以查看建議的變更。</span><span class="sxs-lookup"><span data-stu-id="bc77b-148">You can click on the light bulb displayed with the warning to see the suggested changes.</span></span> <span data-ttu-id="bc77b-149">若接受建議的變更，即會在解決方案中將類型名稱和所有參考更新為該類型。</span><span class="sxs-lookup"><span data-stu-id="bc77b-149">Accepting the suggested changes updates the type name and all references to that type in the solution.</span></span> <span data-ttu-id="bc77b-150">您已了解作用中的初始分析器，現在請關閉第二個 Visual Studio 執行個體，並返回分析器專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-150">Now that you've seen the initial analyzer in action, close the second Visual Studio instance and return to your analyzer project.</span></span>

<span data-ttu-id="bc77b-151">您不需要啟動 Visual Studio 的第二個複本，並建立新的程式碼來測試分析器中的每一項變更。</span><span class="sxs-lookup"><span data-stu-id="bc77b-151">You don't have to start a second copy of Visual Studio and create new code to test every change in your analyzer.</span></span> <span data-ttu-id="bc77b-152">範本也會為您建立單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-152">The template also creates a unit test project for you.</span></span> <span data-ttu-id="bc77b-153">該專案包含兩項測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-153">That project contains two tests.</span></span> <span data-ttu-id="bc77b-154">`TestMethod1` 顯示會分析程式碼而不觸發診斷的一般測試格式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-154">`TestMethod1` shows the typical format of a test that analyzes code without triggering a diagnostic.</span></span> <span data-ttu-id="bc77b-155">`TestMethod2` 顯示會觸發程序然後套用建議程式碼修正的測試格式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-155">`TestMethod2` shows the format of a test that triggers a diagnostic, and then applies a suggested code fix.</span></span> <span data-ttu-id="bc77b-156">當您建置分析器和程式碼修正時，您會為不同的程式碼結構撰寫測試，以確認您的工作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-156">As you build your analyzer and code fix, you'll write tests for different code structures to verify your work.</span></span> <span data-ttu-id="bc77b-157">分析器的單元測試會比使用 Visual Studio 以互動方式測試快得多。</span><span class="sxs-lookup"><span data-stu-id="bc77b-157">Unit tests for analyzers are much quicker than testing them interactively with Visual Studio.</span></span>

> [!TIP]
> <span data-ttu-id="bc77b-158">當您知道哪些程式碼建構應該和不應觸發分析器時，分析器單元測試會是很棒的工具。</span><span class="sxs-lookup"><span data-stu-id="bc77b-158">Analyzer unit tests are a great tool when you know what code constructs should and shouldn't trigger your analyzer.</span></span> <span data-ttu-id="bc77b-159">在 Visual Studio 的另一個複本中載入您的分析器，可極有效地瀏覽和尋找您可能未考量到的建構。</span><span class="sxs-lookup"><span data-stu-id="bc77b-159">Loading your analyzer in another copy of Visual Studio is a great tool to explore and find constructs you may not have thought about yet.</span></span>

## <a name="create-analyzer-registrations"></a><span data-ttu-id="bc77b-160">建立分析器註冊</span><span class="sxs-lookup"><span data-stu-id="bc77b-160">Create analyzer registrations</span></span>

<span data-ttu-id="bc77b-161">範本會在 **MakeConstAnalyzer.cs** 檔案中建立初始 `DiagnosticAnalyzer` 類別，。</span><span class="sxs-lookup"><span data-stu-id="bc77b-161">The template creates the initial `DiagnosticAnalyzer` class, in the **MakeConstAnalyzer.cs** file.</span></span> <span data-ttu-id="bc77b-162">此初始分析器會顯示每個分析器的兩個重要屬性。</span><span class="sxs-lookup"><span data-stu-id="bc77b-162">This initial analyzer shows two important properties of every analyzer.</span></span>

- <span data-ttu-id="bc77b-163">每個診斷分析器都必須提供 `[DiagnosticAnalyzer]` 屬性，以說明它據以運作的語言。</span><span class="sxs-lookup"><span data-stu-id="bc77b-163">Every diagnostic analyzer must provide a `[DiagnosticAnalyzer]` attribute that describes the language it operates on.</span></span>
- <span data-ttu-id="bc77b-164">每個診斷分析器都必須衍生自 <xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer> 類別。</span><span class="sxs-lookup"><span data-stu-id="bc77b-164">Every diagnostic analyzer must derive from the <xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer> class.</span></span>

<span data-ttu-id="bc77b-165">範本也會顯示屬於任何分析器的基本功能：</span><span class="sxs-lookup"><span data-stu-id="bc77b-165">The template also shows the basic features that are part of any analyzer:</span></span>

1. <span data-ttu-id="bc77b-166">註冊動作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-166">Register actions.</span></span> <span data-ttu-id="bc77b-167">動作代表應觸發分析器以檢查程式碼是否違規的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="bc77b-167">The actions represent code changes that should trigger your analyzer to examine code for violations.</span></span> <span data-ttu-id="bc77b-168">當 Visual Studio 偵測到與已註冊的動作相符的程式碼編輯時，就會呼叫分析器已註冊的方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-168">When Visual Studio detects code edits that match a registered action, it calls your analyzer's registered method.</span></span>
1. <span data-ttu-id="bc77b-169">更新診斷。</span><span class="sxs-lookup"><span data-stu-id="bc77b-169">Create diagnostics.</span></span> <span data-ttu-id="bc77b-170">您的分析器在偵測到違規時，將會建立 Visual Studio 用來向使用者通報違規情事的診斷物件。</span><span class="sxs-lookup"><span data-stu-id="bc77b-170">When your analyzer detects a violation, it creates a diagnostic object that Visual Studio uses to notify the user of the violation.</span></span>

<span data-ttu-id="bc77b-171">您可以在 <xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer.Initialize(Microsoft.CodeAnalysis.Diagnostics.AnalysisContext)?displayProperty=nameWithType> 方法的覆寫中註冊動作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-171">You register actions in your override of <xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer.Initialize(Microsoft.CodeAnalysis.Diagnostics.AnalysisContext)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="bc77b-172">在本教學課程中，您會瀏覽**語法節點**以尋找區域宣告，並查看有哪些含有常數值。</span><span class="sxs-lookup"><span data-stu-id="bc77b-172">In this tutorial, you'll visit **syntax nodes** looking for local declarations, and see which of those have constant values.</span></span> <span data-ttu-id="bc77b-173">如果某個宣告可能是常數，分析器即會建立並報告診斷。</span><span class="sxs-lookup"><span data-stu-id="bc77b-173">If a declaration could be constant, your analyzer will create and report a diagnostic.</span></span>

<span data-ttu-id="bc77b-174">第一個步驟是更新註冊常數和 `Initialize` 方法，讓這些常數表示您的「設為常數」分析器。</span><span class="sxs-lookup"><span data-stu-id="bc77b-174">The first step is to update the registration constants and `Initialize` method so these constants indicate your "Make Const" analyzer.</span></span> <span data-ttu-id="bc77b-175">大部分的字串常數都會定義在字串資源檔中。</span><span class="sxs-lookup"><span data-stu-id="bc77b-175">Most of the string constants are defined in the string resource file.</span></span> <span data-ttu-id="bc77b-176">您應遵循該作法，以方便當地語系化。</span><span class="sxs-lookup"><span data-stu-id="bc77b-176">You should follow that practice for easier localization.</span></span> <span data-ttu-id="bc77b-177">開啟 **MakeConst** 分析器專案的 **Resources.resx** 檔案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-177">Open the **Resources.resx** file for the **MakeConst** analyzer project.</span></span> <span data-ttu-id="bc77b-178">這會顯示資源編輯器。</span><span class="sxs-lookup"><span data-stu-id="bc77b-178">This displays the resource editor.</span></span> <span data-ttu-id="bc77b-179">更新字串資源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-179">Update the string resources as follows:</span></span>

- <span data-ttu-id="bc77b-180">將 `AnalyzerTitle` 變更為「變數可設為常數」。</span><span class="sxs-lookup"><span data-stu-id="bc77b-180">Change `AnalyzerTitle` to "Variable can be made constant".</span></span>
- <span data-ttu-id="bc77b-181">將 `AnalyzerMessageFormat` 變更為「可設為常數」。</span><span class="sxs-lookup"><span data-stu-id="bc77b-181">Change `AnalyzerMessageFormat` to "Can be made constant".</span></span>
- <span data-ttu-id="bc77b-182">將 `AnalyzerDescription` 變更為「設為常數」。</span><span class="sxs-lookup"><span data-stu-id="bc77b-182">Change `AnalyzerDescription` to "Make Constant".</span></span>

<span data-ttu-id="bc77b-183">此外，請將 [存取修飾詞]\*\*\*\* 下拉式清單變更為 `public`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-183">Also, change the **Access Modifier** drop-down to `public`.</span></span> <span data-ttu-id="bc77b-184">這可以讓這些常數在單元測試中更易於使用。</span><span class="sxs-lookup"><span data-stu-id="bc77b-184">That makes it easier to use these constants in unit tests.</span></span> <span data-ttu-id="bc77b-185">完成作業後，資源編輯器應會如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-185">When you have finished, the resource editor should appear as follow figure shows:</span></span>

![更新字串資源](media/how-to-write-csharp-analyzer-code-fix/update-string-resources.png)

<span data-ttu-id="bc77b-187">其餘變更位於分析器檔案中。</span><span class="sxs-lookup"><span data-stu-id="bc77b-187">The remaining changes are in the analyzer file.</span></span> <span data-ttu-id="bc77b-188">請在 Visual Studio 中開啟 **MakeConstAnalyzer.cs**。</span><span class="sxs-lookup"><span data-stu-id="bc77b-188">Open **MakeConstAnalyzer.cs** in Visual Studio.</span></span> <span data-ttu-id="bc77b-189">將已註冊的動作從以符號為目標變更為以語法為目標。</span><span class="sxs-lookup"><span data-stu-id="bc77b-189">Change the registered action from one that acts on symbols to one that acts on syntax.</span></span> <span data-ttu-id="bc77b-190">在 `MakeConstAnalyzerAnalyzer.Initialize` 方法中，找出符號的動作是以哪一行註冊的：</span><span class="sxs-lookup"><span data-stu-id="bc77b-190">In the `MakeConstAnalyzerAnalyzer.Initialize` method, find the line that registers the action on symbols:</span></span>

```csharp
context.RegisterSymbolAction(AnalyzeSymbol, SymbolKind.NamedType);
```

<span data-ttu-id="bc77b-191">將其取代為以下這一行：</span><span class="sxs-lookup"><span data-stu-id="bc77b-191">Replace it with the following line:</span></span>

[!code-csharp[Register the node action](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstAnalyzer.cs#RegisterNodeAction "Register a node action")]

<span data-ttu-id="bc77b-192">完成此變更後，您可以刪除 `AnalyzeSymbol` 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-192">After that change, you can delete the `AnalyzeSymbol` method.</span></span> <span data-ttu-id="bc77b-193">此分析器會檢查 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.LocalDeclarationStatement?displayProperty=nameWithType>，而非 <xref:Microsoft.CodeAnalysis.SymbolKind.NamedType?displayProperty=nameWithType> 陳述式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-193">This analyzer examines <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.LocalDeclarationStatement?displayProperty=nameWithType>, not <xref:Microsoft.CodeAnalysis.SymbolKind.NamedType?displayProperty=nameWithType> statements.</span></span> <span data-ttu-id="bc77b-194">請注意，`AnalyzeNode` 的下方有紅色波浪線。</span><span class="sxs-lookup"><span data-stu-id="bc77b-194">Notice that `AnalyzeNode` has red squiggles under it.</span></span> <span data-ttu-id="bc77b-195">您剛才新增的程式碼會參考尚未宣告的 `AnalyzeNode` 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-195">The code you just added references an `AnalyzeNode` method that hasn't been declared.</span></span> <span data-ttu-id="bc77b-196">請使用下列程式碼宣告該方法：</span><span class="sxs-lookup"><span data-stu-id="bc77b-196">Declare that method using the following code:</span></span>

```csharp
private void AnalyzeNode(SyntaxNodeAnalysisContext context)
{
}
```

<span data-ttu-id="bc77b-197">在 **MakeConstAnalyzer.cs** 中將 `Category` 變更為 "Usage"，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-197">Change the `Category` to "Usage" in **MakeConstAnalyzer.cs** as shown in the following code:</span></span>

```csharp
private const string Category = "Usage";
```

## <a name="find-local-declarations-that-could-be-const"></a><span data-ttu-id="bc77b-198">尋找可能是常數的區域宣告</span><span class="sxs-lookup"><span data-stu-id="bc77b-198">Find local declarations that could be const</span></span>

<span data-ttu-id="bc77b-199">現在我們將撰寫 `AnalyzeNode` 方法的第一個版本。</span><span class="sxs-lookup"><span data-stu-id="bc77b-199">It's time to write the first version of the `AnalyzeNode` method.</span></span> <span data-ttu-id="bc77b-200">它會尋找可能是 `const`、但實際並不是的單一區域宣告，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-200">It should look for a single local declaration that could be `const` but is not, like the following code:</span></span>

```csharp
int x = 0;
Console.WriteLine(x);
```

<span data-ttu-id="bc77b-201">第一個步驟是尋找區域宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-201">The first step is to find local declarations.</span></span> <span data-ttu-id="bc77b-202">在 **MakeConstAnalyzer.cs** 中將下列程式碼新增至 `AnalyzeNode`：</span><span class="sxs-lookup"><span data-stu-id="bc77b-202">Add the following code to `AnalyzeNode` in **MakeConstAnalyzer.cs**:</span></span>

```csharp
var localDeclaration = (LocalDeclarationStatementSyntax)context.Node;
```

<span data-ttu-id="bc77b-203">這項轉換一定會成功，因為您的分析器已註冊區域宣告的變更，而且也僅限於區域宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-203">This cast always succeeds because your analyzer registered for changes to local declarations, and only local declarations.</span></span> <span data-ttu-id="bc77b-204">沒有其他節點類型會觸發對 `AnalyzeNode` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="bc77b-204">No other node type triggers a call to your `AnalyzeNode` method.</span></span> <span data-ttu-id="bc77b-205">接下來，請檢查宣告中是否有任何 `const` 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="bc77b-205">Next, check the declaration for any `const` modifiers.</span></span> <span data-ttu-id="bc77b-206">如有發現，請立即傳回。</span><span class="sxs-lookup"><span data-stu-id="bc77b-206">If you find them, return immediately.</span></span> <span data-ttu-id="bc77b-207">下列程式碼會尋找區域宣告上的任何 `const` 修飾詞：</span><span class="sxs-lookup"><span data-stu-id="bc77b-207">The following code looks for any `const` modifiers on the local declaration:</span></span>

```csharp
// make sure the declaration isn't already const:
if (localDeclaration.Modifiers.Any(SyntaxKind.ConstKeyword))
{
    return;
}
```

<span data-ttu-id="bc77b-208">最後，您必須確認變數有可能是 `const`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-208">Finally, you need to check that the variable could be `const`.</span></span> <span data-ttu-id="bc77b-209">其意義是確定變數在初始化後未曾進行指派。</span><span class="sxs-lookup"><span data-stu-id="bc77b-209">That means making sure it is never assigned after it is initialized.</span></span>

<span data-ttu-id="bc77b-210">您將使用 <xref:Microsoft.CodeAnalysis.Diagnostics.SyntaxNodeAnalysisContext> 執行某種語意分析。</span><span class="sxs-lookup"><span data-stu-id="bc77b-210">You'll perform some semantic analysis using the <xref:Microsoft.CodeAnalysis.Diagnostics.SyntaxNodeAnalysisContext>.</span></span> <span data-ttu-id="bc77b-211">您可以使用 `context` 引數判斷區域變數宣告是否可設為 `const`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-211">You use the `context` argument to determine whether the local variable declaration can be made `const`.</span></span> <span data-ttu-id="bc77b-212"><xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType>代表單一原始程式檔中的所有語義資訊。</span><span class="sxs-lookup"><span data-stu-id="bc77b-212">A <xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType> represents all of semantic information in a single source file.</span></span> <span data-ttu-id="bc77b-213">您可以在說明[語意模型](../work-with-semantics.md)的文章中深入了解相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bc77b-213">You can learn more in the article that covers [semantic models](../work-with-semantics.md).</span></span> <span data-ttu-id="bc77b-214">您將使用 <xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType> 執行區域宣告陳述式的資料流程分析。</span><span class="sxs-lookup"><span data-stu-id="bc77b-214">You'll use the <xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType> to perform data flow analysis on the local declaration statement.</span></span> <span data-ttu-id="bc77b-215">然後，您可以使用此資料流程分析的結果，確保區域變數不會在其他任何位置以新值寫入。</span><span class="sxs-lookup"><span data-stu-id="bc77b-215">Then, you use the results of this data flow analysis to ensure that the local variable isn't written with a new value anywhere else.</span></span> <span data-ttu-id="bc77b-216">呼叫 <xref:Microsoft.CodeAnalysis.ModelExtensions.GetDeclaredSymbol%2A> 擴充方法以擷取變數的 <xref:Microsoft.CodeAnalysis.ILocalSymbol>，並確認它並未包含於資料流程分析的 <xref:Microsoft.CodeAnalysis.DataFlowAnalysis.WrittenOutside%2A?displayProperty=nameWithType> 集合中。</span><span class="sxs-lookup"><span data-stu-id="bc77b-216">Call the <xref:Microsoft.CodeAnalysis.ModelExtensions.GetDeclaredSymbol%2A> extension method to retrieve the <xref:Microsoft.CodeAnalysis.ILocalSymbol> for the variable and check that it isn't contained with the <xref:Microsoft.CodeAnalysis.DataFlowAnalysis.WrittenOutside%2A?displayProperty=nameWithType> collection of the data flow analysis.</span></span> <span data-ttu-id="bc77b-217">將下列程式碼新增至 `AnalyzeNode` 方法的結尾：</span><span class="sxs-lookup"><span data-stu-id="bc77b-217">Add the following code to the end of the `AnalyzeNode` method:</span></span>

```csharp
// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

// Retrieve the local symbol for each variable in the local declaration
// and ensure that it is not written outside of the data flow analysis region.
var variable = localDeclaration.Declaration.Variables.Single();
var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
{
    return;
}
```

<span data-ttu-id="bc77b-218">剛才新增的程式碼可確保變數不會修改，因而可設為 `const`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-218">The code just added ensures that the variable isn't modified, and can therefore be made `const`.</span></span> <span data-ttu-id="bc77b-219">現在我們將引發診斷。</span><span class="sxs-lookup"><span data-stu-id="bc77b-219">It's time to raise the diagnostic.</span></span> <span data-ttu-id="bc77b-220">請在 `AnalyzeNode` 中新增下列程式碼，作為最後一行：</span><span class="sxs-lookup"><span data-stu-id="bc77b-220">Add the following code as the last line in `AnalyzeNode`:</span></span>

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, context.Node.GetLocation()));
```

<span data-ttu-id="bc77b-221">您可以按 <kbd>F5</kbd> 執行您的分析器，以查看進度。</span><span class="sxs-lookup"><span data-stu-id="bc77b-221">You can check your progress by pressing <kbd>F5</kbd> to run your analyzer.</span></span> <span data-ttu-id="bc77b-222">您可以載入先前建立的主控台應用程式，然後新增下列測試程式碼：</span><span class="sxs-lookup"><span data-stu-id="bc77b-222">You can load the console application you created earlier and then add the following test code:</span></span>

```csharp
int x = 0;
Console.WriteLine(x);
```

<span data-ttu-id="bc77b-223">此時應該會出現燈泡，且您的分析器應會報告診斷。</span><span class="sxs-lookup"><span data-stu-id="bc77b-223">The light bulb should appear, and your analyzer should report a diagnostic.</span></span> <span data-ttu-id="bc77b-224">不過，燈泡仍使用範本產生的程式碼修正，並指出它可以改為大寫。</span><span class="sxs-lookup"><span data-stu-id="bc77b-224">However, the light bulb still uses the template generated code fix, and tells you it can be made upper case.</span></span> <span data-ttu-id="bc77b-225">下一節會說明如何撰寫程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-225">The next section explains how to write the code fix.</span></span>

## <a name="write-the-code-fix"></a><span data-ttu-id="bc77b-226">撰寫程式碼修正</span><span class="sxs-lookup"><span data-stu-id="bc77b-226">Write the code fix</span></span>

<span data-ttu-id="bc77b-227">分析器可提供一或多個程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-227">An analyzer can provide one or more code fixes.</span></span> <span data-ttu-id="bc77b-228">程式碼修正可定義編輯，用以解決報告的問題。</span><span class="sxs-lookup"><span data-stu-id="bc77b-228">A code fix defines an edit that addresses the reported issue.</span></span> <span data-ttu-id="bc77b-229">對於您所建立的分析器，您可以提供插入 const 關鍵字的程式碼修正：</span><span class="sxs-lookup"><span data-stu-id="bc77b-229">For the analyzer that you created, you can provide a code fix that inserts the const keyword:</span></span>

```csharp
const int x = 0;
Console.WriteLine(x);
```

<span data-ttu-id="bc77b-230">使用者可從編輯器和 Visual Studio 中的燈泡 UI 加以選擇，並變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-230">The user chooses it from the light bulb UI in the editor and Visual Studio changes the code.</span></span>

<span data-ttu-id="bc77b-231">開啟範本所新增的 **MakeConstCodeFixProvider.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-231">Open the **MakeConstCodeFixProvider.cs** file added by the template.</span></span>  <span data-ttu-id="bc77b-232">此程式碼修正已連線到您的診斷分析器所產生的診斷識別碼，但尚未實作正確的程式碼轉換。</span><span class="sxs-lookup"><span data-stu-id="bc77b-232">This code fix is already wired up to the Diagnostic ID produced by your diagnostic analyzer, but it doesn't yet implement the right code transform.</span></span> <span data-ttu-id="bc77b-233">首先，您應移除某些範本程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-233">First you should remove some of the template code.</span></span> <span data-ttu-id="bc77b-234">請將標題字串變更為「設為常數」:</span><span class="sxs-lookup"><span data-stu-id="bc77b-234">Change the title string to "Make constant":</span></span>

[!code-csharp[Update the CodeFix title](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#CodeFixTitle "Update the CodeFix title")]

<span data-ttu-id="bc77b-235">接著，請刪除 `MakeUppercaseAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-235">Next, delete the `MakeUppercaseAsync` method.</span></span> <span data-ttu-id="bc77b-236">該方法已不適用。</span><span class="sxs-lookup"><span data-stu-id="bc77b-236">It no longer applies.</span></span>

<span data-ttu-id="bc77b-237">所有程式碼修正提供者皆衍生自 <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider>。</span><span class="sxs-lookup"><span data-stu-id="bc77b-237">All code fix providers derive from <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider>.</span></span> <span data-ttu-id="bc77b-238">它們全都會覆寫 <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider.RegisterCodeFixesAsync(Microsoft.CodeAnalysis.CodeFixes.CodeFixContext)?displayProperty=nameWithType>，以報告可用的程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-238">They all override <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider.RegisterCodeFixesAsync(Microsoft.CodeAnalysis.CodeFixes.CodeFixContext)?displayProperty=nameWithType> to report available code fixes.</span></span> <span data-ttu-id="bc77b-239">在 `RegisterCodeFixesAsync` 中，將您要搜尋的上階節點類型變更為符合診斷的 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax>：</span><span class="sxs-lookup"><span data-stu-id="bc77b-239">In `RegisterCodeFixesAsync`, change the ancestor node type you're searching for to a <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax> to match the diagnostic:</span></span>

[!code-csharp[Find local declaration node](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#FindDeclarationNode  "Find the local declaration node that raised the diagnostic")]

<span data-ttu-id="bc77b-240">接著，變更最後一行以註冊程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-240">Next, change the last line to register a code fix.</span></span> <span data-ttu-id="bc77b-241">您的修正將會建立在將 `const` 修飾詞新增至現有宣告後而產生的新文件：</span><span class="sxs-lookup"><span data-stu-id="bc77b-241">Your fix will create a new document that results from adding the `const` modifier to an existing declaration:</span></span>

[!code-csharp[Register the new code fix](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#RegisterCodeFix  "Register the new code fix")]

<span data-ttu-id="bc77b-242">在剛才新增程式碼中，您會在符號 `MakeConstAsync` 上看到紅色波浪線。</span><span class="sxs-lookup"><span data-stu-id="bc77b-242">You'll notice red squiggles in the code you just added on the symbol `MakeConstAsync`.</span></span> <span data-ttu-id="bc77b-243">請為 `MakeConstAsync` 新增宣告，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-243">Add a declaration for `MakeConstAsync` like the following code:</span></span>

```csharp
private async Task<Document> MakeConstAsync(Document document,
   LocalDeclarationStatementSyntax localDeclaration,
   CancellationToken cancellationToken)
{
}
```

<span data-ttu-id="bc77b-244">新的 `MakeConstAsync` 方法會將代表使用者來源檔案的 <xref:Microsoft.CodeAnalysis.Document> 轉換為新的 <xref:Microsoft.CodeAnalysis.Document>，此時其中包含 `const` 宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-244">Your new `MakeConstAsync` method will transform the <xref:Microsoft.CodeAnalysis.Document> representing the user's source file into a new <xref:Microsoft.CodeAnalysis.Document> that now contains a `const` declaration.</span></span>

<span data-ttu-id="bc77b-245">您可以建立要在宣告陳述式前面插入的新 `const` 關鍵字權杖。</span><span class="sxs-lookup"><span data-stu-id="bc77b-245">You create a new `const` keyword token to insert at the front of the declaration statement.</span></span> <span data-ttu-id="bc77b-246">請務必先從宣告陳述式的第一個權杖中移除任何前置邏輯，再將其附加至 `const` 權杖。</span><span class="sxs-lookup"><span data-stu-id="bc77b-246">Be careful to first remove any leading trivia from the first token of the declaration statement and attach it to the `const` token.</span></span> <span data-ttu-id="bc77b-247">將下列程式碼新增至 `MakeConstAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="bc77b-247">Add the following code to the `MakeConstAsync` method:</span></span>

[!code-csharp[Create a new const keyword token](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#CreateConstToken  "Create the new const keyword token")]

<span data-ttu-id="bc77b-248">接著，使用下列程式碼將 `const` 權杖新增宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-248">Next, add the `const` token to the declaration using the following code:</span></span>

```csharp
// Insert the const token into the modifiers list, creating a new modifiers list.
var newModifiers = trimmedLocal.Modifiers.Insert(0, constToken);
// Produce the new local declaration.
var newLocal = trimmedLocal
    .WithModifiers(newModifiers)
    .WithDeclaration(localDeclaration.Declaration);
```

<span data-ttu-id="bc77b-249">然後請將新的宣告格式化，以符合 C# 格式化規則。</span><span class="sxs-lookup"><span data-stu-id="bc77b-249">Next, format the new declaration to match C# formatting rules.</span></span> <span data-ttu-id="bc77b-250">將變更格式化以符合現有的程式碼，可產生更理想的體驗。</span><span class="sxs-lookup"><span data-stu-id="bc77b-250">Formatting your changes to match existing code creates a better experience.</span></span> <span data-ttu-id="bc77b-251">緊跟在現有程式碼後面新增下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="bc77b-251">Add the following statement immediately after the existing code:</span></span>

[!code-csharp[Format the new declaration](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#FormatLocal  "Format the new declaration")]

<span data-ttu-id="bc77b-252">此程式碼需要新的命名空間。</span><span class="sxs-lookup"><span data-stu-id="bc77b-252">A new namespace is required for this code.</span></span> <span data-ttu-id="bc77b-253">將下列指示詞新增 `using` 至檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="bc77b-253">Add the following `using` directive to the top of the file:</span></span>

```csharp
using Microsoft.CodeAnalysis.Formatting;
```

<span data-ttu-id="bc77b-254">最後一個步驟是進行編輯。</span><span class="sxs-lookup"><span data-stu-id="bc77b-254">The final step is to make your edit.</span></span> <span data-ttu-id="bc77b-255">此程序有三個步驟：</span><span class="sxs-lookup"><span data-stu-id="bc77b-255">There are three steps to this process:</span></span>

1. <span data-ttu-id="bc77b-256">取得現有文件的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-256">Get a handle to the existing document.</span></span>
1. <span data-ttu-id="bc77b-257">將現有宣告取代為新宣告，以建立新文件。</span><span class="sxs-lookup"><span data-stu-id="bc77b-257">Create a new document by replacing the existing declaration with the new declaration.</span></span>
1. <span data-ttu-id="bc77b-258">傳回新文件。</span><span class="sxs-lookup"><span data-stu-id="bc77b-258">Return the new document.</span></span>

<span data-ttu-id="bc77b-259">將下列程式碼新增至 `MakeConstAsync` 方法的結尾：</span><span class="sxs-lookup"><span data-stu-id="bc77b-259">Add the following code to the end of the `MakeConstAsync` method:</span></span>

[!code-csharp[replace the declaration](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#ReplaceDocument  "Generate a new document by replacing the declaration")]

<span data-ttu-id="bc77b-260">您的程式碼修正已可供試用。</span><span class="sxs-lookup"><span data-stu-id="bc77b-260">Your code fix is ready to try.</span></span>  <span data-ttu-id="bc77b-261">按下 <kbd>F5</kbd> 鍵，在 Visual Studio 的第二個實例中執行分析器專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-261">Press <kbd>F5</kbd> to run the analyzer project in a second instance of Visual Studio.</span></span> <span data-ttu-id="bc77b-262">在第二個 Visual Studio 執行個體中建立新的 C# 主控台應用程式專案，並將數個以常數值初始化的區域變數宣告新增至 Main 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-262">In the second Visual Studio instance, create a new C# Console Application project and add a few local variable declarations initialized with constant values to the Main method.</span></span> <span data-ttu-id="bc77b-263">您會看到系統將其報告為警告，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bc77b-263">You'll see that they are reported as warnings as below.</span></span>

![可設為常數警告](media/how-to-write-csharp-analyzer-code-fix/make-const-warning.png)

<span data-ttu-id="bc77b-265">您已完成許多進度。</span><span class="sxs-lookup"><span data-stu-id="bc77b-265">You've made a lot of progress.</span></span> <span data-ttu-id="bc77b-266">可設為 `const` 的宣告底下會出現波浪線。</span><span class="sxs-lookup"><span data-stu-id="bc77b-266">There are squiggles under the declarations that can be made `const`.</span></span> <span data-ttu-id="bc77b-267">但仍有工作尚待完成。</span><span class="sxs-lookup"><span data-stu-id="bc77b-267">But there is still work to do.</span></span> <span data-ttu-id="bc77b-268">如果您依序以 `i`、`j`、`k` 的順序將 `const` 新增至宣告，則可正常運作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-268">This works fine if you add `const` to the declarations starting with `i`, then `j` and finally `k`.</span></span> <span data-ttu-id="bc77b-269">但是，如果您以不同的順序從 `k` 開始新增 `const` 修飾詞，分析器將會產生錯誤：除非 `i` 和 `j` 皆已為 `const`，否則 `k` 無法宣告為 `const`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-269">But, if you add the `const` modifier in a different order, starting with `k`, your analyzer creates errors: `k` can't be declared `const`, unless `i` and `j` are both already `const`.</span></span> <span data-ttu-id="bc77b-270">您必須執行更多分析，以確保能夠以不同的方式讓變數完成宣告和初始化。</span><span class="sxs-lookup"><span data-stu-id="bc77b-270">You've got to do more analysis to ensure you handle the different ways variables can be declared and initialized.</span></span>

## <a name="build-data-driven-tests"></a><span data-ttu-id="bc77b-271">建置資料驅動型測試</span><span class="sxs-lookup"><span data-stu-id="bc77b-271">Build data driven tests</span></span>

<span data-ttu-id="bc77b-272">在可設為常數的宣告案例中，如果情況單純，您的分析器和程式碼修正就可正常運作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-272">Your analyzer and code fix work on a simple case of a single declaration that can be made const.</span></span> <span data-ttu-id="bc77b-273">但在許多宣告陳述式中，這項實作都有可能發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bc77b-273">There are numerous possible declaration statements where this implementation makes mistakes.</span></span> <span data-ttu-id="bc77b-274">您將使用範本所撰寫的單元測試程式庫，來處理這些案例。</span><span class="sxs-lookup"><span data-stu-id="bc77b-274">You'll address these cases by working with the unit test library written by the template.</span></span> <span data-ttu-id="bc77b-275">其速度會比重複開啟第二個 Visual Studio 複本快得多。</span><span class="sxs-lookup"><span data-stu-id="bc77b-275">It's much faster than repeatedly opening a second copy of Visual Studio.</span></span>

<span data-ttu-id="bc77b-276">在單元測試專案中開啟 **MakeConstUnitTests.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-276">Open the **MakeConstUnitTests.cs** file in the unit test project.</span></span> <span data-ttu-id="bc77b-277">範本依循分析器和程式碼修正單元測試的兩個常見模式，建立了兩項測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-277">The template created two tests that follow the two common patterns for an analyzer and code fix unit test.</span></span> <span data-ttu-id="bc77b-278">`TestMethod1` 顯示可確保分析器不會在不當時機報告診斷的測試模式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-278">`TestMethod1` shows the pattern for a test that ensures the analyzer doesn't report a diagnostic when it shouldn't.</span></span> <span data-ttu-id="bc77b-279">`TestMethod2` 顯示會報告診斷並執行程式碼修正的模式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-279">`TestMethod2` shows the pattern for reporting a diagnostic and running the code fix.</span></span>

<span data-ttu-id="bc77b-280">分析器絕大多數測試的程式碼都會遵循這兩種模式之一。</span><span class="sxs-lookup"><span data-stu-id="bc77b-280">The code for almost every test for your analyzer follows one of these two patterns.</span></span> <span data-ttu-id="bc77b-281">在第一個步驟中，您可以將這些測試修改為資料驅動型測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-281">For the first step, you can rework these tests as data driven tests.</span></span> <span data-ttu-id="bc77b-282">然後，只要新增字串常數以代表不同的測試輸入，即可輕易建立新的測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-282">Then, it will be easy to create new tests by adding new string constants to represent different test inputs.</span></span>

<span data-ttu-id="bc77b-283">為了提高效率，我們的第一個步驟是將兩個測試重構為資料驅動型測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-283">For efficiency, the first step is to refactor the two tests into data driven tests.</span></span> <span data-ttu-id="bc77b-284">然後，您只需要為每個新的測試定義幾個字串常數即可。</span><span class="sxs-lookup"><span data-stu-id="bc77b-284">Then, you only need to define a couple string constants for each new test.</span></span> <span data-ttu-id="bc77b-285">當您重構時，請將這兩種方法重新命名為更好的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc77b-285">While you are refactoring, rename both methods to better names.</span></span> <span data-ttu-id="bc77b-286">請將 `TestMethod1` 取代為確保不會引發任何診斷的這項測試：</span><span class="sxs-lookup"><span data-stu-id="bc77b-286">Replace `TestMethod1` with this test that ensures no diagnostic is raised:</span></span>

```csharp
[DataTestMethod]
[DataRow("")]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
{
    VerifyCSharpDiagnostic(testCode);
}
```

<span data-ttu-id="bc77b-287">您可以定義不應導致診斷觸發警告的任何程式碼片段，為這項測試建立新的資料列。</span><span class="sxs-lookup"><span data-stu-id="bc77b-287">You can create a new data row for this test by defining any code fragment that should not cause your diagnostic to trigger a warning.</span></span> <span data-ttu-id="bc77b-288">未針對來源程式碼片段觸發任何診斷時，就會傳遞此 `VerifyCSharpDiagnostic` 多載。</span><span class="sxs-lookup"><span data-stu-id="bc77b-288">This overload of `VerifyCSharpDiagnostic` passes when there are no diagnostics triggered for the source code fragment.</span></span>

<span data-ttu-id="bc77b-289">接著，請將 `TestMethod2` 取代為確保不會引發診斷的這項測試，以及為來源程式碼片段套用的程式碼修正：</span><span class="sxs-lookup"><span data-stu-id="bc77b-289">Next, replace `TestMethod2` with this test that ensures a diagnostic is raised and a code fix applied for the source code fragment:</span></span>

```csharp
[DataTestMethod]
[DataRow(LocalIntCouldBeConstant, LocalIntCouldBeConstantFixed, 10, 13)]
public void WhenDiagnosticIsRaisedFixUpdatesCode(
    string test,
    string fixTest,
    int line,
    int column)
{
    var expected = new DiagnosticResult
    {
        Id = MakeConstAnalyzer.DiagnosticId,
        Message = new LocalizableResourceString(nameof(MakeConst.Resources.AnalyzerMessageFormat), MakeConst.Resources.ResourceManager, typeof(MakeConst.Resources)).ToString(),
        Severity = DiagnosticSeverity.Warning,
        Locations =
            new[] {
                    new DiagnosticResultLocation("Test0.cs", line, column)
                }
    };

    VerifyCSharpDiagnostic(test, expected);

    VerifyCSharpFix(test, fixTest);
}
```

<span data-ttu-id="bc77b-290">上述程式碼也對建置預期診斷結果的程式碼做了些許變更。</span><span class="sxs-lookup"><span data-stu-id="bc77b-290">The preceding code also made a couple changes to the code that builds the expected diagnostic result.</span></span> <span data-ttu-id="bc77b-291">它會使用在 `MakeConst` 分析器中註冊的公用常數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-291">It uses the public constants registered in the `MakeConst` analyzer.</span></span> <span data-ttu-id="bc77b-292">此外，它會針對輸入和已修正的來源使用兩個字串常數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-292">In addition, it uses two string constants for the input and fixed source.</span></span> <span data-ttu-id="bc77b-293">將下列字串常數新增至 `UnitTest` 類別：</span><span class="sxs-lookup"><span data-stu-id="bc77b-293">Add the following string constants to the `UnitTest` class:</span></span>

[!code-csharp[string constants for fix test](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#FirstFixTest "string constants for fix test")]

<span data-ttu-id="bc77b-294">執行這兩項測試，並確定可通過測試。</span><span class="sxs-lookup"><span data-stu-id="bc77b-294">Run these two tests to make sure they pass.</span></span> <span data-ttu-id="bc77b-295">在 Visual Studio 中選取 [測試]\*\*\*\* > [視窗]\*\*\*\* > [測試總管]\*\*\*\*，以開啟 [測試總管]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="bc77b-295">In Visual Studio, open the **Test Explorer** by selecting **Test** > **Windows** > **Test Explorer**.</span></span> <span data-ttu-id="bc77b-296">然後選取 [ **全部執行** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="bc77b-296">Then select the **Run All** link.</span></span>

## <a name="create-tests-for-valid-declarations"></a><span data-ttu-id="bc77b-297">建立有效宣告的測試</span><span class="sxs-lookup"><span data-stu-id="bc77b-297">Create tests for valid declarations</span></span>

<span data-ttu-id="bc77b-298">一般而言，分析器應盡快結束，而執行最少量的工作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-298">As a general rule, analyzers should exit as quickly as possible, doing minimal work.</span></span> <span data-ttu-id="bc77b-299">Visual Studio 會以使用者編輯程式碼的形式呼叫已註冊的分析器。</span><span class="sxs-lookup"><span data-stu-id="bc77b-299">Visual Studio calls registered analyzers as the user edits code.</span></span> <span data-ttu-id="bc77b-300">回應能力是關鍵需求。</span><span class="sxs-lookup"><span data-stu-id="bc77b-300">Responsiveness is a key requirement.</span></span> <span data-ttu-id="bc77b-301">不應引發診斷的程式碼有數個測試案例。</span><span class="sxs-lookup"><span data-stu-id="bc77b-301">There are several test cases for code that should not raise your diagnostic.</span></span> <span data-ttu-id="bc77b-302">您的分析器已處理其中一個測試，也就是變數會在初始化後進行指派的案例。</span><span class="sxs-lookup"><span data-stu-id="bc77b-302">Your analyzer already handles one of those tests, the case where a variable is assigned after being initialized.</span></span> <span data-ttu-id="bc77b-303">請將下列的字串常數新增至您的測試，以表示該案例：</span><span class="sxs-lookup"><span data-stu-id="bc77b-303">Add the following string constant to your tests to represent that case:</span></span>

[!code-csharp[variable assigned](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#VariableAssigned "a variable that is assigned after being initialized won't raise the diagnostic")]

<span data-ttu-id="bc77b-304">然後，為此測試新增資料列，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="bc77b-304">Then, add a data row for this test as shown in the snippet below:</span></span>

```csharp
[DataTestMethod]
[DataRow(""),
 DataRow(VariableAssigned)]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
```

<span data-ttu-id="bc77b-305">這項測試也會通過。</span><span class="sxs-lookup"><span data-stu-id="bc77b-305">This test passes as well.</span></span> <span data-ttu-id="bc77b-306">接著，為您尚未處理的狀況新增常數：</span><span class="sxs-lookup"><span data-stu-id="bc77b-306">Next, add constants for conditions you haven't handled yet:</span></span>

- <span data-ttu-id="bc77b-307">因為已是常數，而已經是 `const` 的宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-307">Declarations that are already `const`, because they are already const:</span></span>

   [!code-csharp[already const declaration](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#AlreadyConst "a declaration that is already const should not raise the diagnostic")]

- <span data-ttu-id="bc77b-308">因為沒有可使用的值，而沒有初始設定式的宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-308">Declarations that have no initializer, because there is no value to use:</span></span>

   [!code-csharp[declarations that have no initializer](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#NoInitializer "a declaration that has no initializer should not raise the diagnostic")]

- <span data-ttu-id="bc77b-309">因為不可以是編譯時期常數，因此初始設定式不是常數的宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-309">Declarations where the initializer is not a constant, because they can't be compile-time constants:</span></span>

   [!code-csharp[declarations where the initializer isn't const](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#InitializerNotConstant "a declaration where the initializer is not a compile-time constant should not raise the diagnostic")]

<span data-ttu-id="bc77b-310">如果 C# 允許以多個宣告作為一個陳述式，情況可能會更複雜。</span><span class="sxs-lookup"><span data-stu-id="bc77b-310">It can be even more complicated because C# allows multiple declarations as one statement.</span></span> <span data-ttu-id="bc77b-311">請考慮使用下列測試案例字串常數：</span><span class="sxs-lookup"><span data-stu-id="bc77b-311">Consider the following test case string constant:</span></span>

[!code-csharp[multiple initializers](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#MultipleInitializers "A declaration can be made constant only if all variables in that statement can be made constant")]

<span data-ttu-id="bc77b-312">變數 `i` 可設為常數，但變數 `j` 不可。</span><span class="sxs-lookup"><span data-stu-id="bc77b-312">The variable `i` can be made constant, but the variable `j` cannot.</span></span> <span data-ttu-id="bc77b-313">因此，此陳述式不可設為常數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-313">Therefore, this statement cannot be made a const declaration.</span></span> <span data-ttu-id="bc77b-314">請為這些測試全部新增 `DataRow` 宣告：</span><span class="sxs-lookup"><span data-stu-id="bc77b-314">Add the `DataRow` declarations for all these tests:</span></span>

```csharp
[DataTestMethod]
[DataRow(""),
    DataRow(VariableAssigned),
    DataRow(AlreadyConst),
    DataRow(NoInitializer),
    DataRow(InitializerNotConstant),
    DataRow(MultipleInitializers)]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
```

<span data-ttu-id="bc77b-315">重新執行您的測試，您將會發現這些新的測試案例失敗。</span><span class="sxs-lookup"><span data-stu-id="bc77b-315">Run your tests again, and you'll see these new test cases fail.</span></span>

## <a name="update-your-analyzer-to-ignore-correct-declarations"></a><span data-ttu-id="bc77b-316">更新分析器以忽略正確宣告</span><span class="sxs-lookup"><span data-stu-id="bc77b-316">Update your analyzer to ignore correct declarations</span></span>

<span data-ttu-id="bc77b-317">您需要為分析器的 `AnalyzeNode` 方法加入某些功能，以篩選出符合這些條件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-317">You need some enhancements to your analyzer's `AnalyzeNode` method to filter out code that matches these conditions.</span></span> <span data-ttu-id="bc77b-318">這些全都是相關條件，因此類似的變更將會修正所有的此類條件。</span><span class="sxs-lookup"><span data-stu-id="bc77b-318">They are all related conditions, so similar changes will fix all these conditions.</span></span> <span data-ttu-id="bc77b-319">對 `AnalyzeNode` 進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="bc77b-319">Make the following changes to `AnalyzeNode`:</span></span>

- <span data-ttu-id="bc77b-320">您的語意分析檢查了單一變數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-320">Your semantic analysis examined a single variable declaration.</span></span> <span data-ttu-id="bc77b-321">此程式碼必須位於會對在相同陳述式中宣告的所有變數進行檢查的 `foreach` 迴圈中。</span><span class="sxs-lookup"><span data-stu-id="bc77b-321">This code needs to be in a `foreach` loop that examines all the variables declared in the same statement.</span></span>
- <span data-ttu-id="bc77b-322">每個宣告的變數都必須有初始設定式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-322">Each declared variable needs to have an initializer.</span></span>
- <span data-ttu-id="bc77b-323">每個宣告變數的初始設定式都必須是編譯時期常數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-323">Each declared variable's initializer must be a compile-time constant.</span></span>

<span data-ttu-id="bc77b-324">在您的 `AnalyzeNode` 方法中，替換掉原始的語意分析：</span><span class="sxs-lookup"><span data-stu-id="bc77b-324">In your `AnalyzeNode` method, replace the original semantic analysis:</span></span>

```csharp
// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

// Retrieve the local symbol for each variable in the local declaration
// and ensure that it is not written outside of the data flow analysis region.
var variable = localDeclaration.Declaration.Variables.Single();
var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
{
    return;
}
```

<span data-ttu-id="bc77b-325">取代為下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="bc77b-325">with the following code snippet:</span></span>

```csharp
// Ensure that all variables in the local declaration have initializers that
// are assigned with constant values.
foreach (var variable in localDeclaration.Declaration.Variables)
{
    var initializer = variable.Initializer;
    if (initializer == null)
    {
        return;
    }

    var constantValue = context.SemanticModel.GetConstantValue(initializer.Value);
    if (!constantValue.HasValue)
    {
        return;
    }
}

// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

foreach (var variable in localDeclaration.Declaration.Variables)
{
    // Retrieve the local symbol for each variable in the local declaration
    // and ensure that it is not written outside of the data flow analysis region.
    var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
    if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
    {
        return;
    }
}
```

<span data-ttu-id="bc77b-326">第一個 `foreach` 迴圈會使用語法分析檢查每個變數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-326">The first `foreach` loop examines each variable declaration using syntactic analysis.</span></span> <span data-ttu-id="bc77b-327">第一次檢查可確保變數具有初始設定式。</span><span class="sxs-lookup"><span data-stu-id="bc77b-327">The first check guarantees that the variable has an initializer.</span></span> <span data-ttu-id="bc77b-328">第二次檢查可確保初始設定式是常數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-328">The second check guarantees that the initializer is a constant.</span></span> <span data-ttu-id="bc77b-329">第二個迴圈具有原始的語意分析。</span><span class="sxs-lookup"><span data-stu-id="bc77b-329">The second loop has the original semantic analysis.</span></span> <span data-ttu-id="bc77b-330">語意檢查位於個別的迴圈中，因為它對效能有較大的影響。</span><span class="sxs-lookup"><span data-stu-id="bc77b-330">The semantic checks are in a separate loop because it has a greater impact on performance.</span></span> <span data-ttu-id="bc77b-331">重新執行測試後，您應該會看到測試全部通過。</span><span class="sxs-lookup"><span data-stu-id="bc77b-331">Run your tests again, and you should see them all pass.</span></span>

## <a name="add-the-final-polish"></a><span data-ttu-id="bc77b-332">新增最終修改</span><span class="sxs-lookup"><span data-stu-id="bc77b-332">Add the final polish</span></span>

<span data-ttu-id="bc77b-333">就快要完成了。</span><span class="sxs-lookup"><span data-stu-id="bc77b-333">You're almost done.</span></span> <span data-ttu-id="bc77b-334">您的分析器還有幾種條件需要處理。</span><span class="sxs-lookup"><span data-stu-id="bc77b-334">There are a few more conditions for your analyzer to handle.</span></span> <span data-ttu-id="bc77b-335">使用者撰寫程式碼時，Visual Studio 會呼叫分析器。</span><span class="sxs-lookup"><span data-stu-id="bc77b-335">Visual Studio calls analyzers while the user is writing code.</span></span> <span data-ttu-id="bc77b-336">經呼叫的分析器常用來處理未編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-336">It's often the case that your analyzer will be called for code that doesn't compile.</span></span> <span data-ttu-id="bc77b-337">診斷分析器的 `AnalyzeNode` 方法不會檢查常數值是否可轉換成變數類型。</span><span class="sxs-lookup"><span data-stu-id="bc77b-337">The diagnostic analyzer's `AnalyzeNode` method does not check to see if the constant value is convertible to the variable type.</span></span> <span data-ttu-id="bc77b-338">因此，目前的實作會逕行將不正確的宣告 (例如 int i = "abc"') 轉換為區域常數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-338">So, the current implementation will happily convert an incorrect declaration such as int i = "abc"' to a local constant.</span></span> <span data-ttu-id="bc77b-339">請為該條件新增來源字串常數：</span><span class="sxs-lookup"><span data-stu-id="bc77b-339">Add a source string constant for that condition:</span></span>

[!code-csharp[Mismatched types don't raise diagnostics](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#DeclarationIsInvalid "When the variable type and the constant type don't match, there's no diagnostic")]

<span data-ttu-id="bc77b-340">此外，參考類型未正確處理。</span><span class="sxs-lookup"><span data-stu-id="bc77b-340">In addition, reference types are not handled properly.</span></span> <span data-ttu-id="bc77b-341">參考類型唯一允許的常數值為 `null`；此案例中的例外為 <xref:System.String?displayProperty=nameWithType>，它可允許字串常值。</span><span class="sxs-lookup"><span data-stu-id="bc77b-341">The only constant value allowed for a reference type is `null`, except in this case of <xref:System.String?displayProperty=nameWithType>, which allows string literals.</span></span> <span data-ttu-id="bc77b-342">換句話說，`const string s = "abc"` 是合法的，`const object s = "abc"` 則否。</span><span class="sxs-lookup"><span data-stu-id="bc77b-342">In other words, `const string s = "abc"` is legal, but `const object s = "abc"` is not.</span></span> <span data-ttu-id="bc77b-343">下列程式碼片段會驗證該條件：</span><span class="sxs-lookup"><span data-stu-id="bc77b-343">This code snippet verifies that condition:</span></span>

[!code-csharp[Reference types don't raise diagnostics](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#DeclarationIsntString "When the variable type is a reference type other than string, there's no diagnostic")]

<span data-ttu-id="bc77b-344">為求周密，您必須新增另一個測試，以確定您可以建立字串的常數宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-344">To be thorough, you need to add another test to make sure that you can create a constant declaration for a string.</span></span> <span data-ttu-id="bc77b-345">下列程式碼片段會定義引發診斷的程式碼和套用修正後的程式碼：</span><span class="sxs-lookup"><span data-stu-id="bc77b-345">The following snippet defines both the code that raises the diagnostic, and the code after the fix has been applied:</span></span>

[!code-csharp[string reference types raise diagnostics](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#ConstantIsString "When the variable type is string, it can be constant")]

<span data-ttu-id="bc77b-346">最後，如果以 `var` 關鍵字宣告變數，程式碼修正將執行錯誤的動作並產生 `const var` 宣告，但 C# 語言並不加以支援。</span><span class="sxs-lookup"><span data-stu-id="bc77b-346">Finally, if a variable is declared with the `var` keyword, the code fix does the wrong thing and generates a `const var` declaration, which is not supported by the C# language.</span></span> <span data-ttu-id="bc77b-347">若要修正此 Bug，程式碼修正必須將 `var` 關鍵字取代為推斷的類型名稱：</span><span class="sxs-lookup"><span data-stu-id="bc77b-347">To fix this bug, the code fix must replace the `var` keyword with the inferred type's name:</span></span>

[!code-csharp[var references need to use the inferred types](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#VarDeclarations "Declarations made using var must have the type replaced with the inferred type")]

<span data-ttu-id="bc77b-348">這些變更會同時更新這兩項測試的資料列宣告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-348">These changes update the data row declarations for both tests.</span></span> <span data-ttu-id="bc77b-349">下列程式碼顯示這些測試使用所有資料列屬性時的情形：</span><span class="sxs-lookup"><span data-stu-id="bc77b-349">The following code shows these tests with all data row attributes:</span></span>

[!code-csharp[The finished tests](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#FinishedTests "The finished tests for the make const analyzer")]

<span data-ttu-id="bc77b-350">幸運的是，上述所有 Bug 都可以使用您剛才學習的技術來解決。</span><span class="sxs-lookup"><span data-stu-id="bc77b-350">Fortunately, all of the above bugs can be addressed using the same techniques that you just learned.</span></span>

<span data-ttu-id="bc77b-351">若要修正第一個 Bug，請先開啟 **DiagnosticAnalyzer.cs**，並找出會檢查每個區域宣告的初始設定式以確保已為其指派常數值的 foreach 迴圈。</span><span class="sxs-lookup"><span data-stu-id="bc77b-351">To fix the first bug, first open **DiagnosticAnalyzer.cs** and locate the foreach loop where each of the local declaration's initializers are checked to ensure that they're assigned with constant values.</span></span> <span data-ttu-id="bc77b-352">在即將執行第一個 foreach 迴圈_之前_，呼叫 `context.SemanticModel.GetTypeInfo()` 以擷取與區域宣告的宣告類型有關的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="bc77b-352">Immediately _before_ the first foreach loop, call `context.SemanticModel.GetTypeInfo()` to retrieve detailed information about the declared type of the local declaration:</span></span>

```csharp
var variableTypeName = localDeclaration.Declaration.Type;
var variableType = context.SemanticModel.GetTypeInfo(variableTypeName).ConvertedType;
```

<span data-ttu-id="bc77b-353">然後，在您的 `foreach` 迴圈中檢查每個初始設定式，以確定它可轉換成變數類型。</span><span class="sxs-lookup"><span data-stu-id="bc77b-353">Then, inside your `foreach` loop, check each initializer to make sure it's convertible to the variable type.</span></span> <span data-ttu-id="bc77b-354">確定初始設定式是常數之後，請新增下列檢查：</span><span class="sxs-lookup"><span data-stu-id="bc77b-354">Add the following check after ensuring that the initializer is a constant:</span></span>

```csharp
// Ensure that the initializer value can be converted to the type of the
// local declaration without a user-defined conversion.
var conversion = context.SemanticModel.ClassifyConversion(initializer.Value, variableType);
if (!conversion.Exists || conversion.IsUserDefined)
{
    return;
}
```

<span data-ttu-id="bc77b-355">後續變更會以上一次的變更為建置基礎。</span><span class="sxs-lookup"><span data-stu-id="bc77b-355">The next change builds upon the last one.</span></span> <span data-ttu-id="bc77b-356">在第一個 foreach 迴圈右大括號前面新增下列程式碼，以在常數為字串或 Null 時檢查區域宣告的類型。</span><span class="sxs-lookup"><span data-stu-id="bc77b-356">Before the closing curly brace of the first foreach loop, add the following code to check the type of the local declaration when the constant is a string or null.</span></span>

```csharp
// Special cases:
//  * If the constant value is a string, the type of the local declaration
//    must be System.String.
//  * If the constant value is null, the type of the local declaration must
//    be a reference type.
if (constantValue.Value is string)
{
    if (variableType.SpecialType != SpecialType.System_String)
    {
        return;
    }
}
else if (variableType.IsReferenceType && constantValue.Value != null)
{
    return;
}
```

<span data-ttu-id="bc77b-357">您必須在程式碼修正提供者中撰寫更多程式碼，才能以 `var` 正確的型別名稱取代關鍵字。</span><span class="sxs-lookup"><span data-stu-id="bc77b-357">You must write a bit more code in your code fix provider to replace the `var` keyword with the correct type name.</span></span> <span data-ttu-id="bc77b-358">返回 **CodeFixProvider.cs**。</span><span class="sxs-lookup"><span data-stu-id="bc77b-358">Return to **CodeFixProvider.cs**.</span></span> <span data-ttu-id="bc77b-359">您將新增的程式碼會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bc77b-359">The code you'll add does the following steps:</span></span>

- <span data-ttu-id="bc77b-360">檢查宣告是否為 `var` 宣告，如果是則：</span><span class="sxs-lookup"><span data-stu-id="bc77b-360">Check if the declaration is a `var` declaration, and if it is:</span></span>
- <span data-ttu-id="bc77b-361">為推斷的類型建立新類型。</span><span class="sxs-lookup"><span data-stu-id="bc77b-361">Create a new type for the inferred type.</span></span>
- <span data-ttu-id="bc77b-362">確定類型宣告不是別名。</span><span class="sxs-lookup"><span data-stu-id="bc77b-362">Make sure the type declaration is not an alias.</span></span> <span data-ttu-id="bc77b-363">若是如此，則可以宣告 `const var`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-363">If so, it is legal to declare `const var`.</span></span>
- <span data-ttu-id="bc77b-364">確定 `var` 不是此程式中的類型名稱。</span><span class="sxs-lookup"><span data-stu-id="bc77b-364">Make sure that `var` isn't a type name in this program.</span></span> <span data-ttu-id="bc77b-365">(若是如此，則 `const var` 合法)。</span><span class="sxs-lookup"><span data-stu-id="bc77b-365">(If so, `const var` is legal).</span></span>
- <span data-ttu-id="bc77b-366">簡化完整類型名稱</span><span class="sxs-lookup"><span data-stu-id="bc77b-366">Simplify the full type name</span></span>

<span data-ttu-id="bc77b-367">程式碼看似不少。</span><span class="sxs-lookup"><span data-stu-id="bc77b-367">That sounds like a lot of code.</span></span> <span data-ttu-id="bc77b-368">其實並不然。</span><span class="sxs-lookup"><span data-stu-id="bc77b-368">It's not.</span></span> <span data-ttu-id="bc77b-369">請將宣告和初始化 `newLocal` 的那一行取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc77b-369">Replace the line that declares and initializes `newLocal` with the following code.</span></span> <span data-ttu-id="bc77b-370">它會 `newModifiers` 初始化之後立即執行：</span><span class="sxs-lookup"><span data-stu-id="bc77b-370">It goes immediately after the initialization of `newModifiers`:</span></span>

[!code-csharp[Replace Var designations](~/samples/snippets/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#ReplaceVar "Replace a var designation with the explicit type")]

<span data-ttu-id="bc77b-371">您將需要新增一個指示詞 `using` ，以使用 <xref:Microsoft.CodeAnalysis.Simplification.Simplifier> 類型：</span><span class="sxs-lookup"><span data-stu-id="bc77b-371">You'll need to add one `using` directive to use the <xref:Microsoft.CodeAnalysis.Simplification.Simplifier> type:</span></span>

```csharp
using Microsoft.CodeAnalysis.Simplification;
```

<span data-ttu-id="bc77b-372">執行測試，應該全部都會通過。</span><span class="sxs-lookup"><span data-stu-id="bc77b-372">Run your tests, and they should all pass.</span></span> <span data-ttu-id="bc77b-373">請執行您完成的分析器，這值得自傲。</span><span class="sxs-lookup"><span data-stu-id="bc77b-373">Congratulate yourself by running your finished analyzer.</span></span> <span data-ttu-id="bc77b-374">按下<kbd>Ctrl</kbd> + <kbd>F5</kbd> ，在已載入 Roslyn Preview 延伸模組的第二個 Visual Studio 實例中執行分析器專案。</span><span class="sxs-lookup"><span data-stu-id="bc77b-374">Press <kbd>Ctrl</kbd>+<kbd>F5</kbd> to run the analyzer project in a second instance of Visual Studio with the Roslyn Preview extension loaded.</span></span>

- <span data-ttu-id="bc77b-375">在第二個 Visual Studio 執行個體中建立新的 C# 主控台應用程式專案，並將 `int x = "abc";` 新增至 Main 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-375">In the second Visual Studio instance, create a new C# Console Application project and add `int x = "abc";` to the Main method.</span></span> <span data-ttu-id="bc77b-376">由於有第一個 Bug 修正，系統應該不會針對此區域變數宣告發出警告 (雖然如預期發生了編譯器錯誤)。</span><span class="sxs-lookup"><span data-stu-id="bc77b-376">Thanks to the first bug fix, no warning should be reported for this local variable declaration (though there's a compiler error as expected).</span></span>
- <span data-ttu-id="bc77b-377">接著，將 `object s = "abc";` 新增至 Main 方法。</span><span class="sxs-lookup"><span data-stu-id="bc77b-377">Next, add `object s = "abc";` to the Main method.</span></span> <span data-ttu-id="bc77b-378">由於有第二個 Bug 修正，應該不會出現警告。</span><span class="sxs-lookup"><span data-stu-id="bc77b-378">Because of the second bug fix, no warning should be reported.</span></span>
- <span data-ttu-id="bc77b-379">最後，新增另一個使用 `var` 關鍵字的區域變數。</span><span class="sxs-lookup"><span data-stu-id="bc77b-379">Finally, add another local variable that uses the `var` keyword.</span></span> <span data-ttu-id="bc77b-380">您會看到回報的警告，且左下方會出現建議。</span><span class="sxs-lookup"><span data-stu-id="bc77b-380">You'll see that a warning is reported and a suggestion appears beneath to the left.</span></span>
- <span data-ttu-id="bc77b-381">將編輯器插入號移到彎曲的底線上，然後按下<kbd>Ctrl</kbd> + <kbd>.</kbd>鍵。</span><span class="sxs-lookup"><span data-stu-id="bc77b-381">Move the editor caret over the squiggly underline and press <kbd>Ctrl</kbd>+<kbd>.</kbd>.</span></span> <span data-ttu-id="bc77b-382">以顯示建議的程式碼修正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-382">to display the suggested code fix.</span></span> <span data-ttu-id="bc77b-383">選取您的程式碼修正程式時，請注意 `var` 關鍵字現在已正確處理。</span><span class="sxs-lookup"><span data-stu-id="bc77b-383">Upon selecting your code fix, note that the `var` keyword is now handled correctly.</span></span>

<span data-ttu-id="bc77b-384">最後，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bc77b-384">Finally, add the following code:</span></span>

```csharp
int i = 2;
int j = 32;
int k = i + j;
```

<span data-ttu-id="bc77b-385">完成這些變更後，將只有前兩個變數上會有紅色波浪線。</span><span class="sxs-lookup"><span data-stu-id="bc77b-385">After these changes, you get red squiggles only on the first two variables.</span></span> <span data-ttu-id="bc77b-386">將 `const` 新增至 `i` 和 `j` 後，將會出現新的 `k` 警告，因為它現在已可為 `const`。</span><span class="sxs-lookup"><span data-stu-id="bc77b-386">Add `const` to both `i` and `j`, and you get a new warning on `k` because it can now be `const`.</span></span>

<span data-ttu-id="bc77b-387">恭喜！</span><span class="sxs-lookup"><span data-stu-id="bc77b-387">Congratulations!</span></span> <span data-ttu-id="bc77b-388">您已建立第一個 .NET Compiler Platform 延伸模組，可執行即時程式碼分析以偵測問題，並提供快速修正加以更正。</span><span class="sxs-lookup"><span data-stu-id="bc77b-388">You've created your first .NET Compiler Platform extension that performs on-the-fly code analysis to detect an issue and provides a quick fix to correct it.</span></span> <span data-ttu-id="bc77b-389">在本文中，您已認識 .NET Compiler Platform SDK (Roslyn API) 所包含的多種程式碼 API。</span><span class="sxs-lookup"><span data-stu-id="bc77b-389">Along the way, you've learned many of the code APIs that are part of the .NET Compiler Platform SDK (Roslyn APIs).</span></span> <span data-ttu-id="bc77b-390">您可以根據範例 GitHub 存放庫中[已完成的範例](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/Tutorials/MakeConst)檢查您的工作。</span><span class="sxs-lookup"><span data-stu-id="bc77b-390">You can check your work against the [completed sample](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/Tutorials/MakeConst) in our samples GitHub repository.</span></span>

## <a name="other-resources"></a><span data-ttu-id="bc77b-391">其他資源</span><span class="sxs-lookup"><span data-stu-id="bc77b-391">Other resources</span></span>

- [<span data-ttu-id="bc77b-392">開始使用語法分析</span><span class="sxs-lookup"><span data-stu-id="bc77b-392">Get started with syntax analysis</span></span>](../get-started/syntax-analysis.md)
- [<span data-ttu-id="bc77b-393">開始使用語意分析</span><span class="sxs-lookup"><span data-stu-id="bc77b-393">Get started with semantic analysis</span></span>](../get-started/semantic-analysis.md)

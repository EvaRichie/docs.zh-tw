---
title: Managed Extensibility Framework (MEF)
description: 探索 Managed Extensibility Framework (MEF) ，讓應用程式開發人員在 .NET 4 或更新版本中探索及使用擴充功能，而不需要設定。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Managed Extensibility Framework, overview
- MEF, overview
ms.assetid: 6c61b4ec-c6df-4651-80f1-4854f8b14dde
ms.openlocfilehash: b743a26dd401e7015c588be2a197551aa891a687
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555571"
---
# <a name="managed-extensibility-framework-mef"></a><span data-ttu-id="b7fc4-103">Managed Extensibility Framework (MEF)</span><span class="sxs-lookup"><span data-stu-id="b7fc4-103">Managed Extensibility Framework (MEF)</span></span>

<span data-ttu-id="b7fc4-104">本主題提供 .NET Framework 4 中所引入 Managed Extensibility Framework 的概觀。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-104">This topic provides an overview of the Managed Extensibility Framework that was introduced in the .NET Framework 4.</span></span>

## <a name="what-is-mef"></a><span data-ttu-id="b7fc4-105">什麼是 MEF？</span><span class="sxs-lookup"><span data-stu-id="b7fc4-105">What is MEF?</span></span>

<span data-ttu-id="b7fc4-106">Managed Extensibility Framework 或 MEF 是一個程式庫，可用於建立輕量且可擴充的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-106">The Managed Extensibility Framework or MEF is a library for creating lightweight, and extensible applications.</span></span> <span data-ttu-id="b7fc4-107">它可讓應用程式開發人員探索和使用擴充功能，而不需要任何組態。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-107">It allows application developers to discover and use extensions with no configuration required.</span></span> <span data-ttu-id="b7fc4-108">它也可以讓擴充功能開發人員輕鬆地封裝程式碼，並避免易損壞的硬式相依性。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-108">It also lets extension developers easily encapsulate code and avoid fragile hard dependencies.</span></span> <span data-ttu-id="b7fc4-109">MEF 不只允許在應用程式內重複使用擴充功能，也允許跨應用程式重複使用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-109">MEF not only allows extensions to be reused within applications, but across applications as well.</span></span>

## <a name="the-problem-of-extensibility"></a><span data-ttu-id="b7fc4-110">擴充性的問題</span><span class="sxs-lookup"><span data-stu-id="b7fc4-110">The problem of extensibility</span></span>

<span data-ttu-id="b7fc4-111">假設您是必須提供擴充性支援的大型應用程式架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-111">Imagine that you are the architect of a large application that must provide support for extensibility.</span></span> <span data-ttu-id="b7fc4-112">您的應用程式必須包含大量的較小元件，而且會負責建立和執行元件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-112">Your application has to include a potentially large number of smaller components, and is responsible for creating and running them.</span></span>

<span data-ttu-id="b7fc4-113">問題最簡單的解決方式是包含元件做為應用程式中的原始程式碼，並直接從程式碼呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-113">The simplest approach to the problem is to include the components as source code in your application, and call them directly from your code.</span></span> <span data-ttu-id="b7fc4-114">以下為一些明顯的缺點。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-114">This has a number of obvious drawbacks.</span></span> <span data-ttu-id="b7fc4-115">最重要的是，您需要修改原始程式碼才能新增元件，舉例來說，在 Web 應用程式中可能可以接受的限制，在用戶端應用程式中卻是無法作用的限制。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-115">Most importantly, you cannot add new components without modifying the source code, a restriction that might be acceptable in, for example, a Web application, but is unworkable in a client application.</span></span> <span data-ttu-id="b7fc4-116">同樣有問題的地方在於，因為元件可能由協力廠商所開發，所以您可能無法存取元件的原始碼，且基於相同的原因，您也不允許協力廠商存取您元件的原始碼。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-116">Equally problematic, you may not have access to the source code for the components, because they might be developed by third parties, and for the same reason you cannot allow them to access yours.</span></span>

<span data-ttu-id="b7fc4-117">稍微複雜一點的方法是提供擴充點或介面，以允許應用程式與其元件之間的去耦合。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-117">A slightly more sophisticated approach would be to provide an extension point or interface, to permit decoupling between the application and its components.</span></span> <span data-ttu-id="b7fc4-118">在此模型中，您可能會提供元件可以實作的介面，以及提供 API 讓它與您的應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-118">Under this model, you might provide an interface that a component can implement, and an API to enable it to interact with your application.</span></span> <span data-ttu-id="b7fc4-119">這樣可以解決需要原始程式碼存取權的問題，但仍有其困難度。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-119">This solves the problem of requiring source code access, but it still has its own difficulties.</span></span>

<span data-ttu-id="b7fc4-120">因為應用程式沒有任何能力可以自行探索元件，所以還是必須明確告知可用以及應該載入的元件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-120">Because the application lacks any capacity for discovering components on its own, it must still be explicitly told which components are available and should be loaded.</span></span> <span data-ttu-id="b7fc4-121">這通常是透過在組態檔中明確地註冊可用的元件來達成。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-121">This is typically accomplished by explicitly registering the available components in a configuration file.</span></span> <span data-ttu-id="b7fc4-122">這就表示，確保元件正確已成為維護問題，特別是當它是使用者，而不是預期進行更新的開發人員時。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-122">This means that assuring that the components are correct becomes a maintenance issue, particularly if it is the end user and not the developer who is expected to do the updating.</span></span>

<span data-ttu-id="b7fc4-123">此外，元件無法彼此通訊，但透過應用程式本身嚴格定義的通道除外。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-123">In addition, components are incapable of communicating with one another, except through the rigidly defined channels of the application itself.</span></span> <span data-ttu-id="b7fc4-124">如果應用程式架構設計人員不需要進行特定通訊，通常是不可能辦到的。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-124">If the application architect has not anticipated the need for a particular communication, it is usually impossible.</span></span>

<span data-ttu-id="b7fc4-125">最後，元件開發人員必須接受哪一個組件包含他們所實作之介面的硬式相依性。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-125">Finally, the component developers must accept a hard dependency on what assembly contains the interface they implement.</span></span> <span data-ttu-id="b7fc4-126">這樣很難在多個應用程式中使用元件，也可能會在建立元件的測試架構時產生問題。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-126">This makes it difficult for a component to be used in more than one application, and can also create problems when you create a test framework for components.</span></span>

## <a name="what-mef-provides"></a><span data-ttu-id="b7fc4-127">MEF 提供的功能</span><span class="sxs-lookup"><span data-stu-id="b7fc4-127">What MEF provides</span></span>

<span data-ttu-id="b7fc4-128">MEF 提供方法以透過「組合」\*\* 隱含地探索可用元件，而不是明確地註冊可用元件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-128">Instead of this explicit registration of available components, MEF provides a way to discover them implicitly, via *composition*.</span></span> <span data-ttu-id="b7fc4-129">MEF 元件 (稱為「組件」**) 會以宣告方式指定其相依性 (稱為「匯入」**) 及其提供的功能 (稱為「匯出」\*\*)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-129">A MEF component, called a *part*, declaratively specifies both its dependencies (known as *imports*) and what capabilities (known as *exports*) it makes available.</span></span> <span data-ttu-id="b7fc4-130">建立組件時，MEF 組合引擎可滿足具有從其他組件取得之內容的匯入。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-130">When a part is created, the MEF composition engine satisfies its imports with what is available from other parts.</span></span>

<span data-ttu-id="b7fc4-131">這種方法解決前一節所討論的問題。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-131">This approach solves the problems discussed in the previous section.</span></span> <span data-ttu-id="b7fc4-132">因為 MEF 組件是以宣告方式指定其功能，所以可以在執行階段找到它們，這表示應用程式可以使用組件，而不需要硬式編碼參考或易損壞的組態檔。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-132">Because MEF parts declaratively specify their capabilities, they are discoverable at runtime, which means an application can make use of parts without either hard-coded references or fragile configuration files.</span></span> <span data-ttu-id="b7fc4-133">MEF 允許應用程式透過它們的中繼資料來探索和檢查組件 (part)，而不需要具現化應用程式，或甚至載入其組件 (assembly)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-133">MEF allows applications to discover and examine parts by their metadata, without instantiating them or even loading their assemblies.</span></span> <span data-ttu-id="b7fc4-134">因此，不需要仔細地指定何時以及應該如何載入擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-134">As a result, there is no need to carefully specify when and how extensions should be loaded.</span></span>

<span data-ttu-id="b7fc4-135">除了它所提供的匯出之外，組件可以指定其匯入 (將會填入其他組件)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-135">In addition to its provided exports, a part can specify its imports, which will be filled by other parts.</span></span> <span data-ttu-id="b7fc4-136">這不只可讓組件之間進行通訊，而且十分簡單，並允許進行不錯的程式碼分解。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-136">This makes communication among parts not only possible, but easy, and allows for good factoring of code.</span></span> <span data-ttu-id="b7fc4-137">例如，許多元件通用的服務可以分解為個別的組件，而且可以輕鬆地修改或取代。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-137">For example, services common to many components can be factored into a separate part and easily modified or replaced.</span></span>

<span data-ttu-id="b7fc4-138">因為 MEF 模型不需要對特定應用程式組件產生硬式相依性，所以允許在不同的應用程式之間重複使用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-138">Because the MEF model requires no hard dependency on a particular application assembly, it allows extensions to be reused from application to application.</span></span> <span data-ttu-id="b7fc4-139">這也能讓您輕鬆地開發測試載入器 (與應用程式無關) 以測試擴充功能元件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-139">This also makes it easy to develop a test harness, independent of the application, to test extension components.</span></span>

<span data-ttu-id="b7fc4-140">使用 MEF 所撰寫的可延伸應用程式會宣告可填入擴充功能元件的匯入，也可以宣告匯出以向擴充功能公開應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-140">An extensible application written by using MEF declares an import that can be filled by extension components, and may also declare exports in order to expose application services to extensions.</span></span> <span data-ttu-id="b7fc4-141">每個擴充功能元件都會宣告匯出，也可能會宣告匯入。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-141">Each extension component declares an export, and may also declare imports.</span></span> <span data-ttu-id="b7fc4-142">如此一來，擴充功能元件本身是可自動擴充的。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-142">In this way, extension components themselves are automatically extensible.</span></span>

## <a name="where-mef-is-available"></a><span data-ttu-id="b7fc4-143">其中有 MEF 可用</span><span class="sxs-lookup"><span data-stu-id="b7fc4-143">Where MEF is available</span></span>

<span data-ttu-id="b7fc4-144">MEF 是 .NET Framework 4 不可或缺的部分，而且只要使用.NET Framework 就可以使用 MEF。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-144">MEF is an integral part of the .NET Framework 4, and is available wherever the .NET Framework is used.</span></span> <span data-ttu-id="b7fc4-145">在使用 Windows Forms、WPF 或任何其他技術的用戶端應用程式中，還是在使用 ASP.NET 的伺服器應用程式中，您都可以使用 MEF。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-145">You can use MEF in your client applications, whether they use Windows Forms, WPF, or any other technology, or in server applications that use ASP.NET.</span></span>

## <a name="mef-and-maf"></a><span data-ttu-id="b7fc4-146">MEF 和 MAF</span><span class="sxs-lookup"><span data-stu-id="b7fc4-146">MEF and MAF</span></span>

<span data-ttu-id="b7fc4-147">舊版 .NET Framework 已引入管理增益集架構 (MAF)，設計為允許應用程式隔離和管理擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-147">Previous versions of the .NET Framework introduced the Managed Add-in Framework (MAF), designed to allow applications to isolate and manage extensions.</span></span> <span data-ttu-id="b7fc4-148">MAF 的焦點在層次上略高於 MEF，專注於擴充功能隔離以及組件載入和卸載，而 MEF 的焦點在於可搜尋性、擴充性和可攜性。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-148">The focus of MAF is slightly higher-level than MEF, concentrating on extension isolation and assembly loading and unloading, while MEF's focus is on discoverability, extensibility, and portability.</span></span> <span data-ttu-id="b7fc4-149">這兩個架構可以順利地交互操作，而且兩者皆可為單一應用程式所用。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-149">The two frameworks interoperate smoothly, and a single application can take advantage of both.</span></span>

## <a name="simplecalculator-an-example-application"></a><span data-ttu-id="b7fc4-150">SimpleCalculator：範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fc4-150">SimpleCalculator: An example application</span></span>

<span data-ttu-id="b7fc4-151">了解 MEF 用途的最簡單方式是建置一個簡單的 MEF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-151">The simplest way to see what MEF can do is to build a simple MEF application.</span></span> <span data-ttu-id="b7fc4-152">在這個範例中，您建置一個十分簡單的計算機 (名稱為 SimpleCalculator)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-152">In this example, you build a very simple calculator named SimpleCalculator.</span></span> <span data-ttu-id="b7fc4-153">SimpleCalculator 的目標是建立一個接受基本算術命令 (格式為 "5+3" 或 "6-2") 的主控台應用程式，並傳回正確的答案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-153">The goal of SimpleCalculator is to create a console application that accepts basic arithmetic commands, in the form "5+3" or "6-2", and returns the correct answers.</span></span> <span data-ttu-id="b7fc4-154">使用 MEF，您可以新增運算子，而不需要變更應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-154">Using MEF, you'll be able to add new operators without changing the application code.</span></span>

<span data-ttu-id="b7fc4-155">若要下載此範例的完整程式碼，請參閱 [SimpleCalculator 範例 (Visual Basic) ](/samples/dotnet/samples/simple-calculator-vb/)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-155">To download the complete code for this example, see the [SimpleCalculator sample (Visual Basic)](/samples/dotnet/samples/simple-calculator-vb/).</span></span>

> [!NOTE]
> <span data-ttu-id="b7fc4-156">SimpleCalculator 的目的是示範 MEF 的概念和語法，不一定會提供其實際使用案例。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-156">The purpose of SimpleCalculator is to demonstrate the concepts and syntax of MEF, rather than to necessarily provide a realistic scenario for its use.</span></span> <span data-ttu-id="b7fc4-157">許多從 MEF 功能獲得最多益處的應用程式，比 SimpleCalculator 更為複雜。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-157">Many of the applications that would benefit most from the power of MEF are more complex than SimpleCalculator.</span></span> <span data-ttu-id="b7fc4-158">如需更多範例，請參閱 GitHub 上的 [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-158">For more extensive examples, see the [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef) on GitHub.</span></span>

- <span data-ttu-id="b7fc4-159">若要開始，請在 Visual Studio 中建立新的主控台應用程式專案，並且將它命名為 `SimpleCalculator`。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-159">To start, in Visual Studio, create a new Console Application project and name it `SimpleCalculator`.</span></span>

- <span data-ttu-id="b7fc4-160">將參考加入至 `System.ComponentModel.Composition` MEF 所在的元件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-160">Add a reference to the `System.ComponentModel.Composition` assembly, where MEF resides.</span></span>

- <span data-ttu-id="b7fc4-161">開啟 [ *Module1* ] 或 [ *Program.cs* ]，然後 `Imports` 針對和加入或 `using` 語句 `System.ComponentModel.Composition` `System.ComponentModel.Composition.Hosting` 。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-161">Open *Module1.vb* or *Program.cs* and add `Imports` or `using` statements for `System.ComponentModel.Composition` and `System.ComponentModel.Composition.Hosting`.</span></span> <span data-ttu-id="b7fc4-162">這兩個命名空間都包含開發可延伸應用程式所需的 MEF 類型。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-162">These two namespaces contain MEF types you will need to develop an extensible application.</span></span>

- <span data-ttu-id="b7fc4-163">如果您使用 Visual Basic，請將 `Public` 關鍵字新增至宣告 `Module1` 模組的行。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-163">If you're using Visual Basic, add the `Public` keyword to the line that declares the `Module1` module.</span></span>

## <a name="composition-container-and-catalogs"></a><span data-ttu-id="b7fc4-164">組合容器和目錄</span><span class="sxs-lookup"><span data-stu-id="b7fc4-164">Composition container and catalogs</span></span>

<span data-ttu-id="b7fc4-165">MEF 組合模型的核心是「組合容器」\*\*，其中包含所有可用的組件並執行組合。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-165">The core of the MEF composition model is the *composition container*, which contains all the parts available and performs composition.</span></span> <span data-ttu-id="b7fc4-166">組合會將匯入往上對應至匯出。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-166">Composition is the matching up of imports to exports.</span></span> <span data-ttu-id="b7fc4-167">最常見的組合容器類型是 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer>，而且您會將它用於 SimpleCalculator。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-167">The most common type of composition container is <xref:System.ComponentModel.Composition.Hosting.CompositionContainer>, and you'll use this for SimpleCalculator.</span></span>

<span data-ttu-id="b7fc4-168">如果您使用 Visual Basic，請在 [Module1] 中加入名為的公用類別 `Program` 。 *Module1.vb*</span><span class="sxs-lookup"><span data-stu-id="b7fc4-168">If you're using Visual Basic, add a public class named `Program` in *Module1.vb*.</span></span>

<span data-ttu-id="b7fc4-169">將以下這一行新增至 `Program` *Program.cs*中*Module1.vb*的類別：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-169">Add the following line to the `Program` class in *Module1.vb* or *Program.cs*:</span></span>

```vb
Dim _container As CompositionContainer
```

```csharp
private CompositionContainer _container;
```

<span data-ttu-id="b7fc4-170">為了要探索可供組合容器使用的組件，組合容器會利用「目錄」\*\*。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-170">In order to discover the parts available to it, the composition containers makes use of a *catalog*.</span></span> <span data-ttu-id="b7fc4-171">目錄是可從某個來源探索到可用組件的物件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-171">A catalog is an object that makes available parts discovered from some source.</span></span> <span data-ttu-id="b7fc4-172">MEF 提供目錄 (catalog)，以從提供的類型、組件 (assembly) 或目錄 (directory) 探索組件 (part)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-172">MEF provides catalogs to discover parts from a provided type, an assembly, or a directory.</span></span> <span data-ttu-id="b7fc4-173">應用程式開發人員可以輕鬆地建立新的目錄，以從其他來源 (例如 Web 服務) 探索組件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-173">Application developers can easily create new catalogs to discover parts from other sources, such as a Web service.</span></span>

<span data-ttu-id="b7fc4-174">將下列建構函式加入 `Program` 類別：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-174">Add the following constructor to the `Program` class:</span></span>

```vb
Public Sub New()
    ' An aggregate catalog that combines multiple catalogs.
     Dim catalog = New AggregateCatalog()

    ' Adds all the parts found in the same assembly as the Program class.
    catalog.Catalogs.Add(New AssemblyCatalog(GetType(Program).Assembly))

    ' Create the CompositionContainer with the parts in the catalog.
    _container = New CompositionContainer(catalog)

    ' Fill the imports of this object.
    Try
        _container.ComposeParts(Me)
    Catch ex As CompositionException
        Console.WriteLine(ex.ToString)
    End Try
End Sub
```

```csharp
private Program()
{
    // An aggregate catalog that combines multiple catalogs.
    var catalog = new AggregateCatalog();
    // Adds all the parts found in the same assembly as the Program class.
    catalog.Catalogs.Add(new AssemblyCatalog(typeof(Program).Assembly));

    // Create the CompositionContainer with the parts in the catalog.
    _container = new CompositionContainer(catalog);

    // Fill the imports of this object.
    try
    {
        this._container.ComposeParts(this);
    }
    catch (CompositionException compositionException)
    {
        Console.WriteLine(compositionException.ToString());
   }
}
```

<span data-ttu-id="b7fc4-175"><xref:System.ComponentModel.Composition.AttributedModelServices.ComposeParts%2A> 呼叫會告知組合容器撰寫一組特定的組件，在此情況下是目前的 `Program` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-175">The call to <xref:System.ComponentModel.Composition.AttributedModelServices.ComposeParts%2A> tells the composition container to compose a specific set of parts, in this case the current instance of `Program`.</span></span> <span data-ttu-id="b7fc4-176">不過，此時不會發生任何事，因為 `Program` 沒有要填入的匯入。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-176">At this point, however, nothing will happen, since `Program` has no imports to fill.</span></span>

## <a name="imports-and-exports-with-attributes"></a><span data-ttu-id="b7fc4-177">具有屬性的匯入和匯出</span><span class="sxs-lookup"><span data-stu-id="b7fc4-177">Imports and Exports with attributes</span></span>

<span data-ttu-id="b7fc4-178">首先，您讓 `Program` 匯入計算機。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-178">First, you have `Program` import a calculator.</span></span> <span data-ttu-id="b7fc4-179">這允許使用者介面考量 (例如將進入 `Program` 的主控台輸入和輸出) 與計算機的邏輯分隔。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-179">This allows the separation of user interface concerns, such as the console input and output that will go into `Program`, from the logic of the calculator.</span></span>

<span data-ttu-id="b7fc4-180">將下列程式碼新增至 `Program` 類別：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-180">Add the following code to the `Program` class:</span></span>

```vb
<Import(GetType(ICalculator))>
Public Property calculator As ICalculator
```

```csharp
[Import(typeof(ICalculator))]
public ICalculator calculator;
```

<span data-ttu-id="b7fc4-181">請注意，`calculator` 物件的宣告不是異常，而是它使用 <xref:System.ComponentModel.Composition.ImportAttribute> 屬性裝飾。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-181">Notice that the declaration of the `calculator` object is not unusual, but that it is decorated with the <xref:System.ComponentModel.Composition.ImportAttribute> attribute.</span></span> <span data-ttu-id="b7fc4-182">這個屬性會將某個項目宣告為匯入；也就是撰寫物件時，組合引擎將會填入它。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-182">This attribute declares something to be an import; that is, it will be filled by the composition engine when the object is composed.</span></span>

<span data-ttu-id="b7fc4-183">每個匯入都有「合約」\*\*，其會決定將與其相符的匯出。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-183">Every import has a *contract*, which determines what exports it will be matched with.</span></span> <span data-ttu-id="b7fc4-184">合約可以是明確指定的字串，也可以由 MEF 透過指定類型自動產生，在此情況下為 `ICalculator` 介面。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-184">The contract can be an explicitly specified string, or it can be automatically generated by MEF from a given type, in this case the interface `ICalculator`.</span></span> <span data-ttu-id="b7fc4-185">任何已宣告相符合約的匯出都滿足此匯入。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-185">Any export declared with a matching contract will fulfill this import.</span></span> <span data-ttu-id="b7fc4-186">請注意，`calculator` 物件的類型事際上是 `ICalculator` 時，這不是必要項目。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-186">Note that while the type of the `calculator` object is in fact `ICalculator`, this is not required.</span></span> <span data-ttu-id="b7fc4-187">合約與匯入中物件的類型無關 </span><span class="sxs-lookup"><span data-stu-id="b7fc4-187">The contract is independent from the type of the importing object.</span></span> <span data-ttu-id="b7fc4-188">(在此情況下，您可以遺漏 `typeof(ICalculator)`。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-188">(In this case, you could leave out the `typeof(ICalculator)`.</span></span> <span data-ttu-id="b7fc4-189">除非您明確地指定合約，否則 MEF 將會自動假設合約是根據匯入的類型。)</span><span class="sxs-lookup"><span data-stu-id="b7fc4-189">MEF will automatically assume the contract to be based on the type of the import unless you specify it explicitly.)</span></span>

<span data-ttu-id="b7fc4-190">請將這個非常簡單的介面加入模組或 `SimpleCalculator` 命名空間：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-190">Add this very simple interface to the module or `SimpleCalculator` namespace:</span></span>

```vb
Public Interface ICalculator
    Function Calculate(input As String) As String
End Interface
```

```csharp
public interface ICalculator
{
    String Calculate(String input);
}
```

<span data-ttu-id="b7fc4-191">既然您已定義 `ICalculator`，您需要實作它的類別。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-191">Now that you have defined `ICalculator`, you need a class that implements it.</span></span> <span data-ttu-id="b7fc4-192">將下列類別加入模組或 `SimpleCalculator` 命名空間：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-192">Add the following class to the module or `SimpleCalculator` namespace:</span></span>

```vb
<Export(GetType(ICalculator))>
Public Class MySimpleCalculator
   Implements ICalculator

End Class
```

```csharp
[Export(typeof(ICalculator))]
class MySimpleCalculator : ICalculator
{

}
```

<span data-ttu-id="b7fc4-193">以下是符合 `Program` 中匯入的匯出。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-193">Here is the export that will match the import in `Program`.</span></span> <span data-ttu-id="b7fc4-194">若要讓匯出符合匯入，匯出必須具有相同的合約。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-194">In order for the export to match the import, the export must have the same contract.</span></span> <span data-ttu-id="b7fc4-195">按照以 `typeof(MySimpleCalculator)` 為根據的合約，匯出會產生不相符的情況，而且不會填入匯入；合約必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-195">Exporting under a contract based on `typeof(MySimpleCalculator)` would produce a mismatch, and the import would not be filled; the contract needs to match exactly.</span></span>

<span data-ttu-id="b7fc4-196">因為組合容器將會填入這個組件 (assembly) 中可用的所有組件 (part)，所以將可以使用 `MySimpleCalculator` 組件 (part)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-196">Since the composition container will be populated with all the parts available in this assembly, the `MySimpleCalculator` part will be available.</span></span> <span data-ttu-id="b7fc4-197">`Program` 的建構函式對 `Program` 物件執行組合時，其匯入將會填入針對該用途所建立的 `MySimpleCalculator` 物件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-197">When the constructor for `Program` performs composition on the `Program` object, its import will be filled with a `MySimpleCalculator` object, which will be created for that purpose.</span></span>

<span data-ttu-id="b7fc4-198">使用者介面層 (`Program`) 不需要知道任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-198">The user interface layer (`Program`) does not need to know anything else.</span></span> <span data-ttu-id="b7fc4-199">因此，您可以在 `Main` 方法中填入其餘的使用者介面邏輯。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-199">You can therefore fill in the rest of the user interface logic in the `Main` method.</span></span>

<span data-ttu-id="b7fc4-200">將下列程式碼加入 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-200">Add the following code to the `Main` method:</span></span>

```vb
Sub Main()
    ' Composition is performed in the constructor.
    Dim p As New Program()
    Dim s As String
    Console.WriteLine("Enter Command:")
    While (True)
        s = Console.ReadLine()
        Console.WriteLine(p.calculator.Calculate(s))
    End While
End Sub
```

```csharp
static void Main(string[] args)
{
    // Composition is performed in the constructor.
    var p = new Program();
    string s;
    Console.WriteLine("Enter Command:");
    while (true)
    {
        s = Console.ReadLine();
        Console.WriteLine(p.calculator.Calculate(s));
    }
}
```

 <span data-ttu-id="b7fc4-201">此程式碼只會讀取一行輸入，並針對結果呼叫 `Calculate` 的 `ICalculator` 函式，以將結果寫回主控台。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-201">This code simply reads a line of input and calls the `Calculate` function of `ICalculator` on the result, which it writes back to the console.</span></span> <span data-ttu-id="b7fc4-202">這是 `Program` 中您需要的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-202">That is all the code you need in `Program`.</span></span> <span data-ttu-id="b7fc4-203">所有其餘的工作將在組件中進行。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-203">All the rest of the work will happen in the parts.</span></span>

## <a name="further-imports-and-importmany"></a><span data-ttu-id="b7fc4-204">進一步匯入和 ImportMany</span><span class="sxs-lookup"><span data-stu-id="b7fc4-204">Further Imports and ImportMany</span></span>

<span data-ttu-id="b7fc4-205">為了讓 SimpleCalculator 可延伸，它需要匯入作業的清單。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-205">In order for SimpleCalculator to be extensible, it needs to import a list of operations.</span></span> <span data-ttu-id="b7fc4-206">一般 <xref:System.ComponentModel.Composition.ImportAttribute> 屬性只會填入一個 <xref:System.ComponentModel.Composition.ExportAttribute>。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-206">An ordinary <xref:System.ComponentModel.Composition.ImportAttribute> attribute is filled by one and only one <xref:System.ComponentModel.Composition.ExportAttribute>.</span></span> <span data-ttu-id="b7fc4-207">如果有多個可用，組合引擎就會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-207">If more than one is available, the composition engine produces an error.</span></span> <span data-ttu-id="b7fc4-208">若要建立可以填入任意數目匯出的匯入，您可以使用 <xref:System.ComponentModel.Composition.ImportManyAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-208">To create an import that can be filled by any number of exports, you can use the <xref:System.ComponentModel.Composition.ImportManyAttribute> attribute.</span></span>

<span data-ttu-id="b7fc4-209">將下列作業屬性加入至 `MySimpleCalculator` 類別：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-209">Add the following operations property to the `MySimpleCalculator` class:</span></span>

```vb
<ImportMany()>
Public Property operations As IEnumerable(Of Lazy(Of IOperation, IOperationData))
```

```csharp
[ImportMany]
IEnumerable<Lazy<IOperation, IOperationData>> operations;
```

<span data-ttu-id="b7fc4-210"><xref:System.Lazy%602> 是 MEF 所提供的類型，用於保留要匯出的間接參考。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-210"><xref:System.Lazy%602> is a type provided by MEF to hold indirect references to exports.</span></span> <span data-ttu-id="b7fc4-211">在這裡，除了匯出的物件本身之外，您也會取得「匯出中繼資料」\*\* 或描述所匯出物件的資訊。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-211">Here, in addition to the exported object itself, you also get *export metadata*, or information that describes the exported object.</span></span> <span data-ttu-id="b7fc4-212">每個 <xref:System.Lazy%602> 都會包含代表實際作業的 `IOperation` 物件以及代表其中繼資料的 `IOperationData` 物件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-212">Each <xref:System.Lazy%602> contains an `IOperation` object, representing an actual operation, and an `IOperationData` object, representing its metadata.</span></span>

<span data-ttu-id="b7fc4-213">將下列簡單的介面加入模組或 `SimpleCalculator` 命名空間：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-213">Add the following simple interfaces to the module or `SimpleCalculator` namespace:</span></span>

```vb
Public Interface IOperation
    Function Operate(left As Integer, right As Integer) As Integer
End Interface

Public Interface IOperationData
    ReadOnly Property Symbol As Char
End Interface
```

```csharp
public interface IOperation
{
     int Operate(int left, int right);
}

public interface IOperationData
{
    Char Symbol { get; }
}
```

 <span data-ttu-id="b7fc4-214">在此情況下，每個作業的中繼資料都是代表該作業的符號，例如 +、-、 \* 等等。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-214">In this case, the metadata for each operation is the symbol that represents that operation, such as +, -, \*, and so on.</span></span> <span data-ttu-id="b7fc4-215">若要使用加法運算，請將下列類別加入模組或 `SimpleCalculator` 命名空間：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-215">To make the addition operation available, add the following class to the module or `SimpleCalculator` namespace:</span></span>

```vb
<Export(GetType(IOperation))>
<ExportMetadata("Symbol", "+"c)>
Public Class Add
    Implements IOperation

    Public Function Operate(left As Integer, right As Integer) As Integer Implements IOperation.Operate
        Return left + right
    End Function
End Class
```

```csharp
[Export(typeof(IOperation))]
[ExportMetadata("Symbol", '+')]
class Add: IOperation
{
    public int Operate(int left, int right)
    {
        return left + right;
    }
}
```

<span data-ttu-id="b7fc4-216"><xref:System.ComponentModel.Composition.ExportAttribute> 屬性的運作與以前一樣。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-216">The <xref:System.ComponentModel.Composition.ExportAttribute> attribute functions as it did before.</span></span> <span data-ttu-id="b7fc4-217"><xref:System.ComponentModel.Composition.ExportMetadataAttribute> 屬性會將中繼資料 (以名稱/值組的形式) 附加至該匯出。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-217">The <xref:System.ComponentModel.Composition.ExportMetadataAttribute> attribute attaches metadata, in the form of a name-value pair, to that export.</span></span> <span data-ttu-id="b7fc4-218">雖然 `Add` 類別實作 `IOperation`，但是未明確地定義可實作 `IOperationData` 的類別。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-218">While the `Add` class implements `IOperation`, a class that implements `IOperationData` is not explicitly defined.</span></span> <span data-ttu-id="b7fc4-219">相反地，類別由 MEF 所隱含建立，其屬性以提供的中繼資料名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-219">Instead, a class is implicitly created by MEF with properties based on the names of the metadata provided.</span></span> <span data-ttu-id="b7fc4-220">(這是在 MEF 存取中繼資料的數種方式中的一種。)</span><span class="sxs-lookup"><span data-stu-id="b7fc4-220">(This is one of several ways to access metadata in MEF.)</span></span>

<span data-ttu-id="b7fc4-221">MEF 中的組合是「遞迴的」\*\*。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-221">Composition in MEF is *recursive*.</span></span> <span data-ttu-id="b7fc4-222">您已明確地撰寫 `Program` 物件，這樣會匯入結果為 `ICalculator` 類型的 `MySimpleCalculator`。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-222">You explicitly composed the `Program` object, which imported an `ICalculator` that turned out to be of type `MySimpleCalculator`.</span></span> <span data-ttu-id="b7fc4-223">`MySimpleCalculator` 接著會匯入 `IOperation` 物件的集合，而且將會在建立 `MySimpleCalculator` 時填入該匯入，與 `Program` 匯入同時。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-223">`MySimpleCalculator`, in turn, imports a collection of `IOperation` objects, and that import will be filled when `MySimpleCalculator` is created, at the same time as the imports of `Program`.</span></span> <span data-ttu-id="b7fc4-224">如果 `Add` 類別已宣告進一步的匯入，則也必須予以填入，以此類推。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-224">If the `Add` class declared a further import, that too would have to be filled, and so on.</span></span> <span data-ttu-id="b7fc4-225">任何未填入的匯入都會導致組合錯誤。 </span><span class="sxs-lookup"><span data-stu-id="b7fc4-225">Any import left unfilled results in a composition error.</span></span> <span data-ttu-id="b7fc4-226">(不過，可能會將匯入宣告為選擇性，或指派預設值給它們。)</span><span class="sxs-lookup"><span data-stu-id="b7fc4-226">(It is possible, however, to declare imports to be optional or to assign them default values.)</span></span>

## <a name="calculator-logic"></a><span data-ttu-id="b7fc4-227">計算機邏輯</span><span class="sxs-lookup"><span data-stu-id="b7fc4-227">Calculator Logic</span></span>

<span data-ttu-id="b7fc4-228">這些組件都就緒之後，剩下的就是計算機邏輯本身。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-228">With these parts in place, all that remains is the calculator logic itself.</span></span> <span data-ttu-id="b7fc4-229">在 `MySimpleCalculator` 類別中加入下列程式碼，以實作 `Calculate` 方法：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-229">Add the following code in the `MySimpleCalculator` class to implement the `Calculate` method:</span></span>

```vb
Public Function Calculate(input As String) As String Implements ICalculator.Calculate
    Dim left, right As Integer
    Dim operation As Char
    ' Finds the operator.
    Dim fn = FindFirstNonDigit(input)
    If fn < 0 Then
        Return "Could not parse command."
    End If
    operation = input(fn)
    Try
        ' Separate out the operands.
        left = Integer.Parse(input.Substring(0, fn))
        right = Integer.Parse(input.Substring(fn + 1))
    Catch ex As Exception
        Return "Could not parse command."
    End Try
    For Each i As Lazy(Of IOperation, IOperationData) In operations
        If i.Metadata.symbol = operation Then
            Return i.Value.Operate(left, right).ToString()
        End If
    Next
    Return "Operation not found!"
End Function
```

```csharp
public String Calculate(string input)
{
    int left;
    int right;
    char operation;
    // Finds the operator.
    int fn = FindFirstNonDigit(input);
    if (fn < 0) return "Could not parse command.";

    try
    {
        // Separate out the operands.
        left = int.Parse(input.Substring(0, fn));
        right = int.Parse(input.Substring(fn + 1));
    }
    catch
    {
        return "Could not parse command.";
    }

    operation = input[fn];

    foreach (Lazy<IOperation, IOperationData> i in operations)
    {
        if (i.Metadata.Symbol.Equals(operation)) return i.Value.Operate(left, right).ToString();
    }
    return "Operation Not Found!";
}
```

<span data-ttu-id="b7fc4-230">初始步驟會將輸入字串剖析為左運算元、右運算元和一個運算子字元。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-230">The initial steps parse the input string into left and right operands and an operator character.</span></span> <span data-ttu-id="b7fc4-231">在 `foreach` 迴圈中，會檢查 `operations` 集合的每個成員。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-231">In the `foreach` loop, every member of the `operations` collection is examined.</span></span> <span data-ttu-id="b7fc4-232">這些物件的類型為 <xref:System.Lazy%602>，而且分別可以使用 <xref:System.Lazy%602.Metadata%2A> 屬性和 <xref:System.Lazy%601.Value%2A> 屬性來存取它們的中繼資料值和所匯出的物件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-232">These objects are of type <xref:System.Lazy%602>, and their metadata values and exported object can be accessed with the <xref:System.Lazy%602.Metadata%2A> property and the <xref:System.Lazy%601.Value%2A> property respectively.</span></span> <span data-ttu-id="b7fc4-233">在此情況下，如果發現 `Symbol` 物件的 `IOperationData` 屬性為相符項，則計算機會呼叫 `Operate` 物件的 `IOperation` 方法，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-233">In this case, if the `Symbol` property of the `IOperationData` object is discovered to be a match, the calculator calls the `Operate` method of the `IOperation` object and returns the result.</span></span>

<span data-ttu-id="b7fc4-234">若要完成計算機，您也需要可傳回字串中第一個非數字字元位置的 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-234">To complete the calculator, you also need a helper method that returns the position of the first non-digit character in a string.</span></span> <span data-ttu-id="b7fc4-235">將下列 Helper 方法加入 `MySimpleCalculator` 類別：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-235">Add the following helper method to the `MySimpleCalculator` class:</span></span>

```vb
Private Function FindFirstNonDigit(s As String) As Integer
    For i = 0 To s.Length - 1
        If Not Char.IsDigit(s(i)) Then Return i
    Next
    Return -1
End Function
```

```csharp
private int FindFirstNonDigit(string s)
{
    for (int i = 0; i < s.Length; i++)
    {
        if (!Char.IsDigit(s[i])) return i;
    }
    return -1;
}
```

<span data-ttu-id="b7fc4-236">您現在應該可以編譯和執行專案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-236">You should now be able to compile and run the project.</span></span> <span data-ttu-id="b7fc4-237">在 Visual Basic 中，請確定您已將 `Public` 關鍵字加入 `Module1`。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-237">In Visual Basic, make sure that you added the `Public` keyword to `Module1`.</span></span> <span data-ttu-id="b7fc4-238">在主控台視窗中輸入加法運算 (例如 "5+3")，而計算機將會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-238">In the console window, type an addition operation, such as "5+3", and the calculator returns the results.</span></span> <span data-ttu-id="b7fc4-239">任何其他運算子都會導致「找不到運算！」</span><span class="sxs-lookup"><span data-stu-id="b7fc4-239">Any other operator results in the "Operation Not Found!"</span></span> <span data-ttu-id="b7fc4-240">回應。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-240">message.</span></span>

## <a name="extending-simplecalculator-using-a-new-class"></a><span data-ttu-id="b7fc4-241">使用新類別擴充 SimpleCalculator</span><span class="sxs-lookup"><span data-stu-id="b7fc4-241">Extending SimpleCalculator using a new class</span></span>

<span data-ttu-id="b7fc4-242">計算機作用之後，要加入新的運算十分簡單。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-242">Now that the calculator works, adding a new operation is easy.</span></span> <span data-ttu-id="b7fc4-243">將下列類別加入模組或 `SimpleCalculator` 命名空間：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-243">Add the following class to the module or `SimpleCalculator` namespace:</span></span>

```vb
<Export(GetType(IOperation))>
<ExportMetadata("Symbol", "-"c)>
Public Class Subtract
    Implements IOperation

    Public Function Operate(left As Integer, right As Integer) As Integer Implements IOperation.Operate
        Return left - right
    End Function
End Class
```

```csharp
[Export(typeof(IOperation))]
[ExportMetadata("Symbol", '-')]
class Subtract : IOperation
{
    public int Operate(int left, int right)
    {
        return left - right;
    }
}
```

<span data-ttu-id="b7fc4-244">編譯並執行專案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-244">Compile and run the project.</span></span> <span data-ttu-id="b7fc4-245">輸入減法運算 (例如 "5-3")。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-245">Type a subtraction operation, such as "5-3".</span></span> <span data-ttu-id="b7fc4-246">計算機現在支援減法和加法。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-246">The calculator now supports subtraction as well as addition.</span></span>

## <a name="extending-simplecalculator-using-a-new-assembly"></a><span data-ttu-id="b7fc4-247">使用新元件擴充 SimpleCalculator</span><span class="sxs-lookup"><span data-stu-id="b7fc4-247">Extending SimpleCalculator using a new assembly</span></span>

<span data-ttu-id="b7fc4-248">將類別加入原始程式碼相當簡單，但是 MEF 可讓您搜尋應用程式專屬組件來源的外部。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-248">Adding classes to the source code is simple enough, but MEF provides the ability to look outside an application’s own source for parts.</span></span> <span data-ttu-id="b7fc4-249">若要示範此情況，您需要修改 SimpleCalculator 來搜尋目錄 (和其專屬組件 (assembly)) 中的組件 (part)，方法是加入 <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog>。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-249">To demonstrate this, you will need to modify SimpleCalculator to search a directory, as well as its own assembly, for parts, by adding a <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog>.</span></span>

<span data-ttu-id="b7fc4-250">將名為 `Extensions` 的新目錄加入至 SimpleCalculator 專案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-250">Add a new directory named `Extensions` to the SimpleCalculator project.</span></span> <span data-ttu-id="b7fc4-251">請務必在專案層級加入它，而非方案層級。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-251">Make sure to add it at the project level, and not at the solution level.</span></span> <span data-ttu-id="b7fc4-252">然後將新的類別庫專案加入至名為 `ExtendedOperations` 的方案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-252">Then add a new Class Library project to the solution, named `ExtendedOperations`.</span></span> <span data-ttu-id="b7fc4-253">新的專案將會編譯成不同的組件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-253">The new project will compile into a separate assembly.</span></span>

<span data-ttu-id="b7fc4-254">開啟 ExtendedOperations 專案的專案屬性設計工具，然後按一下 [**編譯**] 或 [**建立**] 索引標籤。變更**組建輸出路徑**或**輸出路徑**，以指向 SimpleCalculator 專案目錄中的延伸模組目錄 (\*。\SimpleCalculator\Extensions \\ \*) 。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-254">Open the Project Properties Designer for the ExtendedOperations project and click the **Compile** or **Build** tab. Change the **Build output path** or **Output path** to point to the Extensions directory in the SimpleCalculator project directory (*..\SimpleCalculator\Extensions\\*).</span></span>

 <span data-ttu-id="b7fc4-255">在*Module1.vb* *Program.cs*中，將下列程式程式碼加入至函式 `Program` ：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-255">In *Module1.vb* or *Program.cs*, add the following line to the `Program` constructor:</span></span>

```vb
catalog.Catalogs.Add(New DirectoryCatalog("C:\SimpleCalculator\SimpleCalculator\Extensions"))
```

```csharp
catalog.Catalogs.Add(new DirectoryCatalog("C:\\SimpleCalculator\\SimpleCalculator\\Extensions"));
```

<span data-ttu-id="b7fc4-256">請將範例路徑取代為 Extensions 目錄的路徑 。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-256">Replace the example path with the path to your Extensions directory.</span></span> <span data-ttu-id="b7fc4-257">(這個絕對路徑僅供偵錯用途。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-257">(This absolute path is for debugging purposes only.</span></span> <span data-ttu-id="b7fc4-258">在生產應用程式中，您可以使用相對路徑。 ) <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog> 現在將會將擴充功能目錄中任何元件的任何元件新增至組合容器。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-258">In a production application, you would use a relative path.) The <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog> will now add any parts found in any assemblies in the Extensions directory to the composition container.</span></span>

<span data-ttu-id="b7fc4-259">在 ExtendedOperations 專案中，加入 SimpleCalculator 和 System.ComponentModel.Composition 的參考。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-259">In the ExtendedOperations project, add references to SimpleCalculator and System.ComponentModel.Composition.</span></span> <span data-ttu-id="b7fc4-260">在 ExtendedOperations 類別檔案中，針對 System.ComponentModel.Composition 加入 `Imports` 或 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-260">In the ExtendedOperations class file, add an `Imports` or a `using` statement for System.ComponentModel.Composition.</span></span> <span data-ttu-id="b7fc4-261">在 Visual Basic 中，也會針對 SimpleCalculator 加入 `Imports` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-261">In Visual Basic, also add an `Imports` statement for SimpleCalculator.</span></span> <span data-ttu-id="b7fc4-262">然後將下列類別加入 ExtendedOperations 類別檔案：</span><span class="sxs-lookup"><span data-stu-id="b7fc4-262">Then add the following class to the ExtendedOperations class file:</span></span>

```vb
<Export(GetType(SimpleCalculator.IOperation))>
<ExportMetadata("Symbol", "%"c)>
Public Class Modulo
    Implements IOperation

    Public Function Operate(left As Integer, right As Integer) As Integer Implements IOperation.Operate
        Return left Mod right
    End Function
End Class
```

```csharp
[Export(typeof(SimpleCalculator.IOperation))]
[ExportMetadata("Symbol", '%')]
public class Mod : SimpleCalculator.IOperation
{
    public int Operate(int left, int right)
    {
        return left % right;
    }
}
```

<span data-ttu-id="b7fc4-263">請注意，為了讓合約相符，<xref:System.ComponentModel.Composition.ExportAttribute> 屬性的類型必須與 <xref:System.ComponentModel.Composition.ImportAttribute> 相同。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-263">Note that in order for the contract to match, the <xref:System.ComponentModel.Composition.ExportAttribute> attribute must have the same type as the <xref:System.ComponentModel.Composition.ImportAttribute>.</span></span>

<span data-ttu-id="b7fc4-264">編譯並執行專案。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-264">Compile and run the project.</span></span> <span data-ttu-id="b7fc4-265">測試新的 Mod (%) 運算子。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-265">Test the new Mod (%) operator.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b7fc4-266">結論</span><span class="sxs-lookup"><span data-stu-id="b7fc4-266">Conclusion</span></span>

<span data-ttu-id="b7fc4-267">本主題涵蓋 MEF 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-267">This topic covered the basic concepts of MEF.</span></span>

- <span data-ttu-id="b7fc4-268">組件、目錄和組合容器</span><span class="sxs-lookup"><span data-stu-id="b7fc4-268">Parts, catalogs, and the composition container</span></span>

     <span data-ttu-id="b7fc4-269">組件和組合容器是 MEF 應用程式的基本建置組塊。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-269">Parts and the composition container are the basic building blocks of a MEF application.</span></span> <span data-ttu-id="b7fc4-270">組件是匯入或匯出值 (隨本身變化且包含本身) 的任何物件。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-270">A part is any object that imports or exports a value, up to and including itself.</span></span> <span data-ttu-id="b7fc4-271">目錄提供來自特定來源的組件集合。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-271">A catalog provides a collection of parts from a particular source.</span></span> <span data-ttu-id="b7fc4-272">組合容器會使用目錄所提供的組件來執行組合 (將匯入繫結至匯出)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-272">The composition container uses the parts provided by a catalog to perform composition, the binding of imports to exports.</span></span>

- <span data-ttu-id="b7fc4-273">匯入和匯出</span><span class="sxs-lookup"><span data-stu-id="b7fc4-273">Imports and exports</span></span>

     <span data-ttu-id="b7fc4-274">匯入和匯出是元件用來進行通訊的方式。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-274">Imports and exports are the way by which components communicate.</span></span> <span data-ttu-id="b7fc4-275">元件可以透過匯入來指定需要特定的值或物件，而透過匯出則可以指定值的可用性。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-275">With an import, the component specifies a need for a particular value or object, and with an export it specifies the availability of a value.</span></span> <span data-ttu-id="b7fc4-276">每個匯入都會透過其合約與匯出清單進行比對。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-276">Each import is matched with a list of exports by way of its contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7fc4-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7fc4-277">Next steps</span></span>

<span data-ttu-id="b7fc4-278">若要下載此範例的完整程式碼，請參閱 [SimpleCalculator 範例 (Visual Basic) ](/samples/dotnet/samples/simple-calculator-vb/)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-278">To download the complete code for this example, see the [SimpleCalculator sample (Visual Basic)](/samples/dotnet/samples/simple-calculator-vb/).</span></span>

 <span data-ttu-id="b7fc4-279">如需詳細資訊和更多程式碼範例，請參閱 [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-279">For more information and code examples, see [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef).</span></span> <span data-ttu-id="b7fc4-280">如需 MEF 類型的清單，請參閱 <xref:System.ComponentModel.Composition?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="b7fc4-280">For a list of the MEF types, see the <xref:System.ComponentModel.Composition?displayProperty=nameWithType> namespace.</span></span>

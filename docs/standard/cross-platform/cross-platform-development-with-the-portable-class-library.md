---
title: 可攜式類別庫的跨平台開發
ms.date: 09/17/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- Portable Class Library [.NET Framework]
- targeting multiple platforms
- multiple platforms, targeting
ms.assetid: c31e1663-c164-4e65-b66d-d3aa8750a154
ms.openlocfilehash: 033c9bc6e506d0ae2b9f20fedb72d1b7f29e434b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288910"
---
# <a name="cross-platform-development-with-the-portable-class-library"></a><span data-ttu-id="99470-102">使用可移植的類別庫進行跨平臺開發</span><span class="sxs-lookup"><span data-stu-id="99470-102">Cross-platform development with the Portable Class Library</span></span>

<span data-ttu-id="99470-103">Visual Studio 中的可移植類別庫專案類型，可協助您快速且輕鬆地建立適用于 Microsoft 平臺的跨平臺應用程式和程式庫。</span><span class="sxs-lookup"><span data-stu-id="99470-103">The Portable Class Library project type in Visual Studio helps you build cross-platform apps and libraries for Microsoft platforms quickly and easily.</span></span>

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

<span data-ttu-id="99470-104">可攜式類別庫可幫助您減少開發及測試程式碼的時間和成本。</span><span class="sxs-lookup"><span data-stu-id="99470-104">Portable class libraries can help you reduce the time and costs of developing and testing code.</span></span> <span data-ttu-id="99470-105">使用此專案類型來撰寫及建立可移植的 .NET Framework 元件，然後從以多個平臺（例如 .NET Framework、iOS 或 Mac）為目標的應用程式參考這些元件。</span><span class="sxs-lookup"><span data-stu-id="99470-105">Use this project type to write and build portable .NET Framework assemblies, and then reference those assemblies from apps that target multiple platforms such as the .NET Framework, iOS, or Mac.</span></span>

<span data-ttu-id="99470-106">即使在 Visual Studio 中建立可攜式類別庫專案並開始開發之後，您還是可以變更目標平台。</span><span class="sxs-lookup"><span data-stu-id="99470-106">Even after you create a Portable Class Library project in Visual Studio and start developing it, you can change the target platforms.</span></span> <span data-ttu-id="99470-107">Visual Studio 使用新的元件來編譯您的程式庫，以協助您識別需要在程式碼中進行的變更。</span><span class="sxs-lookup"><span data-stu-id="99470-107">Visual Studio compiles your library with the new assemblies, which helps you identify the changes you need to make in your code.</span></span>

## <a name="create-a-portable-class-library-project"></a><span data-ttu-id="99470-108">建立可移植的類別庫專案</span><span class="sxs-lookup"><span data-stu-id="99470-108">Create a Portable Class Library project</span></span>

<span data-ttu-id="99470-109">若要建立可移植的類別庫，請使用 Visual Studio 中提供的範本。</span><span class="sxs-lookup"><span data-stu-id="99470-109">To create a Portable Class Library, use the template provided in Visual Studio.</span></span> <span data-ttu-id="99470-110">建立新的**專案（**  >  [檔案] [**新增專案**]），然後在 [**新增專案**] 對話方塊中，選取您的程式設計語言（Visual c # 或 Visual Basic）。</span><span class="sxs-lookup"><span data-stu-id="99470-110">Create a new project (**File** > **New Project**), and in the **New Project** dialog box, select your programming language (Visual C# or Visual Basic).</span></span> <span data-ttu-id="99470-111">然後，選取 [**類別庫（舊版可移植）** ] 範本。</span><span class="sxs-lookup"><span data-stu-id="99470-111">Then, select the **Class Library (Legacy Portable)** template.</span></span> <span data-ttu-id="99470-112">輸入專案的 [名稱]，然後選擇 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="99470-112">Enter a name for your project and choose **OK**.</span></span>

<span data-ttu-id="99470-113">[**新增可移植的類別庫**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="99470-113">The **Add Portable Class Library** dialog box appears.</span></span> <span data-ttu-id="99470-114">選擇兩個或多個目標，然後選擇 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="99470-114">Choose two or more targets, and then choose **OK**.</span></span>

![在 Visual Studio 中新增可移植的類別庫目標](media/add-portable-class-library.png)

## <a name="change-targets"></a><span data-ttu-id="99470-116">變更目標</span><span class="sxs-lookup"><span data-stu-id="99470-116">Change targets</span></span>

<span data-ttu-id="99470-117">當您建立時，或在開始開發之後，可以變更可移植類別庫專案的目標平臺。</span><span class="sxs-lookup"><span data-stu-id="99470-117">You can change the target platforms of a portable class library project when you create it or after you've started development.</span></span> <span data-ttu-id="99470-118">如果您想要在建立專案之後變更目標，請在 [**方案總管**中，開啟您的可移植類別庫專案（而非方案）的快捷方式功能表，然後選擇 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="99470-118">If you want to change the targets after you've created your project, in **Solution Explorer**, open the shortcut menu for your Portable Class Library project (not the solution), and then choose **Properties**.</span></span> <span data-ttu-id="99470-119">在 [專案屬性] 頁面上，[連結**庫**] 索引標籤會顯示您的專案目前的目標平臺。</span><span class="sxs-lookup"><span data-stu-id="99470-119">On the project properties page, the **Library** tab shows the platforms that your project currently targets.</span></span>

![Visual Studio 中可移植類別庫的專案屬性](media/pcl-project-properties.png)

<span data-ttu-id="99470-121">若要新增或移除目標，請選擇 [**變更**] 按鈕，然後選取並清除適當的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="99470-121">To add or remove targets, choose the **Change** button, and then select and clear the appropriate check boxes.</span></span>

<span data-ttu-id="99470-122">當您變更目標時，可供您用來開發專案的 API 會變更，以配合您的選項。</span><span class="sxs-lookup"><span data-stu-id="99470-122">When you change the targets, the APIs that are available to you for developing your project will change to match your selection.</span></span> <span data-ttu-id="99470-123">Visual Studio 會提報因為目標變更而可能發生的錯誤和警告。</span><span class="sxs-lookup"><span data-stu-id="99470-123">Visual Studio reports the errors and warnings that may occur as a result of the targets changing.</span></span>

<span data-ttu-id="99470-124">如果您想要先評估元件的可攜性，再于 Visual Studio 中進行變更，您可以使用[.net 可攜性分析器](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)。</span><span class="sxs-lookup"><span data-stu-id="99470-124">If you want to evaluate the portability of your assemblies before you make changes in Visual Studio, you can use the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span>

## <a name="supported-types-and-members"></a><span data-ttu-id="99470-125">支援的類型和成員</span><span class="sxs-lookup"><span data-stu-id="99470-125">Supported types and members</span></span>

<span data-ttu-id="99470-126">可攜式類別庫專案中提供的類型和成員受到多個相容性因素所限制：</span><span class="sxs-lookup"><span data-stu-id="99470-126">The types and members that are available in Portable Class Library projects are constrained by several compatibility factors:</span></span>

- <span data-ttu-id="99470-127">它們必須在您選取的目標之間共用。</span><span class="sxs-lookup"><span data-stu-id="99470-127">They must be shared across the targets you selected.</span></span>

- <span data-ttu-id="99470-128">它們必須在這些目標上具有類似的行為。</span><span class="sxs-lookup"><span data-stu-id="99470-128">The must behave similarly across those targets.</span></span>

- <span data-ttu-id="99470-129">它們不能是要被取代的候選項。</span><span class="sxs-lookup"><span data-stu-id="99470-129">They must not be candidates for deprecation.</span></span>

- <span data-ttu-id="99470-130">它們在可攜式環境中必須是合理的，尤其是支援成員無法移植時。</span><span class="sxs-lookup"><span data-stu-id="99470-130">They must make sense in a portable environment, especially when supporting members are not portable.</span></span>

<span data-ttu-id="99470-131">如果可攜式類別庫和您選取的目標可支援某成員，該成員就會出現在 IntelliSense 的專案中。</span><span class="sxs-lookup"><span data-stu-id="99470-131">If a member is supported in the Portable Class Library and for your selected targets, it will appear in your project in IntelliSense.</span></span> <span data-ttu-id="99470-132">不過，請記得，可攜式類別庫可能會支援 API，但您是否可以使用 API，取決於您選取的目標。</span><span class="sxs-lookup"><span data-stu-id="99470-132">However, remember that an API may be supported in the Portable Class Library, but whether you can use the API depends on the targets you select.</span></span>

## <a name="api-differences-in-the-portable-class-library"></a><span data-ttu-id="99470-133">可攜式類別庫中的 API 差異</span><span class="sxs-lookup"><span data-stu-id="99470-133">API differences in the Portable Class Library</span></span>

<span data-ttu-id="99470-134">為了讓可攜式類別庫組件在所有支援的平台上都相容，可攜式類別庫中有部分成員已稍微變更。</span><span class="sxs-lookup"><span data-stu-id="99470-134">To make Portable Class Library assemblies compatible across all supported platforms, some members have been slightly changed in the Portable Class Library.</span></span>

## <a name="use-the-portable-class-library"></a><span data-ttu-id="99470-135">使用可移植的類別庫</span><span class="sxs-lookup"><span data-stu-id="99470-135">Use the Portable Class Library</span></span>

<span data-ttu-id="99470-136">建立可攜式類別庫專案之後，即可從其他專案參考該專案。</span><span class="sxs-lookup"><span data-stu-id="99470-136">After you build your Portable Class Library project, you just reference it from other projects.</span></span> <span data-ttu-id="99470-137">您可以參考此專案，或是包含您想要存取之類別的特定組件。</span><span class="sxs-lookup"><span data-stu-id="99470-137">You can reference either the project or specific assemblies that contain the classes you want to access.</span></span>

<span data-ttu-id="99470-138">若要執行參考可攜式類別庫組件的應用程式，電腦上必須安裝目標平台所需的版本 (或以後版本)。</span><span class="sxs-lookup"><span data-stu-id="99470-138">To run an app that references a Portable Class Library assembly, the required version (or later) of the targeted platforms must be installed on your computer.</span></span> <span data-ttu-id="99470-139">Visual Studio 包含所有必要架構，因此不需要進一步修改用來開發應用程式的電腦，即可執行該應用程式。</span><span class="sxs-lookup"><span data-stu-id="99470-139">Visual Studio contains all the required frameworks, so you can run the app without further modification on the computer that you used to develop the app.</span></span>

### <a name="deploy-a-universal-windows-app"></a><span data-ttu-id="99470-140">部署通用 Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="99470-140">Deploy a Universal Windows app</span></span>

<span data-ttu-id="99470-141">當您建立參考可移植類別庫元件的通用 Windows 應用程式時，您部署應用程式所需的所有專案都會包含在應用程式套件中，而且不需要進一步的步驟。</span><span class="sxs-lookup"><span data-stu-id="99470-141">When you create a Universal Windows app that references a Portable Class Library assembly, everything you need to deploy the app is included in the app package, and no further steps are required.</span></span>

### <a name="deploy-a-net-framework-app"></a><span data-ttu-id="99470-142">部署 .NET Framework 應用程式</span><span class="sxs-lookup"><span data-stu-id="99470-142">Deploy a .NET Framework app</span></span>

<span data-ttu-id="99470-143">當您部署參考可攜式類別庫組件的 .NET Framework 應用程式時，必須指定正確 .NET Framework 版本的相依性。</span><span class="sxs-lookup"><span data-stu-id="99470-143">When you deploy a .NET Framework app that references a Portable Class Library assembly, you must specify a dependency on the correct version of the .NET Framework.</span></span> <span data-ttu-id="99470-144">藉由指定此相依性，您就可以確保所需的版本會隨著您的應用程式一起安裝。</span><span class="sxs-lookup"><span data-stu-id="99470-144">By specifying this dependency, you ensure that the required version is installed with your app.</span></span>

- <span data-ttu-id="99470-145">若要建立與 ClickOnce 部署的相依性：在**方案總管**中，選擇您要發行之專案的專案節點。</span><span class="sxs-lookup"><span data-stu-id="99470-145">To create a dependency with ClickOnce deployment: In **Solution Explorer**, choose the project node for the project you want to publish.</span></span> <span data-ttu-id="99470-146">（這是參考可移植類別庫專案的專案）。在功能表列上，選擇 [**專案**  >  **屬性**]，然後選擇 [**發行**] 索引標籤。在 [**發行**] 頁面上，選擇 [**必要條件**]。</span><span class="sxs-lookup"><span data-stu-id="99470-146">(This is the project that references the Portable Class Library project.) On the menu bar, choose **Project** > **Properties**, and then choose the **Publish** tab. On the **Publish** page, choose **Prerequisites**.</span></span> <span data-ttu-id="99470-147">選取所需的 .NET Framework 版本做為必要條件。</span><span class="sxs-lookup"><span data-stu-id="99470-147">Select the required .NET Framework version as a prerequisite.</span></span>

- <span data-ttu-id="99470-148">若要建立與安裝專案的相依性：在**方案總管**中，選擇安裝專案。</span><span class="sxs-lookup"><span data-stu-id="99470-148">To create a dependency with a setup project: In **Solution Explorer**, choose the setup project.</span></span> <span data-ttu-id="99470-149">在功能表列上，選擇 [**專案**  >  **屬性**] [  >  **必要條件**]。</span><span class="sxs-lookup"><span data-stu-id="99470-149">On the menu bar, choose **Project** > **Properties** > **Prerequisites**.</span></span> <span data-ttu-id="99470-150">選取所需的 .NET Framework 版本做為必要條件。</span><span class="sxs-lookup"><span data-stu-id="99470-150">Select the required .NET Framework version as a prerequisite.</span></span>

<span data-ttu-id="99470-151">如需部署 .NET Framework 應用程式的詳細資訊，請參閱[開發人員部署指南](../../framework/deployment/deployment-guide-for-developers.md)。</span><span class="sxs-lookup"><span data-stu-id="99470-151">For more information about deploying .NET Framework apps, see [Deployment Guide for Developers](../../framework/deployment/deployment-guide-for-developers.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="99470-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="99470-152">See also</span></span>

- [<span data-ttu-id="99470-153">搭配 MVVM 使用可攜式類別庫</span><span class="sxs-lookup"><span data-stu-id="99470-153">Using Portable Class Library with MVVM</span></span>](using-portable-class-library-with-model-view-view-model.md)
- [<span data-ttu-id="99470-154">以多平臺為目標之程式庫的應用程式資源</span><span class="sxs-lookup"><span data-stu-id="99470-154">App Resources for Libraries That Target Multiple Platforms</span></span>](app-resources-for-libraries-that-target-multiple-platforms.md)
- [<span data-ttu-id="99470-155">.NET Portability Analyzer</span><span class="sxs-lookup"><span data-stu-id="99470-155">.NET Portability Analyzer</span></span>](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)
- [<span data-ttu-id="99470-156">適用於 Windows 市集應用程式和 Windows 執行階段的 .NET Framework 支援</span><span class="sxs-lookup"><span data-stu-id="99470-156">.NET Framework Support for Windows Store Apps and Windows Runtime</span></span>](support-for-windows-store-apps-and-windows-runtime.md)
- [<span data-ttu-id="99470-157">部署</span><span class="sxs-lookup"><span data-stu-id="99470-157">Deployment</span></span>](../../framework/deployment/net-framework-applications.md)

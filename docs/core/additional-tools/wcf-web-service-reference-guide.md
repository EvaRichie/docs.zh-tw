---
title: 新增 WCF Web Service Reference
description: 新增 .NET Core 和 ASP.NET Core 專案功能的 Microsoft WCF Web Service Reference Provider 工具概觀，與 .NET Framework 專案的「新增服務參考」類似。
author: dasetser
ms.date: 10/29/2019
ms.custom: mvc
ms.openlocfilehash: 1f7b1831a956553dbef26f58f4f257c2f3914ede
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400600"
---
# <a name="use-the-wcf-web-service-reference-provider-tool"></a><span data-ttu-id="2c9e7-103">使用 WCF Web Service Reference Provider 工具</span><span class="sxs-lookup"><span data-stu-id="2c9e7-103">Use the WCF Web Service Reference Provider Tool</span></span>

<span data-ttu-id="2c9e7-104">多年來，許多 Visual Studio 開發人員都享受 [**新增服務參考**](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference)工具在其 .NET Framework 專案需要存取 Web 服務時所提供的生產力。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-104">Over the years, many Visual Studio developers have enjoyed the productivity that the [**Add Service Reference**](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference) tool provided when their .NET Framework projects needed to access web services.</span></span>  <span data-ttu-id="2c9e7-105">**WCF Web Service Reference** 工具是 Visual Studio 連線服務延伸模組，以針對 .NET Core 和 ASP.NET Core 專案提供「新增服務參考」功能這類體驗。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-105">The **WCF Web Service Reference** tool is a Visual Studio connected service extension that provides an experience like the Add Service Reference functionality for .NET Core and ASP.NET Core projects.</span></span> <span data-ttu-id="2c9e7-106">此工具可從目前解決方案中的 Web 服務、網路位置或 WSDL 檔案擷取中繼資料，且能產生與 .NET Core 相容的來源檔案，其中包含的 Windows Communication Foundation (WCF) 用戶端 Proxy 程式碼可讓您用於存取 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-106">This tool retrieves metadata from a web service in the current solution, on a network location, or from a WSDL file, and generates a .NET Core compatible source file containing Windows Communication Foundation (WCF) client proxy code that you can use to access the web service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c9e7-107">您只應該參考來自信任來源的服務。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-107">You should only reference services from a trusted source.</span></span> <span data-ttu-id="2c9e7-108">新增不信任來源的參考可能會危及安全性。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-108">Adding references from an untrusted source may compromise security.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c9e7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="2c9e7-109">Prerequisites</span></span>

- <span data-ttu-id="2c9e7-110">[Visual Studio 2017 15.5 版](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="2c9e7-110">[Visual Studio 2017 version 15.5](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) or later versions</span></span>

## <a name="how-to-use-the-extension"></a><span data-ttu-id="2c9e7-111">如何使用延伸模組</span><span class="sxs-lookup"><span data-stu-id="2c9e7-111">How to use the extension</span></span>

> [!NOTE]
> <span data-ttu-id="2c9e7-112">**WCF Web Service Reference** 選項適用於使用下列專案範本建立的專案：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-112">The **WCF Web Service Reference** option is applicable to projects created using the following project templates:</span></span>
>
> - <span data-ttu-id="2c9e7-113">**Visual c #**  > **.Net Core**</span><span class="sxs-lookup"><span data-stu-id="2c9e7-113">**Visual C#** > **.NET Core**</span></span>
> - <span data-ttu-id="2c9e7-114">**Visual c #**  > **.NET Standard**</span><span class="sxs-lookup"><span data-stu-id="2c9e7-114">**Visual C#** > **.NET Standard**</span></span>
> - <span data-ttu-id="2c9e7-115">**Visual c #**  > **Web**  > **ASP.NET Core Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="2c9e7-115">**Visual C#** > **Web** > **ASP.NET Core Web Application**</span></span>

<span data-ttu-id="2c9e7-116">使用 **ASP.NET Core Web 應用程式** 專案範本作為範例，本文會引導您完成將 WCF 服務參考新增至專案：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-116">Using the **ASP.NET Core Web Application** project template as an example, this article walks you through adding a WCF service reference to the project:</span></span>

1. <span data-ttu-id="2c9e7-117">在方案總管中，按兩下專案的 [已連線的服務] 節點 (針對 .NET Core 或 .NET Standard 專案，在方案總管中，以滑鼠右鍵按一下專案的 [相依性] 節點時，可以使用此選項)。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-117">In Solution Explorer, double-click the **Connected Services** node of the project (for a .NET Core or .NET Standard project this option is available when you right-click on the **Dependencies** node of the project in Solution Explorer).</span></span>

    <span data-ttu-id="2c9e7-118">[已連線的服務] 頁面隨即顯示 (如下圖所示)：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-118">The **Connected Services** page appears as shown in the following image:</span></span>

    ![適用於 .NET Core 的 [Visual Studio 連線服務] 索引標籤](./media/wcf-web-service-reference-guide/wcfcs-ConnectedServicesPage.png)

2. <span data-ttu-id="2c9e7-120">在 [已連線的服務] 頁面上，按一下 [Microsoft WCF Web Service Reference Provider]。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-120">On the **Connected Services** page, click **Microsoft WCF Web Service Reference Provider**.</span></span> <span data-ttu-id="2c9e7-121">這會啟動 [設定 WCF Web 服務參考精靈]：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-121">This brings up the **Configure WCF Web Service Reference** wizard:</span></span>

    ![適用於 .NET Core 的 [Visual Studio 服務端點] 索引標籤](./media/wcf-web-service-reference-guide/wcfcs-ServiceEndpointPage.png)

3. <span data-ttu-id="2c9e7-123">選取服務。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-123">Select a service.</span></span>

    <span data-ttu-id="2c9e7-124">3a.</span><span class="sxs-lookup"><span data-stu-id="2c9e7-124">3a.</span></span> <span data-ttu-id="2c9e7-125">[設定 WCF Web 服務參考精靈] 內有數個服務搜尋選項可用：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-125">There are several services search options available within the **Configure WCF Web Service Reference** wizard:</span></span>

     * <span data-ttu-id="2c9e7-126">若要搜尋目前方案中所定義的服務，請按一下 [探索] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-126">To search for services defined in the current solution, click the **Discover** button.</span></span>
     * <span data-ttu-id="2c9e7-127">若要搜尋所指定位址裝載的服務，請在 [位址] 方塊中輸入服務 URL，然後按一下 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-127">To search for services hosted at a specified address, enter a service URL in the **Address** box and click the **Go** button.</span></span>
     * <span data-ttu-id="2c9e7-128">若要選取包含 Web 服務中繼資料資訊的 WSDL 檔案，請按一下 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-128">To select a WSDL file that contains the web service metadata information, click the **Browse** button.</span></span>

    <span data-ttu-id="2c9e7-129">3b.</span><span class="sxs-lookup"><span data-stu-id="2c9e7-129">3b.</span></span> <span data-ttu-id="2c9e7-130">在 [服務] 方塊中，從搜尋結果清單中選取服務。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-130">Select the service from the search results list in the **Services** box.</span></span> <span data-ttu-id="2c9e7-131">如有需要，請在對應的 [命名空間] 文字方塊中輸入已產生程式碼的命名空間。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-131">If needed, enter the namespace for the generated code in the corresponding **Namespace** text box.</span></span>

    <span data-ttu-id="2c9e7-132">3c.</span><span class="sxs-lookup"><span data-stu-id="2c9e7-132">3c.</span></span> <span data-ttu-id="2c9e7-133">按一下 [下一步] 按鈕以開啟 [資料類型選項] 和 [用戶端選項] 頁面。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-133">Click the **Next** button to open the **Data Type Options** and the **Client Options** pages.</span></span> <span data-ttu-id="2c9e7-134">或者，按一下 [完成] 按鈕以使用預設選項。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-134">Alternatively, click the **Finish** button to use the default options.</span></span>

4. <span data-ttu-id="2c9e7-135">[資料類型選項] 表單可讓您精簡所產生的服務參考組態設定：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-135">The **Data Type Options** form enables you to refine the generated service reference configuration settings:</span></span>

    ![適用於 .NET Core 的 [Visual Studio 資料類型選項] 索引標籤](./media/wcf-web-service-reference-guide/wcfcs-DataTypesPage.png)

    > [!NOTE]
    > <span data-ttu-id="2c9e7-137">其中一個專案的參考組件內定義服務參考程式碼產生所需的資料類型時，[重複使用參考組件中的類型] 核取方塊選項十分有用。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-137">The **Reuse types in referenced assemblies** check box option is useful when data types needed for service reference code generation are defined in one of your project's referenced assemblies.</span></span>  <span data-ttu-id="2c9e7-138">請務必重複使用這些現有資料類型，避免造成編譯時期類型衝突或執行階段問題。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-138">It's important to reuse those existing data types to avoid compile-time type clash or runtime issues.</span></span>

    <span data-ttu-id="2c9e7-139">根據專案相依性數目和其他系統效能因素，在載入類型資訊時可能會延遲。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-139">There may be a delay while type information is loaded, depending on the number of project dependencies and other system performance factors.</span></span> <span data-ttu-id="2c9e7-140">除非取消核取 [重複使用參考組件中的類型] 核取方塊，否則會在載入期間停用 [完成] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-140">The **Finish** button is disabled during loading unless the **Reuse types in referenced assemblies** check box is unchecked.</span></span>

5. <span data-ttu-id="2c9e7-141">完成時，請按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-141">Click **Finish** when you are done.</span></span>

<span data-ttu-id="2c9e7-142">顯示進度時，此工具會：</span><span class="sxs-lookup"><span data-stu-id="2c9e7-142">While displaying progress, the tool:</span></span>

- <span data-ttu-id="2c9e7-143">從 WCF 服務下載中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-143">Downloads metadata from the WCF service.</span></span>
- <span data-ttu-id="2c9e7-144">在名為 *reference.cs* 的檔案中產生服務參考程式碼，並將它新增至 [已連線的服務] 節點下方的專案。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-144">Generates the service reference code in a file named *reference.cs* , and adds it to your project under the **Connected Services** node.</span></span>
- <span data-ttu-id="2c9e7-145">使用在目標平台上編譯和執行所需的 NuGet 套件參考來更新專案檔 (.csproj)。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-145">Updates the project file (.csproj) with NuGet package references required to compile and run on the target platform.</span></span>

![Visual Studio 進度視窗](./media/wcf-web-service-reference-guide/wcfcs-ProgressWindow.png)

<span data-ttu-id="2c9e7-147">完成這些程序時，您可以建立已產生 WCF 用戶端類型的執行個體，並叫用服務作業。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-147">When these processes complete, you can create an instance of the generated WCF client type and invoke the service operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="2c9e7-148">請參閱</span><span class="sxs-lookup"><span data-stu-id="2c9e7-148">See also</span></span>

- [<span data-ttu-id="2c9e7-149">開始使用 Windows Communication Foundation 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c9e7-149">Get started with Windows Communication Foundation applications</span></span>](../../framework/wcf/getting-started-tutorial.md)
- [<span data-ttu-id="2c9e7-150">Visual Studio 中的 Windows Communication Foundation 服務和 WCF 資料服務</span><span class="sxs-lookup"><span data-stu-id="2c9e7-150">Windows Communication Foundation services and WCF data services in Visual Studio</span></span>](/visualstudio/data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio)
- [<span data-ttu-id="2c9e7-151">.NET Core 上的 WCF 支援功能</span><span class="sxs-lookup"><span data-stu-id="2c9e7-151">WCF supported features on .NET Core</span></span>](https://github.com/dotnet/wcf/blob/master/release-notes/SupportedFeatures-v2.1.0.md)

## <a name="feedback--questions"></a><span data-ttu-id="2c9e7-152">意見反應和問題</span><span class="sxs-lookup"><span data-stu-id="2c9e7-152">Feedback & questions</span></span>

<span data-ttu-id="2c9e7-153">如果您有任何產品意見反應，請使用「回報[問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)」工具在[開發人員社群](https://aka.ms/feedback/report?space=61)上報告。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-153">If you have any product feedback, report it at [Developer Community](https://aka.ms/feedback/report?space=61) using the [Report a problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) tool.</span></span>

## <a name="release-notes"></a><span data-ttu-id="2c9e7-154">版本資訊</span><span class="sxs-lookup"><span data-stu-id="2c9e7-154">Release notes</span></span>

- <span data-ttu-id="2c9e7-155">如需已更新的版本資訊，請參閱[版本資訊](https://github.com/dotnet/wcf/blob/master/release-notes/WCF-Web-Service-Reference-notes.md) (包含已知問題)。</span><span class="sxs-lookup"><span data-stu-id="2c9e7-155">Refer to the [Release notes](https://github.com/dotnet/wcf/blob/master/release-notes/WCF-Web-Service-Reference-notes.md) for updated release information, including known issues.</span></span>

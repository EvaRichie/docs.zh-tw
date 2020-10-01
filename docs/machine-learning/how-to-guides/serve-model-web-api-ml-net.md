---
title: 在 ASP.NET Core Web API 中部署模型
description: 使用 ASP.NET Core Web API 在網際網路上提供 ML.NET 情感分析機器學習模型
ms.date: 11/07/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: f588d4681ee277ad15b50d5553473b1c9e84d578
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608760"
---
# <a name="deploy-a-model-in-an-aspnet-core-web-api"></a><span data-ttu-id="53da0-103">在 ASP.NET Core Web API 中部署模型</span><span class="sxs-lookup"><span data-stu-id="53da0-103">Deploy a model in an ASP.NET Core Web API</span></span>

<span data-ttu-id="53da0-104">了解如何使用 ASP.NET Core Web API，在 Web 上提供預先定型的 ML.NET 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-104">Learn how to serve a pre-trained ML.NET machine learning model on the web using an ASP.NET Core Web API.</span></span> <span data-ttu-id="53da0-105">透過 Web API 提供模型可讓您透過標準 HTTP 方法進行預測。</span><span class="sxs-lookup"><span data-stu-id="53da0-105">Serving a model over a web API enables predictions via standard HTTP methods.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53da0-106">先決條件</span><span class="sxs-lookup"><span data-stu-id="53da0-106">Prerequisites</span></span>

- <span data-ttu-id="53da0-107">已安裝「.NET Core 跨平臺開發」工作負載， [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)或更新版本或 Visual Studio 2017 15.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="53da0-107">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or later or Visual Studio 2017 version 15.6 or later with the ".NET Core cross-platform development" workload installed.</span></span>
- <span data-ttu-id="53da0-108">PowerShell。</span><span class="sxs-lookup"><span data-stu-id="53da0-108">PowerShell.</span></span>
- <span data-ttu-id="53da0-109">預先定型的模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-109">Pre-trained model.</span></span> <span data-ttu-id="53da0-110">使用 [ML.NET 情感分析教學課程](../tutorials/sentiment-analysis.md)來建置您自己的模型，或是下載這個[預先定型的情感分析機器學習模型](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)</span><span class="sxs-lookup"><span data-stu-id="53da0-110">Use the [ML.NET Sentiment Analysis tutorial](../tutorials/sentiment-analysis.md) to build your own model or download this [pre-trained sentiment analysis machine learning model](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)</span></span>

## <a name="create-aspnet-core-web-api-project"></a><span data-ttu-id="53da0-111">建立 ASP.NET Core Web API 專案</span><span class="sxs-lookup"><span data-stu-id="53da0-111">Create ASP.NET Core Web API project</span></span>

1. <span data-ttu-id="53da0-112">開啟 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="53da0-112">Open Visual Studio 2017.</span></span> <span data-ttu-id="53da0-113">從功能表列中選取 [檔案] > [新增] > [專案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-113">Select **File > New > Project** from the menu bar.</span></span> <span data-ttu-id="53da0-114">在 [新增專案] 對話方塊中，選取 [Visual C#]\*\*\*\* 節點，然後選取 [Web]\*\*\*\* 節點。</span><span class="sxs-lookup"><span data-stu-id="53da0-114">In the New Project dialog, select the **Visual C#** node followed by the **Web** node.</span></span> <span data-ttu-id="53da0-115">然後，選取 [ASP.NET Core Web 應用程式]\*\*\*\* 專案範本。</span><span class="sxs-lookup"><span data-stu-id="53da0-115">Then select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="53da0-116">在 [名稱]\*\*\*\* 文字方塊中，輸入 "SentimentAnalysisWebAPI"，然後選取 [確定]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-116">In the **Name** text box, type "SentimentAnalysisWebAPI" and then select the **OK** button.</span></span>

1. <span data-ttu-id="53da0-117">在顯示不同類型的 ASP.NET Core 專案的視窗中，選取 [API]\*\*\*\*，然後選取 [確定]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-117">In the window that displays the different types of ASP.NET Core Projects, select **API** and the select the **OK** button.</span></span>

1. <span data-ttu-id="53da0-118">在專案中建立名為 *MLModels* 的目錄，以儲存您預先建置的機器學習模型檔案：</span><span class="sxs-lookup"><span data-stu-id="53da0-118">Create a directory named *MLModels* in your project to save your pre-built machine learning model files:</span></span>

    <span data-ttu-id="53da0-119">在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="53da0-119">In Solution Explorer, right-click on your project and select Add > New Folder.</span></span> <span data-ttu-id="53da0-120">輸入 "MLModels"，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="53da0-120">Type "MLModels" and hit Enter.</span></span>

1. <span data-ttu-id="53da0-121">安裝「Microsoft.ML NuGet 套件」\*\*\*\*：</span><span class="sxs-lookup"><span data-stu-id="53da0-121">Install the **Microsoft.ML NuGet Package**:</span></span>

    <span data-ttu-id="53da0-122">在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-122">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="53da0-123">選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 **Microsoft.ML**、從清單中選取該套件，然後選取 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-123">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**, select that package in the list, and select the Install button.</span></span> <span data-ttu-id="53da0-124">在 [預覽變更]\*\*\*\* 對話方塊上，選取 [確定]\*\*\*\* 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-124">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the License Acceptance dialog if you agree with the license terms for the packages listed.</span></span>

1. <span data-ttu-id="53da0-125">安裝 **Microsoft.Extensions.ML Nuget 套件**：</span><span class="sxs-lookup"><span data-stu-id="53da0-125">Install the **Microsoft.Extensions.ML Nuget Package**:</span></span>

    <span data-ttu-id="53da0-126">在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-126">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="53da0-127">選擇 "nuget.org" 作為 [套件來源]、選取 [瀏覽] 索引標籤、搜尋 **Microsoft.Extensions.ML**、從清單中選取該套件，然後選取 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-127">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.Extensions.ML**, select that package in the list, and select the Install button.</span></span> <span data-ttu-id="53da0-128">在 [預覽變更]\*\*\*\* 對話方塊上，選取 [確定]\*\*\*\* 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-128">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the License Acceptance dialog if you agree with the license terms for the packages listed.</span></span>

### <a name="add-model-to-aspnet-core-web-api-project"></a><span data-ttu-id="53da0-129">將模型新增至 ASP.NET Core Web API 專案</span><span class="sxs-lookup"><span data-stu-id="53da0-129">Add model to ASP.NET Core Web API project</span></span>

1. <span data-ttu-id="53da0-130">將預先建置的模型複製到 *MLModels* 目錄</span><span class="sxs-lookup"><span data-stu-id="53da0-130">Copy your pre-built model to the *MLModels* directory</span></span>
1. <span data-ttu-id="53da0-131">在 [方案總管] 中，以滑鼠右鍵按一下模型 zip 檔案，並選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="53da0-131">In Solution Explorer, right-click the model zip file and select Properties.</span></span> <span data-ttu-id="53da0-132">在 [進階] 下，將 [複製到輸出目錄] 的值變更為 [有更新才複製]。</span><span class="sxs-lookup"><span data-stu-id="53da0-132">Under Advanced, change the value of Copy to Output Directory to Copy if newer.</span></span>

## <a name="create-data-models"></a><span data-ttu-id="53da0-133">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="53da0-133">Create data models</span></span>

<span data-ttu-id="53da0-134">您必須為輸入資料和預測建立一些類別。</span><span class="sxs-lookup"><span data-stu-id="53da0-134">You need to create some classes for your input data and predictions.</span></span> <span data-ttu-id="53da0-135">將新類別新增至專案：</span><span class="sxs-lookup"><span data-stu-id="53da0-135">Add a new class to your project:</span></span>

1. <span data-ttu-id="53da0-136">在您的專案中建立名為 *DataModels* 的目錄以儲存資料模型：</span><span class="sxs-lookup"><span data-stu-id="53da0-136">Create a directory named *DataModels* in your project to save your data models:</span></span>

    <span data-ttu-id="53da0-137">在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="53da0-137">In Solution Explorer, right-click on your project and select Add > New Folder.</span></span> <span data-ttu-id="53da0-138">輸入 "DataModels"，然後按 **Enter 鍵**。</span><span class="sxs-lookup"><span data-stu-id="53da0-138">Type "DataModels" and hit **Enter**.</span></span>

2. <span data-ttu-id="53da0-139">在 [方案總管] 中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="53da0-139">In Solution Explorer, right-click the *DataModels* directory, and then select Add > New Item.</span></span>
3. <span data-ttu-id="53da0-140">在 [新增項目]\*\*\*\* 對話方塊中，選取 [類別]\*\*\*\*，然後將 [名稱]\*\*\*\* 欄位變更為 *SentimentData.cs*。</span><span class="sxs-lookup"><span data-stu-id="53da0-140">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *SentimentData.cs*.</span></span> <span data-ttu-id="53da0-141">接著，選取 [新增]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-141">Then, select the **Add** button.</span></span> <span data-ttu-id="53da0-142">*SentimentData.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="53da0-142">The *SentimentData.cs* file opens in the code editor.</span></span> <span data-ttu-id="53da0-143">將下列 using 陳述式新增至 *SentimentData.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="53da0-143">Add the following using statement to the top of *SentimentData.cs*:</span></span>

    ```csharp
    using Microsoft.ML.Data;
    ```

    <span data-ttu-id="53da0-144">移除現有的類別定義，然後將下列程式碼新增至 **SentimentData.cs** 檔案：</span><span class="sxs-lookup"><span data-stu-id="53da0-144">Remove the existing class definition and add the following code to the **SentimentData.cs** file:</span></span>

    ```csharp
    public class SentimentData
    {
        [LoadColumn(0)]
        public string SentimentText;

        [LoadColumn(1)]
        [ColumnName("Label")]
        public bool Sentiment;
    }
    ```

4. <span data-ttu-id="53da0-145">在方案總管中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [ **新增 > 新專案**]。</span><span class="sxs-lookup"><span data-stu-id="53da0-145">In Solution Explorer, right-click the *DataModels* directory, and then select **Add > New Item**.</span></span>
5. <span data-ttu-id="53da0-146">在 [加入新項目]\*\*\*\* 對話方塊中，選取 [類別]\*\*\*\*，然後將 [名稱]\*\*\*\* 欄位變更為 *SentimentPrediction.cs*。</span><span class="sxs-lookup"><span data-stu-id="53da0-146">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *SentimentPrediction.cs*.</span></span> <span data-ttu-id="53da0-147">接著，選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-147">Then, select the Add button.</span></span> <span data-ttu-id="53da0-148">*SentimentPrediction.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="53da0-148">The *SentimentPrediction.cs* file opens in the code editor.</span></span> <span data-ttu-id="53da0-149">將下列 using 陳述式新增至 *SentimentPrediction.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="53da0-149">Add the following using statement to the top of *SentimentPrediction.cs*:</span></span>

    ```csharp
    using Microsoft.ML.Data;
    ```

    <span data-ttu-id="53da0-150">移除現有的類別定義，然後將下列程式碼新增至 *SentimentPrediction.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="53da0-150">Remove the existing class definition and add the following code to the *SentimentPrediction.cs* file:</span></span>

    ```csharp
    public class SentimentPrediction : SentimentData
    {

        [ColumnName("PredictedLabel")]
        public bool Prediction { get; set; }

        public float Probability { get; set; }

        public float Score { get; set; }
    }
    ```

    <span data-ttu-id="53da0-151">`SentimentPrediction` 繼承自 `SentimentData`。</span><span class="sxs-lookup"><span data-stu-id="53da0-151">`SentimentPrediction` inherits from `SentimentData`.</span></span> <span data-ttu-id="53da0-152">這可讓您更輕易地看到 `SentimentText` 屬性中的原始資料，以及模型所產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="53da0-152">This makes it easier to see the original data in the `SentimentText` property along with the output generated by the model.</span></span>

## <a name="register-predictionenginepool-for-use-in-the-application"></a><span data-ttu-id="53da0-153">登錄 PredictionEnginePool 以在應用程式中使用</span><span class="sxs-lookup"><span data-stu-id="53da0-153">Register PredictionEnginePool for use in the application</span></span>

<span data-ttu-id="53da0-154">若要進行單一預測，您必須建立 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 。</span><span class="sxs-lookup"><span data-stu-id="53da0-154">To make a single prediction, you have to create a [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602).</span></span> <span data-ttu-id="53da0-155">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 不是安全線程。</span><span class="sxs-lookup"><span data-stu-id="53da0-155">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) is not thread-safe.</span></span> <span data-ttu-id="53da0-156">此外，您必須在應用程式內需要的任何地方建立其實例。</span><span class="sxs-lookup"><span data-stu-id="53da0-156">Additionally, you have to create an instance of it everywhere it is needed within your application.</span></span> <span data-ttu-id="53da0-157">當您的應用程式成長時，此程式可能會變得難以管理。</span><span class="sxs-lookup"><span data-stu-id="53da0-157">As your application grows, this process can become unmanageable.</span></span> <span data-ttu-id="53da0-158">為了改善效能和執行緒安全性，請使用相依性插入和服務的組合 `PredictionEnginePool` ，以建立可 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 在整個應用程式中使用的物件。</span><span class="sxs-lookup"><span data-stu-id="53da0-158">For improved performance and thread safety, use a combination of dependency injection and the `PredictionEnginePool` service, which creates an [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) of [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) objects for use throughout your application.</span></span>

<span data-ttu-id="53da0-159">如果您想要深入瞭解 [ASP.NET Core 中](/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1)的相依性插入，下列連結會提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="53da0-159">The following link provides more information if you want to learn more about [dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1).</span></span>

1. <span data-ttu-id="53da0-160">開啟 *Startup.cs* 類別，並將下列 using 陳述式新增至檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="53da0-160">Open the *Startup.cs* class and add the following using statement to the top of the file:</span></span>

    ```csharp
    using Microsoft.AspNetCore.Builder;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

2. <span data-ttu-id="53da0-161">將下列程式碼新增到 *ConfigureServices* 方法：</span><span class="sxs-lookup"><span data-stu-id="53da0-161">Add the following code to the *ConfigureServices* method:</span></span>

    ```csharp
    services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
        .FromFile(modelName: "SentimentAnalysisModel", filePath:"MLModels/sentiment_model.zip", watchForChanges: true);
    ```

<span data-ttu-id="53da0-162">概括而言，此程式碼會在應用程式要求時自動初始化物件和服務，以供稍後使用，而不需要手動執行。</span><span class="sxs-lookup"><span data-stu-id="53da0-162">At a high level, this code initializes the objects and services automatically for later use when requested by the application instead of having to manually do it.</span></span>

<span data-ttu-id="53da0-163">機器學習模型不是靜態的。</span><span class="sxs-lookup"><span data-stu-id="53da0-163">Machine learning models are not static.</span></span> <span data-ttu-id="53da0-164">當新的定型資料變成可用時，就會重新定型並重新部署模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-164">As new training data becomes available, the model is retrained and redeployed.</span></span> <span data-ttu-id="53da0-165">在應用程式中取得最新版本模型的方法之一，就是重新部署整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="53da0-165">One way to get the latest version of the model into your application is to redeploy the entire application.</span></span> <span data-ttu-id="53da0-166">不過，這會造成應用程式停機。</span><span class="sxs-lookup"><span data-stu-id="53da0-166">However, this introduces application downtime.</span></span> <span data-ttu-id="53da0-167">`PredictionEnginePool`服務會提供一種機制，以重載已更新的模型，而不需要讓您的應用程式停止運作。</span><span class="sxs-lookup"><span data-stu-id="53da0-167">The `PredictionEnginePool` service provides a mechanism to reload an updated model without taking your application down.</span></span>

<span data-ttu-id="53da0-168">將 `watchForChanges` 參數設定為 `true` ，並 `PredictionEnginePool` 啟動，以 [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher) 接聽檔案系統變更通知，並在檔案變更時引發事件。</span><span class="sxs-lookup"><span data-stu-id="53da0-168">Set the `watchForChanges` parameter to `true`, and the `PredictionEnginePool` starts a [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher) that listens to the file system change notifications and raises events when there is a change to the file.</span></span> <span data-ttu-id="53da0-169">這會提示 `PredictionEnginePool` 自動重載模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-169">This prompts the `PredictionEnginePool` to automatically reload the model.</span></span>

<span data-ttu-id="53da0-170">模型是由參數識別， `modelName` 因此，每個應用程式可以在變更時重載一個以上的模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-170">The model is identified by the `modelName` parameter so that more than one model per application can be reloaded upon change.</span></span>

> [!TIP]
> <span data-ttu-id="53da0-171">或者，您可以在使用 `FromUri` 遠端儲存的模型時使用方法。</span><span class="sxs-lookup"><span data-stu-id="53da0-171">Alternatively, you can use the `FromUri` method when working with models stored remotely.</span></span> <span data-ttu-id="53da0-172">並不會監看檔案變更的事件，而是會 `FromUri` 輪詢遠端位置的變更。</span><span class="sxs-lookup"><span data-stu-id="53da0-172">Rather than watching for file changed events, `FromUri` polls the remote location for changes.</span></span> <span data-ttu-id="53da0-173">輪詢間隔預設為5分鐘。</span><span class="sxs-lookup"><span data-stu-id="53da0-173">The polling interval defaults to 5 minutes.</span></span> <span data-ttu-id="53da0-174">您可以根據應用程式的需求來增加或減少輪詢間隔。</span><span class="sxs-lookup"><span data-stu-id="53da0-174">You can increase or decrease the polling interval based on your application's requirements.</span></span> <span data-ttu-id="53da0-175">在下列程式碼範例中，會 `PredictionEnginePool` 每分鐘輪詢儲存在指定 URI 上的模型。</span><span class="sxs-lookup"><span data-stu-id="53da0-175">In the code sample below, the `PredictionEnginePool` polls the model stored at the specified URI every minute.</span></span>
>
>```csharp
>services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
>   .FromUri(
>       modelName: "SentimentAnalysisModel",
>       uri:"https://github.com/dotnet/samples/raw/master/machine-learning/models/sentimentanalysis/sentiment_model.zip",
>       period: TimeSpan.FromMinutes(1));
>```

## <a name="create-predict-controller"></a><span data-ttu-id="53da0-176">建立預測控制器</span><span class="sxs-lookup"><span data-stu-id="53da0-176">Create Predict controller</span></span>

<span data-ttu-id="53da0-177">若要處理傳入的 HTTP 要求，請建立一個控制器。</span><span class="sxs-lookup"><span data-stu-id="53da0-177">To process your incoming HTTP requests, create a controller.</span></span>

1. <span data-ttu-id="53da0-178">在 [方案總管] 中，以滑鼠右鍵按一下 *Controllers* 目錄，然後選取 [新增] > [控制器]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-178">In Solution Explorer, right-click the *Controllers* directory, and then select **Add > Controller**.</span></span>
1. <span data-ttu-id="53da0-179">在 [加入新項目]\*\*\*\* 對話方塊中，選取 [API 控制器 - 空白]\*\*\*\*，然後選取 [新增]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="53da0-179">In the **Add New Item** dialog box, select **API Controller Empty** and select **Add**.</span></span>
1. <span data-ttu-id="53da0-180">在提示中，將 [控制器名稱]\*\*\*\* 欄位變更為 *PredictController.cs*。</span><span class="sxs-lookup"><span data-stu-id="53da0-180">In the prompt change the **Controller Name** field to *PredictController.cs*.</span></span> <span data-ttu-id="53da0-181">接著，選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53da0-181">Then, select the Add button.</span></span> <span data-ttu-id="53da0-182">*PredictController.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="53da0-182">The *PredictController.cs* file opens in the code editor.</span></span> <span data-ttu-id="53da0-183">將下列 using 陳述式新增至 *PredictController.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="53da0-183">Add the following using statement to the top of *PredictController.cs*:</span></span>

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

    <span data-ttu-id="53da0-184">移除現有的類別定義，然後將下列程式碼新增至 *PredictController.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="53da0-184">Remove the existing class definition and add the following code to the *PredictController.cs* file:</span></span>

    ```csharp
    public class PredictController : ControllerBase
    {
        private readonly PredictionEnginePool<SentimentData, SentimentPrediction> _predictionEnginePool;

        public PredictController(PredictionEnginePool<SentimentData,SentimentPrediction> predictionEnginePool)
        {
            _predictionEnginePool = predictionEnginePool;
        }

        [HttpPost]
        public ActionResult<string> Post([FromBody] SentimentData input)
        {
            if(!ModelState.IsValid)
            {
                return BadRequest();
            }

            SentimentPrediction prediction = _predictionEnginePool.Predict(modelName: "SentimentAnalysisModel", example: input);

            string sentiment = Convert.ToBoolean(prediction.Prediction) ? "Positive" : "Negative";

            return Ok(sentiment);
        }
    }
    ```

<span data-ttu-id="53da0-185">此程式碼會透過將預測服務傳遞至控制器的建構函式 (透過相依性插入取得) 來指派 `PredictionEnginePool`。</span><span class="sxs-lookup"><span data-stu-id="53da0-185">This code assigns the `PredictionEnginePool` by passing it to the controller's constructor which you get via dependency injection.</span></span> <span data-ttu-id="53da0-186">然後， `Predict` 控制器的 `Post` 方法會使用在 `PredictionEnginePool` 類別中註冊的來進行預測 `SentimentAnalysisModel` `Startup` ，並在成功時將結果傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="53da0-186">Then, the `Predict` controller's `Post` method uses the `PredictionEnginePool` to make predictions using the `SentimentAnalysisModel` registered in the `Startup` class and returns the results back to the user if successful.</span></span>

## <a name="test-web-api-locally"></a><span data-ttu-id="53da0-187">在本機測試 Web API</span><span class="sxs-lookup"><span data-stu-id="53da0-187">Test web API locally</span></span>

<span data-ttu-id="53da0-188">一切都設定好後，就可以開始測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="53da0-188">Once everything is set up, it's time to test the application.</span></span>

1. <span data-ttu-id="53da0-189">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="53da0-189">Run the application.</span></span>
1. <span data-ttu-id="53da0-190">開啟 PowerShell 並輸入下列程式碼，其中 PORT 是您的應用程式所接聽的埠。</span><span class="sxs-lookup"><span data-stu-id="53da0-190">Open PowerShell and enter the following code where PORT is the port your application is listening on.</span></span>

    ```powershell
    Invoke-RestMethod "https://localhost:<PORT>/api/predict" -Method Post -Body (@{SentimentText="This was a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    <span data-ttu-id="53da0-191">如果成功，輸出看起來應該類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="53da0-191">If successful, the output should look similar to the text below:</span></span>

    ```powershell
    Negative
    ```

<span data-ttu-id="53da0-192">恭喜！</span><span class="sxs-lookup"><span data-stu-id="53da0-192">Congratulations!</span></span> <span data-ttu-id="53da0-193">您已成功提供您的模型，使用 ASP.NET Core Web API 在網際網路上進行預測。</span><span class="sxs-lookup"><span data-stu-id="53da0-193">You have successfully served your model to make predictions over the internet using an ASP.NET Core Web API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53da0-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53da0-194">Next Steps</span></span>

- [<span data-ttu-id="53da0-195">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="53da0-195">Deploy to Azure</span></span>](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure)

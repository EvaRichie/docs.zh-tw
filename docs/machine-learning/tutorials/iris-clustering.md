---
title: 教學課程：分類鳶尾花鮮花-k-表示群集
description: 了解如何在群集案例中使用 ML.NET
author: pkulikov
ms.date: 06/30/2020
ms.topic: tutorial
ms.custom: mvc, title-hack-0516
ms.openlocfilehash: 8ee8b177dc9cc89c4f54956b8c0a274b1d093ece
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2020
ms.locfileid: "86282081"
---
# <a name="tutorial-categorize-iris-flowers-using-k-means-clustering-with-mlnet"></a><span data-ttu-id="8b611-103">教學課程：使用 k 來分類鳶尾花的花卉-表示使用 ML.NET 的叢集</span><span class="sxs-lookup"><span data-stu-id="8b611-103">Tutorial: Categorize iris flowers using k-means clustering with ML.NET</span></span>

<span data-ttu-id="8b611-104">本教學課程說明如何使用 ML.NET 為[鳶尾花資料集](https://en.wikipedia.org/wiki/Iris_flower_data_set)建立一個[群集模型](../resources/tasks.md#clustering)。</span><span class="sxs-lookup"><span data-stu-id="8b611-104">This tutorial illustrates how to use ML.NET to build a [clustering model](../resources/tasks.md#clustering) for the [iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span></span>

<span data-ttu-id="8b611-105">在本教學課程中，您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="8b611-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="8b611-106">了解問題</span><span class="sxs-lookup"><span data-stu-id="8b611-106">Understand the problem</span></span>
> - <span data-ttu-id="8b611-107">選取適當的機器學習工作</span><span class="sxs-lookup"><span data-stu-id="8b611-107">Select the appropriate machine learning task</span></span>
> - <span data-ttu-id="8b611-108">準備資料</span><span class="sxs-lookup"><span data-stu-id="8b611-108">Prepare the data</span></span>
> - <span data-ttu-id="8b611-109">載入並轉換資料</span><span class="sxs-lookup"><span data-stu-id="8b611-109">Load and transform the data</span></span>
> - <span data-ttu-id="8b611-110">選擇學習演算法</span><span class="sxs-lookup"><span data-stu-id="8b611-110">Choose a learning algorithm</span></span>
> - <span data-ttu-id="8b611-111">將模型定型</span><span class="sxs-lookup"><span data-stu-id="8b611-111">Train the model</span></span>
> - <span data-ttu-id="8b611-112">使用模型來進行預測</span><span class="sxs-lookup"><span data-stu-id="8b611-112">Use the model for predictions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b611-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="8b611-113">Prerequisites</span></span>

- <span data-ttu-id="8b611-114">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)或更新版本，或是已安裝「.net Core 跨平臺開發」工作負載的 Visual Studio 2017 15.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8b611-114">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or later or Visual Studio 2017 version 15.6 or later with the ".NET Core cross-platform development" workload installed.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="8b611-115">了解問題</span><span class="sxs-lookup"><span data-stu-id="8b611-115">Understand the problem</span></span>

<span data-ttu-id="8b611-116">這個問題是關於將一組鳶尾花按照花卉特徵分成不同的群組。</span><span class="sxs-lookup"><span data-stu-id="8b611-116">This problem is about dividing the set of iris flowers in different groups based on the flower features.</span></span> <span data-ttu-id="8b611-117">這些特徵是萼片的長度和寬度以及花瓣的長度和寬度。</span><span class="sxs-lookup"><span data-stu-id="8b611-117">Those features are the length and width of a sepal and the length and width of a petal.</span></span> <span data-ttu-id="8b611-118">本教學課程中假設不知道每個花卉的類型。</span><span class="sxs-lookup"><span data-stu-id="8b611-118">For this tutorial, assume that the type of each flower is unknown.</span></span> <span data-ttu-id="8b611-119">您想要從特徵了解資料集的結構，還要預測資料執行個體如何符合此結構。</span><span class="sxs-lookup"><span data-stu-id="8b611-119">You want to learn the structure of a data set from the features and predict how a data instance fits this structure.</span></span>

## <a name="select-the-appropriate-machine-learning-task"></a><span data-ttu-id="8b611-120">選取適當的機器學習工作</span><span class="sxs-lookup"><span data-stu-id="8b611-120">Select the appropriate machine learning task</span></span>

<span data-ttu-id="8b611-121">因為您不知道每個花卉屬於哪個群組，所以您選擇[非監督式機器學習](../resources/glossary.md#unsupervised-machine-learning)工作。</span><span class="sxs-lookup"><span data-stu-id="8b611-121">As you don't know to which group each flower belongs to, you choose the [unsupervised machine learning](../resources/glossary.md#unsupervised-machine-learning) task.</span></span> <span data-ttu-id="8b611-122">若要按照類似元素歸於同一群組中的方式來分割群組中的資料集，請使用[群集](../resources/tasks.md#clustering)機器學習工作。</span><span class="sxs-lookup"><span data-stu-id="8b611-122">To divide a data set in groups in such a way that elements in the same group are more similar to each other than to those in other groups, use a [clustering](../resources/tasks.md#clustering) machine learning task.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="8b611-123">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="8b611-123">Create a console application</span></span>

1. <span data-ttu-id="8b611-124">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8b611-124">Open Visual Studio.</span></span> <span data-ttu-id="8b611-125">**File**  >  **New**  >  從功能表列選取 [檔案] [新增**專案**]。</span><span class="sxs-lookup"><span data-stu-id="8b611-125">Select **File** > **New** > **Project** from the menu bar.</span></span> <span data-ttu-id="8b611-126">在 [新增專案]\*\*\*\* 對話方塊中，選取 [Visual C#]\*\*\*\* 節點，然後選取 [.NET Core]\*\*\*\* 節點。</span><span class="sxs-lookup"><span data-stu-id="8b611-126">In the **New Project** dialog, select the **Visual C#** node followed by the **.NET Core** node.</span></span> <span data-ttu-id="8b611-127">然後選取 [主控台應用程式 (.NET Core)]\*\*\*\* 專案範本。</span><span class="sxs-lookup"><span data-stu-id="8b611-127">Then select the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="8b611-128">在 [名稱]\*\*\*\* 文字方塊中，鍵入 "IrisFlowerClustering"，然後選取 [確定]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b611-128">In the **Name** text box, type "IrisFlowerClustering" and then select the **OK** button.</span></span>

1. <span data-ttu-id="8b611-129">在您的專案中建立名為*Data*的目錄，以儲存資料集和模型檔案：</span><span class="sxs-lookup"><span data-stu-id="8b611-129">Create a directory named *Data* in your project to store the data set and model files:</span></span>

    <span data-ttu-id="8b611-130">在 [方案總管]\*\*\*\* 中，以滑鼠右鍵按一下專案，然後選取 [新增]\*\*\*\* > [新增資料夾]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8b611-130">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="8b611-131">輸入 "Data"，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="8b611-131">Type "Data" and hit Enter.</span></span>

1. <span data-ttu-id="8b611-132">安裝**Microsoft.ML** NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="8b611-132">Install the **Microsoft.ML** NuGet package:</span></span>

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    <span data-ttu-id="8b611-133">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="8b611-133">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="8b611-134">選擇 [nuget.org] 作為 [套件來源]，選取 [**流覽**] 索引標籤，搜尋**Microsoft.ML** ，然後選取 [**安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b611-134">Choose "nuget.org" as the Package source, select the **Browse** tab, search for **Microsoft.ML** and select the **Install** button.</span></span> <span data-ttu-id="8b611-135">在 [預覽變更]\*\*\*\* 對話方塊上，選取 [確定]\*\*\*\* 按鈕，然後在 [授權接受]\*\*\*\* 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8b611-135">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span>

## <a name="prepare-the-data"></a><span data-ttu-id="8b611-136">準備資料</span><span class="sxs-lookup"><span data-stu-id="8b611-136">Prepare the data</span></span>

1. <span data-ttu-id="8b611-137">下載 [iris.data](https://github.com/dotnet/machinelearning/blob/master/test/data/iris.data) 資料集，並將它儲存到上一個步驟中建立的 *Data* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8b611-137">Download the [iris.data](https://github.com/dotnet/machinelearning/blob/master/test/data/iris.data) data set and save it to the *Data* folder you've created at the previous step.</span></span> <span data-ttu-id="8b611-138">如需有關鳶尾花資料集的詳細資訊，請參閱[鳶尾花資料集](https://en.wikipedia.org/wiki/Iris_flower_data_set)維基百科頁面和[鳶尾花資料集](http://archive.ics.uci.edu/ml/datasets/Iris)頁面 (也就是資料集的來源)。</span><span class="sxs-lookup"><span data-stu-id="8b611-138">For more information about the iris data set, see the [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set) Wikipedia page and the [Iris Data Set](http://archive.ics.uci.edu/ml/datasets/Iris) page, which is the source of the data set.</span></span>

1. <span data-ttu-id="8b611-139">以滑鼠右鍵按一下 [方案總管]\*\*\*\* 中的 *iris.data* 檔案，然後選取 [內容]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8b611-139">In **Solution Explorer**, right-click the *iris.data* file and select **Properties**.</span></span> <span data-ttu-id="8b611-140">在 [ **Advanced**] 底下，將 [**複製到輸出目錄**] 的值變更為 [**更新時複製**]。</span><span class="sxs-lookup"><span data-stu-id="8b611-140">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="8b611-141">*Iris.data* 檔案包含五個資料行，分別表示：</span><span class="sxs-lookup"><span data-stu-id="8b611-141">The *iris.data* file contains five columns that represent:</span></span>

- <span data-ttu-id="8b611-142">萼片長度（以釐米為單位）</span><span class="sxs-lookup"><span data-stu-id="8b611-142">sepal length in centimeters</span></span>
- <span data-ttu-id="8b611-143">萼片寬度（以釐米為單位）</span><span class="sxs-lookup"><span data-stu-id="8b611-143">sepal width in centimeters</span></span>
- <span data-ttu-id="8b611-144">花瓣長度（以釐米為單位）</span><span class="sxs-lookup"><span data-stu-id="8b611-144">petal length in centimeters</span></span>
- <span data-ttu-id="8b611-145">花瓣寬度（以釐米為單位）</span><span class="sxs-lookup"><span data-stu-id="8b611-145">petal width in centimeters</span></span>
- <span data-ttu-id="8b611-146">鳶尾花的類型</span><span class="sxs-lookup"><span data-stu-id="8b611-146">type of iris flower</span></span>

<span data-ttu-id="8b611-147">為了示範群集方法，本教學課程會略過最後一個資料行。</span><span class="sxs-lookup"><span data-stu-id="8b611-147">For the sake of the clustering example, this tutorial ignores the last column.</span></span>

## <a name="create-data-classes"></a><span data-ttu-id="8b611-148">建立資料類別</span><span class="sxs-lookup"><span data-stu-id="8b611-148">Create data classes</span></span>

<span data-ttu-id="8b611-149">為輸入資料和預測建立類別：</span><span class="sxs-lookup"><span data-stu-id="8b611-149">Create classes for the input data and the predictions:</span></span>

1. <span data-ttu-id="8b611-150">在 [方案總管]\*\*\*\* 中，以滑鼠右鍵按一下專案，然後選取 [新增]\*\*\*\* > [新項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8b611-150">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="8b611-151">在 [新增項目]\*\*\*\* 對話方塊中，選取 [類別]\*\*\*\*，然後將 [名稱]\*\*\*\* 欄位變更為 *IrisData.cs*。</span><span class="sxs-lookup"><span data-stu-id="8b611-151">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *IrisData.cs*.</span></span> <span data-ttu-id="8b611-152">接著，選取 [新增]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b611-152">Then, select the **Add** button.</span></span>
1. <span data-ttu-id="8b611-153">將下列的 `using` 指示詞加入新檔案：</span><span class="sxs-lookup"><span data-stu-id="8b611-153">Add the following `using` directive to the new file:</span></span>

   [!code-csharp[Add necessary usings](./snippets/iris-clustering/csharp/IrisData.cs#Usings)]

<span data-ttu-id="8b611-154">移除現有的類別定義，然後將下列程式碼 (定義 `IrisData` 和 `ClusterPrediction` 這兩個類別) 新增至 *IrisData.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="8b611-154">Remove the existing class definition and add the following code, which defines the classes `IrisData` and `ClusterPrediction`, to the *IrisData.cs* file:</span></span>

[!code-csharp[Define data classes](./snippets/iris-clustering/csharp/IrisData.cs#ClassDefinitions)]

<span data-ttu-id="8b611-155">`IrisData` 是輸入資料類別，它含有資料集中每個特徵的定義。</span><span class="sxs-lookup"><span data-stu-id="8b611-155">`IrisData` is the input data class and has definitions for each feature from the data set.</span></span> <span data-ttu-id="8b611-156">請使用 [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute) 屬性來指定資料集檔案中來源資料行的索引。</span><span class="sxs-lookup"><span data-stu-id="8b611-156">Use the [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute) attribute to specify the indices of the source columns in the data set file.</span></span>

<span data-ttu-id="8b611-157">`ClusterPrediction` 類別代表套用至 `IrisData` 執行個體的群集模型結果。</span><span class="sxs-lookup"><span data-stu-id="8b611-157">The `ClusterPrediction` class represents the output of the clustering model applied to an `IrisData` instance.</span></span> <span data-ttu-id="8b611-158">使用 [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute) 屬性分別將 `PredictedClusterId` 和 `Distances` 欄位繫結至 **PredictedLabel** 和 **Score** 資料行。</span><span class="sxs-lookup"><span data-stu-id="8b611-158">Use the [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute) attribute to bind the `PredictedClusterId` and `Distances` fields to the **PredictedLabel** and **Score** columns respectively.</span></span> <span data-ttu-id="8b611-159">群集這些資料行的工作具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="8b611-159">In case of the clustering task those columns have the following meaning:</span></span>

- <span data-ttu-id="8b611-160">**PredictedLabel** 資料行包含預測群集的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b611-160">**PredictedLabel** column contains the ID of the predicted cluster.</span></span>
- <span data-ttu-id="8b611-161">**Score** 資料行包含平方歐幾里得距離到群集矩心的陣列。</span><span class="sxs-lookup"><span data-stu-id="8b611-161">**Score** column contains an array with squared Euclidean distances to the cluster centroids.</span></span> <span data-ttu-id="8b611-162">陣列長度等於群集數目。</span><span class="sxs-lookup"><span data-stu-id="8b611-162">The array length is equal to the number of clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="8b611-163">使用 `float` 型別表示輸入和預測資料類別中的浮點值。</span><span class="sxs-lookup"><span data-stu-id="8b611-163">Use the `float` type to represent floating-point values in the input and prediction data classes.</span></span>

## <a name="define-data-and-model-paths"></a><span data-ttu-id="8b611-164">定義資料和模型路徑</span><span class="sxs-lookup"><span data-stu-id="8b611-164">Define data and model paths</span></span>

<span data-ttu-id="8b611-165">返回 *Program.cs* 檔案並新增兩個欄位，保存資料集檔案的路徑以及儲存模型之檔案的路徑：</span><span class="sxs-lookup"><span data-stu-id="8b611-165">Go back to the *Program.cs* file and add two fields to hold the paths to the data set file and to the file to save the model:</span></span>

- <span data-ttu-id="8b611-166">`_dataPath` 會針對具有用來定型模型之資料集的檔案，包含檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="8b611-166">`_dataPath` contains the path to the file with the data set used to train the model.</span></span>
- <span data-ttu-id="8b611-167">`_modelPath` 會針對儲存定型模型的檔案，包含檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="8b611-167">`_modelPath` contains the path to the file where the trained model is stored.</span></span>

<span data-ttu-id="8b611-168">將下列程式碼加入 `Main` 方法的緊鄰上方，以指定這些路徑：</span><span class="sxs-lookup"><span data-stu-id="8b611-168">Add the following code right above the `Main` method to specify those paths:</span></span>

[!code-csharp[Initialize paths](./snippets/iris-clustering/csharp/Program.cs#Paths)]

<span data-ttu-id="8b611-169">若要將上述的程式碼進行編譯，請在 *Program.cs* 檔案頂端加入下列 `using` 指示詞：</span><span class="sxs-lookup"><span data-stu-id="8b611-169">To make the preceding code compile, add the following `using` directives at the top of the *Program.cs* file:</span></span>

[!code-csharp[Add usings for paths](./snippets/iris-clustering/csharp/Program.cs#UsingsForPaths)]

## <a name="create-ml-context"></a><span data-ttu-id="8b611-170">建立 ML 內容</span><span class="sxs-lookup"><span data-stu-id="8b611-170">Create ML context</span></span>

<span data-ttu-id="8b611-171">在 *Program.cs* 檔案頂端加入下列額外的 `using` 指示詞：</span><span class="sxs-lookup"><span data-stu-id="8b611-171">Add the following additional `using` directives to the top of the *Program.cs* file:</span></span>

[!code-csharp[Add Microsoft.ML usings](./snippets/iris-clustering/csharp/Program.cs#MLUsings)]

<span data-ttu-id="8b611-172">在 `Console.WriteLine("Hello World!");` 方法中，以下列程式碼取代 `Main` 行：</span><span class="sxs-lookup"><span data-stu-id="8b611-172">In the `Main` method, replace the `Console.WriteLine("Hello World!");` line with the following code:</span></span>

[!code-csharp[Create ML context](./snippets/iris-clustering/csharp/Program.cs#CreateContext)]

<span data-ttu-id="8b611-173"><xref:Microsoft.ML.MLContext?displayProperty=nameWithType> 類別表示機器學習環境，並為資料載入、模型定型、預測和其他工作提供記錄機制和進入點。</span><span class="sxs-lookup"><span data-stu-id="8b611-173">The <xref:Microsoft.ML.MLContext?displayProperty=nameWithType> class represents the machine learning environment and provides mechanisms for logging and entry points for data loading, model training, prediction, and other tasks.</span></span> <span data-ttu-id="8b611-174">這在概念上類似於在 Entity Framework 中使用的 `DbContext`。</span><span class="sxs-lookup"><span data-stu-id="8b611-174">This is comparable conceptually to using `DbContext` in Entity Framework.</span></span>

## <a name="set-up-data-loading"></a><span data-ttu-id="8b611-175">設定資料載入</span><span class="sxs-lookup"><span data-stu-id="8b611-175">Set up data loading</span></span>

<span data-ttu-id="8b611-176">將下列程式碼新增至 `Main` 方法，以設定載入資料的方式：</span><span class="sxs-lookup"><span data-stu-id="8b611-176">Add the following code to the `Main` method to set up the way to load data:</span></span>

[!code-csharp[Create text loader](./snippets/iris-clustering/csharp/Program.cs#CreateDataView)]

<span data-ttu-id="8b611-177">泛型[ `MLContext.Data.LoadFromTextFile` 擴充方法](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)會從提供的型別推斷資料集架構 `IrisData` ，並傳回 <xref:Microsoft.ML.IDataView> 可當做轉換器輸入使用的。</span><span class="sxs-lookup"><span data-stu-id="8b611-177">The generic [`MLContext.Data.LoadFromTextFile` extension method](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) infers the data set schema from the provided `IrisData` type and returns <xref:Microsoft.ML.IDataView> which can be used as input for transformers.</span></span>

## <a name="create-a-learning-pipeline"></a><span data-ttu-id="8b611-178">建立學習管線</span><span class="sxs-lookup"><span data-stu-id="8b611-178">Create a learning pipeline</span></span>

<span data-ttu-id="8b611-179">在本教學課程中，叢集工作的學習管線包含下列兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="8b611-179">For this tutorial, the learning pipeline of the clustering task comprises two following steps:</span></span>

- <span data-ttu-id="8b611-180">將載入的資料行串連成一個 [特徵]\*\*\*\* 資料行，以供叢集定型器使用；</span><span class="sxs-lookup"><span data-stu-id="8b611-180">concatenate loaded columns into one **Features** column, which is used by a clustering trainer;</span></span>
- <span data-ttu-id="8b611-181">使用 <xref:Microsoft.ML.Trainers.KMeansTrainer> 定型器透過 k-means++ 叢集演算法將模型定型。</span><span class="sxs-lookup"><span data-stu-id="8b611-181">use a <xref:Microsoft.ML.Trainers.KMeansTrainer> trainer to train the model using the k-means++ clustering algorithm.</span></span>

<span data-ttu-id="8b611-182">將下列程式碼加入 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="8b611-182">Add the following code to the `Main` method:</span></span>

[!code-csharp[Create pipeline](./snippets/iris-clustering/csharp/Program.cs#CreatePipeline)]

<span data-ttu-id="8b611-183">此程式碼指定應該將資料集分成三個叢集。</span><span class="sxs-lookup"><span data-stu-id="8b611-183">The code specifies that the data set should be split in three clusters.</span></span>

## <a name="train-the-model"></a><span data-ttu-id="8b611-184">將模型定型</span><span class="sxs-lookup"><span data-stu-id="8b611-184">Train the model</span></span>

<span data-ttu-id="8b611-185">上述小節中加入的步驟已準備好訓練的管道，不過，還沒有開始執行。</span><span class="sxs-lookup"><span data-stu-id="8b611-185">The steps added in the preceding sections prepared the pipeline for training, however, none have been executed.</span></span> <span data-ttu-id="8b611-186">將下列程式碼行新增至 `Main` 方法，以執行資料載入和模型定型：</span><span class="sxs-lookup"><span data-stu-id="8b611-186">Add the following line to the `Main` method to perform data loading and model training:</span></span>

[!code-csharp[Train the model](./snippets/iris-clustering/csharp/Program.cs#TrainModel)]

### <a name="save-the-model"></a><span data-ttu-id="8b611-187">儲存模型</span><span class="sxs-lookup"><span data-stu-id="8b611-187">Save the model</span></span>

<span data-ttu-id="8b611-188">此時，您已有一個可整合至任何現有或新 .NET 應用程式的模型。</span><span class="sxs-lookup"><span data-stu-id="8b611-188">At this point, you have a model that can be integrated into any of your existing or new .NET applications.</span></span> <span data-ttu-id="8b611-189">若要將您的模型儲存成 .zip 檔案，請將下列程式碼新增至 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="8b611-189">To save your model to a .zip file, add the following code to the `Main` method:</span></span>

[!code-csharp[Save the model](./snippets/iris-clustering/csharp/Program.cs#SaveModel)]

## <a name="use-the-model-for-predictions"></a><span data-ttu-id="8b611-190">使用模型來進行預測</span><span class="sxs-lookup"><span data-stu-id="8b611-190">Use the model for predictions</span></span>

<span data-ttu-id="8b611-191">為了進行預測，請使用 <xref:Microsoft.ML.PredictionEngine%602> 類別，其帶領輸入類型的執行個體通過轉換程式管線，並產生輸出類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b611-191">To make predictions, use the <xref:Microsoft.ML.PredictionEngine%602> class that takes instances of the input type through the transformer pipeline and produces instances of the output type.</span></span> <span data-ttu-id="8b611-192">將下列程式碼行新增至 `Main` 方法，以建立該類別的執行個體：</span><span class="sxs-lookup"><span data-stu-id="8b611-192">Add the following line to the `Main` method to create an instance of that class:</span></span>

[!code-csharp[Create predictor](./snippets/iris-clustering/csharp/Program.cs#Predictor)]

<span data-ttu-id="8b611-193">[PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)是一個方便的 API，可讓您在單一資料實例上執行預測。</span><span class="sxs-lookup"><span data-stu-id="8b611-193">The [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) is a convenience API, which allows you to perform a prediction on a single instance of data.</span></span> <span data-ttu-id="8b611-194">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)不是安全線程。</span><span class="sxs-lookup"><span data-stu-id="8b611-194">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) is not thread-safe.</span></span> <span data-ttu-id="8b611-195">可接受在單一執行緒或原型環境中使用。</span><span class="sxs-lookup"><span data-stu-id="8b611-195">It's acceptable to use in single-threaded or prototype environments.</span></span> <span data-ttu-id="8b611-196">為了改善生產環境中的效能和執行緒安全，請使用 `PredictionEnginePool` 服務，這會建立物件的， [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) 以便在 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 整個應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="8b611-196">For improved performance and thread safety in production environments, use the `PredictionEnginePool` service, which creates an [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) of [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) objects for use throughout your application.</span></span> <span data-ttu-id="8b611-197">請參閱本指南，以瞭解如何[ `PredictionEnginePool` 在 ASP.NET CORE Web API 中使用](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application)。</span><span class="sxs-lookup"><span data-stu-id="8b611-197">See this guide on how to [use `PredictionEnginePool` in an ASP.NET Core Web API](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application).</span></span>

> [!NOTE]
> <span data-ttu-id="8b611-198">`PredictionEnginePool` 服務延伸模組目前處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="8b611-198">`PredictionEnginePool` service extension is currently in preview.</span></span>

<span data-ttu-id="8b611-199">建立 `TestIrisData` 類型以容納測試資料執行個體：</span><span class="sxs-lookup"><span data-stu-id="8b611-199">Create the `TestIrisData` class to house test data instances:</span></span>

1. <span data-ttu-id="8b611-200">在 [方案總管]\*\*\*\* 中，以滑鼠右鍵按一下專案，然後選取 [新增]\*\*\*\* > [新項目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8b611-200">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="8b611-201">在 [新增項目]\*\*\*\* 對話方塊中，選取 [類別]\*\*\*\*，然後將 [名稱]\*\*\*\* 欄位變更為 *TestIrisData.cs*。</span><span class="sxs-lookup"><span data-stu-id="8b611-201">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *TestIrisData.cs*.</span></span> <span data-ttu-id="8b611-202">接著，選取 [新增]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b611-202">Then, select the **Add** button.</span></span>
1. <span data-ttu-id="8b611-203">將類別修改成靜態，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="8b611-203">Modify the class to be static like in the following example:</span></span>

   [!code-csharp[Make class static](./snippets/iris-clustering/csharp/TestIrisData.cs#Static)]

<span data-ttu-id="8b611-204">本教學課程介紹此類別內一個鳶尾花資料執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b611-204">This tutorial introduces one iris data instance within this class.</span></span> <span data-ttu-id="8b611-205">您可以新增其他案例來對此模型進行實驗。</span><span class="sxs-lookup"><span data-stu-id="8b611-205">You can add other scenarios to experiment with the model.</span></span> <span data-ttu-id="8b611-206">將下列程式碼新增至 `TestIrisData` 類別：</span><span class="sxs-lookup"><span data-stu-id="8b611-206">Add the following code into the `TestIrisData` class:</span></span>

[!code-csharp[Test data](./snippets/iris-clustering/csharp/TestIrisData.cs#TestData)]

<span data-ttu-id="8b611-207">若要找出指定項目所屬的群集，請返回 *Program.cs* 檔案，然後將下列程式碼加入至 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="8b611-207">To find out the cluster to which the specified item belongs to, go back to the *Program.cs* file and add the following code into the `Main` method:</span></span>

[!code-csharp[Predict and output results](./snippets/iris-clustering/csharp/Program.cs#PredictionExample)]

<span data-ttu-id="8b611-208">執行程式，以查看哪些群集包含指定的資料執行個體以及從該執行個體到群集矩心的平方距離。</span><span class="sxs-lookup"><span data-stu-id="8b611-208">Run the program to see which cluster contains the specified data instance and squared distances from that instance to the cluster centroids.</span></span> <span data-ttu-id="8b611-209">您的結果應該與以下類似：</span><span class="sxs-lookup"><span data-stu-id="8b611-209">Your results should be similar to the following:</span></span>

```text
Cluster: 2
Distances: 11.69127 0.02159119 25.59896
```

<span data-ttu-id="8b611-210">恭喜！</span><span class="sxs-lookup"><span data-stu-id="8b611-210">Congratulations!</span></span> <span data-ttu-id="8b611-211">您現在已成功建置用來群集鳶尾花並進行預測的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="8b611-211">You've now successfully built a machine learning model for iris clustering and used it to make predictions.</span></span> <span data-ttu-id="8b611-212">您可以在 [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/IrisFlowerClustering) GitHub 存放庫中找到本教學課程的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="8b611-212">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/IrisFlowerClustering) GitHub repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b611-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b611-213">Next steps</span></span>

<span data-ttu-id="8b611-214">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="8b611-214">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="8b611-215">了解問題</span><span class="sxs-lookup"><span data-stu-id="8b611-215">Understand the problem</span></span>
> - <span data-ttu-id="8b611-216">選取適當的機器學習工作</span><span class="sxs-lookup"><span data-stu-id="8b611-216">Select the appropriate machine learning task</span></span>
> - <span data-ttu-id="8b611-217">準備資料</span><span class="sxs-lookup"><span data-stu-id="8b611-217">Prepare the data</span></span>
> - <span data-ttu-id="8b611-218">載入並轉換資料</span><span class="sxs-lookup"><span data-stu-id="8b611-218">Load and transform the data</span></span>
> - <span data-ttu-id="8b611-219">選擇學習演算法</span><span class="sxs-lookup"><span data-stu-id="8b611-219">Choose a learning algorithm</span></span>
> - <span data-ttu-id="8b611-220">將模型定型</span><span class="sxs-lookup"><span data-stu-id="8b611-220">Train the model</span></span>
> - <span data-ttu-id="8b611-221">使用模型來進行預測</span><span class="sxs-lookup"><span data-stu-id="8b611-221">Use the model for predictions</span></span>

<span data-ttu-id="8b611-222">請查看我們的 GitHub 存放庫來繼續學習及尋找更多範例。</span><span class="sxs-lookup"><span data-stu-id="8b611-222">Check out our GitHub repository to continue learning and find more samples.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8b611-223">dotnet/machinelearning GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="8b611-223">dotnet/machinelearning GitHub repository</span></span>](https://github.com/dotnet/machinelearning/)

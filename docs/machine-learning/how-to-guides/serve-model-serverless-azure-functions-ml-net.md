---
title: 將模型部署到 Azure Functions
description: 使用 Azure Functions 在網際網路上提供 ML.NET 情感分析機器學習模型以進行預測
ms.date: 02/21/2020
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 74a7a5b941596ba9fffc62ef87a01763937d88c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2020
ms.locfileid: "91608773"
---
# <a name="deploy-a-model-to-azure-functions"></a>將模型部署到 Azure Functions

了解如何部署預先定型的 ML.NET 機器學習模型，以使用 Azure Functions 無伺服器環境透過 HTTP 進行預測。

> [!NOTE]
> 此範例會執行服務的預覽版本 `PredictionEnginePool` 。

## <a name="prerequisites"></a>Prerequisites

- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 或更新版本，或已安裝「.net Core 跨平臺開發」和「Azure 開發」工作負載的 Visual Studio 2017 15.6 版或更新版本。
- [Azure Functions 工具](/azure/azure-functions/functions-develop-vs#check-your-tools-version)
- PowerShell
- 預先定型的模型。 使用 [ML.NET 情感分析教學課程](../tutorials/sentiment-analysis.md)來建置您自己的模型，或是下載這個[預先定型的情感分析機器學習模型](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)

## <a name="azure-functions-sample-overview"></a>Azure Functions 範例總覽

此範例是 **c # HTTP 觸發程式 Azure Functions 應用程式** ，它會使用預先定型二元分類模型，將文字的情感分類為正面或負面。 Azure Functions 提供簡單的方式，在雲端中的受控無伺服器環境上大規模執行一小段程式碼。 您可以在 GitHub 上的 [dotnet/machinelearning 範例](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction) 存放庫中找到此範例的程式碼。

## <a name="create-azure-functions-project"></a>建立 Azure Functions 專案

1. 開啟 Visual Studio 2017。 **File**  >  **New**  >  從功能表列選取 [檔案新 **專案**]。 在 [新增專案] 對話方塊中，選取 [Visual C#] 節點，然後選取 [雲端] 節點。 然後選取 [Azure Functions] 專案範本。 在 [名稱] 文字方塊中，輸入 "SentimentAnalysisFunctionsApp"，然後選取 [確定] 按鈕。
1. 在 [新增專案] 對話方塊中，開啟專案選項上方的下拉式清單，然後選取 [Azure Functions v2 (.NET Core)]。 然後，選取 [Http 觸發程序] 專案，然後選取 [確定] 按鈕。
1. 在您的專案中建立名為 *MLModels* 的目錄，以儲存您的模型：

    在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [新增] > [新增資料夾]。 輸入 "MLModels"，然後按 Enter。

1. 安裝 **Microsoft.ML NuGet 套件** 版本 **1.3.1**：

    在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。 選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 **Microsoft.ML**、從清單中選取該套件，然後選取 [安裝] 按鈕。 在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。

1. 安裝 **Microsoft.Azure.Functions.Extensions NuGet 套件**：

    在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。 選擇 "nuget.org" 作為 [套件來源]、選取 [瀏覽] 索引標籤、搜尋 **Microsoft.Azure.Functions.Extensions**、從清單中選取該套件，然後選取 [安裝] 按鈕。 在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。

1. 安裝 **Microsoft.Extensions.ML NuGet 套件** 版本 **0.15.1**：

    在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。 選擇 "nuget.org" 作為 [套件來源]、選取 [瀏覽] 索引標籤、搜尋 **Microsoft.Extensions.ML**、從清單中選取該套件，然後選取 [安裝] 按鈕。 在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。

1. 安裝 **1.0.31** 的函式 **NuGet 套件** 版本：

    在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。 選擇 "nuget.org" 作為 [套件來源]，選取 [已安裝] 索引標籤，搜尋 [1.0.31 **]，在** 清單中選取該套件，從 [版本] 下拉式清單選取 [ **1.0.31** ]，然後選取 [**更新**] 按鈕。 在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。

## <a name="add-pre-trained-model-to-project"></a>將預先定型的模型新增到專案

1. 將預先建置的模型複製到 *MLModels* 目錄。
1. 在 [方案總管] 中，以滑鼠右鍵按一下您預先建置的模型檔案，並選取 [內容]。 在 [ **Advanced**] 底下，將 [ **複製到輸出目錄** ] 的值變更為 [ **更新時複製**]。

## <a name="create-azure-function-to-analyze-sentiment"></a>建立 Azure Function 來分析情感

建立用來預測情緒的類別。 將新類別新增至專案：

1. 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [新增] > [新項目]。

1. 在 [新增項目] 對話方塊中，選取 [Azure Function]，然後將 [名稱] 欄位變更為 *AnalyzeSentiment.cs*。 接著，選取 [新增] 按鈕。

1. 在 [新增 Azure 函式] 對話方塊中，選取 [Http 觸發程序]。 然後，選取 [確定] 按鈕。

    *AnalyzeSentiment.cs* 檔案隨即在程式碼編輯器中開啟。 將下列 `using` 陳述式新增到 *AnalyzeSentiment.cs* 的頂端：

    [!code-csharp [AnalyzeUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L1-L11)]

    根據預設，`AnalyzeSentiment` 類別為 `static`。 請務必從類別定義移除 `static` 關鍵字。

    ```csharp
    public class AnalyzeSentiment
    {

    }
    ```

## <a name="create-data-models"></a>建立資料模型

您必須為輸入資料和預測建立一些類別。 將新類別新增至專案：

1. 在專案中建立名為 *DataModels* 的目錄以儲存資料模型：在方案總管中，以滑鼠右鍵按一下您的專案，然後選取 [ **加入 > 新資料夾**]。 輸入 "DataModels"，然後按 Enter。
2. 在方案總管中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [ **新增 > 新專案**]。
3. 在 [新增項目] 對話方塊中，選取 [類別]，然後將 [名稱] 欄位變更為 *SentimentData.cs*。 接著，選取 [新增] 按鈕。

    *SentimentData.cs* 檔案隨即在程式碼編輯器中開啟。 將下列 using 陳述式新增至 *SentimentData.cs* 頂端：

    [!code-csharp [SentimentDataUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L1)]

    移除現有的類別定義，然後將下列程式碼新增至 *SentimentData.cs* 檔案：

    [!code-csharp [SentimentData](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L5-L13)]

4. 在方案總管中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [ **新增 > 新專案**]。
5. 在 [加入新項目] 對話方塊中，選取 [類別]，然後將 [名稱] 欄位變更為 *SentimentPrediction.cs*。 接著，選取 [新增] 按鈕。 *SentimentPrediction.cs* 檔案隨即在程式碼編輯器中開啟。 將下列 using 陳述式新增至 *SentimentPrediction.cs* 頂端：

    [!code-csharp [SentimentPredictionUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L1)]

    移除現有的類別定義，然後將下列程式碼新增至 *SentimentPrediction.cs* 檔案：

    [!code-csharp [SentimentPrediction](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L5-L14)]

    `SentimentPrediction` 會從 `SentimentData` 繼承，後者會在 `SentimentText` 屬性中提供原始資料的存取，以及由模型產生的輸出。

## <a name="register-predictionenginepool-service"></a>登錄 PredictionEnginePool 服務

若要進行單一預測，您必須建立 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 。 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 不是安全線程。 此外，您必須在應用程式內需要的任何地方建立其實例。 當您的應用程式成長時，此程式可能會變得難以管理。 為了改善效能和執行緒安全性，請使用相依性插入和服務的組合 `PredictionEnginePool` ，以建立可 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 在整個應用程式中使用的物件。

如果您想要深入瞭解相依性 [插入](https://en.wikipedia.org/wiki/Dependency_injection)，下列連結會提供詳細資訊。

1. 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [新增] > [新項目]。
1. 在 [新增項目] 對話方塊中，選取 [類別]，然後將 [名稱] 欄位變更為 *Startup.cs*。 接著，選取 [新增] 按鈕。
1. 將下列 using 語句新增至 *Startup.cs* 頂端：

    [!code-csharp [StartupUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L1-L6)]

1. 移除 using 語句下方的現有程式碼，並加入下列程式碼：

    ```csharp
    [assembly: FunctionsStartup(typeof(Startup))]
    namespace SentimentAnalysisFunctionsApp
    {
        public class Startup : FunctionsStartup
        {

        }
    }
    ```

1. 定義變數以儲存應用程式執行所在的環境，以及該模型位於類別內的檔案路徑 `Startup`

    [!code-csharp [DefineStartupVars](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L13-L14)]

1. 接著，建立一個可設定和變數值的函式 `_environment` `_modelPath` 。 當應用程式在本機執行時，預設環境為 *開發* 環境。

    [!code-csharp [StartupCtor](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L16-L29)]

1. 然後，新增名為的新方法， `Configure` `PredictionEnginePool` 在此函式下方註冊服務。

    [!code-csharp [ConfigureServices](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L31-L35)]

概括而言，此程式碼會在應用程式要求時自動初始化物件和服務，以供稍後使用，而不需要手動執行。

機器學習模型不是靜態的。 當新的定型資料變成可用時，就會重新定型並重新部署模型。 在應用程式中取得最新版本模型的方法之一，就是重新部署整個應用程式。 不過，這會造成應用程式停機。 `PredictionEnginePool`服務會提供一種機制，以重載已更新的模型，而不需要讓您的應用程式停止運作。

將 `watchForChanges` 參數設定為 `true` ，並 `PredictionEnginePool` 啟動，以 [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher) 接聽檔案系統變更通知，並在檔案變更時引發事件。 這會提示 `PredictionEnginePool` 自動重載模型。

模型是由參數識別， `modelName` 因此，每個應用程式可以在變更時重載一個以上的模型。

> [!TIP]
> 或者，您可以在使用 `FromUri` 遠端儲存的模型時使用方法。 並不會監看檔案變更的事件，而是會 `FromUri` 輪詢遠端位置的變更。 輪詢間隔預設為5分鐘。 您可以根據應用程式的需求來增加或減少輪詢間隔。 在下列程式碼範例中，會 `PredictionEnginePool` 每分鐘輪詢儲存在指定 URI 上的模型。
>
>```csharp
>builder.Services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
>   .FromUri(
>       modelName: "SentimentAnalysisModel",
>       uri:"https://github.com/dotnet/samples/raw/master/machine-learning/models/sentimentanalysis/sentiment_model.zip",
>       period: TimeSpan.FromMinutes(1));
>```

## <a name="load-the-model-into-the-function"></a>將模型載入函式

將下列程式碼插入 *AnalyzeSentiment* 類別：

[!code-csharp [AnalyzeCtor](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L18-L24)]

此程式碼會透過將 `PredictionEnginePool` 傳遞到您透過相依性插入所取得的函式建構函式來指派它。

## <a name="use-the-model-to-make-predictions"></a>使用模型進行預測

使用下列程式碼取代 *AnalyzeSentiment* 類別中 *Run* 方法的現有實作：

[!code-csharp [AnalyzeRunMethod](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L26-L45)]

`Run` 方法執行時，來自 HTTP 請求的傳入資料會還原序列化，並用來作為 `PredictionEnginePool` 的輸入。 `Predict`然後呼叫方法，使用在 `SentimentAnalysisModel` 類別中註冊的來進行預測 `Startup` ，並在成功時將結果傳回給使用者。

## <a name="test-locally"></a>本機測試

一切都設定好後，就可以開始測試應用程式：

1. 執行應用程式
1. 開啟 Powershell 並在提示字元中輸入下列程式碼，其中 PORT 是正在執行您應用程式的連接埠。 一般來說，連接埠是 7071。

    ```powershell
    Invoke-RestMethod "http://localhost:<PORT>/api/AnalyzeSentiment" -Method Post -Body (@{SentimentText="This is a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    如果成功，輸出看起來應該類似下列文字：

    ```powershell
    Negative
    ```

恭喜！ 您已成功提供您的模型，以使用 Azure Function 在網際網路上進行預測。

## <a name="next-steps"></a>後續步驟

- [部署至 Azure](/azure/azure-functions/functions-develop-vs#publish-to-azure)

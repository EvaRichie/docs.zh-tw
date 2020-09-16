---
title: 如何使用 ML.NET 自動化的 ML API
description: ML.NET 自動化的 ML API 會自動化模型建置程序，並產生隨時可供部署的模型。 了解您可用來設定自動化機器學習工作的選項。
ms.date: 12/18/2019
ms.custom: mvc,how-to
ms.openlocfilehash: b1ef526301e01e1e75e71e0646f4d11e68215d69
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540728"
---
# <a name="how-to-use-the-mlnet-automated-machine-learning-api"></a>如何使用 ML.NET 自動化的機器學習 API

自動化的機器學習 (AutoML) 會自動化將機器學習套用至資料的程序。 指定資料集，您可以執行 AutoML **實驗**來逐一查看不同的資料特徵化、機器學習演算法和超參數，以選取最佳的模型。

> [!NOTE]
> 本主題是指 ML.NET 的自動化機器學習 API，目前為預覽版。 資料可能會有變更。

## <a name="load-data"></a>載入資料

自動化的機器學習支援將資料集載入至 [IDataView](xref:Microsoft.ML.IDataView)。 資料的格式可以是定位字元分隔值 (TSV) 檔案和逗號分隔值 (CSV) 檔案。

範例：

```csharp
using Microsoft.ML;
using Microsoft.ML.AutoML;
    // ...
    MLContext mlContext = new MLContext();
    IDataView trainDataView = mlContext.Data.LoadFromTextFile<SentimentIssue>("my-data-file.csv", hasHeader: true);
```

## <a name="select-the-machine-learning-task-type"></a>選取機器學習工作類型

建立實驗之前，請先決定您想要解決的機器學習問題種類。 自動化的機器學習支援下列 ML 工作：

* 二元分類
* 多元分類
* 迴歸
* 建議

## <a name="create-experiment-settings"></a>建立實驗設定

建立已決定 ML 工作類型的實驗設定：

* 二元分類

  ```csharp
  var experimentSettings = new BinaryExperimentSettings();
  ```

* 多元分類

  ```csharp
  var experimentSettings = new MulticlassExperimentSettings();
  ```

* 迴歸

  ```csharp
  var experimentSettings = new RegressionExperimentSettings();
  ```

* 建議

  ```csharp
  var experimentSettings = new RecommendationExperimentSettings();
  ```

## <a name="configure-experiment-settings"></a>設定實驗設定

實驗的可設定程度很高。 如需組態設定的完整清單，請參閱 [AutoML API 文件](/dotnet/api/microsoft.ml.automl?view=ml-dotnet-preview)。

部分範例包括：

1. 指定允許執行實驗的時間上限。

    ```csharp
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    ```

1. 在排程完成前先使用取消權杖取消實驗。

    ```csharp
    experimentSettings.CancellationToken = cts.Token;

    // Cancel experiment after the user presses any key
    CancelExperimentAfterAnyKeyPress(cts);
    ```

1. 指定不同的最佳化計量。

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.OptimizingMetric = RegressionMetric.MeanSquaredError;
    ```

1. `CacheDirectory` 設定是目錄的指標，所有在 AutoML 工作期間定型的模型都儲存在此目錄。 如果 `CacheDirectory` 設為 null，則模型會保留在記憶體中，而不是寫入磁碟。

    ```csharp
    experimentSettings.CacheDirectory = null;
    ```

1. 指示自動化的 ML 不要使用某些定型器。

    依工作探索要最佳化之定型器的預設清單。 這份清單可針對每個實驗修改。 例如，您可從清單移除對資料集執行緩慢的定型器。 若要最佳化一個特定的定型器，請呼叫 `experimentSettings.Trainers.Clear()`，然後新增您想要使用的定型器。

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.Trainers.Remove(RegressionTrainer.LbfgsPoissonRegression);
    experimentSettings.Trainers.Remove(RegressionTrainer.OnlineGradientDescent);
    ```

依 ML 工作支援的定型器清單位在對應連結中，如下所示：

* [支援的二元分類演算法](xref:Microsoft.ML.AutoML.BinaryClassificationTrainer)
* [支援的多元分類演算法](xref:Microsoft.ML.AutoML.MulticlassClassificationTrainer)
* [支援的迴歸演算法](xref:Microsoft.ML.AutoML.RegressionTrainer)
* [支援的建議演算法](xref:Microsoft.ML.AutoML.RecommendationTrainer)

## <a name="optimizing-metric"></a>最佳化計量

最佳化度量，如上例所示，決定要在模型定型期間最佳化的計量。 您可以選取的最佳化計量由您所選工作類型決定。 以下為可用計量的清單。

|[二元分類](xref:Microsoft.ML.AutoML.BinaryClassificationMetric) | [多元分類](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric) |[回歸 & 建議](xref:Microsoft.ML.AutoML.RegressionMetric)
|-- |-- |--
|精確度| LogLoss | RSquared
|AreaUnderPrecisionRecallCurve | LogLossReduction | MeanAbsoluteError
|AreaUnderRocCurve | MacroAccuracy | MeanSquaredError
|F1Score | MicroAccuracy | RootMeanSquaredError
|NegativePrecision | TopKAccuracy
|NegativeRecall |
|PositivePrecision
|PositiveRecall

## <a name="data-pre-processing-and-featurization"></a>資料預先處理與特徵化

> [!NOTE]
> Feature 資料行僅支援 <xref:System.Boolean> 、和的類型 <xref:System.Single> <xref:System.String> 。

根據預設，資料予以前置處理，並為您自動執行下列步驟：

1. 卸除無有用資訊的特性

    將無實用資訊的特徵從定型與驗證集合中卸除。 其中包括遺漏所有值、所有資料列之間的值相同，或具有極高基數 (例如雜湊、識別碼或 GUID) 的特徵。

1. 遺漏值表示和插補

    以資料類型的預設值填入遺漏值資料格。 以和輸入資料行相同的插槽數附加指標特性。 如果輸入資料行中的值遺漏，則附加指標特性中的值是 `1`；否則為 `0`。

1. 產生其他特徵

    針對文字功能：使用 unigrams 和三字元字元的全字組功能。

    針對類別功能：適用于低基數功能的一種經常性編碼，以及高基數類別功能的一次熱雜湊編碼。

1. 轉換與編碼

    極少數唯一值轉換成類別特性的文字特性。 視類別特性的基數而定，執行 One-Hot 編碼或 One-Hot 雜湊編碼。

## <a name="exit-criteria"></a>允出準則

定義完成工作的準則：

1. 在一段時間後結束 - 在您的實驗設定中使用 `MaxExperimentTimeInSeconds`，您可以定義工作應該繼續執行的秒數。

1. 於取消權杖處結束 - 您可以使用取消權杖，讓您在排程完成前取消工作。

    ```csharp
    var cts = new CancellationTokenSource();
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    experimentSettings.CancellationToken = cts.Token;
    ```

## <a name="create-an-experiment"></a>建立實驗

一旦設定了實驗設定，您就隨時可以建立實驗。

```csharp
RegressionExperiment experiment = mlContext.Auto().CreateRegressionExperiment(experimentSettings);
```

## <a name="run-the-experiment"></a>執行實驗

執行實驗會觸發前置處理資料、選取學習演算法，以及微調超參數。 AutoML 會繼續產生特徵化、學習演算法和超參數的組合，直到達到 `MaxExperimentTimeInSeconds` 或實驗終止。

```csharp
ExperimentResult<RegressionMetrics> experimentResult = experiment
    .Execute(trainingDataView, LabelColumnName, progressHandler: progressHandler);
```

如果您想要傳入驗證資料、指出資料行目的的資料行資訊或前置特徵化工具，請探索 `Execute()` 的其他多載。

## <a name="training-modes"></a>定型模式

### <a name="training-dataset"></a>定型資料集

AutoML 提供多載的實驗執行方法，讓您提供定型資料。 就內部而言，自動化的 ML 會將資料分成定型驗證分割。

```csharp
experiment.Execute(trainDataView);
```

### <a name="custom-validation-dataset"></a>自訂驗證資料集

如不接受隨機分割，請使用自訂的驗證資料集，時間序列資料通常是這種情況。 您可以指定自己的驗證資料集。 針對指定的驗證資料集評估模型，而不是一或多個隨機資料集。

```csharp
experiment.Execute(trainDataView, validationDataView);
```

## <a name="explore-model-metrics"></a>探索模型計量

每次反覆運算 ML 實驗之後，會儲存與該工作相關的計量。

例如，我們可以存取最佳回合的驗證計量：

```csharp
RegressionMetrics metrics = experimentResult.BestRun.ValidationMetrics;
Console.WriteLine($"R-Squared: {metrics.RSquared:0.##}");
Console.WriteLine($"Root Mean Squared Error: {metrics.RootMeanSquaredError:0.##}");
```

下列是每項 ML 工作的所有可用計量：

* [二元分類計量](xref:Microsoft.ML.AutoML.BinaryClassificationMetric)
* [多元分類計量](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric)
* [回歸 & 建議計量](xref:Microsoft.ML.AutoML.RegressionMetric)

## <a name="see-also"></a>另請參閱

如需完整的程式碼範例和更多範例，請瀏覽 GitHub 存放庫的 [ 範例](https://github.com/dotnet/machinelearning-samples/tree/master#automate-mlnet-models-generation-preview-state)。

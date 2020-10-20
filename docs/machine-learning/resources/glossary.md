---
title: 機器學習字彙
description: 對於您在 ML.NET 中建置自訂模型來說，相當實用的重要機器學習詞彙。
ms.topic: reference
ms.date: 07/31/2019
ms.openlocfilehash: 32ccb6df1cb08db45ebd25a0d1c0ea4396a6c50b
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223740"
---
# <a name="machine-learning-glossary-of-important-terms"></a><span data-ttu-id="bd1ae-103">機器學習詞彙的重要字詞</span><span class="sxs-lookup"><span data-stu-id="bd1ae-103">Machine learning glossary of important terms</span></span>

<span data-ttu-id="bd1ae-104">以下清單匯集了對於您在 ML.NET 中建置自訂模型來說，相當實用的重要機器學習字詞。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-104">The following list is a compilation of important machine learning terms that are useful as you build your custom models in ML.NET.</span></span>

## <a name="accuracy"></a><span data-ttu-id="bd1ae-105">精確度</span><span class="sxs-lookup"><span data-stu-id="bd1ae-105">Accuracy</span></span>

<span data-ttu-id="bd1ae-106">在[分類](#classification)中，準確率係指正確分類的項目數，除以測試集內的項目總數後，所得出的值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-106">In [classification](#classification), accuracy is the number of correctly classified items divided by the total number of items in the test set.</span></span> <span data-ttu-id="bd1ae-107">範圍為 0 (最不準確) 到 1 (最準確)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-107">Ranges from 0 (least accurate) to 1 (most accurate).</span></span> <span data-ttu-id="bd1ae-108">準確率是模型效能的其中一個評估計量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-108">Accuracy is one of evaluation metrics of the model performance.</span></span> <span data-ttu-id="bd1ae-109">請將它與[精確率](#precision)、[召回率](#recall)及 [F 分數](#f-score)一起考量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-109">Consider it in conjunction with [precision](#precision), [recall](#recall), and [F-score](#f-score).</span></span>

## <a name="area-under-the-curve-auc"></a><span data-ttu-id="bd1ae-110">曲線下的面積 (AUC)</span><span class="sxs-lookup"><span data-stu-id="bd1ae-110">Area under the curve (AUC)</span></span>

<span data-ttu-id="bd1ae-111">在[二元分類](#binary-classification)中，作為曲線下面積值的評估計量，此面積會繪製出真陽性率 (Y 軸上) 與偽陽性率 (X 軸上) 的對比。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-111">In [binary classification](#binary-classification), an evaluation metric that is the value of the area under the curve that plots the true positives rate (on the y-axis) against the false positives rate (on the x-axis).</span></span> <span data-ttu-id="bd1ae-112">範圍為 0.5 (最差) 到 1 (最佳)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-112">Ranges from 0.5 (worst) to 1 (best).</span></span> <span data-ttu-id="bd1ae-113">這也稱為 ROC 曲線 (亦即 Receiver Operating Characteristic Curve (接收者操作特徵曲線)) 下的面積。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-113">Also known as the area under the ROC curve, i.e., receiver operating characteristic curve.</span></span> <span data-ttu-id="bd1ae-114">如需詳細資訊，請參閱維基百科上的[接收者操作特徵](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-114">For more information, see the [Receiver operating characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) article on Wikipedia.</span></span>

## <a name="binary-classification"></a><span data-ttu-id="bd1ae-115">二元分類</span><span class="sxs-lookup"><span data-stu-id="bd1ae-115">Binary classification</span></span>

<span data-ttu-id="bd1ae-116">[標籤](#label)僅來自兩個類別其中之一的[分類](#classification)案例。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-116">A [classification](#classification) case where the [label](#label) is only one out of two classes.</span></span> <span data-ttu-id="bd1ae-117">如需詳細資訊，請參閱[機器學習工作](tasks.md)主題的[二元分類](tasks.md#binary-classification)一節。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-117">For more information, see the [Binary classification](tasks.md#binary-classification) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="calibration"></a><span data-ttu-id="bd1ae-118">校正</span><span class="sxs-lookup"><span data-stu-id="bd1ae-118">Calibration</span></span>

<span data-ttu-id="bd1ae-119">校正是將未經處理分數對應到二元和多元分類類別成員資格的程序。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-119">Calibration is the process of mapping a raw score onto a class membership, for binary and multiclass classification.</span></span> <span data-ttu-id="bd1ae-120">有一些 ML.NET 定型器有 `NonCalibrated` 尾碼。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-120">Some ML.NET trainers have a `NonCalibrated` suffix.</span></span> <span data-ttu-id="bd1ae-121">這些演算法會產生必須對應至類別機率的未經處理分數。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-121">These algorithms produce a raw score that then must be mapped to a class probability.</span></span>

## <a name="catalog"></a><span data-ttu-id="bd1ae-122">目錄</span><span class="sxs-lookup"><span data-stu-id="bd1ae-122">Catalog</span></span>

<span data-ttu-id="bd1ae-123">在 ML.NET 中，目錄是延伸模組函式集合，依一般用途分組。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-123">In ML.NET, a catalog is a collection of extension functions, grouped by a common purpose.</span></span>

<span data-ttu-id="bd1ae-124">例如，每個機器學習工作 (二元分類、迴歸、排名等等) 都有可用的機器學習演算法 (定型器) 目錄。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-124">For example, each machine learning task (binary classification, regression, ranking etc) has a catalog of available machine learning algorithms (trainers).</span></span> <span data-ttu-id="bd1ae-125">二元分類定型器的目錄是：<xref:Microsoft.ML.BinaryClassificationCatalog.BinaryClassificationTrainers>。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-125">The catalog for the binary classification trainers is: <xref:Microsoft.ML.BinaryClassificationCatalog.BinaryClassificationTrainers>.</span></span>

## <a name="classification"></a><span data-ttu-id="bd1ae-126">分類</span><span class="sxs-lookup"><span data-stu-id="bd1ae-126">Classification</span></span>

<span data-ttu-id="bd1ae-127">使用資料來預測分類時，[監督式機器學習](#supervised-machine-learning)工作便稱為分類。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-127">When the data is used to predict a category, [supervised machine learning](#supervised-machine-learning) task is called classification.</span></span> <span data-ttu-id="bd1ae-128">[二元分類](#binary-classification)係指僅預測兩個分類 (例如，將影像分類成「貓」或「狗」的圖片)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-128">[Binary classification](#binary-classification) refers to predicting only two categories (for example, classifying an image as a picture of either a 'cat' or a 'dog').</span></span> <span data-ttu-id="bd1ae-129">[多元分類](#multiclass-classification)係指預測多個分類 (例如，將影像分類成一種特定狗品種的圖片)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-129">[Multiclass classification](#multiclass-classification) refers to predicting multiple categories (for example, when classifying an image as a picture of a specific breed of dog).</span></span>

## <a name="coefficient-of-determination"></a><span data-ttu-id="bd1ae-130">決定係數</span><span class="sxs-lookup"><span data-stu-id="bd1ae-130">Coefficient of determination</span></span>

<span data-ttu-id="bd1ae-131">在[迴歸](#regression)中，指出資料與模型相符程度的評估計量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-131">In [regression](#regression), an evaluation metric that indicates how well data fits a model.</span></span> <span data-ttu-id="bd1ae-132">範圍為 0 到 1。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-132">Ranges from 0 to 1.</span></span> <span data-ttu-id="bd1ae-133">值為 0 時，表示資料為隨機資料，或與模型不相符。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-133">A value of 0 means that the data is random or otherwise cannot be fit to the model.</span></span> <span data-ttu-id="bd1ae-134">值為 1 時，表示模型與資料完全相符。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-134">A value of 1 means that the model exactly matches the data.</span></span> <span data-ttu-id="bd1ae-135">這通常稱為r<sup>2</sup>R<sup>2</sup> 或 R 平方。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-135">This is often referred to as r<sup>2</sup>, R<sup>2</sup>, or r-squared.</span></span>

## <a name="data"></a><span data-ttu-id="bd1ae-136">資料</span><span class="sxs-lookup"><span data-stu-id="bd1ae-136">Data</span></span>

<span data-ttu-id="bd1ae-137">資料是所有機器學習應用程式的中心。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-137">Data is central to any machine learning application.</span></span> <span data-ttu-id="bd1ae-138">在 ML.NET 中，資料是由 <xref:Microsoft.ML.IDataView> 物件表示。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-138">In ML.NET data is represented by <xref:Microsoft.ML.IDataView> objects.</span></span> <span data-ttu-id="bd1ae-139">資料檢視物件：</span><span class="sxs-lookup"><span data-stu-id="bd1ae-139">Data view objects:</span></span>

- <span data-ttu-id="bd1ae-140">由資料行和資料列組成</span><span class="sxs-lookup"><span data-stu-id="bd1ae-140">are made up of columns and rows</span></span>
- <span data-ttu-id="bd1ae-141">延遲評估，即作業呼叫它時，它們只載入資料</span><span class="sxs-lookup"><span data-stu-id="bd1ae-141">are lazily evaluated, that is they only load data when an operation calls for it</span></span>
- <span data-ttu-id="bd1ae-142">包含定義每個資料行類型、格式和長度的結構描述</span><span class="sxs-lookup"><span data-stu-id="bd1ae-142">contain a schema that defines the type, format and length of each column</span></span>

## <a name="estimator"></a><span data-ttu-id="bd1ae-143">評估工具</span><span class="sxs-lookup"><span data-stu-id="bd1ae-143">Estimator</span></span>

<span data-ttu-id="bd1ae-144">ML.NET 中實作 <xref:Microsoft.ML.IEstimator%601> 介面的類別。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-144">A class in ML.NET that implements the <xref:Microsoft.ML.IEstimator%601> interface.</span></span>

<span data-ttu-id="bd1ae-145">評估工具是轉換的規格 (資料準備轉換和機器學習模型定型轉換)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-145">An estimator is a specification of a transformation (both data preparation transformation and machine learning model training transformation).</span></span> <span data-ttu-id="bd1ae-146">評估工具可以一起鏈結到轉換管線。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-146">Estimators can be chained together into a pipeline of transformations.</span></span> <span data-ttu-id="bd1ae-147">評估工具參數或評估工具管線是在呼叫 <xref:Microsoft.ML.IEstimator%601.Fit%2A> 時學到。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-147">The parameters of an estimator or pipeline of estimators are learned when <xref:Microsoft.ML.IEstimator%601.Fit%2A> is called.</span></span> <span data-ttu-id="bd1ae-148"><xref:Microsoft.ML.IEstimator%601.Fit%2A> 的結果是[轉換器](#transformer)。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-148">The result of <xref:Microsoft.ML.IEstimator%601.Fit%2A> is a [Transformer](#transformer).</span></span>

## <a name="extension-method"></a><span data-ttu-id="bd1ae-149">擴充方法</span><span class="sxs-lookup"><span data-stu-id="bd1ae-149">Extension method</span></span>

<span data-ttu-id="bd1ae-150">屬於類別，但定義在類別外的 .NET 方法。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-150">A .NET method that is part of a class but is defined outside of the class.</span></span> <span data-ttu-id="bd1ae-151">擴充方法的第一個參數是擴充方法所屬類別的靜態 `this` 參考。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-151">The first parameter of an extension method is a static `this` reference to the class to which the extension method belongs.</span></span>

<span data-ttu-id="bd1ae-152">擴充方法密集用在 ML.NET 中，以建構[評估工具](#estimator)的執行個體。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-152">Extension methods are used extensively in ML.NET to construct instances of [estimators](#estimator).</span></span>

## <a name="feature"></a><span data-ttu-id="bd1ae-153">功能</span><span class="sxs-lookup"><span data-stu-id="bd1ae-153">Feature</span></span>

<span data-ttu-id="bd1ae-154">所評估之現象的可評估屬性，通常是一個數 (雙精度浮點數) 值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-154">A measurable property of the phenomenon being measured, typically a numeric (double) value.</span></span> <span data-ttu-id="bd1ae-155">多個特徵會稱為**特徵向量**，且通常會儲存成 `double[]`。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-155">Multiple features are referred to as a **Feature vector** and typically stored as `double[]`.</span></span> <span data-ttu-id="bd1ae-156">特徵定義了所評估之現象的重要特性。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-156">Features define the important characteristics of the phenomenon being measured.</span></span> <span data-ttu-id="bd1ae-157">如需詳細資訊，請參閱維基百科上的[特徵](https://en.wikipedia.org/wiki/Feature_(machine_learning)) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-157">For more information, see the [Feature](https://en.wikipedia.org/wiki/Feature_(machine_learning)) article on Wikipedia.</span></span>

## <a name="feature-engineering"></a><span data-ttu-id="bd1ae-158">特徵設計</span><span class="sxs-lookup"><span data-stu-id="bd1ae-158">Feature engineering</span></span>

<span data-ttu-id="bd1ae-159">特徵工程是一個程序，牽涉到定義一組[特徵](#feature)，並開發能從可用現象資料產生特徵向量 (亦即特徵擷取) 的軟體。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-159">Feature engineering is the process that involves defining a set of [features](#feature) and developing software that produces feature vectors from available phenomenon data, i.e., feature extraction.</span></span> <span data-ttu-id="bd1ae-160">如需詳細資訊，請參閱維基百科上的[特徵工程](https://en.wikipedia.org/wiki/Feature_engineering) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-160">For more information, see the [Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering) article on Wikipedia.</span></span>

## <a name="f-score"></a><span data-ttu-id="bd1ae-161">F 分數</span><span class="sxs-lookup"><span data-stu-id="bd1ae-161">F-score</span></span>

<span data-ttu-id="bd1ae-162">在[分類](#classification)中，用來平衡[精準率](#precision)和[召回率](#recall)的評估計量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-162">In [classification](#classification), an evaluation metric that balances [precision](#precision) and [recall](#recall).</span></span>

## <a name="hyperparameter"></a><span data-ttu-id="bd1ae-163">超參數</span><span class="sxs-lookup"><span data-stu-id="bd1ae-163">Hyperparameter</span></span>

<span data-ttu-id="bd1ae-164">機器學習演算法的參數。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-164">A parameter of a machine learning algorithm.</span></span> <span data-ttu-id="bd1ae-165">範例包括決策樹系中要學習的樹數目，或梯度下降演算法中的步階大小。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-165">Examples include the number of trees to learn in a decision forest or the step size in a gradient descent algorithm.</span></span> <span data-ttu-id="bd1ae-166">「超參數」\*\* 的值是在將模型定型之前設定的，並且會控管尋找預測函式之參數 (例如決策樹中的比較點或線性迴歸模型中的加權) 的程序。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-166">Values of *Hyperparameters* are set before training the model and govern the process of finding the parameters of the prediction function, for example, the comparison points in a decision tree or the weights in a linear regression model.</span></span> <span data-ttu-id="bd1ae-167">如需詳細資訊，請參閱維基百科上的[超參數](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-167">For more information, see the [Hyperparameter](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) article on Wikipedia.</span></span>

## <a name="label"></a><span data-ttu-id="bd1ae-168">標籤</span><span class="sxs-lookup"><span data-stu-id="bd1ae-168">Label</span></span>

<span data-ttu-id="bd1ae-169">要使用機器學習模型來預測的元素。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-169">The element to be predicted with the machine learning model.</span></span> <span data-ttu-id="bd1ae-170">例如，狗的品種或未來的股價。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-170">For example, the breed of dog or a future stock price.</span></span>

## <a name="log-loss"></a><span data-ttu-id="bd1ae-171">對數損失</span><span class="sxs-lookup"><span data-stu-id="bd1ae-171">Log loss</span></span>

<span data-ttu-id="bd1ae-172">在[分類](#classification)中，描述分類器準確率特性的評估計量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-172">In [classification](#classification), an evaluation metric that characterizes the accuracy of a classifier.</span></span> <span data-ttu-id="bd1ae-173">對數損失越小，分類器的準確率就越高。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-173">The smaller log loss is, the more accurate a classifier is.</span></span>

## <a name="loss-function"></a><span data-ttu-id="bd1ae-174">Loss 函式</span><span class="sxs-lookup"><span data-stu-id="bd1ae-174">Loss function</span></span>

<span data-ttu-id="bd1ae-175">Loss 函式是定型標籤值和模型所做預測之間的差異。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-175">A loss function is the difference between the training label values and the prediction made by the model.</span></span> <span data-ttu-id="bd1ae-176">模型的參數是透過將 loss 函式降到最低來評估。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-176">The parameters of the model are estimated by minimizing the loss function.</span></span>

<span data-ttu-id="bd1ae-177">不同的定型器可使用不同 loss 函式設定。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-177">Different trainers can be configured with different loss functions.</span></span>

## <a name="mean-absolute-error-mae"></a><span data-ttu-id="bd1ae-178">平均絕對誤差 (MAE)</span><span class="sxs-lookup"><span data-stu-id="bd1ae-178">Mean absolute error (MAE)</span></span>

<span data-ttu-id="bd1ae-179">在[迴歸](#regression)中，作為所有模型誤差平均值的評估計量，其中模型誤差係指所預測[標籤](#label)值與正確標籤值之間的差距。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-179">In [regression](#regression), an evaluation metric that is the average of all the model errors, where model error is the distance between the predicted [label](#label) value and the correct label value.</span></span>

## <a name="model"></a><span data-ttu-id="bd1ae-180">模型</span><span class="sxs-lookup"><span data-stu-id="bd1ae-180">Model</span></span>

<span data-ttu-id="bd1ae-181">傳統上，預測函式的參數。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-181">Traditionally, the parameters for the prediction function.</span></span> <span data-ttu-id="bd1ae-182">例如，線性迴歸模型中的加權，或決策樹中的分割點。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-182">For example, the weights in a linear regression model or the split points in a decision tree.</span></span> <span data-ttu-id="bd1ae-183">在 ML.NET 中，模型包含預測領域物件 (例如影像或文字) [標籤](#label)所需的一切資訊。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-183">In ML.NET, a model contains all the information necessary to predict the [label](#label) of a domain object (for example, image or text).</span></span> <span data-ttu-id="bd1ae-184">這意謂著 ML.NET 模型除了包含預測函式的參數之外，也包含必要的特徵化步驟。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-184">This means that ML.NET models include the featurization steps necessary as well as the parameters for the prediction function.</span></span>

## <a name="multiclass-classification"></a><span data-ttu-id="bd1ae-185">多元分類</span><span class="sxs-lookup"><span data-stu-id="bd1ae-185">Multiclass classification</span></span>

<span data-ttu-id="bd1ae-186">[標籤](#label)來自三個或更多個類別其中之一的[分類](#classification)案例。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-186">A [classification](#classification) case where the [label](#label) is one out of three or more classes.</span></span> <span data-ttu-id="bd1ae-187">如需詳細資訊，請參閱[機器學習工作](tasks.md)主題的[多元分類](tasks.md#multiclass-classification)一節。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-187">For more information, see the [Multiclass classification](tasks.md#multiclass-classification) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="n-gram"></a><span data-ttu-id="bd1ae-188">N 連語法 (N-gram)</span><span class="sxs-lookup"><span data-stu-id="bd1ae-188">N-gram</span></span>

<span data-ttu-id="bd1ae-189">文字資料的特徵擷取配置：任何一連串的 N 個單字會轉換成[特徵](#feature)值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-189">A feature extraction scheme for text data: any sequence of N words turns into a [feature](#feature) value.</span></span>

## <a name="normalization"></a><span data-ttu-id="bd1ae-190">正規化</span><span class="sxs-lookup"><span data-stu-id="bd1ae-190">Normalization</span></span>

<span data-ttu-id="bd1ae-191">正規化是將浮點資料調整為 0 與 1 之間值的流程。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-191">Normalization is the process of scaling floating point data to values between 0 and 1.</span></span> <span data-ttu-id="bd1ae-192">ML.NET 中使用的許多定型演算法都需要將輸入功能資料標準化。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-192">Many of the training algorithms used in ML.NET require input feature data to be normalized.</span></span> <span data-ttu-id="bd1ae-193">ML.NET 提供一系列[用於正規化的轉換](transforms.md#normalization-and-scaling)</span><span class="sxs-lookup"><span data-stu-id="bd1ae-193">ML.NET provides a series of [transforms for normalization](transforms.md#normalization-and-scaling)</span></span>

## <a name="numerical-feature-vector"></a><span data-ttu-id="bd1ae-194">數值特徵向量</span><span class="sxs-lookup"><span data-stu-id="bd1ae-194">Numerical feature vector</span></span>

<span data-ttu-id="bd1ae-195">僅由數值組成的[特徵](#feature)向量。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-195">A [feature](#feature) vector consisting only of numerical values.</span></span> <span data-ttu-id="bd1ae-196">這與 `double[]` 類似。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-196">This is similar to `double[]`.</span></span>

## <a name="pipeline"></a><span data-ttu-id="bd1ae-197">管線</span><span class="sxs-lookup"><span data-stu-id="bd1ae-197">Pipeline</span></span>

<span data-ttu-id="bd1ae-198">讓模型與資料集相符所需的所有作業。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-198">All of the operations needed to fit a model to a data set.</span></span> <span data-ttu-id="bd1ae-199">管線會由資料輸入、轉換、特徵化及學習步驟所組成。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-199">A pipeline consists of data import, transformation, featurization, and learning steps.</span></span> <span data-ttu-id="bd1ae-200">在管線定型之後，就會轉換成模型。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-200">Once a pipeline is trained, it turns into a model.</span></span>

## <a name="precision"></a><span data-ttu-id="bd1ae-201">Precision</span><span class="sxs-lookup"><span data-stu-id="bd1ae-201">Precision</span></span>

<span data-ttu-id="bd1ae-202">在[分類](#classification)中，類別的精確率係指正確預測為屬於該類別的項目數，除以預測為屬於該類別的項目總數後，所得出的值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-202">In [classification](#classification), the precision for a class is the number of items correctly predicted as belonging to that class divided by the total number of items predicted as belonging to the class.</span></span>

## <a name="recall"></a><span data-ttu-id="bd1ae-203">召回</span><span class="sxs-lookup"><span data-stu-id="bd1ae-203">Recall</span></span>

<span data-ttu-id="bd1ae-204">在[分類](#classification)中，類別的召回率係指正確預測為屬於該類別的項目數，除以實際屬於該類別的項目總數後，所得出的值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-204">In [classification](#classification), the recall for a class is the number of items correctly predicted as belonging to that class divided by the total number of items that actually belong to the class.</span></span>

## <a name="regularization"></a><span data-ttu-id="bd1ae-205">正規化</span><span class="sxs-lookup"><span data-stu-id="bd1ae-205">Regularization</span></span>

 <span data-ttu-id="bd1ae-206">正規化不利於太過複雜的線性模型。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-206">Regularization penalizes a linear model for being too complicated.</span></span> <span data-ttu-id="bd1ae-207">正規化有兩種：</span><span class="sxs-lookup"><span data-stu-id="bd1ae-207">There are two types of regularization:</span></span>

- <span data-ttu-id="bd1ae-208">$L_1$ 正規化零加權不顯著的特性。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-208">$L_1$ regularization zeros weights for insignificant features.</span></span> <span data-ttu-id="bd1ae-209">在這種正規化後，已儲存的模型大小可能會變得較小。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-209">The size of the saved model may become smaller after this type of regularization.</span></span>
- <span data-ttu-id="bd1ae-210">$L _2 $ 正規化可將沒有意義特徵的加權範圍降至最低。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-210">$L_2$ regularization minimizes weight range for insignificant features.</span></span> <span data-ttu-id="bd1ae-211">這是更一般的程式，對極端值而言較不敏感。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-211">This is a more general process and is less sensitive to outliers.</span></span>

## <a name="regression"></a><span data-ttu-id="bd1ae-212">迴歸</span><span class="sxs-lookup"><span data-stu-id="bd1ae-212">Regression</span></span>

<span data-ttu-id="bd1ae-213">輸出為實際值 (例如雙精度浮點數) 的[機器學習](#supervised-machine-learning)工作。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-213">A [supervised machine learning](#supervised-machine-learning) task where the output is a real value, for example, double.</span></span> <span data-ttu-id="bd1ae-214">範例包括預測股價。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-214">Examples include predicting stock prices.</span></span> <span data-ttu-id="bd1ae-215">如需詳細資訊，請參閱[機器學習工作](tasks.md)主題的[迴歸](tasks.md#regression)一節。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-215">For more information, see the [Regression](tasks.md#regression) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="relative-absolute-error"></a><span data-ttu-id="bd1ae-216">相對絕對誤差</span><span class="sxs-lookup"><span data-stu-id="bd1ae-216">Relative absolute error</span></span>

<span data-ttu-id="bd1ae-217">在[迴歸](#regression)中，此評估計量是所有絕對誤差的總和除以正確[標籤](#label)值與所有正確標籤值之平均值的差距總和後，所得出的值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-217">In [regression](#regression), an evaluation metric that is the sum of all absolute errors divided by the sum of distances between correct [label](#label) values and the average of all correct label values.</span></span>

## <a name="relative-squared-error"></a><span data-ttu-id="bd1ae-218">相對平方誤差</span><span class="sxs-lookup"><span data-stu-id="bd1ae-218">Relative squared error</span></span>

<span data-ttu-id="bd1ae-219">在[迴歸](#regression)中，此評估計量是所有平方絕對誤差的總和除以正確[標籤](#label)值與所有正確標籤值之平均值的平方差距總和後，所得出的值。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-219">In [regression](#regression), an evaluation metric that is the sum of all squared absolute errors divided by the sum of squared distances between correct [label](#label) values and the average of all correct label values.</span></span>

## <a name="root-of-mean-squared-error-rmse"></a><span data-ttu-id="bd1ae-220">均方根誤差 (RMSE)</span><span class="sxs-lookup"><span data-stu-id="bd1ae-220">Root of mean squared error (RMSE)</span></span>

<span data-ttu-id="bd1ae-221">在[迴歸](#regression)中，此評估計量是誤差平方值之平均值的平方根。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-221">In [regression](#regression), an evaluation metric that is the square root of the average of the squares of the errors.</span></span>

## <a name="scoring"></a><span data-ttu-id="bd1ae-222">計分</span><span class="sxs-lookup"><span data-stu-id="bd1ae-222">Scoring</span></span>

<span data-ttu-id="bd1ae-223">評分是將新資料套用至定型機器學習模型並產生預測的流程。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-223">Scoring is the process of applying new data to a trained machine learning model, and generating predictions.</span></span> <span data-ttu-id="bd1ae-224">評分也稱為推斷。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-224">Scoring is also known as inferencing.</span></span> <span data-ttu-id="bd1ae-225">根據模型的類型而定，分數可能是原始值、機率或類別。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-225">Depending on the type of model, the score may be a raw value, a probability, or a category.</span></span>

## <a name="supervised-machine-learning"></a><span data-ttu-id="bd1ae-226">監督式機器學習</span><span class="sxs-lookup"><span data-stu-id="bd1ae-226">Supervised machine learning</span></span>

<span data-ttu-id="bd1ae-227">這是機器學習的子集，其中所需的模型會預測尚未顯示資料的標籤。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-227">A subclass of machine learning in which a desired model predicts the label for yet-unseen data.</span></span> <span data-ttu-id="bd1ae-228">範例包括分類、迴歸及結構化預測。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-228">Examples include classification, regression, and structured prediction.</span></span> <span data-ttu-id="bd1ae-229">如需詳細資訊，請參閱維基百科上的[監督式學習](https://en.wikipedia.org/wiki/Supervised_learning) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-229">For more information, see the  [Supervised learning](https://en.wikipedia.org/wiki/Supervised_learning) article on Wikipedia.</span></span>

## <a name="training"></a><span data-ttu-id="bd1ae-230">訓練</span><span class="sxs-lookup"><span data-stu-id="bd1ae-230">Training</span></span>

<span data-ttu-id="bd1ae-231">針對所指定定型資料集，識別[模型](#model)的程序。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-231">The process of identifying a [model](#model) for a given training data set.</span></span> <span data-ttu-id="bd1ae-232">就線性模型而言，這意謂著要尋找加權。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-232">For a linear model, this means finding the weights.</span></span> <span data-ttu-id="bd1ae-233">就決策樹而言，則涉及識別分割點。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-233">For a tree, it involves identifying the split points.</span></span>

## <a name="transformer"></a><span data-ttu-id="bd1ae-234">轉換器</span><span class="sxs-lookup"><span data-stu-id="bd1ae-234">Transformer</span></span>

<span data-ttu-id="bd1ae-235">實作 <xref:Microsoft.ML.ITransformer> 介面的 ML.NET 類別。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-235">An ML.NET class that implements the <xref:Microsoft.ML.ITransformer> interface.</span></span>

<span data-ttu-id="bd1ae-236">轉換器會將一個 <xref:Microsoft.ML.IDataView> 轉換成另一個。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-236">A transformer transforms one <xref:Microsoft.ML.IDataView> into another.</span></span> <span data-ttu-id="bd1ae-237">轉換器是透過定型[評估工具](#estimator)或評估管線所建立。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-237">A transformer is created by training an [estimator](#estimator), or an estimator pipeline.</span></span>

## <a name="unsupervised-machine-learning"></a><span data-ttu-id="bd1ae-238">非監督式機器學習</span><span class="sxs-lookup"><span data-stu-id="bd1ae-238">Unsupervised machine learning</span></span>

<span data-ttu-id="bd1ae-239">一個機器學習子集，其中所需的模型會尋找資料中隱藏 (或潛伏) 的結構。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-239">A subclass of machine learning in which a desired model finds hidden (or latent) structure in data.</span></span> <span data-ttu-id="bd1ae-240">範例包括群集、建立主題模型，以及縮減維度。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-240">Examples include clustering, topic modeling, and dimensionality reduction.</span></span> <span data-ttu-id="bd1ae-241">如需詳細資訊，請參閱維基百科上的[非監督式學習](https://en.wikipedia.org/wiki/Unsupervised_learning) \(英文\) 一文。</span><span class="sxs-lookup"><span data-stu-id="bd1ae-241">For more information, see the [Unsupervised learning](https://en.wikipedia.org/wiki/Unsupervised_learning) article on Wikipedia.</span></span>

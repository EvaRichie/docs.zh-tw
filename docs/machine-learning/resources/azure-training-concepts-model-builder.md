---
title: 模型產生器 Azure 訓練資源
description: Azure Machine Learning 的資源指南
ms.topic: reference
ms.date: 06/01/2020
ms.author: luquinta
author: luisquintanilla
ms.openlocfilehash: 8622b580b7925adfd7895317815021f57960e9ee
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924574"
---
# <a name="model-builder-azure-training-resources"></a><span data-ttu-id="bfbc5-103">模型產生器 Azure 訓練資源</span><span class="sxs-lookup"><span data-stu-id="bfbc5-103">Model Builder Azure Training Resources</span></span>

<span data-ttu-id="bfbc5-104">下列指南可協助您深入瞭解在 Azure 中使用模型產生器來定型模型所用的資源。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-104">The following is a guide to help you learn more about resources used to train models in Azure with Model Builder.</span></span>

## <a name="what-is-an-azure-machine-learning-experiment"></a><span data-ttu-id="bfbc5-105">什麼是 Azure Machine Learning 實驗？</span><span class="sxs-lookup"><span data-stu-id="bfbc5-105">What is an Azure Machine Learning experiment?</span></span>

<span data-ttu-id="bfbc5-106">Azure Machine Learning 實驗是在 Azure 上執行模型產生器訓練之前必須建立的資源。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-106">An Azure Machine Learning experiment is a resource that needs to be created before running Model Builder training on Azure.</span></span>

<span data-ttu-id="bfbc5-107">實驗會針對一或多個機器學習訓練執行封裝設定和結果。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-107">The experiment encapsulates the configuration and results for one or more machine learning training runs.</span></span> <span data-ttu-id="bfbc5-108">實驗屬於特定的工作區。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-108">Experiments belong to a specific workspace.</span></span> <span data-ttu-id="bfbc5-109">第一次建立實驗時，其名稱會在工作區中註冊。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-109">The first time an experiment is created, its name is registered in the workspace.</span></span> <span data-ttu-id="bfbc5-110">任何後續的執行-如果使用相同的實驗名稱，則會記錄為相同實驗的一部分。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-110">Any subsequent runs - if the same experiment name is used - are logged as part of the same experiment.</span></span> <span data-ttu-id="bfbc5-111">否則，會建立新的實驗。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-111">Otherwise, a new experiment is created.</span></span>

## <a name="what-is-an-azure-machine-learning-workspace"></a><span data-ttu-id="bfbc5-112">什麼是 Azure Machine Learning 工作區？</span><span class="sxs-lookup"><span data-stu-id="bfbc5-112">What is an Azure Machine Learning workspace?</span></span>

<span data-ttu-id="bfbc5-113">工作區是一種 Azure Machine Learning 資源，可針對在定型執行過程中建立的所有 Azure Machine Learning 資源和成品提供集中位置。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-113">A workspace is an Azure Machine Learning resource that provides a central place for all Azure Machine Learning resources and artifacts created as part of training run.</span></span>

<span data-ttu-id="bfbc5-114">若要建立 Azure Machine Learning 工作區，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-114">To create an Azure Machine Learning workspace, the following are required:</span></span>

- <span data-ttu-id="bfbc5-115">名稱：您的工作區名稱，介於3-33 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-115">Name: A name for your workspace between 3-33 characters.</span></span> <span data-ttu-id="bfbc5-116">名稱只可包含英數位元和連字號。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-116">Names may only contain alphanumeric characters and hyphens.</span></span>
- <span data-ttu-id="bfbc5-117">區域：您的工作區和資源部署所在之資料中心的地理位置。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-117">Region: The geographic location of the data center where your workspace and resources are deployed to.</span></span> <span data-ttu-id="bfbc5-118">建議您選擇靠近您或客戶的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-118">It is recommended that you choose a location close to where you or your customers are.</span></span>
- <span data-ttu-id="bfbc5-119">資源群組：容器，其中包含 Azure 解決方案的所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-119">Resource group: A container that contains all related resources for an Azure solution.</span></span>

## <a name="what-is-an-azure-machine-learning-compute"></a><span data-ttu-id="bfbc5-120">什麼是 Azure Machine Learning 計算？</span><span class="sxs-lookup"><span data-stu-id="bfbc5-120">What is an Azure Machine Learning compute?</span></span>

<span data-ttu-id="bfbc5-121">Azure Machine Learning 計算是用於定型的雲端式 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-121">An Azure Machine Learning compute is a cloud-based Linux VM used for training.</span></span>

<span data-ttu-id="bfbc5-122">若要建立 Azure Machine Learning 工作區，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-122">To create an Azure Machine Learning workspace, the following are required:</span></span>

- <span data-ttu-id="bfbc5-123">名稱：您的工作區名稱，介於2-16 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-123">Name: A name for your workspace between 2-16 characters.</span></span> <span data-ttu-id="bfbc5-124">名稱只可包含英數位元和連字號。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-124">Names may only contain alphanumeric characters and hyphens.</span></span>
- <span data-ttu-id="bfbc5-125">計算大小</span><span class="sxs-lookup"><span data-stu-id="bfbc5-125">Compute size</span></span>

    <span data-ttu-id="bfbc5-126">模型產生器可以使用下列其中一種 GPU 優化計算類型：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-126">Model Builder can use one of the following GPU-optimized compute types:</span></span>

    | <span data-ttu-id="bfbc5-127">大小</span><span class="sxs-lookup"><span data-stu-id="bfbc5-127">Size</span></span> | <span data-ttu-id="bfbc5-128">vCPU</span><span class="sxs-lookup"><span data-stu-id="bfbc5-128">vCPU</span></span> | <span data-ttu-id="bfbc5-129">記憶體：GiB</span><span class="sxs-lookup"><span data-stu-id="bfbc5-129">Memory: GiB</span></span> | <span data-ttu-id="bfbc5-130">暫存儲存體 (SSD) GiB</span><span class="sxs-lookup"><span data-stu-id="bfbc5-130">Temp storage (SSD) GiB</span></span> | <span data-ttu-id="bfbc5-131">GPU</span><span class="sxs-lookup"><span data-stu-id="bfbc5-131">GPU</span></span> | <span data-ttu-id="bfbc5-132">GPU 記憶體：GiB</span><span class="sxs-lookup"><span data-stu-id="bfbc5-132">GPU memory: GiB</span></span> | <span data-ttu-id="bfbc5-133">最大資料磁碟</span><span class="sxs-lookup"><span data-stu-id="bfbc5-133">Max data disks</span></span> | <span data-ttu-id="bfbc5-134">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="bfbc5-134">Max NICs</span></span> |
    |---|---|---|---|---|---|---|---|
    | <span data-ttu-id="bfbc5-135">Standard_NC12</span><span class="sxs-lookup"><span data-stu-id="bfbc5-135">Standard_NC12</span></span>   | <span data-ttu-id="bfbc5-136">12</span><span class="sxs-lookup"><span data-stu-id="bfbc5-136">12</span></span> | <span data-ttu-id="bfbc5-137">112</span><span class="sxs-lookup"><span data-stu-id="bfbc5-137">112</span></span> | <span data-ttu-id="bfbc5-138">680</span><span class="sxs-lookup"><span data-stu-id="bfbc5-138">680</span></span>  | <span data-ttu-id="bfbc5-139">2</span><span class="sxs-lookup"><span data-stu-id="bfbc5-139">2</span></span> | <span data-ttu-id="bfbc5-140">24</span><span class="sxs-lookup"><span data-stu-id="bfbc5-140">24</span></span> | <span data-ttu-id="bfbc5-141">48</span><span class="sxs-lookup"><span data-stu-id="bfbc5-141">48</span></span> | <span data-ttu-id="bfbc5-142">2</span><span class="sxs-lookup"><span data-stu-id="bfbc5-142">2</span></span> |
    | <span data-ttu-id="bfbc5-143">Standard_NC24</span><span class="sxs-lookup"><span data-stu-id="bfbc5-143">Standard_NC24</span></span>   | <span data-ttu-id="bfbc5-144">24</span><span class="sxs-lookup"><span data-stu-id="bfbc5-144">24</span></span> | <span data-ttu-id="bfbc5-145">224</span><span class="sxs-lookup"><span data-stu-id="bfbc5-145">224</span></span> | <span data-ttu-id="bfbc5-146">1440</span><span class="sxs-lookup"><span data-stu-id="bfbc5-146">1440</span></span> | <span data-ttu-id="bfbc5-147">4</span><span class="sxs-lookup"><span data-stu-id="bfbc5-147">4</span></span> | <span data-ttu-id="bfbc5-148">48</span><span class="sxs-lookup"><span data-stu-id="bfbc5-148">48</span></span> | <span data-ttu-id="bfbc5-149">64</span><span class="sxs-lookup"><span data-stu-id="bfbc5-149">64</span></span> | <span data-ttu-id="bfbc5-150">4</span><span class="sxs-lookup"><span data-stu-id="bfbc5-150">4</span></span> |

    <span data-ttu-id="bfbc5-151">如需 GPU 優化計算類型的詳細資訊，請流覽[NC 系列 LINUX VM 檔](https://docs.microsoft.com/azure/virtual-machines/nc-series?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json)。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-151">Visit the [NC-series Linux VM documentation](https://docs.microsoft.com/azure/virtual-machines/nc-series?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json) for more details on GPU optimized compute types.</span></span>
- <span data-ttu-id="bfbc5-152">計算優先順序</span><span class="sxs-lookup"><span data-stu-id="bfbc5-152">Compute priority</span></span>

  - <span data-ttu-id="bfbc5-153">低優先順序：適用于執行時間較短的工作。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-153">Low-priority: Suited for tasks with shorter execution times.</span></span> <span data-ttu-id="bfbc5-154">可能受到中斷的影響，而且沒有可用的可用性。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-154">May be impacted by interruptions and lack of availability.</span></span> <span data-ttu-id="bfbc5-155">成本通常較低，因為它會利用 Azure 中剩餘的容量。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-155">Usually costs less because it takes advantage of surplus capacity in Azure.</span></span>
  - <span data-ttu-id="bfbc5-156">專用：適用于任何持續時間的工作，但特別是長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-156">Dedicated: Suited for tasks of any duration, but especially long-running jobs.</span></span> <span data-ttu-id="bfbc5-157">不受中斷或沒有可用性影響。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-157">Not impacted by interruptions or lack of availability.</span></span> <span data-ttu-id="bfbc5-158">成本通常會更高，因為它會在 Azure 中為您的工作保留一組專屬的計算資源。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-158">Usually costs more because it reserves a dedicated set of compute resources in Azure for your tasks.</span></span>

## <a name="training"></a><span data-ttu-id="bfbc5-159">訓練</span><span class="sxs-lookup"><span data-stu-id="bfbc5-159">Training</span></span>

<span data-ttu-id="bfbc5-160">Azure 上的訓練僅適用于模型產生器影像分類案例。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-160">Training on Azure is only available for the Model Builder image classification scenario.</span></span> <span data-ttu-id="bfbc5-161">用來定型這些模型的演算法是以 ResNet50 架構為基礎的深度類神經網路。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-161">The algorithm used to train these models is a Deep Neural Network based on the ResNet50 architecture.</span></span> <span data-ttu-id="bfbc5-162">定型程式需要一些時間，且時間量可能會根據所選計算的大小以及資料量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-162">The training process takes some time and the amount of time may vary depending on the size of compute selected as well as amount of data.</span></span> <span data-ttu-id="bfbc5-163">您可以藉由選取 Visual Studio 中的 [在 Azure 入口網站中監視目前的執行] 連結來追蹤執行進度。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-163">You can track the progress of your runs by selecting the "Monitor current run in Azure portal" link in Visual Studio.</span></span>

## <a name="results"></a><span data-ttu-id="bfbc5-164">結果</span><span class="sxs-lookup"><span data-stu-id="bfbc5-164">Results</span></span>

<span data-ttu-id="bfbc5-165">定型完成後，會將兩個專案新增至您的方案，並具有下列尾碼：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-165">Once training is complete, two projects are added to your solution with the following suffixes:</span></span>

- <span data-ttu-id="bfbc5-166">*Consoleapp.exe*： c # .net Core 主控台應用程式，可提供起始程式碼來建立預測管線並進行預測。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-166">*ConsoleApp*: A C# .NET Core console application that provides starter code to build the prediction pipeline and make predictions.</span></span>
- <span data-ttu-id="bfbc5-167">*Model*： c # .NET Standard 應用程式，其中包含定義輸入和輸出模型資料之架構的資料模型，以及下列資產：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-167">*Model*: A C# .NET Standard application that contains the data models that define the schema of input and output model data as well as the following assets:</span></span>

  - <span data-ttu-id="bfbc5-168">bestModel. onnx：以 Open Neural Network Exchange （ONNX）格式的模型序列化版本。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-168">bestModel.onnx: A serialized version of the model in Open Neural Network Exchange (ONNX) format.</span></span> <span data-ttu-id="bfbc5-169">ONNX 是 AI 模型的開放原始碼格式，可支援 ML.NET、PyTorch 和 TensorFlow 等架構之間的互通性。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-169">ONNX is an open source format for AI models that supports interoperability between frameworks like ML.NET, PyTorch and TensorFlow.</span></span>
  - <span data-ttu-id="bfbc5-170">bestModelMap.js于：進行預測以將模型輸出對應至文字分類時所使用的類別目錄清單。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-170">bestModelMap.json: A list of categories used when making predictions to map the model output to a text category.</span></span>
  - <span data-ttu-id="bfbc5-171">MLModel.zip： ML.NET 預測管線的序列化版本，其使用模型*bestModel*的序列化版本來進行預測，並使用檔案來對應輸出 `bestModelMap.json` 。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-171">MLModel.zip: A serialized version of the ML.NET prediction pipeline that uses the serialized version of the model *bestModel.onnx* to make predictions and maps outputs using the `bestModelMap.json` file.</span></span>

## <a name="use-the-machine-learning-model"></a><span data-ttu-id="bfbc5-172">使用機器學習模型</span><span class="sxs-lookup"><span data-stu-id="bfbc5-172">Use the machine learning model</span></span>

<span data-ttu-id="bfbc5-173">`ModelInput` `ModelOutput` *模型*專案中的和類別會分別定義模型預期之輸入和輸出的架構。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-173">The `ModelInput` and `ModelOutput` classes in the *Model* project define the schema of the model's expected input and output respectively.</span></span>

<span data-ttu-id="bfbc5-174">在影像分類案例中， `ModelInput` 包含兩個數據行：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-174">In an image classification scenario, the `ModelInput` contains two columns:</span></span>

- <span data-ttu-id="bfbc5-175">`ImageSource`：影像位置的字串路徑。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-175">`ImageSource`: The string path of the image location.</span></span>
- <span data-ttu-id="bfbc5-176">`Label`：影像所屬的實體類別目錄。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-176">`Label`: The actual category the image belongs to.</span></span> <span data-ttu-id="bfbc5-177">`Label`在進行定型時，只會當做輸入使用，而在進行預測時則不需要提供。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-177">`Label` is only used as an input when training and does not need to be provided when making predictions.</span></span>

<span data-ttu-id="bfbc5-178">`ModelOutput`包含兩個數據行：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-178">The `ModelOutput` contains two columns:</span></span>

- <span data-ttu-id="bfbc5-179">`Prediction`：影像的預測類別。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-179">`Prediction`: The image's predicted category.</span></span>
- <span data-ttu-id="bfbc5-180">`Score`：所有類別的機率清單（最高的屬於 `Prediction` ）。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-180">`Score`: The list of probabilities for all categories (the highest belongs to the `Prediction`).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bfbc5-181">疑難排解</span><span class="sxs-lookup"><span data-stu-id="bfbc5-181">Troubleshooting</span></span>

### <a name="cannot-create-compute"></a><span data-ttu-id="bfbc5-182">無法建立計算</span><span class="sxs-lookup"><span data-stu-id="bfbc5-182">Cannot create compute</span></span>

<span data-ttu-id="bfbc5-183">如果在建立 Azure Machine Learning 計算期間發生錯誤，計算資源可能仍存在，錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-183">If an error occurs during Azure Machine Learning compute creation, the compute resource may still exist, in an errored state.</span></span> <span data-ttu-id="bfbc5-184">如果您嘗試以相同的名稱重新建立計算資源，作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="bfbc5-184">If you try to re-create the compute resource with the same name, the operation fails.</span></span> <span data-ttu-id="bfbc5-185">若要修正此錯誤，請使用以下其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="bfbc5-185">To fix this error, either:</span></span>

- <span data-ttu-id="bfbc5-186">以不同的名稱建立新的計算</span><span class="sxs-lookup"><span data-stu-id="bfbc5-186">Create the new compute with a different name</span></span>
- <span data-ttu-id="bfbc5-187">移至 Azure 入口網站，並移除原始的計算資源</span><span class="sxs-lookup"><span data-stu-id="bfbc5-187">Go to the Azure portal, and remove the original compute resource</span></span>

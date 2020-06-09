---
title: 依 ML.NET CLI 排列的遙測集合
description: 了解 ML.NET CLI 遙測特性，它會收集用於分析、要收集哪些資料，以及如何停用的使用資訊。 此外，尋找 Microsoft GDPR 合規性 .NET 授權合約和相關資訊的連結。
ms.topic: conceptual
ms.date: 06/03/2020
ms.custom: mlnet-tooling
ms.openlocfilehash: 833ee2ae54cf3a52adaf070837a33e00267d25dc
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599828"
---
# <a name="telemetry-collection-by-the-mlnet-cli"></a><span data-ttu-id="c9c60-104">依 ML.NET CLI 排列的遙測集合</span><span class="sxs-lookup"><span data-stu-id="c9c60-104">Telemetry collection by the ML.NET CLI</span></span>

<span data-ttu-id="c9c60-105">[ML.NET CLI](https://aka.ms/mlnet-cli) 包含遙測特性，會收集彙總供 Microsoft 使用的匿名使用資料。</span><span class="sxs-lookup"><span data-stu-id="c9c60-105">The [ML.NET CLI](https://aka.ms/mlnet-cli) includes a telemetry feature that collects anonymous usage data that is aggregated for use by Microsoft.</span></span>

## <a name="how-microsoft-uses-the-data"></a><span data-ttu-id="c9c60-106">Microsoft 如何使用資料</span><span class="sxs-lookup"><span data-stu-id="c9c60-106">How Microsoft uses the data</span></span>

<span data-ttu-id="c9c60-107">產品小組會使用 ML.NET CLI 遙測資料協助您了解如何改善工具。</span><span class="sxs-lookup"><span data-stu-id="c9c60-107">The product team uses ML.NET CLI telemetry data to help understand how to improve the tools.</span></span> <span data-ttu-id="c9c60-108">例如，如果客戶不常使用特定的機器學習工作，產品小組會調查原因並使用結果來排定特性開發的優先順序。</span><span class="sxs-lookup"><span data-stu-id="c9c60-108">For example, if customers infrequently use a particular machine learning task, the product team investigates why and uses findings to prioritize feature development.</span></span> <span data-ttu-id="c9c60-109">ML.NET CLI 遙測也可協助偵錯問題，例如當機和程式碼異常。</span><span class="sxs-lookup"><span data-stu-id="c9c60-109">ML.NET CLI telemetry also helps with debugging of issues such as crashes and code anomalies.</span></span>

<span data-ttu-id="c9c60-110">雖然產品小組感激此見解，但我們也知道不是所有人都願意傳送此資料。</span><span class="sxs-lookup"><span data-stu-id="c9c60-110">While the product team appreciates this insight, we also know that not everyone wants to send this data.</span></span> [<span data-ttu-id="c9c60-111">了解如何停用遙測。</span><span class="sxs-lookup"><span data-stu-id="c9c60-111">Find out how to disable telemetry.</span></span>](#opt-out-of-data-collection)

## <a name="scope"></a><span data-ttu-id="c9c60-112">影響範圍</span><span class="sxs-lookup"><span data-stu-id="c9c60-112">Scope</span></span>

<span data-ttu-id="c9c60-113">`mlnet` 命令會啟動 ML.NET CLI，但命令本身不會收集遙測。</span><span class="sxs-lookup"><span data-stu-id="c9c60-113">The `mlnet` command launches the ML.NET CLI, but the command itself doesn't collect telemetry.</span></span>

<span data-ttu-id="c9c60-114">當您執行 `mlnet` 命令不附加任何其他命令時，「不啟用」\*\* 遙測。</span><span class="sxs-lookup"><span data-stu-id="c9c60-114">Telemetry *isn't enabled* when you run the `mlnet` command with no other command attached.</span></span> <span data-ttu-id="c9c60-115">例如：</span><span class="sxs-lookup"><span data-stu-id="c9c60-115">For example:</span></span>

- `mlnet`
- `mlnet --help`

<span data-ttu-id="c9c60-116">當您執行 [ML.NET CLI 命令](../reference/ml-net-cli-reference.md)時，例如 `mlnet classification`，會「啟用」\*\* 遙測。</span><span class="sxs-lookup"><span data-stu-id="c9c60-116">Telemetry *is enabled* when you run an [ML.NET CLI command](../reference/ml-net-cli-reference.md), such as `mlnet classification`.</span></span>

## <a name="opt-out-of-data-collection"></a><span data-ttu-id="c9c60-117">選擇不使用資料收集</span><span class="sxs-lookup"><span data-stu-id="c9c60-117">Opt out of data collection</span></span>

<span data-ttu-id="c9c60-118">預設啟用 ML.NET CLI 遙測特性。</span><span class="sxs-lookup"><span data-stu-id="c9c60-118">The ML.NET CLI telemetry feature is enabled by default.</span></span>

<span data-ttu-id="c9c60-119">將 `MLDOTNET_CLI_TELEMETRY_OPTOUT` 環境變數設成 `1` 或 `true`，選擇退出遙測功能。</span><span class="sxs-lookup"><span data-stu-id="c9c60-119">Opt out of the telemetry feature by setting the `MLDOTNET_CLI_TELEMETRY_OPTOUT` environment variable to `1` or `true`.</span></span> <span data-ttu-id="c9c60-120">此環境變數會全域套用至 ML.NET CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="c9c60-120">This environment variable applies globally to the ML.NET CLI tool.</span></span>

## <a name="data-points-collected"></a><span data-ttu-id="c9c60-121">已收集資料點</span><span class="sxs-lookup"><span data-stu-id="c9c60-121">Data points collected</span></span>

<span data-ttu-id="c9c60-122">這個功能會收集下列資料︰</span><span class="sxs-lookup"><span data-stu-id="c9c60-122">The feature collects the following data:</span></span>

- <span data-ttu-id="c9c60-123">已叫用哪個命令，例如 `classification`</span><span class="sxs-lookup"><span data-stu-id="c9c60-123">What command was invoked, such as `classification`</span></span>
- <span data-ttu-id="c9c60-124">使用的命令列參數名稱（也就是「資料集、標籤欄、輸出路徑、訓練時間、詳細資訊」）</span><span class="sxs-lookup"><span data-stu-id="c9c60-124">Command-line parameter names used (that is, "dataset, label-col, output-path, train-time, verbosity")</span></span>
- <span data-ttu-id="c9c60-125">雜湊 MAC 位址：機器的密碼編譯 (SHA256) 匿名唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="c9c60-125">Hashed MAC address: a cryptographically (SHA256) anonymous and unique ID for a machine</span></span>
- <span data-ttu-id="c9c60-126">叫用的時間戳記</span><span class="sxs-lookup"><span data-stu-id="c9c60-126">Timestamp of an invocation</span></span>
- <span data-ttu-id="c9c60-127">僅用來判斷地理位置的三個八位元 IP 位址 (非完整 IP 位址)</span><span class="sxs-lookup"><span data-stu-id="c9c60-127">Three octet IP address (not full IP address) used only to determine geographical location</span></span>
- <span data-ttu-id="c9c60-128">所有使用的引數/參數名稱。</span><span class="sxs-lookup"><span data-stu-id="c9c60-128">Name of all arguments/parameters used.</span></span> <span data-ttu-id="c9c60-129">不是客戶的值，例如字串</span><span class="sxs-lookup"><span data-stu-id="c9c60-129">Not the customer's values, such as strings</span></span>
- <span data-ttu-id="c9c60-130">經雜湊處理的資料集檔案名稱</span><span class="sxs-lookup"><span data-stu-id="c9c60-130">Hashed dataset filename</span></span>
- <span data-ttu-id="c9c60-131">資料集檔案大小貯體</span><span class="sxs-lookup"><span data-stu-id="c9c60-131">Dataset file-size bucket</span></span>
- <span data-ttu-id="c9c60-132">作業系統和版本</span><span class="sxs-lookup"><span data-stu-id="c9c60-132">Operating system and version</span></span>
- <span data-ttu-id="c9c60-133">ML 工作命令的值：類別值，例如 `regression` 、 `classification` 和。`recommendation`</span><span class="sxs-lookup"><span data-stu-id="c9c60-133">Value of ML task commands: Categorical values, such as `regression`, `classification`, and `recommendation`</span></span>
- <span data-ttu-id="c9c60-134">ML.NET CLI 版本（也就是0.3.27703.4）</span><span class="sxs-lookup"><span data-stu-id="c9c60-134">ML.NET CLI version (that is, 0.3.27703.4)</span></span>

<span data-ttu-id="c9c60-135">資料會使用 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 技術安全傳送至 Microsoft 伺服器、保留在限制存取權下，並在安全 [Azure 儲存體](https://azure.microsoft.com/services/storage/)系統的嚴格安全性控制項下使用。</span><span class="sxs-lookup"><span data-stu-id="c9c60-135">The data is sent securely to Microsoft servers using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) technology, held under restricted access, and used under strict security controls from secure [Azure Storage](https://azure.microsoft.com/services/storage/) systems.</span></span>

### <a name="data-points-not-collected"></a><span data-ttu-id="c9c60-136">未收集資料點</span><span class="sxs-lookup"><span data-stu-id="c9c60-136">Data points not collected</span></span>

<span data-ttu-id="c9c60-137">遙測特性「不」\*\* 收集：</span><span class="sxs-lookup"><span data-stu-id="c9c60-137">The telemetry feature *doesn't* collect:</span></span>

- <span data-ttu-id="c9c60-138">個人資料，例如使用者姓名</span><span class="sxs-lookup"><span data-stu-id="c9c60-138">personal data, such as usernames</span></span>
- <span data-ttu-id="c9c60-139">資料集檔案名稱</span><span class="sxs-lookup"><span data-stu-id="c9c60-139">dataset filenames</span></span>
- <span data-ttu-id="c9c60-140">來自資料集檔案的資料</span><span class="sxs-lookup"><span data-stu-id="c9c60-140">data from dataset files</span></span>

<span data-ttu-id="c9c60-141">如果您懷疑 ML.NET CLI 遙測正在收集敏感性資料，或資料處理的方式不安全或不適當，請在 [ML.NET](https://github.com/dotnet/machinelearning) 存放庫中提出問題以供調查。</span><span class="sxs-lookup"><span data-stu-id="c9c60-141">If you suspect that the ML.NET CLI telemetry is collecting sensitive data or that the data is being insecurely or inappropriately handled, file an issue in the [ML.NET](https://github.com/dotnet/machinelearning) repository for investigation.</span></span>

## <a name="license"></a><span data-ttu-id="c9c60-142">授權</span><span class="sxs-lookup"><span data-stu-id="c9c60-142">License</span></span>

<span data-ttu-id="c9c60-143">Microsoft 的 ML.NET CLI 散發已獲得[Microsoft 軟體授權條款： microsoft .Net Library](https://aka.ms/dotnet-core-eula)。</span><span class="sxs-lookup"><span data-stu-id="c9c60-143">The Microsoft distribution of ML.NET CLI is licensed with the [Microsoft Software License Terms: Microsoft .NET Library](https://aka.ms/dotnet-core-eula).</span></span> <span data-ttu-id="c9c60-144">如需資料收集與處理的詳細資訊，請參閱＜資料＞一節。</span><span class="sxs-lookup"><span data-stu-id="c9c60-144">For details on data collection and processing, see the section entitled "Data."</span></span>

## <a name="disclosure"></a><span data-ttu-id="c9c60-145">公開</span><span class="sxs-lookup"><span data-stu-id="c9c60-145">Disclosure</span></span>

<span data-ttu-id="c9c60-146">當您第一次執行 [ML.NET CLI 命令](../reference/ml-net-cli-reference.md)時，例如 `mlnet classification`，ML.NET CLI 工具會顯示揭露文字，告訴您如何選擇退出遙測。</span><span class="sxs-lookup"><span data-stu-id="c9c60-146">When you first run a [ML.NET CLI command](../reference/ml-net-cli-reference.md) such as `mlnet classification`, the ML.NET CLI tool displays disclosure text that tells you how to opt out of telemetry.</span></span> <span data-ttu-id="c9c60-147">文字可能因您執行的 CLI 版本而略有不同。</span><span class="sxs-lookup"><span data-stu-id="c9c60-147">Text may vary slightly depending on the version of the CLI you're running.</span></span>

## <a name="see-also"></a><span data-ttu-id="c9c60-148">請參閱</span><span class="sxs-lookup"><span data-stu-id="c9c60-148">See also</span></span>

- [<span data-ttu-id="c9c60-149">ML.NET CLI 參考</span><span class="sxs-lookup"><span data-stu-id="c9c60-149">ML.NET CLI reference</span></span>](../reference/ml-net-cli-reference.md)
- [<span data-ttu-id="c9c60-150">Microsoft 軟體授權條款： Microsoft .NET 程式庫</span><span class="sxs-lookup"><span data-stu-id="c9c60-150">Microsoft Software License Terms: Microsoft .NET Library</span></span>](https://aka.ms/dotnet-core-eula)
- [<span data-ttu-id="c9c60-151">Microsoft 隱私權</span><span class="sxs-lookup"><span data-stu-id="c9c60-151">Privacy at Microsoft</span></span>](https://www.microsoft.com/trustcenter/privacy/)
- [<span data-ttu-id="c9c60-152">Microsoft 隱私權聲明</span><span class="sxs-lookup"><span data-stu-id="c9c60-152">Microsoft Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)

---
ms.openlocfilehash: 06f4186e8f233f5c769dfc5e05d2de5eacd9b053
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621950"
---
### <a name="svctraceviewer-combobox-high-contrast-change"></a><span data-ttu-id="eab5f-101">svcTraceViewer ComboBox 高對比變更</span><span class="sxs-lookup"><span data-stu-id="eab5f-101">svcTraceViewer ComboBox high contrast change</span></span>

#### <a name="details"></a><span data-ttu-id="eab5f-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="eab5f-102">Details</span></span>

<span data-ttu-id="eab5f-103">在 [Microsoft 服務追蹤檢視器工具](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中，某些高對比佈景主題的 ComboBox 控制項未顯示正確色彩。</span><span class="sxs-lookup"><span data-stu-id="eab5f-103">In the [Microsoft Service Trace Viewer tool](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), ComboBox controls were not displayed in the correct color in certain high contrast themes.</span></span> <span data-ttu-id="eab5f-104">此問題已在 .NET Framework 4.7.2 中修正。</span><span class="sxs-lookup"><span data-stu-id="eab5f-104">The issue was fixed in .NET Framework 4.7.2.</span></span> <span data-ttu-id="eab5f-105">不過，由於 .NET Framework SDK 的回溯相容性需求，因此預設為客戶看不到此項修正。</span><span class="sxs-lookup"><span data-stu-id="eab5f-105">However, due to .NET Framework SDK backward compatibility requirements, the fix was not visible to customers by default.</span></span> <span data-ttu-id="eab5f-106">.NET 4.8 將下列 [AppContext 組態參數](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)新增至 svcTraceViewer.exe.config 檔案，以呈現這項變更：</span><span class="sxs-lookup"><span data-stu-id="eab5f-106">.NET 4.8 surfaces this change by adding the following [AppContext configuration switches](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to the svcTraceViewer.exe.config file:</span></span><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>

#### <a name="suggestion"></a><span data-ttu-id="eab5f-107">建議</span><span class="sxs-lookup"><span data-stu-id="eab5f-107">Suggestion</span></span>

<ul><li><span data-ttu-id="eab5f-108">如果您不希望高對比行為變更，可從 svcTraceViewer.exe.config 檔案移除下列區段將其停用，以選擇退出變更：</span><span class="sxs-lookup"><span data-stu-id="eab5f-108">How to opt out of the change If you don't want to have the high contrast behavior change, you can disable it by removing the following section from the svcTraceViewer.exe.config file:</span></span></li></ul><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="eab5f-109">名稱</span><span class="sxs-lookup"><span data-stu-id="eab5f-109">Name</span></span>    | <span data-ttu-id="eab5f-110">值</span><span class="sxs-lookup"><span data-stu-id="eab5f-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="eab5f-111">影響範圍</span><span class="sxs-lookup"><span data-stu-id="eab5f-111">Scope</span></span>   |<span data-ttu-id="eab5f-112">Edge</span><span class="sxs-lookup"><span data-stu-id="eab5f-112">Edge</span></span>|
|<span data-ttu-id="eab5f-113">版本</span><span class="sxs-lookup"><span data-stu-id="eab5f-113">Version</span></span>|<span data-ttu-id="eab5f-114">4.8</span><span class="sxs-lookup"><span data-stu-id="eab5f-114">4.8</span></span>|
|<span data-ttu-id="eab5f-115">類型</span><span class="sxs-lookup"><span data-stu-id="eab5f-115">Type</span></span>|<span data-ttu-id="eab5f-116">執行階段</span><span class="sxs-lookup"><span data-stu-id="eab5f-116">Runtime</span></span>|

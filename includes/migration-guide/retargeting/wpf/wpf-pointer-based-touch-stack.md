---
ms.openlocfilehash: eb89cbc72d8b09fd1aa5bc775a6c539eb208fa70
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614404"
---
### <a name="wpf-pointer-based-touch-stack"></a><span data-ttu-id="fcf94-101">WPF 指標式觸控堆疊</span><span class="sxs-lookup"><span data-stu-id="fcf94-101">WPF Pointer-Based Touch Stack</span></span>

#### <a name="details"></a><span data-ttu-id="fcf94-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="fcf94-102">Details</span></span>

<span data-ttu-id="fcf94-103">這項變更將能夠啟用選用的 WM_POINTER 式 WPF 觸控/手寫筆堆疊。</span><span class="sxs-lookup"><span data-stu-id="fcf94-103">This change adds the ability to enable an optional WM_POINTER based WPF touch/stylus stack.</span></span>  <span data-ttu-id="fcf94-104">開發人員若未明確地啟用此項目，應該不會看到任何 WPF 觸控/手寫筆行為的變更。以下是選用之 WM_POINTER 式觸控/手寫筆堆疊的目前已知問題：</span><span class="sxs-lookup"><span data-stu-id="fcf94-104">Developers that do not explicitly enable this should see no change in WPF touch/stylus behavior.Current Known Issues With optional WM_POINTER based touch/stylus stack:</span></span>

- <span data-ttu-id="fcf94-105">不支援即時筆跡。</span><span class="sxs-lookup"><span data-stu-id="fcf94-105">No support for real-time inking.</span></span>
- <span data-ttu-id="fcf94-106">雖然筆跡和手寫筆外掛程式還能運作，但它們是在 UI 執行緒上處理，可能會導致效能不佳。</span><span class="sxs-lookup"><span data-stu-id="fcf94-106">While inking and StylusPlugins will still work, they will be processed on the UI Thread which can lead to poor performance.</span></span>
- <span data-ttu-id="fcf94-107">從觸控/手寫筆事件提升為滑鼠事件的變更，因而產生行為變更</span><span class="sxs-lookup"><span data-stu-id="fcf94-107">Behavioral changes due to changes in promotion from touch/stylus events to mouse events</span></span>
- <span data-ttu-id="fcf94-108">操作可能有不同的行為</span><span class="sxs-lookup"><span data-stu-id="fcf94-108">Manipulation may behave differently</span></span>
- <span data-ttu-id="fcf94-109">拖放動作無法對觸控輸入顯示適當的回應</span><span class="sxs-lookup"><span data-stu-id="fcf94-109">Drag/Drop will not show appropriate feedback for touch input</span></span>
- <span data-ttu-id="fcf94-110">這不影響手寫筆輸入</span><span class="sxs-lookup"><span data-stu-id="fcf94-110">This does not affect stylus input</span></span>
- <span data-ttu-id="fcf94-111">無法再針對觸控/手寫筆事件起始拖放動作</span><span class="sxs-lookup"><span data-stu-id="fcf94-111">Drag/Drop can no longer be initiated on touch/stylus events</span></span>
- <span data-ttu-id="fcf94-112">這可能會使應用程式停止回應到偵測到滑鼠輸入為止。</span><span class="sxs-lookup"><span data-stu-id="fcf94-112">This can potentially hang the application until mouse input is detected.</span></span>
- <span data-ttu-id="fcf94-113">開發人員應改為從滑鼠事件起始拖放動作。</span><span class="sxs-lookup"><span data-stu-id="fcf94-113">Instead, developers should initiate drag and drop from mouse events.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="fcf94-114">建議</span><span class="sxs-lookup"><span data-stu-id="fcf94-114">Suggestion</span></span>

<span data-ttu-id="fcf94-115">想要啟用此堆疊的開發人員可以將以下內容新增/合併至其應用程式的 App.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="fcf94-115">Developers who wish to enable this stack can add/merge the following to their application's App.config file:</span></span>

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Input.Stylus.EnablePointerSupport=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

<span data-ttu-id="fcf94-116">移除此項目或將其值設為 false 可關閉這個選用堆疊。請注意，此堆疊僅適用於 Windows 10 Creators Update 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="fcf94-116">Removing this or setting the value to false will turn this optional stack off.Note that this stack is available only on Windows 10 Creators Update and above.</span></span>

| <span data-ttu-id="fcf94-117">名稱</span><span class="sxs-lookup"><span data-stu-id="fcf94-117">Name</span></span>    | <span data-ttu-id="fcf94-118">值</span><span class="sxs-lookup"><span data-stu-id="fcf94-118">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="fcf94-119">影響範圍</span><span class="sxs-lookup"><span data-stu-id="fcf94-119">Scope</span></span>   | <span data-ttu-id="fcf94-120">Edge</span><span class="sxs-lookup"><span data-stu-id="fcf94-120">Edge</span></span>        |
| <span data-ttu-id="fcf94-121">版本</span><span class="sxs-lookup"><span data-stu-id="fcf94-121">Version</span></span> | <span data-ttu-id="fcf94-122">4.7</span><span class="sxs-lookup"><span data-stu-id="fcf94-122">4.7</span></span>         |
| <span data-ttu-id="fcf94-123">類型</span><span class="sxs-lookup"><span data-stu-id="fcf94-123">Type</span></span>    | <span data-ttu-id="fcf94-124">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="fcf94-124">Retargeting</span></span> |

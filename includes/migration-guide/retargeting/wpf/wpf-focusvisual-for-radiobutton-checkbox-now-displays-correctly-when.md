---
ms.openlocfilehash: 9e70bcd95393a7ff24de43577d26869ce674067b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614615"
---
### <a name="wpf-focusvisual-for-radiobutton-and-checkbox-now-displays-correctly-when-the-controls-have-no-content"></a><span data-ttu-id="9d9bf-101">現在，當控制項沒有內容時，RadioButton 和 CheckBox 的 WPF 焦點視覺效果會正確顯示</span><span class="sxs-lookup"><span data-stu-id="9d9bf-101">WPF FocusVisual for RadioButton and CheckBox Now Displays Correctly When The Controls Have No Content</span></span>

#### <a name="details"></a><span data-ttu-id="9d9bf-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="9d9bf-102">Details</span></span>

<span data-ttu-id="9d9bf-103">在 .NET Framework 4.7.1 和舊版的傳統和高對比佈景主題中，WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWithType> 和 <xref:System.Windows.Controls.RadioButton?displayProperty=nameWithType> 的焦點視覺效果不一致且不正確。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-103">In the .NET Framework 4.7.1 and earlier versions, WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWithType> and <xref:System.Windows.Controls.RadioButton?displayProperty=nameWithType> have inconsistent and, in Classic and High Contrast themes, incorrect focus visuals.</span></span>  <span data-ttu-id="9d9bf-104">當控制項沒有任何內容集時，會發生上述問題。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-104">These issues occur in cases where the controls do not have any content set.</span></span>  <span data-ttu-id="9d9bf-105">這可能會讓人混淆佈景主題之間的轉換，也看不清楚焦點視覺效果。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-105">This can make the transition between themes confusing and the focus visual hard to see.</span></span> <span data-ttu-id="9d9bf-106">現在，.NET Framework 4.7.2 的這些視覺效果在各佈景主題之間會更一致；在傳統和高對比佈景主題中也可以看得更清楚。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-106">In the .NET Framework 4.7.2, these visuals are now more consistent across themes and more easily visible in Classic and High Contrast themes.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="9d9bf-107">建議</span><span class="sxs-lookup"><span data-stu-id="9d9bf-107">Suggestion</span></span>

<span data-ttu-id="9d9bf-108">如果開發人員是以 .NET Framework 4.7.2 為目標，並想要還原為 .NET 4.7.1 的行為，則必須設定下列 AppContext 旗標。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-108">A developer targeting .NET Framework 4.7.2 that wants to revert to the behavior in .NET 4.7.1 will need to set the following AppContext flag.</span></span>

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures.2=true;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

<span data-ttu-id="9d9bf-109">如果開發人員想要利用這項變更，同時以 .NET 4.7.2 以下的 Framework 版本為目標，則必須設定下列 AppContext 旗標。請注意，所有旗標都必須正確設定，而且安裝的 .NET Framework 版本必須為 4.7.2 或更新版本。您必須具備 WPF 應用程式，才能選擇使用所有舊版的協助工具改進功能，並取得最新的改進功能。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-109">A developer who wants to utilize this change while targeting a framework version below .NET 4.7.2 must set the following AppContext flags.Note that all the flags must be set appropriately and the installed version of the .NET Framework must be 4.7.2 or greater.WPF applications are required to opt in to all earlier accessibility improvements to get the latest improvements.</span></span> <span data-ttu-id="9d9bf-110">若要這樣做，請確認 'Switch.UseLegacyAccessibilityFeatures' 和 'Switch.UseLegacyAccessibilityFeatures.2' 這兩個 AppContext 參數均設為 false。</span><span class="sxs-lookup"><span data-stu-id="9d9bf-110">To do this, ensure that both the AppContext switches 'Switch.UseLegacyAccessibilityFeatures' and 'Switch.UseLegacyAccessibilityFeatures.2' are set to false.</span></span>

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="9d9bf-111">名稱</span><span class="sxs-lookup"><span data-stu-id="9d9bf-111">Name</span></span>    | <span data-ttu-id="9d9bf-112">值</span><span class="sxs-lookup"><span data-stu-id="9d9bf-112">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="9d9bf-113">影響範圍</span><span class="sxs-lookup"><span data-stu-id="9d9bf-113">Scope</span></span>   | <span data-ttu-id="9d9bf-114">Edge</span><span class="sxs-lookup"><span data-stu-id="9d9bf-114">Edge</span></span>        |
| <span data-ttu-id="9d9bf-115">版本</span><span class="sxs-lookup"><span data-stu-id="9d9bf-115">Version</span></span> | <span data-ttu-id="9d9bf-116">4.7.2</span><span class="sxs-lookup"><span data-stu-id="9d9bf-116">4.7.2</span></span>       |
| <span data-ttu-id="9d9bf-117">類型</span><span class="sxs-lookup"><span data-stu-id="9d9bf-117">Type</span></span>    | <span data-ttu-id="9d9bf-118">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="9d9bf-118">Retargeting</span></span> |

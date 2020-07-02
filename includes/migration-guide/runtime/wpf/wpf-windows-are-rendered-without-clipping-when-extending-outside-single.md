---
ms.openlocfilehash: d276e2bbf24c8b2389a0a8078c62c327c3729d50
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621156"
---
### <a name="wpf-windows-are-rendered-without-clipping-when-extending-outside-a-single-monitor"></a><span data-ttu-id="01446-101">WPF 視窗在擴充到單一顯示器之外時呈現而不裁剪</span><span class="sxs-lookup"><span data-stu-id="01446-101">WPF windows are rendered without clipping when extending outside a single monitor</span></span>

#### <a name="details"></a><span data-ttu-id="01446-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="01446-102">Details</span></span>

<span data-ttu-id="01446-103">在 Windows 8 和更新版本中執行的 .NET Framework 4.6 多重監視器案例中，如果視窗擴充到單一顯示畫面之外，可呈現完整視窗而不會將其裁剪。</span><span class="sxs-lookup"><span data-stu-id="01446-103">In the .NET Framework 4.6 running on Windows 8 and above, the entire window is rendered without clipping when it extends outside of single display in a multi-monitor scenario.</span></span> <span data-ttu-id="01446-104">這與舊版 .NET Framework 不同，後者會在 WPF 視窗擴充到單一顯示畫面之外時裁剪該視窗。</span><span class="sxs-lookup"><span data-stu-id="01446-104">This is different from previous versions of the .NET Framework which would clip WPF windows that extended beyond a single display.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="01446-105">建議</span><span class="sxs-lookup"><span data-stu-id="01446-105">Suggestion</span></span>

<span data-ttu-id="01446-106">您可以在應用程式組態檔的 <code>&lt;appSettings&gt;</code> 中使用 <code>&lt;EnableMultiMonitorDisplayClipping&gt;</code> 項目，或在應用程式啟動時藉由設定 <code>EnableMultiMonitorDisplayClipping</code> 屬性，來明確設定這項行為 (不論是否裁剪)。</span><span class="sxs-lookup"><span data-stu-id="01446-106">This behavior (whether to clip or not) can be explicitly set using the <code>&lt;EnableMultiMonitorDisplayClipping&gt;</code> element in <code>&lt;appSettings&gt;</code> in an application's configuration file, or by setting the <code>EnableMultiMonitorDisplayClipping</code> property at app startup.</span></span>

| <span data-ttu-id="01446-107">名稱</span><span class="sxs-lookup"><span data-stu-id="01446-107">Name</span></span>    | <span data-ttu-id="01446-108">值</span><span class="sxs-lookup"><span data-stu-id="01446-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="01446-109">影響範圍</span><span class="sxs-lookup"><span data-stu-id="01446-109">Scope</span></span>   |<span data-ttu-id="01446-110">Minor</span><span class="sxs-lookup"><span data-stu-id="01446-110">Minor</span></span>|
|<span data-ttu-id="01446-111">版本</span><span class="sxs-lookup"><span data-stu-id="01446-111">Version</span></span>|<span data-ttu-id="01446-112">4.6</span><span class="sxs-lookup"><span data-stu-id="01446-112">4.6</span></span>|
|<span data-ttu-id="01446-113">類型</span><span class="sxs-lookup"><span data-stu-id="01446-113">Type</span></span>|<span data-ttu-id="01446-114">執行階段</span><span class="sxs-lookup"><span data-stu-id="01446-114">Runtime</span></span>|

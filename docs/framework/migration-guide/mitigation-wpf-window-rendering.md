---
title: 風險降低：WPF 視窗呈現
description: 瞭解在 Windows 8 或更新版本上執行的 .NET Framework 4.6 中，WPF 視窗呈現的影響和緩和。
ms.date: 03/30/2017
ms.assetid: 28ed6bf8-141b-4b73-a4e3-44a99fae5084
ms.openlocfilehash: d624478d17a4076107438f71b0a86eeb6d9f3ea4
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475329"
---
# <a name="mitigation-wpf-window-rendering"></a><span data-ttu-id="1c66a-103">風險降低：WPF 視窗呈現</span><span class="sxs-lookup"><span data-stu-id="1c66a-103">Mitigation: WPF Window Rendering</span></span>

<span data-ttu-id="1c66a-104">在 Windows 8 和更新版本中執行的 .NET Framework 4.6 多重監視器案例中，如果視窗擴充到單一顯示畫面之外，可呈現完整視窗而不會將其裁剪。</span><span class="sxs-lookup"><span data-stu-id="1c66a-104">In the .NET Framework 4.6 running on Windows 8 and above, the entire window is rendered without clipping when it extends outside of single display in a multi-monitor scenario.</span></span>

## <a name="impact"></a><span data-ttu-id="1c66a-105">影響</span><span class="sxs-lookup"><span data-stu-id="1c66a-105">Impact</span></span>

<span data-ttu-id="1c66a-106">一般而言，當跨多個監視器時，不裁剪而呈現整個視窗是預期的行為。</span><span class="sxs-lookup"><span data-stu-id="1c66a-106">In general, rendering an entire window across multiple monitors without clipping is the expected behavior.</span></span> <span data-ttu-id="1c66a-107">不過，在 Windows 7 和舊版中，如果 WPF 視窗超過單一顯示畫面，會將其裁剪，主要是因為要在第二個監視器呈現部分視窗時，會造成顯著的效能影響。</span><span class="sxs-lookup"><span data-stu-id="1c66a-107">However, on Windows 7 and earlier versions, WPF windows are clipped when they extend beyond a single display because rendering a portion of the window on the second monitor has a significant performance impact.</span></span>

<span data-ttu-id="1c66a-108">在 Windows 8 和更新版本中，跨監視器呈現 WPF 視窗的影響涉及太多因素，因此無法精確量化。</span><span class="sxs-lookup"><span data-stu-id="1c66a-108">The precise impact of rendering WPF windows across monitors on Windows 8 and above is not precisely quantifiable since it depends on a large number of factors.</span></span> <span data-ttu-id="1c66a-109">在某些情況下，它仍可能會產生不良的效能影響，特別是針對執行使用大量圖形的應用程式並有跨監視器顯示視窗的使用者來說，更是明顯。</span><span class="sxs-lookup"><span data-stu-id="1c66a-109">In some cases, it may still produce an undesirable impact on performance, particularly for users who run graphics-intensive applications and have windows straddling monitors.</span></span> <span data-ttu-id="1c66a-110">在其他情況下，您可能只需要 .NET Framework 版本之間保持一致的行為。</span><span class="sxs-lookup"><span data-stu-id="1c66a-110">In other cases, you may simply want a consistent behavior across .NET Framework versions.</span></span>

## <a name="mitigation"></a><span data-ttu-id="1c66a-111">降低</span><span class="sxs-lookup"><span data-stu-id="1c66a-111">Mitigation</span></span>

<span data-ttu-id="1c66a-112">您可以停用這項變更並還原為先前的行為，即可在超出單一顯示畫面時裁剪 WPF 視窗。</span><span class="sxs-lookup"><span data-stu-id="1c66a-112">You can disable this change and revert to the previous behavior of clipping a WPF window when it extends beyond a single display.</span></span> <span data-ttu-id="1c66a-113">作法有二：</span><span class="sxs-lookup"><span data-stu-id="1c66a-113">There are two ways to do this:</span></span>

- <span data-ttu-id="1c66a-114">您可將 `<EnableMultiMonitorDisplayClipping>` 項目加入應用程式組態檔的 `<appSettings>` 區段，以針對在 Windows 8 或更新版本中執行的應用程式停用或啟用此行為。</span><span class="sxs-lookup"><span data-stu-id="1c66a-114">By adding the `<EnableMultiMonitorDisplayClipping>` element to the `<appSettings>` section of your application configuration file, you can disable or enable this behavior on apps running on Windows 8 or later.</span></span> <span data-ttu-id="1c66a-115">例如，下列組態區段會停用呈現時不裁剪的行為：</span><span class="sxs-lookup"><span data-stu-id="1c66a-115">For example, the following configuration section disables rendering without clipping:</span></span>

  ```xml
  <appSettings>
      <add key="EnableMultiMonitorDisplayClipping" value="true"/>
    </appSettings>
  ```

  <span data-ttu-id="1c66a-116">`<EnableMultiMonitorDisplayClipping>` 組態設定可以為下列兩個值之一：</span><span class="sxs-lookup"><span data-stu-id="1c66a-116">The `<EnableMultiMonitorDisplayClipping>` configuration setting can have either of two values:</span></span>

  - <span data-ttu-id="1c66a-117">若要在呈現期間，啟用將視窗裁剪至監視器界限的行為，即為 `true`。</span><span class="sxs-lookup"><span data-stu-id="1c66a-117">`true`, to enable clipping of windows to monitor bounds during rendering.</span></span>

  - <span data-ttu-id="1c66a-118">若要在呈現期間，停用將視窗裁剪至監視器界限的行為，即為 `false`。</span><span class="sxs-lookup"><span data-stu-id="1c66a-118">`false`, to disable clipping of windows to monitor bounds during rendering.</span></span>

- <span data-ttu-id="1c66a-119">方法是在應用程式啟動時，將 <xref:System.Windows.CoreCompatibilityPreferences.EnableMultiMonitorDisplayClipping%2A> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="1c66a-119">By setting the <xref:System.Windows.CoreCompatibilityPreferences.EnableMultiMonitorDisplayClipping%2A> property to `true` at app startup.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c66a-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1c66a-120">See also</span></span>

- [<span data-ttu-id="1c66a-121">應用程式相容性</span><span class="sxs-lookup"><span data-stu-id="1c66a-121">Application compatibility</span></span>](application-compatibility.md)

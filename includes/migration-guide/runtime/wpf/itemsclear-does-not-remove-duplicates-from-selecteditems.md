---
ms.openlocfilehash: 75f176133697056bab9349ba1d18d7a0e1aa7da2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619814"
---
### <a name="itemsclear-does-not-remove-duplicates-from-selecteditems"></a><span data-ttu-id="77d67-101">Items.Clear 不會從 SelectedItems 移除重複項目</span><span class="sxs-lookup"><span data-stu-id="77d67-101">Items.Clear does not remove duplicates from SelectedItems</span></span>

#### <a name="details"></a><span data-ttu-id="77d67-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="77d67-102">Details</span></span>

<span data-ttu-id="77d67-103">假設選取器 (啟用了多個選取項目) 在其 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 集合中有重複項目 - 相同的項目出現一次以上。</span><span class="sxs-lookup"><span data-stu-id="77d67-103">Suppose a Selector (with multiple selection enabled) has duplicates in its <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> collection - the same item appears more than once.</span></span>  <span data-ttu-id="77d67-104">從資料來源移除這些項目 (例如，藉由呼叫 Items.Clear) 無法從 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 中加以移除；只會移除第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="77d67-104">Removing those items from the data source (e.g. by calling Items.Clear) fails to remove them from <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName>; only the first instance is removed.</span></span> <span data-ttu-id="77d67-105">此外，後續使用 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> (例如 SelectedItems.Clear()) 可能會發生像是 <xref:System.ArgumentException?displayProperty=fullName> 的問題，因為 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 包含已不在資料來源中的項目。</span><span class="sxs-lookup"><span data-stu-id="77d67-105">Furthermore, subsequent use of <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> (e.g. SelectedItems.Clear()) can encounter problems such as <xref:System.ArgumentException?displayProperty=fullName>, because <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> contains items that are no longer in the data source.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="77d67-106">建議</span><span class="sxs-lookup"><span data-stu-id="77d67-106">Suggestion</span></span>

<span data-ttu-id="77d67-107">如有可能，請升級至 .NET Framework 4.6.2。</span><span class="sxs-lookup"><span data-stu-id="77d67-107">Upgrade if possible to .NET Framework 4.6.2.</span></span>

| <span data-ttu-id="77d67-108">名稱</span><span class="sxs-lookup"><span data-stu-id="77d67-108">Name</span></span>    | <span data-ttu-id="77d67-109">值</span><span class="sxs-lookup"><span data-stu-id="77d67-109">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="77d67-110">影響範圍</span><span class="sxs-lookup"><span data-stu-id="77d67-110">Scope</span></span>   |<span data-ttu-id="77d67-111">Minor</span><span class="sxs-lookup"><span data-stu-id="77d67-111">Minor</span></span>|
|<span data-ttu-id="77d67-112">版本</span><span class="sxs-lookup"><span data-stu-id="77d67-112">Version</span></span>|<span data-ttu-id="77d67-113">4.5</span><span class="sxs-lookup"><span data-stu-id="77d67-113">4.5</span></span>|
|<span data-ttu-id="77d67-114">類型</span><span class="sxs-lookup"><span data-stu-id="77d67-114">Type</span></span>|<span data-ttu-id="77d67-115">執行階段</span><span class="sxs-lookup"><span data-stu-id="77d67-115">Runtime</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="77d67-116">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="77d67-116">Affected APIs</span></span>

-<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=nameWithType></li></ul>|

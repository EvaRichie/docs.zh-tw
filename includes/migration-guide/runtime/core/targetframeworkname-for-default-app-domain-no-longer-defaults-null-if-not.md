---
ms.openlocfilehash: f955e270f709ddf6eea2e44bbcf386e372b9f6e3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621137"
---
### <a name="targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a><span data-ttu-id="046af-101">預設應用程式定義域的 TargetFrameworkName 若未設定，不會再預設為 Null</span><span class="sxs-lookup"><span data-stu-id="046af-101">TargetFrameworkName for default app domain no longer defaults to null if not set</span></span>

#### <a name="details"></a><span data-ttu-id="046af-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="046af-102">Details</span></span>

<span data-ttu-id="046af-103">除非明確設定，否則 <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> 之前在預設應用程式定義域中為 Null。</span><span class="sxs-lookup"><span data-stu-id="046af-103">The <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> was previously null in the default app domain, unless it was explicitly set.</span></span> <span data-ttu-id="046af-104">從 4.6 開始，預設應用程式定義域的 <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> 屬性會有衍生自 TargetFrameworkAttribute 的預設值 (如果有一個預設值的話)。</span><span class="sxs-lookup"><span data-stu-id="046af-104">Beginning in 4.6, the <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> property for the default app domain will have a default value derived from the TargetFrameworkAttribute (if one is present).</span></span> <span data-ttu-id="046af-105">除非明確遭到覆寫，否則非預設應用程式定義域會繼續從預設應用程式定義域繼承其 <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> (在 4.6 中不會預設為 Null)。</span><span class="sxs-lookup"><span data-stu-id="046af-105">Non-default app domains will continue to inherit their <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> from the default app domain (which will not default to null in 4.6) unless it is explicitly overridden.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="046af-106">建議</span><span class="sxs-lookup"><span data-stu-id="046af-106">Suggestion</span></span>

<span data-ttu-id="046af-107">您應該更新程式碼，讓 <xref:System.AppDomainSetup.TargetFrameworkName> 不會預設為 Null。</span><span class="sxs-lookup"><span data-stu-id="046af-107">Code should be updated to not depend on <xref:System.AppDomainSetup.TargetFrameworkName> defaulting to null.</span></span> <span data-ttu-id="046af-108">如果此屬性必須繼續評估為 Null，則可以將它明確設定為該值。</span><span class="sxs-lookup"><span data-stu-id="046af-108">If it is required that this property continue to evaluate to null, it can be explicitly set to that value.</span></span>

| <span data-ttu-id="046af-109">名稱</span><span class="sxs-lookup"><span data-stu-id="046af-109">Name</span></span>    | <span data-ttu-id="046af-110">值</span><span class="sxs-lookup"><span data-stu-id="046af-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="046af-111">影響範圍</span><span class="sxs-lookup"><span data-stu-id="046af-111">Scope</span></span>   |<span data-ttu-id="046af-112">Edge</span><span class="sxs-lookup"><span data-stu-id="046af-112">Edge</span></span>|
|<span data-ttu-id="046af-113">版本</span><span class="sxs-lookup"><span data-stu-id="046af-113">Version</span></span>|<span data-ttu-id="046af-114">4.6</span><span class="sxs-lookup"><span data-stu-id="046af-114">4.6</span></span>|
|<span data-ttu-id="046af-115">類型</span><span class="sxs-lookup"><span data-stu-id="046af-115">Type</span></span>|<span data-ttu-id="046af-116">執行階段</span><span class="sxs-lookup"><span data-stu-id="046af-116">Runtime</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="046af-117">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="046af-117">Affected APIs</span></span>

-<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=nameWithType></li></ul>|

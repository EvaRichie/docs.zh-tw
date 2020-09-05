---
ms.openlocfilehash: 0d38e2177377e7e9ea911071eb65aa13aa1f5900
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497477"
---
### <a name="dataannotationsdatatypeattributedisableregex-app-setting-is-on-by-default-in-net-framework-472"></a><span data-ttu-id="1665a-101">"dataAnnotations:dataTypeAttribute:disableRegEx" 應用程式設定，在 .NET Framework 4.7.2 中預設會開啟</span><span class="sxs-lookup"><span data-stu-id="1665a-101">"dataAnnotations:dataTypeAttribute:disableRegEx" app setting is on by default in .NET Framework 4.7.2</span></span>

#### <a name="details"></a><span data-ttu-id="1665a-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1665a-102">Details</span></span>

<span data-ttu-id="1665a-103">在 .NET Framework 4.6.1 中，提供了應用程式設定 (<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code>)，可讓使用者能停用在資料類型屬性 (例如 <xref:System.ComponentModel.DataAnnotations.EmailAddressAttribute?displayProperty=nameWithType>、<xref:System.ComponentModel.DataAnnotations.UrlAttribute?displayProperty=nameWithType> 及 <xref:System.ComponentModel.DataAnnotations.PhoneAttribute?displayProperty=nameWithType>) 中使用規則運算式。</span><span class="sxs-lookup"><span data-stu-id="1665a-103">In .NET Framework 4.6.1, an app setting (<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code>) was introduced that allows users to disable the use of regular expressions in data type attributes (such as <xref:System.ComponentModel.DataAnnotations.EmailAddressAttribute?displayProperty=nameWithType>, <xref:System.ComponentModel.DataAnnotations.UrlAttribute?displayProperty=nameWithType>, and <xref:System.ComponentModel.DataAnnotations.PhoneAttribute?displayProperty=nameWithType>).</span></span> <span data-ttu-id="1665a-104">如此有助於降低安全性弱點，例如避免發生使用特定規則運算式的拒絕服務攻擊之可能性。</span><span class="sxs-lookup"><span data-stu-id="1665a-104">This helps to reduce security vulnerability such as avoiding the possibility of a Denial of Service attack using specific regular expressions.</span></span><br/><span data-ttu-id="1665a-105">在 .NET Framework 4.6.1 中，停用使用 RegEx 的此應用程式設定，預設會設為 <code>false</code>。</span><span class="sxs-lookup"><span data-stu-id="1665a-105">In .NET Framework 4.6.1, this app setting to disable RegEx usage was set to <code>false</code> by default.</span></span> <span data-ttu-id="1665a-106">從 .NET Framework 4.7.2 開始，此設定參數預設會設定為， <code>true</code> 以進一步降低以 .NET Framework 4.7.2 和更新版本為目標之 web 應用程式的安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="1665a-106">Starting with .NET Framework 4.7.2, this config switch is set to <code>true</code> by default to further reduce secure vulnerability for web applications that target .NET Framework 4.7.2 and above.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="1665a-107">建議</span><span class="sxs-lookup"><span data-stu-id="1665a-107">Suggestion</span></span>

<span data-ttu-id="1665a-108">若您發現您 Web 應用程式中的規則運算式，在升級至 .NET Framework 4.7.2 之後無法運作，可將 <code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code> 設定的值，更新為 <code>false</code>，以還原為先前的行為。</span><span class="sxs-lookup"><span data-stu-id="1665a-108">If you find that regular expressions in your web application do not work after upgrading to .NET Framework 4.7.2, you can update the value of the <code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code> setting to <code>false</code> to revert to the previous behavior.</span></span><pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot; value=&quot;false&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="1665a-109">名稱</span><span class="sxs-lookup"><span data-stu-id="1665a-109">Name</span></span>    | <span data-ttu-id="1665a-110">值</span><span class="sxs-lookup"><span data-stu-id="1665a-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="1665a-111">範圍</span><span class="sxs-lookup"><span data-stu-id="1665a-111">Scope</span></span>   |<span data-ttu-id="1665a-112">Minor</span><span class="sxs-lookup"><span data-stu-id="1665a-112">Minor</span></span>|
|<span data-ttu-id="1665a-113">版本</span><span class="sxs-lookup"><span data-stu-id="1665a-113">Version</span></span>|<span data-ttu-id="1665a-114">4.7.2</span><span class="sxs-lookup"><span data-stu-id="1665a-114">4.7.2</span></span>|
|<span data-ttu-id="1665a-115">類型</span><span class="sxs-lookup"><span data-stu-id="1665a-115">Type</span></span>|<span data-ttu-id="1665a-116">執行階段</span><span class="sxs-lookup"><span data-stu-id="1665a-116">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="1665a-117">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="1665a-117">Affected APIs</span></span>

<span data-ttu-id="1665a-118">無法透過 API 分析偵測。</span><span class="sxs-lookup"><span data-stu-id="1665a-118">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->

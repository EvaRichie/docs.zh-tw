---
ms.openlocfilehash: c8f017084fc1ec1eca636ef0178a40559e15b2c5
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497844"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a><span data-ttu-id="9a4ee-101">針對 Net.Tcp 憑證驗證改善的 WCF 鏈結信任憑證驗證</span><span class="sxs-lookup"><span data-stu-id="9a4ee-101">Improved WCF chain trust certificate validation for Net.Tcp certificate authentication</span></span>

#### <a name="details"></a><span data-ttu-id="9a4ee-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="9a4ee-102">Details</span></span>

<span data-ttu-id="9a4ee-103">.NET Framework 4.7.2 若以傳輸安全性搭配 WCF 使用憑證驗證，就可以改善鏈結信任憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-103">.NET Framework 4.7.2 improves chain trust certificate validation when using certificate authentication with transport security with WCF.</span></span> <span data-ttu-id="9a4ee-104">利用這項改善，必須針對用戶端驗證設定用來驗證伺服器的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-104">With this improvement, client certificates that are used to authenticate to a server must be configured for client authentication.</span></span>  <span data-ttu-id="9a4ee-105">同樣地，必須針對伺服器驗證設定用來驗證伺服器的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-105">Similarly server certificates that are for the authenticating a server must be configured for server authentication.</span></span> <span data-ttu-id="9a4ee-106">利用這項變更，如果已停用根憑證，憑證鏈結驗證就會失敗。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-106">With this change, if the root certificate is disabled, the certificate chain validation fails.</span></span> <span data-ttu-id="9a4ee-107">同時，已透過 Windows 安全性彙總對 .NET Framework 3.5 和更新版本進行了相同的變更。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-107">The same change was also made to .NET Framework 3.5 and later versions via Windows security roll-up.</span></span> <span data-ttu-id="9a4ee-108">您可以在[這裡](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7)找到更多資訊。這項變更預設為開啟，而且可以透過組態設定加以關閉。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-108">You can find more information [here](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7).This change is on by default and can be turned off by a configuration setting.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="9a4ee-109">建議</span><span class="sxs-lookup"><span data-stu-id="9a4ee-109">Suggestion</span></span>

<ul><li><span data-ttu-id="9a4ee-110">驗證您的伺服器和用戶端憑證是否具有必要的 EKU OID。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-110">Validate if your server and client certification has the required EKU OID.</span></span> <span data-ttu-id="9a4ee-111">如果沒有，請更新您的憑證。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-111">If not, update your certification.</span></span></li><li><span data-ttu-id="9a4ee-112">驗證您的根憑證是否無效。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-112">Validate if your root certificate is invalid.</span></span> <span data-ttu-id="9a4ee-113">如果是，請更新根憑證。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-113">If so, update the root certificate.</span></span></li><li><span data-ttu-id="9a4ee-114">如何選擇退出變更：如果無法更新憑證，您可以使用下列組態設定暫時解決這項重大變更，不過，選擇退出此變更會使您的系統容易受到安全性問題影響。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-114">How to opt out of the change: If you can't update the certificate, you can work around the breaking change temporarily with the following configration setting,  However, opting out of the change will leave your system vulnerable to the security issue.</span></span></li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="9a4ee-115">名稱</span><span class="sxs-lookup"><span data-stu-id="9a4ee-115">Name</span></span>    | <span data-ttu-id="9a4ee-116">值</span><span class="sxs-lookup"><span data-stu-id="9a4ee-116">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="9a4ee-117">範圍</span><span class="sxs-lookup"><span data-stu-id="9a4ee-117">Scope</span></span>   |<span data-ttu-id="9a4ee-118">Minor</span><span class="sxs-lookup"><span data-stu-id="9a4ee-118">Minor</span></span>|
|<span data-ttu-id="9a4ee-119">版本</span><span class="sxs-lookup"><span data-stu-id="9a4ee-119">Version</span></span>|<span data-ttu-id="9a4ee-120">4.7.2</span><span class="sxs-lookup"><span data-stu-id="9a4ee-120">4.7.2</span></span>|
|<span data-ttu-id="9a4ee-121">類型</span><span class="sxs-lookup"><span data-stu-id="9a4ee-121">Type</span></span>|<span data-ttu-id="9a4ee-122">執行階段</span><span class="sxs-lookup"><span data-stu-id="9a4ee-122">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="9a4ee-123">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="9a4ee-123">Affected APIs</span></span>

<span data-ttu-id="9a4ee-124">無法透過 API 分析偵測。</span><span class="sxs-lookup"><span data-stu-id="9a4ee-124">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->

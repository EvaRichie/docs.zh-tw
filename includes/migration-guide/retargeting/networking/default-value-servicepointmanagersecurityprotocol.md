---
ms.openlocfilehash: 5c86be598ab6196ecf4da05451c7f22d2be52c12
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614344"
---
### <a name="default-value-of-servicepointmanagersecurityprotocol-is-securityprotocoltypesystemdefault"></a><span data-ttu-id="9bff4-101">ServicePointManager.SecurityProtocol 的預設值是 SecurityProtocolType.System.Default</span><span class="sxs-lookup"><span data-stu-id="9bff4-101">Default value of ServicePointManager.SecurityProtocol is SecurityProtocolType.System.Default</span></span>

#### <a name="details"></a><span data-ttu-id="9bff4-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="9bff4-102">Details</span></span>

<span data-ttu-id="9bff4-103">從以 .NET Framework 4.7 為目標的應用程式開始，<xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> 屬性是 <xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="9bff4-103">Starting with apps that target the .NET Framework 4.7, the default value of the <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> property is <xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType>.</span></span> <span data-ttu-id="9bff4-104">這項變更可以讓以 SslStream 為基礎的 .NET Framework 網路 API (例如 FTP、HTTPS 及 SMTP) 繼承作業系統的預設安全性通訊協定，而不要使用由 .NET Framework 定義的硬式編碼值。</span><span class="sxs-lookup"><span data-stu-id="9bff4-104">This change allows .NET Framework networking APIs based on SslStream (such as FTP, HTTPS, and SMTP) to inherit the default security protocols from the operating system instead of using hard-coded values defined by the .NET Framework.</span></span> <span data-ttu-id="9bff4-105">預設值會依作業系統和系統管理員執行的任何自訂設定而異。</span><span class="sxs-lookup"><span data-stu-id="9bff4-105">The default varies by operating system and any custom configuration performed by the system administrator.</span></span> <span data-ttu-id="9bff4-106">如需每個 Windows 作業系統版本中預設 SChannel 通訊協定的資訊，請參閱 [Protocols in TLS/SSL (Schannel SSP)](https://docs.microsoft.com/windows/desktop/SecAuthN/protocols-in-tls-ssl--schannel-ssp-) (TLS/SSL 中的通訊協定 (Schannel SSP))。</span><span class="sxs-lookup"><span data-stu-id="9bff4-106">For information on the default SChannel protocol in each version of the Windows operating system, see [Protocols in TLS/SSL (Schannel SSP)](https://docs.microsoft.com/windows/desktop/SecAuthN/protocols-in-tls-ssl--schannel-ssp-).</span></span></p><span data-ttu-id="9bff4-107">目標是舊版 .NET Framework 的應用程式，<xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> 屬性的預設值視目標的 .NET framework 版本而定。</span><span class="sxs-lookup"><span data-stu-id="9bff4-107">For applications that target an earlier version of the .NET Framework, the default value of the <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> property depends on the version of the .NET Framework targeted.</span></span> <span data-ttu-id="9bff4-108">如需詳細資訊，請參閱[從 .NET Framework 4.5.2 移轉到 4.6 的重定目標變更的網路區段](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#networking)。</span><span class="sxs-lookup"><span data-stu-id="9bff4-108">See the [Networking section of Retargeting Changes for Migration from .NET Framework 4.5.2 to 4.6](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#networking) for more information.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="9bff4-109">建議</span><span class="sxs-lookup"><span data-stu-id="9bff4-109">Suggestion</span></span>

<span data-ttu-id="9bff4-110">這項變更會影響目標為 .NET Framework 4.7 或更新版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bff4-110">This change affects applications that target the .NET Framework 4.7 or later versions.</span></span> <span data-ttu-id="9bff4-111">如果您偏好使用定義的通訊協定，而不是依賴系統預設，您可以明確設定 <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="9bff4-111">If you prefer to use a defined protocol rather than relying on the system default, you can explicitly set the value of the <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="9bff4-112">如果不需要這項變更，您可以新增設定至 [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 應用程式佈建檔的區段，以退出宣告。</span><span class="sxs-lookup"><span data-stu-id="9bff4-112">If this change is undesirable, you can opt out of it by adding a configuration setting to the [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) section of your application configuration file.</span></span> <span data-ttu-id="9bff4-113">下列範例顯示 `<runtime>` 區段及 `Switch.System.Net.DontEnableSystemDefaultTlsVersions` 選擇退出參數：</span><span class="sxs-lookup"><span data-stu-id="9bff4-113">The following example shows both the `<runtime>` section and the `Switch.System.Net.DontEnableSystemDefaultTlsVersions` opt-out switch:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSystemDefaultTlsVersions=true" />
</runtime>
```

| <span data-ttu-id="9bff4-114">名稱</span><span class="sxs-lookup"><span data-stu-id="9bff4-114">Name</span></span>    | <span data-ttu-id="9bff4-115">值</span><span class="sxs-lookup"><span data-stu-id="9bff4-115">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="9bff4-116">影響範圍</span><span class="sxs-lookup"><span data-stu-id="9bff4-116">Scope</span></span>   | <span data-ttu-id="9bff4-117">Minor</span><span class="sxs-lookup"><span data-stu-id="9bff4-117">Minor</span></span>       |
| <span data-ttu-id="9bff4-118">版本</span><span class="sxs-lookup"><span data-stu-id="9bff4-118">Version</span></span> | <span data-ttu-id="9bff4-119">4.7</span><span class="sxs-lookup"><span data-stu-id="9bff4-119">4.7</span></span>         |
| <span data-ttu-id="9bff4-120">類型</span><span class="sxs-lookup"><span data-stu-id="9bff4-120">Type</span></span>    | <span data-ttu-id="9bff4-121">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="9bff4-121">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="9bff4-122">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="9bff4-122">Affected APIs</span></span>

- <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType>

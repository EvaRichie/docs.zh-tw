---
ms.openlocfilehash: c646372104457e8bc5d418744847f3ee771c8d8b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614377"
---
### <a name="wcf-message-security-now-is-able-to-use-tls11-and-tls12"></a><span data-ttu-id="b2a01-101">WCF 訊息安全性現在能夠使用 TLS1.1 和 TLS1.2</span><span class="sxs-lookup"><span data-stu-id="b2a01-101">WCF message security now is able to use TLS1.1 and TLS1.2</span></span>

#### <a name="details"></a><span data-ttu-id="b2a01-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b2a01-102">Details</span></span>

<span data-ttu-id="b2a01-103">從 .NET Framework 4.7 開始，除了 SSL3.0 和 TLS1.0 之外，客戶還可以透過應用程式組態設定，在 WCF 訊息安全性設定 TLS1.1 或 TLS1.2。</span><span class="sxs-lookup"><span data-stu-id="b2a01-103">Starting in the .NET Framework 4.7, customers can configure either TLS1.1 or TLS1.2 in WCF message security in addition to SSL3.0 and TLS1.0 through application configuration settings.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="b2a01-104">建議</span><span class="sxs-lookup"><span data-stu-id="b2a01-104">Suggestion</span></span>

<span data-ttu-id="b2a01-105">在 .NET Framework 4.7 中，預設會停用 WCF 訊息安全性中的 TLS1.1 和 TLS1.2 支援。</span><span class="sxs-lookup"><span data-stu-id="b2a01-105">In the .NET Framework 4.7, support for TLS1.1 and TLS1.2 in WCF message security is disabled by default.</span></span> <span data-ttu-id="b2a01-106">您可以將下行新增到 app.config 或 web.config 檔案的 `<runtime>` 區段來啟用它：</span><span class="sxs-lookup"><span data-stu-id="b2a01-106">You can enable it by adding the following line to the `<runtime>` section of the app.config or web.config file:</span></span>

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
</runtime>
```

| <span data-ttu-id="b2a01-107">名稱</span><span class="sxs-lookup"><span data-stu-id="b2a01-107">Name</span></span>    | <span data-ttu-id="b2a01-108">值</span><span class="sxs-lookup"><span data-stu-id="b2a01-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="b2a01-109">影響範圍</span><span class="sxs-lookup"><span data-stu-id="b2a01-109">Scope</span></span>   | <span data-ttu-id="b2a01-110">Edge</span><span class="sxs-lookup"><span data-stu-id="b2a01-110">Edge</span></span>        |
| <span data-ttu-id="b2a01-111">版本</span><span class="sxs-lookup"><span data-stu-id="b2a01-111">Version</span></span> | <span data-ttu-id="b2a01-112">4.7</span><span class="sxs-lookup"><span data-stu-id="b2a01-112">4.7</span></span>         |
| <span data-ttu-id="b2a01-113">類型</span><span class="sxs-lookup"><span data-stu-id="b2a01-113">Type</span></span>    | <span data-ttu-id="b2a01-114">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="b2a01-114">Retargeting</span></span> |

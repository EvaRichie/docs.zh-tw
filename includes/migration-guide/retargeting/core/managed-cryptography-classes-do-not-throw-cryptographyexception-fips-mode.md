---
ms.openlocfilehash: 0b62eff8d70873293aafa539f40bf032672df57a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617793"
---
### <a name="managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode"></a><span data-ttu-id="6de92-101">受控加密類別在 FIPS 模式中不會擲回 CryptographyException</span><span class="sxs-lookup"><span data-stu-id="6de92-101">Managed cryptography classes do not throw a CryptographyException in FIPS mode</span></span>

#### <a name="details"></a><span data-ttu-id="6de92-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="6de92-102">Details</span></span>

<span data-ttu-id="6de92-103">在舊版 .NET Framework 4.7.2 及更早版本中，受控加密提供者類別 (例如 <xref:System.Security.Cryptography.SHA256Managed>) 會在系統密碼編譯程式庫以 FIPS 模式設定時擲回 <xref:System.Security.Cryptography.CryptographicException>。</span><span class="sxs-lookup"><span data-stu-id="6de92-103">In .NET Framework 4.7.2 and earlier versions, managed cryptographic provider classes such as <xref:System.Security.Cryptography.SHA256Managed> throw a <xref:System.Security.Cryptography.CryptographicException> when the system cryptographic libraries are configured in FIPS mode.</span></span> <span data-ttu-id="6de92-104">因為受控版本未經過 FIPS (聯邦資訊處理標準) 140-2 認證，並封鎖可能不受 FIPS 規則核准的加密演算法，因此會擲回這些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6de92-104">These exceptions are thrown because the managed versions have not undergone FIPS (Federal Information Processing Standards) 140-2 certification, as well as to block cryptographic algorithms that were not considered to be approved based on the FIPS rules.</span></span>  <span data-ttu-id="6de92-105">因為只有極少數開發人員以 FIP 模式使用開發電腦，因此這些例外狀況通常僅在生產系統上擲回。以 .NET Framework 4.8 及更新版本為目標的應用程式，會自動切換至較新且寬鬆的原則，以便不再於此情況下根據預設擲回 <xref:System.Security.Cryptography.CryptographicException>。</span><span class="sxs-lookup"><span data-stu-id="6de92-105">Because few developers have their development machines in FIPS mode, these exceptions are frequently thrown only on production systems.Applications that target .NET Framework 4.8 and later versions automatically switch to the newer, relaxed policy, so that a <xref:System.Security.Cryptography.CryptographicException> is no longer thrown by default in such cases.</span></span> <span data-ttu-id="6de92-106">相反地，這些受控加密類別會將加密作業重新導向到系統加密程式庫。</span><span class="sxs-lookup"><span data-stu-id="6de92-106">Instead, the managed cryptography classes redirect cryptographic operations to a system cryptography library.</span></span> <span data-ttu-id="6de92-107">此原則變更有效地去除了開發人員環境與生產環境之間的潛在混淆，而且讓原生元件與受控元件在相同的密碼編譯原則下執行。</span><span class="sxs-lookup"><span data-stu-id="6de92-107">This policy change effectively removes a potentially confusing difference between developer environments and the production environments and makes native components and managed components operate under the same cryptographic policy.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="6de92-108">建議</span><span class="sxs-lookup"><span data-stu-id="6de92-108">Suggestion</span></span>

<span data-ttu-id="6de92-109">如果不需要此行為，您可以選擇退出並還原先前行為，以便藉由將下列 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 組態設定新增至應用程式組態檔的 [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 區段，在 FIPS 模式中擲回 <xref:System.Security.Cryptography.CryptographicException>：</span><span class="sxs-lookup"><span data-stu-id="6de92-109">If this behavior is undesirable, you can opt out of it and restore the previous behavior so that a <xref:System.Security.Cryptography.CryptographicException> is thrown in FIPS mode by adding the following [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) configuration setting to the [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) section of your application configuration file:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.UseLegacyFipsThrow=true" />
</runtime>
```

<span data-ttu-id="6de92-110">如果您的應用程式以 .NET Framework 4.7.2 或更早版本為目標，您也可以藉由將下列 [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 組態設定新增至應用程式組態檔的 [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 區段，選擇使用這項變更：</span><span class="sxs-lookup"><span data-stu-id="6de92-110">If your application targets .NET Framework 4.7.2 or earlier, you can also opt in to this change by adding the following [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) configuration setting to the [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) section of your application configuration file:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.UseLegacyFipsThrow=false" />
</runtime>
```

| <span data-ttu-id="6de92-111">名稱</span><span class="sxs-lookup"><span data-stu-id="6de92-111">Name</span></span>    | <span data-ttu-id="6de92-112">值</span><span class="sxs-lookup"><span data-stu-id="6de92-112">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="6de92-113">影響範圍</span><span class="sxs-lookup"><span data-stu-id="6de92-113">Scope</span></span>   | <span data-ttu-id="6de92-114">Edge</span><span class="sxs-lookup"><span data-stu-id="6de92-114">Edge</span></span>        |
| <span data-ttu-id="6de92-115">版本</span><span class="sxs-lookup"><span data-stu-id="6de92-115">Version</span></span> | <span data-ttu-id="6de92-116">4.8</span><span class="sxs-lookup"><span data-stu-id="6de92-116">4.8</span></span>         |
| <span data-ttu-id="6de92-117">類型</span><span class="sxs-lookup"><span data-stu-id="6de92-117">Type</span></span>    | <span data-ttu-id="6de92-118">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="6de92-118">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="6de92-119">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="6de92-119">Affected APIs</span></span>

- <xref:System.Security.Cryptography.AesManaged?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.MD5Cng?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.MD5CryptoServiceProvider?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RC2CryptoServiceProvider?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RijndaelManaged?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RIPEMD160Managed?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.SHA1Managed?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.SHA256Managed?displayProperty=nameWithType>

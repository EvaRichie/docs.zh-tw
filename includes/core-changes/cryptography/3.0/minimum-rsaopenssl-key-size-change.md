---
ms.openlocfilehash: 3d94023fc508a56304587121c6cf1444c87b0d52
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721015"
---
### <a name="minimum-size-for-rsaopenssl-key-generation-has-increased"></a><span data-ttu-id="7b8bd-101">RSAOpenSsl 金鑰產生的大小下限已增加</span><span class="sxs-lookup"><span data-stu-id="7b8bd-101">Minimum size for RSAOpenSsl key generation has increased</span></span>

<span data-ttu-id="7b8bd-102">在 Linux 上產生新 RSA 金鑰的最小大小已從 384-位增加至512位。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-102">The minimum size for generating new RSA keys on Linux has increased from 384-bit to 512-bit.</span></span>

#### <a name="change-description"></a><span data-ttu-id="7b8bd-103">變更描述</span><span class="sxs-lookup"><span data-stu-id="7b8bd-103">Change description</span></span>

<span data-ttu-id="7b8bd-104">從 .NET Core 3.0 開始，Linux 上、和的 RSA 實例上的屬性所報告的最低合法金鑰大小， `LegalKeySizes` <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A> <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A> 從384增加到512。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-104">Starting with .NET Core 3.0, the minimum legal key size reported by the `LegalKeySizes` property on RSA instances from <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>, <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A>, and <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A> on Linux has increased from 384 to 512.</span></span>

<span data-ttu-id="7b8bd-105">因此，在 .NET Core 2.2 和更早版本中，方法呼叫（例如）會 `RSA.Create(384)` 成功。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-105">As a result, in .NET Core 2.2 and earlier versions, a method call such as `RSA.Create(384)` succeeds.</span></span> <span data-ttu-id="7b8bd-106">在 .NET Core 3.0 和更新版本中，方法呼叫會擲回例外狀況， `RSA.Create(384)` 指出大小太小。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-106">In .NET Core 3.0 and later versions, the method call `RSA.Create(384)` throws an exception indicating the size is too small.</span></span>

<span data-ttu-id="7b8bd-107">此變更的原因是，OpenSSL 會在 Linux 上執行密碼編譯作業，並在版本1.0.2 和1.1.0 之間產生最小值。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-107">This change was made because OpenSSL, which performs the cryptographic operations on Linux, raised its minimum between versions 1.0.2 and 1.1.0.</span></span> <span data-ttu-id="7b8bd-108">.NET Core 3.0 傾向于將 OpenSSL 1.1. x 新增至 1.0. x，並產生最小的回報版本，以反映這項較高的相依性限制。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-108">.NET Core 3.0 prefers OpenSSL 1.1.x to 1.0.x, and the minimum reported version was raised to reflect this new higher dependency limitation.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="7b8bd-109">引進的版本</span><span class="sxs-lookup"><span data-stu-id="7b8bd-109">Version introduced</span></span>

<span data-ttu-id="7b8bd-110">3.0</span><span class="sxs-lookup"><span data-stu-id="7b8bd-110">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="7b8bd-111">建議的動作</span><span class="sxs-lookup"><span data-stu-id="7b8bd-111">Recommended action</span></span>

<span data-ttu-id="7b8bd-112">如果您呼叫任何受影響的 Api，請確定任何產生的金鑰大小不小於提供者的最小值。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-112">If you call any of the affected APIs, ensure that the size of any generated keys is not less than the provider minimum.</span></span>

> [!NOTE]
> <span data-ttu-id="7b8bd-113">384位 RSA 已經被視為不安全（如同512位 RSA）。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-113">384-bit RSA is already considered insecure (as is 512-bit RSA).</span></span> <span data-ttu-id="7b8bd-114">新式建議（例如[NIST 特殊發行集800-57 第1部分修訂 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf)）會建議2048位做為新產生之金鑰的最小大小。</span><span class="sxs-lookup"><span data-stu-id="7b8bd-114">Modern recommendations, such as [NIST Special Publication 800-57 Part 1 Revision 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf), suggest 2048-bit as the minimum size for newly generated keys.</span></span>

#### <a name="category"></a><span data-ttu-id="7b8bd-115">類別</span><span class="sxs-lookup"><span data-stu-id="7b8bd-115">Category</span></span>

<span data-ttu-id="7b8bd-116">密碼編譯</span><span class="sxs-lookup"><span data-stu-id="7b8bd-116">Cryptography</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="7b8bd-117">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="7b8bd-117">Affected APIs</span></span>

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A>
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A>

<!--
#### Affected APIs

- `P:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes`
- `Overload:System.Security.Cryptography.RSA.Create`
- `Overload:System.Security.Cryptography.RSAOpenSsl.#ctor`
- `Overload:System.Security.Cryptography.RSACryptoServiceProvider.#ctor`

-->

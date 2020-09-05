---
ms.openlocfilehash: a9011514c7c4393ec44de2c7fae88768cdccf435
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497604"
---
### <a name="the-net-framework-46-does-not-use-a-45xx-version-when-registering-itself-in-the-registry"></a><span data-ttu-id="417be-101">.NET Framework 4.6 在登錄中註冊本身時不使用 4.5.x.x 版本</span><span class="sxs-lookup"><span data-stu-id="417be-101">The .NET Framework 4.6 does not use a 4.5.x.x version when registering itself in the registry</span></span>

#### <a name="details"></a><span data-ttu-id="417be-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="417be-102">Details</span></span>

<span data-ttu-id="417be-103">如預期一般，.NET Framework 4.6 在登錄中的版本機碼設定 (位於 <code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full</code>) 開頭為 '4.6'，而不是 '4.5'。</span><span class="sxs-lookup"><span data-stu-id="417be-103">As one might expect, the version key set in the registry (at <code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full</code>) for the .NET Framework 4.6 begins with '4.6', not '4.5'.</span></span> <span data-ttu-id="417be-104">相依於這些登錄機碼以得知電腦上所安裝之 .NET Framework 版本的應用程式應該加以更新，才能了解 4.6 是新的可能版本，以及其與先前的 4.5.x 版相容。</span><span class="sxs-lookup"><span data-stu-id="417be-104">Apps that depend on these registry keys to know which .NET Framework versions are installed on a machine should be updated to understand that 4.6 is a new possible version, and one that is compatible with previous 4.5.x releases.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="417be-105">建議</span><span class="sxs-lookup"><span data-stu-id="417be-105">Suggestion</span></span>

<span data-ttu-id="417be-106">藉由尋找 4.5 登錄機碼來更新 .NET Framework 4.5 安裝的應用程式探查，使其也接受 4.6。</span><span class="sxs-lookup"><span data-stu-id="417be-106">Update apps probing for a .NET Framework 4.5 install by looking for 4.5 registry keys to also accept 4.6.</span></span>

| <span data-ttu-id="417be-107">名稱</span><span class="sxs-lookup"><span data-stu-id="417be-107">Name</span></span>    | <span data-ttu-id="417be-108">值</span><span class="sxs-lookup"><span data-stu-id="417be-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="417be-109">範圍</span><span class="sxs-lookup"><span data-stu-id="417be-109">Scope</span></span>   |<span data-ttu-id="417be-110">Edge</span><span class="sxs-lookup"><span data-stu-id="417be-110">Edge</span></span>|
|<span data-ttu-id="417be-111">版本</span><span class="sxs-lookup"><span data-stu-id="417be-111">Version</span></span>|<span data-ttu-id="417be-112">4.6</span><span class="sxs-lookup"><span data-stu-id="417be-112">4.6</span></span>|
|<span data-ttu-id="417be-113">類型</span><span class="sxs-lookup"><span data-stu-id="417be-113">Type</span></span>|<span data-ttu-id="417be-114">執行階段</span><span class="sxs-lookup"><span data-stu-id="417be-114">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="417be-115">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="417be-115">Affected APIs</span></span>

<span data-ttu-id="417be-116">無法透過 API 分析偵測。</span><span class="sxs-lookup"><span data-stu-id="417be-116">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->

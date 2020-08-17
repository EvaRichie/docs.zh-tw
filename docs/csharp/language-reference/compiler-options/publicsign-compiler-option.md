---
title: -publicsign (C# 編譯器選項)
ms.date: 05/15/2018
f1_keywords:
- /publicsign
helpviewer_keywords:
- -publicsign compiler option [C#]
- publicsign compiler option [C#]
- /publicsign compiler option [C#]
ms.openlocfilehash: 2655e0216a412053e052ab2ec2fcc8c68ea4f968
ms.sourcegitcommit: 0100be20fcf23f61dab672deced70059ed71bb2e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88268045"
---
# <a name="-publicsign-c-compiler-options"></a><span data-ttu-id="9053d-102">-publicsign (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="9053d-102">-publicsign (C# Compiler Options)</span></span>

<span data-ttu-id="9053d-103">此選項會導致編譯器套用公開金鑰，但實際上不會簽署組件。</span><span class="sxs-lookup"><span data-stu-id="9053d-103">This option causes the compiler to apply a public key but does not actually sign the assembly.</span></span> <span data-ttu-id="9053d-104">**-publicsign** 選項也會在組件中設定一個位元，以告知執行階段該檔案實際上已經過簽署。</span><span class="sxs-lookup"><span data-stu-id="9053d-104">The **-publicsign** option also sets a bit in the assembly that tells the runtime that the file is actually signed.</span></span>

## <a name="syntax"></a><span data-ttu-id="9053d-105">語法</span><span class="sxs-lookup"><span data-stu-id="9053d-105">Syntax</span></span>

```console
-publicsign
```

## <a name="arguments"></a><span data-ttu-id="9053d-106">引數</span><span class="sxs-lookup"><span data-stu-id="9053d-106">Arguments</span></span>

<span data-ttu-id="9053d-107">無。</span><span class="sxs-lookup"><span data-stu-id="9053d-107">None.</span></span>

## <a name="remarks"></a><span data-ttu-id="9053d-108">備註</span><span class="sxs-lookup"><span data-stu-id="9053d-108">Remarks</span></span>

<span data-ttu-id="9053d-109">**-publicsign** 選項需要使用 [-keyfile](keyfile-compiler-option.md) 或 [-keycontainer](keycontainer-compiler-option.md)。</span><span class="sxs-lookup"><span data-stu-id="9053d-109">The **-publicsign** option requires the use of the [-keyfile](keyfile-compiler-option.md) or [-keycontainer](keycontainer-compiler-option.md).</span></span> <span data-ttu-id="9053d-110">**Keyfile** 或 **keycontainer** 選項會指定公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="9053d-110">The **keyfile** or **keycontainer** options specify the public key.</span></span>

<span data-ttu-id="9053d-111">**-publicsign** 和 **-delaysign** 選項是互斥的。</span><span class="sxs-lookup"><span data-stu-id="9053d-111">The **-publicsign** and **-delaysign** options are mutually exclusive.</span></span>

<span data-ttu-id="9053d-112">有時稱為「假簽署」或「OSS 簽署」，公開簽署會在輸出組件中包含公開金鑰並設定「已簽署」的旗標，但實際上不會使用私密金鑰來簽署組件。</span><span class="sxs-lookup"><span data-stu-id="9053d-112">Sometimes called "fake sign" or "OSS sign", public signing includes the public key in an output assembly and sets the "signed" flag, but doesn't actually sign the assembly with a private key.</span></span> <span data-ttu-id="9053d-113">這對開放原始碼專案非常實用。在這類專案中，人員想要建置可與已發行「完整簽署」組件相容的組件，但該組件無法存取可用來簽署組件的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="9053d-113">This is useful for open source projects where people want to build assemblies which are compatible with the released "fully signed" assemblies, but don't have access to the private key used to sign the assemblies.</span></span> <span data-ttu-id="9053d-114">由於實際上幾乎沒有任何取用者需要檢查組件是否已完整簽署，因此，這些公開建置的組件幾乎適用於每個要使用完整簽署組件的案例。</span><span class="sxs-lookup"><span data-stu-id="9053d-114">Since almost no consumers actually need to check if the assembly is fully signed, these publicly built assemblies are useable in almost every scenario where the fully signed one would be used.</span></span>

### <a name="to-set-this-compiler-option-in-a-csproj-file"></a><span data-ttu-id="9053d-115">若要在 .csproj 檔案中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="9053d-115">To set this compiler option in a csproj file</span></span>

<span data-ttu-id="9053d-116">開啟專案的 .csproj 檔案，然後加入下列元素：</span><span class="sxs-lookup"><span data-stu-id="9053d-116">Open the .csproj file for a project, and add the following element:</span></span>

```xml
<PublicSign>true</PublicSign>
```

## <a name="see-also"></a><span data-ttu-id="9053d-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9053d-117">See also</span></span>

- [<span data-ttu-id="9053d-118">C# 編譯器 -delaysign 選項</span><span class="sxs-lookup"><span data-stu-id="9053d-118">C# Compiler -delaysign option</span></span>](delaysign-compiler-option.md)
- [<span data-ttu-id="9053d-119">C# 編譯器 -keyfile 選項</span><span class="sxs-lookup"><span data-stu-id="9053d-119">C# Compiler -keyfile option</span></span>](keyfile-compiler-option.md)
- [<span data-ttu-id="9053d-120">C# 編譯器 -keycontainer 選項</span><span class="sxs-lookup"><span data-stu-id="9053d-120">C# Compiler -keycontainer option</span></span>](keycontainer-compiler-option.md)
- [<span data-ttu-id="9053d-121">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="9053d-121">C# Compiler Options</span></span>](index.md)
- [<span data-ttu-id="9053d-122">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="9053d-122">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

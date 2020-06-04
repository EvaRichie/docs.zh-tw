---
title: -delaysign
ms.date: 03/10/2018
helpviewer_keywords:
- delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
ms.openlocfilehash: c9bb302e2b34ebe1f51cf39bb3db1094d420d7f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408695"
---
# <a name="-delaysign"></a><span data-ttu-id="41b07-102">-delaysign</span><span class="sxs-lookup"><span data-stu-id="41b07-102">-delaysign</span></span>

<span data-ttu-id="41b07-103">指定將要完整簽署還是部分簽署組件。</span><span class="sxs-lookup"><span data-stu-id="41b07-103">Specifies whether the assembly will be fully or partially signed.</span></span>

## <a name="syntax"></a><span data-ttu-id="41b07-104">語法</span><span class="sxs-lookup"><span data-stu-id="41b07-104">Syntax</span></span>

```console
-delaysign[+ | -]
```

## <a name="arguments"></a><span data-ttu-id="41b07-105">引數</span><span class="sxs-lookup"><span data-stu-id="41b07-105">Arguments</span></span>

<span data-ttu-id="41b07-106">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="41b07-106">`+` &#124; `-`</span></span>  
<span data-ttu-id="41b07-107">選擇性。</span><span class="sxs-lookup"><span data-stu-id="41b07-107">Optional.</span></span> <span data-ttu-id="41b07-108">如果要完整簽署組件，請使用 `-delaysign-`。</span><span class="sxs-lookup"><span data-stu-id="41b07-108">Use `-delaysign-` if you want a fully signed assembly.</span></span> <span data-ttu-id="41b07-109">`-delaysign+`如果您想要將公開金鑰放在元件中，並為帶正負號的雜湊保留空間，請使用。</span><span class="sxs-lookup"><span data-stu-id="41b07-109">Use `-delaysign+` if you want to place the public key in the assembly and reserve space for the signed hash.</span></span> <span data-ttu-id="41b07-110">預設值為 `-delaysign-`。</span><span class="sxs-lookup"><span data-stu-id="41b07-110">The default is `-delaysign-`.</span></span>

## <a name="remarks"></a><span data-ttu-id="41b07-111">備註</span><span class="sxs-lookup"><span data-stu-id="41b07-111">Remarks</span></span>

<span data-ttu-id="41b07-112">`-delaysign`除非搭配[-keyfile](keyfile.md)或[-keycontainer](keycontainer.md)使用，否則選項不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="41b07-112">The `-delaysign` option has no effect unless used with [-keyfile](keyfile.md) or [-keycontainer](keycontainer.md).</span></span>

<span data-ttu-id="41b07-113">當您要求完整簽署的組件時，編譯器會雜湊包含資訊清單 (組件中繼資料) 的檔案，並使用私密金鑰簽署該雜湊。</span><span class="sxs-lookup"><span data-stu-id="41b07-113">When you request a fully signed assembly, the compiler hashes the file that contains the manifest (assembly metadata) and signs that hash with the private key.</span></span> <span data-ttu-id="41b07-114">所產生的數位簽章會儲存在包含資訊清單的檔案中。</span><span class="sxs-lookup"><span data-stu-id="41b07-114">The resulting digital signature is stored in the file that contains the manifest.</span></span> <span data-ttu-id="41b07-115">當元件延遲簽署時，編譯器不會計算和儲存簽章，但會在檔案中保留空間，以便稍後新增簽章。</span><span class="sxs-lookup"><span data-stu-id="41b07-115">When an assembly is delay signed, the compiler does not compute and store the signature but reserves space in the file so the signature can be added later.</span></span>

<span data-ttu-id="41b07-116">例如，藉由使用 `-delaysign+` ，組織中的開發人員可以散發元件的未簽署測試版本，讓測試人員可以向全域組件快取註冊並使用。</span><span class="sxs-lookup"><span data-stu-id="41b07-116">For example, by using `-delaysign+`, a developer in an organization can distribute unsigned test versions of an assembly that testers can register with the global assembly cache and use.</span></span> <span data-ttu-id="41b07-117">當元件上的工作完成時，負責組織之私密金鑰的人員可以完整簽署元件。</span><span class="sxs-lookup"><span data-stu-id="41b07-117">When work on the assembly is completed, the person responsible for the organization's private key can fully sign the assembly.</span></span> <span data-ttu-id="41b07-118">這項區隔可保護組織的私密金鑰免于洩漏，同時允許所有開發人員處理元件。</span><span class="sxs-lookup"><span data-stu-id="41b07-118">This compartmentalization protects the organization's private key from disclosure, while allowing all developers to work on the assemblies.</span></span>

<span data-ttu-id="41b07-119">如需簽署元件的詳細資訊，請參閱[建立和使用強式名稱的元件](../../../standard/assembly/create-use-strong-named.md)。</span><span class="sxs-lookup"><span data-stu-id="41b07-119">See [Creating and Using Strong-Named Assemblies](../../../standard/assembly/create-use-strong-named.md) for more information on signing an assembly.</span></span>

### <a name="to-set--delaysign-in-the-visual-studio-integrated-development-environment"></a><span data-ttu-id="41b07-120">在 Visual Studio 的整合式開發環境中設定-delaysign</span><span class="sxs-lookup"><span data-stu-id="41b07-120">To set -delaysign in the Visual Studio integrated development environment</span></span>

1. <span data-ttu-id="41b07-121">在 **方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="41b07-121">Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="41b07-122">按一下 [專案]\*\*\*\* 功能表上的 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="41b07-122">On the **Project** menu, click **Properties**.</span></span>

2. <span data-ttu-id="41b07-123">按一下 [ **簽署** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="41b07-123">Click the **Signing** tab.</span></span>

3. <span data-ttu-id="41b07-124">在 [**延遲簽署**] 方塊中設定值。</span><span class="sxs-lookup"><span data-stu-id="41b07-124">Set the value in the **Delay sign only** box.</span></span>

## <a name="see-also"></a><span data-ttu-id="41b07-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="41b07-125">See also</span></span>

- [<span data-ttu-id="41b07-126">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="41b07-126">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="41b07-127">-keyfile</span><span class="sxs-lookup"><span data-stu-id="41b07-127">-keyfile</span></span>](keyfile.md)
- [<span data-ttu-id="41b07-128">-keycontainer</span><span class="sxs-lookup"><span data-stu-id="41b07-128">-keycontainer</span></span>](keycontainer.md)
- [<span data-ttu-id="41b07-129">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="41b07-129">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)

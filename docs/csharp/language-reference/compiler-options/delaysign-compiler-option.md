---
description: -delaysign (C# 編譯器選項)
title: -delaysign (C# 編譯器選項)
ms.date: 05/15/2018
f1_keywords:
- /delaysign
helpviewer_keywords:
- -delaysign compiler option [C#]
- delaysign compiler option [C#]
- /delaysign compiler option [C#]
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
ms.openlocfilehash: 5512ebeca4672f5d69852ab07c3f3fa40c305327
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125835"
---
# <a name="-delaysign-c-compiler-options"></a><span data-ttu-id="84137-103">-delaysign (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="84137-103">-delaysign (C# Compiler Options)</span></span>

<span data-ttu-id="84137-104">這個選項可讓編譯器保留輸出檔案中的空間，以便稍後新增數位簽章。</span><span class="sxs-lookup"><span data-stu-id="84137-104">This option causes the compiler to reserve space in the output file so that a digital signature can be added later.</span></span>

## <a name="syntax"></a><span data-ttu-id="84137-105">語法</span><span class="sxs-lookup"><span data-stu-id="84137-105">Syntax</span></span>

```console
-delaysign[ + | - ]
```

## <a name="arguments"></a><span data-ttu-id="84137-106">引數</span><span class="sxs-lookup"><span data-stu-id="84137-106">Arguments</span></span>

<span data-ttu-id="84137-107">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="84137-107">`+` &#124; `-`</span></span>

<span data-ttu-id="84137-108">如果需要完整簽署的組件，請使用 **-delaysign-**。</span><span class="sxs-lookup"><span data-stu-id="84137-108">Use **-delaysign-** if you want a fully signed assembly.</span></span> <span data-ttu-id="84137-109">如果只想在組件中放置公開金鑰，請使用 **-delaysign+**。</span><span class="sxs-lookup"><span data-stu-id="84137-109">Use **-delaysign+** if you only want to place the public key in the assembly.</span></span> <span data-ttu-id="84137-110">預設值為 **-delaysign-**。</span><span class="sxs-lookup"><span data-stu-id="84137-110">The default is **-delaysign-**.</span></span>

## <a name="remarks"></a><span data-ttu-id="84137-111">備註</span><span class="sxs-lookup"><span data-stu-id="84137-111">Remarks</span></span>

<span data-ttu-id="84137-112">除非搭配[-keyfile](./keyfile-compiler-option.md)或[-keycontainer](./keycontainer-compiler-option.md)使用，否則 **-delaysign**選項不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="84137-112">The **-delaysign** option has no effect unless used with [-keyfile](./keyfile-compiler-option.md) or [-keycontainer](./keycontainer-compiler-option.md).</span></span>

<span data-ttu-id="84137-113">**-delaysign** 和 **-publicsign** 選項是互斥的。</span><span class="sxs-lookup"><span data-stu-id="84137-113">The **-delaysign** and **-publicsign** options are mutually exclusive.</span></span>

<span data-ttu-id="84137-114">當您要求完整簽署的組件時，編譯器會雜湊包含資訊清單 (組件中繼資料) 的檔案，並使用私密金鑰簽署該雜湊。</span><span class="sxs-lookup"><span data-stu-id="84137-114">When you request a fully signed assembly, the compiler hashes the file that contains the manifest (assembly metadata) and signs that hash with the private key.</span></span> <span data-ttu-id="84137-115">該作業會建立數位簽章，並儲存於包含資訊清單的檔案中。</span><span class="sxs-lookup"><span data-stu-id="84137-115">That operation creates a digital signature which is stored in the file that contains the manifest.</span></span> <span data-ttu-id="84137-116">當延遲簽署組件時，編譯器不會去計算和儲存簽章，但會保留檔案中的空間，以便稍後再加入簽章。</span><span class="sxs-lookup"><span data-stu-id="84137-116">When an assembly is delay signed, the compiler does not compute and store the signature, but reserves space in the file so the signature can be added later.</span></span>

<span data-ttu-id="84137-117">例如，使用 **-delaysign+** 時，可讓測試人員將組件放入全域快取中。</span><span class="sxs-lookup"><span data-stu-id="84137-117">For example, using **-delaysign+** allows a tester to put the assembly in the global cache.</span></span> <span data-ttu-id="84137-118">測試之後，您可以使用 [Assembly Linker](../../../framework/tools/al-exe-assembly-linker.md) 公用程式將私密金鑰放入組件中，以完整簽署組件。</span><span class="sxs-lookup"><span data-stu-id="84137-118">After testing, you can fully sign the assembly by placing the private key in the assembly using the [Assembly Linker](../../../framework/tools/al-exe-assembly-linker.md) utility.</span></span>

<span data-ttu-id="84137-119">如需詳細資訊，請參閱[建立和使用強式名稱的組件](../../../standard/assembly/create-use-strong-named.md)和[延遲簽署組件](../../../standard/assembly/delay-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="84137-119">For more information, see [Creating and Using Strong-Named Assemblies](../../../standard/assembly/create-use-strong-named.md) and [Delay Signing an Assembly](../../../standard/assembly/delay-sign.md).</span></span>

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="84137-120">在 Visual Studio 開發環境中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="84137-120">To set this compiler option in the Visual Studio development environment</span></span>

1. <span data-ttu-id="84137-121">開啟專案的 [屬性] \*\*\*\* 頁面。</span><span class="sxs-lookup"><span data-stu-id="84137-121">Open the **Properties** page for the project.</span></span>
1. <span data-ttu-id="84137-122">修改 [僅延遲簽署]\*\*\*\* 屬性。</span><span class="sxs-lookup"><span data-stu-id="84137-122">Modify the **Delay sign only** property.</span></span>

<span data-ttu-id="84137-123">如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>。</span><span class="sxs-lookup"><span data-stu-id="84137-123">For information on how to set this compiler option programmatically, see <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.</span></span>

## <a name="see-also"></a><span data-ttu-id="84137-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84137-124">See also</span></span>

- [<span data-ttu-id="84137-125">C# -publicsign 選項</span><span class="sxs-lookup"><span data-stu-id="84137-125">C# -publicsign option</span></span>](publicsign-compiler-option.md)
- [<span data-ttu-id="84137-126">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="84137-126">C# Compiler Options</span></span>](index.md)
- [<span data-ttu-id="84137-127">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="84137-127">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

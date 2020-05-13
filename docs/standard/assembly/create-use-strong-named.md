---
title: 建立和使用強式名稱的組件
description: 本文說明如何在 .NET 中使用強式名稱簽署元件，並于稍後依該名稱參考它。
ms.date: 08/19/2019
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, about strong-named assemblies
- strong-named assemblies
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, scenarios
- assemblies [.NET Framework], strong-named
- strong-named assemblies, loading into trusted application domains
- assembly binding, strong-named
ms.assetid: ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9
ms.openlocfilehash: 79c8cf2c21210fd80392a8aacf92840c11a36e43
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378525"
---
# <a name="create-and-use-strong-named-assemblies"></a><span data-ttu-id="b4a53-103">建立和使用強式名稱的組件</span><span class="sxs-lookup"><span data-stu-id="b4a53-103">Create and use strong-named assemblies</span></span>

<span data-ttu-id="b4a53-104">強式名稱 (Strong Name) 是由組件的識別 (Identity)，也就是其簡單文字名稱、版本號碼及文化特性資訊 (如果有提供)，加上公開金鑰和數位簽章所組成的。</span><span class="sxs-lookup"><span data-stu-id="b4a53-104">A strong name consists of the assembly's identity—its simple text name, version number, and culture information (if provided)—plus a public key and a digital signature.</span></span> <span data-ttu-id="b4a53-105">這是使用對應的私密金鑰，從組件檔案所產生 </span><span class="sxs-lookup"><span data-stu-id="b4a53-105">It is generated from an assembly file using the corresponding private key.</span></span> <span data-ttu-id="b4a53-106">(組件檔案包含附屬組件資訊清單，而資訊清單則包含組件中所有檔案的名稱和雜湊)。</span><span class="sxs-lookup"><span data-stu-id="b4a53-106">(The assembly file contains the assembly manifest, which contains the names and hashes of all the files that make up the assembly.)</span></span>

> [!WARNING]
> <span data-ttu-id="b4a53-107">請勿依賴強式名稱提供安全性。</span><span class="sxs-lookup"><span data-stu-id="b4a53-107">Do not rely on strong names for security.</span></span> <span data-ttu-id="b4a53-108">強式名稱僅提供唯一識別。</span><span class="sxs-lookup"><span data-stu-id="b4a53-108">They provide a unique identity only.</span></span>

<span data-ttu-id="b4a53-109">強式名稱的組件只可使用來自其他強式名稱組件的類型。</span><span class="sxs-lookup"><span data-stu-id="b4a53-109">A strong-named assembly can only use types from other strong-named assemblies.</span></span> <span data-ttu-id="b4a53-110">否則，強式名稱組件的完整性會受到危害。</span><span class="sxs-lookup"><span data-stu-id="b4a53-110">Otherwise, the integrity of the strong-named assembly would be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a53-111">雖然 .NET Core 支援強式名稱的元件，而且 .NET Core 程式庫中的所有元件都已簽署，但大部分的協力廠商元件都不需要強名稱。</span><span class="sxs-lookup"><span data-stu-id="b4a53-111">Although .NET Core supports strong-named assemblies, and all assemblies in the .NET Core library are signed, the majority of third-party assemblies do not need strong names.</span></span> <span data-ttu-id="b4a53-112">如需詳細資訊，請參閱 GitHub 上的[強式名稱簽署](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a53-112">For more information, see [Strong Name Signing](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md) on GitHub.</span></span>

## <a name="strong-name-scenario"></a><span data-ttu-id="b4a53-113">強式名稱案例</span><span class="sxs-lookup"><span data-stu-id="b4a53-113">Strong name scenario</span></span>

<span data-ttu-id="b4a53-114">下列案例概述處理序如何使用強式名稱簽署組件，然後再使用該名稱參考該組件。</span><span class="sxs-lookup"><span data-stu-id="b4a53-114">The following scenario outlines the process of signing an assembly with a strong name and later referencing it by that name.</span></span>

1. <span data-ttu-id="b4a53-115">組件 A 是以下列方法之一，使用強式名稱所建立：</span><span class="sxs-lookup"><span data-stu-id="b4a53-115">Assembly A is created with a strong name using one of the following methods:</span></span>

    - <span data-ttu-id="b4a53-116">使用支援建立強式名稱的開發環境，例如 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b4a53-116">Using a development environment that supports creating strong names, such as Visual Studio.</span></span>

    - <span data-ttu-id="b4a53-117">使用[強式名稱工具 (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 建立密碼編譯金鑰組，並使用命令列編譯器或[組件連結器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 將該金鑰組指派給組件。</span><span class="sxs-lookup"><span data-stu-id="b4a53-117">Creating a cryptographic key pair using the [Strong Name tool (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) and assigning that key pair to the assembly using either a command-line compiler or the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md).</span></span> <span data-ttu-id="b4a53-118">Windows SDK 提供 Sn.exe 與 Al.exe。</span><span class="sxs-lookup"><span data-stu-id="b4a53-118">The Windows SDK provides both Sn.exe and Al.exe.</span></span>

2. <span data-ttu-id="b4a53-119">開發環境或工具會使用開發人員的私密金鑰簽署檔案雜湊，而該檔案中包含組件的資訊清單。</span><span class="sxs-lookup"><span data-stu-id="b4a53-119">The development environment or tool signs the hash of the file containing the assembly's manifest with the developer's private key.</span></span> <span data-ttu-id="b4a53-120">此數位簽章儲存在可攜式執行檔 (PE) 中，而該檔案包含組件 A 的 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="b4a53-120">This digital signature is stored in the portable executable (PE) file that contains Assembly A's manifest.</span></span>

3. <span data-ttu-id="b4a53-121">組件 B 是組件 A 的消費者。組件 B 的資訊清單參考區段包含代表組件 A 公開金鑰的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b4a53-121">Assembly B is a consumer of Assembly A. The reference section of Assembly B's manifest includes a token that represents Assembly A's public key.</span></span> <span data-ttu-id="b4a53-122">語彙基元是完整公開金鑰的一部分，會取代金鑰本身來節省空間。</span><span class="sxs-lookup"><span data-stu-id="b4a53-122">A token is a portion of the full public key and is used rather than the key itself to save space.</span></span>

4. <span data-ttu-id="b4a53-123">當組件放在全域組件快取時，Common Language Runtime 會驗證強式名稱簽草章。</span><span class="sxs-lookup"><span data-stu-id="b4a53-123">The common language runtime verifies the strong name signature when the assembly is placed in the global assembly cache.</span></span> <span data-ttu-id="b4a53-124">Common Language Runtime 在執行階段以強式名稱繫結時，會比較儲存在組件 B 資訊清單的金鑰，以及用來產生組件 A 強式名稱的金鑰。若 .NET Framework 通過安全性檢查且繫結成功，組件 B 就能保證組件 A 的位元未被修改，而且確實來自組件 A 的開發人員。</span><span class="sxs-lookup"><span data-stu-id="b4a53-124">When binding by strong name at run time, the common language runtime compares the key stored in Assembly B's manifest with the key used to generate the strong name for Assembly A. If the .NET Framework security checks pass and the bind succeeds, Assembly B has a guarantee that Assembly A's bits have not been tampered with and that these bits actually come from the developers of Assembly A.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a53-125">此案例無法解決信任問題。</span><span class="sxs-lookup"><span data-stu-id="b4a53-125">This scenario doesn't address trust issues.</span></span> <span data-ttu-id="b4a53-126">除了強式名稱之外，組件能夠包含完整的 Microsoft Authenticode 簽章。</span><span class="sxs-lookup"><span data-stu-id="b4a53-126">Assemblies can carry full Microsoft Authenticode signatures in addition to a strong name.</span></span> <span data-ttu-id="b4a53-127">Authenticode 簽章包含建立信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="b4a53-127">Authenticode signatures include a certificate that establishes trust.</span></span> <span data-ttu-id="b4a53-128">請務必注意，強式名稱不會要求程式碼以這種方式簽署。</span><span class="sxs-lookup"><span data-stu-id="b4a53-128">It's important to note that strong names don't require code to be signed in this way.</span></span> <span data-ttu-id="b4a53-129">強式名稱僅提供唯一身分識別。</span><span class="sxs-lookup"><span data-stu-id="b4a53-129">Strong names only provide a unique identity.</span></span>

## <a name="bypass-signature-verification-of-trusted-assemblies"></a><span data-ttu-id="b4a53-130">略過信任組件的簽章驗證</span><span class="sxs-lookup"><span data-stu-id="b4a53-130">Bypass signature verification of trusted assemblies</span></span>

<span data-ttu-id="b4a53-131">從 .NET Framework 3.5 Service Pack 1 開始，當組件載入到完全信任的應用程式網域 (例如適用於 `MyComputer` 區域的預設應用程式網域) 時，不會驗證強式名稱簽章。</span><span class="sxs-lookup"><span data-stu-id="b4a53-131">Starting with the .NET Framework 3.5 Service Pack 1, strong-name signatures are not validated when an assembly is loaded into a full-trust application domain, such as the default application domain for the `MyComputer` zone.</span></span> <span data-ttu-id="b4a53-132">這是指強式名稱略過功能。</span><span class="sxs-lookup"><span data-stu-id="b4a53-132">This is referred to as the strong-name bypass feature.</span></span> <span data-ttu-id="b4a53-133">在完全信任環境中，不論簽章為何，已簽署、完全信任的組件要求 <xref:System.Security.Permissions.StrongNameIdentityPermission> 一律會成功。</span><span class="sxs-lookup"><span data-stu-id="b4a53-133">In a full-trust environment, demands for <xref:System.Security.Permissions.StrongNameIdentityPermission> always succeed for signed, full-trust assemblies, regardless of their signature.</span></span> <span data-ttu-id="b4a53-134">強式名稱略過功能可以避免在這種狀況中不必要的額外負荷，也就是完全信任組件的強式名稱簽章驗證，讓組件能夠更快載入。</span><span class="sxs-lookup"><span data-stu-id="b4a53-134">The strong-name bypass feature avoids the unnecessary overhead of strong-name signature verification of full-trust assemblies in this situation, allowing the assemblies to load faster.</span></span>

<span data-ttu-id="b4a53-135">略過功能適用於任何以強式名稱簽署並具有下列特性的組件：</span><span class="sxs-lookup"><span data-stu-id="b4a53-135">The bypass feature applies to any assembly that is signed with a strong name and that has the following characteristics:</span></span>

- <span data-ttu-id="b4a53-136">完全信任而不具有 <xref:System.Security.Policy.StrongName> 辨識項 (例如具有 `MyComputer` 區域辨識項)。</span><span class="sxs-lookup"><span data-stu-id="b4a53-136">Fully trusted without <xref:System.Security.Policy.StrongName> evidence (for example, has `MyComputer` zone evidence).</span></span>

- <span data-ttu-id="b4a53-137">載入到完全信任的 <xref:System.AppDomain>。</span><span class="sxs-lookup"><span data-stu-id="b4a53-137">Loaded into a fully trusted <xref:System.AppDomain>.</span></span>

- <span data-ttu-id="b4a53-138">從 <xref:System.AppDomain> 的 <xref:System.AppDomainSetup.ApplicationBase%2A> 屬性下的位置載入。</span><span class="sxs-lookup"><span data-stu-id="b4a53-138">Loaded from a location under the <xref:System.AppDomainSetup.ApplicationBase%2A> property of that <xref:System.AppDomain>.</span></span>

- <span data-ttu-id="b4a53-139">不延遲簽署。</span><span class="sxs-lookup"><span data-stu-id="b4a53-139">Not delay-signed.</span></span>

<span data-ttu-id="b4a53-140">個別應用程式或電腦可停用此功能。</span><span class="sxs-lookup"><span data-stu-id="b4a53-140">This feature can be disabled for individual applications or for a computer.</span></span> <span data-ttu-id="b4a53-141">請參閱[如何：停用強式名稱略過功能](disable-strong-name-bypass-feature.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a53-141">See [How to: Disable the strong-name bypass feature](disable-strong-name-bypass-feature.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="b4a53-142">相關主題</span><span class="sxs-lookup"><span data-stu-id="b4a53-142">Related topics</span></span>

|<span data-ttu-id="b4a53-143">Title</span><span class="sxs-lookup"><span data-stu-id="b4a53-143">Title</span></span>|<span data-ttu-id="b4a53-144">描述</span><span class="sxs-lookup"><span data-stu-id="b4a53-144">Description</span></span>|
|-----------|-----------------|
|[<span data-ttu-id="b4a53-145">如何：建立公開/私密金鑰組</span><span class="sxs-lookup"><span data-stu-id="b4a53-145">How to: Create a public-private key pair</span></span>](create-public-private-key-pair.md)|<span data-ttu-id="b4a53-146">描述如何建立簽署組件的密碼編譯金鑰組。</span><span class="sxs-lookup"><span data-stu-id="b4a53-146">Describes how to create a cryptographic key pair for signing an assembly.</span></span>|
|[<span data-ttu-id="b4a53-147">如何：使用強式名稱簽署元件</span><span class="sxs-lookup"><span data-stu-id="b4a53-147">How to: Sign an assembly with a strong name</span></span>](sign-strong-name.md)|<span data-ttu-id="b4a53-148">描述如何建立強式名稱組件。</span><span class="sxs-lookup"><span data-stu-id="b4a53-148">Describes how to create a strong-named assembly.</span></span>|
|[<span data-ttu-id="b4a53-149">增強的強式命名</span><span class="sxs-lookup"><span data-stu-id="b4a53-149">Enhanced strong naming</span></span>](enhanced-strong-naming.md)|<span data-ttu-id="b4a53-150">描述 .NET Framework 4.5 中強式名稱的增強項目。</span><span class="sxs-lookup"><span data-stu-id="b4a53-150">Describes enhancements to strong-names in the .NET Framework 4.5.</span></span>|
|[<span data-ttu-id="b4a53-151">如何：參考強式名稱的元件</span><span class="sxs-lookup"><span data-stu-id="b4a53-151">How to: Reference a strong-named assembly</span></span>](reference-strong-named.md)|<span data-ttu-id="b4a53-152">描述如何在編譯或執行階段期間，參考以強式名稱命名之組件中的類型或資源。</span><span class="sxs-lookup"><span data-stu-id="b4a53-152">Describes how to reference types or resources in a strong-named assembly at compile time or run time.</span></span>|
|[<span data-ttu-id="b4a53-153">如何：停用強式名稱略過功能</span><span class="sxs-lookup"><span data-stu-id="b4a53-153">How to: Disable the strong-name bypass feature</span></span>](disable-strong-name-bypass-feature.md)|<span data-ttu-id="b4a53-154">描述如何停用會略過強式名稱簽章驗證的功能。</span><span class="sxs-lookup"><span data-stu-id="b4a53-154">Describes how to disable the feature that bypasses the validation of strong-name signatures.</span></span> <span data-ttu-id="b4a53-155">所有應用程式皆可停用此功能，也可以只停用特定應用程式中的此功能。</span><span class="sxs-lookup"><span data-stu-id="b4a53-155">This feature can be disabled for all or for specific applications.</span></span>|
|[<span data-ttu-id="b4a53-156">建立組件</span><span class="sxs-lookup"><span data-stu-id="b4a53-156">Create assemblies</span></span>](create.md)|<span data-ttu-id="b4a53-157">提供單一檔案和多檔案組件的概觀。</span><span class="sxs-lookup"><span data-stu-id="b4a53-157">Provides an overview of single-file and multifile assemblies.</span></span>|
|[<span data-ttu-id="b4a53-158">如何在 Visual Studio 中延遲簽署元件</span><span class="sxs-lookup"><span data-stu-id="b4a53-158">How to delay sign an assembly in Visual Studio</span></span>](/visualstudio/ide/managing-assembly-and-manifest-signing#how-to-sign-an-assembly-in-visual-studio)|<span data-ttu-id="b4a53-159">說明如何在建立組件之後，使用強式名稱簽署組件。</span><span class="sxs-lookup"><span data-stu-id="b4a53-159">Explains how to sign an assembly with a strong name after the assembly has been created.</span></span>|
|[<span data-ttu-id="b4a53-160">Sn.exe （強式名稱工具）</span><span class="sxs-lookup"><span data-stu-id="b4a53-160">Sn.exe (Strong Name tool)</span></span>](../../framework/tools/sn-exe-strong-name-tool.md)|<span data-ttu-id="b4a53-161">描述 .NET Framework 中可協助使用強式名稱來建立組件的工具。</span><span class="sxs-lookup"><span data-stu-id="b4a53-161">Describes the tool included in the .NET Framework that helps create assemblies with strong names.</span></span> <span data-ttu-id="b4a53-162">這個工具提供了金鑰管理、簽章產生和簽章驗證的選項。</span><span class="sxs-lookup"><span data-stu-id="b4a53-162">This tool provides options for key management, signature generation, and signature verification.</span></span>|
|[<span data-ttu-id="b4a53-163">Al.exe (組件連接器)</span><span class="sxs-lookup"><span data-stu-id="b4a53-163">Al.exe (Assembly linker)</span></span>](../../framework/tools/al-exe-assembly-linker.md)|<span data-ttu-id="b4a53-164">描述 .NET Framework 中可產生檔案的工具，而該檔案具有來自模組或資源檔案組件的資訊清單。</span><span class="sxs-lookup"><span data-stu-id="b4a53-164">Describes the tool included in the .NET Framework that generates a file that has an assembly manifest from modules or resource files.</span></span>|

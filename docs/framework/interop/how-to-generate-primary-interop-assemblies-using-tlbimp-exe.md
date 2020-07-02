---
title: 作法：使用 Tlbimp.exe 產生主要 Interop 組件
description: 瞭解如何使用 Windows SDK 提供的型別程式庫匯入工具（Tlbimp.exe），產生主要 interop 元件。
ms.date: 03/30/2017
helpviewer_keywords:
- primary interop assemblies, generating
- Tlbimp.exe
- Type Library Importer
ms.assetid: 5419011c-6e57-40f6-8c65-386db8f7a651
ms.openlocfilehash: 779b4863b6f1513f3566d4ab31660d88cda1039b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619126"
---
# <a name="how-to-generate-primary-interop-assemblies-using-tlbimpexe"></a><span data-ttu-id="d5220-103">作法：使用 Tlbimp.exe 產生主要 Interop 組件</span><span class="sxs-lookup"><span data-stu-id="d5220-103">How to: Generate Primary Interop Assemblies Using Tlbimp.exe</span></span>

<span data-ttu-id="d5220-104">有兩種方式可產生主要 Interop 組件：</span><span class="sxs-lookup"><span data-stu-id="d5220-104">There are two ways to generate a primary interop assembly:</span></span>

- <span data-ttu-id="d5220-105">使用 Windows SDK 提供的[型別程式庫匯入工具 (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)。</span><span class="sxs-lookup"><span data-stu-id="d5220-105">Using the [Type Library Importer (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md) provided by the Windows SDK.</span></span>

  <span data-ttu-id="d5220-106">產生主要 Interop 組件最直接的方法是使用[型別程式庫匯入工具 (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)。</span><span class="sxs-lookup"><span data-stu-id="d5220-106">The most straightforward way to produce primary interop assemblies is to use the [Tlbimp.exe (Type Library Importer)](../tools/tlbimp-exe-type-library-importer.md).</span></span> <span data-ttu-id="d5220-107">Tlbimp.exe 會提供下列保護措施：</span><span class="sxs-lookup"><span data-stu-id="d5220-107">Tlbimp.exe provides the following safeguards:</span></span>

  - <span data-ttu-id="d5220-108">建立任何巢狀類型程式庫參考的新 Interop 組件之前，檢查是否有其他已註冊的主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-108">Checks for other registered primary interop assemblies before creating new interop assemblies for any nested type library references.</span></span>

  - <span data-ttu-id="d5220-109">如果您未指定容器或檔案名稱，來指定主要 Interop 組件的強式名稱，則無法發出主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-109">Fails to emit the primary interop assembly if you do not specify either the container or file name to give the primary interop assembly a strong name.</span></span>

  - <span data-ttu-id="d5220-110">如果您省略相依組件的參考，則無法發出主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-110">Fails to emit a primary interop assembly if you omit references to dependent assemblies.</span></span>

  - <span data-ttu-id="d5220-111">如果您加入非主要 Interop 組件的相依組件的參考，則無法發出主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-111">Fails to emit a primary interop assembly if you add references to dependent assemblies that are not primary interop assemblies.</span></span>

- <span data-ttu-id="d5220-112">使用與 Common Language Specification (CLS) 相容的語言，例如 C#，在原始程式碼中手動建立主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-112">Creating primary interop assemblies manually in source code by using a language that is compliant with the Common Language Specification (CLS), such as C#.</span></span> <span data-ttu-id="d5220-113">無法使用類型程式庫時，這個方法就很有用。</span><span class="sxs-lookup"><span data-stu-id="d5220-113">This approach is useful when a type library is unavailable.</span></span>

<span data-ttu-id="d5220-114">您必須使用密碼編譯金鑰組將組件簽署為強式名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-114">You must have a cryptographic key pair to sign the assembly with a strong name.</span></span> <span data-ttu-id="d5220-115">如需詳細資料，請參閱[建立金鑰組](../../standard/assembly/create-public-private-key-pair.md)。</span><span class="sxs-lookup"><span data-stu-id="d5220-115">For details, see [Creating A Key Pair](../../standard/assembly/create-public-private-key-pair.md).</span></span>

### <a name="to-generate-a-primary-interop-assembly-using-tlbimpexe"></a><span data-ttu-id="d5220-116">使用 Tlbimp.exe 產生主要 Interop 組件</span><span class="sxs-lookup"><span data-stu-id="d5220-116">To generate a primary interop assembly using Tlbimp.exe</span></span>

1. <span data-ttu-id="d5220-117">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="d5220-117">At the command prompt, type:</span></span>

    <span data-ttu-id="d5220-118">**tlbimp** *tlbfile*  **/primary /keyfile:** *filename* **/out:** *assemblyname*</span><span class="sxs-lookup"><span data-stu-id="d5220-118">**tlbimp** *tlbfile*  **/primary /keyfile:** *filename* **/out:** *assemblyname*</span></span>

    <span data-ttu-id="d5220-119">在這個命令中，*tlbfile* 是含有 COM 類型程式庫的檔案，*filename* 是含有金鑰組的容器或檔案名稱，而 *assemblyname* 則是要簽署為強式名稱的組件名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-119">In this command, *tlbfile* is the file containing the COM type library, *filename* is the name of the container or file that contains the key pair, and *assemblyname* is the name of the assembly to sign with a strong name.</span></span>

<span data-ttu-id="d5220-120">主要 Interop 組件只能參考其他主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-120">Primary interop assemblies can reference only other primary interop assemblies.</span></span> <span data-ttu-id="d5220-121">如果您的組件參考來自協力廠商 COM 類型程式庫的類型，則您必須先從發行者取得主要 Interop 組件，才能產生主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-121">If your assembly references types from a third-party COM type library, you must obtain a primary interop assembly from the publisher before you can generate your primary interop assembly.</span></span> <span data-ttu-id="d5220-122">如果您是發行者，您必須先產生相依類別程式庫的主要 Interop 組件，才能產生參考的主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-122">If you are the publisher, you must generate a primary interop assembly for the dependent type library before generating the referencing primary interop assembly.</span></span>

<span data-ttu-id="d5220-123">安裝在目前的目錄時，無法探索與原始類型程式庫版本號碼不同的相依主要 Interop 組件。</span><span class="sxs-lookup"><span data-stu-id="d5220-123">A dependent primary interop assembly with a version number that differs from that of the original type library is not discoverable when installed in the current directory.</span></span> <span data-ttu-id="d5220-124">您必須在 Windows 登錄中登錄相依的主要 Interop 組件，或使用 **/reference** 選項，以確定 Tlbimp.exe 能找到相依的 DLL。</span><span class="sxs-lookup"><span data-stu-id="d5220-124">You must either register the dependent primary interop assembly in the Windows registry or use the **/reference** option to be sure that Tlbimp.exe finds the dependent DLL.</span></span>

<span data-ttu-id="d5220-125">您也可以包裝類型程式庫的多個版本。</span><span class="sxs-lookup"><span data-stu-id="d5220-125">You can also wrap multiple versions of a type library.</span></span> <span data-ttu-id="d5220-126">如需相關指示，請參閱[如何：包裝型別程式庫的多個版本](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/1565h6hc(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="d5220-126">For instructions, see [How to: Wrap Multiple Versions of Type Libraries](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/1565h6hc(v=vs.100)).</span></span>

## <a name="example"></a><span data-ttu-id="d5220-127">範例</span><span class="sxs-lookup"><span data-stu-id="d5220-127">Example</span></span>

<span data-ttu-id="d5220-128">下列範例會匯入 COM 類型程式庫  `LibUtil.tlb`，並使用金鑰檔案 `CompanyA.snk` 將組件 `LibUtil.dll` 簽署為強式名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-128">The following example imports the COM type library `LibUtil.tlb` and signs the assembly `LibUtil.dll` with a strong name using the key file `CompanyA.snk`.</span></span> <span data-ttu-id="d5220-129">藉由略過特定命名空間名稱，此範例會產生預設的命名空間 `LibUtil`。</span><span class="sxs-lookup"><span data-stu-id="d5220-129">By omitting a specific namespace name, this example produces the default namespace, `LibUtil`.</span></span>

```console
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /out:LibUtil.dll
```

<span data-ttu-id="d5220-130">如需更具描述性的名稱 (使用 *VendorName*.*LibraryName* 命名指導方針)，下列範例會覆寫預設組件檔案名稱和命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-130">For a more descriptive name (using the *VendorName*.*LibraryName* naming guideline), the following example overrides the default assembly file name and namespace name.</span></span>

```console
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /namespace:CompanyA.LibUtil /out:CompanyA.LibUtil.dll
```

<span data-ttu-id="d5220-131">下列範例會匯入 `MyLib.tlb`，它參考 `CompanyA.LibUtil.dll` 並使用金鑰檔案 `CompanyB.snk` 將組件 `CompanyB.MyLib.dll` 簽署為強式名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-131">The following example imports `MyLib.tlb`, which references `CompanyA.LibUtil.dll`, and signs the assembly `CompanyB.MyLib.dll` with a strong name using the key file `CompanyB.snk`.</span></span> <span data-ttu-id="d5220-132">命名空間 `CompanyB.MyLib` 會覆寫預設命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="d5220-132">The namespace, `CompanyB.MyLib`, overrides the default namespace name.</span></span>

```console
tlbimp MyLib.tlb /primary /keyfile:CompanyB.snk /namespace:CompanyB.MyLib /reference:CompanyA.LibUtil.dll /out:CompanyB.MyLib.dll
```

## <a name="see-also"></a><span data-ttu-id="d5220-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5220-133">See also</span></span>

- [<span data-ttu-id="d5220-134">作法：登錄主要 Interop 組件</span><span class="sxs-lookup"><span data-stu-id="d5220-134">How to: Register Primary Interop Assemblies</span></span>](how-to-register-primary-interop-assemblies.md)

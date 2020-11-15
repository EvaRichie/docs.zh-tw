---
title: dotnet store 命令
description: "'dotnet store' 命令會在執行階段套件存放區中儲存指定的組件。"
ms.date: 02/14/2020
ms.openlocfilehash: 8efb11c6bf648bc7787d5627e02b180abb8a0afd
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634333"
---
# <a name="dotnet-store"></a><span data-ttu-id="62d47-103">dotnet store</span><span class="sxs-lookup"><span data-stu-id="62d47-103">dotnet store</span></span>

<span data-ttu-id="62d47-104">本文 **適用于：** ✔️ .net CORE 2.x SDK 和更新版本</span><span class="sxs-lookup"><span data-stu-id="62d47-104">**This article applies to:** ✔️ .NET Core 2.x SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="62d47-105">名稱</span><span class="sxs-lookup"><span data-stu-id="62d47-105">Name</span></span>

<span data-ttu-id="62d47-106">`dotnet store` - 會在[執行階段套件存放區](../deploying/runtime-store.md)中儲存指定的組件。</span><span class="sxs-lookup"><span data-stu-id="62d47-106">`dotnet store` - Stores the specified assemblies in the [runtime package store](../deploying/runtime-store.md).</span></span>

## <a name="synopsis"></a><span data-ttu-id="62d47-107">概要</span><span class="sxs-lookup"><span data-stu-id="62d47-107">Synopsis</span></span>

```dotnetcli
dotnet store -m|--manifest <PATH_TO_MANIFEST_FILE>
    -f|--framework <FRAMEWORK_VERSION> -r|--runtime <RUNTIME_IDENTIFIER>
    [--framework-version <FRAMEWORK_VERSION>] [--output <OUTPUT_DIRECTORY>]
    [--skip-optimization] [--skip-symbols] [-v|--verbosity <LEVEL>]
    [--working-dir <WORKING_DIRECTORY>]

dotnet store -h|--help
```

## <a name="description"></a><span data-ttu-id="62d47-108">描述</span><span class="sxs-lookup"><span data-stu-id="62d47-108">Description</span></span>

<span data-ttu-id="62d47-109">`dotnet store` 會在[執行階段套件存放區](../deploying/runtime-store.md)中儲存指定的組件。</span><span class="sxs-lookup"><span data-stu-id="62d47-109">`dotnet store` stores the specified assemblies in the [runtime package store](../deploying/runtime-store.md).</span></span> <span data-ttu-id="62d47-110">根據預設，會針對目標執行階段和架構最佳化組件。</span><span class="sxs-lookup"><span data-stu-id="62d47-110">By default, assemblies are optimized for the target runtime and framework.</span></span> <span data-ttu-id="62d47-111">如需詳細資訊，請參閱[執行階段套件存放區](../deploying/runtime-store.md)主題。</span><span class="sxs-lookup"><span data-stu-id="62d47-111">For more information, see the [runtime package store](../deploying/runtime-store.md) topic.</span></span>

## <a name="required-options"></a><span data-ttu-id="62d47-112">必要選項</span><span class="sxs-lookup"><span data-stu-id="62d47-112">Required options</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="62d47-113">指定[目標 Framework](../../standard/frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="62d47-113">Specifies the [target framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="62d47-114">必須在專案檔中指定此目標架構。</span><span class="sxs-lookup"><span data-stu-id="62d47-114">The target framework has to be specified in the project file.</span></span>

- **`-m|--manifest <PATH_TO_MANIFEST_FILE>`**

  <span data-ttu-id="62d47-115">「套件存放區資訊清單檔」是 XML 檔，包含要儲存的套件清單。</span><span class="sxs-lookup"><span data-stu-id="62d47-115">The *package store manifest file* is an XML file that contains the list of packages to store.</span></span> <span data-ttu-id="62d47-116">資訊清單檔的格式相容於 SDK 樣式專案格式。</span><span class="sxs-lookup"><span data-stu-id="62d47-116">The format of the manifest file is compatible with the SDK-style project format.</span></span> <span data-ttu-id="62d47-117">因此，參考所需套件的專案檔可以搭配 `-m|--manifest` 選項，將組件儲存在執行階段套件存放區中。</span><span class="sxs-lookup"><span data-stu-id="62d47-117">So, a project file that references the desired packages can be used with the `-m|--manifest` option to store assemblies in the runtime package store.</span></span> <span data-ttu-id="62d47-118">若要指定多個資訊清單檔，請為每個檔案重複選項和路徑。</span><span class="sxs-lookup"><span data-stu-id="62d47-118">To specify multiple manifest files, repeat the option and path for each file.</span></span> <span data-ttu-id="62d47-119">例如：`--manifest packages1.csproj --manifest packages2.csproj`。</span><span class="sxs-lookup"><span data-stu-id="62d47-119">For example: `--manifest packages1.csproj --manifest packages2.csproj`.</span></span>

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  <span data-ttu-id="62d47-120">要設為目標的 [執行時間識別碼](../rid-catalog.md) 。</span><span class="sxs-lookup"><span data-stu-id="62d47-120">The [runtime identifier](../rid-catalog.md) to target.</span></span>

## <a name="optional-options"></a><span data-ttu-id="62d47-121">選擇性的選項</span><span class="sxs-lookup"><span data-stu-id="62d47-121">Optional options</span></span>

- **`--framework-version <FRAMEWORK_VERSION>`**

  <span data-ttu-id="62d47-122">指定 .NET SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="62d47-122">Specifies the .NET SDK version.</span></span> <span data-ttu-id="62d47-123">此選項可讓您在 `-f|--framework` 選項指定的 Framework 之外，選取特定的 Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="62d47-123">This option enables you to select a specific framework version beyond the framework specified by the `-f|--framework` option.</span></span>

- **`-h|--help`**

  <span data-ttu-id="62d47-124">顯示說明資訊。</span><span class="sxs-lookup"><span data-stu-id="62d47-124">Shows help information.</span></span>

- **`-o|--output <OUTPUT_DIRECTORY>`**

  <span data-ttu-id="62d47-125">指定執行階段套件存放區的路徑。</span><span class="sxs-lookup"><span data-stu-id="62d47-125">Specifies the path to the runtime package store.</span></span> <span data-ttu-id="62d47-126">如果未指定，則會預設為使用者設定檔 .NET 安裝目錄的 *儲存* 子目錄。</span><span class="sxs-lookup"><span data-stu-id="62d47-126">If not specified, it defaults to the *store* subdirectory of the user profile .NET installation directory.</span></span>

- **`--skip-optimization`**

  <span data-ttu-id="62d47-127">略過最佳化階段。</span><span class="sxs-lookup"><span data-stu-id="62d47-127">Skips the optimization phase.</span></span>

- **`--skip-symbols`**

  <span data-ttu-id="62d47-128">略過符號產生。</span><span class="sxs-lookup"><span data-stu-id="62d47-128">Skips symbol generation.</span></span> <span data-ttu-id="62d47-129">目前，只能在 Windows 和 Linux 產生符號。</span><span class="sxs-lookup"><span data-stu-id="62d47-129">Currently, you can only generate symbols on Windows and Linux.</span></span>

- **`-v|--verbosity <LEVEL>`**

  <span data-ttu-id="62d47-130">設定命令的詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="62d47-130">Sets the verbosity level of the command.</span></span> <span data-ttu-id="62d47-131">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="62d47-131">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span>

- **`-w|--working-dir <WORKING_DIRECTORY>`**

  <span data-ttu-id="62d47-132">命令使用的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="62d47-132">The working directory used by the command.</span></span> <span data-ttu-id="62d47-133">如未指定，則使用目前目錄的 *obj* 子目錄。</span><span class="sxs-lookup"><span data-stu-id="62d47-133">If not specified, it uses the *obj* subdirectory of the current directory.</span></span>

## <a name="examples"></a><span data-ttu-id="62d47-134">範例</span><span class="sxs-lookup"><span data-stu-id="62d47-134">Examples</span></span>

- <span data-ttu-id="62d47-135">儲存 .NET Core 2.0.0 的 *packages.csproj* 專案中指定的套件：</span><span class="sxs-lookup"><span data-stu-id="62d47-135">Store the packages specified in the *packages.csproj* project file for .NET Core 2.0.0:</span></span>

  ```dotnetcli
  dotnet store --manifest packages.csproj --framework-version 2.0.0
  ```

- <span data-ttu-id="62d47-136">儲存 *packages.csproj* 中指定的套件，不需要最佳化：</span><span class="sxs-lookup"><span data-stu-id="62d47-136">Store the packages specified in the *packages.csproj* without optimization:</span></span>

  ```dotnetcli
  dotnet store --manifest packages.csproj --skip-optimization
  ```

## <a name="see-also"></a><span data-ttu-id="62d47-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="62d47-137">See also</span></span>

- [<span data-ttu-id="62d47-138">執行階段套件存放區</span><span class="sxs-lookup"><span data-stu-id="62d47-138">Runtime package store</span></span>](../deploying/runtime-store.md)

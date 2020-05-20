---
title: 在 Ubuntu 20.04 套件管理員上安裝 .NET Core-.NET Core
description: 使用套件管理員在 Ubuntu 20.04 上安裝 .NET Core SDK 和執行時間。
author: thraka
ms.author: adegeo
ms.date: 05/13/2020
ms.openlocfilehash: 4d7d7ee9117314ef360097fee929f24943c7a7f2
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83619285"
---
# <a name="ubuntu-2004-package-manager---install-net-core"></a><span data-ttu-id="f6911-103">Ubuntu 20.04 套件管理員-安裝 .NET Core</span><span class="sxs-lookup"><span data-stu-id="f6911-103">Ubuntu 20.04 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

<span data-ttu-id="f6911-104">本文說明如何使用套件管理員在 Ubuntu 20.04 上安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="f6911-104">This article describes how to use a package manager to install .NET Core on Ubuntu 20.04.</span></span>

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="add-microsoft-repository-key-and-feed"></a><span data-ttu-id="f6911-105">新增 Microsoft 存放庫金鑰和摘要</span><span class="sxs-lookup"><span data-stu-id="f6911-105">Add Microsoft repository key and feed</span></span>

<span data-ttu-id="f6911-106">安裝 .NET 之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="f6911-106">Before installing .NET, you'll need to:</span></span>

- <span data-ttu-id="f6911-107">將 Microsoft 封裝簽署金鑰新增至受信任的金鑰清單。</span><span class="sxs-lookup"><span data-stu-id="f6911-107">Add the Microsoft package signing key to the list of trusted keys.</span></span>
- <span data-ttu-id="f6911-108">將存放庫新增至套件管理員。</span><span class="sxs-lookup"><span data-stu-id="f6911-108">Add the repository to the package manager.</span></span>
- <span data-ttu-id="f6911-109">安裝必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="f6911-109">Install required dependencies.</span></span>

<span data-ttu-id="f6911-110">每部電腦只需要執行這項作業一次。</span><span class="sxs-lookup"><span data-stu-id="f6911-110">This only needs to be done once per machine.</span></span>

<span data-ttu-id="f6911-111">開啟終端機並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f6911-111">Open a terminal and run the following commands.</span></span>

```bash
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="f6911-112">安裝 .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="f6911-112">Install the .NET Core SDK</span></span>

<span data-ttu-id="f6911-113">更新可供安裝的產品，然後安裝 .NET Core SDK。</span><span class="sxs-lookup"><span data-stu-id="f6911-113">Update the products available for installation, then install the .NET Core SDK.</span></span> <span data-ttu-id="f6911-114">在您的終端機中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f6911-114">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="f6911-115">如果您收到類似 [**找不到封裝 dotnet-sdk-3.1**] 的錯誤訊息，請參閱[疑難排解套件管理員](#troubleshoot-the-package-manager)一節。</span><span class="sxs-lookup"><span data-stu-id="f6911-115">If you receive an error message similar to **Unable to locate package dotnet-sdk-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="f6911-116">安裝 ASP.NET Core 執行時間</span><span class="sxs-lookup"><span data-stu-id="f6911-116">Install the ASP.NET Core runtime</span></span>

<span data-ttu-id="f6911-117">更新可供安裝的產品，然後安裝 ASP.NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="f6911-117">Update the products available for installation, then install the ASP.NET Core runtime.</span></span> <span data-ttu-id="f6911-118">在您的終端機中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f6911-118">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install aspnetcore-runtime-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="f6911-119">如果您收到類似 [**找不到封裝 aspnetcore-執行時間-3.1**] 的錯誤訊息，請參閱[疑難排解封裝管理員](#troubleshoot-the-package-manager)一節。</span><span class="sxs-lookup"><span data-stu-id="f6911-119">If you receive an error message similar to **Unable to locate package aspnetcore-runtime-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="f6911-120">安裝 .NET Core 執行時間</span><span class="sxs-lookup"><span data-stu-id="f6911-120">Install the .NET Core runtime</span></span>

<span data-ttu-id="f6911-121">更新可供安裝的產品，然後安裝 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="f6911-121">Update the products available for installation, then install the .NET Core runtime.</span></span> <span data-ttu-id="f6911-122">在您的終端機中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f6911-122">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-runtime-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="f6911-123">如果您收到類似 [**找不到封裝 dotnet-執行時間-3.1**] 的錯誤訊息，請參閱[疑難排解封裝管理員](#troubleshoot-the-package-manager)一節。</span><span class="sxs-lookup"><span data-stu-id="f6911-123">If you receive an error message similar to **Unable to locate package dotnet-runtime-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="f6911-124">如何安裝其他版本</span><span class="sxs-lookup"><span data-stu-id="f6911-124">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="f6911-125">針對套件管理員進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f6911-125">Troubleshoot the package manager</span></span>

<span data-ttu-id="f6911-126">本節提供使用封裝管理員安裝 .NET Core 時，可能會收到的常見錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="f6911-126">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="unable-to-locate"></a><span data-ttu-id="f6911-127">找不到</span><span class="sxs-lookup"><span data-stu-id="f6911-127">Unable to locate</span></span>

<span data-ttu-id="f6911-128">如果您收到類似「**找不到封裝 {.Net Core 封裝}**」的錯誤訊息，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f6911-128">If you receive an error message similar to **Unable to locate package {the .NET Core package}**, run the following commands.</span></span>

```bash
sudo dpkg --purge packages-microsoft-prod && sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install {the .NET Core package}
```

<span data-ttu-id="f6911-129">如果無法解決問題，您可以使用下列命令來執行手動安裝。</span><span class="sxs-lookup"><span data-stu-id="f6911-129">If that doesn't work, you can run a manual install with the following commands.</span></span>

```bash
sudo apt-get install -y gpg
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/ubuntu/20.04/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
sudo apt-get install -y apt-transport-https
sudo apt-get update
sudo apt-get install {the .NET Core package}
```

### <a name="failed-to-fetch"></a><span data-ttu-id="f6911-130">無法提取</span><span class="sxs-lookup"><span data-stu-id="f6911-130">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-deb](includes/package-manager-failed-to-fetch-deb.md)]

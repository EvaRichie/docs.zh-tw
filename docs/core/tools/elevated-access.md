---
title: Dotnet 命令的提升存取權限
description: 了解適用於需要提升存取權限的 dotnet 命令最佳做法。
author: wli3
ms.date: 06/26/2019
ms.openlocfilehash: b34a4d631ec0e5ef641e1ffbc91e081d25645157
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634047"
---
# <a name="elevated-access-for-dotnet-commands"></a><span data-ttu-id="66f0c-103">Dotnet 命令的提升存取權限</span><span class="sxs-lookup"><span data-stu-id="66f0c-103">Elevated access for dotnet commands</span></span>

<span data-ttu-id="66f0c-104">軟體開發最佳做法會引導開發人員撰寫需要最少權限的軟體。</span><span class="sxs-lookup"><span data-stu-id="66f0c-104">Software development best practices guide developers to writing software that requires the least amount of privilege.</span></span> <span data-ttu-id="66f0c-105">但是，由於作業系統規則，有些軟體 (例如效能監視工具) 會需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="66f0c-105">However, some software, like performance monitoring tools, requires admin permission because of operating system rules.</span></span> <span data-ttu-id="66f0c-106">下列指導會描述使用 .NET Core 撰寫這類軟體時的支援案例。</span><span class="sxs-lookup"><span data-stu-id="66f0c-106">The following guidance describes supported scenarios for writing such software with .NET Core.</span></span>

<span data-ttu-id="66f0c-107">下列命令可以提升的權限來執行：</span><span class="sxs-lookup"><span data-stu-id="66f0c-107">The following commands can be run elevated:</span></span>

- <span data-ttu-id="66f0c-108">`dotnet tool` 命令，例如 [dotnet tool install](dotnet-tool-install.md)。</span><span class="sxs-lookup"><span data-stu-id="66f0c-108">`dotnet tool` commands, such as [dotnet tool install](dotnet-tool-install.md).</span></span>
- `dotnet run --no-build`
- `dotnet-core-uninstall`

<span data-ttu-id="66f0c-109">我們不建議執行其他提升的權限命令。</span><span class="sxs-lookup"><span data-stu-id="66f0c-109">We don't recommend running other commands elevated.</span></span> <span data-ttu-id="66f0c-110">特別是，我們不建議針對使用 MSBuild 的命令提升權限，例如 [dotnet restore](dotnet-restore.md)、[dotnet build](dotnet-build.md) 和 [dotnet run](dotnet-run.md)。</span><span class="sxs-lookup"><span data-stu-id="66f0c-110">In particular, we don't recommend elevation with commands that use MSBuild, such as [dotnet restore](dotnet-restore.md), [dotnet build](dotnet-build.md), and [dotnet run](dotnet-run.md).</span></span> <span data-ttu-id="66f0c-111">主要問題是使用者在發出 dotnet 命令後，在根及限制帳戶之間來回轉換時的權限管理問題。</span><span class="sxs-lookup"><span data-stu-id="66f0c-111">The primary issue is permission management problems when a user transitions back and forth between root and a restricted account after issuing dotnet commands.</span></span> <span data-ttu-id="66f0c-112">您可能會發現作為限制的使用者，您無法存取由根使用者建置的檔案。</span><span class="sxs-lookup"><span data-stu-id="66f0c-112">You may find as a restricted user that you don't have access to the file built by a root user.</span></span> <span data-ttu-id="66f0c-113">雖然有數種方法可以解決這種情況，但您從一開始其實就可以避免它們。</span><span class="sxs-lookup"><span data-stu-id="66f0c-113">There are ways to resolve this situation, but they're unnecessary to get into in the first place.</span></span>

<span data-ttu-id="66f0c-114">只要您不是在根和受限帳戶之間來回轉換，您就可以將命令以 root 的形式執行。</span><span class="sxs-lookup"><span data-stu-id="66f0c-114">You can run commands as root as long as you don't transition back and forth between root and a restricted account.</span></span> <span data-ttu-id="66f0c-115">例如，根據預設 Docker 容器會以根帳戶執行，因此它們便具有這種特性。</span><span class="sxs-lookup"><span data-stu-id="66f0c-115">For example, Docker containers run as root by default, so they have this characteristic.</span></span>

## <a name="global-tool-installation"></a><span data-ttu-id="66f0c-116">全域工具安裝</span><span class="sxs-lookup"><span data-stu-id="66f0c-116">Global tool installation</span></span>

<span data-ttu-id="66f0c-117">下列指示示範安裝、執行和卸載需要提高許可權來執行之 .NET 工具的建議方式。</span><span class="sxs-lookup"><span data-stu-id="66f0c-117">The following instructions demonstrate the recommended way to install, run, and uninstall .NET tools that require elevated permissions to execute.</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="windows"></a>[<span data-ttu-id="66f0c-118">Windows</span><span class="sxs-lookup"><span data-stu-id="66f0c-118">Windows</span></span>](#tab/windows)

### <a name="install-the-tool"></a><span data-ttu-id="66f0c-119">安裝工具</span><span class="sxs-lookup"><span data-stu-id="66f0c-119">Install the tool</span></span>

<span data-ttu-id="66f0c-120">若資料夾 `%ProgramFiles%\dotnet-tools` 已存在，請執行下列操作來檢查 "Users" 群組是否有寫入或修改該目錄的權限：</span><span class="sxs-lookup"><span data-stu-id="66f0c-120">If the folder `%ProgramFiles%\dotnet-tools` already exists, do the following to check whether the "Users" group has permission to write or modify that directory:</span></span>

- <span data-ttu-id="66f0c-121">以滑鼠右鍵按一下 `%ProgramFiles%\dotnet-tools` 資料夾，然後選取 [ **屬性** ]。</span><span class="sxs-lookup"><span data-stu-id="66f0c-121">Right-click the `%ProgramFiles%\dotnet-tools` folder and select **Properties**.</span></span> <span data-ttu-id="66f0c-122">[通用屬性] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="66f0c-122">The **Common Properties** dialog box opens.</span></span>
- <span data-ttu-id="66f0c-123">選取 [ **安全性** ] 索引標籤。在 [ **群組或使用者名稱** ] 底下，檢查 "Users" 群組是否有寫入或修改目錄的許可權。</span><span class="sxs-lookup"><span data-stu-id="66f0c-123">Select the **Security** tab. Under **Group or user names** , check whether the "Users" group has permission to write or modify the directory.</span></span>
- <span data-ttu-id="66f0c-124">若 "Users" 群組可以寫入或修改目錄，請在安裝工具時使用不同的目錄名稱，而非 *dotnet-tools* 。</span><span class="sxs-lookup"><span data-stu-id="66f0c-124">If the "Users" group can write or modify the directory, use a different directory name when installing the tools rather than *dotnet-tools*.</span></span>

<span data-ttu-id="66f0c-125">若要安裝工具，請以提升權限的命令提示字元來執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="66f0c-125">To install tools, run the following command in elevated prompt.</span></span> <span data-ttu-id="66f0c-126">它會在安裝期間建立 *dotnet-tools* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="66f0c-126">It will create the *dotnet-tools* folder during the installation.</span></span>

```dotnetcli
dotnet tool install PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools".
```

### <a name="run-the-global-tool"></a><span data-ttu-id="66f0c-127">執行全域工具</span><span class="sxs-lookup"><span data-stu-id="66f0c-127">Run the global tool</span></span>

<span data-ttu-id="66f0c-128">**選項 1** ：搭配提升權限的命令提示字元使用完整路徑：</span><span class="sxs-lookup"><span data-stu-id="66f0c-128">**Option 1** Use the full path with elevated prompt:</span></span>

```cmd
"%ProgramFiles%\dotnet-tools\TOOLCOMMAND"
```

<span data-ttu-id="66f0c-129">**選項 2** ：將新建立的資料夾新增到 `%Path%`。</span><span class="sxs-lookup"><span data-stu-id="66f0c-129">**Option 2** Add the newly created folder to `%Path%`.</span></span> <span data-ttu-id="66f0c-130">您只需要執行此作業一次。</span><span class="sxs-lookup"><span data-stu-id="66f0c-130">You only need to do this operation once.</span></span>

```cmd
setx Path "%Path%;%ProgramFiles%\dotnet-tools\"
```

<span data-ttu-id="66f0c-131">然後使用以下項目執行：</span><span class="sxs-lookup"><span data-stu-id="66f0c-131">And run with:</span></span>

```cmd
TOOLCOMMAND
```

### <a name="uninstall-the-global-tool"></a><span data-ttu-id="66f0c-132">解除安裝全域工具</span><span class="sxs-lookup"><span data-stu-id="66f0c-132">Uninstall the global tool</span></span>

<span data-ttu-id="66f0c-133">在提升權限的命令提示字元中，鍵入下列命令：</span><span class="sxs-lookup"><span data-stu-id="66f0c-133">In an elevated prompt, type the following command:</span></span>

```dotnetcli
dotnet tool uninstall PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools"
```

# <a name="linux"></a>[<span data-ttu-id="66f0c-134">Linux</span><span class="sxs-lookup"><span data-stu-id="66f0c-134">Linux</span></span>](#tab/linux)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

# <a name="macos"></a>[<span data-ttu-id="66f0c-135">macOS</span><span class="sxs-lookup"><span data-stu-id="66f0c-135">macOS</span></span>](#tab/macos)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

---

## <a name="local-tools"></a><span data-ttu-id="66f0c-136">本機工具</span><span class="sxs-lookup"><span data-stu-id="66f0c-136">Local tools</span></span>

<span data-ttu-id="66f0c-137">本機工具範圍會限制在每一位使用者的每個子樹狀目錄中。</span><span class="sxs-lookup"><span data-stu-id="66f0c-137">Local tools are scoped per subdirectory tree, per user.</span></span> <span data-ttu-id="66f0c-138">以提升的權限執行時，本機工具會將受限制使用者環境共用到提升權限的環境。</span><span class="sxs-lookup"><span data-stu-id="66f0c-138">When run elevated, local tools share a restricted user environment to the elevated environment.</span></span> <span data-ttu-id="66f0c-139">在 Linux 和 macOS 中，這會導致以僅限根使用者的存取來設定檔案。</span><span class="sxs-lookup"><span data-stu-id="66f0c-139">In Linux and macOS, this results in files being set with root user-only access.</span></span> <span data-ttu-id="66f0c-140">若使用者切換回限制的帳戶，使用者便無法繼續存取或寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="66f0c-140">If the user switches back to a restricted account, the user can no longer access or write to the files.</span></span> <span data-ttu-id="66f0c-141">因此，我們不建議將需要提升權限的工具作為本機工具安裝。</span><span class="sxs-lookup"><span data-stu-id="66f0c-141">So installing tools that require elevation as local tools isn't recommended.</span></span> <span data-ttu-id="66f0c-142">請改為使用 `--tool-path` 選項及先前適用於全域工具的指導方針。</span><span class="sxs-lookup"><span data-stu-id="66f0c-142">Instead, use the `--tool-path` option and the previous guidelines for global tools.</span></span>

## <a name="elevation-during-development"></a><span data-ttu-id="66f0c-143">開發期間的提升權限</span><span class="sxs-lookup"><span data-stu-id="66f0c-143">Elevation during development</span></span>

<span data-ttu-id="66f0c-144">在開發期間，您可能需要提升的存取權限來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="66f0c-144">During development, you may need elevated access to test your application.</span></span> <span data-ttu-id="66f0c-145">例如，針對 IoT 應用程式，此案例相當常見。</span><span class="sxs-lookup"><span data-stu-id="66f0c-145">This scenario is common for IoT apps, for example.</span></span> <span data-ttu-id="66f0c-146">我們建議您在不使用提升權限的情況下建置應用程式，然後使用提升權限來執行它。</span><span class="sxs-lookup"><span data-stu-id="66f0c-146">We recommend that you build the application without elevation and then run it with elevation.</span></span> <span data-ttu-id="66f0c-147">有數種模式可以進行此操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f0c-147">There are a few patterns, as follows:</span></span>

- <span data-ttu-id="66f0c-148">使用產生的可執行檔 (它可提供最佳的啟動效能)：</span><span class="sxs-lookup"><span data-stu-id="66f0c-148">Using generated executable (it provides the best startup performance):</span></span>

   ```dotnetcli
   dotnet build
   sudo ./bin/Debug/netcoreapp3.0/APPLICATIONNAME
   ```

- <span data-ttu-id="66f0c-149">搭配 `—no-build` 旗標使用 [dotnet run](dotnet-run.md) 來避免產生新的二進位檔案：</span><span class="sxs-lookup"><span data-stu-id="66f0c-149">Using the [dotnet run](dotnet-run.md) command with the `—no-build` flag to avoid generating new binaries:</span></span>

   ```dotnetcli
   dotnet build
   sudo dotnet run --no-build
   ```

## <a name="see-also"></a><span data-ttu-id="66f0c-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66f0c-150">See also</span></span>

- [<span data-ttu-id="66f0c-151">.NET 工具總覽</span><span class="sxs-lookup"><span data-stu-id="66f0c-151">.NET tools overview</span></span>](global-tools.md)

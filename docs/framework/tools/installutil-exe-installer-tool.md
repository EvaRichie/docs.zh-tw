---
title: Installutil.exe (安裝程式工具)
description: 使用安裝程式工具 Installutil.exe。 這項工具可讓您在指定的元件中執行安裝程式元件，以安裝或卸載伺服器資源。
ms.date: 03/30/2017
helpviewer_keywords:
- uninstalling server resources
- removing server resources
- status information for installation
- installation progress reports
- installing server resources
- Installer tool
- Installutil.exe
- files, Installer tool
- progress information for installation
- reporting installation progress
ms.assetid: 3f9d0533-f895-4897-b4ea-528284e0241d
ms.openlocfilehash: 042e5f64a7a863173db9c4e601d3152b0df46d97
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164443"
---
# <a name="installutilexe-installer-tool"></a><span data-ttu-id="0aa7a-104">Installutil.exe (安裝程式工具)</span><span class="sxs-lookup"><span data-stu-id="0aa7a-104">Installutil.exe (Installer Tool)</span></span>

<span data-ttu-id="0aa7a-105">安裝程式工具是一種命令列公用程式，可讓您透過執行指定之組件中的安裝程式元件，來安裝和解除安裝伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-105">The Installer tool is a command-line utility that allows you to install and uninstall server resources by executing the installer components in specified assemblies.</span></span> <span data-ttu-id="0aa7a-106">這個工具可以與 <xref:System.Configuration.Install> 命名空間中的類別一起使用。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-106">This tool works in conjunction with classes in the <xref:System.Configuration.Install> namespace.</span></span>

<span data-ttu-id="0aa7a-107">此工具會自動與 Visual Studio 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-107">This tool is automatically installed with Visual Studio.</span></span> <span data-ttu-id="0aa7a-108">若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-108">To run the tool, use the Developer Command Prompt for Visual Studio (or the Visual Studio Command Prompt in Windows 7).</span></span> <span data-ttu-id="0aa7a-109">如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-109">For more information, see [Command Prompts](developer-command-prompt-for-vs.md).</span></span>

<span data-ttu-id="0aa7a-110">在命令提示字元中，請輸入下列項目：</span><span class="sxs-lookup"><span data-stu-id="0aa7a-110">At the command prompt, type the following:</span></span>

## <a name="syntax"></a><span data-ttu-id="0aa7a-111">語法</span><span class="sxs-lookup"><span data-stu-id="0aa7a-111">Syntax</span></span>

```console
installutil [/u[ninstall]] [options] assembly [[options] assembly] ...
```

## <a name="parameters"></a><span data-ttu-id="0aa7a-112">參數</span><span class="sxs-lookup"><span data-stu-id="0aa7a-112">Parameters</span></span>

|<span data-ttu-id="0aa7a-113">引數</span><span class="sxs-lookup"><span data-stu-id="0aa7a-113">Argument</span></span>|<span data-ttu-id="0aa7a-114">描述</span><span class="sxs-lookup"><span data-stu-id="0aa7a-114">Description</span></span>|
|--------------|-----------------|
|`assembly`|<span data-ttu-id="0aa7a-115">要執行安裝程式元件之組件的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-115">The file name of the assembly in which to execute the installer components.</span></span> <span data-ttu-id="0aa7a-116">如果您要使用 `/AssemblyName` 選項指定組件的強式名稱，請略過此參數。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-116">Omit this parameter if you want to specify the assembly's strong name by using the `/AssemblyName` option.</span></span>|

<a name="options"></a>

## <a name="options"></a><span data-ttu-id="0aa7a-117">選項。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-117">Options</span></span>

|<span data-ttu-id="0aa7a-118">選項</span><span class="sxs-lookup"><span data-stu-id="0aa7a-118">Option</span></span>|<span data-ttu-id="0aa7a-119">描述</span><span class="sxs-lookup"><span data-stu-id="0aa7a-119">Description</span></span>|
|------------|-----------------|
|`/h[elp]`<br /><br /> <span data-ttu-id="0aa7a-120">-或-</span><span class="sxs-lookup"><span data-stu-id="0aa7a-120">-or-</span></span><br /><br /> `/?`|<span data-ttu-id="0aa7a-121">顯示工具的命令語法和選項。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-121">Displays command syntax and options for the tool.</span></span>|
|<span data-ttu-id="0aa7a-122">`/help`*元件*</span><span class="sxs-lookup"><span data-stu-id="0aa7a-122">`/help` *assembly*</span></span><br /><br /> <span data-ttu-id="0aa7a-123">-或-</span><span class="sxs-lookup"><span data-stu-id="0aa7a-123">-or-</span></span><br /><br /> <span data-ttu-id="0aa7a-124">`/?`*元件*</span><span class="sxs-lookup"><span data-stu-id="0aa7a-124">`/?` *assembly*</span></span>|<span data-ttu-id="0aa7a-125">顯示指定之組件中的個別安裝程式所辨識的其他選項，以及 InstallUtil.exe 的指令語法和選項。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-125">Displays additional options recognized by individual installers within the specified assembly, along with command syntax and options for InstallUtil.exe.</span></span> <span data-ttu-id="0aa7a-126">這個選項會將每個安裝程式元件之 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 屬性所傳回的文字加入至 InstallUtil.exe 的説明文字。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-126">This option adds the text returned by each installer component's <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> property to the help text of InstallUtil.exe.</span></span>|
|<span data-ttu-id="0aa7a-127">`/AssemblyName`「*assemblyName*</span><span class="sxs-lookup"><span data-stu-id="0aa7a-127">`/AssemblyName` "*assemblyName*</span></span><br /><br /> <span data-ttu-id="0aa7a-128">,Version=*major.minor.build.revision*</span><span class="sxs-lookup"><span data-stu-id="0aa7a-128">,Version=*major.minor.build.revision*</span></span><br /><br /> <span data-ttu-id="0aa7a-129">,Culture=*locale*</span><span class="sxs-lookup"><span data-stu-id="0aa7a-129">,Culture=*locale*</span></span><br /><br /> <span data-ttu-id="0aa7a-130">,PublicKeyToken=*publicKeyToken*"</span><span class="sxs-lookup"><span data-stu-id="0aa7a-130">,PublicKeyToken=*publicKeyToken*"</span></span>|<span data-ttu-id="0aa7a-131">指定組件的強式名稱，必須在全域組件快取中登錄此名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-131">Specifies the strong name of an assembly, which must be registered in the global assembly cache.</span></span> <span data-ttu-id="0aa7a-132">您必須利用組件的版本、文化特性 (Culture) 和公開金鑰語彙基元 (Token) 以完整限定組件名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-132">The assembly name must be fully qualified with the version, culture, and public key token of the assembly.</span></span> <span data-ttu-id="0aa7a-133">必須以引號括住完整名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-133">The fully qualified name must be surrounded by quotes.</span></span><br /><br /> <span data-ttu-id="0aa7a-134">例如，"myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0" 就是完整的組件名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-134">For example, "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0" is a fully qualified assembly name.</span></span>|
|<span data-ttu-id="0aa7a-135">`/InstallStateDir=[`*directoryName*`]`</span><span class="sxs-lookup"><span data-stu-id="0aa7a-135">`/InstallStateDir=[` *directoryName* `]`</span></span>|<span data-ttu-id="0aa7a-136">指定 .InstallState 檔案的目錄，其中包含用於解除安裝組件的資料。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-136">Specifies the directory of the .InstallState file that contains the data used to uninstall the assembly.</span></span> <span data-ttu-id="0aa7a-137">預設是包含組件的目錄。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-137">The default is the directory that contains the assembly.</span></span>|
|<span data-ttu-id="0aa7a-138">`/LogFile=`[*filename*]</span><span class="sxs-lookup"><span data-stu-id="0aa7a-138">`/LogFile=`[*filename*]</span></span>|<span data-ttu-id="0aa7a-139">指定記錄安裝進度的記錄檔名稱。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-139">Specifies the name of the log file where installation progress is recorded.</span></span> <span data-ttu-id="0aa7a-140">預設情況下，如果省略 `/LogFile` 選項，則會建立名為 *assemblyname*.InstallLog 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-140">By default, if the `/LogFile` option is omitted, a log file named *assemblyname*.InstallLog is created.</span></span> <span data-ttu-id="0aa7a-141">如果省略 *filename*，則不會產生任何記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-141">If *filename* is omitted, no log file is generated.</span></span>|
|<span data-ttu-id="0aa7a-142">`/LogToConsole`={`true`&#124;`false`}</span><span class="sxs-lookup"><span data-stu-id="0aa7a-142">`/LogToConsole`={`true`&#124;`false`}</span></span>|<span data-ttu-id="0aa7a-143">如果為 `true`，則會在主控台顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-143">If `true`, displays output to the console.</span></span> <span data-ttu-id="0aa7a-144">如果為 `false` (預設值)，則隱藏對主控台的輸出。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-144">If `false` (the default), suppresses output to the console.</span></span>|
|`/ShowCallStack`|<span data-ttu-id="0aa7a-145">如果在安裝期間的任何時間點上發生例外狀況，則將呼叫堆疊輸出到記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-145">Outputs the call stack to the log file if an exception occurs at any point during installation.</span></span>|
|<span data-ttu-id="0aa7a-146">`/u`[`ninstall`]</span><span class="sxs-lookup"><span data-stu-id="0aa7a-146">`/u`[`ninstall`]</span></span>|<span data-ttu-id="0aa7a-147">解除安裝指定的組件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-147">Uninstalls the specified assemblies.</span></span> <span data-ttu-id="0aa7a-148">不同於其他選項，`/u` 會套用至所有組件 (與選項出現在命令列上的位置無關)。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-148">Unlike the other options, `/u` applies to all assemblies regardless of where the option appears on the command line.</span></span>|

<a name="cmdline"></a>

## <a name="additional-installer-options"></a><span data-ttu-id="0aa7a-149">其他安裝程式選項</span><span class="sxs-lookup"><span data-stu-id="0aa7a-149">Additional Installer Options</span></span>

<span data-ttu-id="0aa7a-150">組件中使用的個別安裝程式可能會辨識列在[選項](#options)區段以外的選項。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-150">Individual installers used within an assembly may recognize options in addition to those listed in the [Options](#options) section.</span></span> <span data-ttu-id="0aa7a-151">若要了解這些選項，請在命令列上使用組件路徑搭配 `/?` 或 `/help` 選項以執行 InstallUtil.exe。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-151">To learn about these options, run InstallUtil.exe with the paths of the assemblies on the command line along with the `/?` or `/help` option.</span></span> <span data-ttu-id="0aa7a-152">若要指定這些選項，請在命令列上將這些選項與 InstallUtil.exe 辨識的選項包含在一起。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-152">To specify these options, you include them on the command line along with the options recognized by InstallUtil.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa7a-153">個別安裝程式元件所支援之選項上的說明文字由 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 屬性傳回。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-153">Help text on the options supported by individual installer components is returned by the <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="0aa7a-154">已經在命令列上輸入的個別選項可透過程式設計方式從 <xref:System.Configuration.Install.Installer.Context%2A?displayProperty=nameWithType> 屬性中存取。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-154">The individual options that have been entered on the command line are accessible programmatically from the <xref:System.Configuration.Install.Installer.Context%2A?displayProperty=nameWithType> property.</span></span>

<span data-ttu-id="0aa7a-155">所有選項和命令列參數皆會寫入安裝記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-155">All options and command-line parameters are written to the installation log file.</span></span> <span data-ttu-id="0aa7a-156">但是，如果您使用某些安裝程式元件可識別的 `/Password` 參數，則會以八個星號 (\*) 取代密碼資訊，因此密碼不會出現在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-156">However, if you use the `/Password` parameter, which is recognized by some installer components, the password information will be replaced by eight asterisks (\*) and will not appear in the log file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0aa7a-157">在某些情況下，傳遞給安裝程式的參數可能包含機密或可識別個人身分的資訊，這些資訊預設是寫入到純文字的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-157">In some cases, parameters passed to the installer may include sensitive or personally identifiable information, which, by default, is written to a plain text log file.</span></span> <span data-ttu-id="0aa7a-158">若要防止這個行為，您可以在命令列上的 Installutil.exe 後面指定 `/LogFile=` (不含 *filename* 引數) 以隱藏記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-158">To prevent this behavior, you can suppress the log file by specifying `/LogFile=` (with no *filename* argument) after Installutil.exe on the command line.</span></span>

## <a name="remarks"></a><span data-ttu-id="0aa7a-159">備註</span><span class="sxs-lookup"><span data-stu-id="0aa7a-159">Remarks</span></span>

<span data-ttu-id="0aa7a-160">.NET Framework 應用程式由傳統的程式檔和關聯的資源組成，例如訊息佇列、事件記錄檔，以及部署應用程式時所必須建立的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-160">.NET Framework applications consist of traditional program files and associated resources, such as message queues, event logs, and performance counters that must be created when the application is deployed.</span></span> <span data-ttu-id="0aa7a-161">安裝應用程式時，您可以使用組件的安裝元件來建立這些資源，並在解除安裝應用程式時移除它們。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-161">You can use an assembly's installer components to create these resources when your application is installed and to remove them when your application is uninstalled.</span></span> <span data-ttu-id="0aa7a-162">Installutil.exe 會偵測並執行這些安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-162">Installutil.exe detects and executes these installer components.</span></span>

<span data-ttu-id="0aa7a-163">您可以在相同命令列上指定多個組件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-163">You can specify multiple assemblies on the same command line.</span></span> <span data-ttu-id="0aa7a-164">任何出現在組件名稱之前的選項都會套用到該組件的安裝。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-164">Any option that occurs before an assembly name applies to that assembly's installation.</span></span> <span data-ttu-id="0aa7a-165">除了 `/u` 和 `/AssemblyName` 之外，選項可以累積但不可覆寫。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-165">Except for `/u` and `/AssemblyName`, options are cumulative but overridable.</span></span> <span data-ttu-id="0aa7a-166">也就是說，除非以新的值指定選項，否則為一個組件指定的選項會套用到所有後續的組件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-166">That is, options specified for one assembly apply to all subsequent assemblies unless the option is specified with a new value.</span></span>

<span data-ttu-id="0aa7a-167">如果對組件執行 Installutil.exe 而沒有指定任何選項的話，它會將下列三個檔案放置到組件的目錄中：</span><span class="sxs-lookup"><span data-stu-id="0aa7a-167">If you run Installutil.exe against an assembly without specifying any options, it places the following three files into the assembly's directory:</span></span>

- <span data-ttu-id="0aa7a-168">InstallUtil.InstallLog：包含安裝進度的一般說明。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-168">InstallUtil.InstallLog - Contains a general description of the installation progress.</span></span>

- <span data-ttu-id="0aa7a-169">*assemblyname*.InstallLog - 包含安裝程序認可階段的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-169">*assemblyname*.InstallLog - Contains information specific to the commit phase of the installation process.</span></span> <span data-ttu-id="0aa7a-170">如需關於認可階段的詳細資訊，請參閱 <xref:System.Configuration.Install.Installer.Commit%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-170">For more information about the commit phase, see the <xref:System.Configuration.Install.Installer.Commit%2A> method.</span></span>

- <span data-ttu-id="0aa7a-171">*assemblyname*.InstallState - 包含用來解除安裝組件的資料。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-171">*assemblyname*.InstallState - Contains data used to uninstall the assembly.</span></span>

<span data-ttu-id="0aa7a-172">Installutil.exe 使用反射來檢查指定的組件並找到所有 <xref:System.Configuration.Install.Installer> 類型，這些類型的 <xref:System.ComponentModel.RunInstallerAttribute?displayProperty=nameWithType> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-172">Installutil.exe uses reflection to inspect the specified assemblies and to find all <xref:System.Configuration.Install.Installer> types that have the <xref:System.ComponentModel.RunInstallerAttribute?displayProperty=nameWithType> attribute set to `true`.</span></span> <span data-ttu-id="0aa7a-173">然後工具會在 <xref:System.Configuration.Install.Installer.Install%2A?displayProperty=nameWithType> 類型的每個執行個體上執行 <xref:System.Configuration.Install.Installer.Uninstall%2A?displayProperty=nameWithType> 或 <xref:System.Configuration.Install.Installer> 方法。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-173">The tool then executes either the <xref:System.Configuration.Install.Installer.Install%2A?displayProperty=nameWithType> or the <xref:System.Configuration.Install.Installer.Uninstall%2A?displayProperty=nameWithType> method on each instance of the <xref:System.Configuration.Install.Installer> type.</span></span> <span data-ttu-id="0aa7a-174">Installutil.exe 會以交易方式執行安裝；也就是說，如果其中一個組件安裝失敗，便會復原所有其他組件的安裝。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-174">Installutil.exe performs installation in a transactional manner; that is, if one of the assemblies fails to install, it rolls back the installations of all other assemblies.</span></span> <span data-ttu-id="0aa7a-175">解除安裝不是可異動的。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-175">Uninstall is not transactional.</span></span>

<span data-ttu-id="0aa7a-176">Installutil.exe 無法安裝或解除安裝延遲簽署的組件，但是可以安裝或解除安裝強式命名的組件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-176">Installutil.exe cannot install or uninstall delay-signed assemblies, but it can install or uninstall strong-named assemblies.</span></span>

<span data-ttu-id="0aa7a-177">從 .NET Framework 2.0 版開始，32 位元版本的通用語言執行平台 (CLR) 僅會隨附於 32 位元版本的安裝程式工具，但是 64 位元版本的 CLR 則會隨附於 32 位元和 64 位元版本的安裝程式工具。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-177">Starting with the .NET Framework version 2.0, the 32-bit version of the common language runtime (CLR) ships with only the 32-bit version of the Installer tool, but the 64-bit version of the CLR ships with both 32-bit and 64-bit versions of the Installer tool.</span></span> <span data-ttu-id="0aa7a-178">當您使用 64 位元的 CLR 時，請使用 32 位元的安裝程式工具來安裝 32 位元的組件，並使用 64 位元的安裝程式工具來安裝 64 位元和 Microsoft Intermediate Language (MSIL) 的組件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-178">When using the 64-bit CLR, use the 32-bit Installer tool to install 32-bit assemblies, and the 64-bit Installer tool to install 64-bit and Microsoft intermediate language (MSIL) assemblies.</span></span> <span data-ttu-id="0aa7a-179">這兩種版本的安裝程式工具會有相同的行為方式。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-179">Both versions of the Installer tool behave the same.</span></span>

<span data-ttu-id="0aa7a-180">您不能使用 Installutil.exe 部署使用 C++ 建立的 Windows 服務，因為 Installutil.exe 無法辨識由 C++ 編譯器產生的內嵌機器碼。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-180">You cannot use Installutil.exe to deploy a Windows service that was created by using C++, because Installutil.exe cannot recognize the embedded native code that is produced by the C++ compiler.</span></span> <span data-ttu-id="0aa7a-181">如果您嘗試使用 Installutil.exe 部署 C++ Windows 服務，就會擲回類似 <xref:System.BadImageFormatException> 的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-181">If you try to deploy a C++ Windows service with Installutil.exe, an exception such as <xref:System.BadImageFormatException> will be thrown.</span></span> <span data-ttu-id="0aa7a-182">若要處理這種案例，請將服務程式碼移至 C++ 模組，然後以 C# 或 Visual Basic 撰寫安裝程式物件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-182">To work with this scenario, move the service code to a C++ module, and then write the installer object in C# or Visual Basic.</span></span>

## <a name="examples"></a><span data-ttu-id="0aa7a-183">範例</span><span class="sxs-lookup"><span data-stu-id="0aa7a-183">Examples</span></span>

<span data-ttu-id="0aa7a-184">下列命令會顯示 InstallUtil.exe 命令語法及選項的描述。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-184">The following command displays a description of the command syntax and options for InstallUtil.exe.</span></span>

```console
installutil /?
```

<span data-ttu-id="0aa7a-185">下列命令會顯示 InstallUtil.exe 命令語法及選項的描述。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-185">The following command displays a description of the command syntax and options for InstallUtil.exe.</span></span> <span data-ttu-id="0aa7a-186">如果已將說明文字指派給安裝程式的 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 屬性，還會顯示 `myAssembly.exe` 中的安裝程式元件所支援的選項描述和清單。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-186">It also displays a description and list of options supported by the installer components in `myAssembly.exe` if help text has been assigned to the installer's <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> property.</span></span>

```console
installutil /? myAssembly.exe
```

<span data-ttu-id="0aa7a-187">下列命令會執行 `myAssembly.exe` 組件中的安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-187">The following command executes the installer components in the assembly `myAssembly.exe`.</span></span>

```console
installutil myAssembly.exe
```

<span data-ttu-id="0aa7a-188">下列命令會使用 `/AssemblyName` 參數和完整名稱，執行組件中的安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-188">The following command executes the installer components in an assembly by using the `/AssemblyName` switch and a fully qualified name.</span></span>

```console
installutil /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"
```

<span data-ttu-id="0aa7a-189">下列命令會執行檔案名稱及強式名稱所指定之組件中的安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-189">The following command executes the installer components in an assembly specified by file name and in an assembly specified by strong name.</span></span> <span data-ttu-id="0aa7a-190">請注意，所有依檔案名稱指定的組件必須在命令列中以強式名稱指定的組件之前，因為不可覆寫 `/AssemblyName` 選項。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-190">Note that all assemblies specified by file name must precede assemblies specified by strong name on the command line, because the `/AssemblyName` option cannot be overridden.</span></span>

```console
installutil myAssembly.exe /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"
```

<span data-ttu-id="0aa7a-191">下列命令會執行 `myAssembly.exe` 組件中的解除安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-191">The following command executes the uninstaller components in the assembly `myAssembly.exe`.</span></span>

```console
installutil /u myAssembly.exe
```

<span data-ttu-id="0aa7a-192">下列命令會執行組件 `myAssembly1.exe` 和 `myAssembly2.exe` 中的解除安裝程式元件。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-192">The following command executes the uninstaller components in the assemblies `myAssembly1.exe` and `myAssembly2.exe`.</span></span>

```console
installutil myAssembly1.exe /u myAssembly2.exe
```

<span data-ttu-id="0aa7a-193">因為 `/u` 選項在命令列中的位置並不重要，因此這會等於下列指令。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-193">Because the position of the `/u` option on the command line is not important, this is equivalent to the following command.</span></span>

```console
installutil /u myAssembly1.exe myAssembly2.exe
```

<span data-ttu-id="0aa7a-194">下列命令會執行 `myAssembly.exe` 組件中的安裝程式，並指定將進度資訊寫入 `myLog.InstallLog`。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-194">The following command executes the installers in the assembly `myAssembly.exe` and specifies that progress information will be written to `myLog.InstallLog`.</span></span>

```console
installutil /LogFile=myLog.InstallLog myAssembly.exe
```

<span data-ttu-id="0aa7a-195">下列命令會執行組件 `myAssembly.exe` 中的安裝程式、指定要將進度資訊寫入 `myLog.InstallLog`，然後使用安裝程式的自訂 `/reg` 選項指定要對系統登錄進行更新。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-195">The following command executes the installers in the assembly `myAssembly.exe`, specifies that progress information should be written to `myLog.InstallLog`, and uses the installers' custom `/reg` option to specify that updates should be made to the system registry.</span></span>

```console
installutil /LogFile=myLog.InstallLog /reg=true myAssembly.exe
```

<span data-ttu-id="0aa7a-196">下列命令會執行組件 `myAssembly.exe` 中的安裝程式、使用安裝程式的自訂 `/email` 選項指定使用者的電子郵件地址，並隱藏對記錄檔的輸出。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-196">The following command executes the installers in the assembly `myAssembly.exe`, uses the installer's custom `/email` option to specify the user's email address, and suppresses output to the log file.</span></span>

```console
installutil /LogFile= /email=admin@mycompany.com myAssembly.exe
```

<span data-ttu-id="0aa7a-197">下列命令會將 `myAssembly.exe` 的安裝進度寫入到 `myLog.InstallLog`，並且將 `myTestAssembly.exe` 的進度寫入到 `myTestLog.InstallLog`。</span><span class="sxs-lookup"><span data-stu-id="0aa7a-197">The following command writes the installation progress for `myAssembly.exe` to `myLog.InstallLog` and writes the progress for `myTestAssembly.exe` to `myTestLog.InstallLog`.</span></span>

```console
installutil /LogFile=myLog.InstallLog myAssembly.exe /LogFile=myTestLog.InstallLog myTestAssembly.exe
```

## <a name="see-also"></a><span data-ttu-id="0aa7a-198">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0aa7a-198">See also</span></span>

- <xref:System.Configuration.Install>
- [<span data-ttu-id="0aa7a-199">工具</span><span class="sxs-lookup"><span data-stu-id="0aa7a-199">Tools</span></span>](index.md)
- [<span data-ttu-id="0aa7a-200">命令提示字元</span><span class="sxs-lookup"><span data-stu-id="0aa7a-200">Command Prompts</span></span>](developer-command-prompt-for-vs.md)

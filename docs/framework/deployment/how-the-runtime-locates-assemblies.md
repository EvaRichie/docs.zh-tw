---
title: 執行階段如何找出組件
description: 瞭解 common language runtime （CLR）如何找出並系結至在 .NET 中組成應用程式的元件。
ms.date: 03/30/2017
helpviewer_keywords:
- app.config files, assembly locations
- deploying applications [.NET Framework], assembly locations
- application configuration files, locating assemblies
- .NET Framework application deployment, locating assemblies
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 772ac6f4-64d2-4cfb-92fd-58096dcd6c34
ms.openlocfilehash: 4cf1e5787fe2e430d20208d8e79b610e9126c67c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622623"
---
# <a name="how-the-runtime-locates-assemblies"></a><span data-ttu-id="d981d-103">執行階段如何找出組件</span><span class="sxs-lookup"><span data-stu-id="d981d-103">How the Runtime Locates Assemblies</span></span>

<span data-ttu-id="d981d-104">若要成功部署 .NET Framework 應用程式，您必須了解 Common Language Runtime 如何找出並繫結至構成應用程式的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-104">To successfully deploy your .NET Framework application, you must understand how the common language runtime locates and binds to the assemblies that make up your application.</span></span> <span data-ttu-id="d981d-105">根據預設，執行階段會嘗試與用來建置應用程式的組件正確版本繫結。</span><span class="sxs-lookup"><span data-stu-id="d981d-105">By default, the runtime attempts to bind with the exact version of an assembly that the application was built with.</span></span> <span data-ttu-id="d981d-106">組態檔設定可覆寫這個預設行為。</span><span class="sxs-lookup"><span data-stu-id="d981d-106">This default behavior can be overridden by configuration file settings.</span></span>

<span data-ttu-id="d981d-107">在嘗試找出組件，並解析組件參考時，Common Language Runtime 會執行數個步驟。</span><span class="sxs-lookup"><span data-stu-id="d981d-107">The common language runtime performs a number of steps when attempting to locate an assembly and resolve an assembly reference.</span></span> <span data-ttu-id="d981d-108">以下各節將會說明每個步驟。</span><span class="sxs-lookup"><span data-stu-id="d981d-108">Each step is explained in the following sections.</span></span> <span data-ttu-id="d981d-109">在說明執行階段如何找出組件時，常會使用詞彙探查；它會依據其名稱和文化特性，參考用來尋找組件的啟發學習法集合。</span><span class="sxs-lookup"><span data-stu-id="d981d-109">The term probing is often used when describing how the runtime locates assemblies; it refers to the set of heuristics used to locate the assembly based on its name and culture.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-110">您可以使用 Windows SDK 中隨附的[組件繫結記錄檢視器 (Fuslogvw.exe)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md) 來檢視記錄檔中的繫結資訊。</span><span class="sxs-lookup"><span data-stu-id="d981d-110">You can view binding information in the log file using the [Assembly Binding Log Viewer (Fuslogvw.exe)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md), which is included in the Windows SDK.</span></span>

## <a name="initiating-the-bind"></a><span data-ttu-id="d981d-111">初始化繫結</span><span class="sxs-lookup"><span data-stu-id="d981d-111">Initiating the Bind</span></span>

<span data-ttu-id="d981d-112">當執行階段嘗試將參考解析成另一個組件時，尋找並繫結至組件的程序即開始。</span><span class="sxs-lookup"><span data-stu-id="d981d-112">The process of locating and binding to an assembly begins when the runtime attempts to resolve a reference to another assembly.</span></span> <span data-ttu-id="d981d-113">此參考可以是靜態或動態。</span><span class="sxs-lookup"><span data-stu-id="d981d-113">This reference can be either static or dynamic.</span></span> <span data-ttu-id="d981d-114">編譯器會在建置時，將靜態參考記錄在組件資訊清單的中繼資料中。</span><span class="sxs-lookup"><span data-stu-id="d981d-114">The compiler records static references in the assembly manifest's metadata at build time.</span></span> <span data-ttu-id="d981d-115">動態參考則是呼叫各種方法 (例如 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>) 時，即時建構的結果。</span><span class="sxs-lookup"><span data-stu-id="d981d-115">Dynamic references are constructed on the fly as a result of calling various methods, such as <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="d981d-116">參考組件時，最好是使用完整參考，包括組件名稱、版本、文化特性和公開金鑰語彙基元 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="d981d-116">The preferred way to reference an assembly is to use a full reference, including the assembly name, version, culture, and public key token (if one exists).</span></span> <span data-ttu-id="d981d-117">執行階段會使用此資訊來尋找組件 (依照本節稍後說明的步驟)。</span><span class="sxs-lookup"><span data-stu-id="d981d-117">The runtime uses this information to locate the assembly, following the steps described later in this section.</span></span> <span data-ttu-id="d981d-118">不論是靜態或動態組件的參考，執行階段都會使用相同的解析程序。</span><span class="sxs-lookup"><span data-stu-id="d981d-118">The runtime uses the same resolution process regardless of whether the reference is for a static or dynamic assembly.</span></span>

<span data-ttu-id="d981d-119">您也可以只提供組件的部分資訊給呼叫方法 (例如只指定組件名稱)，以對組件進行動態參考。</span><span class="sxs-lookup"><span data-stu-id="d981d-119">You can also make a dynamic reference to an assembly by providing the calling method with only partial information about the assembly, such as specifying only the assembly name.</span></span> <span data-ttu-id="d981d-120">在此情況下，只會搜尋組件的應用程式目錄，而不會進行任何其他檢查。</span><span class="sxs-lookup"><span data-stu-id="d981d-120">In this case, only the application directory is searched for the assembly, and no other checking occurs.</span></span> <span data-ttu-id="d981d-121">您可以使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>等各種方法來載入組件，以進行部分參考。</span><span class="sxs-lookup"><span data-stu-id="d981d-121">You make a partial reference using any of the various methods for loading assemblies such as <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="d981d-122">最後，您可以使用之類的方法來建立動態參考 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> ，只提供部分資訊; 接著，您可以使用 [\<qualifyAssembly>](../configure-apps/file-schema/runtime/qualifyassembly-element.md) 應用程式佈建檔中的專案來限定參考。</span><span class="sxs-lookup"><span data-stu-id="d981d-122">Finally, you can make a dynamic reference using a method such as <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> and provide only partial information; you then qualify the reference using the [\<qualifyAssembly>](../configure-apps/file-schema/runtime/qualifyassembly-element.md) element in the application configuration file.</span></span> <span data-ttu-id="d981d-123">這個項目可讓您在應用程式組態檔中，而不是在您的程式碼中，提供完整的參考資訊 (名稱、版本、文化特性和 (適用的話) 公開金鑰語彙基元)。</span><span class="sxs-lookup"><span data-stu-id="d981d-123">This element allows you to provide the full reference information (name, version, culture and, if applicable, the public key token) in your application configuration file instead of in your code.</span></span> <span data-ttu-id="d981d-124">如果您想要完整限定參考外部應用程式目錄中的組件，或者如果您想要參考全域組件快取中的組件，但又想要在組態檔中 (而不是在您的程式碼中) 指定完整參考的方便性，您就會使用這項技術。</span><span class="sxs-lookup"><span data-stu-id="d981d-124">You would use this technique if you wanted to fully qualify a reference to an assembly outside the application directory, or if you wanted to reference an assembly in the global assembly cache but you wanted the convenience of specifying the full reference in the configuration file instead of in your code.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-125">這種類型的部分參考不應該用於數個應用程式之間共用的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-125">This type of partial reference should not be used with assemblies that are shared among several applications.</span></span> <span data-ttu-id="d981d-126">因為組態設定是依各應用程式來套用，而且依各組件，所以使用這種部分參考的共用組件，會要求使用共用組件的每個應用程式，在其組態檔中都要有合格的資訊。</span><span class="sxs-lookup"><span data-stu-id="d981d-126">Because configuration settings are applied per application and not per assembly, a shared assembly using this type of partial reference would require each application using the shared assembly to have the qualifying information in its configuration file.</span></span>

<span data-ttu-id="d981d-127">執行階段會使用下列步驟來解析組件參考：</span><span class="sxs-lookup"><span data-stu-id="d981d-127">The runtime uses the following steps to resolve an assembly reference:</span></span>

1. <span data-ttu-id="d981d-128">檢查適用的組態檔，包括應用程式組態檔、發行者原則檔和電腦組態檔，以[判斷正確的組件版本](#step1) 。</span><span class="sxs-lookup"><span data-stu-id="d981d-128">[Determines the correct assembly version](#step1) by examining applicable configuration files, including the application configuration file, publisher policy file, and machine configuration file.</span></span> <span data-ttu-id="d981d-129">如果組態檔位於遠端電腦上，執行階段必須先找出並下載應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-129">If the configuration file is located on a remote machine, the runtime must locate and download the application configuration file first.</span></span>

2. <span data-ttu-id="d981d-130">[檢查組件名稱之前是否已經被繫結](#step2) ，如果是的話，會使用先前載入的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-130">[Checks whether the assembly name has been bound to before](#step2) and, if so, uses the previously loaded assembly.</span></span> <span data-ttu-id="d981d-131">如果先前載入組件的要求失敗，此要求會立即失敗，而不會嘗試載入組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-131">If a previous request to load the assembly failed, the request is failed immediately without attempting to load the assembly.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d981d-132">快取組件繫結失敗是 .NET Framework 2.0 版的新功能。</span><span class="sxs-lookup"><span data-stu-id="d981d-132">The caching of assembly binding failures is new in the .NET Framework version 2.0.</span></span>

3. <span data-ttu-id="d981d-133">[檢查全域組件快取](#step3)。</span><span class="sxs-lookup"><span data-stu-id="d981d-133">[Checks the global assembly cache](#step3).</span></span> <span data-ttu-id="d981d-134">如果那裡找到組件，執行階段會使用此組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-134">If the assembly is found there, the runtime uses this assembly.</span></span>

4. <span data-ttu-id="d981d-135">使用下列步驟來[探查組件](#step4) ：</span><span class="sxs-lookup"><span data-stu-id="d981d-135">[Probes for the assembly](#step4) using the following steps:</span></span>

    1. <span data-ttu-id="d981d-136">如果組態和發行者原則不會影響原始參考，而且如果繫結要求是使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法來建立的，執行階段會檢查位置提示。</span><span class="sxs-lookup"><span data-stu-id="d981d-136">If configuration and publisher policy do not affect the original reference and if the bind request was created using the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method, the runtime checks for location hints.</span></span>

    2. <span data-ttu-id="d981d-137">如果在組態檔中找到程式碼基底，執行階段只會檢查這個位置。</span><span class="sxs-lookup"><span data-stu-id="d981d-137">If a codebase is found in the configuration files, the runtime checks only this location.</span></span> <span data-ttu-id="d981d-138">如果此探查失敗，執行階段會判定繫結要求失敗，且不會再發生其他探查。</span><span class="sxs-lookup"><span data-stu-id="d981d-138">If this probe fails, the runtime determines that the binding request failed and no other probing occurs.</span></span>

    3. <span data-ttu-id="d981d-139">[探查一節](#step4)中會說明如何使用啟發學習法來探查組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-139">Probes for the assembly using the heuristics described in the [probing section](#step4).</span></span> <span data-ttu-id="d981d-140">如果在探查之後找不到組件，執行階段會要求 Windows Installer 提供組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-140">If the assembly is not found after probing, the runtime requests the Windows Installer to provide the assembly.</span></span> <span data-ttu-id="d981d-141">這可以做為隨選安裝功能。</span><span class="sxs-lookup"><span data-stu-id="d981d-141">This acts as an install-on-demand feature.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d981d-142">針對沒有強式名稱的組件，不會進行版本檢查，執行階段也不會在全域組件快取中檢查沒有強式名稱的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-142">There is no version checking for assemblies without strong names, nor does the runtime check in the global assembly cache for assemblies without strong names.</span></span>

<a name="step1"></a>

## <a name="step-1-examining-the-configuration-files"></a><span data-ttu-id="d981d-143">步驟 1：檢查組態檔</span><span class="sxs-lookup"><span data-stu-id="d981d-143">Step 1: Examining the Configuration Files</span></span>

<span data-ttu-id="d981d-144">根據下列三個 XML 檔案，可以在不同層級設定組件繫結行為：</span><span class="sxs-lookup"><span data-stu-id="d981d-144">Assembly binding behavior can be configured at different levels based on three XML files:</span></span>

- <span data-ttu-id="d981d-145">應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-145">Application configuration file.</span></span>

- <span data-ttu-id="d981d-146">發行者原則檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-146">Publisher policy file.</span></span>

- <span data-ttu-id="d981d-147">電腦組態檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-147">Machine configuration file.</span></span>

<span data-ttu-id="d981d-148">這些檔案遵循相同的語法，並提供繫結重新導向、程式碼位置，以及特定組件的繫結模式等資訊。</span><span class="sxs-lookup"><span data-stu-id="d981d-148">These files follow the same syntax and provide information such as binding redirects, the location of code, and binding modes for particular assemblies.</span></span> <span data-ttu-id="d981d-149">每個設定檔都可以包含重新導向系結進程的[ \<assemblyBinding> 元素](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-149">Each configuration file can contain an [\<assemblyBinding> element](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) that redirects the binding process.</span></span> <span data-ttu-id="d981d-150">[ \<assemblyBinding> 元素](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)的子專案包含[ \<dependentAssembly> 專案。](../configure-apps/file-schema/runtime/dependentassembly-element.md)</span><span class="sxs-lookup"><span data-stu-id="d981d-150">The child elements of the [\<assemblyBinding> element](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) include the [\<dependentAssembly> element](../configure-apps/file-schema/runtime/dependentassembly-element.md).</span></span> <span data-ttu-id="d981d-151">[ \<dependentAssembly> 元素](../configure-apps/file-schema/runtime/dependentassembly-element.md)的子系包括[ \<assemblyIdentity> 元素](/visualstudio/deployment/assemblyidentity-element-clickonce-deployment)、專案和[ \<bindingRedirect> ](../configure-apps/file-schema/runtime/bindingredirect-element.md)專案[ \<codeBase> 。](../configure-apps/file-schema/runtime/codebase-element.md)</span><span class="sxs-lookup"><span data-stu-id="d981d-151">The children of [\<dependentAssembly> element](../configure-apps/file-schema/runtime/dependentassembly-element.md) include the [\<assemblyIdentity> element](/visualstudio/deployment/assemblyidentity-element-clickonce-deployment), the [\<bindingRedirect> element](../configure-apps/file-schema/runtime/bindingredirect-element.md), and the [\<codeBase> element](../configure-apps/file-schema/runtime/codebase-element.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-152">您可以在這三個組態檔中找到組態資訊；並非所有組態檔中的所有項目都有效。</span><span class="sxs-lookup"><span data-stu-id="d981d-152">Configuration information can be found in the three configuration files; not all elements are valid in all configuration files.</span></span> <span data-ttu-id="d981d-153">例如，繫結模式和私用路徑資訊只能在應用程式組態檔中。</span><span class="sxs-lookup"><span data-stu-id="d981d-153">For example, binding mode and private path information can only be in the application configuration file.</span></span> <span data-ttu-id="d981d-154">如需每個檔案內含資訊的完整清單，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-154">For a complete list of the information that is contained in each file, see [Configuring Apps by Using Configuration Files](../configure-apps/index.md).</span></span>

### <a name="application-configuration-file"></a><span data-ttu-id="d981d-155">應用程式組態檔</span><span class="sxs-lookup"><span data-stu-id="d981d-155">Application Configuration File</span></span>

<span data-ttu-id="d981d-156">第一，Common Language Runtime 會檢查應用程式組態檔中，是否有資訊會覆寫儲存在呼叫組件資訊清單中的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d981d-156">First, the common language runtime checks the application configuration file for information that overrides the version information stored in the calling assembly's manifest.</span></span> <span data-ttu-id="d981d-157">應用程式組態檔可以隨著應用程式一起部署，但並不是執行應用程式的必要項目。</span><span class="sxs-lookup"><span data-stu-id="d981d-157">The application configuration file can be deployed with an application, but is not required for application execution.</span></span> <span data-ttu-id="d981d-158">通常擷取這個檔案幾乎是瞬間完成，但是如果應用程式基底是在遠端電腦上 (例如在 Internet Explorer Web 架構案例中)，就必須下載組態檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-158">Usually the retrieval of this file is almost instantaneous, but in situations where the application base is on a remote computer, such as in an Internet Explorer Web-based scenario, the configuration file must be downloaded.</span></span>

<span data-ttu-id="d981d-159">針對用戶端可執行檔，應用程式組態檔會位在與應用程式可執行檔相同的目錄中，而且基底名稱與可執行檔相同，副檔名為 .config。</span><span class="sxs-lookup"><span data-stu-id="d981d-159">For client executables, the application configuration file resides in the same directory as the application's executable and has the same base name as the executable with a .config extension.</span></span> <span data-ttu-id="d981d-160">例如，C:\Program Files\Myapp\Myapp.exe 的設定檔是 C:\Program Files\Myapp\Myapp.exe.config。在以瀏覽器為基礎的案例中，HTML 檔案必須使用 **\<link>** 元素明確指向設定檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-160">For example, the configuration file for C:\Program Files\Myapp\Myapp.exe is C:\Program Files\Myapp\Myapp.exe.config. In a browser-based scenario, the HTML file must use the **\<link>** element to explicitly point to the configuration file.</span></span>

<span data-ttu-id="d981d-161">下列程式碼提供應用程式組態檔的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="d981d-161">The following code provides a simple example of an application configuration file.</span></span> <span data-ttu-id="d981d-162">這個範例會將 <xref:System.Diagnostics.TextWriterTraceListener> 加入 <xref:System.Diagnostics.Debug.Listeners%2A> 集合，以啟用將偵錯資訊記錄至檔案的功能。</span><span class="sxs-lookup"><span data-stu-id="d981d-162">This example adds a <xref:System.Diagnostics.TextWriterTraceListener> to the <xref:System.Diagnostics.Debug.Listeners%2A> collection to enable recording debug information to a file.</span></span>

```xml
<configuration>
   <system.diagnostics>
      <trace useGlobalLock="false" autoflush="true" indentsize="0">
         <listeners>
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />
         </listeners>
      </trace>
   </system.diagnostics>
</configuration>
```

### <a name="publisher-policy-file"></a><span data-ttu-id="d981d-163">發行者原則檔</span><span class="sxs-lookup"><span data-stu-id="d981d-163">Publisher Policy File</span></span>

<span data-ttu-id="d981d-164">第二，執行階段會檢查發行者原則檔 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="d981d-164">Second, the runtime examines the publisher policy file, if one exists.</span></span> <span data-ttu-id="d981d-165">元件發行者會將發行者原則檔以修正或更新形式發佈至共用元件。</span><span class="sxs-lookup"><span data-stu-id="d981d-165">Publisher policy files are distributed by a component publisher as a fix or update to a shared component.</span></span> <span data-ttu-id="d981d-166">這些檔案包含共用元件發行者所發行的相容性資訊，可將組件參考導向至新版本。</span><span class="sxs-lookup"><span data-stu-id="d981d-166">These files contain compatibility information issued by the publisher of the shared component that directs an assembly reference to a new version.</span></span> <span data-ttu-id="d981d-167">不同於應用程式和電腦組態檔，發行者原則檔是包含在自己的組件中，必須安裝在全域組件快取中。</span><span class="sxs-lookup"><span data-stu-id="d981d-167">Unlike application and machine configuration files, publisher policy files are contained in their own assembly that must be installed in the global assembly cache.</span></span>

<span data-ttu-id="d981d-168">發行者原則組態檔的範例如下：</span><span class="sxs-lookup"><span data-stu-id="d981d-168">The following is an example of a Publisher Policy configuration file:</span></span>

```xml
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">

            <dependentAssembly>
                <assemblyIdentity name="asm6" publicKeyToken="c0305c36380ba429" />
                <bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0"/>
            </dependentAssembly>

        </assemblyBinding>
    </runtime>
</configuration>
```

<span data-ttu-id="d981d-169">若要建立組件，您可以使用[組件連結器 (Al.exe)](../tools/al-exe-assembly-linker.md) 工具來搭配如下命令：</span><span class="sxs-lookup"><span data-stu-id="d981d-169">To create an assembly, you can use the [Al.exe (Assembly Linker)](../tools/al-exe-assembly-linker.md) tool with a command such as the following:</span></span>

```console
Al.exe /link:asm6.exe.config /out:policy.3.0.asm6.dll /keyfile: compatkey.dat /v:3.0.0.0
```

<span data-ttu-id="d981d-170">`compatkey.dat` 是強式名稱金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="d981d-170">`compatkey.dat` is a strong-name key file.</span></span> <span data-ttu-id="d981d-171">此命令會建立可以放在全域組件快取中的強式名稱組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-171">This command creates a strong-named assembly you can place in the global assembly cache.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-172">發行者原則會影響使用共用元件的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="d981d-172">Publisher policy affects all applications that use a shared component.</span></span>

<span data-ttu-id="d981d-173">發行者原則組態檔會覆寫來自應用程式的版本資訊 (也就是來自組件資訊清單，或來自應用程式組態檔)。</span><span class="sxs-lookup"><span data-stu-id="d981d-173">The publisher policy configuration file overrides version information that comes from the application (that is, from the assembly manifest or from the application configuration file).</span></span> <span data-ttu-id="d981d-174">如果應用程式組態檔中沒有陳述式來將組件資訊清單中指定的版本重新導向，發行者原則檔就會覆寫組件資訊清單中指定的版本。</span><span class="sxs-lookup"><span data-stu-id="d981d-174">If there is no statement in the application configuration file to redirect the version specified in the assembly manifest, the publisher policy file overrides the version specified in the assembly manifest.</span></span> <span data-ttu-id="d981d-175">不過，如果應用程式組態檔中有重新導向陳述式，發行者原則會覆寫該版本，而不是資訊清單中指定的版本。</span><span class="sxs-lookup"><span data-stu-id="d981d-175">However, if there is a redirecting statement in the application configuration file, publisher policy overrides that version rather than the one specified in the manifest.</span></span>

<span data-ttu-id="d981d-176">當共用元件更新時，就會使用發行者原則檔，而且使用該元件的所有應用程式，都應該收取共用元件的新版本。</span><span class="sxs-lookup"><span data-stu-id="d981d-176">A publisher policy file is used when a shared component is updated and the new version of the shared component should be picked up by all applications using that component.</span></span> <span data-ttu-id="d981d-177">除非應用程式組態檔強制執行安全模式，否則發行者原則檔中的設定會覆寫應用程式組態檔中的設定。</span><span class="sxs-lookup"><span data-stu-id="d981d-177">The settings in the publisher policy file override settings in the application configuration file, unless the application configuration file enforces safe mode.</span></span>

#### <a name="safe-mode"></a><span data-ttu-id="d981d-178">安全模式</span><span class="sxs-lookup"><span data-stu-id="d981d-178">Safe Mode</span></span>
<span data-ttu-id="d981d-179">發行者原則檔通常會做為 Service Pack 或程式更新的一部分明確安裝。</span><span class="sxs-lookup"><span data-stu-id="d981d-179">Publisher policy files are usually explicitly installed as part of a service pack or program update.</span></span> <span data-ttu-id="d981d-180">如果升級後的共用元件有任何問題，您可以使用安全模式來忽略發行者原則檔中的覆寫。</span><span class="sxs-lookup"><span data-stu-id="d981d-180">If there is any problem with the upgraded shared component, you can ignore the overrides in the publisher policy file using safe mode.</span></span> <span data-ttu-id="d981d-181">安全模式是由專案所決定，該專案 **\<publisherPolicy apply="yes**&#124;**no"/>** 僅位於應用程式佈建檔中。</span><span class="sxs-lookup"><span data-stu-id="d981d-181">Safe mode is determined by the **\<publisherPolicy apply="yes**&#124;**no"/>** element, located only in the application configuration file.</span></span> <span data-ttu-id="d981d-182">它會指定是否應該將發行者原則組態資訊從繫結程序中移除。</span><span class="sxs-lookup"><span data-stu-id="d981d-182">It specifies whether the publisher policy configuration information should be removed from the binding process.</span></span>

<span data-ttu-id="d981d-183">您可以針對整個應用程式或選取的組件來設定安全模式。</span><span class="sxs-lookup"><span data-stu-id="d981d-183">Safe mode can be set for the entire application or for selected assemblies.</span></span> <span data-ttu-id="d981d-184">亦即，您可以針對構成應用程式的所有組件，關閉此原則，或是針對某些組件開啟此原則，但其他組件不開啟此原則。</span><span class="sxs-lookup"><span data-stu-id="d981d-184">That is, you can turn off the policy for all assemblies that make up the application, or turn it on for some assemblies but not others.</span></span> <span data-ttu-id="d981d-185">若要選擇性地將發行者原則套用至構成應用程式的元件，請設定 **\<publisherPolicy apply\=no/>** 並指定您想要使用元素影響的元件 \<**dependentAssembly**> 。</span><span class="sxs-lookup"><span data-stu-id="d981d-185">To selectively apply publisher policy to assemblies that make up an application, set **\<publisherPolicy apply\=no/>** and specify which assemblies you want to be affected using the \<**dependentAssembly**> element.</span></span> <span data-ttu-id="d981d-186">若要將發行者原則套用至構成應用程式的所有元件，請設定 **\<publisherPolicy apply\=no/>** 無相依元件元素。</span><span class="sxs-lookup"><span data-stu-id="d981d-186">To apply publisher policy to all assemblies that make up the application, set **\<publisherPolicy apply\=no/>** with no dependent assembly elements.</span></span> <span data-ttu-id="d981d-187">如需組態的詳細資訊，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-187">For more about configuration, see [Configuring Apps by using Configuration Files](../configure-apps/index.md).</span></span>

### <a name="machine-configuration-file"></a><span data-ttu-id="d981d-188">電腦組態檔</span><span class="sxs-lookup"><span data-stu-id="d981d-188">Machine Configuration File</span></span>
<span data-ttu-id="d981d-189">第三，執行階段會檢查電腦組態檔。</span><span class="sxs-lookup"><span data-stu-id="d981d-189">Third, the runtime examines the machine configuration file.</span></span> <span data-ttu-id="d981d-190">此檔案名為 Machine.config，位在本機電腦上，執行階段安裝所在之根目錄的 Config 子目錄中。</span><span class="sxs-lookup"><span data-stu-id="d981d-190">This file, called Machine.config, resides on the local computer in the Config subdirectory of the root directory where the runtime is installed.</span></span> <span data-ttu-id="d981d-191">系統管理員可以使用這個檔案來指定電腦本機的組件繫結限制。</span><span class="sxs-lookup"><span data-stu-id="d981d-191">This file can be used by administrators to specify assembly binding restrictions that are local to that computer.</span></span> <span data-ttu-id="d981d-192">電腦組態檔中的設定優先順序高於所有其他組態設定；不過，這不表示所有組態設定都應該放在這個檔案中。</span><span class="sxs-lookup"><span data-stu-id="d981d-192">The settings in the machine configuration file take precedence over all other configuration settings; however, this does not mean that all configuration settings should be put in this file.</span></span> <span data-ttu-id="d981d-193">系統管理員原則檔決定的版本為最終版本，不能覆寫。</span><span class="sxs-lookup"><span data-stu-id="d981d-193">The version determined by the administrator policy file is final, and cannot be overridden.</span></span> <span data-ttu-id="d981d-194">在 Machine.config 檔案中指定覆寫會影響所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="d981d-194">Overrides specified in the Machine.config file affect all applications.</span></span> <span data-ttu-id="d981d-195">如需組態檔的詳細資訊，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-195">For more information about configuration files, see [Configuring Apps by using Configuration Files](../configure-apps/index.md).</span></span>

<a name="step2"></a>

## <a name="step-2-checking-for-previously-referenced-assemblies"></a><span data-ttu-id="d981d-196">步驟 2：檢查先前參考的組件</span><span class="sxs-lookup"><span data-stu-id="d981d-196">Step 2: Checking for Previously Referenced Assemblies</span></span>

<span data-ttu-id="d981d-197">如果先前的呼叫中也有要求現在所要求的組件，Common Language Runtime 會使用已載入的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-197">If the requested assembly has also been requested in previous calls, the common language runtime uses the assembly that is already loaded.</span></span> <span data-ttu-id="d981d-198">在為構成應用程式的組件命名時，這可能會有分歧。</span><span class="sxs-lookup"><span data-stu-id="d981d-198">This can have ramifications when naming assemblies that make up an application.</span></span> <span data-ttu-id="d981d-199">如需有關為組件命名的詳細資訊，請參閱 [組件名稱](../../standard/assembly/names.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-199">For more information about naming assemblies, see [Assembly Names](../../standard/assembly/names.md).</span></span>

<span data-ttu-id="d981d-200">如果先前要求組件失敗，後續要求該組件會立即失敗，而不會嘗試載入組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-200">If a previous request for the assembly failed, subsequent requests for the assembly are failed immediately without attempting to load the assembly.</span></span> <span data-ttu-id="d981d-201">從 .NET Framework 2.0 版開始，會快取組件繫結失敗，而所快取的資訊會用來判斷是否要嘗試載入組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-201">Starting with the .NET Framework version 2.0, assembly binding failures are cached, and the cached information is used to determine whether to attempt to load the assembly.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-202">若要還原為不會快取系結失敗之 .NET Framework 版本1.0 和1.1 的行為，請在您的設定檔中包含[ \<disableCachingBindingFailures> 元素](../configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md)。</span><span class="sxs-lookup"><span data-stu-id="d981d-202">To revert to the behavior of the .NET Framework versions 1.0 and 1.1, which did not cache binding failures, include the [\<disableCachingBindingFailures> Element](../configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md) in your configuration file.</span></span>

<a name="step3"></a>

## <a name="step-3-checking-the-global-assembly-cache"></a><span data-ttu-id="d981d-203">步驟 3：檢查全域組件快取</span><span class="sxs-lookup"><span data-stu-id="d981d-203">Step 3: Checking the Global Assembly Cache</span></span>

<span data-ttu-id="d981d-204">針對強式名稱組件，繫結程序會繼續在全域組件快取中查看。</span><span class="sxs-lookup"><span data-stu-id="d981d-204">For strong-named assemblies, the binding process continues by looking in the global assembly cache.</span></span> <span data-ttu-id="d981d-205">全域組件快取會儲存可供電腦上數個應用程式使用的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-205">The global assembly cache stores assemblies that can be used by several applications on a computer.</span></span> <span data-ttu-id="d981d-206">全域組件快取中的所有組件都必須具有強式名稱。</span><span class="sxs-lookup"><span data-stu-id="d981d-206">All assemblies in the global assembly cache must have strong names.</span></span>

<a name="step4"></a>

## <a name="step-4-locating-the-assembly-through-codebases-or-probing"></a><span data-ttu-id="d981d-207">步驟 4：透過程式碼基底或探查找出組件</span><span class="sxs-lookup"><span data-stu-id="d981d-207">Step 4: Locating the Assembly through Codebases or Probing</span></span>

<span data-ttu-id="d981d-208">使用呼叫組件參考和組態檔中的資訊來判斷正確的組件版本之後，以及在其簽入全域組件快取 (僅適用於強式名稱組件) 之後，Common Language Runtime 會嘗試尋找組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-208">After the correct assembly version has been determined by using the information in the calling assembly's reference and in the configuration files, and after it has checked in the global assembly cache (only for strong-named assemblies), the common language runtime attempts to find the assembly.</span></span> <span data-ttu-id="d981d-209">尋找組件的程序包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d981d-209">The process of locating an assembly involves the following steps:</span></span>

1. <span data-ttu-id="d981d-210">如果在 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 應用程式佈建檔中找到元素，執行時間就會檢查指定的位置。</span><span class="sxs-lookup"><span data-stu-id="d981d-210">If a [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element is found in the application configuration file, the runtime checks the specified location.</span></span> <span data-ttu-id="d981d-211">如果找到相符項目，則會使用該組件，而不會進行探查。</span><span class="sxs-lookup"><span data-stu-id="d981d-211">If a match is found, that assembly is used and no probing occurs.</span></span> <span data-ttu-id="d981d-212">如果在那裡沒有找到該組件，則繫結要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="d981d-212">If the assembly is not found there, the binding request fails.</span></span>

2. <span data-ttu-id="d981d-213">然後執行階段會使用本節稍後指定的規則來探查參考的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-213">The runtime then probes for the referenced assembly using the rules specified later in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-214">如果目錄中有多個版本的元件，而您想要參考該元件的特定版本，您必須使用專案， [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 而不是專案的 `privatePath` 屬性 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) 。</span><span class="sxs-lookup"><span data-stu-id="d981d-214">If you have multiple versions of an assembly in a directory and you want to reference a particular version of that assembly, you must use the [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element instead of the `privatePath` attribute of the [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) element.</span></span> <span data-ttu-id="d981d-215">如果您使用專案 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) ，執行時間會在第一次找到符合所參考之簡單元件名稱的元件時停止探查，不論它是否為正確的相符專案。</span><span class="sxs-lookup"><span data-stu-id="d981d-215">If you use the [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) element, the runtime stops probing the first time it finds an assembly that matches the simple assembly name referenced, whether it is a correct match or not.</span></span> <span data-ttu-id="d981d-216">如果是正確的相符項目，就會使用該組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-216">If it is a correct match, that assembly is used.</span></span> <span data-ttu-id="d981d-217">如果不是正確的相符項目，就會停止探查，且繫結失敗。</span><span class="sxs-lookup"><span data-stu-id="d981d-217">If it is not a correct match, probing stops and binding fails.</span></span>

### <a name="locating-the-assembly-through-codebases"></a><span data-ttu-id="d981d-218">透過程式碼基底找出組件</span><span class="sxs-lookup"><span data-stu-id="d981d-218">Locating the Assembly through Codebases</span></span>

<span data-ttu-id="d981d-219">程式碼基底資訊可以使用 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 設定檔中的元素來提供。</span><span class="sxs-lookup"><span data-stu-id="d981d-219">Codebase information can be provided by using a [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element in a configuration file.</span></span> <span data-ttu-id="d981d-220">在執行階段嘗試探查參考的組件之前，一定會先檢查此程式碼基底。</span><span class="sxs-lookup"><span data-stu-id="d981d-220">This codebase is always checked before the runtime attempts to probe for the referenced assembly.</span></span> <span data-ttu-id="d981d-221">如果包含最終版本重新導向的發行者原則檔也包含 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 元素，該專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 就是所使用的元素。</span><span class="sxs-lookup"><span data-stu-id="d981d-221">If a publisher policy file containing the final version redirect also contains a [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element, that [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element is the one that is used.</span></span> <span data-ttu-id="d981d-222">例如，如果您的應用程式佈建檔指定專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，而覆寫應用程式資訊的發行者原則檔也指定了專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，則 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 會使用發行者原則檔中的元素。</span><span class="sxs-lookup"><span data-stu-id="d981d-222">For example, if your application configuration file specifies a [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element, and a publisher policy file that is overriding the application information also specifies a [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element, the [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element in the publisher policy file is used.</span></span>

<span data-ttu-id="d981d-223">如果在元素指定的位置找不到相符專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，則系結要求會失敗，且不會採取任何進一步的步驟。</span><span class="sxs-lookup"><span data-stu-id="d981d-223">If no match is found at the location specified by the [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element, the bind request fails and no further steps are taken.</span></span> <span data-ttu-id="d981d-224">如果執行階段判斷有組件符合呼叫組件的準則，就會使用該組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-224">If the runtime determines that an assembly matches the calling assembly's criteria, it uses that assembly.</span></span> <span data-ttu-id="d981d-225">當載入指定專案所指定的檔案時 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，執行時間會進行檢查，以確定名稱、版本、文化特性和公開金鑰與呼叫元件的參考相符。</span><span class="sxs-lookup"><span data-stu-id="d981d-225">When the file specified by the given [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element is loaded, the runtime checks to make sure that the name, version, culture, and public key match the calling assembly's reference.</span></span>

> [!NOTE]
> <span data-ttu-id="d981d-226">應用程式根目錄之外的參考元件必須具有強式名稱，而且必須安裝在全域組件快取中，或使用元素指定 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 。</span><span class="sxs-lookup"><span data-stu-id="d981d-226">Referenced assemblies outside the application's root directory must have strong names and must either be installed in the global assembly cache or specified using the [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element.</span></span>

### <a name="locating-the-assembly-through-probing"></a><span data-ttu-id="d981d-227">透過探查找出組件</span><span class="sxs-lookup"><span data-stu-id="d981d-227">Locating the Assembly through Probing</span></span>

<span data-ttu-id="d981d-228">如果 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 應用程式佈建檔中沒有專案，則執行時間會使用四個準則來探查元件：</span><span class="sxs-lookup"><span data-stu-id="d981d-228">If there is no [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) element in the application configuration file, the runtime probes for the assembly using four criteria:</span></span>

- <span data-ttu-id="d981d-229">應用程式基底，這是執行應用程式所在的根位置。</span><span class="sxs-lookup"><span data-stu-id="d981d-229">Application base, which is the root location where the application is being executed.</span></span>

- <span data-ttu-id="d981d-230">文化特性，這是所參考之組件的文化特性屬性。</span><span class="sxs-lookup"><span data-stu-id="d981d-230">Culture, which is the culture attribute of the assembly being referenced.</span></span>

- <span data-ttu-id="d981d-231">名稱，這是所參考之組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="d981d-231">Name, which is the name of the referenced assembly.</span></span>

- <span data-ttu-id="d981d-232">`privatePath`元素的屬性 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) ，這是根位置底下的使用者定義子目錄清單。</span><span class="sxs-lookup"><span data-stu-id="d981d-232">The `privatePath` attribute of the [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) element, which is the user-defined list of subdirectories under the root location.</span></span> <span data-ttu-id="d981d-233">您可以使用應用程式定義域的 <xref:System.AppDomainSetup.PrivateBinPath?displayProperty=nameWithType> 屬性，將這個位置指定在應用程式組態檔和 Managed 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="d981d-233">This location can be specified in the application configuration file and in managed code using the <xref:System.AppDomainSetup.PrivateBinPath?displayProperty=nameWithType> property for an application domain.</span></span> <span data-ttu-id="d981d-234">如果指定在 Managed 程式碼中，會先探查 Managed 程式碼 `privatePath` ，後面接著應用程式組態檔中指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="d981d-234">When specified in managed code, the managed code `privatePath` is probed first, followed by the path specified in the application configuration file.</span></span>

#### <a name="probing-the-application-base-and-culture-directories"></a><span data-ttu-id="d981d-235">探查應用程式基底和文化特性目錄</span><span class="sxs-lookup"><span data-stu-id="d981d-235">Probing the Application Base and Culture Directories</span></span>

<span data-ttu-id="d981d-236">執行階段一定會從應用程式的基底開始探查，該基底可以是 URL，或是應用程式在電腦上的根目錄。</span><span class="sxs-lookup"><span data-stu-id="d981d-236">The runtime always begins probing in the application's base, which can be either a URL or the application's root directory on a computer.</span></span> <span data-ttu-id="d981d-237">如果在應用程式基底中找不到參考的組件，而且沒有提供任何文化特性資訊，執行階段會搜尋具有該組件名稱的任何子目錄。</span><span class="sxs-lookup"><span data-stu-id="d981d-237">If the referenced assembly is not found in the application base and no culture information is provided, the runtime searches any subdirectories with the assembly name.</span></span> <span data-ttu-id="d981d-238">所探查的目錄包括：</span><span class="sxs-lookup"><span data-stu-id="d981d-238">The directories probed include:</span></span>

- <span data-ttu-id="d981d-239">[應用程式基底] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-239">[application base] / [assembly name].dll</span></span>

- <span data-ttu-id="d981d-240">[應用程式基底] / [組件名稱] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-240">[application base] / [assembly name] / [assembly name].dll</span></span>

<span data-ttu-id="d981d-241">如果有為參考的組件指定文化特性資訊，就只會探查下列目錄：</span><span class="sxs-lookup"><span data-stu-id="d981d-241">If culture information is specified for the referenced assembly, only the following directories are probed:</span></span>

- <span data-ttu-id="d981d-242">[應用程式基底] / [文化特性] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-242">[application base] / [culture] / [assembly name].dll</span></span>

- <span data-ttu-id="d981d-243">[應用程式基底] / [文化特性] / [組件名稱] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-243">[application base] / [culture] / [assembly name] / [assembly name].dll</span></span>

#### <a name="probing-with-the-privatepath-attribute"></a><span data-ttu-id="d981d-244">使用 privatePath 屬性進行探查</span><span class="sxs-lookup"><span data-stu-id="d981d-244">Probing with the privatePath Attribute</span></span>

<span data-ttu-id="d981d-245">除了文化特性子目錄以及為參考元件所命名的子目錄以外，執行時間也會探查使用專案的屬性指定的目錄 `privatePath` [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) 。</span><span class="sxs-lookup"><span data-stu-id="d981d-245">In addition to the culture subdirectories and the subdirectories named for the referenced assembly, the runtime also probes directories specified using the `privatePath` attribute of the [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) element.</span></span> <span data-ttu-id="d981d-246">使用 `privatePath` 屬性來指定的目錄，必須是應用程式根目錄的子目錄。</span><span class="sxs-lookup"><span data-stu-id="d981d-246">The directories specified using the `privatePath` attribute must be subdirectories of the application's root directory.</span></span> <span data-ttu-id="d981d-247">所探查的目錄會因為文化特性資訊是否包含在參考的組件要求中而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d981d-247">The directories probed vary depending on whether culture information is included in the referenced assembly request.</span></span>

<span data-ttu-id="d981d-248">執行階段只要一找到符合所參考之簡單組件名稱的組件 (無論是否確實相符)，就會停止探查。</span><span class="sxs-lookup"><span data-stu-id="d981d-248">The runtime stops probing the first time it finds an assembly that matches the simple assembly name referenced, whether it is a correct match or not.</span></span> <span data-ttu-id="d981d-249">如果是正確的相符項目，就會使用該組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-249">If it is a correct match, that assembly is used.</span></span> <span data-ttu-id="d981d-250">如果不是正確的相符項目，就會停止探查，且繫結失敗。</span><span class="sxs-lookup"><span data-stu-id="d981d-250">If it is not a correct match, probing stops and binding fails.</span></span>

<span data-ttu-id="d981d-251">如果包含文化特性，就會探查下列目錄：</span><span class="sxs-lookup"><span data-stu-id="d981d-251">If culture is included, the following directories are probed:</span></span>

- <span data-ttu-id="d981d-252">[應用程式基底] / [bin 路徑] / [文化特性] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-252">[application base] / [binpath] / [culture] / [assembly name].dll</span></span>

- <span data-ttu-id="d981d-253">[應用程式基底] / [bin 路徑] / [文化特性] / [組件名稱] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-253">[application base] / [binpath] / [culture] / [assembly name] / [assembly name].dll</span></span>

<span data-ttu-id="d981d-254">如果沒有包含文化特性資訊，就會探查下列目錄：</span><span class="sxs-lookup"><span data-stu-id="d981d-254">If culture information is not included, the following directories are probed:</span></span>

- <span data-ttu-id="d981d-255">[應用程式基底] / [bin 路徑] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-255">[application base] / [binpath] / [assembly name].dll</span></span>

- <span data-ttu-id="d981d-256">[應用程式基底] / [bin 路徑] / [組件名稱] / [組件名稱].dll</span><span class="sxs-lookup"><span data-stu-id="d981d-256">[application base] / [binpath] / [assembly name] / [assembly name].dll</span></span>

#### <a name="probing-examples"></a><span data-ttu-id="d981d-257">探查範例</span><span class="sxs-lookup"><span data-stu-id="d981d-257">Probing Examples</span></span>

<span data-ttu-id="d981d-258">假設有下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d981d-258">Given the following information:</span></span>

- <span data-ttu-id="d981d-259">參考的組件名稱：myAssembly</span><span class="sxs-lookup"><span data-stu-id="d981d-259">Referenced assembly name: myAssembly</span></span>

- <span data-ttu-id="d981d-260">應用程式根目錄：`http://www.code.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="d981d-260">Application root directory: `http://www.code.microsoft.com`</span></span>

- <span data-ttu-id="d981d-261">[\<probing>](../configure-apps/file-schema/runtime/probing-element.md)設定檔中的元素指定： bin</span><span class="sxs-lookup"><span data-stu-id="d981d-261">[\<probing>](../configure-apps/file-schema/runtime/probing-element.md) element in configuration file specifies: bin</span></span>

- <span data-ttu-id="d981d-262">文化特性：de</span><span class="sxs-lookup"><span data-stu-id="d981d-262">Culture: de</span></span>

<span data-ttu-id="d981d-263">執行階段會探查下列 URL：</span><span class="sxs-lookup"><span data-stu-id="d981d-263">The runtime probes the following URLs:</span></span>

- `http://www.code.microsoft.com/de/myAssembly.dll`

- `http://www.code.microsoft.com/de/myAssembly/myAssembly.dll`

- `http://www.code.microsoft.com/bin/de/myAssembly.dll`

- `http://www.code.microsoft.com/bin/de/myAssembly/myAssembly.dll`

##### <a name="multiple-assemblies-with-the-same-name"></a><span data-ttu-id="d981d-264">具有相同名稱的多個組件</span><span class="sxs-lookup"><span data-stu-id="d981d-264">Multiple Assemblies with the Same Name</span></span>

<span data-ttu-id="d981d-265">下列範例示範如何設定具有相同名稱的多個組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-265">The following example shows how to configure multiple assemblies with the same name.</span></span>

```xml
<dependentAssembly>
   <assemblyIdentity name="Server" publicKeyToken="c0305c36380ba429" />
   <codeBase version="1.0.0.0" href="v1/Server.dll" />
   <codeBase version="2.0.0.0" href="v2/Server.dll" />
</dependentAssembly>
```

#### <a name="other-locations-probed"></a><span data-ttu-id="d981d-266">探查的其他位置</span><span class="sxs-lookup"><span data-stu-id="d981d-266">Other Locations Probed</span></span>

<span data-ttu-id="d981d-267">組件位置也可以使用目前的繫結內容來決定。</span><span class="sxs-lookup"><span data-stu-id="d981d-267">Assembly location can also be determined using the current binding context.</span></span> <span data-ttu-id="d981d-268">當使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法時，以及在 COM Interop 案例中，最常發生這個情況。</span><span class="sxs-lookup"><span data-stu-id="d981d-268">This most often occurs when the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method is used and in COM interop scenarios.</span></span> <span data-ttu-id="d981d-269">如果組件使用 <xref:System.Reflection.Assembly.LoadFrom%2A> 方法來參考另一個組件，呼叫組件的位置會被視為有關在哪裡可以找到參考組件的提示。</span><span class="sxs-lookup"><span data-stu-id="d981d-269">If an assembly uses the <xref:System.Reflection.Assembly.LoadFrom%2A> method to reference another assembly, the calling assembly's location is considered to be a hint about where to find the referenced assembly.</span></span> <span data-ttu-id="d981d-270">如果找到相符項目，就會載入該組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-270">If a match is found, that assembly is loaded.</span></span> <span data-ttu-id="d981d-271">如果沒有找到相符項目，執行階段會繼續進行其搜尋語意，然後查詢 Windows Installer，以提供組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-271">If no match is found, the runtime continues with its search semantics and then queries the Windows Installer to provide the assembly.</span></span> <span data-ttu-id="d981d-272">如果沒有提供符合繫結要求的組件，則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d981d-272">If no assembly is provided that matches the binding request, an exception is thrown.</span></span> <span data-ttu-id="d981d-273">如果有參考類型，此例外狀況是 Managed 程式碼中的 <xref:System.TypeLoadException> ，如果找不到要載入的組件，則為 <xref:System.IO.FileNotFoundException> 。</span><span class="sxs-lookup"><span data-stu-id="d981d-273">This exception is a <xref:System.TypeLoadException> in managed code if a type was referenced, or a <xref:System.IO.FileNotFoundException> if an assembly being loaded was not found.</span></span>

<span data-ttu-id="d981d-274">比方說，如果 Assembly1 參考 Assembly2，而且 Assembly1 是從 `http://www.code.microsoft.com/utils` 下載，則該位置會被視為有關在哪裡可以找到 Assembly2.dll 的提示。</span><span class="sxs-lookup"><span data-stu-id="d981d-274">For example, if Assembly1 references Assembly2 and Assembly1 was downloaded from `http://www.code.microsoft.com/utils`, that location is considered to be a hint about where to find Assembly2.dll.</span></span> <span data-ttu-id="d981d-275">執行階段接著會探查 `http://www.code.microsoft.com/utils/Assembly2.dll` 和 `http://www.code.microsoft.com/utils/Assembly2/Assembly2.dll` 中的組件。</span><span class="sxs-lookup"><span data-stu-id="d981d-275">The runtime then probes for the assembly in `http://www.code.microsoft.com/utils/Assembly2.dll` and `http://www.code.microsoft.com/utils/Assembly2/Assembly2.dll`.</span></span> <span data-ttu-id="d981d-276">如果在這兩個位置都找不到 Assembly2，執行階段就會查詢 Windows Installer。</span><span class="sxs-lookup"><span data-stu-id="d981d-276">If Assembly2 is not found at either of those locations, the runtime queries the Windows Installer.</span></span>

## <a name="see-also"></a><span data-ttu-id="d981d-277">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d981d-277">See also</span></span>

- [<span data-ttu-id="d981d-278">組件載入的最佳做法</span><span class="sxs-lookup"><span data-stu-id="d981d-278">Best Practices for Assembly Loading</span></span>](best-practices-for-assembly-loading.md)
- [<span data-ttu-id="d981d-279">部署</span><span class="sxs-lookup"><span data-stu-id="d981d-279">Deployment</span></span>](index.md)

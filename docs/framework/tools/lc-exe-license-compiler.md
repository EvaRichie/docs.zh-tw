---
title: Lc.exe (授權編譯器)
description: 使用 Lc.exe 授權編譯器。 此工具會讀取具有授權資訊的文字檔，並將二進位檔案內嵌在 CLR 可執行檔中做為資源。
ms.date: 03/30/2017
helpviewer_keywords:
- Lc.exe
- .licx file
- License Compiler
- control licenses [Windows Forms]
- compiling licenses file
- license file
- .licenses file
- Windows Forms, control licenses
- licensed controls [Windows Forms]
ms.assetid: 2de803b8-495e-4982-b209-19a72aba0460
ms.openlocfilehash: d1644ff4d69c857e36e87f7e83f668908b7ba021
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275758"
---
# <a name="lcexe-license-compiler"></a><span data-ttu-id="cc99d-104">Lc.exe (授權編譯器)</span><span class="sxs-lookup"><span data-stu-id="cc99d-104">Lc.exe (License Compiler)</span></span>

<span data-ttu-id="cc99d-105">授權編譯器可以讀取包含授權資訊的文字檔，並產生可內嵌於通用語言執行平台可執行檔的二進位檔案做為資源。</span><span class="sxs-lookup"><span data-stu-id="cc99d-105">The License Compiler reads text files that contain licensing information and produces a binary file that can be embedded in a common language runtime executable as a resource.</span></span>  
  
 <span data-ttu-id="cc99d-106">每當將授權控制項加入至表單時，Windows Form 設計工具便會自動產生或更新 .licx 文字檔。</span><span class="sxs-lookup"><span data-stu-id="cc99d-106">A .licx text file is automatically generated or updated by the Windows Forms Designer whenever a licensed control is added to the form.</span></span> <span data-ttu-id="cc99d-107">專案系統會將 .licx 文字檔轉換為可支援 .NET 控制項授權的 .licenses 二進位資源，當做編譯的一部分。</span><span class="sxs-lookup"><span data-stu-id="cc99d-107">As part of compilation, the project system will transform the .licx text file into a .licenses binary resource that provides support for .NET control licensing.</span></span> <span data-ttu-id="cc99d-108">接著此二進位資源將嵌入專案輸出。</span><span class="sxs-lookup"><span data-stu-id="cc99d-108">The binary resource will then be embedded in the project output.</span></span>  
  
 <span data-ttu-id="cc99d-109">使用授權編譯器建置您的專案時，不支援 32 位元與 64 位元之間的跨平台編譯。</span><span class="sxs-lookup"><span data-stu-id="cc99d-109">Cross compilation between 32-bit and 64-bit is not supported when you use the License Compiler when building your project.</span></span> <span data-ttu-id="cc99d-110">這是因為授權編譯器必須載入組件，卻不允許從 32 位元應用程式載入 64 位元組件，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="cc99d-110">This is because the License Compiler has to load assemblies, and loading 64-bit assemblies from a 32-bit application is not allowed, and vice versa.</span></span> <span data-ttu-id="cc99d-111">在這種情況下，請使用授權編譯器，以手動方式從命令列編譯授權，並指定對應的架構。</span><span class="sxs-lookup"><span data-stu-id="cc99d-111">In this case, use the License Compiler from the command line to compile the license manually, and specify the corresponding architecture.</span></span>  
  
 <span data-ttu-id="cc99d-112">此工具會自動與 Visual Studio 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="cc99d-112">This tool is automatically installed with Visual Studio.</span></span> <span data-ttu-id="cc99d-113">若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。</span><span class="sxs-lookup"><span data-stu-id="cc99d-113">To run the tool, use the Developer Command Prompt for Visual Studio (or the Visual Studio Command Prompt in Windows 7).</span></span> <span data-ttu-id="cc99d-114">如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="cc99d-114">For more information, see [Command Prompts](developer-command-prompt-for-vs.md).</span></span>  
  
 <span data-ttu-id="cc99d-115">在命令提示字元中，請輸入下列項目：</span><span class="sxs-lookup"><span data-stu-id="cc99d-115">At the command prompt, type the following:</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="cc99d-116">Syntax</span><span class="sxs-lookup"><span data-stu-id="cc99d-116">Syntax</span></span>  
  
```console
      lc /target:  
targetPE /complist:filename [-outdir:path]  
/i:modules [/nologo] [/v]  
```  
  
|<span data-ttu-id="cc99d-117">選項</span><span class="sxs-lookup"><span data-stu-id="cc99d-117">Option</span></span>|<span data-ttu-id="cc99d-118">描述</span><span class="sxs-lookup"><span data-stu-id="cc99d-118">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="cc99d-119">**/complist: filename** </span><span class="sxs-lookup"><span data-stu-id="cc99d-119">**/complist:** *filename*</span></span>|<span data-ttu-id="cc99d-120">指定要包含在 .licenses 檔案中含有授權元件清單的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="cc99d-120">Specifies the name of a file that contains the list of licensed components to include in the .licenses file.</span></span> <span data-ttu-id="cc99d-121">使用元件的完整名稱與每行只有一個元件方式參考每個元件。</span><span class="sxs-lookup"><span data-stu-id="cc99d-121">Each component is referenced using its full name with only one component per line.</span></span><br /><br /> <span data-ttu-id="cc99d-122">命令列使用者可以為專案中的每個表單指定個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="cc99d-122">Command-line users can specify a separate file for each form in the project.</span></span> <span data-ttu-id="cc99d-123">Lc.exe 接受多個輸入檔並產生單一 .licenses 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc99d-123">Lc.exe accepts multiple input files and produces a single .licenses file.</span></span>|  
|<span data-ttu-id="cc99d-124">**/h**[**elp**]</span><span class="sxs-lookup"><span data-stu-id="cc99d-124">**/h**[**elp**]</span></span>|<span data-ttu-id="cc99d-125">顯示工具的命令語法和選項。</span><span class="sxs-lookup"><span data-stu-id="cc99d-125">Displays command syntax and options for the tool.</span></span>|  
|<span data-ttu-id="cc99d-126">**/i: module** </span><span class="sxs-lookup"><span data-stu-id="cc99d-126">**/i:** *module*</span></span>|<span data-ttu-id="cc99d-127">指定包含列於 **/complist** 檔案中之元件的模組。</span><span class="sxs-lookup"><span data-stu-id="cc99d-127">Specifies the modules that contain the components listed in the **/complist** file.</span></span> <span data-ttu-id="cc99d-128">若要指定一個以上的模組，請使用多個 **/i** 旗標。</span><span class="sxs-lookup"><span data-stu-id="cc99d-128">To specify more than one module, use multiple **/i** flags.</span></span>|  
|<span data-ttu-id="cc99d-129">**/nologo**</span><span class="sxs-lookup"><span data-stu-id="cc99d-129">**/nologo**</span></span>|<span data-ttu-id="cc99d-130">隱藏 Microsoft 程式啟始資訊顯示。</span><span class="sxs-lookup"><span data-stu-id="cc99d-130">Suppresses the Microsoft startup banner display.</span></span>|  
|<span data-ttu-id="cc99d-131">**/outdir: path** </span><span class="sxs-lookup"><span data-stu-id="cc99d-131">**/outdir:** *path*</span></span>|<span data-ttu-id="cc99d-132">指定要放置輸出 .licenses 檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="cc99d-132">Specifies the directory in which to place the output .licenses file.</span></span>|  
|<span data-ttu-id="cc99d-133">**/target: targetPE** </span><span class="sxs-lookup"><span data-stu-id="cc99d-133">**/target:** *targetPE*</span></span>|<span data-ttu-id="cc99d-134">指定要產生 .licenses 檔案的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="cc99d-134">Specifies the executable for which the .licenses file is being generated.</span></span>|  
|<span data-ttu-id="cc99d-135">**/v**</span><span class="sxs-lookup"><span data-stu-id="cc99d-135">**/v**</span></span>|<span data-ttu-id="cc99d-136">指定詳細資訊模式；顯示編譯程序資訊。</span><span class="sxs-lookup"><span data-stu-id="cc99d-136">Specifies verbose mode; displays compilation progress information.</span></span>|  
|<span data-ttu-id="cc99d-137">\**@\*\*\*file* 檔案</span><span class="sxs-lookup"><span data-stu-id="cc99d-137">**@** *file*</span></span>|<span data-ttu-id="cc99d-138">指定回應檔 (.rsp)。</span><span class="sxs-lookup"><span data-stu-id="cc99d-138">Specifies the response (.rsp) file.</span></span>|  
|<span data-ttu-id="cc99d-139">**/?**</span><span class="sxs-lookup"><span data-stu-id="cc99d-139">**/?**</span></span>|<span data-ttu-id="cc99d-140">顯示工具的命令語法和選項。</span><span class="sxs-lookup"><span data-stu-id="cc99d-140">Displays command syntax and options for the tool.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="cc99d-141">範例</span><span class="sxs-lookup"><span data-stu-id="cc99d-141">Example</span></span>  
  
1. <span data-ttu-id="cc99d-142">如果您要使用名為 `HostApp.exe` 之應用程式中 `Samples.DLL` 所包含的授權控制項 `MyCompany.Samples.LicControl1`，可以建立包含下列程式碼的 `HostAppLic.txt`。</span><span class="sxs-lookup"><span data-stu-id="cc99d-142">If you are using a licensed control `MyCompany.Samples.LicControl1` contained in `Samples.DLL` in an application called `HostApp.exe`*,* you can create `HostAppLic.txt` that contains the following.</span></span>  
  
    ```text
    MyCompany.Samples.LicControl1, Samples.DLL  
    ```  
  
2. <span data-ttu-id="cc99d-143">使用下列命令建立這個稱為 `HostApp.exe.licenses` 的 .licenses 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc99d-143">Create the .licenses file called `HostApp.exe.licenses` using the following command.</span></span>  
  
    ```console  
    lc /target:HostApp.exe /complist:hostapplic.txt /i:Samples.DLL /outdir:c:\bindir  
    ```  
  
3. <span data-ttu-id="cc99d-144">建置包含 .licenses 檔案當做資源的 `HostApp.exe`。</span><span class="sxs-lookup"><span data-stu-id="cc99d-144">Build `HostApp.exe` including the .licenses file as a resource.</span></span> <span data-ttu-id="cc99d-145">如果您正在建置 C# 應用程式，可以使用下列命令來建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc99d-145">If you were building a C# application you would use the following command to build your application.</span></span>  
  
    ```console
    csc /res:HostApp.exe.licenses /out:HostApp.exe *.cs  
    ```  
  
 <span data-ttu-id="cc99d-146">下列命令會從由 `myApp.licenses`、`hostapplic.txt` 和 `hostapplic2.txt` 所指定的授權元件清單編譯 `hostapplic3.txt`。</span><span class="sxs-lookup"><span data-stu-id="cc99d-146">The following command compiles `myApp.licenses` from the lists of licensed components specified by `hostapplic.txt`, `hostapplic2.txt` and `hostapplic3.txt`.</span></span> <span data-ttu-id="cc99d-147">`modulesList` 引數是指定包含授權元件的模組。</span><span class="sxs-lookup"><span data-stu-id="cc99d-147">The `modulesList` argument specifies the modules that contain the licensed components.</span></span>  
  
```console  
lc /target:myApp /complist:hostapplic.txt /complist:hostapplic2.txt /complist: hostapplic3.txt /i:modulesList  
```  
  
## <a name="response-file-example"></a><span data-ttu-id="cc99d-148">回應檔範例</span><span class="sxs-lookup"><span data-stu-id="cc99d-148">Response File Example</span></span>  

 <span data-ttu-id="cc99d-149">下列清單顯示回應檔 `response.rsp` 的範例。</span><span class="sxs-lookup"><span data-stu-id="cc99d-149">The following listing shows an example of a response file, `response.rsp`.</span></span> <span data-ttu-id="cc99d-150">如需回應檔的詳細資訊，請參閱[回應檔](/visualstudio/msbuild/msbuild-response-files)。</span><span class="sxs-lookup"><span data-stu-id="cc99d-150">For more information on response files, see [Response Files](/visualstudio/msbuild/msbuild-response-files).</span></span>  
  
```text  
/target:hostapp.exe  
/complist:hostapplic.txt
/i:WFCPrj.dll
/outdir:"C:\My Folder"  
```  
  
 <span data-ttu-id="cc99d-151">下列命令列使用 `response.rsp` 檔。</span><span class="sxs-lookup"><span data-stu-id="cc99d-151">The following command line uses the `response.rsp` file.</span></span>  
  
```console  
lc @response.rsp  
```  
  
## <a name="see-also"></a><span data-ttu-id="cc99d-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cc99d-152">See also</span></span>

- [<span data-ttu-id="cc99d-153">工具</span><span class="sxs-lookup"><span data-stu-id="cc99d-153">Tools</span></span>](index.md)
- [<span data-ttu-id="cc99d-154">Al.exe (元件連結器) </span><span class="sxs-lookup"><span data-stu-id="cc99d-154">Al.exe (Assembly Linker)</span></span>](al-exe-assembly-linker.md)
- [<span data-ttu-id="cc99d-155">命令提示字元</span><span class="sxs-lookup"><span data-stu-id="cc99d-155">Command Prompts</span></span>](developer-command-prompt-for-vs.md)

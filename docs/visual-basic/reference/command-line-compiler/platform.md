---
title: -platform
ms.date: 03/13/2018
helpviewer_keywords:
- platform compiler option [Visual Basic]
- /platform compiler option [Visual Basic]
- -platform compiler option [Visual Basic]
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
ms.openlocfilehash: 488a1da6b25bcb4b42f0d355c6faee542046d0f5
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91098887"
---
# <a name="-platform-visual-basic"></a><span data-ttu-id="1ddc4-102">-platform (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="1ddc4-102">-platform (Visual Basic)</span></span>

<span data-ttu-id="1ddc4-103">指定通用語言執行平台 (CLR) 的哪個平台版本可以執行輸出檔。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-103">Specifies which platform version of common language runtime (CLR) can run the output file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1ddc4-104">語法</span><span class="sxs-lookup"><span data-stu-id="1ddc4-104">Syntax</span></span>  
  
```console  
-platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## <a name="arguments"></a><span data-ttu-id="1ddc4-105">引數</span><span class="sxs-lookup"><span data-stu-id="1ddc4-105">Arguments</span></span>  
  
|<span data-ttu-id="1ddc4-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="1ddc4-106">Term</span></span>|<span data-ttu-id="1ddc4-107">定義</span><span class="sxs-lookup"><span data-stu-id="1ddc4-107">Definition</span></span>|  
|---|---|  
|`x86`|<span data-ttu-id="1ddc4-108">將組件編譯為以 32 位元、與 x86 相容的 CLR 執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-108">Compiles your assembly to be run by the 32-bit, x86-compatible CLR.</span></span>|  
|`x64`|<span data-ttu-id="1ddc4-109">在支援 AMD64 或 EM64T 指令集的電腦上編譯將由 64 位元 CLR 所執行的組件。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-109">Compiles your assembly to be run by the 64-bit CLR on a computer that supports the AMD64 or EM64T instruction set.</span></span>|  
|`Itanium`|<span data-ttu-id="1ddc4-110">將組件編譯為可以在使用 Itanium 處理器的電腦上以 64 位元 CLR 執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-110">Compiles your assembly to be run by the 64-bit CLR on a computer with an Itanium processor.</span></span>|  
|`arm`|<span data-ttu-id="1ddc4-111">將組件編譯為可以在配備 ARM (進階 RISC 機器) 處理器的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-111">Compiles your assembly to be run on a computer with an ARM (Advanced RISC Machine) processor.</span></span>|  
|`anycpu`|<span data-ttu-id="1ddc4-112">編譯要在任何平台上執行的組件。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-112">Compiles your assembly to run on any platform.</span></span> <span data-ttu-id="1ddc4-113">應用程式將在 32 位元版本的 Windows 上當做 32 位元應用程式執行，並在 64 位元版本的 Windows 上當做 64 位元應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-113">The application will run as a 32-bit application on 32-bit versions of Windows and as a 64-bit application on 64-bit versions of Windows.</span></span> <span data-ttu-id="1ddc4-114">此旗標為預設值。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-114">This flag is the default value.</span></span>|  
|`anycpu32bitpreferred`|<span data-ttu-id="1ddc4-115">編譯要在任何平台上執行的組件。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-115">Compiles your assembly to run on any platform.</span></span> <span data-ttu-id="1ddc4-116">應用程式將在 32 位元和 64 位元版本的 Windows 上當做 32 位元應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-116">The application will run as a 32-bit application on both 32-bit and 64-bit versions of Windows.</span></span> <span data-ttu-id="1ddc4-117">只有 ( 可執行檔時，此旗標才有效。EXE) ，且需要 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-117">This flag is valid only for executables (.EXE) and requires .NET Framework 4.5.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="1ddc4-118">備註</span><span class="sxs-lookup"><span data-stu-id="1ddc4-118">Remarks</span></span>  

 <span data-ttu-id="1ddc4-119">使用 `-platform` 選項指定做為輸出檔目標的處理器類型。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-119">Use the `-platform` option to specify the type of processor targeted by the output file.</span></span>  
  
 <span data-ttu-id="1ddc4-120">一般而言，不論是何種平台，以 Visual Basic 撰寫的.NET Framework 組件將會執行相同作業。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-120">In general, .NET Framework assemblies written in Visual Basic will run the same regardless of the platform.</span></span> <span data-ttu-id="1ddc4-121">不過，有某些情況下，在不同的平台上有不同的行為。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-121">However, there are some cases that behave differently on different platforms.</span></span> <span data-ttu-id="1ddc4-122">常見的情況如下：</span><span class="sxs-lookup"><span data-stu-id="1ddc4-122">These common cases are:</span></span>  
  
- <span data-ttu-id="1ddc4-123">包含的成員視平台而變更大小的結構，例如任何指標類型。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-123">Structures that contain members that change size depending on the platform, such as any pointer type.</span></span>  
  
- <span data-ttu-id="1ddc4-124">包含常數大小的指標算術。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-124">Pointer arithmetic that includes constant sizes.</span></span>  
  
- <span data-ttu-id="1ddc4-125">不正確的平台叫用，或是使用 `Integer` 而不是 <xref:System.IntPtr> 作為控點的 COM 宣告。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-125">Incorrect platform invoke or COM declarations that use `Integer` for handles instead of <xref:System.IntPtr>.</span></span>  
  
- <span data-ttu-id="1ddc4-126">將 <xref:System.IntPtr> 轉型為 `Integer`。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-126">Casting <xref:System.IntPtr> to `Integer`.</span></span>  
  
- <span data-ttu-id="1ddc4-127">使用其元件不存在於所有平台的平台叫用或 COM Interop。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-127">Using platform invoke or COM interop with components that do not exist on all platforms.</span></span>  
  
 <span data-ttu-id="1ddc4-128">如果您知道您已對程式碼將在其上執行的架構進行假設，則 **-platform** 選項將可緩和某些問題。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-128">The **-platform** option will mitigate some issues if you know you have made assumptions about the architecture your code will run on.</span></span> <span data-ttu-id="1ddc4-129">尤其是：</span><span class="sxs-lookup"><span data-stu-id="1ddc4-129">Specifically:</span></span>  
  
- <span data-ttu-id="1ddc4-130">如果您決定以 64 位元平台為目標，並在 32 位元電腦上執行應用程式，錯誤訊息會遠遠較早出現，而且會較以平台為目標，超過以不使用這個參數所發生的錯誤為目標。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-130">If you decide to target a 64-bit platform, and the application is run on a 32-bit machine, the error message comes much earlier and is more targeted at the problem than the error that occurs without using this switch.</span></span>  
  
- <span data-ttu-id="1ddc4-131">如果您在選項上設定 `x86` 旗標，且隨後在 64 位元電腦上執行應用程式，則應用程式會在 WOW 子系統中執行，而不是以原生方式執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-131">If you set the `x86` flag on the option and the application is subsequently run on a 64-bit machine, the application will run in the WOW subsystem instead of running natively.</span></span>  
  
 <span data-ttu-id="1ddc4-132">在 64 位元 Windows 作業系統上：</span><span class="sxs-lookup"><span data-stu-id="1ddc4-132">On a 64-bit Windows operating system:</span></span>  
  
- <span data-ttu-id="1ddc4-133">使用 `-platform:x86` 編譯的組件將在 WOW64 下執行的 32 位元 CLR 上執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-133">Assemblies compiled with `-platform:x86` will execute on the 32-bit CLR running under WOW64.</span></span>  
  
- <span data-ttu-id="1ddc4-134">使用 `-platform:anycpu` 編譯的可執行檔將在 64 位元 CLR 上執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-134">Executables compiled with the `-platform:anycpu` will execute on the 64-bit CLR.</span></span>  
  
- <span data-ttu-id="1ddc4-135">使用 `-platform:anycpu` 編譯的 DLL 將在與其載入所在處理序相同的 CLR 上執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-135">A DLL compiled with the `-platform:anycpu` will execute on the same CLR as the process into which it loaded.</span></span>  
  
- <span data-ttu-id="1ddc4-136">使用 `-platform:anycpu32bitpreferred` 編譯的可執行檔將在 32 位元 CLR 上執行。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-136">Executables that are compiled with `-platform:anycpu32bitpreferred` will execute on the 32-bit CLR.</span></span>  
  
 <span data-ttu-id="1ddc4-137">如需如何開發應用程式以在64位版本的 Windows 上執行的詳細資訊，請參閱 [64 位應用程式](../../../framework/64-bit-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-137">For more information about how to develop an application to run on a 64-bit version of Windows, see [64-bit Applications](../../../framework/64-bit-apps.md).</span></span>  
  
### <a name="to-set--platform-in-the-visual-studio-ide"></a><span data-ttu-id="1ddc4-138">在 Visual Studio IDE 中設定平臺</span><span class="sxs-lookup"><span data-stu-id="1ddc4-138">To set -platform in the Visual Studio IDE</span></span>  
  
1. <span data-ttu-id="1ddc4-139">在 **方案總管**中，選擇專案，開啟 [ **專案** ] 功能表，然後按一下 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-139">In **Solution Explorer**, choose the project, open the **Project** menu, and then click **Properties**.</span></span>  
  
2. <span data-ttu-id="1ddc4-140">在 [ **編譯** ] 索引標籤上，選取或清除 [ **慣用 32** 位] 核取方塊，或在 [ **目標 CPU** ] 清單中選擇一個值。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-140">On the **Compile** tab, select or clear the **Prefer 32-bit** check box, or, in the **Target CPU** list, choose a value.</span></span>  
  
     <span data-ttu-id="1ddc4-141">如需詳細資訊，請參閱 [編譯頁面、專案設計工具 (Visual Basic) ](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-141">For more information, see [Compile Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic).</span></span>  
  
## <a name="example"></a><span data-ttu-id="1ddc4-142">範例</span><span class="sxs-lookup"><span data-stu-id="1ddc4-142">Example</span></span>  

 <span data-ttu-id="1ddc4-143">下列範例說明如何使用 `-platform` 編譯器選項。</span><span class="sxs-lookup"><span data-stu-id="1ddc4-143">The following example illustrates how to use the `-platform` compiler option.</span></span>  
  
```console
vbc -platform:x86 myFile.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="1ddc4-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1ddc4-144">See also</span></span>

- [<span data-ttu-id="1ddc4-145">-目標 (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="1ddc4-145">-target (Visual Basic)</span></span>](target.md)
- [<span data-ttu-id="1ddc4-146">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="1ddc4-146">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="1ddc4-147">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="1ddc4-147">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)

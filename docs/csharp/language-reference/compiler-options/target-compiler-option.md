---
title: -target (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /target
helpviewer_keywords:
- target compiler options [C#]
- /target compiler options [C#]
- assemblies [C#], compiling
- -target compiler options [C#]
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
ms.openlocfilehash: 80cec001b27000e71b74f380a0f33e30602c01af
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86473905"
---
# <a name="-target-c-compiler-options"></a><span data-ttu-id="8a2a5-102">-target (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="8a2a5-102">-target (C# Compiler Options)</span></span>
<span data-ttu-id="8a2a5-103">可以用下列其中一種形式指定 **-target**編譯器選項：</span><span class="sxs-lookup"><span data-stu-id="8a2a5-103">The **-target** compiler option can be specified in one of the following forms:</span></span>  
  
 [<span data-ttu-id="8a2a5-104">-target:appcontainerexe</span><span class="sxs-lookup"><span data-stu-id="8a2a5-104">-target:appcontainerexe</span></span>](./target-appcontainerexe-compiler-option.md)  
 <span data-ttu-id="8a2a5-105">建立 Windows 8.x 存放區應用程式的 .exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-105">To create an .exe file for Windows 8.x Store apps.</span></span>  
  
 [<span data-ttu-id="8a2a5-106">-target:exe</span><span class="sxs-lookup"><span data-stu-id="8a2a5-106">-target:exe</span></span>](./target-exe-compiler-option.md)  
 <span data-ttu-id="8a2a5-107">建立 .exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-107">To create an .exe file.</span></span>  
  
 [<span data-ttu-id="8a2a5-108">-target:library</span><span class="sxs-lookup"><span data-stu-id="8a2a5-108">-target:library</span></span>](./target-library-compiler-option.md)  
 <span data-ttu-id="8a2a5-109">建立程式碼程式庫。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-109">To create a code library.</span></span>  
  
 [<span data-ttu-id="8a2a5-110">-target:module</span><span class="sxs-lookup"><span data-stu-id="8a2a5-110">-target:module</span></span>](./target-module-compiler-option.md)  
 <span data-ttu-id="8a2a5-111">建立模組。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-111">To create a module.</span></span>  
  
 [<span data-ttu-id="8a2a5-112">-target:winexe</span><span class="sxs-lookup"><span data-stu-id="8a2a5-112">-target:winexe</span></span>](./target-winexe-compiler-option.md)  
 <span data-ttu-id="8a2a5-113">建立 Windows 程式。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-113">To create a Windows program.</span></span>  
  
 [<span data-ttu-id="8a2a5-114">-target:winmdobj</span><span class="sxs-lookup"><span data-stu-id="8a2a5-114">-target:winmdobj</span></span>](./target-winmdobj-compiler-option.md)  
 <span data-ttu-id="8a2a5-115">建立中繼 .winmdobj 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-115">To create an intermediate .winmdobj file.</span></span>  
  
 <span data-ttu-id="8a2a5-116">除非您指定 **-target： module**，否則 **-target**會將 .NET Framework 的組件資訊清單放在輸出檔中。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-116">Unless you specify **-target:module**, **-target** causes a .NET Framework assembly manifest to be placed in an output file.</span></span> <span data-ttu-id="8a2a5-117">如需詳細資訊，請參閱[.net 中的元件](../../../standard/assembly/index.md)和[通用屬性](../attributes/global.md)。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-117">For more information, see [Assemblies in .NET](../../../standard/assembly/index.md) and [Common Attributes](../attributes/global.md).</span></span>  
  
 <span data-ttu-id="8a2a5-118">編譯時，組件資訊清單會放在第一個 .exe 輸出檔，如果沒有 .exe 輸出檔，則會放在第一個 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-118">The assembly manifest is placed in the first .exe output file in the compilation or in the first DLL, if there is no .exe output file.</span></span> <span data-ttu-id="8a2a5-119">例如，在下列命令列中，資訊清單會放在 `1.exe` 中：</span><span class="sxs-lookup"><span data-stu-id="8a2a5-119">For example, in the following command line, the manifest will be placed in `1.exe`:</span></span>  
  
```console  
csc -out:1.exe t1.cs -out:2.netmodule t2.cs  
```  
  
 <span data-ttu-id="8a2a5-120">編譯器在每次編譯時都只會建立一個組件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-120">The compiler creates only one assembly manifest per compilation.</span></span> <span data-ttu-id="8a2a5-121">編譯中所有檔案的資訊會放入組件資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-121">Information about all files in a compilation is placed in the assembly manifest.</span></span> <span data-ttu-id="8a2a5-122">除了以 **-target： module**所建立的輸出檔以外，所有輸出檔案都可以包含組件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-122">All output files except those created with **-target:module** can contain an assembly manifest.</span></span> <span data-ttu-id="8a2a5-123">在命令列產生多個輸出檔時，只能建立一個組件資訊清單，而且它必須移至命令列上所指定的第一個輸出檔。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-123">When producing multiple output files at the command line, only one assembly manifest can be created and it must go into the first output file specified on the command line.</span></span> <span data-ttu-id="8a2a5-124">不論第一個輸出檔是什麼（**-target： exe**、 **-target： winexe**、 **-target： library**或-target **： module**），在相同編譯中產生的任何其他輸出檔都必須是模組（**-target： module**）。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-124">No matter what the first output file is (**-target:exe**, **-target:winexe**, **-target:library** or **-target:module**), any other output files produced in the same compilation must be modules (**-target:module**).</span></span>  
  
 <span data-ttu-id="8a2a5-125">如果您建立組件，則可以使用 <xref:System.CLSCompliantAttribute> 屬性指出所有或部分程式碼符合 CLS 標準。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-125">If you create an assembly, you can indicate that all or part of your code is CLS compliant with the <xref:System.CLSCompliantAttribute> attribute.</span></span>  
  
```csharp  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 <span data-ttu-id="8a2a5-126">如需以程式設計方式設定這個編譯器選項的詳細資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。</span><span class="sxs-lookup"><span data-stu-id="8a2a5-126">For more information about setting this compiler option programmatically, see <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8a2a5-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a2a5-127">See also</span></span>

- [<span data-ttu-id="8a2a5-128">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="8a2a5-128">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="8a2a5-129">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="8a2a5-129">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
- [<span data-ttu-id="8a2a5-130">-subsystemversion (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="8a2a5-130">-subsystemversion (C# Compiler Options)</span></span>](./subsystemversion-compiler-option.md)

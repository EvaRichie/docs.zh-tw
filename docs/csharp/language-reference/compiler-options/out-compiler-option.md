---
description: -out (C# 編譯器選項)
title: -out (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /out
helpviewer_keywords:
- /out compiler option [C#]
- out compiler option [C#]
- -out compiler option [C#]
ms.assetid: 70d91d01-7bd2-4aea-ba8b-4e9807e9caa5
ms.openlocfilehash: 409760ee0b147065a2128c62c304fb5d70cfcf42
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193877"
---
# <a name="-out-c-compiler-options"></a><span data-ttu-id="32971-103">-out (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="32971-103">-out (C# Compiler Options)</span></span>

<span data-ttu-id="32971-104">**-out** 選項指定輸出檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="32971-104">The **-out** option specifies the name of the output file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="32971-105">語法</span><span class="sxs-lookup"><span data-stu-id="32971-105">Syntax</span></span>  
  
```console  
-out:filename  
```  
  
## <a name="arguments"></a><span data-ttu-id="32971-106">引數</span><span class="sxs-lookup"><span data-stu-id="32971-106">Arguments</span></span>  

 `filename`  
 <span data-ttu-id="32971-107">編譯器所建立的輸出檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="32971-107">The name of the output file created by the compiler.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="32971-108">備註</span><span class="sxs-lookup"><span data-stu-id="32971-108">Remarks</span></span>  

 <span data-ttu-id="32971-109">在命令列中，可以為您的編譯指定多個輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="32971-109">On the command line, it is possible to specify multiple output files for your compilation.</span></span> <span data-ttu-id="32971-110">編譯器預期在 **-out** 選項之後找到一或多個原始程式碼檔。</span><span class="sxs-lookup"><span data-stu-id="32971-110">The compiler expects to find one or more source code files following the **-out** option.</span></span> <span data-ttu-id="32971-111">之後，所有原始程式碼檔都會編譯至 **-out** 選項所指定的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="32971-111">Then, all source code files will be compiled into the output file specified by that **-out** option.</span></span>  
  
 <span data-ttu-id="32971-112">請指定您要建立的檔案的完整名稱和副檔名。</span><span class="sxs-lookup"><span data-stu-id="32971-112">Specify the full name and extension of the file you want to create.</span></span>  
  
 <span data-ttu-id="32971-113">如果您未指定輸出檔案的名稱：</span><span class="sxs-lookup"><span data-stu-id="32971-113">If you do not specify the name of the output file:</span></span>  
  
- <span data-ttu-id="32971-114">.exe 的名稱將來自從包含 **Main** 方法的原始程式碼檔。</span><span class="sxs-lookup"><span data-stu-id="32971-114">An .exe will take its name from the source code file that contains the **Main** method.</span></span>  
  
- <span data-ttu-id="32971-115">.dll 或 .netmodule 的名稱將來自第一個原始程式碼檔。</span><span class="sxs-lookup"><span data-stu-id="32971-115">A .dll or .netmodule will take its name from the first source code file.</span></span>  
  
 <span data-ttu-id="32971-116">用來編譯某個輸出檔案的原始程式碼檔，不能在同一個編譯中用於編譯另一個輸出檔。</span><span class="sxs-lookup"><span data-stu-id="32971-116">A source code file used to compile one output file cannot be used in the same compilation for the compilation of another output file.</span></span>  
  
 <span data-ttu-id="32971-117">在命令列編譯中產生多個輸出檔案時，請記住，只有其中一個輸出檔案可以是組件，而且只有 (使用 **-out** 隱含或明確) 指定的第一個輸出檔案可以是組件。</span><span class="sxs-lookup"><span data-stu-id="32971-117">When producing multiple output files in a command-line compilation, keep in mind that only one of the output files can be an assembly and that only the first output file specified (implicitly or explicitly with **-out**) can be the assembly.</span></span>  
  
 <span data-ttu-id="32971-118">任何在編譯過程中產生的模組，都會變成與編譯中同時產生的任何組件建立關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="32971-118">Any modules produced as part of a compilation become files associated with any assembly also produced in the compilation.</span></span> <span data-ttu-id="32971-119">請使用 [ildasm.exe](../../../framework/tools/ildasm-exe-il-disassembler.md) 來檢視組件資訊清單，以查看關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="32971-119">Use [ildasm.exe](../../../framework/tools/ildasm-exe-il-disassembler.md) to view the assembly manifest to see the associated files.</span></span>  
  
 <span data-ttu-id="32971-120">必須有 -out 編譯器選項，才能讓 exe 成為 Friend 組件的目標。</span><span class="sxs-lookup"><span data-stu-id="32971-120">The -out compiler option is required in order for an exe to be the target of a friend assembly.</span></span> <span data-ttu-id="32971-121">如需詳細資訊，請參閱 [Friend 組件](../../../standard/assembly/friend.md)。</span><span class="sxs-lookup"><span data-stu-id="32971-121">For more information see [Friend Assemblies](../../../standard/assembly/friend.md).</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="32971-122">在 Visual Studio 開發環境中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="32971-122">To set this compiler option in the Visual Studio development environment</span></span>  
  
1. <span data-ttu-id="32971-123">開啟專案的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="32971-123">Open the project's **Properties** page.</span></span>  
  
2. <span data-ttu-id="32971-124">按一下 [應用程式] 屬性頁。</span><span class="sxs-lookup"><span data-stu-id="32971-124">Click the **Application** property page.</span></span>  
  
3. <span data-ttu-id="32971-125">修改 **組件名稱** 屬性。</span><span class="sxs-lookup"><span data-stu-id="32971-125">Modify the **Assembly name** property.</span></span>  
  
     <span data-ttu-id="32971-126">若要以程式設計方式設定這個編譯器選項：<xref:VSLangProj80.ProjectProperties3.OutputFileName%2A> 是唯讀屬性，它是由專案類型 (exe、程式庫等等) 和組件名稱的組合所決定。</span><span class="sxs-lookup"><span data-stu-id="32971-126">To set this compiler option programmatically: the <xref:VSLangProj80.ProjectProperties3.OutputFileName%2A> is a read-only property, which is determined by a combination of the project type (exe, library, and so forth) and the assembly name.</span></span> <span data-ttu-id="32971-127">若要設定輸出檔案名稱，則必須修改一個或這兩個屬性。</span><span class="sxs-lookup"><span data-stu-id="32971-127">Modifying one or both of these properties will be necessary to set the output file name.</span></span>  
  
## <a name="example"></a><span data-ttu-id="32971-128">範例</span><span class="sxs-lookup"><span data-stu-id="32971-128">Example</span></span>  

 <span data-ttu-id="32971-129">編譯 `t.cs` 並建立 `t.exe` 輸出檔案，以及建置 `t2.cs` 並建立 `mymodule.netmodule` 模組輸出檔案：</span><span class="sxs-lookup"><span data-stu-id="32971-129">Compile `t.cs` and create output file `t.exe`, as well as build `t2.cs` and create module output file `mymodule.netmodule`:</span></span>  
  
```console  
csc t.cs -out:mymodule.netmodule -target:module t2.cs  
```  
  
## <a name="see-also"></a><span data-ttu-id="32971-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="32971-130">See also</span></span>

- [<span data-ttu-id="32971-131">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="32971-131">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="32971-132">Friend 組件</span><span class="sxs-lookup"><span data-stu-id="32971-132">Friend Assemblies</span></span>](../../../standard/assembly/friend.md)
- [<span data-ttu-id="32971-133">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="32971-133">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

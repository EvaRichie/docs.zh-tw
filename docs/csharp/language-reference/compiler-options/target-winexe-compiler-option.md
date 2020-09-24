---
description: -target:winexe (C# 編譯器選項)
title: -target:winexe (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /target:winexe
helpviewer_keywords:
- /target compiler options [C#], /target:winexe
- -target compiler options [C#], /target:winexe
- target compiler options [C#], /target:winexe
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
ms.openlocfilehash: 6e14a2aac427c7adfd69f66eaf624816b75f6ea2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168929"
---
# <a name="-targetwinexe-c-compiler-options"></a><span data-ttu-id="bd64e-103">-target:winexe (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="bd64e-103">-target:winexe (C# Compiler Options)</span></span>

<span data-ttu-id="bd64e-104">**-target:winexe** 選項可讓編譯器建立可執行檔 (EXE)，其為一個 Windows 程式。</span><span class="sxs-lookup"><span data-stu-id="bd64e-104">The **-target:winexe** option causes the compiler to create an executable (EXE), Windows program.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bd64e-105">語法</span><span class="sxs-lookup"><span data-stu-id="bd64e-105">Syntax</span></span>  
  
```console  
-target:winexe  
```  
  
## <a name="remarks"></a><span data-ttu-id="bd64e-106">備註</span><span class="sxs-lookup"><span data-stu-id="bd64e-106">Remarks</span></span>  

 <span data-ttu-id="bd64e-107">將會建立副檔名為 .exe 的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="bd64e-107">The executable file will be created with the .exe extension.</span></span> <span data-ttu-id="bd64e-108">Windows 程式是從 .NET 程式庫或 Windows Api 提供使用者介面的程式。</span><span class="sxs-lookup"><span data-stu-id="bd64e-108">A Windows program is one that provides a user interface from either the .NET library or with the Windows APIs.</span></span>  
  
 <span data-ttu-id="bd64e-109">使用 [-target:exe](./target-exe-compiler-option.md) 建立主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd64e-109">Use [-target:exe](./target-exe-compiler-option.md) to create a console application.</span></span>  
  
 <span data-ttu-id="bd64e-110">除非特別使用 [-out](./out-compiler-option.md) 選項指定輸出檔案名稱，否則輸出檔案名稱會採用包含 [Main](../../programming-guide/main-and-command-args/index.md) 方法的輸入檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bd64e-110">Unless otherwise specified with the [-out](./out-compiler-option.md) option, the output file name takes the name of the input file that contains the [Main](../../programming-guide/main-and-command-args/index.md) method.</span></span>  
  
 <span data-ttu-id="bd64e-111">指定於命令列時，下一個 **-out** 或 [-target](./target-compiler-option.md) 選項之前的所有檔案都是用來建立 Windows 程式。</span><span class="sxs-lookup"><span data-stu-id="bd64e-111">When specified at the command line, all files until the next **-out** or [-target](./target-compiler-option.md) option are used to create the Windows program.</span></span>  
  
 <span data-ttu-id="bd64e-112">編譯為 .exe 檔案的原始程式碼檔中只需要一個 **Main** 方法。</span><span class="sxs-lookup"><span data-stu-id="bd64e-112">One and only one **Main** method is required in the source code files that are compiled into an .exe file.</span></span> <span data-ttu-id="bd64e-113">如果您的程式碼有多個具有 **Main** 方法的類別，則 [-main](./main-compiler-option.md) 選項可讓您指定哪個類別包含 **Main** 方法。</span><span class="sxs-lookup"><span data-stu-id="bd64e-113">The [-main](./main-compiler-option.md) option lets you specify which class contains the **Main** method, in cases where your code has more than one class with a **Main** method.</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="bd64e-114">在 Visual Studio 開發環境中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="bd64e-114">To set this compiler option in the Visual Studio development environment</span></span>  
  
1. <span data-ttu-id="bd64e-115">開啟專案的 [屬性]\*\*\*\* 頁面。</span><span class="sxs-lookup"><span data-stu-id="bd64e-115">Open the project's **Properties** page.</span></span>  
  
2. <span data-ttu-id="bd64e-116">按一下 [應用程式]\*\*\*\* 屬性頁。</span><span class="sxs-lookup"><span data-stu-id="bd64e-116">Click the **Application** property page.</span></span>  
  
3. <span data-ttu-id="bd64e-117">修改 [輸出類型]\*\*\*\* 屬性。</span><span class="sxs-lookup"><span data-stu-id="bd64e-117">Modify the **Output type** property.</span></span>  
  
 <span data-ttu-id="bd64e-118">如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。</span><span class="sxs-lookup"><span data-stu-id="bd64e-118">For information on how to set this compiler option programmatically, see <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="bd64e-119">範例</span><span class="sxs-lookup"><span data-stu-id="bd64e-119">Example</span></span>  

 <span data-ttu-id="bd64e-120">將 `in.cs` 編譯為 Windows 程式︰</span><span class="sxs-lookup"><span data-stu-id="bd64e-120">Compile `in.cs` into a Windows program:</span></span>  
  
```console  
csc -target:winexe in.cs  
```  
  
## <a name="see-also"></a><span data-ttu-id="bd64e-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bd64e-121">See also</span></span>

- [<span data-ttu-id="bd64e-122">-目標 (c # 編譯器選項) </span><span class="sxs-lookup"><span data-stu-id="bd64e-122">-target (C# Compiler Options)</span></span>](./target-compiler-option.md)
- [<span data-ttu-id="bd64e-123">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="bd64e-123">C# Compiler Options</span></span>](./index.md)

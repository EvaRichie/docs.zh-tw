---
description: -target:winmdobj (C# 編譯器選項)
title: -target:winmdobj (C# 編譯器選項)
ms.date: 07/20/2015
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
ms.openlocfilehash: 66a4bddb34832705ad4779829e561afd9442be8f
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89139082"
---
# <a name="-targetwinmdobj-c-compiler-options"></a><span data-ttu-id="d662e-103">-target:winmdobj (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="d662e-103">-target:winmdobj (C# Compiler Options)</span></span>
<span data-ttu-id="d662e-104">如果您使用 **-target:winmdobj** 編譯器選項，編譯器會建立一個可轉換成 Windows 執行階段二進位檔案 (.winmd) 的中繼 .winmdobj 檔案。</span><span class="sxs-lookup"><span data-stu-id="d662e-104">If you use the **-target:winmdobj** compiler option, the compiler creates an intermediate .winmdobj file that you can convert to a Windows Runtime binary (.winmd) file.</span></span> <span data-ttu-id="d662e-105">除了 Managed 語言程式之外，JavaScript 和 C++ 程式也可以使用 .winmd 檔案。</span><span class="sxs-lookup"><span data-stu-id="d662e-105">The .winmd file can then be consumed by JavaScript and C++ programs, in addition to managed language programs.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d662e-106">語法</span><span class="sxs-lookup"><span data-stu-id="d662e-106">Syntax</span></span>  
  
```console  
-target:winmdobj  
```  
  
## <a name="remarks"></a><span data-ttu-id="d662e-107">備註</span><span class="sxs-lookup"><span data-stu-id="d662e-107">Remarks</span></span>  
 <span data-ttu-id="d662e-108">**winmdobj** 設定對編譯器發出訊號，表示需要中繼模組。</span><span class="sxs-lookup"><span data-stu-id="d662e-108">The **winmdobj** setting signals to the compiler that an intermediate module is required.</span></span> <span data-ttu-id="d662e-109">Visual Studio 將 C# 類別庫編譯為 .winmdobj 檔案，做為回應。</span><span class="sxs-lookup"><span data-stu-id="d662e-109">In response, Visual Studio compiles the C# class library as a .winmdobj file.</span></span> <span data-ttu-id="d662e-110">然後 .winmdobj 檔案可以透過 <xref:Microsoft.Build.Tasks.WinMDExp> 匯出工具產生 Windows 中繼資料 (.winmd) 檔案。</span><span class="sxs-lookup"><span data-stu-id="d662e-110">The .winmdobj file can then be fed through the <xref:Microsoft.Build.Tasks.WinMDExp> export tool to produce a Windows metadata (.winmd) file.</span></span> <span data-ttu-id="d662e-111">.winmd 檔案包含原始類別庫的程式碼，以及 JavaScript 或 C++ 和 Windows 執行階段所使用的 WinMD 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d662e-111">The .winmd file contains both the code from the original library and the WinMD metadata that is used by JavaScript or C++ and by the Windows Runtime.</span></span>  
  
 <span data-ttu-id="d662e-112">使用 **-target:winmdobj** 編譯器選項所編譯之檔案的輸出，其設計目的只作為 WimMDExp 匯出工具的輸入，並不能直接參考 .winmdobj 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="d662e-112">The output of a file that’s compiled by using the **-target:winmdobj** compiler option is designed to be used only as input for the WimMDExp export tool; the .winmdobj file itself isn’t referenced directly.</span></span>  
  
 <span data-ttu-id="d662e-113">除非您使用 [-out](./out-compiler-option.md) 選項指定輸出檔案名稱，否則輸出檔案名稱會採用第一個輸入檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="d662e-113">Unless you use the [-out](./out-compiler-option.md) option, the output file name takes the name of the first input file.</span></span> <span data-ttu-id="d662e-114">不需要 [Main](../../programming-guide/main-and-command-args/index.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="d662e-114">A [Main](../../programming-guide/main-and-command-args/index.md) method isn’t required.</span></span>  
  
 <span data-ttu-id="d662e-115">如果您在命令提示字元指定 -target:winmdobj 選項，下一個 **-out** 或 [-target:module](./target-module-compiler-option.md) 選項之前的所有檔案都是用來建立 Windows 程式。</span><span class="sxs-lookup"><span data-stu-id="d662e-115">If you specify the -target:winmdobj option at a command prompt, all files until the next **-out** or [-target:module](./target-module-compiler-option.md) option are used to create the Windows program.</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-ide-for-a-windows-store-app"></a><span data-ttu-id="d662e-116">若要在 Visual Studio IDE 中為 Windows 市集應用程式設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="d662e-116">To set this compiler option in the Visual Studio IDE for a Windows Store app</span></span>  
  
1. <span data-ttu-id="d662e-117">在方案總管\*\*\*\* 中，開啟專案的捷徑功能表，然後選擇 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d662e-117">In **Solution Explorer**, open the shortcut menu for your project, and then choose **Properties**.</span></span>  
  
2. <span data-ttu-id="d662e-118">選擇 [應用程式]\*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d662e-118">Choose the **Application** tab.</span></span>  
  
3. <span data-ttu-id="d662e-119">在 [輸出類型]\*\*\*\* 清單中，選擇 [WinMD 檔案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d662e-119">In the **Output type** list, choose **WinMD File**.</span></span>  
  
     <span data-ttu-id="d662e-120">**WinMD**檔案選項僅適用于 Windows 8. x Store 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="d662e-120">The **WinMD File** option is available only for Windows 8.x Store app templates.</span></span>  
  
 <span data-ttu-id="d662e-121">如需如何以程式設計方式設定這個編譯器選項的詳細資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。</span><span class="sxs-lookup"><span data-stu-id="d662e-121">For information about how to set this compiler option programmatically, see <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d662e-122">範例</span><span class="sxs-lookup"><span data-stu-id="d662e-122">Example</span></span>  
 <span data-ttu-id="d662e-123">下列命令會將 `filename.cs` 編譯到中繼 .winmdobj 檔案。</span><span class="sxs-lookup"><span data-stu-id="d662e-123">The following command compiles `filename.cs` into an intermediate .winmdobj file.</span></span>  
  
```console  
csc -target:winmdobj filename.cs  
```  
  
## <a name="see-also"></a><span data-ttu-id="d662e-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d662e-124">See also</span></span>

- [<span data-ttu-id="d662e-125">-目標 (c # 編譯器選項) </span><span class="sxs-lookup"><span data-stu-id="d662e-125">-target (C# Compiler Options)</span></span>](./target-compiler-option.md)
- [<span data-ttu-id="d662e-126">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="d662e-126">C# Compiler Options</span></span>](./index.md)

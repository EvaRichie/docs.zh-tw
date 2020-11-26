---
description: -filealign (C# 編譯器選項)
title: -filealign (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: 4b61217a3d6812ea3ab036f82d49bba05c20629e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173239"
---
# <a name="-filealign-c-compiler-options"></a><span data-ttu-id="74355-103">-filealign (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="74355-103">-filealign (C# Compiler Options)</span></span>

<span data-ttu-id="74355-104">**-filealign** 選項可讓您指定輸出檔案中的區段大小。</span><span class="sxs-lookup"><span data-stu-id="74355-104">The **-filealign** option lets you specify the size of sections in your output file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="74355-105">語法</span><span class="sxs-lookup"><span data-stu-id="74355-105">Syntax</span></span>  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a><span data-ttu-id="74355-106">引數</span><span class="sxs-lookup"><span data-stu-id="74355-106">Arguments</span></span>  

 `number`  
 <span data-ttu-id="74355-107">指定輸出檔案中區段大小的值。</span><span class="sxs-lookup"><span data-stu-id="74355-107">A value that specifies the size of sections in the output file.</span></span> <span data-ttu-id="74355-108">有效值為 512、1024、2048、4096 和 8192。</span><span class="sxs-lookup"><span data-stu-id="74355-108">Valid values are 512, 1024, 2048, 4096, and 8192.</span></span> <span data-ttu-id="74355-109">這些值是以位元組為單位。</span><span class="sxs-lookup"><span data-stu-id="74355-109">These values are in bytes.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="74355-110">備註</span><span class="sxs-lookup"><span data-stu-id="74355-110">Remarks</span></span>  

 <span data-ttu-id="74355-111">每個區段都會對齊界限，而這個界限是 **-filealign** 值的倍數。</span><span class="sxs-lookup"><span data-stu-id="74355-111">Each section will be aligned on a boundary that is a multiple of the **-filealign** value.</span></span> <span data-ttu-id="74355-112">沒有固定預設值。</span><span class="sxs-lookup"><span data-stu-id="74355-112">There is no fixed default.</span></span> <span data-ttu-id="74355-113">如果未指定 **-filealign**，通用語言執行平台會在編譯時期選取預設值。</span><span class="sxs-lookup"><span data-stu-id="74355-113">If **-filealign** is not specified, the common language runtime picks a default at compile time.</span></span>  
  
 <span data-ttu-id="74355-114">您可以藉由指定區段大小，來影響輸出檔案的大小。</span><span class="sxs-lookup"><span data-stu-id="74355-114">By specifying the section size, you affect the size of the output file.</span></span> <span data-ttu-id="74355-115">修改區段大小對執行於較小裝置上的程式而言可能很有用。</span><span class="sxs-lookup"><span data-stu-id="74355-115">Modifying section size may be useful for programs that will run on smaller devices.</span></span>  
  
 <span data-ttu-id="74355-116">請使用 [DUMPBIN](/cpp/build/reference/dumpbin-options) 來查看輸出檔案中區段的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="74355-116">Use [DUMPBIN](/cpp/build/reference/dumpbin-options) to see information about sections in your output file.</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="74355-117">在 Visual Studio 開發環境中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="74355-117">To set this compiler option in the Visual Studio development environment</span></span>  
  
1. <span data-ttu-id="74355-118">開啟專案的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="74355-118">Open the project's **Properties** page.</span></span>  
  
2. <span data-ttu-id="74355-119">按一下 [建置] 屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="74355-119">Click the **Build** property page.</span></span>  
  
3. <span data-ttu-id="74355-120">按一下 [進階]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="74355-120">Click the **Advanced** button.</span></span>  
  
4. <span data-ttu-id="74355-121">修改 [檔案對齊] 屬性。</span><span class="sxs-lookup"><span data-stu-id="74355-121">Modify the **File Alignment** property.</span></span>  
  
 <span data-ttu-id="74355-122">如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>。</span><span class="sxs-lookup"><span data-stu-id="74355-122">For information on how to set this compiler option programmatically, see <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="74355-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="74355-123">See also</span></span>

- [<span data-ttu-id="74355-124">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="74355-124">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="74355-125">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="74355-125">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

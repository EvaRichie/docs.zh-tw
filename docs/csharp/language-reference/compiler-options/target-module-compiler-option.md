---
description: -target:module (C# 編譯器選項)
title: -target:module (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /target:module
helpviewer_keywords:
- -target compiler options [C#], /target:module
- target compiler options [C#], /target:module
- /target compiler options [C#], /target:module
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
ms.openlocfilehash: d8691e5e4477dbbe989344469b44382d5e0e7c8b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193604"
---
# <a name="-targetmodule-c-compiler-options"></a><span data-ttu-id="31cd4-103">-target:module (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="31cd4-103">-target:module (C# Compiler Options)</span></span>

<span data-ttu-id="31cd4-104">這個選項可讓編譯器不要產生組件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="31cd4-104">This option causes the compiler to not generate an assembly manifest.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="31cd4-105">語法</span><span class="sxs-lookup"><span data-stu-id="31cd4-105">Syntax</span></span>  
  
```console  
-target:module  
```  
  
## <a name="remarks"></a><span data-ttu-id="31cd4-106">備註</span><span class="sxs-lookup"><span data-stu-id="31cd4-106">Remarks</span></span>  

 <span data-ttu-id="31cd4-107">根據預設，使用這個選項編譯時，所建立的輸出檔副檔名會是 .netmodule。</span><span class="sxs-lookup"><span data-stu-id="31cd4-107">By default, the output file created by compiling with this option will have an extension of .netmodule.</span></span>  
  
 <span data-ttu-id="31cd4-108">.NET 執行時間無法載入沒有組件資訊清單的檔案。</span><span class="sxs-lookup"><span data-stu-id="31cd4-108">A file that does not have an assembly manifest cannot be loaded by the .NET runtime.</span></span> <span data-ttu-id="31cd4-109">不過，這類檔案可以透過 [-addmodule](./addmodule-compiler-option.md) 併入組件的組件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="31cd4-109">However, such a file can be incorporated into the assembly manifest of an assembly by means of [-addmodule](./addmodule-compiler-option.md).</span></span>  
  
 <span data-ttu-id="31cd4-110">如果在單一編譯中建立多個模組，則編譯中的其他模組可以使用某個模組中的 [internal](../keywords/internal.md) 類型。</span><span class="sxs-lookup"><span data-stu-id="31cd4-110">If more than one module is created in a single compilation, [internal](../keywords/internal.md) types in one module will be available to other modules in the compilation.</span></span> <span data-ttu-id="31cd4-111">某個模組中的程式碼參考另一個模組中的 `internal` 類型時，必須透過 **-addmodule** 將這兩個模組併入組件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="31cd4-111">When code in one module references `internal` types in another module, then both modules must be incorporated into an assembly manifest, by means of **-addmodule**.</span></span>  
  
 <span data-ttu-id="31cd4-112">Visual Studio 開發環境不支援建立模組。</span><span class="sxs-lookup"><span data-stu-id="31cd4-112">Creating a module is not supported in the Visual Studio development environment.</span></span>  
  
 <span data-ttu-id="31cd4-113">如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。</span><span class="sxs-lookup"><span data-stu-id="31cd4-113">For information on how to set this compiler option programmatically, see <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="31cd4-114">範例</span><span class="sxs-lookup"><span data-stu-id="31cd4-114">Example</span></span>  

 <span data-ttu-id="31cd4-115">建立 `in.netmodule` 以編譯 `in.cs`：</span><span class="sxs-lookup"><span data-stu-id="31cd4-115">Compile `in.cs`, creating `in.netmodule`:</span></span>  
  
```console  
csc -target:module in.cs  
```  
  
## <a name="see-also"></a><span data-ttu-id="31cd4-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="31cd4-116">See also</span></span>

- [<span data-ttu-id="31cd4-117">-目標 (c # 編譯器選項) </span><span class="sxs-lookup"><span data-stu-id="31cd4-117">-target (C# Compiler Options)</span></span>](./target-compiler-option.md)
- [<span data-ttu-id="31cd4-118">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="31cd4-118">C# Compiler Options</span></span>](./index.md)

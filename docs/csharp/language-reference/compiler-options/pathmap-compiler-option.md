---
description: -pathmap (C# 編譯器選項)
title: -pathmap (C# 編譯器選項)
ms.date: 05/16/2018
f1_keywords:
- /pathmap
helpviewer_keywords:
- -pathmap compiler option [C#]
- pathmap compiler option [C#]
- /pathmap compiler option [C#]
ms.openlocfilehash: 707a37c6946cfcaf429552f0aeece6b87f3ad71d
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "89125003"
---
# <a name="-pathmap-c-compiler-options"></a><span data-ttu-id="08de9-103">-pathmap (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="08de9-103">-pathmap (C# Compiler Options)</span></span>

<span data-ttu-id="08de9-104">**-pathmap** 編譯器選項會指定如何將實體路徑對應到編譯器所輸出的來源路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="08de9-104">The **-pathmap** compiler option specifies how to map physical paths to source path names output by the compiler.</span></span>

## <a name="syntax"></a><span data-ttu-id="08de9-105">語法</span><span class="sxs-lookup"><span data-stu-id="08de9-105">Syntax</span></span>

```console
-pathmap:path1=sourcePath1,path2=sourcePath2
```

## <a name="arguments"></a><span data-ttu-id="08de9-106">引數</span><span class="sxs-lookup"><span data-stu-id="08de9-106">Arguments</span></span>

 <span data-ttu-id="08de9-107">`path1` 目前環境中原始程式檔的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="08de9-107">`path1` The full path to the source files in the current environment</span></span>

 <span data-ttu-id="08de9-108">`sourcePath1` 任何輸出檔案中替代 `path1` 的來源路徑。</span><span class="sxs-lookup"><span data-stu-id="08de9-108">`sourcePath1` The source path substituted for `path1` in any output files.</span></span>

<span data-ttu-id="08de9-109">若要指定多個對應的來源路徑，請以逗號隔開每個來源路徑。</span><span class="sxs-lookup"><span data-stu-id="08de9-109">To specify multiple mapped source paths, separate each with a comma.</span></span>

## <a name="remarks"></a><span data-ttu-id="08de9-110">備註</span><span class="sxs-lookup"><span data-stu-id="08de9-110">Remarks</span></span>

<span data-ttu-id="08de9-111">編譯器會基於下列因素，將來源路徑寫入其輸出中：</span><span class="sxs-lookup"><span data-stu-id="08de9-111">The compiler writes the source path into its output for the following reasons:</span></span>

1. <span data-ttu-id="08de9-112">將 <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> 套用到選擇性參數時，會針對引數替代來源路徑。</span><span class="sxs-lookup"><span data-stu-id="08de9-112">The source path is substituted for an argument when the <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> is applied to an optional parameter.</span></span>
1. <span data-ttu-id="08de9-113">來源路徑內嵌於 PDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="08de9-113">The source path is embedded in a PDB file.</span></span>
1. <span data-ttu-id="08de9-114">PDB 檔案的路徑內嵌於 PE (可攜式執行檔) 檔案。</span><span class="sxs-lookup"><span data-stu-id="08de9-114">The path of the PDB file is embedded into a PE (portable executable) file.</span></span>

<span data-ttu-id="08de9-115">此選項會將編譯器執行所在電腦上的每個實體路徑對應到應寫入輸出檔案的對應路徑。</span><span class="sxs-lookup"><span data-stu-id="08de9-115">This option maps each physical path on the machine where the compiler runs to a corresponding path that should be written in the output files.</span></span>

## <a name="example"></a><span data-ttu-id="08de9-116">範例</span><span class="sxs-lookup"><span data-stu-id="08de9-116">Example</span></span>

<span data-ttu-id="08de9-117">在目錄 **C:\\work\\tests** 中編譯 `t.cs`，並將該目錄對應到輸出中的 **\publish**：</span><span class="sxs-lookup"><span data-stu-id="08de9-117">Compile `t.cs` in the directory **C:\\work\\tests** and map that directory to **\publish** in the output:</span></span>

```console
csc -pathmap:C:\work\tests=\publish t.cs
```

## <a name="see-also"></a><span data-ttu-id="08de9-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="08de9-118">See also</span></span>

- [<span data-ttu-id="08de9-119">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="08de9-119">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="08de9-120">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="08de9-120">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

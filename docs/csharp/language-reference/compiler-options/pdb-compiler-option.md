---
description: -pdb (C# 編譯器選項)
title: -pdb (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /pdb
helpviewer_keywords:
- -pdb compiler option [C#]
- pdb compiler option [C#]
- /pdb compiler option [C#]
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
ms.openlocfilehash: 0dcafd0fd260488922c74a2330b312e80467e779
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89124912"
---
# <a name="-pdb-c-compiler-options"></a><span data-ttu-id="af07e-103">-pdb (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="af07e-103">-pdb (C# Compiler Options)</span></span>
<span data-ttu-id="af07e-104">**-pdb** 編譯器選項指定偵錯符號檔的名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="af07e-104">The **-pdb** compiler option specifies the name and location of the debug symbols file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="af07e-105">語法</span><span class="sxs-lookup"><span data-stu-id="af07e-105">Syntax</span></span>  
  
```console  
-pdb:filename  
```  
  
## <a name="arguments"></a><span data-ttu-id="af07e-106">引數</span><span class="sxs-lookup"><span data-stu-id="af07e-106">Arguments</span></span>  
 `filename`  
 <span data-ttu-id="af07e-107">偵錯符號檔案的名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="af07e-107">The name and location of the debug symbols file.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="af07e-108">備註</span><span class="sxs-lookup"><span data-stu-id="af07e-108">Remarks</span></span>  
 <span data-ttu-id="af07e-109">當您指定 [-debug (C# 編譯器選項)](./debug-compiler-option.md) 時，編譯器會在相同的目錄中建立 .pdb 檔案，而編譯器會在此目錄中建立檔案名稱與輸出檔案名稱相同的輸出檔案 (.exe 或 .dll)。</span><span class="sxs-lookup"><span data-stu-id="af07e-109">When you specify [-debug (C# Compiler Options)](./debug-compiler-option.md), the compiler will create a .pdb file in the same directory where the compiler will create the output file (.exe or .dll) with a file name that is the same as the name of the output file.</span></span>  
  
 <span data-ttu-id="af07e-110">**-pdb** 可讓您指定 .pdb 檔案的非預設檔案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="af07e-110">**-pdb** allows you to specify a non-default file name and location for the .pdb file.</span></span>  
  
 <span data-ttu-id="af07e-111">無法在 Visual Studio 開發環境中設定此編譯器選項，也無法以程式設計方式進行變更。</span><span class="sxs-lookup"><span data-stu-id="af07e-111">This compiler option cannot be set in the Visual Studio development environment, nor can it be changed programmatically.</span></span>  
  
## <a name="example"></a><span data-ttu-id="af07e-112">範例</span><span class="sxs-lookup"><span data-stu-id="af07e-112">Example</span></span>  
 <span data-ttu-id="af07e-113">編譯 `t.cs` 並建立稱為 tt.pdb 的 .pdb 檔案：</span><span class="sxs-lookup"><span data-stu-id="af07e-113">Compile `t.cs` and create a .pdb file called tt.pdb:</span></span>  
  
```console  
csc -debug -pdb:tt t.cs  
```  
  
## <a name="see-also"></a><span data-ttu-id="af07e-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af07e-114">See also</span></span>

- [<span data-ttu-id="af07e-115">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="af07e-115">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="af07e-116">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="af07e-116">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)

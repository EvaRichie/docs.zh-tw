---
title: -out
ms.date: 07/20/2015
helpviewer_keywords:
- /out compiler option [Visual Basic]
- -out compiler option [Visual Basic]
- out compiler option [Visual Basic]
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
ms.openlocfilehash: 75f3ee7f24112f911803732ccb8d39eeafa95e3d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400509"
---
# <a name="-out-visual-basic"></a><span data-ttu-id="cb7f9-102">-out （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="cb7f9-102">-out (Visual Basic)</span></span>
<span data-ttu-id="cb7f9-103">指定輸出檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-103">Specifies the name of the output file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="cb7f9-104">語法</span><span class="sxs-lookup"><span data-stu-id="cb7f9-104">Syntax</span></span>  
  
```console  
-out:filename  
```  
  
## <a name="arguments"></a><span data-ttu-id="cb7f9-105">引數</span><span class="sxs-lookup"><span data-stu-id="cb7f9-105">Arguments</span></span>  
  
|<span data-ttu-id="cb7f9-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="cb7f9-106">Term</span></span>|<span data-ttu-id="cb7f9-107">定義</span><span class="sxs-lookup"><span data-stu-id="cb7f9-107">Definition</span></span>|  
|---|---|  
|`filename`|<span data-ttu-id="cb7f9-108">必要。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-108">Required.</span></span> <span data-ttu-id="cb7f9-109">編譯器所建立之輸出檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-109">The name of the output file the compiler creates.</span></span> <span data-ttu-id="cb7f9-110">如果檔案名包含空格，請將名稱括在引號（""）中。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-110">If the file name contains a space, enclose the name in quotation marks (" ").</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="cb7f9-111">備註</span><span class="sxs-lookup"><span data-stu-id="cb7f9-111">Remarks</span></span>  
 <span data-ttu-id="cb7f9-112">指定要建立之檔案的完整名稱和副檔名。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-112">Specify the full name and extension of the file to create.</span></span> <span data-ttu-id="cb7f9-113">如果不這麼做，.exe 檔案會從包含程式的原始程式碼檔案取得其名稱 `Sub Main` ，而 .dll 檔案會從第一個原始程式碼檔案取得其名稱。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-113">If you do not, the .exe file takes its name from the source-code file containing the `Sub Main` procedure, and the .dll file takes its name from the first source-code file.</span></span>  
  
 <span data-ttu-id="cb7f9-114">如果您指定不含 .exe 或 .dll 副檔名的檔案名，編譯器會自動為您加入延伸模組，視針對編譯器選項所指定的值而定 `-target` 。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-114">If you specify a file name without an .exe or .dll extension, the compiler automatically adds the extension for you, depending on the value specified for the `-target` compiler option.</span></span>  
  
|<span data-ttu-id="cb7f9-115">在 Visual Studio 的整合式開發環境中設定</span><span class="sxs-lookup"><span data-stu-id="cb7f9-115">To set -out in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="cb7f9-116">1. 在**方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-116">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="cb7f9-117">按一下 [專案]\*\*\*\* 功能表上的 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-117">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="cb7f9-118">2. 按一下 [**應用程式**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-118">2.  Click the **Application** tab.</span></span><br /><span data-ttu-id="cb7f9-119">3. 修改 [**元件名稱**] 方塊中的值。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-119">3.  Modify the value in the **Assembly Name** box.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="cb7f9-120">範例</span><span class="sxs-lookup"><span data-stu-id="cb7f9-120">Example</span></span>  
 <span data-ttu-id="cb7f9-121">下列程式碼會編譯 `T2.vb` 並建立輸出檔 `T2.exe` 。</span><span class="sxs-lookup"><span data-stu-id="cb7f9-121">The following code compiles `T2.vb` and creates output file `T2.exe`.</span></span>  
  
```console
vbc t2.vb -out:t3.exe  
```  
  
## <a name="see-also"></a><span data-ttu-id="cb7f9-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cb7f9-122">See also</span></span>

- [<span data-ttu-id="cb7f9-123">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="cb7f9-123">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="cb7f9-124">-target （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="cb7f9-124">-target (Visual Basic)</span></span>](target.md)
- [<span data-ttu-id="cb7f9-125">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="cb7f9-125">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)

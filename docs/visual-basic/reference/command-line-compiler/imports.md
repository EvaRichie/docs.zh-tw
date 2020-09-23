---
title: -imports
ms.date: 03/10/2018
helpviewer_keywords:
- /imports compiler option [Visual Basic]
- imports compiler option [Visual Basic]
- -imports compiler option [Visual Basic]
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
ms.openlocfilehash: 69781dff1474e42ae5f735fdefd694c6447636b5
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91085252"
---
# <a name="-imports-visual-basic"></a><span data-ttu-id="3938d-102">-匯入 (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="3938d-102">-imports (Visual Basic)</span></span>

<span data-ttu-id="3938d-103">從指定的元件匯入命名空間。</span><span class="sxs-lookup"><span data-stu-id="3938d-103">Imports namespaces from a specified assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3938d-104">語法</span><span class="sxs-lookup"><span data-stu-id="3938d-104">Syntax</span></span>  
  
```console  
-imports:namespaceList  
```  
  
## <a name="arguments"></a><span data-ttu-id="3938d-105">引數</span><span class="sxs-lookup"><span data-stu-id="3938d-105">Arguments</span></span>  
  
|<span data-ttu-id="3938d-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="3938d-106">Term</span></span>|<span data-ttu-id="3938d-107">定義</span><span class="sxs-lookup"><span data-stu-id="3938d-107">Definition</span></span>|  
|---|---|  
|`namespaceList`|<span data-ttu-id="3938d-108">必要。</span><span class="sxs-lookup"><span data-stu-id="3938d-108">Required.</span></span> <span data-ttu-id="3938d-109">要匯入的命名空間清單（以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="3938d-109">Comma-delimited list of namespaces to be imported.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3938d-110">備註</span><span class="sxs-lookup"><span data-stu-id="3938d-110">Remarks</span></span>  

 <span data-ttu-id="3938d-111">選項會匯 `-imports` 入目前的原始程式檔集合或任何參考元件中定義的任何命名空間。</span><span class="sxs-lookup"><span data-stu-id="3938d-111">The `-imports` option imports any namespace defined within the current set of source files or from any referenced assembly.</span></span>  
  
 <span data-ttu-id="3938d-112">使用指定的命名空間中的成員， `-imports` 可供編譯中的所有原始程式碼檔案使用。</span><span class="sxs-lookup"><span data-stu-id="3938d-112">The members in a namespace specified with `-imports` are available to all source-code files in the compilation.</span></span> <span data-ttu-id="3938d-113">使用 [Imports 語句 ( .Net 命名空間和類型) ](../../language-reference/statements/imports-statement-net-namespace-and-type.md) ，以在單一原始程式碼檔中使用命名空間。</span><span class="sxs-lookup"><span data-stu-id="3938d-113">Use the [Imports Statement (.NET Namespace and Type)](../../language-reference/statements/imports-statement-net-namespace-and-type.md) to use a namespace in a single source-code file.</span></span>  
  
|<span data-ttu-id="3938d-114">在 Visual Studio 整合式開發環境中設定-匯入</span><span class="sxs-lookup"><span data-stu-id="3938d-114">To set -imports in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="3938d-115">1. 在 **方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="3938d-115">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="3938d-116">按一下 [專案] 功能表上的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="3938d-116">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="3938d-117">2. 按一下 [ **參考** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3938d-117">2.  Click the **References** tab.</span></span><br /><span data-ttu-id="3938d-118">3. 在 [ **新增使用者匯入** ] 按鈕旁邊的方塊中輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="3938d-118">3.  Enter the namespace name in the box beside the **Add User Import** button.</span></span><br /><span data-ttu-id="3938d-119">4. 按一下 [ **新增使用者匯入** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3938d-119">4.  Click the **Add User Import** button.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="3938d-120">範例</span><span class="sxs-lookup"><span data-stu-id="3938d-120">Example</span></span>  

 <span data-ttu-id="3938d-121">下列程式碼會在 `-imports:system.globalization` 指定時進行編譯。</span><span class="sxs-lookup"><span data-stu-id="3938d-121">The following code compiles when `-imports:system.globalization` is specified.</span></span> <span data-ttu-id="3938d-122">如果沒有它，成功的編譯就需要將 `Imports System.Globalization` 語句包含在原始程式碼檔的開頭，或是將屬性完整限定為 `System.Globalization.CultureInfo.CurrentCulture.Name` 。</span><span class="sxs-lookup"><span data-stu-id="3938d-122">Without it, successful compilation requires either that an `Imports System.Globalization` statement be included at the beginning of the source code file, or that the property be fully qualified as `System.Globalization.CultureInfo.CurrentCulture.Name`.</span></span>

```vb
Module Example
   Public Sub Main()
      Console.WriteLine($"The current culture is {CultureInfo.CurrentCulture.Name}")
   End Sub
End Module
```

## <a name="see-also"></a><span data-ttu-id="3938d-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3938d-123">See also</span></span>

- [<span data-ttu-id="3938d-124">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="3938d-124">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="3938d-125">References 與 Imports 陳述式</span><span class="sxs-lookup"><span data-stu-id="3938d-125">References and the Imports Statement</span></span>](../../programming-guide/program-structure/references-and-the-imports-statement.md)
- [<span data-ttu-id="3938d-126">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="3938d-126">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)

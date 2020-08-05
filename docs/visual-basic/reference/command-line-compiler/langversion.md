---
title: -langversion
ms.date: 03/10/2018
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
ms.openlocfilehash: 286dd8bd9949b584cec38642f44ba9ac5e924732
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557173"
---
# <a name="-langversion-visual-basic"></a><span data-ttu-id="8a442-102">-langversion (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="8a442-102">-langversion (Visual Basic)</span></span>
<span data-ttu-id="8a442-103">使編譯器只接受指定的 Visual Basic 語言版本中所包含的語法。</span><span class="sxs-lookup"><span data-stu-id="8a442-103">Causes the compiler to accept only syntax that is included in the specified Visual Basic language version.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8a442-104">語法</span><span class="sxs-lookup"><span data-stu-id="8a442-104">Syntax</span></span>  
  
```console  
-langversion:version  
```  
  
## <a name="arguments"></a><span data-ttu-id="8a442-105">引數</span><span class="sxs-lookup"><span data-stu-id="8a442-105">Arguments</span></span>  
 `version`  
 <span data-ttu-id="8a442-106">必要。</span><span class="sxs-lookup"><span data-stu-id="8a442-106">Required.</span></span> <span data-ttu-id="8a442-107">要在編譯期間使用的語言版本。</span><span class="sxs-lookup"><span data-stu-id="8a442-107">The language version to be used during the compilation.</span></span> <span data-ttu-id="8a442-108">接受的值為 `9` 、 `10` 、 `11` 、、、、、 `12` `14` `15` `15.3` `15.5` `default` 和 `latest` 。</span><span class="sxs-lookup"><span data-stu-id="8a442-108">Accepted values are `9`, `10`, `11`, `12`, `14`, `15`, `15.3`, `15.5`, `default` and `latest`.</span></span>

 <span data-ttu-id="8a442-109">您也可以使用將任何整數指定 `.0` 為次要版本，例如 `11.0` 。</span><span class="sxs-lookup"><span data-stu-id="8a442-109">Any of the whole numbers may also be specified using `.0` as the minor version, for example, `11.0`.</span></span>

 <span data-ttu-id="8a442-110">您可以 `-langversion:?` 在命令列上指定，以查看所有可能值的清單。</span><span class="sxs-lookup"><span data-stu-id="8a442-110">You can see the list of all possible values by specifying `-langversion:?` on the command line.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8a442-111">備註</span><span class="sxs-lookup"><span data-stu-id="8a442-111">Remarks</span></span>  
 <span data-ttu-id="8a442-112">`-langversion`選項會指定編譯器接受的語法。</span><span class="sxs-lookup"><span data-stu-id="8a442-112">The `-langversion` option specifies what syntax the compiler accepts.</span></span> <span data-ttu-id="8a442-113">例如，如果您指定語言版本是9.0，則編譯器會針對只有10.0 版和更新版本中有效的語法產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a442-113">For example, if you specify that the language version is 9.0, the compiler generates errors for syntax that is valid only in version 10.0 and later.</span></span>  
  
 <span data-ttu-id="8a442-114">當您開發以不同 .NET Framework 版本為目標的應用程式時，可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="8a442-114">You can use this option when you develop applications that target different versions of the .NET Framework.</span></span> <span data-ttu-id="8a442-115">例如，如果您的目標是 .NET Framework 3.5，您可以使用此選項來確保不會使用語言版本10.0 中的語法。</span><span class="sxs-lookup"><span data-stu-id="8a442-115">For example, if you are targeting .NET Framework 3.5, you could use this option to ensure that you do not use syntax from language version 10.0.</span></span>  
  
 <span data-ttu-id="8a442-116">您只能 `-langversion` 使用命令列來直接設定。</span><span class="sxs-lookup"><span data-stu-id="8a442-116">You can set `-langversion` directly only by using the command line.</span></span> <span data-ttu-id="8a442-117">如需詳細資訊，請參閱[以特定的 .NET Framework 版本為目標](/visualstudio/ide/visual-studio-multi-targeting-overview)。</span><span class="sxs-lookup"><span data-stu-id="8a442-117">For more information, see [Targeting a Specific .NET Framework Version](/visualstudio/ide/visual-studio-multi-targeting-overview).</span></span>  
  
## <a name="example"></a><span data-ttu-id="8a442-118">範例</span><span class="sxs-lookup"><span data-stu-id="8a442-118">Example</span></span>  
 <span data-ttu-id="8a442-119">下列程式碼會 `sample.vb` 針對 Visual Basic 9.0 進行編譯。</span><span class="sxs-lookup"><span data-stu-id="8a442-119">The following code compiles `sample.vb` for Visual Basic 9.0.</span></span>  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="8a442-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a442-120">See also</span></span>

- [<span data-ttu-id="8a442-121">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="8a442-121">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="8a442-122">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="8a442-122">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)

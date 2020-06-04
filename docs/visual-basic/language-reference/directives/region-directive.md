---
title: '#Region 指示詞'
ms.date: 07/20/2015
f1_keywords:
- vb.Region
- vb.#Region
helpviewer_keywords:
- Visual Basic compiler, compiler directives
- '#region directive'
- region directive (#region)
- '#Region keyword [Visual Basic]'
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
ms.openlocfilehash: cd53a6079c1564a8c73a0a1a6273fc166d18d3e6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409931"
---
# <a name="region-directive"></a><span data-ttu-id="acbbb-102">#Region 指示詞</span><span class="sxs-lookup"><span data-stu-id="acbbb-102">#Region Directive</span></span>

<span data-ttu-id="acbbb-103">摺疊並隱藏 Visual Basic 檔案中的程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="acbbb-103">Collapses and hides sections of code in Visual Basic files.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="acbbb-104">語法</span><span class="sxs-lookup"><span data-stu-id="acbbb-104">Syntax</span></span>  

```vb
#Region "identifier_string"  
#End Region  
```  
  
## <a name="parts"></a><span data-ttu-id="acbbb-105">組件</span><span class="sxs-lookup"><span data-stu-id="acbbb-105">Parts</span></span>  
  
|<span data-ttu-id="acbbb-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="acbbb-106">Term</span></span>|<span data-ttu-id="acbbb-107">定義</span><span class="sxs-lookup"><span data-stu-id="acbbb-107">Definition</span></span>|  
|---|---|  
|`identifier_string`|<span data-ttu-id="acbbb-108">必要。</span><span class="sxs-lookup"><span data-stu-id="acbbb-108">Required.</span></span> <span data-ttu-id="acbbb-109">做為摺疊區域標題的字串。</span><span class="sxs-lookup"><span data-stu-id="acbbb-109">String that acts as the title of a region when it is collapsed.</span></span> <span data-ttu-id="acbbb-110">區域預設會摺疊。</span><span class="sxs-lookup"><span data-stu-id="acbbb-110">Regions are collapsed by default.</span></span>|  
|`#End Region`|<span data-ttu-id="acbbb-111">終止 `#Region` 區塊。</span><span class="sxs-lookup"><span data-stu-id="acbbb-111">Terminates the `#Region` block.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="acbbb-112">備註</span><span class="sxs-lookup"><span data-stu-id="acbbb-112">Remarks</span></span>  

 <span data-ttu-id="acbbb-113">使用 `#Region` 指示詞來指定程式碼區段，以在使用 Visual Studio 程式碼編輯器的大綱功能時展開或摺疊。</span><span class="sxs-lookup"><span data-stu-id="acbbb-113">Use the `#Region` directive to specify a block of code to expand or collapse when using the outlining feature of the Visual Studio Code Editor.</span></span> <span data-ttu-id="acbbb-114">您可以將區域放在其他區域中，或加以*嵌套*，將類似的區域群組在一起。</span><span class="sxs-lookup"><span data-stu-id="acbbb-114">You can place, or *nest*, regions within other regions to group similar regions together.</span></span>  
  
## <a name="example"></a><span data-ttu-id="acbbb-115">範例</span><span class="sxs-lookup"><span data-stu-id="acbbb-115">Example</span></span>  

 <span data-ttu-id="acbbb-116">此範例使用 `#Region` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="acbbb-116">This example uses the `#Region` directive.</span></span>  
  
 [!code-vb[VbVbalrConditionalComp#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="acbbb-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="acbbb-117">See also</span></span>

- [<span data-ttu-id="acbbb-118">#If .。。Then ... #Else 指示詞</span><span class="sxs-lookup"><span data-stu-id="acbbb-118">#If...Then...#Else Directives</span></span>](if-then-else-directives.md)
- [<span data-ttu-id="acbbb-119">大綱</span><span class="sxs-lookup"><span data-stu-id="acbbb-119">Outlining</span></span>](/visualstudio/ide/outlining)
- [<span data-ttu-id="acbbb-120">作法：摺疊及隱藏程式碼區段</span><span class="sxs-lookup"><span data-stu-id="acbbb-120">How to: Collapse and Hide Sections of Code</span></span>](../../programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)

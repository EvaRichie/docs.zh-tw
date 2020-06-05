---
title: 函式評估已停用，因為先前的函式評估逾時
ms.date: 07/20/2015
f1_keywords:
- bc30957
- vbc30957
helpviewer_keywords:
- BC30957
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
ms.openlocfilehash: 7b0113e9c1018772da6dc180f7fc5beb0e922917
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402949"
---
# <a name="function-evaluation-is-disabled-because-a-previous-function-evaluation-timed-out"></a><span data-ttu-id="671cc-102">函式評估已停用，因為先前的函式評估逾時</span><span class="sxs-lookup"><span data-stu-id="671cc-102">Function evaluation is disabled because a previous function evaluation timed out</span></span>
<span data-ttu-id="671cc-103">函數評估已停用，因為先前的函數評估已超時。若要重新啟用函數評估，請再次執行或重新開機偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="671cc-103">Function evaluation is disabled because a previous function evaluation timed out. To re-enable function evaluation, step again or restart debugging.</span></span>  
  
 <span data-ttu-id="671cc-104">在 Visual Studio 偵錯工具中，運算式會指定程序呼叫，但另一個評估會超時。</span><span class="sxs-lookup"><span data-stu-id="671cc-104">In the Visual Studio debugger, an expression specifies a procedure call, but another evaluation has timed out.</span></span>  
  
 <span data-ttu-id="671cc-105">程序呼叫超時的可能原因包括無限迴圈或無止盡*迴圈*。</span><span class="sxs-lookup"><span data-stu-id="671cc-105">Possible causes for a procedure call to time out include an infinite loop or *endless loop*.</span></span> <span data-ttu-id="671cc-106">如需詳細資訊，請參閱[For .。。下一個語句](../statements/for-next-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="671cc-106">For more information, see [For...Next Statement](../statements/for-next-statement.md).</span></span>  
  
 <span data-ttu-id="671cc-107">無限迴圈的特殊情況是*遞迴*。</span><span class="sxs-lookup"><span data-stu-id="671cc-107">A special case of an infinite loop is *recursion*.</span></span> <span data-ttu-id="671cc-108">如需詳細資訊，請參閱[遞迴程式](../../programming-guide/language-features/procedures/recursive-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="671cc-108">For more information, see [Recursive Procedures](../../programming-guide/language-features/procedures/recursive-procedures.md).</span></span>  
  
 <span data-ttu-id="671cc-109">**錯誤識別碼：** BC30957</span><span class="sxs-lookup"><span data-stu-id="671cc-109">**Error ID:** BC30957</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="671cc-110">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="671cc-110">To correct this error</span></span>  
  
1. <span data-ttu-id="671cc-111">可能的話，請判斷先前的函式評估為何，以及造成它超時的原因。否則，您可能會再次遇到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="671cc-111">If possible, determine what the previous function evaluation was and what caused it to time out. Otherwise, you might encounter this error again.</span></span>  
  
2. <span data-ttu-id="671cc-112">請重新執行偵錯工具，或終止並重新啟動偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="671cc-112">Either step the debugger again, or terminate and restart debugging.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="671cc-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="671cc-113">See also</span></span>

- [<span data-ttu-id="671cc-114">Visual Studio 偵錯</span><span class="sxs-lookup"><span data-stu-id="671cc-114">Debugging in Visual Studio</span></span>](/visualstudio/debugger/debugger-feature-tour)
- [<span data-ttu-id="671cc-115">使用偵錯工具巡覽程式碼</span><span class="sxs-lookup"><span data-stu-id="671cc-115">Navigating through Code with the Debugger</span></span>](/visualstudio/debugger/navigating-through-code-with-the-debugger)

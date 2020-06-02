---
title: 作法：從工作傳回值
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to return a value
ms.assetid: c4bc0f44-eba2-4e96-9e03-1cc787461e61
ms.openlocfilehash: 144d004d697b84a011cedafc7d07b679ef8852c3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288143"
---
# <a name="how-to-return-a-value-from-a-task"></a><span data-ttu-id="88bb7-102">作法：從工作傳回值</span><span class="sxs-lookup"><span data-stu-id="88bb7-102">How to: Return a Value from a Task</span></span>
<span data-ttu-id="88bb7-103">這個範例示範如何使用 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 類型從 <xref:System.Threading.Tasks.Task%601.Result%2A> 屬性傳回值。</span><span class="sxs-lookup"><span data-stu-id="88bb7-103">This example shows how to use the <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> type to return a value from the <xref:System.Threading.Tasks.Task%601.Result%2A> property.</span></span> <span data-ttu-id="88bb7-104">它需要有 C:\Users\Public\Pictures\Sample Pictures\ 目錄存在，且其中包含檔案。</span><span class="sxs-lookup"><span data-stu-id="88bb7-104">It requires that the C:\Users\Public\Pictures\Sample Pictures\ directory exists, and that it contains files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="88bb7-105">範例</span><span class="sxs-lookup"><span data-stu-id="88bb7-105">Example</span></span>  
 [!code-csharp[TPL#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/returnavalue10.cs#10)]
 [!code-vb[TPL#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/10_returnavalue.vb#10)]  
  
 <span data-ttu-id="88bb7-106"><xref:System.Threading.Tasks.Task%601.Result%2A> 屬性會封鎖呼叫執行緒，直到工作完成。</span><span class="sxs-lookup"><span data-stu-id="88bb7-106">The <xref:System.Threading.Tasks.Task%601.Result%2A> property blocks the calling thread until the task finishes.</span></span>  
  
 <span data-ttu-id="88bb7-107">若要查看如何傳遞一個 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 的結果到接續工作，請參閱[使用接續工作鏈結工作](chaining-tasks-by-using-continuation-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="88bb7-107">To see how to pass the result of one <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> to a continuation task, see [Chaining Tasks by Using Continuation Tasks](chaining-tasks-by-using-continuation-tasks.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="88bb7-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="88bb7-108">See also</span></span>

- [<span data-ttu-id="88bb7-109">以工作為基礎的非同步程式設計</span><span class="sxs-lookup"><span data-stu-id="88bb7-109">Task-based Asynchronous Programming</span></span>](task-based-asynchronous-programming.md)
- [<span data-ttu-id="88bb7-110">PLINQ 和 TPL 中的 Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="88bb7-110">Lambda Expressions in PLINQ and TPL</span></span>](lambda-expressions-in-plinq-and-tpl.md)

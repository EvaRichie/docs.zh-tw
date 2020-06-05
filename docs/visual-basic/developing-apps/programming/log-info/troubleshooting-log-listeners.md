---
title: 疑難排解：記錄檔接聽程式
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: 8d2d8294d9e9bb42d72fe4f6c37bf846bd644907
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398314"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a><span data-ttu-id="7d322-102">疑難排解：記錄檔接聽程式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7d322-102">Troubleshooting: Log Listeners (Visual Basic)</span></span>

<span data-ttu-id="7d322-103">您可以使用 `My.Application.Log` 和 `My.Log` 物件來記錄應用程式中發生之事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7d322-103">You can use the `My.Application.Log` and `My.Log` objects to log information about events that occur in your application.</span></span>  
  
 <span data-ttu-id="7d322-104">若要判斷哪些記錄檔接聽程式接收這些訊息，請參閱[逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)。</span><span class="sxs-lookup"><span data-stu-id="7d322-104">To determine which log listeners receive those messages, see [Walkthrough: Determining Where My.Application.Log Writes Information](walkthrough-determining-where-my-application-log-writes-information.md).</span></span>  
  
 <span data-ttu-id="7d322-105">`Log` 物件可以使用記錄檔篩選來限制記錄的資訊數量。</span><span class="sxs-lookup"><span data-stu-id="7d322-105">The `Log` object can use log filtering to limit the amount of information that it logs.</span></span> <span data-ttu-id="7d322-106">如果篩選條件設定錯誤，記錄檔可能包含錯誤的資訊。</span><span class="sxs-lookup"><span data-stu-id="7d322-106">If the filters are misconfigured, the logs might contain the wrong information.</span></span> <span data-ttu-id="7d322-107">如需詳細資訊，請參閱[逐步解說：篩選 My.Application.Log 輸出](walkthrough-filtering-my-application-log-output.md)。</span><span class="sxs-lookup"><span data-stu-id="7d322-107">For more information about filtering, see [Walkthrough: Filtering My.Application.Log Output](walkthrough-filtering-my-application-log-output.md).</span></span>  
  
 <span data-ttu-id="7d322-108">不過，如果記錄檔設定不正確，您可能需要目前組態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7d322-108">However, if a log is configured incorrectly, you may need more information about its current configuration.</span></span> <span data-ttu-id="7d322-109">您可以透過記錄檔的進階 `TraceSource` 屬性來取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="7d322-109">You can get to this information through the log's advanced `TraceSource` property.</span></span>  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a><span data-ttu-id="7d322-110">判斷程式碼中記錄檔物件的記錄檔接聽程式</span><span class="sxs-lookup"><span data-stu-id="7d322-110">To determine the log listeners for the Log object in code</span></span>  
  
1. <span data-ttu-id="7d322-111">在程式碼檔案的開頭處匯入 <xref:System.Diagnostics> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="7d322-111">Import the <xref:System.Diagnostics> namespace at the beginning of the code file.</span></span> <span data-ttu-id="7d322-112">如需詳細資訊，請參閱 [Imports 陳述式 (.NET 命名空間和類型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)。</span><span class="sxs-lookup"><span data-stu-id="7d322-112">For more information, see [Imports Statement (.NET Namespace and Type)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md).</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2. <span data-ttu-id="7d322-113">建立會傳回字串的函式，而該字串包含每個記錄檔接聽程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="7d322-113">Create a function that returns a string consisting of information for each of the log's listeners.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3. <span data-ttu-id="7d322-114">將記錄檔的追蹤接聽程式集合傳遞至 `GetListeners` 函式，並顯示傳回值。</span><span class="sxs-lookup"><span data-stu-id="7d322-114">Pass the collection of the log's trace listeners to the `GetListeners` function, and display the return value.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     <span data-ttu-id="7d322-115">如需詳細資訊，請參閱 <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7d322-115">For more information, see <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7d322-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7d322-116">See also</span></span>

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [<span data-ttu-id="7d322-117">使用應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="7d322-117">Working with Application Logs</span></span>](working-with-application-logs.md)
- [<span data-ttu-id="7d322-118">逐步解說：判斷 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="7d322-118">Walkthrough: Determining Where My.Application.Log Writes Information</span></span>](walkthrough-determining-where-my-application-log-writes-information.md)

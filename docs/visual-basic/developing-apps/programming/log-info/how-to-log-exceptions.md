---
title: 作法：記錄例外狀況
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, logging
- exceptions, tracking
ms.assetid: a26c60e2-ae39-444a-aebb-33eccadc0eeb
ms.openlocfilehash: 59ed7b836126a38f32b7c6f479570a566d236e6c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410110"
---
# <a name="how-to-log-exceptions-in-visual-basic"></a><span data-ttu-id="84e5e-102">如何：在 Visual Basic 中記錄例外狀況</span><span class="sxs-lookup"><span data-stu-id="84e5e-102">How to: Log Exceptions in Visual Basic</span></span>

<span data-ttu-id="84e5e-103">您可以使用 `My.Application.Log` 和 `My.Log` 物件來記錄應用程式中發生之例外狀況的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="84e5e-103">You can use the `My.Application.Log` and `My.Log` objects to log information about exceptions that occur in your application.</span></span> <span data-ttu-id="84e5e-104">下列範例示範如何使用 `My.Application.Log.WriteException` 方法，以記錄您明確攔截到的例外狀況和未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="84e5e-104">These examples show how to use the `My.Application.Log.WriteException` method to log exceptions that you catch explicitly and exceptions that are unhandled.</span></span>  
  
 <span data-ttu-id="84e5e-105">如需記錄追蹤資訊，請使用 `My.Application.Log.WriteEntry` 方法。</span><span class="sxs-lookup"><span data-stu-id="84e5e-105">For logging tracing information, use the `My.Application.Log.WriteEntry` method.</span></span> <span data-ttu-id="84e5e-106">如需詳細資訊，請參閱＜<xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>＞</span><span class="sxs-lookup"><span data-stu-id="84e5e-106">For more information, see <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A></span></span>  
  
### <a name="to-log-a-handled-exception"></a><span data-ttu-id="84e5e-107">記錄已處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="84e5e-107">To log a handled exception</span></span>  
  
1. <span data-ttu-id="84e5e-108">建立將產生例外狀況資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="84e5e-108">Create the method that will generate the exception information.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#9)]  
  
2. <span data-ttu-id="84e5e-109">使用 `Try...Catch` 區塊來攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="84e5e-109">Use a `Try...Catch` block to catch the exception.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#6)]  
  
3. <span data-ttu-id="84e5e-110">將可產生例外狀況的程式碼放在 `Try` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="84e5e-110">Put the code that could generate an exception in the `Try` block.</span></span>  
  
     <span data-ttu-id="84e5e-111">取消 `Dim` 和 `MsgBox` 行的註解，造成 <xref:System.NullReferenceException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="84e5e-111">Uncomment the `Dim` and `MsgBox` lines to cause a <xref:System.NullReferenceException> exception.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#7)]  
  
4. <span data-ttu-id="84e5e-112">在 `Catch` 區塊中，使用 `My.Application.Log.WriteException` 方法來寫入例外狀況資訊。</span><span class="sxs-lookup"><span data-stu-id="84e5e-112">In the `Catch` block, use the `My.Application.Log.WriteException` method to write the exception information.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#8)]  
  
     <span data-ttu-id="84e5e-113">下列範例顯示用於記錄已處理例外狀況的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="84e5e-113">The following example shows the complete code for logging a handled exception.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#10)]  
  
### <a name="to-log-an-unhandled-exception"></a><span data-ttu-id="84e5e-114">記錄未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="84e5e-114">To log an unhandled exception</span></span>  
  
1. <span data-ttu-id="84e5e-115">在 **方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="84e5e-115">Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="84e5e-116">在 [**專案**] 功能表上，選擇 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="84e5e-116">On the **Project** menu, choose **Properties**.</span></span>  
  
2. <span data-ttu-id="84e5e-117">按一下 [應用程式] \*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="84e5e-117">Click the **Application** tab.</span></span>  
  
3. <span data-ttu-id="84e5e-118">按一下 [檢視應用程式事件] \*\*\*\* 按鈕以開啟 [程式碼編輯器]。</span><span class="sxs-lookup"><span data-stu-id="84e5e-118">Click the **View Application Events** button to open the Code Editor.</span></span>  
  
     <span data-ttu-id="84e5e-119">這會開啟 ApplicationEvents.vb 檔案。</span><span class="sxs-lookup"><span data-stu-id="84e5e-119">This opens the ApplicationEvents.vb file.</span></span>  
  
4. <span data-ttu-id="84e5e-120">在 [程式碼編輯器] 中開啟 ApplicationEvents.vb 檔案。</span><span class="sxs-lookup"><span data-stu-id="84e5e-120">Have the ApplicationEvents.vb file open in the Code Editor.</span></span> <span data-ttu-id="84e5e-121">在 [一般] \*\*\*\* 功能表上，選擇 [MyApplication 事件] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="84e5e-121">On the **General** menu, choose **MyApplication Events**.</span></span>  
  
5. <span data-ttu-id="84e5e-122">在 [宣告]\*\*\*\* 功能表上，選擇 [未處理的例外狀況]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="84e5e-122">On the **Declarations** menu, choose **UnhandledException**.</span></span>  
  
     <span data-ttu-id="84e5e-123">應用程式在主應用程式執行之前，引發 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 事件。</span><span class="sxs-lookup"><span data-stu-id="84e5e-123">The application raises the <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> event before the main application runs.</span></span>  
  
6. <span data-ttu-id="84e5e-124">將 `My.Application.Log.WriteException` 方法加入 `UnhandledException` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="84e5e-124">Add the `My.Application.Log.WriteException` method to the `UnhandledException` event handler.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#4)]  
  
     <span data-ttu-id="84e5e-125">下列範例顯示用於記錄未處理例外狀況的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="84e5e-125">The following example shows the complete code for logging an unhandled exception.</span></span>  
  
     [!code-vb[VbVbalrMyApplicationLog#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="84e5e-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84e5e-126">See also</span></span>

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [<span data-ttu-id="84e5e-127">使用應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="84e5e-127">Working with Application Logs</span></span>](working-with-application-logs.md)
- [<span data-ttu-id="84e5e-128">作法：寫入記錄檔訊息</span><span class="sxs-lookup"><span data-stu-id="84e5e-128">How to: Write Log Messages</span></span>](how-to-write-log-messages.md)
- [<span data-ttu-id="84e5e-129">逐步解說：判斷 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="84e5e-129">Walkthrough: Determining Where My.Application.Log Writes Information</span></span>](walkthrough-determining-where-my-application-log-writes-information.md)
- [<span data-ttu-id="84e5e-130">逐步解說：變更 My.Application.Log 寫入資訊的位置</span><span class="sxs-lookup"><span data-stu-id="84e5e-130">Walkthrough: Changing Where My.Application.Log Writes Information</span></span>](walkthrough-changing-where-my-application-log-writes-information.md)

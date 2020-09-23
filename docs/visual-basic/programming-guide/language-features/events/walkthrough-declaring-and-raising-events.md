---
title: 宣告和引發事件
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], events
- events [Visual Basic], walkthroughs
- declaring events [Visual Basic], walkthroughs
- events [Visual Basic], declaring
- events [Visual Basic], raising
- raising events [Visual Basic], walkthroughs
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
ms.openlocfilehash: 07ef611b50cfa13f77fa168d58dd3b43e97eeec6
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91057984"
---
# <a name="walkthrough-declaring-and-raising-events-visual-basic"></a><span data-ttu-id="1a920-102">逐步解說：宣告和引發事件 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1a920-102">Walkthrough: Declaring and Raising Events (Visual Basic)</span></span>

<span data-ttu-id="1a920-103">本逐步解說示範如何針對名為的類別宣告和引發事件 `Widget` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-103">This walkthrough demonstrates how to declare and raise events for a class named `Widget`.</span></span> <span data-ttu-id="1a920-104">完成這些步驟之後，您可能想要閱讀「 [逐步解說：處理事件](walkthrough-handling-events.md)」等主題，其中顯示如何使用 `Widget` 物件中的事件來提供應用程式中的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="1a920-104">After you complete the steps, you might want to read the companion topic, [Walkthrough: Handling Events](walkthrough-handling-events.md), which shows how to use events from `Widget` objects to provide status information in an application.</span></span>  
  
## <a name="the-widget-class"></a><span data-ttu-id="1a920-105">Widget 類別</span><span class="sxs-lookup"><span data-stu-id="1a920-105">The Widget Class</span></span>  

 <span data-ttu-id="1a920-106">假設您有一個 `Widget` 類別。</span><span class="sxs-lookup"><span data-stu-id="1a920-106">Assume for the moment that you have a `Widget` class.</span></span> <span data-ttu-id="1a920-107">您的 `Widget` 類別具有可能需要很長時間才能執行的方法，而且您想要讓應用程式能夠產生某種類型的完成指標。</span><span class="sxs-lookup"><span data-stu-id="1a920-107">Your `Widget` class has a method that can take a long time to execute, and you want your application to be able to put up some kind of completion indicator.</span></span>  
  
 <span data-ttu-id="1a920-108">當然，您可以將 `Widget` 物件顯示為 [百分比-完成] 對話方塊，但是在您使用類別的每個專案中，您會在該對話方塊中停滯 `Widget` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-108">Of course, you could make the `Widget` object show a percent-complete dialog box, but then you would be stuck with that dialog box in every project in which you used the `Widget` class.</span></span> <span data-ttu-id="1a920-109">物件設計的好準則是讓使用物件的應用程式處理使用者介面，除非物件的整個目的是要管理表單或對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1a920-109">A good principle of object design is to let the application that uses an object handle the user interface—unless the whole purpose of the object is to manage a form or dialog box.</span></span>  
  
 <span data-ttu-id="1a920-110">的目的 `Widget` 是要執行其他工作，因此最好加入 `PercentDone` 事件，然後讓呼叫 `Widget` 的方法的程式處理該事件，並顯示狀態更新。</span><span class="sxs-lookup"><span data-stu-id="1a920-110">The purpose of `Widget` is to perform other tasks, so it is better to add a `PercentDone` event and let the procedure that calls `Widget`'s methods handle that event and display status updates.</span></span> <span data-ttu-id="1a920-111">此 `PercentDone` 事件也可以提供取消工作的機制。</span><span class="sxs-lookup"><span data-stu-id="1a920-111">The `PercentDone` event can also provide a mechanism for canceling the task.</span></span>  
  
#### <a name="to-build-the-code-example-for-this-topic"></a><span data-ttu-id="1a920-112">若要建立本主題的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1a920-112">To build the code example for this topic</span></span>  
  
1. <span data-ttu-id="1a920-113">開啟新的 Visual Basic Windows 應用程式專案，並建立名為的表單 `Form1` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-113">Open a new Visual Basic Windows Application project and create a form named `Form1`.</span></span>  
  
2. <span data-ttu-id="1a920-114">將兩個按鈕和標籤新增至 `Form1` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-114">Add two buttons and a label to `Form1`.</span></span>  
  
3. <span data-ttu-id="1a920-115">依照下表所示的方式，命名物件。</span><span class="sxs-lookup"><span data-stu-id="1a920-115">Name the objects as shown in the following table.</span></span>  
  
    |<span data-ttu-id="1a920-116">Object</span><span class="sxs-lookup"><span data-stu-id="1a920-116">Object</span></span>|<span data-ttu-id="1a920-117">屬性</span><span class="sxs-lookup"><span data-stu-id="1a920-117">Property</span></span>|<span data-ttu-id="1a920-118">設定</span><span class="sxs-lookup"><span data-stu-id="1a920-118">Setting</span></span>|  
    |------------|--------------|-------------|  
    |`Button1`|`Text`|<span data-ttu-id="1a920-119">啟動工作</span><span class="sxs-lookup"><span data-stu-id="1a920-119">Start Task</span></span>|  
    |`Button2`|`Text`|<span data-ttu-id="1a920-120">取消</span><span class="sxs-lookup"><span data-stu-id="1a920-120">Cancel</span></span>|  
    |`Label`|<span data-ttu-id="1a920-121">`(Name)`, `Text`</span><span class="sxs-lookup"><span data-stu-id="1a920-121">`(Name)`, `Text`</span></span>|<span data-ttu-id="1a920-122">lblPercentDone，0</span><span class="sxs-lookup"><span data-stu-id="1a920-122">lblPercentDone, 0</span></span>|  
  
4. <span data-ttu-id="1a920-123">在 [ **專案** ] 功能表上，選擇 [ **加入類別** ]，將名為的類別加入 `Widget.vb` 至專案。</span><span class="sxs-lookup"><span data-stu-id="1a920-123">On the **Project** menu, choose **Add Class** to add a class named `Widget.vb` to the project.</span></span>  
  
#### <a name="to-declare-an-event-for-the-widget-class"></a><span data-ttu-id="1a920-124">宣告 Widget 類別的事件</span><span class="sxs-lookup"><span data-stu-id="1a920-124">To declare an event for the Widget class</span></span>  
  
- <span data-ttu-id="1a920-125">使用 `Event` 關鍵字來宣告類別中的事件 `Widget` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-125">Use the `Event` keyword to declare an event in the `Widget` class.</span></span> <span data-ttu-id="1a920-126">請注意，事件可以有 `ByVal` 和 `ByRef` 引數，如事件所示 `Widget` `PercentDone` ：</span><span class="sxs-lookup"><span data-stu-id="1a920-126">Note that an event can have `ByVal` and `ByRef` arguments, as `Widget`'s `PercentDone` event demonstrates:</span></span>  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#1)]  
  
 <span data-ttu-id="1a920-127">當呼叫物件接收事件時 `PercentDone` ， `Percent` 引數會包含已完成工作的百分比。</span><span class="sxs-lookup"><span data-stu-id="1a920-127">When the calling object receives a `PercentDone` event, the `Percent` argument contains the percentage of the task that is complete.</span></span> <span data-ttu-id="1a920-128">`Cancel`引數可以設定為， `True` 以取消引發事件的方法。</span><span class="sxs-lookup"><span data-stu-id="1a920-128">The `Cancel` argument can be set to `True` to cancel the method that raised the event.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1a920-129">您可以像處理常式的引數一樣宣告事件引數，但有下列例外狀況：事件不能有 `Optional` 或 `ParamArray` 引數，而且事件沒有傳回值。</span><span class="sxs-lookup"><span data-stu-id="1a920-129">You can declare event arguments just as you do arguments of procedures, with the following exceptions: Events cannot have `Optional` or `ParamArray` arguments, and events do not have return values.</span></span>  
  
 <span data-ttu-id="1a920-130">此 `PercentDone` 事件是由類別的 `LongTask` 方法所引發 `Widget` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-130">The `PercentDone` event is raised by the `LongTask` method of the `Widget` class.</span></span> <span data-ttu-id="1a920-131">`LongTask` 採用兩個引數：方法經過偽裝來執行工作的時間長度，以及 `LongTask` 暫停以引發事件的最小時間間隔 `PercentDone` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-131">`LongTask` takes two arguments: the length of time the method pretends to be doing work, and the minimum time interval before `LongTask` pauses to raise the `PercentDone` event.</span></span>  
  
#### <a name="to-raise-the-percentdone-event"></a><span data-ttu-id="1a920-132">引發 PercentDone 事件</span><span class="sxs-lookup"><span data-stu-id="1a920-132">To raise the PercentDone event</span></span>  
  
1. <span data-ttu-id="1a920-133">若要簡化 `Timer` 這個類別所使用之屬性的存取，請將 `Imports` 語句加入至類別模組的宣告區段頂端的 `Class Widget` 語句上方。</span><span class="sxs-lookup"><span data-stu-id="1a920-133">To simplify access to the `Timer` property used by this class, add an `Imports` statement to the top of the declarations section of your class module, above the `Class Widget` statement.</span></span>  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#2)]  
  
2. <span data-ttu-id="1a920-134">將下列程式碼新增至 `Widget` 類別：</span><span class="sxs-lookup"><span data-stu-id="1a920-134">Add the following code to the `Widget` class:</span></span>  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#3)]  
  
 <span data-ttu-id="1a920-135">當您的應用程式呼叫 `LongTask` 方法時， `Widget` 類別每秒會引發 `PercentDone` 事件 `MinimumInterval` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-135">When your application calls the `LongTask` method, the `Widget` class raises the `PercentDone` event every `MinimumInterval` seconds.</span></span> <span data-ttu-id="1a920-136">當事件傳回時，會 `LongTask` 檢查是否 `Cancel` 已將引數設定為 `True` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-136">When the event returns, `LongTask` checks to see if the `Cancel` argument was set to `True`.</span></span>  
  
 <span data-ttu-id="1a920-137">這裡有幾個免責聲明。</span><span class="sxs-lookup"><span data-stu-id="1a920-137">A few disclaimers are necessary here.</span></span> <span data-ttu-id="1a920-138">為了簡單起見，此程式 `LongTask` 會假設您事先知道工作將花費多少時間。</span><span class="sxs-lookup"><span data-stu-id="1a920-138">For simplicity, the `LongTask` procedure assumes you know in advance how long the task will take.</span></span> <span data-ttu-id="1a920-139">這幾乎不會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="1a920-139">This is almost never the case.</span></span> <span data-ttu-id="1a920-140">將工作分割成偶數的區塊可能會很困難，而且最重要的是，使用者最重要的是，這只是讓使用者知道發生問題的時間量。</span><span class="sxs-lookup"><span data-stu-id="1a920-140">Dividing tasks into chunks of even size can be difficult, and often what matters most to users is simply the amount of time that passes before they get an indication that something is happening.</span></span>  
  
 <span data-ttu-id="1a920-141">在此範例中，您可能已發現另一個瑕疵。</span><span class="sxs-lookup"><span data-stu-id="1a920-141">You may have spotted another flaw in this sample.</span></span> <span data-ttu-id="1a920-142">`Timer`屬性會傳回從午夜開始經過的秒數，因此，如果應用程式是在午夜前啟動，就會停滯。</span><span class="sxs-lookup"><span data-stu-id="1a920-142">The `Timer` property returns the number of seconds that have passed since midnight; therefore, the application gets stuck if it is started just before midnight.</span></span> <span data-ttu-id="1a920-143">更謹慎的測量時間方法會將界限條件（如這項考慮）納入考慮，或使用等屬性來完全避免 `Now` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-143">A more careful approach to measuring time would take boundary conditions such as this into consideration, or avoid them altogether, using properties such as `Now`.</span></span>  
  
 <span data-ttu-id="1a920-144">現在 `Widget` 類別可以引發事件，接下來您可以移至下一個逐步解說。</span><span class="sxs-lookup"><span data-stu-id="1a920-144">Now that the `Widget` class can raise events, you can move to the next walkthrough.</span></span> <span data-ttu-id="1a920-145">[逐步解說：處理事件](walkthrough-handling-events.md) 示範如何使用 `WithEvents` ，將事件處理常式與事件產生關聯 `PercentDone` 。</span><span class="sxs-lookup"><span data-stu-id="1a920-145">[Walkthrough: Handling Events](walkthrough-handling-events.md) demonstrates how to use `WithEvents` to associate an event handler with the `PercentDone` event.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1a920-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1a920-146">See also</span></span>

- <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>
- <xref:Microsoft.VisualBasic.DateAndTime.Now%2A>
- [<span data-ttu-id="1a920-147">逐步解說：處理事件</span><span class="sxs-lookup"><span data-stu-id="1a920-147">Walkthrough: Handling Events</span></span>](walkthrough-handling-events.md)
- [<span data-ttu-id="1a920-148">事件</span><span class="sxs-lookup"><span data-stu-id="1a920-148">Events</span></span>](index.md)

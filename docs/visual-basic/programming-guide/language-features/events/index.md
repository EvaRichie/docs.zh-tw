---
title: 事件
ms.date: 07/20/2015
helpviewer_keywords:
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
ms.openlocfilehash: c61e960078557282de39bdc30f1d614ce8a77f29
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405115"
---
# <a name="events-visual-basic"></a><span data-ttu-id="b880e-102">事件 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b880e-102">Events (Visual Basic)</span></span>
<span data-ttu-id="b880e-103">雖然您可能會將 Visual Studio 專案視覺化成一系列以序列方式執行的程式，但實際上，大部分的程式都是事件驅動的，這表示執行流程是由稱為*事件*的外部出現專案所決定。</span><span class="sxs-lookup"><span data-stu-id="b880e-103">While you might visualize a Visual Studio project as a series of procedures that execute in a sequence, in reality, most programs are event driven—meaning the flow of execution is determined by external occurrences called *events*.</span></span>  
  
 <span data-ttu-id="b880e-104">事件是通知應用程式發生重要事件的信號。</span><span class="sxs-lookup"><span data-stu-id="b880e-104">An event is a signal that informs an application that something important has occurred.</span></span> <span data-ttu-id="b880e-105">例如，當使用者按一下表單上的控制項時，表單可以引發 `Click` 事件，並呼叫處理事件的程序。</span><span class="sxs-lookup"><span data-stu-id="b880e-105">For example, when a user clicks a control on a form, the form can raise a `Click` event and call a procedure that handles the event.</span></span> <span data-ttu-id="b880e-106">事件也允許個別工作進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b880e-106">Events also allow separate tasks to communicate.</span></span> <span data-ttu-id="b880e-107">例如，假設您的應用程式與主應用程式個別執行排序工作。</span><span class="sxs-lookup"><span data-stu-id="b880e-107">Say, for example, that your application performs a sort task separately from the main application.</span></span> <span data-ttu-id="b880e-108">如果使用者取消排序，則您的應用程式可以傳送取消事件，以指示排序處理序停止。</span><span class="sxs-lookup"><span data-stu-id="b880e-108">If a user cancels the sort, your application can send a cancel event instructing the sort process to stop.</span></span>  
  
## <a name="event-terms-and-concepts"></a><span data-ttu-id="b880e-109">事件詞彙和概念</span><span class="sxs-lookup"><span data-stu-id="b880e-109">Event Terms and Concepts</span></span>  
 <span data-ttu-id="b880e-110">本節說明 Visual Basic 中的事件所使用的詞彙和概念。</span><span class="sxs-lookup"><span data-stu-id="b880e-110">This section describes the terms and concepts used with events in Visual Basic.</span></span>  
  
### <a name="declaring-events"></a><span data-ttu-id="b880e-111">宣告事件</span><span class="sxs-lookup"><span data-stu-id="b880e-111">Declaring Events</span></span>  
 <span data-ttu-id="b880e-112">您可以在類別、結構、模組和介面內，使用 `Event` 關鍵字宣告事件，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b880e-112">You declare events within classes, structures, modules, and interfaces using the `Event` keyword, as in the following example:</span></span>  
  
 [!code-vb[VbVbalrEvents#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#24)]  
  
### <a name="raising-events"></a><span data-ttu-id="b880e-113">引發事件</span><span class="sxs-lookup"><span data-stu-id="b880e-113">Raising Events</span></span>  
 <span data-ttu-id="b880e-114">事件就像是訊息，會告知發生了重要事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-114">An event is like a message announcing that something important has occurred.</span></span> <span data-ttu-id="b880e-115">廣播訊息的動作稱為「引發」\*\* 事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-115">The act of broadcasting the message is called *raising* the event.</span></span> <span data-ttu-id="b880e-116">在 Visual Basic 中，您會使用語句引發事件 `RaiseEvent` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b880e-116">In Visual Basic, you raise events with the `RaiseEvent` statement, as in the following example:</span></span>  
  
 [!code-vb[VbVbalrEvents#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#25)]  
  
 <span data-ttu-id="b880e-117">事件必須在其宣告所在的類別、模組或結構範圍內引發。</span><span class="sxs-lookup"><span data-stu-id="b880e-117">Events must be raised within the scope of the class, module, or structure where they are declared.</span></span> <span data-ttu-id="b880e-118">例如，衍生的類別無法引發繼承自基底類別的事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-118">For example, a derived class cannot raise events inherited from a base class.</span></span>  
  
### <a name="event-senders"></a><span data-ttu-id="b880e-119">事件傳送者</span><span class="sxs-lookup"><span data-stu-id="b880e-119">Event Senders</span></span>  
 <span data-ttu-id="b880e-120">任何可引發事件的物件都是「事件傳送者」**，亦稱為「事件來源」**。</span><span class="sxs-lookup"><span data-stu-id="b880e-120">Any object capable of raising an event is an *event sender*, also known as an *event source*.</span></span> <span data-ttu-id="b880e-121">表單、控制項和使用者定義的物件都是事件傳送者的範例。</span><span class="sxs-lookup"><span data-stu-id="b880e-121">Forms, controls, and user-defined objects are examples of event senders.</span></span>  
  
### <a name="event-handlers"></a><span data-ttu-id="b880e-122">事件處理常式</span><span class="sxs-lookup"><span data-stu-id="b880e-122">Event Handlers</span></span>  
 <span data-ttu-id="b880e-123">「事件處理常式」\*\* 是在發生相對應事件時所呼叫的程序。</span><span class="sxs-lookup"><span data-stu-id="b880e-123">*Event handlers* are procedures that are called when a corresponding event occurs.</span></span> <span data-ttu-id="b880e-124">您可以使用具有相符簽章的任何有效副程式，做為事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b880e-124">You can use any valid subroutine with a matching signature as an event handler.</span></span> <span data-ttu-id="b880e-125">不過，您無法使用函式做為事件處理常式，因為它無法將值傳回事件來源。</span><span class="sxs-lookup"><span data-stu-id="b880e-125">You cannot use a function as an event handler, however, because it cannot return a value to the event source.</span></span>  
  
 <span data-ttu-id="b880e-126">Visual Basic 針對事件處理常式（結合事件傳送者的名稱、底線和事件名稱）使用標準命名慣例。</span><span class="sxs-lookup"><span data-stu-id="b880e-126">Visual Basic uses a standard naming convention for event handlers that combines the name of the event sender, an underscore, and the name of the event.</span></span> <span data-ttu-id="b880e-127">例如，將名為 `button1` 的按鈕 `Click` 事件命名為 `Sub button1_Click`。</span><span class="sxs-lookup"><span data-stu-id="b880e-127">For example, the `Click` event of a button named `button1` would be named `Sub button1_Click`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b880e-128">我們建議您在為自己的事件定義事件處理常式時，使用此命名慣例，但這並非必要；您可以使用任何有效的副程式名稱。</span><span class="sxs-lookup"><span data-stu-id="b880e-128">We recommend that you use this naming convention when defining event handlers for your own events, but it is not required; you can use any valid subroutine name.</span></span>  
  
## <a name="associating-events-with-event-handlers"></a><span data-ttu-id="b880e-129">建立事件與事件處理常式的關聯</span><span class="sxs-lookup"><span data-stu-id="b880e-129">Associating Events with Event Handlers</span></span>  
 <span data-ttu-id="b880e-130">讓事件處理常式變成可用之前，您必須先使用 `Handles` 或 `AddHandler` 陳述式來建立它與事件的關聯。</span><span class="sxs-lookup"><span data-stu-id="b880e-130">Before an event handler becomes usable, you must first associate it with an event by using either the `Handles` or `AddHandler` statement.</span></span>  
  
### <a name="withevents-and-the-handles-clause"></a><span data-ttu-id="b880e-131">WithEvents 和 Handles 子句</span><span class="sxs-lookup"><span data-stu-id="b880e-131">WithEvents and the Handles Clause</span></span>  
 <span data-ttu-id="b880e-132">`WithEvents` 陳述式和 `Handles` 子句提供一種宣告式方式來指定事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b880e-132">The `WithEvents` statement and `Handles` clause provide a declarative way of specifying event handlers.</span></span> <span data-ttu-id="b880e-133">使用 `WithEvents` 關鍵字宣告之物件所引發的事件可以透過任何具有 `Handles` 陳述式的程序來處理，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b880e-133">An event raised by an object declared with the `WithEvents` keyword can be handled by any procedure with a `Handles` statement for that event, as shown in the following example:</span></span>  
  
 [!code-vb[VbVbalrEvents#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#1)]  
  
 <span data-ttu-id="b880e-134">`WithEvents` 陳述式和 `Handles` 子句通常是事件處理常式的最佳選擇，因為它們使用的宣告式語法讓事件能夠更容易處理程式碼、讀取及偵錯。</span><span class="sxs-lookup"><span data-stu-id="b880e-134">The `WithEvents` statement and the `Handles` clause are often the best choice for event handlers because the declarative syntax they use makes event handling easier to code, read and debug.</span></span> <span data-ttu-id="b880e-135">不過，請注意下列有關使用 `WithEvents` 變數的限制：</span><span class="sxs-lookup"><span data-stu-id="b880e-135">However, be aware of the following limitations on the use of `WithEvents` variables:</span></span>  
  
- <span data-ttu-id="b880e-136">您不能使用 `WithEvents` 變數做為物件變數。</span><span class="sxs-lookup"><span data-stu-id="b880e-136">You cannot use a `WithEvents` variable as an object variable.</span></span> <span data-ttu-id="b880e-137">也就是說，您無法將它宣告為 `Object` - 當您宣告變數時，必須指定類別名稱。</span><span class="sxs-lookup"><span data-stu-id="b880e-137">That is, you cannot declare it as `Object`—you must specify the class name when you declare the variable.</span></span>  
  
- <span data-ttu-id="b880e-138">由於共用事件不會系結至類別實例，因此您無法使用 `WithEvents` 以宣告方式處理共用事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-138">Because shared events are not tied to class instances, you cannot use `WithEvents` to declaratively handle shared events.</span></span> <span data-ttu-id="b880e-139">同樣地，您不能使用 `WithEvents` 或 `Handles`，處理來自 `Structure` 的事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-139">Similarly, you cannot use `WithEvents` or `Handles` to handle events from a `Structure`.</span></span> <span data-ttu-id="b880e-140">在這兩種情況下，您可以使用 `AddHandler` 陳述式來處理這些事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-140">In both cases, you can use the `AddHandler` statement to handle those events.</span></span>  
  
- <span data-ttu-id="b880e-141">您無法建立 `WithEvents` 變數的陣列。</span><span class="sxs-lookup"><span data-stu-id="b880e-141">You cannot create arrays of `WithEvents` variables.</span></span>  
  
 <span data-ttu-id="b880e-142">`WithEvents` 變數可讓單一事件處理常式處理一或多種事件，或者讓一或多個事件處理常式處理相同種類的事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-142">`WithEvents` variables allow a single event handler to handle one or more kind of event, or one or more event handlers to handle the same kind of event.</span></span>  
  
 <span data-ttu-id="b880e-143">雖然 `Handles` 子句是建立事件與事件處理常式之關聯的標準方式，但它只能在編譯時期建立事件與事件處理常式的關聯。</span><span class="sxs-lookup"><span data-stu-id="b880e-143">Although the `Handles` clause is the standard way of associating an event with an event handler, it is limited to associating events with event handlers at compile time.</span></span>  
  
 <span data-ttu-id="b880e-144">在某些情況下，例如使用與表單或控制項相關聯的事件，Visual Basic 會自動將空的事件處理常式存根，並將其與事件產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b880e-144">In some cases, such as with events associated with forms or controls, Visual Basic automatically stubs out an empty event handler and associates it with an event.</span></span> <span data-ttu-id="b880e-145">例如，當您在設計模式中按兩下表單上的命令按鈕時，Visual Basic 會建立空的事件處理常式和 `WithEvents` 命令按鈕的變數，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b880e-145">For example, when you double-click a command button on a form in design mode, Visual Basic creates an empty event handler and a `WithEvents` variable for the command button, as in the following code:</span></span>  
  
 [!code-vb[VbVbalrEvents#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#26)]  
  
### <a name="addhandler-and-removehandler"></a><span data-ttu-id="b880e-146">AddHandler 和 RemoveHandler</span><span class="sxs-lookup"><span data-stu-id="b880e-146">AddHandler and RemoveHandler</span></span>  
 <span data-ttu-id="b880e-147">`AddHandler` 陳述式類似 `Handles` 子句，這兩者都能讓您指定事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b880e-147">The `AddHandler` statement is similar to the `Handles` clause in that both allow you to specify an event handler.</span></span> <span data-ttu-id="b880e-148">不過，與 `RemoveHandler` 搭配使用的 `AddHandler` 所提供的彈性比 `Handles` 子句更大，可讓您以動態方式加入、移除及變更與事件相關聯的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b880e-148">However, `AddHandler`, used with `RemoveHandler`, provides greater flexibility than the `Handles` clause, allowing you to dynamically add, remove, and change the event handler associated with an event.</span></span> <span data-ttu-id="b880e-149">如果您想要處理共用的事件或來自結構的事件，就必須使用 `AddHandler`。</span><span class="sxs-lookup"><span data-stu-id="b880e-149">If you want to handle shared events or events from a structure, you must use `AddHandler`.</span></span>  
  
 <span data-ttu-id="b880e-150">`AddHandler` 會採用兩個引數︰來自事件傳送者的事件名稱 (例如控制項)，以及評估委派的運算式。</span><span class="sxs-lookup"><span data-stu-id="b880e-150">`AddHandler` takes two arguments: the name of an event from an event sender such as a control, and an expression that evaluates to a delegate.</span></span> <span data-ttu-id="b880e-151">使用 `AddHandler` 時，您不需明確指定委派類別，因為 `AddressOf` 陳述式一律會傳回對委派的參考。</span><span class="sxs-lookup"><span data-stu-id="b880e-151">You do not need to explicitly specify the delegate class when using `AddHandler`, since the `AddressOf` statement always returns a reference to the delegate.</span></span> <span data-ttu-id="b880e-152">下列範例會建立事件處理常式與物件所引發之事件的關聯：</span><span class="sxs-lookup"><span data-stu-id="b880e-152">The following example associates an event handler with an event raised by an object:</span></span>  
  
 [!code-vb[VbVbalrEvents#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#28)]  
  
 <span data-ttu-id="b880e-153">`RemoveHandler` (其會中斷事件與事件處理常式的關聯) 會使用與 `AddHandler` 相同的語法。</span><span class="sxs-lookup"><span data-stu-id="b880e-153">`RemoveHandler`, which disconnects an event from an event handler, uses the same syntax as `AddHandler`.</span></span> <span data-ttu-id="b880e-154">例如：</span><span class="sxs-lookup"><span data-stu-id="b880e-154">For example:</span></span>  
  
 [!code-vb[VbVbalrEvents#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#29)]  
  
 <span data-ttu-id="b880e-155">在下列範例中，事件處理常式會與事件相關聯，並引發事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-155">In the following example, an event handler is associated with an event, and the event is raised.</span></span> <span data-ttu-id="b880e-156">事件處理常式會攔截事件，並顯示一則訊息。</span><span class="sxs-lookup"><span data-stu-id="b880e-156">The event handler catches the event and displays a message.</span></span>  
  
 <span data-ttu-id="b880e-157">接著，移除第一個事件處理常式，並將不同的事件處理常式關聯至該事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-157">Then the first event handler is removed and a different event handler is associated with the event.</span></span> <span data-ttu-id="b880e-158">再次引發事件時，即會顯示不同的訊息。</span><span class="sxs-lookup"><span data-stu-id="b880e-158">When the event is raised again, a different message is displayed.</span></span>  
  
 <span data-ttu-id="b880e-159">最後，移除第二個事件處理常式，然後第三次引發事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-159">Finally, the second event handler is removed and the event is raised for a third time.</span></span> <span data-ttu-id="b880e-160">由於不再有與事件相關聯的事件處理常式，因此不會採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="b880e-160">Because there is no longer an event handler associated with the event, no action is taken.</span></span>  
  
 [!code-vb[VbVbalrEvents#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class2.vb#38)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a><span data-ttu-id="b880e-161">處理繼承自基底類別的事件</span><span class="sxs-lookup"><span data-stu-id="b880e-161">Handling Events Inherited from a Base Class</span></span>  
 <span data-ttu-id="b880e-162">「衍生類別」\*\*(繼承基底類別特性的類別) 可以使用 `Handles MyBase` 陳述式，來處理其基底類別所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-162">*Derived classes*—classes that inherit characteristics from a base class—can handle events raised by their base class using the `Handles MyBase` statement.</span></span>  
  
### <a name="to-handle-events-from-a-base-class"></a><span data-ttu-id="b880e-163">處理來自基底類別的事件</span><span class="sxs-lookup"><span data-stu-id="b880e-163">To handle events from a base class</span></span>  
  
- <span data-ttu-id="b880e-164">在衍生類別中宣告事件處理常式，方法是將 `Handles MyBase.`*eventname* 陳述式加入至事件處理常式程序的宣告行中，其中 *eventname* 為您要處理之基底類別中的事件名稱。</span><span class="sxs-lookup"><span data-stu-id="b880e-164">Declare an event handler in the derived class by adding a `Handles MyBase.`*eventname* statement to the declaration line of your event-handler procedure, where *eventname* is the name of the event in the base class you are handling.</span></span> <span data-ttu-id="b880e-165">例如：</span><span class="sxs-lookup"><span data-stu-id="b880e-165">For example:</span></span>  
  
     [!code-vb[VbVbalrEvents#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#12)]  
  
## <a name="related-sections"></a><span data-ttu-id="b880e-166">相關章節</span><span class="sxs-lookup"><span data-stu-id="b880e-166">Related Sections</span></span>  
  
|<span data-ttu-id="b880e-167">Title</span><span class="sxs-lookup"><span data-stu-id="b880e-167">Title</span></span>|<span data-ttu-id="b880e-168">描述</span><span class="sxs-lookup"><span data-stu-id="b880e-168">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="b880e-169">逐步解說：宣告和引發事件</span><span class="sxs-lookup"><span data-stu-id="b880e-169">Walkthrough: Declaring and Raising Events</span></span>](walkthrough-declaring-and-raising-events.md)|<span data-ttu-id="b880e-170">提供如何宣告和引發類別事件的逐步說明。</span><span class="sxs-lookup"><span data-stu-id="b880e-170">Provides a step-by-step description of how to declare and raise events for a class.</span></span>|  
|[<span data-ttu-id="b880e-171">逐步解說：處理事件</span><span class="sxs-lookup"><span data-stu-id="b880e-171">Walkthrough: Handling Events</span></span>](walkthrough-handling-events.md)|<span data-ttu-id="b880e-172">示範如何撰寫事件處理常式的程序。</span><span class="sxs-lookup"><span data-stu-id="b880e-172">Demonstrates how to write an event-handler procedure.</span></span>|  
|[<span data-ttu-id="b880e-173">如何：宣告自訂事件以避免封鎖</span><span class="sxs-lookup"><span data-stu-id="b880e-173">How to: Declare Custom Events To Avoid Blocking</span></span>](how-to-declare-custom-events-to-avoid-blocking.md)|<span data-ttu-id="b880e-174">示範如何定義自訂事件，以非同步方式呼叫它的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b880e-174">Demonstrates how to define a custom event that allows its event handlers to be called asynchronously.</span></span>|  
|[<span data-ttu-id="b880e-175">如何：宣告自訂事件以節省記憶體</span><span class="sxs-lookup"><span data-stu-id="b880e-175">How to: Declare Custom Events To Conserve Memory</span></span>](how-to-declare-custom-events-to-conserve-memory.md)|<span data-ttu-id="b880e-176">示範如何定義只有在處理事件時才會使用記憶體的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-176">Demonstrates how to define a custom event that uses memory only when the event is handled.</span></span>|  
|[<span data-ttu-id="b880e-177">Visual Basic 中的繼承事件處理常式疑難排解</span><span class="sxs-lookup"><span data-stu-id="b880e-177">Troubleshooting Inherited Event Handlers in Visual Basic</span></span>](troubleshooting-inherited-event-handlers.md)|<span data-ttu-id="b880e-178">列出繼承元件中的事件處理常式所引發的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b880e-178">Lists common issues that arise with event handlers in inherited components.</span></span>|  
|[<span data-ttu-id="b880e-179">事件</span><span class="sxs-lookup"><span data-stu-id="b880e-179">Events</span></span>](../../../../standard/events/index.md)|<span data-ttu-id="b880e-180">提供 .NET Framework 中事件模型的概觀。</span><span class="sxs-lookup"><span data-stu-id="b880e-180">Provides an overview of the event model in the .NET Framework.</span></span>|  
|[<span data-ttu-id="b880e-181">在 Windows Form 中建立事件處理常式</span><span class="sxs-lookup"><span data-stu-id="b880e-181">Creating Event Handlers in Windows Forms</span></span>](../../../../framework/winforms/creating-event-handlers-in-windows-forms.md)|<span data-ttu-id="b880e-182">描述如何使用與 Windows Form 物件相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="b880e-182">Describes how to work with events associated with Windows Forms objects.</span></span>|  
|[<span data-ttu-id="b880e-183">委派</span><span class="sxs-lookup"><span data-stu-id="b880e-183">Delegates</span></span>](../delegates/index.md)|<span data-ttu-id="b880e-184">提供 Visual Basic 中的委派概觀。</span><span class="sxs-lookup"><span data-stu-id="b880e-184">Provides an overview of delegates in Visual Basic.</span></span>|

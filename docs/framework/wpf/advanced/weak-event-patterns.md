---
title: 弱式事件模式
description: 瞭解 Windows Presentation Foundation 弱式事件模式，其可解決未終結的處理常式問題，避免記憶體流失。
ms.date: 03/30/2017
helpviewer_keywords:
- weak event pattern implementation [WPF]
- event handlers [WPF], weak event pattern
- IWeakEventListener interface [WPF]
ms.assetid: e7c62920-4812-4811-94d8-050a65c856f6
ms.openlocfilehash: 75c6888c8ac20c41d13e3787005377c75248c5d9
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168268"
---
# <a name="weak-event-patterns"></a><span data-ttu-id="bab56-103">弱式事件模式</span><span class="sxs-lookup"><span data-stu-id="bab56-103">Weak Event Patterns</span></span>
<span data-ttu-id="bab56-104">在應用程式中，附加到事件來源的處理常式可能不會在與附加處理常式至來源的接聽程式物件協調時遭到破壞。</span><span class="sxs-lookup"><span data-stu-id="bab56-104">In applications, it is possible that handlers that are attached to event sources will not be destroyed in coordination with the listener object that attached the handler to the source.</span></span> <span data-ttu-id="bab56-105">這種情況可能會導致記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="bab56-105">This situation can lead to memory leaks.</span></span> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]<span data-ttu-id="bab56-106">引進一種設計模式，可以用來解決這個問題，方法是提供特定事件的專用管理員類別，並在該事件的接聽程式上執行介面。</span><span class="sxs-lookup"><span data-stu-id="bab56-106">introduces a design pattern that can be used to address this issue, by providing a dedicated manager class for particular events and implementing an interface on listeners for that event.</span></span> <span data-ttu-id="bab56-107">這個設計模式就是所謂的「*弱式事件模式*」。</span><span class="sxs-lookup"><span data-stu-id="bab56-107">This design pattern is known as the *weak event pattern*.</span></span>  
  
## <a name="why-implement-the-weak-event-pattern"></a><span data-ttu-id="bab56-108">為什麼要執行弱式事件模式？</span><span class="sxs-lookup"><span data-stu-id="bab56-108">Why Implement the Weak Event Pattern?</span></span>  
 <span data-ttu-id="bab56-109">接聽事件可能會導致記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="bab56-109">Listening for events can lead to memory leaks.</span></span> <span data-ttu-id="bab56-110">接聽事件的一般方法是使用特定語言的語法，將處理常式附加至來源上的事件。</span><span class="sxs-lookup"><span data-stu-id="bab56-110">The typical technique for listening to an event is to use the language-specific syntax that attaches a handler to an event on a source.</span></span> <span data-ttu-id="bab56-111">例如，在 c # 中，該語法為： `source.SomeEvent += new SomeEventHandler(MyEventHandler)` 。</span><span class="sxs-lookup"><span data-stu-id="bab56-111">For example, in C#, that syntax is: `source.SomeEvent += new SomeEventHandler(MyEventHandler)`.</span></span>  
  
 <span data-ttu-id="bab56-112">這項技術會建立從事件來源到事件接聽程式的強式參考。</span><span class="sxs-lookup"><span data-stu-id="bab56-112">This technique creates a strong reference from the event source to the event listener.</span></span> <span data-ttu-id="bab56-113">通常，附加接聽項的事件處理常式會導致接聽程式具有受來源物件存留期影響的物件存留期（除非明確地移除事件處理常式）。</span><span class="sxs-lookup"><span data-stu-id="bab56-113">Ordinarily, attaching an event handler for a listener causes the listener to have an object lifetime that is influenced by the object lifetime of the source (unless the event handler is explicitly removed).</span></span> <span data-ttu-id="bab56-114">但在某些情況下，您可能想要讓接聽程式的物件存留期受到其他因素的控制，例如它目前是否屬於應用程式的視覺化樹狀結構，而不是來源的存留期。</span><span class="sxs-lookup"><span data-stu-id="bab56-114">But in certain circumstances, you might want the object lifetime of the listener to be controlled by other factors, such as whether it currently belongs to the visual tree of the application, and not by the lifetime of the source.</span></span> <span data-ttu-id="bab56-115">每當來源物件存留期延伸超出接聽程式的物件存留期時，一般事件模式就會導致記憶體流失：接聽程式的存留時間比預期的長。</span><span class="sxs-lookup"><span data-stu-id="bab56-115">Whenever the source object lifetime extends beyond the object lifetime of the listener, the normal event pattern leads to a memory leak: the listener is kept alive longer than intended.</span></span>  
  
 <span data-ttu-id="bab56-116">弱式事件模式的設計目的是要解決這個記憶體流失的問題。</span><span class="sxs-lookup"><span data-stu-id="bab56-116">The weak event pattern is designed to solve this memory leak problem.</span></span> <span data-ttu-id="bab56-117">每當接聽程式需要註冊事件時，就可以使用弱式事件模式，但是接聽程式並不明確知道何時取消註冊。</span><span class="sxs-lookup"><span data-stu-id="bab56-117">The weak event pattern can be used whenever a listener needs to register for an event, but the listener does not explicitly know when to unregister.</span></span> <span data-ttu-id="bab56-118">只要來源的物件存留期超過接聽程式的有用物件存留期，也可以使用弱式事件模式。</span><span class="sxs-lookup"><span data-stu-id="bab56-118">The weak event pattern can also be used whenever the object lifetime of the source exceeds the useful object lifetime of the listener.</span></span> <span data-ttu-id="bab56-119">（在此案例中，*有用*的是由您所決定）。弱式事件模式可讓接聽程式註冊並接收事件，而不會以任何方式影響接聽項的物件存留期特性。</span><span class="sxs-lookup"><span data-stu-id="bab56-119">(In this case, *useful* is determined by you.) The weak event pattern allows the listener to register for and receive the event without affecting the object lifetime characteristics of the listener in any way.</span></span> <span data-ttu-id="bab56-120">實際上，來自來源的隱含參考不會判斷接聽程式是否符合垃圾收集的資格。</span><span class="sxs-lookup"><span data-stu-id="bab56-120">In effect, the implied reference from the source does not determine whether the listener is eligible for garbage collection.</span></span> <span data-ttu-id="bab56-121">參考是弱式參考，因此會命名弱式事件模式和相關的 Api。</span><span class="sxs-lookup"><span data-stu-id="bab56-121">The reference is a weak reference, thus the naming of the weak event pattern and the related APIs.</span></span> <span data-ttu-id="bab56-122">接聽程式可以進行垃圾收集或以其他方式終結，而來源可以繼續，而不會保留目前已損毀物件的構成處理常式參考。</span><span class="sxs-lookup"><span data-stu-id="bab56-122">The listener can be garbage collected or otherwise destroyed, and the source can continue without retaining noncollectible handler references to a now destroyed object.</span></span>  
  
## <a name="who-should-implement-the-weak-event-pattern"></a><span data-ttu-id="bab56-123">誰應該實行弱式事件模式？</span><span class="sxs-lookup"><span data-stu-id="bab56-123">Who Should Implement the Weak Event Pattern?</span></span>  
 <span data-ttu-id="bab56-124">執行弱式事件模式主要是對控制項作者感興趣。</span><span class="sxs-lookup"><span data-stu-id="bab56-124">Implementing the weak event pattern is interesting primarily for control authors.</span></span> <span data-ttu-id="bab56-125">身為控制項作者，您主要負責控制控制項的行為和內含專案，以及它對插入它的應用程式所造成的影響。</span><span class="sxs-lookup"><span data-stu-id="bab56-125">As a control author, you are largely responsible for the behavior and containment of your control and the impact it has on applications in which it is inserted.</span></span> <span data-ttu-id="bab56-126">這包括控制物件存留期行為，特別是處理所述記憶體流失的問題。</span><span class="sxs-lookup"><span data-stu-id="bab56-126">This includes the control object lifetime behavior, in particular the handling of the described memory leak problem.</span></span>  
  
 <span data-ttu-id="bab56-127">某些案例原本就是將自己帶到弱式事件模式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bab56-127">Certain scenarios inherently lend themselves to the application of the weak event pattern.</span></span> <span data-ttu-id="bab56-128">其中一種情況就是資料系結。</span><span class="sxs-lookup"><span data-stu-id="bab56-128">One such scenario is data binding.</span></span> <span data-ttu-id="bab56-129">在 [資料系結] 中，來源物件與接聽程式物件完全獨立，這是系結的目標。</span><span class="sxs-lookup"><span data-stu-id="bab56-129">In data binding, it is common for the source object to be completely independent of the listener object, which is a target of a binding.</span></span> <span data-ttu-id="bab56-130">資料系結的許多層面 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 已經有在事件的執行方式中所套用的弱式事件模式。</span><span class="sxs-lookup"><span data-stu-id="bab56-130">Many aspects of [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] data binding already have the weak event pattern applied in how the events are implemented.</span></span>  
  
## <a name="how-to-implement-the-weak-event-pattern"></a><span data-ttu-id="bab56-131">如何執行弱式事件模式</span><span class="sxs-lookup"><span data-stu-id="bab56-131">How to Implement the Weak Event Pattern</span></span>  
 <span data-ttu-id="bab56-132">有三種方式可執行弱式事件模式。</span><span class="sxs-lookup"><span data-stu-id="bab56-132">There are three ways to implement weak event pattern.</span></span> <span data-ttu-id="bab56-133">下表列出這三種方法，並提供一些使用時機的指引。</span><span class="sxs-lookup"><span data-stu-id="bab56-133">The following table lists the three approaches and provides some guidance for when you should use each.</span></span>  
  
|<span data-ttu-id="bab56-134">方法</span><span class="sxs-lookup"><span data-stu-id="bab56-134">Approach</span></span>|<span data-ttu-id="bab56-135">執行時機</span><span class="sxs-lookup"><span data-stu-id="bab56-135">When to Implement</span></span>|  
|--------------|-----------------------|  
|<span data-ttu-id="bab56-136">使用現有的弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-136">Use an existing weak event manager class</span></span>|<span data-ttu-id="bab56-137">如果您要訂閱的事件具有對應的 <xref:System.Windows.WeakEventManager> ，請使用現有的弱式事件管理員。</span><span class="sxs-lookup"><span data-stu-id="bab56-137">If the event you want to subscribe to has a corresponding <xref:System.Windows.WeakEventManager>, use the existing weak event manager.</span></span> <span data-ttu-id="bab56-138">如需 WPF 隨附之弱式事件管理員的清單，請參閱類別中的繼承階層架構 <xref:System.Windows.WeakEventManager> 。</span><span class="sxs-lookup"><span data-stu-id="bab56-138">For a list of weak event managers that are included with WPF, see the inheritance hierarchy in the <xref:System.Windows.WeakEventManager> class.</span></span> <span data-ttu-id="bab56-139">由於內含的弱式事件管理員受到限制，因此您可能需要選擇其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="bab56-139">Because the included weak event managers are limited, you will probably need to choose one of the other approaches.</span></span>|  
|<span data-ttu-id="bab56-140">使用一般弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-140">Use a generic weak event manager class</span></span>|<span data-ttu-id="bab56-141"><xref:System.Windows.WeakEventManager%602>當現有的無法使用時 <xref:System.Windows.WeakEventManager> ，您需要簡單的方法來執行，而且您不在意效率。</span><span class="sxs-lookup"><span data-stu-id="bab56-141">Use a generic <xref:System.Windows.WeakEventManager%602> when an existing <xref:System.Windows.WeakEventManager> is not available, you want an easy way to implement, and you are not concerned about efficiency.</span></span> <span data-ttu-id="bab56-142">一般 <xref:System.Windows.WeakEventManager%602> 比現有或自訂弱式事件管理員更有效率。</span><span class="sxs-lookup"><span data-stu-id="bab56-142">The generic <xref:System.Windows.WeakEventManager%602> is less efficient than an existing or custom weak event manager.</span></span> <span data-ttu-id="bab56-143">例如，泛型類別會執行更多反映，以便在指定事件名稱的情況下探索事件。</span><span class="sxs-lookup"><span data-stu-id="bab56-143">For example, the generic class does more reflection to discover the event given the event's name.</span></span> <span data-ttu-id="bab56-144">此外，使用泛型來註冊事件的程式碼， <xref:System.Windows.WeakEventManager%602> 比使用現有或自訂更詳細 <xref:System.Windows.WeakEventManager> 。</span><span class="sxs-lookup"><span data-stu-id="bab56-144">Also, the code to register the event by using the generic <xref:System.Windows.WeakEventManager%602> is more verbose than using an existing or custom <xref:System.Windows.WeakEventManager>.</span></span>|  
|<span data-ttu-id="bab56-145">建立自訂弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-145">Create a custom weak event manager class</span></span>|<span data-ttu-id="bab56-146"><xref:System.Windows.WeakEventManager>當現有的 <xref:System.Windows.WeakEventManager> 無法使用，且您想要獲得最佳效率時，請建立自訂。</span><span class="sxs-lookup"><span data-stu-id="bab56-146">Create a custom <xref:System.Windows.WeakEventManager> when an existing <xref:System.Windows.WeakEventManager> is not available and you want the best efficiency.</span></span> <span data-ttu-id="bab56-147">使用自訂的 <xref:System.Windows.WeakEventManager> 來訂閱事件將會更有效率，但在一開始就會產生更多程式碼的成本。</span><span class="sxs-lookup"><span data-stu-id="bab56-147">Using a custom <xref:System.Windows.WeakEventManager> to subscribe to an event will be more efficient, but you do incur the cost of writing more code at the beginning.</span></span>|  
|<span data-ttu-id="bab56-148">使用協力廠商弱式事件管理員</span><span class="sxs-lookup"><span data-stu-id="bab56-148">Use a third-party weak event manager</span></span>|<span data-ttu-id="bab56-149">NuGet 有[數個弱式事件管理員](https://www.nuget.org/packages?q=weak+event+manager&prerel=false)，而許多 WPF 架構也支援模式（例如，請參閱[Prism 的檔，以取得鬆散結合的事件訂](https://github.com/PrismLibrary/Prism-Documentation/blob/master/docs/wpf/legacy/Communication.md#subscribing-to-events)用帳戶）。</span><span class="sxs-lookup"><span data-stu-id="bab56-149">NuGet has [several weak event managers](https://www.nuget.org/packages?q=weak+event+manager&prerel=false) and many WPF frameworks also support the pattern (for instance, see [Prism's documentation on loosely coupled event subscription](https://github.com/PrismLibrary/Prism-Documentation/blob/master/docs/wpf/legacy/Communication.md#subscribing-to-events)).</span></span>|

 <span data-ttu-id="bab56-150">下列各節說明如何執行弱式事件模式。</span><span class="sxs-lookup"><span data-stu-id="bab56-150">The following sections describe how to implement the weak event pattern.</span></span>  <span data-ttu-id="bab56-151">基於此討論的目的，訂閱的事件具有下列特性。</span><span class="sxs-lookup"><span data-stu-id="bab56-151">For purposes of this discussion, the event to subscribe to has the following characteristics.</span></span>  
  
- <span data-ttu-id="bab56-152">事件名稱為 `SomeEvent` 。</span><span class="sxs-lookup"><span data-stu-id="bab56-152">The event name is `SomeEvent`.</span></span>  
  
- <span data-ttu-id="bab56-153">事件是由 `EventSource` 類別引發。</span><span class="sxs-lookup"><span data-stu-id="bab56-153">The event is raised by the `EventSource` class.</span></span>  
  
- <span data-ttu-id="bab56-154">事件處理常式的類型為： `SomeEventEventHandler` （或 `EventHandler<SomeEventEventArgs>` ）。</span><span class="sxs-lookup"><span data-stu-id="bab56-154">The event handler has type: `SomeEventEventHandler` (or `EventHandler<SomeEventEventArgs>`).</span></span>  
  
- <span data-ttu-id="bab56-155">事件會將類型的參數傳遞 `SomeEventEventArgs` 給事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="bab56-155">The event passes a parameter of type `SomeEventEventArgs` to the event handlers.</span></span>  
  
### <a name="using-an-existing-weak-event-manager-class"></a><span data-ttu-id="bab56-156">使用現有的弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-156">Using an Existing Weak Event Manager Class</span></span>  
  
1. <span data-ttu-id="bab56-157">尋找現有的弱式事件管理員。</span><span class="sxs-lookup"><span data-stu-id="bab56-157">Find an existing weak event manager.</span></span>  
  
     <span data-ttu-id="bab56-158">如需 WPF 隨附之弱式事件管理員的清單，請參閱類別中的繼承階層架構 <xref:System.Windows.WeakEventManager> 。</span><span class="sxs-lookup"><span data-stu-id="bab56-158">For a list of weak event managers that are included with WPF, see the inheritance hierarchy in the <xref:System.Windows.WeakEventManager> class.</span></span>  
  
2. <span data-ttu-id="bab56-159">使用新的弱式事件管理員，而不是一般事件連結。</span><span class="sxs-lookup"><span data-stu-id="bab56-159">Use the new weak event manager instead of the normal event hookup.</span></span>  
  
     <span data-ttu-id="bab56-160">例如，如果您的程式碼使用下列模式來訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="bab56-160">For example, if your code uses the following pattern to subscribe to an event:</span></span>  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     <span data-ttu-id="bab56-161">將它變更為下列模式：</span><span class="sxs-lookup"><span data-stu-id="bab56-161">Change it to the following pattern:</span></span>  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     <span data-ttu-id="bab56-162">同樣地，如果您的程式碼使用下列模式來取消訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="bab56-162">Similarly, if your code uses the following pattern to unsubscribe from an event:</span></span>  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     <span data-ttu-id="bab56-163">將它變更為下列模式：</span><span class="sxs-lookup"><span data-stu-id="bab56-163">Change it to the following pattern:</span></span>  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
### <a name="using-the-generic-weak-event-manager-class"></a><span data-ttu-id="bab56-164">使用一般弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-164">Using the Generic Weak Event Manager Class</span></span>  
  
1. <span data-ttu-id="bab56-165">使用泛型 <xref:System.Windows.WeakEventManager%602> 類別，而不是一般事件連結。</span><span class="sxs-lookup"><span data-stu-id="bab56-165">Use the generic <xref:System.Windows.WeakEventManager%602> class instead of the normal event hookup.</span></span>  
  
     <span data-ttu-id="bab56-166">當您使用 <xref:System.Windows.WeakEventManager%602> 註冊事件接聽程式時，您會提供事件來源和 <xref:System.EventArgs> 類型做為類別的型別參數，並呼叫， <xref:System.Windows.WeakEventManager%602.AddHandler%2A> 如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="bab56-166">When you use <xref:System.Windows.WeakEventManager%602> to register event listeners, you supply the event source and <xref:System.EventArgs> type as the type parameters to the class and call <xref:System.Windows.WeakEventManager%602.AddHandler%2A> as shown in the following code:</span></span>  
  
    ```csharp  
    WeakEventManager<EventSource, SomeEventEventArgs>.AddHandler(source, "SomeEvent", source_SomeEvent);  
    ```  
  
### <a name="creating-a-custom-weak-event-manager-class"></a><span data-ttu-id="bab56-167">建立自訂弱式事件管理員類別</span><span class="sxs-lookup"><span data-stu-id="bab56-167">Creating a Custom Weak Event Manager Class</span></span>  
  
1. <span data-ttu-id="bab56-168">將下列類別範本複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="bab56-168">Copy the following class template to your project.</span></span>  
  
     <span data-ttu-id="bab56-169">這個類別繼承自 <xref:System.Windows.WeakEventManager> 類別。</span><span class="sxs-lookup"><span data-stu-id="bab56-169">This class inherits from the <xref:System.Windows.WeakEventManager> class.</span></span>  
  
     [!code-csharp[WeakEvents#WeakEventManagerTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/WeakEvents/CSharp/WeakEventManagerTemplate.cs#weakeventmanagertemplate)]  
  
2. <span data-ttu-id="bab56-170">將 `SomeEventWeakEventManager` 名稱取代為您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="bab56-170">Replace the `SomeEventWeakEventManager` name with your own name.</span></span>  
  
3. <span data-ttu-id="bab56-171">將先前所述的三個名稱取代為您事件的對應名稱。</span><span class="sxs-lookup"><span data-stu-id="bab56-171">Replace the three names described previously with the corresponding names for your event.</span></span> <span data-ttu-id="bab56-172">（ `SomeEvent` 、 `EventSource` 和 `SomeEventEventArgs` ）</span><span class="sxs-lookup"><span data-stu-id="bab56-172">(`SomeEvent`, `EventSource`, and `SomeEventEventArgs`)</span></span>  
  
4. <span data-ttu-id="bab56-173">將弱式事件管理員類別的可見度（公用/內部/私用）設定為與它所管理之事件相同的可見度。</span><span class="sxs-lookup"><span data-stu-id="bab56-173">Set the visibility (public / internal / private) of the weak event manager class to the same visibility as event it manages.</span></span>  
  
5. <span data-ttu-id="bab56-174">使用新的弱式事件管理員，而不是一般事件連結。</span><span class="sxs-lookup"><span data-stu-id="bab56-174">Use the new weak event manager instead of the normal event hookup.</span></span>  
  
     <span data-ttu-id="bab56-175">例如，如果您的程式碼使用下列模式來訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="bab56-175">For example, if your code uses the following pattern to subscribe to an event:</span></span>  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     <span data-ttu-id="bab56-176">將它變更為下列模式：</span><span class="sxs-lookup"><span data-stu-id="bab56-176">Change it to the following pattern:</span></span>  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     <span data-ttu-id="bab56-177">同樣地，如果您的程式碼使用下列模式來取消訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="bab56-177">Similarly, if your code uses the following pattern to unsubscribe to an event:</span></span>  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     <span data-ttu-id="bab56-178">將它變更為下列模式：</span><span class="sxs-lookup"><span data-stu-id="bab56-178">Change it to the following pattern:</span></span>  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="bab56-179">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bab56-179">See also</span></span>

- <xref:System.Windows.WeakEventManager>
- <xref:System.Windows.IWeakEventListener>
- [<span data-ttu-id="bab56-180">路由事件概觀</span><span class="sxs-lookup"><span data-stu-id="bab56-180">Routed Events Overview</span></span>](routed-events-overview.md)
- [<span data-ttu-id="bab56-181">資料系結總覽</span><span class="sxs-lookup"><span data-stu-id="bab56-181">Data Binding Overview</span></span>](../../../desktop-wpf/data/data-binding-overview.md)

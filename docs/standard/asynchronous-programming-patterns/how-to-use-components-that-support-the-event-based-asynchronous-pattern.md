---
title: 作法：使用支援事件架構非同步模式的元件
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
ms.openlocfilehash: c41a695226068615efca5132985e50503060148b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555662"
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a><span data-ttu-id="8de93-102">作法：使用支援事件架構非同步模式的元件</span><span class="sxs-lookup"><span data-stu-id="8de93-102">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="8de93-103">許多元件可讓您選擇以非同步方式執行其工作。</span><span class="sxs-lookup"><span data-stu-id="8de93-103">Many components provide you with the option of performing their work asynchronously.</span></span> <span data-ttu-id="8de93-104">例如，<xref:System.Media.SoundPlayer> 和 <xref:System.Windows.Forms.PictureBox> 元件可讓您「在背景」載入音效和影像，同時主執行緒會繼續執行而不中斷。</span><span class="sxs-lookup"><span data-stu-id="8de93-104">The <xref:System.Media.SoundPlayer> and <xref:System.Windows.Forms.PictureBox> components, for example, enable you to load sounds and images "in the background" while your main thread continues running without interruption.</span></span>  
  
 <span data-ttu-id="8de93-105">對支援[事件架構非同步模式概觀](event-based-asynchronous-pattern-overview.md)的類別使用非同步方法，就像處理其他任何事件一樣簡單，只要將事件處理常式附加到元件的 _MethodName_**Completed** 事件即可。</span><span class="sxs-lookup"><span data-stu-id="8de93-105">Using asynchronous methods on a class that supports the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md) can be as simple as attaching an event handler to the component's _MethodName_**Completed** event, just as you would for any other event.</span></span> <span data-ttu-id="8de93-106">當您呼叫 _MethodName_**Async** 方法時，應用程式將會繼續執行而不中斷，直到引發 _MethodName_**Completed** 事件為止。</span><span class="sxs-lookup"><span data-stu-id="8de93-106">When you call the _MethodName_**Async** method, your application will continue running without interruption until the _MethodName_**Completed** event is raised.</span></span> <span data-ttu-id="8de93-107">在事件處理常式中，您可以檢查 <xref:System.ComponentModel.AsyncCompletedEventArgs> 參數來判斷非同步作業已成功完成或已取消。</span><span class="sxs-lookup"><span data-stu-id="8de93-107">In your event handler, you can examine the <xref:System.ComponentModel.AsyncCompletedEventArgs> parameter to determine if the asynchronous operation successfully completed or if it was canceled.</span></span>  
  
 <span data-ttu-id="8de93-108">如需使用事件處理常式的詳細資訊，請參閱[事件處理常式概觀](/dotnet/desktop/winforms/event-handlers-overview-windows-forms)。</span><span class="sxs-lookup"><span data-stu-id="8de93-108">For more information about using event handlers, see [Event Handlers Overview](/dotnet/desktop/winforms/event-handlers-overview-windows-forms).</span></span>  
  
 <span data-ttu-id="8de93-109">下列程序示範如何使用 <xref:System.Windows.Forms.PictureBox> 控制項的非同步影像載入功能。</span><span class="sxs-lookup"><span data-stu-id="8de93-109">The following procedure shows how to use the asynchronous image-loading capability of a <xref:System.Windows.Forms.PictureBox> control.</span></span>  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a><span data-ttu-id="8de93-110">啟用 PictureBox 控制項以非同步方式載入影像</span><span class="sxs-lookup"><span data-stu-id="8de93-110">To enable a PictureBox control to asynchronously load an image</span></span>  
  
1. <span data-ttu-id="8de93-111">建立表單中 <xref:System.Windows.Forms.PictureBox> 元件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8de93-111">Create an instance of the <xref:System.Windows.Forms.PictureBox> component in your form.</span></span>  
  
2. <span data-ttu-id="8de93-112">將事件處理常式指派給 <xref:System.Windows.Forms.PictureBox.LoadCompleted>。</span><span class="sxs-lookup"><span data-stu-id="8de93-112">Assign an event handler to the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event.</span></span>  
  
     <span data-ttu-id="8de93-113">請檢查非同步下載期間是否發生任何任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="8de93-113">Check for any errors that may have occurred during the asynchronous download here.</span></span> <span data-ttu-id="8de93-114">您也可在此時檢查取消。</span><span class="sxs-lookup"><span data-stu-id="8de93-114">This is also where you check for cancellation.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#5)]  
  
3. <span data-ttu-id="8de93-115">將稱為 `loadButton` 和 `cancelLoadButton` 的兩個按鈕加入至表單。</span><span class="sxs-lookup"><span data-stu-id="8de93-115">Add two buttons, called `loadButton` and `cancelLoadButton`, to your form.</span></span> <span data-ttu-id="8de93-116">新增 <xref:System.Windows.Forms.Control.Click> 事件處理常式，以啟動和取消下載。</span><span class="sxs-lookup"><span data-stu-id="8de93-116">Add <xref:System.Windows.Forms.Control.Click> event handlers to start and cancel the download.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#4)]  
  
4. <span data-ttu-id="8de93-117">執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8de93-117">Run your application.</span></span>  
  
     <span data-ttu-id="8de93-118">在進行影像下載時，您可以隨意移動表單、將它縮至最小以及最大化。</span><span class="sxs-lookup"><span data-stu-id="8de93-118">As the image download proceeds, you can move the form freely, minimize it, and maximize it.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8de93-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8de93-119">See also</span></span>

- [<span data-ttu-id="8de93-120">作法：在背景執行作業</span><span class="sxs-lookup"><span data-stu-id="8de93-120">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="8de93-121">事件架構非同步模式概觀</span><span class="sxs-lookup"><span data-stu-id="8de93-121">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)

---
title: Windows 總覽
description: 熟悉在 Windows Presentation Foundation （WPF）中為獨立應用程式建立和管理 windows 的基本概念。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XAML [WPF], displaying content via
- XAML pages [WPF], displaying
- content [WPF], displaying via XAML
- window objects [WPF]
- hosting [WPF], applications
- managing windows [WPF]
- dialog boxes [WPF]
- Page object [WPF]
- NavigationWindow objects [WPF]
- applications [WPF], hosting
- content [WPF], displaying
- events [WPF]
- content [WPF], displaying via procedural code
- modal windows [WPF]
- procedural code [WPF], displaying content via
- displaying content via procedural code [WPF]
- window management [WPF]
- displaying content [WPF]
- window events [WPF]
- windows [WPF]
- modal dialog boxes [WPF]
- displaying XAML pages [WPF]
ms.assetid: 737d04ec-8861-46c3-8d44-fa11d3528d23
ms.openlocfilehash: e1ad3c118fbaea8f1e23d012721f0cf3c2c50015
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622883"
---
# <a name="wpf-windows-overview"></a><span data-ttu-id="7f7c0-103">WPF 視窗概觀</span><span class="sxs-lookup"><span data-stu-id="7f7c0-103">WPF Windows Overview</span></span>
<span data-ttu-id="7f7c0-104">使用者透過 Windows 與 Windows Presentation Foundation （WPF）獨立應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-104">Users interact with Windows Presentation Foundation (WPF) standalone applications through windows.</span></span> <span data-ttu-id="7f7c0-105">視窗的主要用途是裝載內容，以視覺化方式檢視資料，並讓使用者可以與資料互動。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-105">The primary purpose of a window is to host content that visualizes data and enables users to interact with data.</span></span> <span data-ttu-id="7f7c0-106">獨立 WPF 應用程式會使用類別來提供自己的視窗 <xref:System.Windows.Window> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-106">Standalone WPF applications provide their own windows by using the <xref:System.Windows.Window> class.</span></span> <span data-ttu-id="7f7c0-107">本主題將介紹在 <xref:System.Windows.Window> 獨立應用程式中建立和管理 windows 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-107">This topic introduces <xref:System.Windows.Window> before covering the fundamentals of creating and managing windows in standalone applications.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-108">瀏覽器裝載的 WPF 應用程式，包括 XAML 瀏覽器應用程式（Xbap）和鬆散 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 分頁，並不提供自己的視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-108">Browser-hosted WPF applications, including XAML browser applications (XBAPs) and loose [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] pages, don't provide their own windows.</span></span> <span data-ttu-id="7f7c0-109">相反地，它們是裝載于 Windows Internet Explorer 所提供的 windows 中。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-109">Instead, they are hosted in windows provided by Windows Internet Explorer.</span></span> <span data-ttu-id="7f7c0-110">請參閱[WPF XAML 瀏覽器應用程式總覽](wpf-xaml-browser-applications-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-110">See [WPF XAML Browser Applications Overview](wpf-xaml-browser-applications-overview.md).</span></span>  

<a name="TheWindowClass"></a>
## <a name="the-window-class"></a><span data-ttu-id="7f7c0-111">Window 類別</span><span class="sxs-lookup"><span data-stu-id="7f7c0-111">The Window Class</span></span>  
 <span data-ttu-id="7f7c0-112">下圖說明視窗的構成部分：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-112">The following figure illustrates the constituent parts of a window:</span></span>  
  
 ![顯示視窗元素的螢幕擷取畫面。](./media/wpf-windows-overview/window-constituent-elements.png)  
  
 <span data-ttu-id="7f7c0-114">視窗分為兩個區域︰非工作區和工作區。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-114">A window is divided into two areas: the non-client area and client area.</span></span>  
  
 <span data-ttu-id="7f7c0-115">視窗的*非工作區*是由 WPF 所執行，而且包含大部分視窗通用的視窗部分，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-115">The *non-client area* of a window is implemented by WPF and includes the parts of a window that are common to most windows, including the following:</span></span>  
  
- <span data-ttu-id="7f7c0-116">框線。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-116">A border.</span></span>  
  
- <span data-ttu-id="7f7c0-117">標題列。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-117">A title bar.</span></span>  
  
- <span data-ttu-id="7f7c0-118">圖示。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-118">An icon.</span></span>  
  
- <span data-ttu-id="7f7c0-119">[最小化]、[最大化] 和 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-119">Minimize, Maximize, and Restore buttons.</span></span>  
  
- <span data-ttu-id="7f7c0-120">[關閉] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-120">A Close button.</span></span>  
  
- <span data-ttu-id="7f7c0-121">[系統] 功能表，具有允許使用者最小化、最大化、還原、移動、調整大小和關閉視窗的功能表項目。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-121">A System menu with menu items that allow users to minimize, maximize, restore, move, resize, and close a window.</span></span>  
  
 <span data-ttu-id="7f7c0-122">視窗的*工作區*是在視窗的非工作區中的區域，開發人員會使用它來新增應用程式特定的內容，例如功能表列、工具列和控制項。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-122">The *client area* of a window is the area within a window's non-client area and is used by developers to add application-specific content, such as menu bars, tool bars, and controls.</span></span>  
  
 <span data-ttu-id="7f7c0-123">在 WPF 中，視窗是由 <xref:System.Windows.Window> 您用來執行下列動作的類別所封裝：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-123">In WPF, a window is encapsulated by the <xref:System.Windows.Window> class that you use to do the following:</span></span>  
  
- <span data-ttu-id="7f7c0-124">顯示視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-124">Display a window.</span></span>  
  
- <span data-ttu-id="7f7c0-125">設定視窗的大小、位置和外觀。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-125">Configure the size, position, and appearance of a window.</span></span>  
  
- <span data-ttu-id="7f7c0-126">裝載應用程式特定內容。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-126">Host application-specific content.</span></span>  
  
- <span data-ttu-id="7f7c0-127">管理視窗的存留期。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-127">Manage the lifetime of a window.</span></span>  
  
<a name="DefiningAWindow"></a>
## <a name="implementing-a-window"></a><span data-ttu-id="7f7c0-128">實作視窗</span><span class="sxs-lookup"><span data-stu-id="7f7c0-128">Implementing a Window</span></span>  
 <span data-ttu-id="7f7c0-129">一般視窗的執行包含外觀和行為，其中的*外觀*會定義視窗外觀給使用者的方式，而*行為*會定義視窗功能與使用者互動的方式。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-129">The implementation of a typical window comprises both appearance and behavior, where *appearance* defines how a window looks to users and *behavior* defines the way a window functions as users interact with it.</span></span> <span data-ttu-id="7f7c0-130">在 WPF 中，您可以使用程式碼或標記來執行視窗的外觀和行為 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-130">In WPF, you can implement the appearance and behavior of a window using either code or [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup.</span></span>  
  
 <span data-ttu-id="7f7c0-131">不過，一般情況下，視窗的外觀會使用標記來執行 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，而且其行為會使用程式碼後置來執行，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-131">In general, however, the appearance of a window is implemented using [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup, and its behavior is implemented using code-behind, as shown in the following example.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
 <span data-ttu-id="7f7c0-132">若要讓 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記檔和程式碼後置檔案一起工作，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-132">To enable a [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup file and code-behind file to work together, the following are required:</span></span>  
  
- <span data-ttu-id="7f7c0-133">在標記中， `Window` 元素必須包含 `x:Class` 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-133">In markup, the `Window` element must include the `x:Class` attribute.</span></span> <span data-ttu-id="7f7c0-134">建立應用程式時，標記檔案中的存在 `x:Class` 會導致 Microsoft build engine （MSBuild）建立 `partial` 衍生自的類別， <xref:System.Windows.Window> 並具有屬性所指定的名稱 `x:Class` 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-134">When the application is built, the existence of `x:Class` in the markup file causes Microsoft build engine (MSBuild) to create a `partial` class that derives from <xref:System.Windows.Window> and has the name that is specified by the `x:Class` attribute.</span></span> <span data-ttu-id="7f7c0-135">這需要新增架構的 XML 命名空間宣告 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] （ `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"` ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-135">This requires the addition of an XML namespace declaration for the [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] schema ( `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"` ).</span></span> <span data-ttu-id="7f7c0-136">產生的 `partial` 類別會執行 `InitializeComponent` 方法，其會呼叫來註冊事件並設定在標記中執行的屬性。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-136">The generated `partial` class implements the `InitializeComponent` method, which is called to register the events and set the properties that are implemented in markup.</span></span>  
  
- <span data-ttu-id="7f7c0-137">在程式碼後置中，類別必須是 `partial` 具有與標記中的屬性所指定相同名稱的類別 `x:Class` ，而且必須衍生自 <xref:System.Windows.Window> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-137">In code-behind, the class must be a `partial` class with the same name that is specified by the `x:Class` attribute in markup, and it must derive from <xref:System.Windows.Window>.</span></span> <span data-ttu-id="7f7c0-138">這可讓程式碼後置檔案與 `partial` 建立應用程式時為標記檔案產生的類別相關聯（請參閱[建立 WPF 應用程式](building-a-wpf-application-wpf.md)）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-138">This allows the code-behind file to be associated with the `partial` class that is generated for the markup file when the application is built (see [Building a WPF Application](building-a-wpf-application-wpf.md)).</span></span>  
  
- <span data-ttu-id="7f7c0-139">在程式碼後置中， <xref:System.Windows.Window> 類別必須執行呼叫方法的函式 `InitializeComponent` 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-139">In code-behind, the <xref:System.Windows.Window> class must implement a constructor that calls the `InitializeComponent` method.</span></span> <span data-ttu-id="7f7c0-140">`InitializeComponent`會由標記檔案產生的 `partial` 類別來執行，以註冊事件並設定在標記中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-140">`InitializeComponent` is implemented by the markup file's generated `partial` class to register events and set properties that are defined in markup.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-141">當您使用 Visual Studio 將新的新增 <xref:System.Windows.Window> 至專案時， <xref:System.Windows.Window> 會使用標記和程式碼後置來實作為，並包含必要的設定來建立標記和程式碼後置檔案之間的關聯，如這裡所述。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-141">When you add a new <xref:System.Windows.Window> to your project by using Visual Studio, the <xref:System.Windows.Window> is implemented using both markup and code-behind, and includes the necessary configuration to create the association between the markup and code-behind files as described here.</span></span>  
  
 <span data-ttu-id="7f7c0-142">設定好此設定之後，您可以專注于在標記中定義視窗的外觀 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，並在程式碼後置中執行其行為。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-142">With this configuration in place, you can focus on defining the appearance of the window in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup and implementing its behavior in code-behind.</span></span> <span data-ttu-id="7f7c0-143">下列範例會顯示一個視窗，其中包含按鈕、在標記中實作為， [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 以及按鈕事件的事件處理常式 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> （在程式碼後置中執行）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-143">The following example shows a window with a button, implemented in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup, and an event handler for the button's <xref:System.Windows.Controls.Primitives.ButtonBase.Click> event, implemented in code-behind.</span></span>  
  
 [!code-xaml[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
<a name="ConfiguringWindowForMSBuild"></a>
## <a name="configuring-a-window-definition-for-msbuild"></a><span data-ttu-id="7f7c0-144">設定 MSBuild 的視窗定義</span><span class="sxs-lookup"><span data-stu-id="7f7c0-144">Configuring a Window Definition for MSBuild</span></span>  
 <span data-ttu-id="7f7c0-145">您在視窗中的執行方式會決定如何設定 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-145">How you implement your window determines how it is configured for MSBuild.</span></span> <span data-ttu-id="7f7c0-146">針對使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記和程式碼後置定義的視窗：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-146">For a window that is defined using both [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup and code-behind:</span></span>  
  
- <span data-ttu-id="7f7c0-147">XAML 標記檔案會設定為 MSBuild `Page` 專案。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-147">XAML markup files are configured as MSBuild `Page` items.</span></span>  
  
- <span data-ttu-id="7f7c0-148">程式碼後置檔案會設定為 MSBuild `Compile` 專案。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-148">Code-behind files are configured as MSBuild `Compile` items.</span></span>  
  
 <span data-ttu-id="7f7c0-149">這會顯示在下列 MSBuild 專案檔中。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-149">This is shown in the following MSBuild project file.</span></span>  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
    ...  
    <Page Include="MarkupAndCodeBehindWindow.xaml" />  
    <Compile Include=" MarkupAndCodeBehindWindow.xaml.cs" />  
    ...  
</Project>  
```  
  
 <span data-ttu-id="7f7c0-150">如需建立 WPF 應用程式的相關資訊，請參閱[建立 Wpf 應用程式](building-a-wpf-application-wpf.md)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-150">For information about building WPF applications, see [Building a WPF Application](building-a-wpf-application-wpf.md).</span></span>  
  
<a name="WindowLifetime"></a>
## <a name="window-lifetime"></a><span data-ttu-id="7f7c0-151">視窗存留期</span><span class="sxs-lookup"><span data-stu-id="7f7c0-151">Window Lifetime</span></span>  
 <span data-ttu-id="7f7c0-152">如同任何類別，視窗有存留期，會在它一開始具現化時開始，在那之後它會被開啟、啟動和停用，並最終關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-152">As with any class, a window has a lifetime that begins when it is first instantiated, after which it is opened, activated and deactivated, and eventually closed.</span></span>  

<a name="Opening_a_Window"></a>
### <a name="opening-a-window"></a><span data-ttu-id="7f7c0-153">開啟視窗</span><span class="sxs-lookup"><span data-stu-id="7f7c0-153">Opening a Window</span></span>  
 <span data-ttu-id="7f7c0-154">若要開啟視窗，您要先建立它的執行個體，如下列範例中示範。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-154">To open a window, you first create an instance of it, which is demonstrated in the following example.</span></span>  
  
 [!code-xaml[WindowsOverviewStartupEventSnippets#AppMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml#appmarkup)]  
  
 [!code-csharp[WindowsOverviewStartupEventSnippets#AppCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml.cs#appcodebehind)]  
  
 <span data-ttu-id="7f7c0-155">在此範例中， `MarkupAndCodeBehindWindow` 會在應用程式啟動時具現化，這會發生在 <xref:System.Windows.Application.Startup> 引發事件時。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-155">In this example, the `MarkupAndCodeBehindWindow` is instantiated when the application starts, which occurs when the <xref:System.Windows.Application.Startup> event is raised.</span></span>  
  
 <span data-ttu-id="7f7c0-156">當視窗具現化時，它的參考會自動加入至由物件管理的視窗清單 <xref:System.Windows.Application> （請參閱 <xref:System.Windows.Application.Windows%2A?displayProperty=nameWithType> ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-156">When a window is instantiated, a reference to it is automatically added to a list of windows that is managed by the <xref:System.Windows.Application> object (see <xref:System.Windows.Application.Windows%2A?displayProperty=nameWithType>).</span></span> <span data-ttu-id="7f7c0-157">此外，根據預設，第一個要具現化的視窗會設定 <xref:System.Windows.Application> 為主應用程式視窗（請參閱 <xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType> ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-157">Additionally, the first window to be instantiated is, by default, set by <xref:System.Windows.Application> as the main application window (see <xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType>).</span></span>  
  
 <span data-ttu-id="7f7c0-158">視窗最後會藉由呼叫方法來開啟，而 <xref:System.Windows.Window.Show%2A> 結果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-158">The window is finally opened by calling the <xref:System.Windows.Window.Show%2A> method; the result is shown in the following figure.</span></span>  
  
 ![藉由呼叫 Window 開啟的視窗。顯示](./media/wpf-windows-overview//window-opened-show-method.png)  
  
 <span data-ttu-id="7f7c0-160">藉由呼叫開啟的視窗 <xref:System.Windows.Window.Show%2A> 為非強制回應視窗，這表示應用程式會以可讓使用者在相同應用程式中啟用其他視窗的模式運作。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-160">A window that is opened by calling <xref:System.Windows.Window.Show%2A> is a modeless window, which means that the application operates in a mode that allows users to activate other windows in the same application.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-161"><xref:System.Windows.Window.ShowDialog%2A>呼叫來以模式開啟視窗，例如對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-161"><xref:System.Windows.Window.ShowDialog%2A> is called to open windows such as dialog boxes modally.</span></span> <span data-ttu-id="7f7c0-162">如需詳細資訊，請參閱[對話方塊總覽](dialog-boxes-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-162">See [Dialog Boxes Overview](dialog-boxes-overview.md) for more information.</span></span>  
  
 <span data-ttu-id="7f7c0-163">當 <xref:System.Windows.Window.Show%2A> 呼叫時，視窗會先執行初始化工作，然後才會顯示它，以建立可讓它接收使用者輸入的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-163">When <xref:System.Windows.Window.Show%2A> is called, a window performs initialization work before it is shown to establish infrastructure that allows it to receive user input.</span></span> <span data-ttu-id="7f7c0-164">初始化視窗時， <xref:System.Windows.Window.SourceInitialized> 會引發事件並顯示視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-164">When the window is initialized, the <xref:System.Windows.Window.SourceInitialized> event is raised and the window is shown.</span></span>  
  
 <span data-ttu-id="7f7c0-165">做為快捷方式， <xref:System.Windows.Application.StartupUri%2A> 可以設定為指定在應用程式啟動時自動開啟的第一個視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-165">As a shortcut, <xref:System.Windows.Application.StartupUri%2A> can be set to specify the first window that is opened automatically when an application starts.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#ApplicationStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/App.xaml#applicationstartupurimarkup)]  
  
 <span data-ttu-id="7f7c0-166">當應用程式啟動時，值所指定的視窗 <xref:System.Windows.Application.StartupUri%2A> 會在方式中開啟; 在內部，會藉由呼叫其方法來開啟視窗 <xref:System.Windows.Window.Show%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-166">When the application starts, the window specified by the value of <xref:System.Windows.Application.StartupUri%2A> is opened modelessly; internally, the window is opened by calling its <xref:System.Windows.Window.Show%2A> method.</span></span>  
  
<a name="Ownership"></a>
#### <a name="window-ownership"></a><span data-ttu-id="7f7c0-167">視窗擁有權</span><span class="sxs-lookup"><span data-stu-id="7f7c0-167">Window Ownership</span></span>  
 <span data-ttu-id="7f7c0-168">使用方法開啟的視窗 <xref:System.Windows.Window.Show%2A> 與建立它的視窗沒有隱含關聯性; 使用者可以與任一視窗獨立互動，這表示任一視窗都可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-168">A window that is opened by using the <xref:System.Windows.Window.Show%2A> method does not have an implicit relationship with the window that created it; users can interact with either window independently of the other, which means that either window can do the following:</span></span>  
  
- <span data-ttu-id="7f7c0-169">涵蓋另一個（除非其中一個視窗的 <xref:System.Windows.Window.Topmost%2A> 屬性設定為 `true` ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-169">Cover the other (unless one of the windows has its <xref:System.Windows.Window.Topmost%2A> property set to `true`).</span></span>  
  
- <span data-ttu-id="7f7c0-170">最小化、最大化和還原而不會影響對方。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-170">Be minimized, maximized, and restored without affecting the other.</span></span>  
  
 <span data-ttu-id="7f7c0-171">某些視窗需要與開啟它們的視窗有關聯性。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-171">Some windows require a relationship with the window that opens them.</span></span> <span data-ttu-id="7f7c0-172">例如，整合式開發環境（IDE）應用程式可能會開啟屬性視窗和工具視窗，其一般行為是涵蓋建立它們的視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-172">For example, an Integrated Development Environment (IDE) application may open property windows and tool windows whose typical behavior is to cover the window that creates them.</span></span> <span data-ttu-id="7f7c0-173">此外，這類視窗應該一律與建立它們的視窗一致地關閉、最小化、最大化和還原。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-173">Furthermore, such windows should always close, minimize, maximize, and restore in concert with the window that created them.</span></span> <span data-ttu-id="7f7c0-174">這種關聯性可以藉由*將一個視窗設為另一個*來建立，並藉由使用擁有者 <xref:System.Windows.Window.Owner%2A> *視窗*的參考來設定*擁有視窗*的屬性來達成。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-174">Such a relationship can be established by making one window *own* another, and is achieved by setting the <xref:System.Windows.Window.Owner%2A> property of the *owned window* with a reference to the *owner window*.</span></span> <span data-ttu-id="7f7c0-175">下列範例會顯示這一點。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-175">This is shown in the following example.</span></span>  
  
 [!code-csharp[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/CSharp/MainWindow.xaml.cs#setwindowownercode)]
 [!code-vb[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/visualbasic/mainwindow.xaml.vb#setwindowownercode)]  
  
 <span data-ttu-id="7f7c0-176">建立擁有權之後︰</span><span class="sxs-lookup"><span data-stu-id="7f7c0-176">After ownership is established:</span></span>  
  
- <span data-ttu-id="7f7c0-177">擁有的視窗可以藉由檢查其屬性的值來參考其擁有者視窗 <xref:System.Windows.Window.Owner%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-177">The owned window can reference its owner window by inspecting the value of its <xref:System.Windows.Window.Owner%2A> property.</span></span>  
  
- <span data-ttu-id="7f7c0-178">[擁有者] 視窗可以藉由檢查其屬性的值，來探索所有 windows it 擁有的內容 <xref:System.Windows.Window.OwnedWindows%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-178">The owner window can discover all the windows it owns by inspecting the value of its <xref:System.Windows.Window.OwnedWindows%2A> property.</span></span>  
  
<a name="Preventing"></a>
#### <a name="preventing-window-activation"></a><span data-ttu-id="7f7c0-179">避免視窗啟動</span><span class="sxs-lookup"><span data-stu-id="7f7c0-179">Preventing Window Activation</span></span>  
 <span data-ttu-id="7f7c0-180">在某些情況下，windows 不應在顯示時啟動，例如網際網路 messenger 樣式應用程式的交談視窗或電子郵件應用程式的通知視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-180">There are scenarios where windows should not be activated when shown, such as conversation windows of an Internet messenger-style application or notification windows of an email application.</span></span>  
  
 <span data-ttu-id="7f7c0-181">如果您的應用程式具有不應在顯示時啟動的視窗，您可以在 <xref:System.Windows.Window.ShowActivated%2A> `false` <xref:System.Windows.Window.Show%2A> 第一次呼叫方法之前，將其屬性設定為。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-181">If your application has a window that shouldn't be activated when shown, you can set its <xref:System.Windows.Window.ShowActivated%2A> property to `false` before calling the <xref:System.Windows.Window.Show%2A> method for the first time.</span></span> <span data-ttu-id="7f7c0-182">因此：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-182">As a consequence:</span></span>  
  
- <span data-ttu-id="7f7c0-183">未啟動視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-183">The window is not activated.</span></span>  
  
- <span data-ttu-id="7f7c0-184">視窗的 <xref:System.Windows.Window.Activated> 事件不會引發。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-184">The window's <xref:System.Windows.Window.Activated> event is not raised.</span></span>  
  
- <span data-ttu-id="7f7c0-185">目前已啟動的視窗會保持已啟動。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-185">The currently activated window remains activated.</span></span>  
  
 <span data-ttu-id="7f7c0-186">不過，當使用者按一下工作區或非工作區來啟動它時，視窗將會啟動。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-186">The window will become activated, however, as soon as the user activates it by clicking either the client or non-client area.</span></span> <span data-ttu-id="7f7c0-187">在此案例中：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-187">In this case:</span></span>  
  
- <span data-ttu-id="7f7c0-188">視窗已啟動。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-188">The window is activated.</span></span>  
  
- <span data-ttu-id="7f7c0-189"><xref:System.Windows.Window.Activated>會引發視窗的事件。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-189">The window's <xref:System.Windows.Window.Activated> event is raised.</span></span>  
  
- <span data-ttu-id="7f7c0-190">先前已啟動的視窗已停用。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-190">The previously activated window is deactivated.</span></span>  
  
- <span data-ttu-id="7f7c0-191">接著，視窗的 <xref:System.Windows.Window.Deactivated> 和 <xref:System.Windows.Window.Activated> 事件會如預期般引發，以回應使用者動作。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-191">The window's <xref:System.Windows.Window.Deactivated> and <xref:System.Windows.Window.Activated> events are subsequently raised as expected in response to user actions.</span></span>  
  
<a name="Window_Activation"></a>
### <a name="window-activation"></a><span data-ttu-id="7f7c0-192">視窗啟動</span><span class="sxs-lookup"><span data-stu-id="7f7c0-192">Window Activation</span></span>  
 <span data-ttu-id="7f7c0-193">當視窗第一次開啟時，它會變成作用中的視窗（除非它是以 <xref:System.Windows.Window.ShowActivated%2A> 設定為的顯示 `false` ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-193">When a window is first opened, it becomes the active window (unless it is shown with <xref:System.Windows.Window.ShowActivated%2A> set to `false`).</span></span> <span data-ttu-id="7f7c0-194">*使用中視窗*是目前正在捕捉使用者輸入的視窗，例如按鍵筆劃和滑鼠點擊。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-194">The *active window* is the window that is currently capturing user input, such as key strokes and mouse clicks.</span></span> <span data-ttu-id="7f7c0-195">當視窗變成作用中狀態時，它會引發 <xref:System.Windows.Window.Activated> 事件。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-195">When a window becomes active, it raises the <xref:System.Windows.Window.Activated> event.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-196">當第一次開啟視窗時， <xref:System.Windows.FrameworkElement.Loaded> <xref:System.Windows.Window.ContentRendered> 只有在引發事件之後，才會引發和事件 <xref:System.Windows.Window.Activated> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-196">When a window is first opened, the <xref:System.Windows.FrameworkElement.Loaded> and <xref:System.Windows.Window.ContentRendered> events are raised only after the <xref:System.Windows.Window.Activated> event is raised.</span></span> <span data-ttu-id="7f7c0-197">記住這一點之後，當引發時，可以有效地將視窗視為 <xref:System.Windows.Window.ContentRendered> 已開啟。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-197">With this in mind, a window can effectively be considered opened when <xref:System.Windows.Window.ContentRendered> is raised.</span></span>  
  
 <span data-ttu-id="7f7c0-198">視窗成為使用中之後，使用者可以在相同應用程式中啟動另一個視窗，或啟動另一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-198">After a window becomes active, a user can activate another window in the same application, or activate another application.</span></span> <span data-ttu-id="7f7c0-199">發生這種情況時，目前作用中的視窗會變成停用狀態，並引發 <xref:System.Windows.Window.Deactivated> 事件。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-199">When that happens, the currently active window becomes deactivated and raises the <xref:System.Windows.Window.Deactivated> event.</span></span> <span data-ttu-id="7f7c0-200">同樣地，當使用者選取目前已停用的視窗時，視窗會再次變成使用中狀態，並 <xref:System.Windows.Window.Activated> 引發。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-200">Likewise, when the user selects a currently deactivated window, the window becomes active again and <xref:System.Windows.Window.Activated> is raised.</span></span>  
  
 <span data-ttu-id="7f7c0-201">處理和的其中一個常見原因 <xref:System.Windows.Window.Activated> <xref:System.Windows.Window.Deactivated> 是啟用和停用只有在視窗作用中時才可執行檔功能。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-201">One common reason to handle <xref:System.Windows.Window.Activated> and <xref:System.Windows.Window.Deactivated> is to enable and disable functionality that can only run when a window is active.</span></span> <span data-ttu-id="7f7c0-202">例如，某些視窗顯示需要使用者持續輸入和注意的互動式內容，包括遊戲和視訊播放程式。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-202">For example, some windows display interactive content that requires constant user input or attention, including games and video players.</span></span> <span data-ttu-id="7f7c0-203">下列範例是簡化的影片播放程式，示範如何處理 <xref:System.Windows.Window.Activated> 及 <xref:System.Windows.Window.Deactivated> 執行此行為。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-203">The following example is a simplified video player that demonstrates how to handle <xref:System.Windows.Window.Activated> and <xref:System.Windows.Window.Deactivated> to implement this behavior.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#ActivationDeactivationMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml#activationdeactivationmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml.cs#activationdeactivationcodebehind)]
 [!code-vb[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/CustomMediaPlayerWindow.xaml.vb#activationdeactivationcodebehind)]  
  
 <span data-ttu-id="7f7c0-204">當視窗已停用時，其他應用程式類型仍然可能會在背景中執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-204">Other types of applications may still run code in the background when a window is deactivated.</span></span> <span data-ttu-id="7f7c0-205">例如，當使用者使用其他應用程式時，郵件用戶端可能會繼續輪詢郵件伺服器。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-205">For example, a mail client may continue polling the mail server while the user is using other applications.</span></span> <span data-ttu-id="7f7c0-206">這類應用程式在主視窗已停用時，通常會提供不同或其他行為。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-206">Applications like these often provide different or additional behavior while the main window is deactivated.</span></span> <span data-ttu-id="7f7c0-207">對於郵件程式，這可能表示同時將新的郵件項目加入收件匣，並將通知圖示加入系統匣。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-207">With respect to the mail program, this may mean both adding the new mail item to the inbox and adding a notification icon to the system tray.</span></span> <span data-ttu-id="7f7c0-208">只有當 [郵件] 視窗不在使用中時，才需要顯示通知圖示，這可以藉由檢查屬性來判斷 <xref:System.Windows.Window.IsActive%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-208">A notification icon need only be displayed when the mail window isn't active, which can be determined by inspecting the <xref:System.Windows.Window.IsActive%2A> property.</span></span>  
  
 <span data-ttu-id="7f7c0-209">如果背景工作完成，視窗可能會想要藉由呼叫方法，更迫切地通知使用者 <xref:System.Windows.Window.Activate%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-209">If a background task completes, a window may want to notify the user more urgently by calling <xref:System.Windows.Window.Activate%2A> method.</span></span> <span data-ttu-id="7f7c0-210">如果使用者與呼叫時啟動的另一個應用程式互動 <xref:System.Windows.Window.Activate%2A> ，視窗的工作列按鈕會閃爍。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-210">If the user is interacting with another application activated when <xref:System.Windows.Window.Activate%2A> is called, the window's taskbar button flashes.</span></span> <span data-ttu-id="7f7c0-211">如果使用者與目前的應用程式互動，則呼叫 <xref:System.Windows.Window.Activate%2A> 會將視窗帶到前景。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-211">If a user is interacting with the current application, calling <xref:System.Windows.Window.Activate%2A> will bring the window to the foreground.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-212">您可以使用和事件來處理應用程式範圍啟用 <xref:System.Windows.Application.Activated?displayProperty=nameWithType> <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-212">You can handle application-scope activation using the <xref:System.Windows.Application.Activated?displayProperty=nameWithType> and <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> events.</span></span>  
  
<a name="Closing_a_Window"></a>
### <a name="closing-a-window"></a><span data-ttu-id="7f7c0-213">關閉視窗</span><span class="sxs-lookup"><span data-stu-id="7f7c0-213">Closing a Window</span></span>  
 <span data-ttu-id="7f7c0-214">視窗的存留期在使用者關閉它時開始進入尾聲。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-214">The life of a window starts coming to an end when a user closes it.</span></span> <span data-ttu-id="7f7c0-215">視窗可以使用非工作區中的項目關閉，包括下列項目︰</span><span class="sxs-lookup"><span data-stu-id="7f7c0-215">A window can be closed by using elements in the non-client area, including the following:</span></span>  
  
- <span data-ttu-id="7f7c0-216">[**系統**] 功能表的**關閉**專案。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-216">The **Close** item of the **System** menu.</span></span>  
  
- <span data-ttu-id="7f7c0-217">按下 ALT+F4。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-217">Pressing ALT+F4.</span></span>  
  
- <span data-ttu-id="7f7c0-218">按下 [**關閉**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-218">Pressing the **Close** button.</span></span>  
  
 <span data-ttu-id="7f7c0-219">您可以提供其他機制讓工作區關閉視窗，較常見的包括下列各項︰</span><span class="sxs-lookup"><span data-stu-id="7f7c0-219">You can provide additional mechanisms to the client area to close a window, the more common of which include the following:</span></span>  
  
- <span data-ttu-id="7f7c0-220">[檔案] 功能表**中的 [結束] 專案，** **通常是針對**主應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-220">An **Exit** item in the **File** menu, typically for main application windows.</span></span>  
  
- <span data-ttu-id="7f7c0-221">[檔案] 功能表中**的 [** **關閉**] 專案，通常是在次要應用程式視窗上。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-221">A **Close** item in the **File** menu, typically on a secondary application window.</span></span>  
  
- <span data-ttu-id="7f7c0-222">[**取消**] 按鈕，通常是在強制回應對話方塊上。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-222">A **Cancel** button, typically on a modal dialog box.</span></span>  
  
- <span data-ttu-id="7f7c0-223">[**關閉**] 按鈕，通常是在非強制回應對話方塊上。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-223">A **Close** button, typically on a modeless dialog box.</span></span>  
  
 <span data-ttu-id="7f7c0-224">若要關閉視窗以回應其中一個自訂機制，您必須呼叫 <xref:System.Windows.Window.Close%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-224">To close a window in response to one of these custom mechanisms, you need to call the <xref:System.Windows.Window.Close%2A> method.</span></span> <span data-ttu-id="7f7c0-225">下列範例會藉由**選擇 [檔案] 功能表上的**[結束]，來執行關閉**視窗的功能**。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-225">The following example implements the ability to close a window by choosing the **Exit** on the **File** menu.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#WindowWithFileExitMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml#windowwithfileexitmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml.cs#windowwithfileexitcodebehind)]
 [!code-vb[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/WindowWithFileExit.xaml.vb#windowwithfileexitcodebehind)]  
  
 <span data-ttu-id="7f7c0-226">當視窗關閉時，它會引發兩個事件： <xref:System.Windows.Window.Closing> 和 <xref:System.Windows.Window.Closed> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-226">When a window closes, it raises two events: <xref:System.Windows.Window.Closing> and <xref:System.Windows.Window.Closed>.</span></span>  
  
 <span data-ttu-id="7f7c0-227"><xref:System.Windows.Window.Closing>會在視窗關閉之前引發，而且它會提供一種機制，讓您可以防止視窗關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-227"><xref:System.Windows.Window.Closing> is raised before the window closes, and it provides a mechanism by which window closure can be prevented.</span></span> <span data-ttu-id="7f7c0-228">防止視窗關閉的一個常見原因，是視窗內容包含已修改的資料。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-228">One common reason to prevent window closure is if window content contains modified data.</span></span> <span data-ttu-id="7f7c0-229">在此情況下， <xref:System.Windows.Window.Closing> 可以處理事件以判斷資料是否已變更，如果是，則要求使用者是否要繼續關閉視窗而不儲存資料，或取消視窗關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-229">In this situation, the <xref:System.Windows.Window.Closing> event can be handled to determine whether data is dirty and, if so, to ask the user whether to either continue closing the window without saving the data or to cancel window closure.</span></span> <span data-ttu-id="7f7c0-230">下列範例顯示處理的重要層面 <xref:System.Windows.Window.Closing> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-230">The following example shows the key aspects of handling <xref:System.Windows.Window.Closing>.</span></span>  
  
 [!code-csharp[WindowClosingSnippets](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowClosingSnippets/CSharp/DataWindow.xaml.cs)]
 [!code-vb[WindowClosingSnippets](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowClosingSnippets/visualbasic/datawindow.xaml.vb)]  

 <span data-ttu-id="7f7c0-231"><xref:System.Windows.Window.Closing>事件處理常式會傳遞 <xref:System.ComponentModel.CancelEventArgs> ，它會執行 `Boolean` <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 您設定為的屬性， `true` 以防止關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-231">The <xref:System.Windows.Window.Closing> event handler is passed a <xref:System.ComponentModel.CancelEventArgs>, which implements the `Boolean`<xref:System.ComponentModel.CancelEventArgs.Cancel%2A> property that you set to `true` to prevent a window from closing.</span></span>  
  
 <span data-ttu-id="7f7c0-232">如果 <xref:System.Windows.Window.Closing> 未處理，或已處理但未取消，視窗將會關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-232">If <xref:System.Windows.Window.Closing> is not handled, or it is handled but not canceled, the window will close.</span></span> <span data-ttu-id="7f7c0-233">在視窗實際關閉之前， <xref:System.Windows.Window.Closed> 會引發。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-233">Just before a window actually closes, <xref:System.Windows.Window.Closed> is raised.</span></span> <span data-ttu-id="7f7c0-234">此時無法防止視窗關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-234">At this point, a window cannot be prevented from closing.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-235">應用程式可以設定為在主應用程式視窗關閉時自動關閉（請參閱 <xref:System.Windows.Application.MainWindow%2A> ），或最後一個視窗關閉。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-235">An application can be configured to shut down automatically when either the main application window closes (see <xref:System.Windows.Application.MainWindow%2A>) or the last window closes.</span></span> <span data-ttu-id="7f7c0-236">如需詳細資訊，請參閱<xref:System.Windows.Application.ShutdownMode%2A>。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-236">For details, see <xref:System.Windows.Application.ShutdownMode%2A>.</span></span>  
  
 <span data-ttu-id="7f7c0-237">雖然可以透過非用戶端和用戶端區域中提供的機制明確地關閉視窗，但也可以在應用程式或視窗的其他部分中，以隱含方式關閉視窗，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-237">While a window can be explicitly closed through mechanisms provided in the non-client and client areas, a window can also be implicitly closed as a result of behavior in other parts of the application or Windows, including the following:</span></span>  
  
- <span data-ttu-id="7f7c0-238">使用者登出或關閉 Windows。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-238">A user logs off or shuts down Windows.</span></span>  
  
- <span data-ttu-id="7f7c0-239">視窗的擁有者會關閉（請參閱 <xref:System.Windows.Window.Owner%2A> ）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-239">A window's owner closes (see <xref:System.Windows.Window.Owner%2A>).</span></span>  
  
- <span data-ttu-id="7f7c0-240">主應用程式視窗已關閉，且 <xref:System.Windows.Application.ShutdownMode%2A> 為 <xref:System.Windows.ShutdownMode.OnMainWindowClose> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-240">The main application window is closed and <xref:System.Windows.Application.ShutdownMode%2A> is <xref:System.Windows.ShutdownMode.OnMainWindowClose>.</span></span>  
  
- <span data-ttu-id="7f7c0-241">呼叫 <xref:System.Windows.Application.Shutdown%2A>。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-241"><xref:System.Windows.Application.Shutdown%2A> is called.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-242">在關閉之後就無法重新開啟視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-242">A window cannot be reopened after it is closed.</span></span>  
  
<a name="Window_Lifetime_Events"></a>
### <a name="window-lifetime-events"></a><span data-ttu-id="7f7c0-243">視窗存留期事件</span><span class="sxs-lookup"><span data-stu-id="7f7c0-243">Window Lifetime Events</span></span>  
 <span data-ttu-id="7f7c0-244">下圖顯示主事件在視窗存留期間的順序：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-244">The following illustration shows the sequence of the principal events in the lifetime of a window:</span></span>  
  
 ![在視窗的存留期內顯示事件的圖表。](./media/wpf-windows-overview/window-lifetime-events.png)  
  
 <span data-ttu-id="7f7c0-246">下圖顯示在未啟用的視窗存留期間內，主體事件的順序（在 <xref:System.Windows.Window.ShowActivated%2A> `false` 顯示視窗之前設定為）：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-246">The following illustration shows the sequence of the principal events in the lifetime of a window that is shown without activation (<xref:System.Windows.Window.ShowActivated%2A> is set to `false` before the window is shown):</span></span>  
  
 ![在不啟用的情況下，于視窗存留期間顯示事件的圖表。](./media/wpf-windows-overview/window-lifetime-no-activation.png)  
  
<a name="WindowLocation"></a>
## <a name="window-location"></a><span data-ttu-id="7f7c0-248">視窗位置</span><span class="sxs-lookup"><span data-stu-id="7f7c0-248">Window Location</span></span>  
 <span data-ttu-id="7f7c0-249">視窗開啟時，它會有相對於桌面的 x 和 y 維度位置。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-249">While a window is open, it has a location in the x and y dimensions relative to the desktop.</span></span> <span data-ttu-id="7f7c0-250">您可以分別檢查和屬性來判斷這個位置 <xref:System.Windows.Window.Left%2A> <xref:System.Windows.Window.Top%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-250">This location can be determined by inspecting the <xref:System.Windows.Window.Left%2A> and <xref:System.Windows.Window.Top%2A> properties, respectively.</span></span> <span data-ttu-id="7f7c0-251">您可以設定這些屬性，以變更視窗的位置。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-251">You can set these properties to change the location of the window.</span></span>  
  
 <span data-ttu-id="7f7c0-252">您也可以 <xref:System.Windows.Window> <xref:System.Windows.Window.WindowStartupLocation%2A> 使用下列其中一個列舉值來設定屬性，以指定第一次出現時的初始位置 <xref:System.Windows.WindowStartupLocation> ：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-252">You can also specify the initial location of a <xref:System.Windows.Window> when it first appears by setting the <xref:System.Windows.Window.WindowStartupLocation%2A> property with one of the following <xref:System.Windows.WindowStartupLocation> enumeration values:</span></span>  
  
- <span data-ttu-id="7f7c0-253"><xref:System.Windows.WindowStartupLocation.CenterOwner> (預設)</span><span class="sxs-lookup"><span data-stu-id="7f7c0-253"><xref:System.Windows.WindowStartupLocation.CenterOwner> (default)</span></span>  
  
- <xref:System.Windows.WindowStartupLocation.CenterScreen>  
  
- <xref:System.Windows.WindowStartupLocation.Manual>  
  
 <span data-ttu-id="7f7c0-254">如果將啟動位置指定為 <xref:System.Windows.WindowStartupLocation.Manual> ，而且 <xref:System.Windows.Window.Left%2A> <xref:System.Windows.Window.Top%2A> 尚未設定和屬性， <xref:System.Windows.Window> 將會要求 Windows 位置出現在中。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-254">If the startup location is specified as <xref:System.Windows.WindowStartupLocation.Manual>, and the <xref:System.Windows.Window.Left%2A> and <xref:System.Windows.Window.Top%2A> properties have not been set, <xref:System.Windows.Window> will ask Windows for a location to appear in.</span></span>  
  
<a name="Topmost_Windows_and_Z_Order"></a>
### <a name="topmost-windows-and-z-order"></a><span data-ttu-id="7f7c0-255">最上層視窗和疊置順序</span><span class="sxs-lookup"><span data-stu-id="7f7c0-255">Topmost Windows and Z-Order</span></span>  
 <span data-ttu-id="7f7c0-256">除了有 x 和 y 位置，視窗也有 z 維度的位置，這決定了它相對於其他視窗的垂直位置。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-256">Besides having an x and y location, a window also has a location in the z dimension, which determines its vertical position with respect to other windows.</span></span> <span data-ttu-id="7f7c0-257">這稱為視窗的疊置順序，並且有兩種類型︰一般疊置順序和最上層疊置順序。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-257">This is known as the window's z-order, and there are two types: normal z-order and topmost z-order.</span></span> <span data-ttu-id="7f7c0-258">視窗在一般迭置*順序*中的位置取決於它目前是否在作用中。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-258">The location of a window in the *normal z-order* is determined by whether it is currently active or not.</span></span> <span data-ttu-id="7f7c0-259">根據預設，視窗位於一般疊置順序。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-259">By default, a window is located in the normal z-order.</span></span> <span data-ttu-id="7f7c0-260">視窗在*最上層*的迭置順序中的位置也取決於目前是否為使用中狀態。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-260">The location of a window in the *topmost z-order* is also determined by whether it is currently active or not.</span></span> <span data-ttu-id="7f7c0-261">此外，最上層疊置順序的視窗一定會位於一般疊置順序的視窗之上。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-261">Furthermore, windows in the topmost z-order are always located above windows in the normal z-order.</span></span> <span data-ttu-id="7f7c0-262">視窗是以最上層的迭置順序，將其 <xref:System.Windows.Window.Topmost%2A> 屬性設定為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-262">A window is located in the topmost z-order by setting its <xref:System.Windows.Window.Topmost%2A> property to `true`.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#TopmostWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TopmostWindow.xaml#topmostwindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-263">在每個疊置順序內，目前使用中視窗會顯示在相同疊置順序中的所有其他視窗之上。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-263">Within each z-order, the currently active window appears above all other windows in the same z-order.</span></span>  
  
<a name="WindowSize"></a>
## <a name="window-size"></a><span data-ttu-id="7f7c0-264">視窗大小</span><span class="sxs-lookup"><span data-stu-id="7f7c0-264">Window Size</span></span>  
 <span data-ttu-id="7f7c0-265">除了擁有桌面位置，視窗的大小是由數個屬性所決定，包括各種寬度和高度屬性和 <xref:System.Windows.Window.SizeToContent%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-265">Besides having a desktop location, a window has a size that is determined by several properties, including the various width and height properties and <xref:System.Windows.Window.SizeToContent%2A>.</span></span>  
  
 <span data-ttu-id="7f7c0-266"><xref:System.Windows.FrameworkElement.MinWidth%2A>、 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 是用來管理視窗在其存留期內可以有的寬度範圍，如下列範例所示設定。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-266"><xref:System.Windows.FrameworkElement.MinWidth%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, and <xref:System.Windows.FrameworkElement.MaxWidth%2A> are used to manage the range of widths that a window can have during its lifetime, and are configured as shown in the following example.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#WidthWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WidthWindow.xaml#widthwindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-267">視窗高度是由 <xref:System.Windows.FrameworkElement.MinHeight%2A> 、和所管理 <xref:System.Windows.FrameworkElement.Height%2A> <xref:System.Windows.FrameworkElement.MaxHeight%2A> ，而且會設定為，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-267">Window height is managed by <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.Height%2A>, and <xref:System.Windows.FrameworkElement.MaxHeight%2A>, and are configured as shown in the following example.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#HeightWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/HeightWindow.xaml#heightwindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-268">因為各種寬度值和高度值都各指定一個範圍，所以可調整大小視窗的高度與寬度可能會是個別維度的指定範圍內的任何位置。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-268">Because the various width values and height values each specify a range, it is possible for the width and height of a resizable window to be anywhere within the specified range for the respective dimension.</span></span> <span data-ttu-id="7f7c0-269">若要偵測其目前的寬度和高度，請 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 分別檢查和 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-269">To detect its current width and height, inspect <xref:System.Windows.FrameworkElement.ActualWidth%2A> and <xref:System.Windows.FrameworkElement.ActualHeight%2A>, respectively.</span></span>  
  
 <span data-ttu-id="7f7c0-270">如果您想要讓視窗的寬度和高度符合視窗內容的大小，您可以使用 <xref:System.Windows.Window.SizeToContent%2A> 屬性，其具有下列值：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-270">If you'd like the width and height of your window to have a size that fits to the size of the window's content, you can use the <xref:System.Windows.Window.SizeToContent%2A> property, which has the following values:</span></span>  
  
- <span data-ttu-id="7f7c0-271"><xref:System.Windows.SizeToContent.Manual>.</span><span class="sxs-lookup"><span data-stu-id="7f7c0-271"><xref:System.Windows.SizeToContent.Manual>.</span></span> <span data-ttu-id="7f7c0-272">無效果 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-272">No effect (default).</span></span>  
  
- <span data-ttu-id="7f7c0-273"><xref:System.Windows.SizeToContent.Width>.</span><span class="sxs-lookup"><span data-stu-id="7f7c0-273"><xref:System.Windows.SizeToContent.Width>.</span></span> <span data-ttu-id="7f7c0-274">符合內容寬度，其效果與將 <xref:System.Windows.FrameworkElement.MinWidth%2A> 和設定 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 為內容的寬度相同。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-274">Fit to content width, which has the same effect as setting both <xref:System.Windows.FrameworkElement.MinWidth%2A> and <xref:System.Windows.FrameworkElement.MaxWidth%2A> to the width of the content.</span></span>  
  
- <span data-ttu-id="7f7c0-275"><xref:System.Windows.SizeToContent.Height>.</span><span class="sxs-lookup"><span data-stu-id="7f7c0-275"><xref:System.Windows.SizeToContent.Height>.</span></span> <span data-ttu-id="7f7c0-276">符合內容高度，其效果等同于將 <xref:System.Windows.FrameworkElement.MinHeight%2A> 和設定 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 為內容的高度。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-276">Fit to content height, which has the same effect as setting both <xref:System.Windows.FrameworkElement.MinHeight%2A> and <xref:System.Windows.FrameworkElement.MaxHeight%2A> to the height of the content.</span></span>  
  
- <span data-ttu-id="7f7c0-277"><xref:System.Windows.SizeToContent.WidthAndHeight>.</span><span class="sxs-lookup"><span data-stu-id="7f7c0-277"><xref:System.Windows.SizeToContent.WidthAndHeight>.</span></span> <span data-ttu-id="7f7c0-278">符合內容寬度和高度，其效果與將和設定為內容的 <xref:System.Windows.FrameworkElement.MinHeight%2A> <xref:System.Windows.FrameworkElement.MaxHeight%2A> 高度相同，並同時將 <xref:System.Windows.FrameworkElement.MinWidth%2A> 和設定 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 為內容的寬度。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-278">Fit to content width and height, which has the same effect as setting both <xref:System.Windows.FrameworkElement.MinHeight%2A> and <xref:System.Windows.FrameworkElement.MaxHeight%2A> to the height of the content, and setting both <xref:System.Windows.FrameworkElement.MinWidth%2A> and <xref:System.Windows.FrameworkElement.MaxWidth%2A> to the width of the content.</span></span>  
  
 <span data-ttu-id="7f7c0-279">下列範例顯示自動調整垂直和水平大小以符合其內容的視窗，第一次顯示時的樣子。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-279">The following example shows a window that automatically sizes to fit its content, both vertically and horizontally, when first shown.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#SizeToContentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/SizeToContentWindow.xaml#sizetocontentwindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-280">下列範例示範如何 <xref:System.Windows.Window.SizeToContent%2A> 在程式碼中設定屬性，以指定視窗的調整大小以符合其內容。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-280">The following example shows how to set the <xref:System.Windows.Window.SizeToContent%2A> property in code to specify how a window resizes to fit its content    .</span></span>
  
 [!code-csharp[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#setwindowsizetocontentpropertycode)]
 [!code-vb[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#setwindowsizetocontentpropertycode)]  
  
<a name="OrderOfPrecedence"></a>
## <a name="order-of-precedence-for-sizing-properties"></a><span data-ttu-id="7f7c0-281">調整大小屬性優先順序</span><span class="sxs-lookup"><span data-stu-id="7f7c0-281">Order of Precedence for Sizing Properties</span></span>  
 <span data-ttu-id="7f7c0-282">基本上，視窗的各種大小屬性會合併起來定義可調整大小的視窗的寬度和高度範圍。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-282">Essentially, the various sizes properties of a window combine to define the range of width and height for a resizable window.</span></span> <span data-ttu-id="7f7c0-283">為確保維持有效的範圍，會 <xref:System.Windows.Window> 使用下列優先順序來評估大小屬性的值。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-283">To ensure a valid range is maintained, <xref:System.Windows.Window> evaluates the values of the size properties using the following orders of precedence.</span></span>  
  
 <span data-ttu-id="7f7c0-284">**針對高度屬性：**</span><span class="sxs-lookup"><span data-stu-id="7f7c0-284">**For Height Properties:**</span></span>  
  
1. <xref:System.Windows.FrameworkElement.MinHeight%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxHeight%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Height?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Height%2A?displayProperty=nameWithType>  
  
 <span data-ttu-id="7f7c0-285">**針對寬度屬性：**</span><span class="sxs-lookup"><span data-stu-id="7f7c0-285">**For Width Properties:**</span></span>  
  
1. <xref:System.Windows.FrameworkElement.MinWidth%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxWidth%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Width?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Width%2A?displayProperty=nameWithType>  
  
 <span data-ttu-id="7f7c0-286">優先順序也可以決定視窗最大化時的大小，而這是使用屬性來管理 <xref:System.Windows.Window.WindowState%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-286">The order of precedence can also determine the size of a window when it is maximized, which is managed with the <xref:System.Windows.Window.WindowState%2A> property.</span></span>  
  
<a name="WindowState"></a>
## <a name="window-state"></a><span data-ttu-id="7f7c0-287">視窗狀態</span><span class="sxs-lookup"><span data-stu-id="7f7c0-287">Window State</span></span>  
 <span data-ttu-id="7f7c0-288">在可調整大小的視窗存留期中，它可以有三種狀態︰標準、最小化及最大化。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-288">During the lifetime of a resizable window, it can have three states: normal, minimized, and maximized.</span></span> <span data-ttu-id="7f7c0-289">具有*正常*狀態的視窗是視窗的預設狀態。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-289">A window with a *normal* state is the default state of a window.</span></span> <span data-ttu-id="7f7c0-290">這種狀態的視窗可以讓使用者移動並使用調整大小底框或框線調整其大小，如果它可調整大小。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-290">A window with this state allows a user to move and resize it by using a resize grip or the border, if it is resizable.</span></span>  
  
 <span data-ttu-id="7f7c0-291">如果設定為，則具有*最小化*狀態的視窗會折迭至其工作列按鈕，否則會折迭 <xref:System.Windows.Window.ShowInTaskbar%2A> `true` 為最小的可能大小，並將其本身重新放置到桌面的左下角。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-291">A window with a *minimized* state collapses to its task bar button if <xref:System.Windows.Window.ShowInTaskbar%2A> is set to `true`; otherwise, it collapses to the smallest possible size it can be and relocates itself to the bottom-left corner of the desktop.</span></span> <span data-ttu-id="7f7c0-292">最小化視窗的類型都無法使用框線或調整大小底框來調整大小，雖然未顯示在工作列中的最小化視窗可以在桌面拖曳。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-292">Neither type of minimized window can be resized using a border or resize grip, although a minimized window that isn't shown in the task bar can be dragged around the desktop.</span></span>  
  
 <span data-ttu-id="7f7c0-293">具有*最大化*狀態的視窗會展開為它可以達到的最大大小，而這只會與其 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 、 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 和屬性所指定的大小一樣大 <xref:System.Windows.Window.SizeToContent%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-293">A window with a *maximized* state expands to the maximum size it can be, which will only be as large as its <xref:System.Windows.FrameworkElement.MaxWidth%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A>, and <xref:System.Windows.Window.SizeToContent%2A> properties dictate.</span></span> <span data-ttu-id="7f7c0-294">就像最小化的視窗，最大化的視窗無法使用調整大小底框或藉由拖曳框線來調整大小。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-294">Like a minimized window, a maximized window cannot be resized by using a resize grip or by dragging the border.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7f7c0-295"><xref:System.Windows.Window.Top%2A>視窗的、 <xref:System.Windows.Window.Left%2A> 、 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 屬性值一律代表正常狀態的值，即使視窗目前已最大化或最小化。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-295">The values of the <xref:System.Windows.Window.Top%2A>, <xref:System.Windows.Window.Left%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, and <xref:System.Windows.FrameworkElement.Height%2A> properties of a window always represent the values for the normal state, even when the window is currently maximized or minimized.</span></span>  
  
 <span data-ttu-id="7f7c0-296">視窗的狀態可以藉由設定其屬性來設定 <xref:System.Windows.Window.WindowState%2A> ，它可以有下列其中一個 <xref:System.Windows.WindowState> 列舉值：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-296">The state of a window can be configured by setting its <xref:System.Windows.Window.WindowState%2A> property, which can have one of the following <xref:System.Windows.WindowState> enumeration values:</span></span>  
  
- <span data-ttu-id="7f7c0-297"><xref:System.Windows.WindowState.Normal> (預設)</span><span class="sxs-lookup"><span data-stu-id="7f7c0-297"><xref:System.Windows.WindowState.Normal> (default)</span></span>  
  
- <xref:System.Windows.WindowState.Maximized>  
  
- <xref:System.Windows.WindowState.Minimized>  
  
 <span data-ttu-id="7f7c0-298">下列範例示範如何建立在開啟時會顯示為最大化的視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-298">The following example shows how to create a window that is shown as maximized when it opens.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStateWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStateWindow.xaml#windowstatewindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-299">一般來說，您應該設定 <xref:System.Windows.Window.WindowState%2A> 以設定視窗的初始狀態。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-299">In general, you should set <xref:System.Windows.Window.WindowState%2A> to configure the initial state of a window.</span></span> <span data-ttu-id="7f7c0-300">可調整大小的視窗顯示後，使用者可以按下視窗標題列上的最小化、最大化和還原按鈕，以變更視窗狀態。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-300">Once a resizable window is shown, users can press the minimize, maximize, and restore buttons on the window's title bar to change the window state.</span></span>  
  
<a name="WindowAppearance"></a>
## <a name="window-appearance"></a><span data-ttu-id="7f7c0-301">視窗外觀</span><span class="sxs-lookup"><span data-stu-id="7f7c0-301">Window Appearance</span></span>  
 <span data-ttu-id="7f7c0-302">您可以新增視窗特定的內容，例如按鈕、標籤和文字方塊，來變更視窗工作區的外觀。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-302">You change the appearance of the client area of a window by adding window-specific content to it, such as buttons, labels, and text boxes.</span></span> <span data-ttu-id="7f7c0-303">若要設定非工作區，會 <xref:System.Windows.Window> 提供數個屬性，包括 <xref:System.Windows.Window.Icon%2A> 設定視窗的圖示以及 <xref:System.Windows.Window.Title%2A> 設定其標題。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-303">To configure the non-client area, <xref:System.Windows.Window> provides several properties, which include <xref:System.Windows.Window.Icon%2A> to set a window's icon and <xref:System.Windows.Window.Title%2A> to set its title.</span></span>  
  
 <span data-ttu-id="7f7c0-304">您也可以藉由設定視窗的調整大小模式、視窗樣式，以及它是否顯示為桌面工作列上的按鈕，變更非工作區框線的外觀和行為。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-304">You can also change the appearance and behavior of non-client area border by configuring a window's resize mode, window style, and whether it appears as a button in the desktop task bar.</span></span>  

<a name="Resize_Mode"></a>
### <a name="resize-mode"></a><span data-ttu-id="7f7c0-305">調整大小模式</span><span class="sxs-lookup"><span data-stu-id="7f7c0-305">Resize Mode</span></span>  
 <span data-ttu-id="7f7c0-306">視 <xref:System.Windows.Window.WindowStyle%2A> 屬性而定，您可以控制使用者可以如何調整視窗大小。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-306">Depending on the <xref:System.Windows.Window.WindowStyle%2A> property, you can control how (and if) users can resize the window.</span></span> <span data-ttu-id="7f7c0-307">視窗樣式的選擇會影響使用者是否可以使用滑鼠拖曳框線來調整視窗大小、是否顯示 [**最小化**]、[**最大化**] 和 [重**設大小**] 按鈕是否出現在非工作區上，以及是否已啟用。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-307">The choice of window style affects whether a user can resize the window by dragging its border with the mouse, whether the **Minimize**, **Maximize**, and **Resize** buttons appear on the non-client area, and, if they do appear, whether they are enabled.</span></span>  
  
 <span data-ttu-id="7f7c0-308">您可以設定視窗的屬性來調整其大小 <xref:System.Windows.Window.ResizeMode%2A> ，它可以是下列其中一個 <xref:System.Windows.ResizeMode> 列舉值：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-308">You can configure how a window resizes by setting its <xref:System.Windows.Window.ResizeMode%2A> property, which can be one of the following <xref:System.Windows.ResizeMode> enumeration values:</span></span>  
  
- <xref:System.Windows.ResizeMode.NoResize>  
  
- <xref:System.Windows.ResizeMode.CanMinimize>  
  
- <span data-ttu-id="7f7c0-309"><xref:System.Windows.ResizeMode.CanResize> (預設)</span><span class="sxs-lookup"><span data-stu-id="7f7c0-309"><xref:System.Windows.ResizeMode.CanResize> (default)</span></span>  
  
- <xref:System.Windows.ResizeMode.CanResizeWithGrip>  
  
 <span data-ttu-id="7f7c0-310">如同 <xref:System.Windows.Window.WindowStyle%2A> ，視窗的調整大小模式不太可能會在其存留期內變更，這表示您很有可能會從 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記進行設定。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-310">As with <xref:System.Windows.Window.WindowStyle%2A>, the resize mode of a window is unlikely to change during its lifetime, which means that you'll most likely set it from [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#ResizeModeWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ResizeModeWindow.xaml#resizemodewindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-311">請注意，您可以藉由檢查屬性，偵測視窗是最大化、最小化或還原 <xref:System.Windows.Window.WindowState%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-311">Note that you can detect whether a window is maximized, minimized, or restored by inspecting the <xref:System.Windows.Window.WindowState%2A> property.</span></span>  
  
<a name="Window_Style"></a>
### <a name="window-style"></a><span data-ttu-id="7f7c0-312">視窗樣式</span><span class="sxs-lookup"><span data-stu-id="7f7c0-312">Window Style</span></span>  
 <span data-ttu-id="7f7c0-313">從視窗非工作區公開的框線適用於大部分的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-313">The border that is exposed from the non-client area of a window is suitable for most applications.</span></span> <span data-ttu-id="7f7c0-314">不過，有一些情況下需要不同型別的框線，或是完全不需要框線，視視窗的型別而定。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-314">However, there are circumstances where different types of borders are needed, or no borders are needed at all, depending on the type of window.</span></span>  
  
 <span data-ttu-id="7f7c0-315">若要控制視窗所取得的框線類型，您可以 <xref:System.Windows.Window.WindowStyle%2A> 使用下列其中一個列舉值來設定其屬性 <xref:System.Windows.WindowStyle> ：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-315">To control what type of border a window gets, you set its <xref:System.Windows.Window.WindowStyle%2A> property with one of the following values of the <xref:System.Windows.WindowStyle> enumeration:</span></span>  
  
- <xref:System.Windows.WindowStyle.None>  
  
- <span data-ttu-id="7f7c0-316"><xref:System.Windows.WindowStyle.SingleBorderWindow> (預設)</span><span class="sxs-lookup"><span data-stu-id="7f7c0-316"><xref:System.Windows.WindowStyle.SingleBorderWindow> (default)</span></span>  
  
- <xref:System.Windows.WindowStyle.ThreeDBorderWindow>  
  
- <xref:System.Windows.WindowStyle.ToolWindow>  
  
 <span data-ttu-id="7f7c0-317">這些視窗樣式的效果如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-317">The effect of these window styles are illustrated in the following figure:</span></span>  
  
 ![視窗框線樣式的說明。](./media/wpf-windows-overview/window-border-styles.png)  
  
 <span data-ttu-id="7f7c0-319">您可以 <xref:System.Windows.Window.WindowStyle%2A> 使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記或程式碼來設定; 因為在視窗存留期間不太可能變更，所以您很可能會使用標記來設定它 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-319">You can set <xref:System.Windows.Window.WindowStyle%2A> using either [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup or code; because it is unlikely to change during the lifetime of a window, you will most likely configure it using [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStyleWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStyleWindow.xaml#windowstylewindowmarkup1)]  
  
#### <a name="non-rectangular-window-style"></a><span data-ttu-id="7f7c0-320">非矩形視窗樣式</span><span class="sxs-lookup"><span data-stu-id="7f7c0-320">Non-Rectangular Window Style</span></span>  
 <span data-ttu-id="7f7c0-321">在某些情況下，可讓您擁有的框線樣式還 <xref:System.Windows.Window.WindowStyle%2A> 不夠。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-321">There are also situations where the border styles that <xref:System.Windows.Window.WindowStyle%2A> allows you to have are not sufficient.</span></span> <span data-ttu-id="7f7c0-322">例如，您可能會想要建立具有非矩形框線的應用程式，例如 Microsoft Windows 媒體播放機使用。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-322">For example, you may want to create an application with a non-rectangular border, like Microsoft Windows Media Player uses.</span></span>  
  
 <span data-ttu-id="7f7c0-323">例如，請考慮下圖所示的語音反升視窗：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-323">For example, consider the speech bubble window shown in the following figure:</span></span>  
  
 ![顯示 [拖曳我] 的語音反升視窗。](./media/wpf-windows-overview/non-rectangular-window-figure.png)  
  
 <span data-ttu-id="7f7c0-325">藉由將 <xref:System.Windows.Window.WindowStyle%2A> 屬性設為 <xref:System.Windows.WindowStyle.None> ，以及使用具有透明度的特殊支援，即可建立這種類型的視窗 <xref:System.Windows.Window> 。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-325">This type of window can be created by setting the <xref:System.Windows.Window.WindowStyle%2A> property to <xref:System.Windows.WindowStyle.None>, and by using special support that <xref:System.Windows.Window> has for transparency.</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#TransparentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TransparentWindow.xaml#transparentwindowmarkup1)]  
  
 <span data-ttu-id="7f7c0-326">這些值的組合會指示視窗要轉譯為完全透明。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-326">This combination of values instructs the window to render completely transparent.</span></span> <span data-ttu-id="7f7c0-327">在此狀態下，無法使用視窗的非工作區裝飾 ([關閉] 功能表、[最小化]、[最大化] 和 [還原] 按鈕等等)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-327">In this state, the window's non-client area adornments (the Close menu, Minimize, Maximize, and Restore buttons, and so on) cannot be used.</span></span> <span data-ttu-id="7f7c0-328">因此，您需要自行提供。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-328">Consequently, you need to provide your own.</span></span>  
  
<a name="Task_Bar_Presence"></a>
### <a name="task-bar-presence"></a><span data-ttu-id="7f7c0-329">工作列目前狀態</span><span class="sxs-lookup"><span data-stu-id="7f7c0-329">Task Bar Presence</span></span>  

<span data-ttu-id="7f7c0-330">視窗的預設面板包括工作列按鈕，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="7f7c0-330">The default appearance of a window includes a taskbar button, like the one shown in the following figure:</span></span>

 ![顯示具有工作列按鈕之視窗的螢幕擷取畫面。](./media/wpf-windows-overview/window-taskbar-button.png)  
  
 <span data-ttu-id="7f7c0-332">有些類型的 windows 沒有工作列按鈕，例如訊息方塊和對話方塊（請參閱[對話方塊總覽](dialog-boxes-overview.md)）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-332">Some types of windows don't have a task bar button, such as message boxes and dialog boxes (see [Dialog Boxes Overview](dialog-boxes-overview.md)).</span></span> <span data-ttu-id="7f7c0-333">您可以藉由設定屬性來控制視窗的工作列按鈕是否顯示 <xref:System.Windows.Window.ShowInTaskbar%2A> （ `true` 預設為）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-333">You can control whether the task bar button for a window is shown by setting the <xref:System.Windows.Window.ShowInTaskbar%2A> property (`true` by default).</span></span>  
  
 [!code-xaml[WindowsOverviewSnippets#ShowInTaskbarWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ShowInTaskbarWindow.xaml#showintaskbarwindowmarkup1)]  
  
<a name="SecurityConsiderations"></a>
## <a name="security-considerations"></a><span data-ttu-id="7f7c0-334">安全性考量</span><span class="sxs-lookup"><span data-stu-id="7f7c0-334">Security Considerations</span></span>  
 <span data-ttu-id="7f7c0-335"><xref:System.Windows.Window>需要具現 `UnmanagedCode` 化安全性許可權。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-335"><xref:System.Windows.Window> requires `UnmanagedCode` security permission to be instantiated.</span></span> <span data-ttu-id="7f7c0-336">對於本機電腦上安裝和啟動的應用程式，這落在授與給該應用程式的權限集範圍內。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-336">For applications installed on and launched from the local machine, this falls within the set of permissions that are granted to the application.</span></span>  
  
 <span data-ttu-id="7f7c0-337">不過，這不在授與使用 ClickOnce 從網際網路或近端內部網路區域啟動之應用程式的許可權集之外。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-337">However, this falls outside the set of permissions granted to applications that are launched from the Internet or Local intranet zone using ClickOnce.</span></span> <span data-ttu-id="7f7c0-338">因此，使用者會收到 ClickOnce 安全性警告，而且必須將應用程式的許可權集合提升為完全信任。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-338">Consequently, users will receive a ClickOnce security warning and will need to elevate the permission set for the application to full trust.</span></span>  
  
 <span data-ttu-id="7f7c0-339">此外，Xbap 預設無法顯示視窗或對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-339">Additionally, XBAPs cannot show windows or dialog boxes by default.</span></span> <span data-ttu-id="7f7c0-340">如需獨立應用程式安全性考慮的討論，請參閱[WPF 安全性策略-平臺安全性](../wpf-security-strategy-platform-security.md)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-340">For a discussion on standalone application security considerations, see [WPF Security Strategy - Platform Security](../wpf-security-strategy-platform-security.md).</span></span>  
  
<a name="Other_Types_of_Windows"></a>
## <a name="other-types-of-windows"></a><span data-ttu-id="7f7c0-341">其他類型的視窗</span><span class="sxs-lookup"><span data-stu-id="7f7c0-341">Other Types of Windows</span></span>  
 <span data-ttu-id="7f7c0-342"><xref:System.Windows.Navigation.NavigationWindow>是設計用來裝載可導覽內容的視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-342"><xref:System.Windows.Navigation.NavigationWindow> is a window that is designed to host navigable content.</span></span> <span data-ttu-id="7f7c0-343">如需詳細資訊，請參閱[導覽總覽](navigation-overview.md)）。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-343">For more information, see [Navigation Overview](navigation-overview.md)).</span></span>  
  
 <span data-ttu-id="7f7c0-344">對話方塊是經常用來從使用者收集資訊以完成一項功能的視窗。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-344">Dialog boxes are windows that are often used to gather information from a user to complete a function.</span></span> <span data-ttu-id="7f7c0-345">例如，當使用者想要開啟檔案時，應用程式通常會顯示 [**開啟**檔案] 對話方塊，以取得使用者的檔案名。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-345">For example, when a user wants to open a file, the **Open File** dialog box is usually displayed by an application to get the file name from the user.</span></span> <span data-ttu-id="7f7c0-346">如需詳細資訊，請參閱[對話方塊概觀](dialog-boxes-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f7c0-346">For more information, see [Dialog Boxes Overview](dialog-boxes-overview.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7f7c0-347">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7f7c0-347">See also</span></span>

- <xref:System.Windows.Window>
- <xref:System.Windows.MessageBox>
- <xref:System.Windows.Navigation.NavigationWindow>
- <xref:System.Windows.Application>
- [<span data-ttu-id="7f7c0-348">對話方塊概觀</span><span class="sxs-lookup"><span data-stu-id="7f7c0-348">Dialog Boxes Overview</span></span>](dialog-boxes-overview.md)
- [<span data-ttu-id="7f7c0-349">建置 WPF 應用程式</span><span class="sxs-lookup"><span data-stu-id="7f7c0-349">Building a WPF Application</span></span>](building-a-wpf-application-wpf.md)

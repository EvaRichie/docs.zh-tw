---
title: 實作 UI 自動化 Invoke 控制項模式
description: 閱讀指導方針和慣例，在使用者介面自動化中執行叫用控制項模式。 請參閱 IInvokeProvider 介面的必要成員。
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Invoke control pattern
- control patterns, Invoke
- Invoke control pattern
ms.assetid: e5b1e239-49f8-468e-bfec-1fba02ec9ac4
ms.openlocfilehash: b464b3ab5cd2b0789798f8b865b946c5eae017eb
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166179"
---
# <a name="implementing-the-ui-automation-invoke-control-pattern"></a><span data-ttu-id="8ef48-104">實作 UI 自動化 Invoke 控制項模式</span><span class="sxs-lookup"><span data-stu-id="8ef48-104">Implementing the UI Automation Invoke Control Pattern</span></span>

> [!NOTE]
> <span data-ttu-id="8ef48-105">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="8ef48-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="8ef48-106">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="8ef48-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>

<span data-ttu-id="8ef48-107">本主題將介紹實作 <xref:System.Windows.Automation.Provider.IInvokeProvider>的方針和慣例，包括事件和屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8ef48-107">This topic introduces guidelines and conventions for implementing <xref:System.Windows.Automation.Provider.IInvokeProvider>, including information about events and properties.</span></span> <span data-ttu-id="8ef48-108">其他參考的連結列於主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="8ef48-108">Links to additional references are listed at the end of the topic.</span></span>

<span data-ttu-id="8ef48-109"><xref:System.Windows.Automation.InvokePattern> 控制項模式用來支援控制項，且這些控制項在啟動時並不會維護狀態，而是會啟始或執行明確的單一動作。</span><span class="sxs-lookup"><span data-stu-id="8ef48-109">The <xref:System.Windows.Automation.InvokePattern> control pattern is used to support controls that do not maintain state when activated but rather initiate or perform a single, unambiguous action.</span></span> <span data-ttu-id="8ef48-110">維護狀態的控制項，例如核取方塊和選項按鈕，必須分別實作 <xref:System.Windows.Automation.Provider.IToggleProvider> 及 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 。</span><span class="sxs-lookup"><span data-stu-id="8ef48-110">Controls that do maintain state, such as check boxes and radio buttons, must instead implement <xref:System.Windows.Automation.Provider.IToggleProvider> and <xref:System.Windows.Automation.Provider.ISelectionItemProvider> respectively.</span></span> <span data-ttu-id="8ef48-111">如需實作叫用控制項模式的控制項，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="8ef48-111">For examples of controls that implement the Invoke control pattern, see [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md).</span></span>

<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="8ef48-112">實作方針和慣例</span><span class="sxs-lookup"><span data-stu-id="8ef48-112">Implementation Guidelines and Conventions</span></span>

<span data-ttu-id="8ef48-113">實作叫用控制項模式時，請注意下列方針和慣例：</span><span class="sxs-lookup"><span data-stu-id="8ef48-113">When implementing the Invoke control pattern, note the following guidelines and conventions:</span></span>

- <span data-ttu-id="8ef48-114">如果未透過另一個控制項模式提供者來公開相同的行為，則控制項會實作 <xref:System.Windows.Automation.Provider.IInvokeProvider> 。</span><span class="sxs-lookup"><span data-stu-id="8ef48-114">Controls implement <xref:System.Windows.Automation.Provider.IInvokeProvider> if the same behavior is not exposed through another control pattern provider.</span></span> <span data-ttu-id="8ef48-115">例如，如果控制項的 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 方法所執行的動作與 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 或 <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 方法相同，該控制項就不應實作 <xref:System.Windows.Automation.Provider.IInvokeProvider>。</span><span class="sxs-lookup"><span data-stu-id="8ef48-115">For example, if the <xref:System.Windows.Automation.InvokePattern.Invoke%2A> method on a control performs the same action as the <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> or <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> method, the control should not implement <xref:System.Windows.Automation.Provider.IInvokeProvider>.</span></span>

- <span data-ttu-id="8ef48-116">通常按一下、按兩下或按 ENTER、使用預先定義的鍵盤快速鍵，或其他按鈕組合，就可以叫用控制項。</span><span class="sxs-lookup"><span data-stu-id="8ef48-116">Invoking a control is generally performed by clicking or double-clicking or pressing ENTER, a predefined keyboard shortcut, or some alternate combination of keystrokes.</span></span>

- <span data-ttu-id="8ef48-117">已啟動的控制項上會引發<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> (以回應執行相關動作的控制項)。</span><span class="sxs-lookup"><span data-stu-id="8ef48-117"><xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> is raised on a control that has been activated (as a response to a control carrying out its associated action).</span></span> <span data-ttu-id="8ef48-118">在可能的情況下，應該是在控制項完成該動作並返回，且沒有發生封鎖時才會引發該事件。</span><span class="sxs-lookup"><span data-stu-id="8ef48-118">If possible, the event should be raised after the control has completed the action and returned without blocking.</span></span> <span data-ttu-id="8ef48-119">在下列情節中，叫用事件應該在服務叫用要求之前引發：</span><span class="sxs-lookup"><span data-stu-id="8ef48-119">The Invoked event should be raised before servicing the Invoke request in the following scenarios:</span></span>

  - <span data-ttu-id="8ef48-120">無法或不適合等待至動作完成。</span><span class="sxs-lookup"><span data-stu-id="8ef48-120">It is not possible or practical to wait until the action is complete.</span></span>

  - <span data-ttu-id="8ef48-121">動作需要使用者互動。</span><span class="sxs-lookup"><span data-stu-id="8ef48-121">The action requires user interaction.</span></span>

  - <span data-ttu-id="8ef48-122">動作費時，且會導致發出呼叫的用戶端長時間凍結。</span><span class="sxs-lookup"><span data-stu-id="8ef48-122">The action is time-consuming and will cause the calling client to block for a significant amount of time.</span></span>

- <span data-ttu-id="8ef48-123">如果叫用控制項會有嚴重的副作用，就必須透過 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A> 屬性公開這些副作用。</span><span class="sxs-lookup"><span data-stu-id="8ef48-123">If invoking the control has significant side-effects, those side-effects should be exposed through the <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A> property.</span></span> <span data-ttu-id="8ef48-124">例如，雖然 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 和選取範圍沒有關聯，但 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 卻可能會造成其他控制項受到選取。</span><span class="sxs-lookup"><span data-stu-id="8ef48-124">For example, even though <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> is not associated with selection, <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> may cause another control to become selected.</span></span>

- <span data-ttu-id="8ef48-125">停留 (滑鼠在上) 效果通常不會形成叫用事件。</span><span class="sxs-lookup"><span data-stu-id="8ef48-125">Hover (or mouse-over) effects generally do not constitute an Invoked event.</span></span> <span data-ttu-id="8ef48-126">但是，根據停留狀態而執行動作 (相對於產生視覺效果) 的控制項，應該要支援 <xref:System.Windows.Automation.InvokePattern> 控制項模式。</span><span class="sxs-lookup"><span data-stu-id="8ef48-126">However, controls that perform an action (as opposed to cause a visual effect) based on the hover state should support the <xref:System.Windows.Automation.InvokePattern> control pattern.</span></span>

> [!NOTE]
> <span data-ttu-id="8ef48-127">如果控制項的叫用是與滑鼠相關的副作用所造成的，便會將這個實作視為協助工具問題。</span><span class="sxs-lookup"><span data-stu-id="8ef48-127">This implementation is considered an accessibility issue if the control can be invoked only as a result of a mouse-related side effect.</span></span>

- <span data-ttu-id="8ef48-128">叫用控制項和選擇項目不同。</span><span class="sxs-lookup"><span data-stu-id="8ef48-128">Invoking a control is different from selecting an item.</span></span> <span data-ttu-id="8ef48-129">但是，依據控制項而定，叫用某些控制項可能會有造成此項目受到選取的副作用。</span><span class="sxs-lookup"><span data-stu-id="8ef48-129">However, depending on the control, invoking it may cause the item to become selected as a side-effect.</span></span> <span data-ttu-id="8ef48-130">例如，叫用 [我的文件] 資料夾中的 Microsoft Word 檔案清單專案時，會選取該專案並開啟該檔。</span><span class="sxs-lookup"><span data-stu-id="8ef48-130">For example, invoking a Microsoft Word document list item in the My Documents folder both selects the item and opens the document.</span></span>

- <span data-ttu-id="8ef48-131">叫用某個項目時，此項目可能會立即從 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構中消失。</span><span class="sxs-lookup"><span data-stu-id="8ef48-131">An element can disappear from the [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] tree immediately upon being invoked.</span></span> <span data-ttu-id="8ef48-132">要求事件回呼所提供的項目資訊，可能會因此而失敗。</span><span class="sxs-lookup"><span data-stu-id="8ef48-132">Requesting information from the element provided by the event callback may fail as a result.</span></span> <span data-ttu-id="8ef48-133">建議的解決方法是預先擷取快取的資訊。</span><span class="sxs-lookup"><span data-stu-id="8ef48-133">Pre-fetching cached information is the recommended workaround.</span></span>

- <span data-ttu-id="8ef48-134">控制項可以實作多個控制項模式。</span><span class="sxs-lookup"><span data-stu-id="8ef48-134">Controls can implement multiple control patterns.</span></span> <span data-ttu-id="8ef48-135">例如，Microsoft Excel 工具列上的 [填滿色彩] 控制項會同時執行 <xref:System.Windows.Automation.InvokePattern> 和 <xref:System.Windows.Automation.ExpandCollapsePattern> 控制項模式。</span><span class="sxs-lookup"><span data-stu-id="8ef48-135">For example, the Fill Color control on the Microsoft Excel toolbar implements both the <xref:System.Windows.Automation.InvokePattern> and the <xref:System.Windows.Automation.ExpandCollapsePattern> control patterns.</span></span> <span data-ttu-id="8ef48-136"><xref:System.Windows.Automation.ExpandCollapsePattern> 會公開功能表，而 <xref:System.Windows.Automation.InvokePattern> 則會以選擇的色彩填滿作用中的選取範圍。</span><span class="sxs-lookup"><span data-stu-id="8ef48-136"><xref:System.Windows.Automation.ExpandCollapsePattern> exposes the menu and the <xref:System.Windows.Automation.InvokePattern> fills the active selection with the chosen color.</span></span>

<a name="Required_Members_for_the_IValueProvider_Interface"></a>

## <a name="required-members-for-iinvokeprovider"></a><span data-ttu-id="8ef48-137">IInvokeProvider 的必要成員</span><span class="sxs-lookup"><span data-stu-id="8ef48-137">Required Members for IInvokeProvider</span></span>

<span data-ttu-id="8ef48-138">以下是實作 <xref:System.Windows.Automation.Provider.IInvokeProvider>的必要屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="8ef48-138">The following properties and methods are required for implementing <xref:System.Windows.Automation.Provider.IInvokeProvider>.</span></span>

|<span data-ttu-id="8ef48-139">必要成員</span><span class="sxs-lookup"><span data-stu-id="8ef48-139">Required members</span></span>|<span data-ttu-id="8ef48-140">成員類型</span><span class="sxs-lookup"><span data-stu-id="8ef48-140">Member type</span></span>|<span data-ttu-id="8ef48-141">注意</span><span class="sxs-lookup"><span data-stu-id="8ef48-141">Notes</span></span>|
|----------------------|-----------------|-----------|
|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A>|<span data-ttu-id="8ef48-142">method</span><span class="sxs-lookup"><span data-stu-id="8ef48-142">method</span></span>|<span data-ttu-id="8ef48-143"><xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 為非同步呼叫，且必須立即返回，不可封鎖。</span><span class="sxs-lookup"><span data-stu-id="8ef48-143"><xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> is an asynchronous call and must return immediately without blocking.</span></span><br /><br /> <span data-ttu-id="8ef48-144">對於叫用時直接或間接啟動強制回應對話方塊的控制項，此行為尤其重要。</span><span class="sxs-lookup"><span data-stu-id="8ef48-144">This behavior is particularly critical for controls that, directly or indirectly, launch a modal dialog when invoked.</span></span> <span data-ttu-id="8ef48-145">任何引發事件的使用者介面自動化用戶端都會維持封鎖的狀態，直到強制回應對話方塊關閉為止。</span><span class="sxs-lookup"><span data-stu-id="8ef48-145">Any UI Automation client that instigated the event will remain blocked until the modal dialog is closed.</span></span>|

<a name="Exceptions"></a>

## <a name="exceptions"></a><span data-ttu-id="8ef48-146">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8ef48-146">Exceptions</span></span>

<span data-ttu-id="8ef48-147">提供者必須擲回下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8ef48-147">Providers must throw the following exceptions.</span></span>

|<span data-ttu-id="8ef48-148">例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="8ef48-148">Exception Type</span></span>|<span data-ttu-id="8ef48-149">條件</span><span class="sxs-lookup"><span data-stu-id="8ef48-149">Condition</span></span>|
|--------------------|---------------|
|<xref:System.Windows.Automation.ElementNotEnabledException>|<span data-ttu-id="8ef48-150">如果未啟用此控制項。</span><span class="sxs-lookup"><span data-stu-id="8ef48-150">If the control is not enabled.</span></span>|

## <a name="see-also"></a><span data-ttu-id="8ef48-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8ef48-151">See also</span></span>

- [<span data-ttu-id="8ef48-152">UI 自動化控制項模式概觀</span><span class="sxs-lookup"><span data-stu-id="8ef48-152">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="8ef48-153">支援 UI 自動化提供者的控制項模式</span><span class="sxs-lookup"><span data-stu-id="8ef48-153">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="8ef48-154">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="8ef48-154">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="8ef48-155">使用 UI 自動化叫用控制項</span><span class="sxs-lookup"><span data-stu-id="8ef48-155">Invoke a Control Using UI Automation</span></span>](invoke-a-control-using-ui-automation.md)
- [<span data-ttu-id="8ef48-156">UI 自動化樹狀目錄概觀</span><span class="sxs-lookup"><span data-stu-id="8ef48-156">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="8ef48-157">使用 UI 自動化中的快取</span><span class="sxs-lookup"><span data-stu-id="8ef48-157">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)

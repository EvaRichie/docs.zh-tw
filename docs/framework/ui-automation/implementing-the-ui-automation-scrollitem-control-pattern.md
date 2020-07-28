---
title: 實作 UI 自動化 ScrollItem 控制項模式
description: 請參閱在使用者介面自動化中執行 ScrollItem 控制項模式的指導方針和慣例。 請參閱 IScrollItemProvider 介面的必要成員。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Scroll Item
- UI Automation, Scroll Item control pattern
- Scroll Item control pattern
ms.assetid: 903bab5c-80c1-44d7-bdc2-0a418893b987
ms.openlocfilehash: a548eb25280d9a8feddc4633a1ba3e7dc022af36
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163575"
---
# <a name="implementing-the-ui-automation-scrollitem-control-pattern"></a><span data-ttu-id="9815b-104">實作 UI 自動化 ScrollItem 控制項模式</span><span class="sxs-lookup"><span data-stu-id="9815b-104">Implementing the UI Automation ScrollItem Control Pattern</span></span>
> [!NOTE]
> <span data-ttu-id="9815b-105">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="9815b-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="9815b-106">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="9815b-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="9815b-107">本主題簡介實作 <xref:System.Windows.Automation.Provider.IScrollItemProvider> 的方針和慣例，包括屬性、方法和事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9815b-107">This topic introduces guidelines and conventions for implementing the <xref:System.Windows.Automation.Provider.IScrollItemProvider>, including information about properties, methods, and events.</span></span> <span data-ttu-id="9815b-108">其他參考的連結列於主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="9815b-108">Links to additional references are listed at the end of the topic.</span></span>  
  
 <span data-ttu-id="9815b-109"><xref:System.Windows.Automation.ScrollItemPattern> 控制項模式是用以支援實作 <xref:System.Windows.Automation.Provider.IScrollProvider> 之容器的個別子控制項。</span><span class="sxs-lookup"><span data-stu-id="9815b-109">The <xref:System.Windows.Automation.ScrollItemPattern> control pattern is used to support individual child controls of containers that implement <xref:System.Windows.Automation.Provider.IScrollProvider>.</span></span> <span data-ttu-id="9815b-110">此控制項模式會擔任子控制項及其容器之間的通訊通道，以確保容器可變更其顯示子控制項的檢視區內目前可見內容 (或區域)。</span><span class="sxs-lookup"><span data-stu-id="9815b-110">This control pattern acts as a communication channel between a child control and its container to ensure that the container can change the currently visible content (or region) within its viewport to display the child control.</span></span> <span data-ttu-id="9815b-111">如需實作此控制項模式的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="9815b-111">For examples of controls that implement this control pattern, see [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md).</span></span>  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="9815b-112">實作方針和慣例</span><span class="sxs-lookup"><span data-stu-id="9815b-112">Implementation Guidelines and Conventions</span></span>  
 <span data-ttu-id="9815b-113">實作捲軸項目控制項模式時，請注意下列方針和慣例：</span><span class="sxs-lookup"><span data-stu-id="9815b-113">When implementing the Scroll Item control pattern, note the following guidelines and conventions:</span></span>  
  
- <span data-ttu-id="9815b-114">視窗或畫布控制項內含的項目不必實作 IScrollItemProvider 介面。</span><span class="sxs-lookup"><span data-stu-id="9815b-114">Items contained within a Window or Canvas control are not required to implement the IScrollItemProvider interface.</span></span> <span data-ttu-id="9815b-115">但若要實作，這些項目就必須公開 <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 的有效位置。</span><span class="sxs-lookup"><span data-stu-id="9815b-115">As an alternative, however, they must expose a valid location for the <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.</span></span> <span data-ttu-id="9815b-116">如此可允許使用者介面自動化用戶端應用程式將 <xref:System.Windows.Automation.ScrollPattern> 控制項模式方法用於顯示子項目的容器。</span><span class="sxs-lookup"><span data-stu-id="9815b-116">This will allow a UI Automation client application to use the <xref:System.Windows.Automation.ScrollPattern> control pattern methods on the container to display the child item.</span></span>  
  
<a name="Required_Members_for_IScrollItemProvider"></a>
## <a name="required-members-for-iscrollitemprovider"></a><span data-ttu-id="9815b-117">IScrollItemProvider 的必要成員</span><span class="sxs-lookup"><span data-stu-id="9815b-117">Required Members for IScrollItemProvider</span></span>  
 <span data-ttu-id="9815b-118">實作 IScrollProvider 介面需要下列方法。</span><span class="sxs-lookup"><span data-stu-id="9815b-118">The following method is required for implementing the IScrollProvider interface.</span></span>  
  
|<span data-ttu-id="9815b-119">必要成員</span><span class="sxs-lookup"><span data-stu-id="9815b-119">Required members</span></span>|<span data-ttu-id="9815b-120">成員類型</span><span class="sxs-lookup"><span data-stu-id="9815b-120">Member type</span></span>|<span data-ttu-id="9815b-121">注意</span><span class="sxs-lookup"><span data-stu-id="9815b-121">Notes</span></span>|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider.ScrollIntoView%2A>|<span data-ttu-id="9815b-122">-方法</span><span class="sxs-lookup"><span data-stu-id="9815b-122">-   Method</span></span>|<span data-ttu-id="9815b-123">None</span><span class="sxs-lookup"><span data-stu-id="9815b-123">None</span></span>|  
  
 <span data-ttu-id="9815b-124">此控制項模式沒有任何相關聯的屬性或事件。</span><span class="sxs-lookup"><span data-stu-id="9815b-124">This control pattern has no associated properties or events.</span></span>  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a><span data-ttu-id="9815b-125">例外狀況</span><span class="sxs-lookup"><span data-stu-id="9815b-125">Exceptions</span></span>  
 <span data-ttu-id="9815b-126">提供者必須擲回下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9815b-126">Providers must throw the following exceptions.</span></span>  
  
|<span data-ttu-id="9815b-127">例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="9815b-127">Exception Type</span></span>|<span data-ttu-id="9815b-128">條件</span><span class="sxs-lookup"><span data-stu-id="9815b-128">Condition</span></span>|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<span data-ttu-id="9815b-129">如果無法將項目捲動到檢視中：</span><span class="sxs-lookup"><span data-stu-id="9815b-129">If an item cannot be scrolled into view:</span></span><br /><br /> -   <xref:System.Windows.Automation.ScrollItemPattern.ScrollIntoView%2A>|  
  
## <a name="see-also"></a><span data-ttu-id="9815b-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9815b-130">See also</span></span>

- [<span data-ttu-id="9815b-131">UI 自動化控制項模式概觀</span><span class="sxs-lookup"><span data-stu-id="9815b-131">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="9815b-132">支援 UI 自動化提供者的控制項模式</span><span class="sxs-lookup"><span data-stu-id="9815b-132">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="9815b-133">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="9815b-133">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="9815b-134">UI 自動化樹狀目錄概觀</span><span class="sxs-lookup"><span data-stu-id="9815b-134">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="9815b-135">使用 UI 自動化中的快取</span><span class="sxs-lookup"><span data-stu-id="9815b-135">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)

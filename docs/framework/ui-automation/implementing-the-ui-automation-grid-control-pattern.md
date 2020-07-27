---
title: 實作 UI 自動化 Grid 控制項模式
description: 瞭解在使用者介面自動化中執行 GridPattern 方格控制項模式的指導方針和慣例。 學習如何執行 IGridProvider 介面。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, grid
- grid control pattern
- UI Automation, grid control pattern
ms.assetid: 234d11a0-7ce7-4309-8989-2f4720e02f78
ms.openlocfilehash: c7aae8e8070c989c4b36e0581aa5f48f51416f97
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165876"
---
# <a name="implementing-the-ui-automation-grid-control-pattern"></a><span data-ttu-id="3589a-104">實作 UI 自動化 Grid 控制項模式</span><span class="sxs-lookup"><span data-stu-id="3589a-104">Implementing the UI Automation Grid Control Pattern</span></span>
> [!NOTE]
> <span data-ttu-id="3589a-105">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="3589a-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="3589a-106">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="3589a-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="3589a-107">本主題簡介實作 <xref:System.Windows.Automation.Provider.IGridProvider>的方針和慣例，包括屬性、方法和事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3589a-107">This topic introduces guidelines and conventions for implementing <xref:System.Windows.Automation.Provider.IGridProvider>, including information about properties, methods, and events.</span></span> <span data-ttu-id="3589a-108">其他參考的連結會在概觀的結尾列出。</span><span class="sxs-lookup"><span data-stu-id="3589a-108">Links to additional references are listed at the end of the overview.</span></span>  
  
 <span data-ttu-id="3589a-109"><xref:System.Windows.Automation.GridPattern> 控制項模式是用以支援當作子項目集合的容器使用的控制項。</span><span class="sxs-lookup"><span data-stu-id="3589a-109">The <xref:System.Windows.Automation.GridPattern> control pattern is used to support controls that act as containers for a collection of child elements.</span></span> <span data-ttu-id="3589a-110">此項目的子系必須實作 <xref:System.Windows.Automation.Provider.IGridItemProvider> ，並組合管理成資料列與資料行可周遊的二維邏輯座標系統。</span><span class="sxs-lookup"><span data-stu-id="3589a-110">The children of this element must implement <xref:System.Windows.Automation.Provider.IGridItemProvider> and be organized in a two-dimensional logical coordinate system that can be traversed by row and column.</span></span> <span data-ttu-id="3589a-111">如需實作此控制項模式的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="3589a-111">For examples of controls that implement this control pattern, see [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md).</span></span>  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="3589a-112">實作方針和慣例</span><span class="sxs-lookup"><span data-stu-id="3589a-112">Implementation Guidelines and Conventions</span></span>  
 <span data-ttu-id="3589a-113">實作方格控制項模式時，請注意下列方針和慣例：</span><span class="sxs-lookup"><span data-stu-id="3589a-113">When implementing the Grid control pattern, note the following guidelines and conventions:</span></span>  
  
- <span data-ttu-id="3589a-114">方格座標是從左上角 (或根據地區為右上儲存格) 以零為起始，座標為 (0, 0)。</span><span class="sxs-lookup"><span data-stu-id="3589a-114">Grid coordinates are zero-based with the upper left (or upper right cell depending on locale) having coordinates (0, 0).</span></span>  
  
- <span data-ttu-id="3589a-115">如果儲存格是空的，仍必須傳回使用者介面自動化項目，才能支援該儲存格的 <xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="3589a-115">If a cell is empty, a UI Automation element must still be returned in order to support the <xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A> property for that cell.</span></span> <span data-ttu-id="3589a-116">當子項目在方格中的配置類似不完全陣列 (請參閱以下範例)，就可能發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="3589a-116">This is possible when the layout of child elements in the grid is similar to a ragged array (see example below).</span></span>  
  
 <span data-ttu-id="3589a-117">![顯示不完全配置的 Windows 檔案總管檢視。](./media/uia-gridpattern-ragged-array.PNG "UIA_GridPattern_Ragged_Array")</span><span class="sxs-lookup"><span data-stu-id="3589a-117">![Windows Explorer view showing ragged layout.](./media/uia-gridpattern-ragged-array.PNG "UIA_GridPattern_Ragged_Array")</span></span>  
<span data-ttu-id="3589a-118">座標是空的方格控制項範例</span><span class="sxs-lookup"><span data-stu-id="3589a-118">Example of a Grid Control with Empty Coordinates</span></span>  
  
- <span data-ttu-id="3589a-119">單一項目的方格仍必須實作 <xref:System.Windows.Automation.Provider.IGridProvider> ，才能在邏輯上視為是方格。</span><span class="sxs-lookup"><span data-stu-id="3589a-119">A grid with a single item is still required to implement <xref:System.Windows.Automation.Provider.IGridProvider> if it is logically considered to be a grid.</span></span> <span data-ttu-id="3589a-120">方格中的子項目數為多少都沒關係。</span><span class="sxs-lookup"><span data-stu-id="3589a-120">The number of child items in the grid is immaterial.</span></span>  
  
- <span data-ttu-id="3589a-121">根據提供者實作而定，隱藏資料列和資料行可能會載入到 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構，因此會反映在 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.RowCount%2A> 和 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.ColumnCount%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="3589a-121">Hidden rows and columns, depending on the provider implementation, may be loaded in the [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] tree and therefore will be reflected in the <xref:System.Windows.Automation.GridPattern.GridPatternInformation.RowCount%2A> and <xref:System.Windows.Automation.GridPattern.GridPatternInformation.ColumnCount%2A> properties.</span></span> <span data-ttu-id="3589a-122">如果隱藏資料列和資料行未載入，則應不會列入計數。</span><span class="sxs-lookup"><span data-stu-id="3589a-122">If the hidden rows and columns have not yet been loaded, they should not be counted.</span></span>  
  
- <span data-ttu-id="3589a-123"><xref:System.Windows.Automation.Provider.IGridProvider> 不會啟用方格的使用中操作，而必須實作 <xref:System.Windows.Automation.Provider.ITransformProvider> 才能啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="3589a-123"><xref:System.Windows.Automation.Provider.IGridProvider> does not enable active manipulation of a grid; <xref:System.Windows.Automation.Provider.ITransformProvider> must be implemented to enable this functionality.</span></span>  
  
- <span data-ttu-id="3589a-124">使用 <xref:System.Windows.Automation.StructureChangedEventHandler> 接聽方格的結構或配置變更，例如新增、移除或合併儲存格。</span><span class="sxs-lookup"><span data-stu-id="3589a-124">Use a <xref:System.Windows.Automation.StructureChangedEventHandler> to listen for structural or layout changes to the grid such as cells that have been added, removed, or merged.</span></span>  
  
- <span data-ttu-id="3589a-125">使用 <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> 追蹤方格項目或儲存格的周遊情形。</span><span class="sxs-lookup"><span data-stu-id="3589a-125">Use a <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> to track traversal through the items or cells of a grid.</span></span>  
  
<a name="Required_Members_for_IGridProvider"></a>
## <a name="required-members-for-igridprovider"></a><span data-ttu-id="3589a-126">IGridProvider 的必要成員</span><span class="sxs-lookup"><span data-stu-id="3589a-126">Required Members for IGridProvider</span></span>  
 <span data-ttu-id="3589a-127">以下是實作 IGridProvider 介面的必要屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="3589a-127">The following properties and methods are required for implementing the IGridProvider interface.</span></span>  
  
|<span data-ttu-id="3589a-128">必要成員</span><span class="sxs-lookup"><span data-stu-id="3589a-128">Required members</span></span>|<span data-ttu-id="3589a-129">類型</span><span class="sxs-lookup"><span data-stu-id="3589a-129">Type</span></span>|<span data-ttu-id="3589a-130">注意</span><span class="sxs-lookup"><span data-stu-id="3589a-130">Notes</span></span>|  
|----------------------|----------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A>|<span data-ttu-id="3589a-131">屬性</span><span class="sxs-lookup"><span data-stu-id="3589a-131">Property</span></span>|<span data-ttu-id="3589a-132">None</span><span class="sxs-lookup"><span data-stu-id="3589a-132">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>|<span data-ttu-id="3589a-133">屬性</span><span class="sxs-lookup"><span data-stu-id="3589a-133">Property</span></span>|<span data-ttu-id="3589a-134">None</span><span class="sxs-lookup"><span data-stu-id="3589a-134">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A>|<span data-ttu-id="3589a-135">方法</span><span class="sxs-lookup"><span data-stu-id="3589a-135">Method</span></span>|<span data-ttu-id="3589a-136">None</span><span class="sxs-lookup"><span data-stu-id="3589a-136">None</span></span>|  
  
 <span data-ttu-id="3589a-137">此控制項模式沒有任何相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="3589a-137">This control pattern has no associated events.</span></span>  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a><span data-ttu-id="3589a-138">例外狀況</span><span class="sxs-lookup"><span data-stu-id="3589a-138">Exceptions</span></span>  
 <span data-ttu-id="3589a-139">提供者必須擲回下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3589a-139">Providers must throw the following exceptions.</span></span>  
  
|<span data-ttu-id="3589a-140">例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="3589a-140">Exception type</span></span>|<span data-ttu-id="3589a-141">條件</span><span class="sxs-lookup"><span data-stu-id="3589a-141">Condition</span></span>|  
|--------------------|---------------|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> <span data-ttu-id="3589a-142">-如果要求的資料列座標大於，或資料行 <xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A> 座標大於 <xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A> 。</span><span class="sxs-lookup"><span data-stu-id="3589a-142">-   If the requested row coordinate is larger than the <xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A> or the column coordinate is larger than the <xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>.</span></span>|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> <span data-ttu-id="3589a-143">-如果要求的資料列或資料行座標之一小於零。</span><span class="sxs-lookup"><span data-stu-id="3589a-143">-   If either of the requested row or column coordinates is less than zero.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="3589a-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3589a-144">See also</span></span>

- [<span data-ttu-id="3589a-145">UI 自動化控制項模式概觀</span><span class="sxs-lookup"><span data-stu-id="3589a-145">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="3589a-146">支援 UI 自動化提供者的控制項模式</span><span class="sxs-lookup"><span data-stu-id="3589a-146">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="3589a-147">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="3589a-147">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="3589a-148">實作 UI 自動化 GridItem 控制項模式</span><span class="sxs-lookup"><span data-stu-id="3589a-148">Implementing the UI Automation GridItem Control Pattern</span></span>](implementing-the-ui-automation-griditem-control-pattern.md)
- [<span data-ttu-id="3589a-149">UI 自動化樹狀目錄概觀</span><span class="sxs-lookup"><span data-stu-id="3589a-149">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="3589a-150">使用 UI 自動化中的快取</span><span class="sxs-lookup"><span data-stu-id="3589a-150">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)

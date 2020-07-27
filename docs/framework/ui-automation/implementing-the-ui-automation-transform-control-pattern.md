---
title: 實作 UI 自動化 Transform 控制項模式
description: 請參閱指導方針和慣例，在使用者介面自動化中執行轉換控制項模式。 知道 ITransformProvider 介面的必要成員。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Transform
- Transform control pattern
- UI Automation, Transform control pattern
ms.assetid: 5f49d843-5845-4800-9d9c-56ce0d146844
ms.openlocfilehash: da11ce4cf9da10c0ebb990f9439b0bbe3621c561
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168216"
---
# <a name="implementing-the-ui-automation-transform-control-pattern"></a><span data-ttu-id="a25d7-104">實作 UI 自動化 Transform 控制項模式</span><span class="sxs-lookup"><span data-stu-id="a25d7-104">Implementing the UI Automation Transform Control Pattern</span></span>
> [!NOTE]
> <span data-ttu-id="a25d7-105">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="a25d7-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="a25d7-106">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="a25d7-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="a25d7-107">本主題簡介實作 <xref:System.Windows.Automation.Provider.ITransformProvider>的方針和慣例，包括屬性、方法和事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a25d7-107">This topic introduces guidelines and conventions for implementing <xref:System.Windows.Automation.Provider.ITransformProvider>, including information about properties, methods, and events.</span></span> <span data-ttu-id="a25d7-108">其他參考的連結列於主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="a25d7-108">Links to additional references are listed at the end of the topic.</span></span>  
  
 <span data-ttu-id="a25d7-109"><xref:System.Windows.Automation.TransformPattern> 控制項模式用來支援可在二維空間內移動、調整大小或旋轉的控制項。</span><span class="sxs-lookup"><span data-stu-id="a25d7-109">The <xref:System.Windows.Automation.TransformPattern> control pattern is used to support controls that can be moved, resized, or rotated within a two-dimensional space.</span></span> <span data-ttu-id="a25d7-110">如需實作此控制項模式的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="a25d7-110">For examples of controls that implement this control pattern, see [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md).</span></span>  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="a25d7-111">實作方針和慣例</span><span class="sxs-lookup"><span data-stu-id="a25d7-111">Implementation Guidelines and Conventions</span></span>  
 <span data-ttu-id="a25d7-112">實作轉換控制項模式時，請注意下列方針和慣例：</span><span class="sxs-lookup"><span data-stu-id="a25d7-112">When implementing the Transform control pattern, note the following guidelines and conventions:</span></span>  
  
- <span data-ttu-id="a25d7-113">此控制項模式的支援不限於桌面上的物件。</span><span class="sxs-lookup"><span data-stu-id="a25d7-113">Support for this control pattern is not limited to objects on the desktop.</span></span> <span data-ttu-id="a25d7-114">若容器物件的子項可以自由在容器的範圍內移動、調整大小或旋轉，則這些子項也必須支援此控制項模式。</span><span class="sxs-lookup"><span data-stu-id="a25d7-114">This control pattern must also be supported by the children of a container object if the children can be moved, resized, or rotated freely within the boundaries of the container.</span></span>  
  
- <span data-ttu-id="a25d7-115">如果物件最後在螢幕上的位置完全在其容器的座標以外，而鍵盤或滑鼠存取不到的話，就無法移動、調整大小或旋轉物件 (例如，最上層的視窗移離螢幕，或是子物件移到容器檢視區範圍以外的地方)。</span><span class="sxs-lookup"><span data-stu-id="a25d7-115">An object cannot be moved, resized, or rotated such that its resulting screen location would be completely outside the coordinates of its container and therefore inaccessible to the keyboard or mouse (for example, when a top-level window is moved off-screen or a child object is moved outside the boundaries of the container's viewport).</span></span> <span data-ttu-id="a25d7-116">在這種情況下，物件會放置到最接近所要求螢幕座標的地方，其上方或左方座標會覆寫成容器範圍內的座標。</span><span class="sxs-lookup"><span data-stu-id="a25d7-116">In these cases, the object is placed as close to the requested screen coordinates as possible with the top or left coordinates overridden to be within the container boundaries.</span></span>  
  
- <span data-ttu-id="a25d7-117">針對多監視器系統，若物件移動、調整大小或旋轉後的位置完全超出合併桌面螢幕座標的範圍，物件就會移至主要監視器上最接近所要求座標的位置。</span><span class="sxs-lookup"><span data-stu-id="a25d7-117">For multi-monitor systems, if an object is moved, resized, or rotated completely outside the combined desktop screen coordinates, the object is placed on the primary monitor as close to the requested coordinates as possible.</span></span>  
  
- <span data-ttu-id="a25d7-118">所有參數和屬性值都是絕對值，不受地區設定影響。</span><span class="sxs-lookup"><span data-stu-id="a25d7-118">All parameters and property values are absolute and independent of locale.</span></span>  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>
## <a name="required-members-for-itransformprovider"></a><span data-ttu-id="a25d7-119">ITransformProvider 的必要成員</span><span class="sxs-lookup"><span data-stu-id="a25d7-119">Required Members for ITransformProvider</span></span>  
 <span data-ttu-id="a25d7-120">以下是實作 <xref:System.Windows.Automation.Provider.ITransformProvider>的必要屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="a25d7-120">The following properties and methods are required for implementing <xref:System.Windows.Automation.Provider.ITransformProvider>.</span></span>  
  
|<span data-ttu-id="a25d7-121">必要成員</span><span class="sxs-lookup"><span data-stu-id="a25d7-121">Required members</span></span>|<span data-ttu-id="a25d7-122">成員類型</span><span class="sxs-lookup"><span data-stu-id="a25d7-122">Member type</span></span>|<span data-ttu-id="a25d7-123">注意</span><span class="sxs-lookup"><span data-stu-id="a25d7-123">Notes</span></span>|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanMove%2A>|<span data-ttu-id="a25d7-124">屬性</span><span class="sxs-lookup"><span data-stu-id="a25d7-124">Property</span></span>|<span data-ttu-id="a25d7-125">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-125">None</span></span>|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanResize%2A>|<span data-ttu-id="a25d7-126">屬性</span><span class="sxs-lookup"><span data-stu-id="a25d7-126">Property</span></span>|<span data-ttu-id="a25d7-127">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-127">None</span></span>|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanRotate%2A>|<span data-ttu-id="a25d7-128">屬性</span><span class="sxs-lookup"><span data-stu-id="a25d7-128">Property</span></span>|<span data-ttu-id="a25d7-129">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-129">None</span></span>|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Move%2A>|<span data-ttu-id="a25d7-130">方法</span><span class="sxs-lookup"><span data-stu-id="a25d7-130">Method</span></span>|<span data-ttu-id="a25d7-131">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-131">None</span></span>|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Resize%2A>|<span data-ttu-id="a25d7-132">方法</span><span class="sxs-lookup"><span data-stu-id="a25d7-132">Method</span></span>|<span data-ttu-id="a25d7-133">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-133">None</span></span>|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Rotate%2A>|<span data-ttu-id="a25d7-134">方法</span><span class="sxs-lookup"><span data-stu-id="a25d7-134">Method</span></span>|<span data-ttu-id="a25d7-135">None</span><span class="sxs-lookup"><span data-stu-id="a25d7-135">None</span></span>|  
  
 <span data-ttu-id="a25d7-136">此控制項模式沒有任何相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="a25d7-136">This control pattern has no associated events.</span></span>  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a><span data-ttu-id="a25d7-137">例外狀況</span><span class="sxs-lookup"><span data-stu-id="a25d7-137">Exceptions</span></span>  
 <span data-ttu-id="a25d7-138">提供者必須擲回下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a25d7-138">Providers must throw the following exceptions.</span></span>  
  
|<span data-ttu-id="a25d7-139">例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="a25d7-139">Exception Type</span></span>|<span data-ttu-id="a25d7-140">條件</span><span class="sxs-lookup"><span data-stu-id="a25d7-140">Condition</span></span>|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Move%2A><br /><br /> <span data-ttu-id="a25d7-141">-如果 <xref:System.Windows.Automation.TransformPatternIdentifiers.CanMoveProperty> 為 false。</span><span class="sxs-lookup"><span data-stu-id="a25d7-141">-   If the <xref:System.Windows.Automation.TransformPatternIdentifiers.CanMoveProperty> is false.</span></span>|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Resize%2A><br /><br /> <span data-ttu-id="a25d7-142">-如果 <xref:System.Windows.Automation.TransformPatternIdentifiers.CanResizeProperty> 為 false。</span><span class="sxs-lookup"><span data-stu-id="a25d7-142">-   If the <xref:System.Windows.Automation.TransformPatternIdentifiers.CanResizeProperty> is false.</span></span>|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Rotate%2A><br /><br /> <span data-ttu-id="a25d7-143">-如果 <xref:System.Windows.Automation.TransformPatternIdentifiers.CanRotateProperty> 為 false。</span><span class="sxs-lookup"><span data-stu-id="a25d7-143">-   If the <xref:System.Windows.Automation.TransformPatternIdentifiers.CanRotateProperty> is false.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="a25d7-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a25d7-144">See also</span></span>

- [<span data-ttu-id="a25d7-145">UI 自動化控制項模式概觀</span><span class="sxs-lookup"><span data-stu-id="a25d7-145">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="a25d7-146">支援 UI 自動化提供者的控制項模式</span><span class="sxs-lookup"><span data-stu-id="a25d7-146">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="a25d7-147">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="a25d7-147">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="a25d7-148">UI 自動化樹狀目錄概觀</span><span class="sxs-lookup"><span data-stu-id="a25d7-148">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="a25d7-149">使用 UI 自動化中的快取</span><span class="sxs-lookup"><span data-stu-id="a25d7-149">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)

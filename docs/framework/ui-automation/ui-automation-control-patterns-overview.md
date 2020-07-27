---
title: UI 自動化控制項模式概觀
description: 請參閱使用者介面自動化控制項模式的總覽。 控制項模式可讓您針對控制項的功能進行分類和公開，而不論類型或外觀為何。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns
- UI Automation, control patterns
ms.assetid: cc229b33-234b-469b-ad60-f0254f32d45d
ms.openlocfilehash: d0df24de4f8a877405dfecb6b0d245ff1caf0418
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163883"
---
# <a name="ui-automation-control-patterns-overview"></a>UI 自動化控制項模式概觀
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本概觀介紹 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 控制項模式。 控制項模式提供一種方式，分類及公開與控制項類型或控制項外觀無關的控制項功能。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 使用控制項模式來代表通用控制項的行為。 例如，您可以使用叫用控制項模式，用於可以叫用 (例如按鈕) 的控制項；也可以使用捲軸控制項模式，用於捲軸控制項 (例如清單方塊、清單檢視或下拉式方塊)。 因為每個控制項模式都代表個別的功能，所以可以結合起來，用以描述特定控制項所支援的完整功能集。  
  
> [!NOTE]
> 彙總控制項以可提供 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 用於父系所公開功能的子控制項所有建立，這應該實作通常會與每個子控制項相關聯的所有控制項模式。 然後相同的控制項模式便不需要由子控制項所實作。  
  
<a name="uiautomation_control_pattern_includes"></a>
## <a name="ui-automation-control-pattern-components"></a>使用者介面自動化控制項模式元件  
 控制項模式支援定義可在控制項中使用個別功能所需的方法、屬性、事件和關聯性。  
  
- 使用者介面自動化項目和其父系、子系和同層級之間的關聯性描述 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構內的項目結構。  
  
- 這些方法可以讓使用者介面自動化用戶端操作此控制項。  
  
- 屬性和事件提供控制項模式功能以及控制項狀態的相關資訊。  
  
 控制項模式與與 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元件物件模型（COM）物件相關聯的 as 介面。 在 COM 中，您可以查詢物件以詢問支援哪些介面，然後使用這些介面來存取功能。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，使用者介面自動化用戶端可以詢問控制項支援何種控制項模式，然後透過支援的控制項模式所公開的屬性、方法、事件和結構與其互動。 例如，對於多行編輯方塊，使用者介面自動化提供者可實作 <xref:System.Windows.Automation.Provider.IScrollProvider>。 當用戶端知道 <xref:System.Windows.Automation.AutomationElement> 支援 <xref:System.Windows.Automation.ScrollPattern> 控制項模式時，它便可以使用該控制項模式所公開的屬性、方法和事件來操作控制項，或存取此控制項的相關資訊。  
  
<a name="uiautomation_control_pattern_client_provider"></a>
## <a name="ui-automation-providers-and-clients"></a>使用者介面自動化提供者和用戶端  
 使用者介面自動化提供者實作控制項模式來公開此控制項所支援特定功能的適當行為。  
  
 使用者介面自動化用戶端存取 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制模式類別的方法和屬性，並使用它們來取得 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]的相關資訊，或操作 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]。 這些控制項模式類別位於 <xref:System.Windows.Automation> 命名空間 (例如 <xref:System.Windows.Automation.InvokePattern> 和 <xref:System.Windows.Automation.SelectionPattern>)。  
  
 用戶端使用 <xref:System.Windows.Automation.AutomationElement> 方法（例如 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> 或 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType> ）或 common LANGUAGE runtime （CLR）存取子來存取 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 模式的屬性。 每個控制項模式類別都有一個欄位成員（例如， <xref:System.Windows.Automation.InvokePattern.Pattern?displayProperty=nameWithType> 或 <xref:System.Windows.Automation.SelectionPattern.Pattern?displayProperty=nameWithType> ），可識別該控制項模式，而且可以當做參數傳遞至 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 或， <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 以取得的該模式 <xref:System.Windows.Automation.AutomationElement> 。  
  
<a name="uiautomation_control_patterns_dynamic"></a>
## <a name="dynamic-control-patterns"></a>動態控制項模式  
 有些控制項不一定支援一組相同的控制項模式。 當控制項模式可用於使用者介面自動化用戶端時，就可視為受支援。 例如，只有當多行編輯方塊包含的文字超出可檢視區域內可顯示的行數時，才會啟用垂直捲動。 移除足夠的文字，因而不再需要捲動之後，捲動便會停用。 此範例中，ScrollPattern 控制項模式會根據控制項 (編輯方塊中有多少文字) 的目前狀態，受到動態支援。  
  
<a name="Control_Pattern_Classes_and_Interfaces"></a>
## <a name="control-pattern-classes-and-interfaces"></a>控制項模式類別和介面  
 下表描述 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制模式。 這個表格也列出使用者介面自動化用戶端用來存取控制模式的類別，以及使用者介面自動化提供者用來實作這些類別的介面。  
  
|控制項模式類別|提供者介面|描述|  
|---------------------------|------------------------|-----------------|  
|<xref:System.Windows.Automation.DockPattern>|<xref:System.Windows.Automation.Provider.IDockProvider>|用於可停駐在停駐容器中的控制項。 例如工具列或工具板。|  
|<xref:System.Windows.Automation.ExpandCollapsePattern>|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|用於可展開或摺疊的控制項。 例如，應用程式中的功能表項目，像是 [檔案] **** 功能表。|  
|<xref:System.Windows.Automation.GridPattern>|<xref:System.Windows.Automation.Provider.IGridProvider>|用於支援格線功能 (例如調整大小及移動至指定的儲存格) 的控制項。 例如，Windows Explorer 中的大型圖示視圖，或 Microsoft Word 中沒有標頭的簡單資料表。|  
|<xref:System.Windows.Automation.GridItemPattern>|<xref:System.Windows.Automation.Provider.IGridItemProvider>|用於格線中有儲存格的控制項。 個別儲存格應該支援 GridItem 模式。 例如，Microsoft Windows Explorer 詳細資料檢視中的每個儲存格。|  
|<xref:System.Windows.Automation.InvokePattern>|<xref:System.Windows.Automation.Provider.IInvokeProvider>|用於可以叫用的控制項，例如按鈕。|  
|<xref:System.Windows.Automation.MultipleViewPattern>|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|用於可以在相同資訊、資料或子系的集合中，切換多種表示方式的控制項。 例如，清單檢視控制項，資料就在縮圖、並排顯示、圖示、清單或詳細資料檢視中。|  
|<xref:System.Windows.Automation.RangeValuePattern>|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|用於範圍值可以套用至控制項的控制項。 例如，包含年份之微調控制項的範圍可能是 1900 到 2010，而另一個代表月份的微調控制項的範圍值則是 1 至 12。|  
|<xref:System.Windows.Automation.ScrollPattern>|<xref:System.Windows.Automation.Provider.IScrollProvider>|用於可捲動的控制項。 例如，具有捲軸，且當包含的資訊超出控制項可檢視區中可顯示的範圍時，捲軸即成為作用中的控制項。|  
|<xref:System.Windows.Automation.ScrollItemPattern>|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|用於在可捲動的清單中具有個別項目的控制項。 例如，在捲動清單中 (例如下拉式方塊控制項) 有個別項目的清單控制項。|  
|<xref:System.Windows.Automation.SelectionPattern>|<xref:System.Windows.Automation.Provider.ISelectionProvider>|用於選取容器控制項。 例如清單方塊及下拉式方塊。|  
|<xref:System.Windows.Automation.SelectionItemPattern>|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|用於選取容器控制項 (例如清單方塊及下拉式方塊) 中的個別項目。|  
|<xref:System.Windows.Automation.TablePattern>|<xref:System.Windows.Automation.Provider.ITableProvider>|用於有格線以及標題資訊的控制項。 例如，Microsoft Excel 工作表。|  
|<xref:System.Windows.Automation.TableItemPattern>|<xref:System.Windows.Automation.Provider.ITableItemProvider>|用於表格中的項目。|  
|<xref:System.Windows.Automation.TextPattern>|<xref:System.Windows.Automation.Provider.ITextProvider>|用於公開文字資訊的編輯控制項及文件。|  
|<xref:System.Windows.Automation.TogglePattern>|<xref:System.Windows.Automation.Provider.IToggleProvider>|用於可切換狀態的控制項。 例如，核取方塊及可勾選的功能表項目。|  
|<xref:System.Windows.Automation.TransformPattern>|<xref:System.Windows.Automation.Provider.ITransformProvider>|用於可以調整大小、移動和旋轉的控制項。 轉換控制項模式通常使用於設計工具、表單、圖形編輯器，以及繪圖應用程式。|  
|<xref:System.Windows.Automation.ValuePattern>|<xref:System.Windows.Automation.Provider.IValueProvider>|允許用戶端對不支援範圍值的控制項，取得或設定一個值。 例如日期時間選擇器。|  
|<xref:System.Windows.Automation.WindowPattern>|<xref:System.Windows.Automation.Provider.IWindowProvider>|公開視窗特定的資訊 (Microsoft Windows 作業系統的基本概念)。 Windows 控制項的範例包括最上層應用程式視窗（Microsoft Word、Microsoft Windows Explorer 等等）、多重文件介面（MDI）子視窗和對話方塊。|  
  
## <a name="see-also"></a>另請參閱

- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
- [UI 自動化用戶端的控制項模式對應](control-pattern-mapping-for-ui-automation-clients.md)
- [UI 自動化概觀](ui-automation-overview.md)
- [用戶端的 UI 自動化屬性](ui-automation-properties-for-clients.md)
- [用戶端的 UI 自動化事件](ui-automation-events-for-clients.md)

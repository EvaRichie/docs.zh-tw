---
title: MenuItem 控制項類型的 UI 自動化支援
description: 取得 MenuItem 控制項類型的 UI 自動化支援的相關資訊。 瞭解必要的樹狀結構、屬性、控制項模式和事件。
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Menu Item
- Menu Item control type
- UI Automation, Menu Item control type
ms.assetid: 54bce311-3d23-40b9-ba90-1bdbdaf8fbba
ms.openlocfilehash: 248fdacee42c3a67c6c3b2d5792b774dfdc8408f
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166015"
---
# <a name="ui-automation-support-for-the-menuitem-control-type"></a>MenuItem 控制項類型的 UI 自動化支援

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。

本主題提供 MenuItem 類型的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 支援相關資訊。 其中說明控制項的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 樹狀結構，並提供 MenuItem 類型的必要屬性和控制項模式。

功能表控制項可將命令和事件處理常式的關聯項目以階層方式組織。 在典型的 Microsoft Windows 應用程式中，功能表列會包含數個功能表項目 **（例如 [** 檔案]、[**編輯**] 和 [**視窗]**），而每個功能表項目都會顯示一個功能表。 功能表又包含一組功能表項目 (例如 [開新檔案] ****、[開啟舊檔] **** 和 [關閉檔案] ****)，這些項目可展開顯示更多的功能表項目，或在按一下時可執行特定的動作。 功能表項目可裝載於功能表、功能表列或工具列中。

下列章節會定義 MenuItem 類型所需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、屬性、控制項模式和事件。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]需求適用于所有清單控制項，不論是 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 、Win32 或 Windows Forms。

<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>必要的使用者介面自動化樹狀結構

下表描述與功能表項目控制項相關之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視和內容檢視，並說明各檢視中可包含的內容。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的詳細資訊，請參閱 [UI Automation Tree Overview](ui-automation-tree-overview.md)。

|控制項檢視|內容檢視|
|------------------|------------------|
|MenuItem 的「說明」<br /><br /> <ul><li>功能表 ([說明] 功能表項目的子功能表)<br /><br /> <ul><li>MenuItem 的「說明主題」</li><li>MenuItem 的「關於記事本」</li></ul></li></ul>|MenuItem 的「說明」<br /><br /> -MenuItem "說明主題"<br />-MenuItem 「關於記事本」|

在功能表項目控制項的控制項檢視中， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構顯示如上。 請**注意，已包含 [說明**] 功能表項目，以便更清楚地說明一般功能表至子功能表階層中的結構。

在內容檢視中， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構沒有功能表，因為它並未傳達任何有意義的資訊給使用者。

<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>必要的使用者介面自動化屬性

下表列出 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性，其值或定義與功能表項目控制項特別有關。 如需屬性的詳細資訊 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ，請參閱[用戶端的 UI 自動化屬性](ui-automation-properties-for-clients.md)。

|屬性|值|描述|
|--------------|-----------|-----------------|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|請參閱備註。|此屬性的值在應用程式中的所有控制項都不得重複。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|請參閱備註。|包含整個控制項的最外層矩形。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|請參閱備註。|如果有週框即受支援。 如果週框中沒有任何可點選的點，而且您執行的是特殊化點擊測試，則會覆寫並提供可點選的點。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|請參閱備註。|如果控制項可接收鍵盤焦點，就必定支援此屬性。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|請參閱備註。|功能表項目控制項會包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的內容檢視中，而且會自行加上名稱標籤。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|沒有標籤。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|MenuItem|此值與所有使用者介面架構的值相同。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「功能表項目」|對應到 MenuItem 控制項類型的當地語系化字串。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|此功能表項目控制項一律不包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的內容檢視中。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|此功能表項目控制項一律包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視中。|

<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>必要的使用者介面自動化控制項模式

下表列出功能表項目控制項必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制項模式。 如需控制項模式的詳細資訊，請參閱 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)。

|控制項模式屬性|支援|注意|
|------------------------------|-------------|-----------|
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|相依|如果可以展開或摺疊控制項，則實作 <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>。|
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|相依|如果控制項執行單一動作或命令，則實作 <xref:System.Windows.Automation.Provider.IInvokeProvider>。|
|<xref:System.Windows.Automation.Provider.IToggleProvider>|相依|如果控制項是可以開啟或關閉的選項，則實作 <xref:System.Windows.Automation.Provider.IToggleProvider>。|
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|相依|如果控制項可用來從功能表項目的選項清單進行選取，則實作 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>。|

<a name="UI_Automation_Events_for_Menu_Item"></a>

## <a name="ui-automation-events-for-menu-item"></a>功能表項目的使用者介面自動化事件

下表列出與功能表項目控制項相關聯的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 事件。

|事件|支援|說明|
|-----------|-------------|-----------------|
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|相依|如果控制項支援叫用控制項模式，則必須引發此一事件。|
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> 屬性變更事件。|相依|如果控制項支援切換控制項模式，則必須引發此一事件。|
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 屬性變更事件。|相依|如果控制項支援展開摺疊控制項模式，則必須引發此一事件。|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|相依|無。|

<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>必要的使用者介面自動化事件

下表列出所有功能表項目控制項都必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 如需 [UI Automation Events Overview](ui-automation-events-overview.md)事件的詳細資訊，請參閱

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支援/值|注意|
|---------------------------------------------------------------------------------|--------------------|-----------|
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|相依|None|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|相依|None|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|相依|None|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|相依|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 屬性變更事件。|相依|None|
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> 屬性變更事件。|相依|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必要|None|

<a name="Legacy_Issues"></a>

## <a name="legacy-issues"></a>舊版問題

只有在檢查 Win32 功能表項目時，才支援切換模式，並可透過程式設計方式決定是否需要支援切換模式。 由於 Win32 功能表項目不會公開是否能夠進行檢查，因此當未核取功能表項目時，將會支援叫用模式。 就算是應該只支援叫用模式的功能表項目，也會有一律支援叫用模式的例外狀況。 如此一來，用戶端就不會對支援叫用模式 (未勾選功能表項目時) 的項目一旦變成勾選時，是否就不再支援該模式的問題感到困惑。

## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Automation.ControlType.MenuItem>
- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [UI 自動化控制項類型概觀](ui-automation-control-types-overview.md)
- [UI 自動化概觀](ui-automation-overview.md)

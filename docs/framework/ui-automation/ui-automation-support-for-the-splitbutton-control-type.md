---
title: SplitButton 控制項類型的 UI 自動化支援
description: 取得 SplitButton 控制項類型的 UI 自動化支援的相關資訊。 瞭解必要的樹狀結構、屬性、控制項模式和事件。
ms.date: 03/30/2017
helpviewer_keywords:
- Split Button control type
- control types, Split Button
- UI Automation, Split Button control type
ms.assetid: 14b05ccf-bcd8-4045-9bae-f7679cd98711
ms.openlocfilehash: e32d10f71eaab491f691e4be0529087af9102f93
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163820"
---
# <a name="ui-automation-support-for-the-splitbutton-control-type"></a>SplitButton 控制項類型的 UI 自動化支援
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題提供 SplitButton 控制項類型的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 支援相關資訊。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，控制項類型是一組控制項條件，控制項必須符合條件才能使用 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 屬性。 這些條件包括 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性值和控制項模式的特定方針。  
  
 使用分割按鈕控制項，可以在控制項上執行動作並且展開控制項查看其他可執行動作的清單。  
  
 下列章節會定義 SplitButton 控制項類型所需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、屬性、控制項模式和事件。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]需求適用于所有分割按鈕控制項，不論是 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 、Win32 或 Windows Forms。  
  
## <a name="required-ui-automation-tree-structure"></a>必要的使用者介面自動化樹狀結構  
 下表描述分割按鈕控制項之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視和內容檢視，並說明各檢視中可包含的內容。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的詳細資訊，請參閱 [UI Automation Properties Overview](ui-automation-tree-overview.md)需求都適用於所有文件控制項。  
  
|控制項檢視|內容檢視|  
|------------------|------------------|  
|SplitButton<br /><br /> <ul><li>Image (0 或 1)</li><li>文字 (0 或 1)</li><li>按鈕 (1 或 2)<br /><br /> <ul><li>功能表 (0 或 1；顯示為支援 ExpandCollapse 模式的按鈕子項目)</li><li>MenuItem (1 個以上)</li></ul></li></ul>|SplitButton<br /><br /> -MenuItem （1到多個）|  
  
## <a name="required-ui-automation-properties"></a>必要的使用者介面自動化屬性  
 下表列示 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性，其值或定義與分割按鈕控制項特別有關。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性的詳細資訊，請參閱 [UI Automation Properties for Clients](ui-automation-properties-for-clients.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性|值|注意|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|請參閱備註。|此屬性的值在應用程式中的所有控制項都不得重複。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|請參閱備註。|包含整個控制項的最外層矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|請參閱備註。|如果有週框即受支援。 如果週框中沒有任何可點選的點，而且您執行的是特殊化點擊測試，則會覆寫並提供可點選的點。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|請參閱備註。|如果控制項可接收鍵盤焦點，就必定支援此屬性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「上一步」|分割按鈕控制項的名稱會顯示在按鈕上。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Null|分割按鈕控制項沒有靜態文字標籤。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|SplitButton|此值與所有使用者介面架構的值相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「分割按鈕」|對應到 SplitButton 控制項類型的當地語系化字串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|請參閱備註。|說明文字可能指出啟動分割按鈕的結果，而這通常是透過工具提示顯示的相同類型資訊。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|分割按鈕控制項包含給使用者的資訊。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|使用者可以看到分割按鈕控制項。|  
  
## <a name="required-ui-automation-control-patterns"></a>必要的使用者介面自動化控制項模式  
 下表列出所有分割按鈕控制項必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制項模式。 如需控制項模式的詳細資訊，請參閱 [F:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty](ui-automation-control-patterns-overview.md)。  
  
|控制項模式|支援|注意|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|必要|分割按鈕一定要有與叫用相關聯的預設動作。|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|必要|分割按鈕一律要能展開選項清單。|  
  
## <a name="required-ui-automation-events"></a>必要的使用者介面自動化事件  
 下表列出所有分割按鈕控制項都必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 如需 [UI Automation Events Overview](ui-automation-events-overview.md)事件的詳細資訊，請參閱  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支援|注意|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|必要|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 屬性變更事件。|必要|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 屬性變更事件。|必要|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 屬性變更事件。|必要|None|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 屬性變更事件。|必要|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必要|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必要|None|  
  
## <a name="splitbutton-control-example"></a>SplitButton 控制項範例  
 下圖顯示在資料格控制項中的 SplitButton 控制項類型。  
  
 ![分割按鈕](./media/uiauto-splitbutton-detailed.gif "uiauto_splitbutton_detailed")  
  
 與資料格和分割按鈕控制項相關、使用者介面自動化樹狀結構的控制項檢視和內容檢視顯示如下。 每個自動化項目的控制項模式顯示在括號中。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 控制項檢視|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 內容檢視|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|<ul><li>SplitButton "名稱" (Invoke, ExpandCollapse)</li><li>Button "更多選項" (Invoke)<br /><br /> <ul><li>功能表</li><li>MenuItem</li><li>…</li></ul></li></ul>|<ul><li>SplitButton "名稱" (Invoke, ExpandCollapse)</li><li>Button "更多選項" (Invoke)<br /><br /> <ul><li>功能表</li><li>MenuItem</li><li>…</li></ul></li></ul>|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Automation.ControlType.SplitButton>
- [UI 自動化控制項類型概觀](ui-automation-control-types-overview.md)
- [UI 自動化概觀](ui-automation-overview.md)

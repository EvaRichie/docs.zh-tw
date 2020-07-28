---
title: DataGrid 控制項類型的 UI 自動化支援
description: 取得 DataGrid 控制項類型的 UI 自動化支援的相關資訊。 瞭解必要的樹狀結構、屬性、控制項模式和事件。
ms.date: 03/30/2017
helpviewer_keywords:
- Data Grid control type
- control types, Data Grid
- UI Automation, Data Grid control type
ms.assetid: a3db4a3f-feb5-4e5f-9b42-aae7fa816e8a
ms.openlocfilehash: 13f265e414383e646f3e138feb890661fa01e2de
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87167997"
---
# <a name="ui-automation-support-for-the-datagrid-control-type"></a>DataGrid 控制項類型的 UI 自動化支援
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題提供 DataGrid 控制項類型的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 支援相關資訊。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，控制項類型是一組控制項條件，控制項必須符合條件才能使用 `ControlType` 屬性。 這些條件包括 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性值和控制項模式的特定方針。  
  
 DataGrid 控制項類型可讓使用者易於使用包含以資料行所表示之中繼資料的項目。 資料格控制項具有項目資料列和關於這些項目的資訊資料行。 Microsoft Vista 檔案總管中的「清單檢視」控制項即是支援 DataGrid 控制項類型的範例。  
  
 下列章節會定義 DataGrid 控制項類型所需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、屬性、控制項模式和事件。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]需求適用于所有資料格控制項，不論是 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 、Win32 或 Windows Forms。  
  
## <a name="required-ui-automation-tree-structure"></a>必要的使用者介面自動化樹狀結構  
 下表描述與資料格項目控制項相關之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視和內容檢視，並說明各檢視中可包含的內容。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的詳細資訊，請參閱 [UI Automation Properties Overview](ui-automation-tree-overview.md)需求都適用於所有文件控制項。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 控制項檢視|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 內容檢視|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|DataGrid<br /><br /> <ul><li>標頭 (0、1 或 2)<br /><br /> <ul><li>HeaderItem (行數或列數)</li></ul></li><li>DataItem (0 或更多；可以結構化為階層)</li></ul>|DataGrid<br /><br /> -DataItem （0或更多; 可以在階層結構中）|  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必要的使用者介面自動化屬性  
 下表列出屬性，其值或定義與資料格項目控制項特別有關。 如需屬性的詳細資訊 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ，請參閱[用戶端的 UI 自動化屬性](ui-automation-properties-for-clients.md)。  
  
|屬性|值|注意|  
|--------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|請參閱備註。|此屬性的值在應用程式中的所有控制項都不得重複。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|請參閱備註。|包含整個控制項的最外層矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|請參閱備註。|如果有週框即受支援。 如果週框中沒有任何可點選的點，而且您執行的是特殊化點擊測試，則會覆寫並提供可點選的點。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|DataGrid|此值與所有使用者介面架構的值相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|這個屬性的值必須一律是 True。 這表示核取方塊控制項一律應包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的內容檢視中。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|這個屬性的值必須一律是 True。 這表示核取方塊控制項一律應包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視中。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|請參閱備註。|如果控制項可接收鍵盤焦點，就必定支援此屬性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|請參閱備註。|如果有靜態文字標籤，那麼這個屬性必須公開該控制項的參考。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「資料格」|對應到 DataGrid 控制項類型的當地語系化字串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|請參閱備註。|資料格控制項通常會從靜態文字標籤取得其 `Name` 屬性值。 如果沒有靜態文字標籤，應用程式開發人員就必須指派 `Name` 屬性的值。 `Name` 屬性的值絕不能是編輯控制項的文字內容。|  
  
## <a name="required-ui-automation-control-patterns"></a>必要的使用者介面自動化控制項模式  
 下表列出所有資料格控制項必須支援的控制項模式。 如需控制項模式的詳細資訊，請參閱 [F:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty](ui-automation-control-patterns-overview.md)。  
  
|控制項模式|支援|注意|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|是|資料格控制項本身一律支援方格控制項模式，因為其所包含的項目具有在格線中配置的中繼資料。|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|相依|資料格可捲動與否，會視內容以及是否有捲軸而定。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|相依|資料格可選取與否，視內容而定。|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|是|資料格控制項在其樹狀子結構一律會有標題，因此必須支援表格控制項模式。|  
  
 資料格容器內的資料項目至少會支援：  
  
- 選取項目控制項模式 (如果資料格可供選取)  
  
- 捲動項目控制項模式 (如果資料格可供捲動)  
  
- 方格項目控制項模式  
  
- Table Item 控制項模式  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必要的使用者介面自動化事件  
 下表列出所有資料項目控制項都必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 如需事件的詳細資訊，請參閱 [UI Automation Events Overview](ui-automation-events-overview.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支援|注意|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必要|無|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 屬性變更事件。|必要|無|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 屬性變更事件。|必要|無|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 屬性變更事件。|必要|無|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|相依|無|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必要|無|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> 屬性變更事件。|相依|無|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 屬性變更事件。|相依|如果此控制項支援捲動模式，就必須支援這個事件。|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|必要|無|  
  
## <a name="date-grid-control-type-example"></a>日期方格控制項類型範例  
 下圖顯示實作 DataGrid 控制項類型的清單檢視控制項。  
  
 ![包含兩個資料項目之 List View 控制項的圖形](./media/uiauto-data-grid-detailed.GIF "uiauto_data_grid_detailed")  
  
 與清單檢視控制項相關之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視和內容檢視顯示如下。 每個自動化項目的控制項模式顯示在括號中。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 控制項檢視|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構 - 內容檢視|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|<ul><li>DataGrid (Table, Grid, Selection)</li><li>頁首<br /><br /> <ul><li>HeaderItem "Name" (Invoke)</li><li>HeaderItem "Date Modified" (Invoke)</li><li>HeaderItem "Size" (Invoke)</li></ul></li><li>群組 "Contoso" （TableItem，GridItem，SelectionItem，Table *，Grid \* ）<br /><br /> <ul><li>DataItem "Accounts Receivable.doc" （SelectionItem、Invoke、TableItem \* 、GridItem \* ）</li><li>DataItem "Accounts Payable.doc" （SelectionItem、Invoke、TableItem \* 、GridItem \* ）</li></ul></li></ul>|<ul><li>DataGrid (Table, Grid, Selection)</li><li>群組 "Contoso" （TableItem，GridItem，SelectionItem，Table *，Grid \* ）<br /><br /> <ul><li>DataItem "Accounts Receivable.doc" （SelectionItem、Invoke、TableItem \* 、GridItem \* ）</li><li>DataItem "Accounts Payable.doc" （SelectionItem、Invoke、TableItem \* 、GridItem \* ）</li></ul></li></ul>|  
  
 \*上一個範例顯示包含多個控制項層級的 DataGrid。 Group ("Contoso") 控制項包含兩個 DataItem 控制項 ("Accounts Receivable.doc" 和 "Accounts Payable.doc")。 DataGrid/GridItem 對組與另一層級的對組無關， Group 底下的 DataItem 控制項也可以公開為 ListItem 控制項類型，如此可以更清楚將其表明為可選取的物件，而非僅是簡單的資料項目。 本範例不包含群組資料項目的子項目。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Automation.ControlType.DataGrid>
- [UI 自動化控制項類型概觀](ui-automation-control-types-overview.md)
- [UI 自動化概觀](ui-automation-overview.md)

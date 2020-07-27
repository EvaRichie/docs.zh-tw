---
title: Edit 控制項類型的 UI 自動化支援
description: 取得編輯控制項類型的 UI 自動化支援的相關資訊。 瞭解必要的樹狀結構、屬性、控制項模式和事件。
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Edit
- Edit control type
- UI Automation, Edit control type
ms.assetid: 6db9d231-c0a0-4e17-910e-ac80357f774f
ms.openlocfilehash: 6c404786d58cfcb4cc7dabd982eea33694b7cd0b
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87167939"
---
# <a name="ui-automation-support-for-the-edit-control-type"></a>Edit 控制項類型的 UI 自動化支援

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。

本主題提供編輯控制項類型的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 支援相關資訊。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，控制項類型是一組控制項條件，控制項必須符合條件才能使用 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 屬性。 這些條件包括 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的特定指導方針、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性值和控制項模式。

本主題提供編輯控制項類型之使用者介面自動化支援的相關資訊。

下列章節會定義編輯控制項類型所需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構、屬性、控制項模式和事件。 這些 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 需求適用于所有編輯控制項，不論是 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 、Win32 或 Windows Forms。

<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>必要的使用者介面自動化樹狀結構

下表描述編輯控制項之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視和內容檢視，並說明各檢視中可包含的內容。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的詳細資訊，請參閱 [UI Automation Properties Overview](ui-automation-tree-overview.md)需求都適用於所有文件控制項。

|控制項檢視|內容檢視|
|------------------|------------------|
|編輯|編輯|

因為實作編輯控制項類型的控制項在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視中是單行控制項，所以一律不會有捲軸。 在某些配置案例中，單行文字可能會換行。 編輯控制項類型最適合用於保存少量可編輯或可選取的文字。

<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>必要的使用者介面自動化屬性

下表列出 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性，其值或定義與編輯控制項特別有關。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性的詳細資訊，請參閱 [UI Automation Properties for Clients](ui-automation-properties-for-clients.md)。

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性|值|注意|
|------------------------------------------------------------------------------------|-----------|-----------|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|請參閱備註。|此屬性的值在應用程式中的所有控制項都不得重複。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|請參閱備註。|包含整個控制項的最外層矩形。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|請參閱備註。|編輯控制項必須有可點選的點，當使用者按一下滑鼠時，會將輸入焦點置於控制項的編輯部分。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|請參閱備註。|如果控制項可接收鍵盤焦點，就必定支援此屬性。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|請參閱備註。|編輯控制項的名稱通常是從靜態文字標籤產生的。 如果沒有靜態文字標籤，則必須由應用程式開發人員指定 `Name` 的屬性值。 `Name` 屬性不應該包含編輯控制項的文字內容。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|請參閱備註。|如果控制項有關聯的靜態文字標籤，則這個屬性必須公開該控制項的參考。 如果文字控制項是其他控制項的子元件，則將不會設定 `LabeledBy` 屬性。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|編輯|此值與所有 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 架構的值相同。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「編輯」|對應到編輯控制項類型的當地語系化字串。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|此編輯控制項一律包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的內容檢視。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|此編輯控制項一律包含在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>|請參閱備註。|包含密碼的編輯控制項必須設為 true。 如果編輯控制項包含密碼內容，則螢幕助讀程式可使用這個屬性來判斷在使用者輸入密碼時，是否應讀出所按的按鍵。|

<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns-and-properties"></a>必要的使用者介面自動化控制項模式和屬性

下表列出所有編輯控制項都必須支援的控制項模式。 如需控制項模式的詳細資訊，請參閱 [F:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty](ui-automation-control-patterns-overview.md)。

|控制項模式/控制項模式屬性|支援/值|注意|
|-----------------------------------------------|--------------------|-----------|
|<xref:System.Windows.Automation.Provider.ITextProvider>|相依|編輯控制項應支援文字控制項模式，因為詳細的文字資訊應一律可供用戶端使用。|
|<xref:System.Windows.Automation.Provider.IValueProvider>|相依|所有採用字串的編輯控制項都必須公開值模式。|
|<xref:System.Windows.Automation.Provider.IValueProvider.IsReadOnly%2A>|請參閱備註。|這個屬性必須設定，以表示控制項是否可擁有以程式設計方式設定的值，或是否可由使用者編輯。|
|<xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>|請參閱備註。|這個屬性將傳回編輯控制項的文字內容。 如果 `IsPasswordProperty` 設為 `true`，在收到要求時，這個屬性必須引發 `InvalidOperationException` 。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|相依|所有使用數值範圍的編輯控制項必須公開範圍值控制項模式。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Minimum%2A>|請參閱備註。|這個屬性必須是編輯控制項的內容可以設成的最小值。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Maximum%2A>|請參閱備註。|這個屬性必須是編輯控制項的內容可以設成的最大值。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.SmallChange%2A>|請參閱備註。|這個屬性必須指定該值可以設定的小數位數。 如果編輯只能使用整數，則 `SmallChangeProperty` 必須為 1。 如果編輯使用 1.0 到 2.0 之間的範圍，則 `SmallChangeProperty` 必須為 0.1。 如果編輯控制項使用 1.00 到 2.00 之間的範圍，則 `SmallChangeProperty` 必須為 0.001。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.LargeChange%2A>|`Null`|編輯控制項無須公開這個屬性。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Value%2A>|請參閱備註。|這個屬性將指定編輯控制項的數值內容。 若 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 用戶端在 `Minimum` 和 `Maximum` 屬性指定的範圍內設定了更精確的值，則 Value 屬性將自動捨入成最接近的接受值。|

<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>必要的使用者介面自動化事件

下表列示所有編輯控制項都必須支援的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 如需事件的詳細資訊，請參閱 [UI Automation Events Overview](ui-automation-events-overview.md)。

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支援|注意|
|---------------------------------------------------------------------------------|-------------|-----------|
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|必要|None|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|必要|None|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> 屬性變更事件。|必要|None|
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> 屬性變更事件。|相依|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 屬性變更事件。|永不|None|
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> 屬性變更事件。|相依|如果此控制項支援範圍值控制項模式，就必須支援這個事件。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必要|None|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必要|None|

## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Automation.ControlType.Edit>
- [UI 自動化控制項類型概觀](ui-automation-control-types-overview.md)
- [UI 自動化概觀](ui-automation-overview.md)

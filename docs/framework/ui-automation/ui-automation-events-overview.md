---
title: UI 自動化事件概觀
description: 請參閱 Microsoft 使用者介面自動化事件通知的總覽。 檢查事件種類、使用者介面自動化事件識別碼，以及使用者介面自動化事件引數。
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, providers
- UI Automation, events
- clients, UI Automation
- events, UI Automation
- providers, UI Automation
- UI Automation, clients
ms.assetid: 69eebd8b-39ed-40e7-93cc-4457c4caf746
ms.openlocfilehash: 4f51a31a433986822a9dba22bf8f17ade00bbb76
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168093"
---
# <a name="ui-automation-events-overview"></a>UI 自動化事件概觀
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 事件通知是輔助技術的重要功能，例如螢幕助讀程式和螢幕放大鏡。 這些 UI 自動化用戶端會追蹤 UI 自動化提供者在 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 發生情況時所引發的事件，並使用此資訊來通知使用者。  
  
 藉由允許提供者應用程式選擇性地引發事件來改善效率，取決於是否有用戶端訂閱那些事件或完全沒有，前提是沒有用戶端正在接聽任何事件。  
  
<a name="Types_of_Events"></a>
## <a name="types-of-events"></a>事件的類型  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件可分類如下。  
  
|事件|描述|  
|-----------|-----------------|  
|屬性變更|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 項目或控制項模式上的屬性變更時引發。 例如，如果用戶端需要監視應用程式的核取方塊控制項，則它可以註冊，以接聽 <xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A> 屬性上的屬性變更事件。 當選取或取消選取核取方塊控制項時，提供者會引發事件，而且用戶端可視需要採取動作。|  
|項目動作|[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中的變更是由於使用者或程式設計活動而產生時引發；例如，當按一下按鈕或透過 <xref:System.Windows.Automation.InvokePattern>叫用按鈕時。|  
|結構變更|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的結構變更時引發。 當新的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目在桌面上可以看見、隱藏不見或遭到移除時，結構即會變更。|  
|全域桌面變更|發生用戶端感興趣的全域動作時 (例如，焦點從一個項目移到另一個項目時，或當視窗關閉時) 引發。|  
  
 某些事件並不一定表示 UI 的狀態已經變更。 例如，如果使用者切換至文字輸入欄位，然後按一下按鈕以更新欄位，則即使使用者實際上並未變更文字，也會引發 `TextChangedEvent` 。 在處理事件時，用戶端應用程式可能需要在採取動作之前檢查是否有任何實際變更。  
  
 即使 UI 的狀態未變更，也可能引發下列事件。  
  
- `AutomationPropertyChangedEvent` (取決於已變更的屬性)  
  
- `ElementSelectedEvent`  
  
- `InvalidatedEvent`  
  
- `TextChangedEvent`  
  
<a name="UI_Automation_Event_Identifiers"></a>
## <a name="ui-automation-event-identifiers"></a>UI 自動化事件識別碼  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 事件是由 <xref:System.Windows.Automation.AutomationEvent> 物件識別。 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 屬性包含專門識別事件類型的值。  
  
 下表提供 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 的可能值，以及用於事件引數的類型。 請注意，用戶端和提供者所使用的識別項是來自不同類別的同名欄位。  
  
|用戶端識別項|提供者識別項|事件引數類型|  
|-----------------------|-------------------------|--------------------------|  
|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|  
|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionPattern.InvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.InvokePattern.InvokedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.LayoutInvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPattern.TextChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationPropertyChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationPropertyChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.StructureChangedEventArgs>|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.WindowClosedEventArgs>|  
  
<a name="UI_Automation_Event_Arguments"></a>
## <a name="ui-automation-event-arguments"></a>UI 自動化事件引數  
 下列類別會封裝事件引數。  
  
|類別|描述|  
|-----------|-----------------|  
|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|包含非同步載入內容的相關資訊，包括已完成的載入百分比。|  
|<xref:System.Windows.Automation.AutomationEventArgs>|包含不需要額外資料之簡單事件的相關資訊。|  
|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|包含輸入焦點從一個項目變更為另一個項目的相關資訊。 這種類型的事件是由 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 系統而不是提供者引發。|  
|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|包含項目或控制項模式之屬性值變更的相關資訊。|  
|<xref:System.Windows.Automation.StructureChangedEventArgs>|包含 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構中變更的相關資訊。|  
|<xref:System.Windows.Automation.WindowClosedEventArgs>|包含視窗關閉的相關資訊。|  
  
 所有事件引數類別都包含 <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A> 成員。 這個識別碼會封裝在 <xref:System.Windows.Automation.AutomationEvent>。  
  
 用來識別事件 <xref:System.Windows.Automation.AutomationEvent> 的物件是提供者從 <xref:System.Windows.Automation.AutomationElementIdentifiers> 中的欄位，以及控制模式識別碼類別 (例如 <xref:System.Windows.Automation.DockPatternIdentifiers>) 所取得。 對等欄位是用戶端應用程式從 <xref:System.Windows.Automation.AutomationElement> 中的欄位，以及控制模式類別 (例如 <xref:System.Windows.Automation.DockPattern>) 所取得。  
  
 如需事件識別碼的清單，請參閱 [UI Automation Events for Clients](ui-automation-events-for-clients.md)。  
  
## <a name="see-also"></a>另請參閱

- [用戶端的 UI 自動化事件](ui-automation-events-for-clients.md)
- [伺服器端 UI 自動化提供者實作](server-side-ui-automation-provider-implementation.md)
- [訂閱 UI 自動化事件](subscribe-to-ui-automation-events.md)

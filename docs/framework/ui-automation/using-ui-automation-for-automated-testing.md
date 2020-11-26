---
title: 使用 UI 自動化進行自動化測試
description: 閱讀概要說明如何使用消費者介面自動化作為架構，以在自動化測試案例中以程式設計方式存取。
ms.date: 03/30/2017
helpviewer_keywords:
- automated testing
- testing, UI Automation
- UI Automation, automated testing
ms.assetid: 3a0435c0-a791-4ad7-ba92-a4c1d1231fde
ms.openlocfilehash: 4b039fbbe636bd56afa25cb4b45605b09ab44662
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96237335"
---
# <a name="using-ui-automation-for-automated-testing"></a>使用 UI 自動化進行自動化測試

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本概觀說明 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 在自動化測試案例中做為程式設計存取的架構有何幫助。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 提供了一致的物件模型，可讓所有 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 架構透過可存取、輕鬆自動化的方式來公開複雜、豐富的功能。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 已開發為 Microsoft Active Accessibility 的後續版本。 Active Accessibility 是現有的架構，其設計目的是要提供可供存取控制項和應用程式的解決方案。 Active Accessibility 不是以測試自動化為考慮而設計，因為它會因為存取範圍和自動化的類似需求而演進至該角色。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]除了提供更精細的協助工具方案之外，還特別設計來提供穩固的自動化測試功能。 例如，Active Accessibility 依賴單一介面來公開 UI 的相關資訊，並收集產品所需的資訊; [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 分隔兩個模型。  
  
 若要實作 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 讓它成為跟自動化測試工具一樣有用，就需要有提供者和用戶端。 消費者介面自動化提供者是 Microsoft Word、Excel 和其他協力廠商應用程式或以 Microsoft Windows 作業系統為基礎的控制項等應用程式。 使用者介面自動化用戶端則包括自動化測試指令碼和輔助技術應用程式。  
  
> [!NOTE]
> 本概觀的用意是展示 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]全新和改善的自動化測試功能， 並不會提供協助工具功能的資訊，除非必要，否則不會說明協助工具。  
  
## <a name="ui-automation-in-a-provider"></a>提供者中的使用者介面自動化  

 若要讓 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 自動化，應用程式或控制項的開發人員必須查看使用者在使用標準鍵盤和滑鼠互動時，可以在 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 物件上執行哪些動作。  
  
 一旦識別出這些按鍵動作，就應該在控制項上實作對應的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制項模式 (也就是可鏡像 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目功能和行為的控制項模式)。 例如，與下拉式方塊控制項 (例如執行對話方塊) 的使用者互動一般會涉及到展開及摺疊下拉式方塊，以隱藏或顯示項目清單、從該清單中選取項目，或透過鍵盤輸入加入新值。  
  
> [!NOTE]
> 藉由其他協助工具模式，開發人員必須直接從個別按鈕、功能或其他控制項收集資訊。 可惜的是，每種控制項類型都有許多次要變化。 換句話說，即使按鈕的十個變化全都以相同方式運作，並執行相同功能，仍必須全都視為唯一的控制項。 無法得知這些控制項是否功能對等。 開發控制項模式的目的就是為了呈現這些常見的控制項行為。 如需詳細資訊，請參閱 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)。  
  
### <a name="implementing-ui-automation"></a>實作使用者介面自動化  

 如上所述，如果沒有 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]所提供的一致模型，測試工具和開發人員就必須知道架構特定的資訊，才能公開該架構中控制項的屬性和行為。 由於 Windows 作業系統中的任何一次都可能有數個不同的 UI 架構，包括 Win32、Windows Forms 和 Windows Presentation Foundation (WPF) ，因此使用看似類似的控制項測試多個應用程式可能是很困難的工作。 例如，下表列出擷取與按鈕控制項相關名稱 (或文字) 時所需的架構特定屬性名稱，並顯示單一對等的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性。  
  
|使用者介面自動化控制項類型|使用者介面架構|架構特定的屬性|使用者介面自動化屬性|  
|--------------------------------|------------------|---------------------------------|----------------------------|  
|按鈕|Windows Presentation Foundation|Content|NameProperty|  
|按鈕|Win32|標題|NameProperty|  
|映像|HTML|alt|NameProperty|  
  
 使用者介面自動化提供者會負責將其控制項的架構特定屬性對應至對等的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性。  
  
 如需在提供者中實作 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的詳細資訊，請參閱 [UI Automation Providers for Managed Code](ui-automation-providers-for-managed-code.md)。 如需實作控制項模式的詳細資訊，請參閱 [UI Automation Control Patterns](ui-automation-control-patterns.md) 和 [UI Automation Text Pattern](ui-automation-text-pattern.md)。  
  
## <a name="ui-automation-in-a-client"></a>用戶端中的使用者介面自動化  

 許多自動化測試工具和案例的目標是提供一致、可重複的使用者介面操作。 這可能涉及到特定控制項單元測試，一直到在一組控制項上反覆一連串動作的測試指令碼錄製及播放。  
  
 自動化應用程式的困難在於測試與動態目標的同步處理。 例如，清單方塊控制項 (例如 Windows 工作管理員中所包含的控制項) 會顯示目前執行中應用程式的清單。 因為該清單方塊中的項目是在測試應用程式的控制之外動態更新的，所以嘗試以任何一致性來重複清單方塊中的特定項目選取是不可能的。 在測試應用程式控制之外的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中嘗試簡單的焦點變更時，也會發生類似問題。  
  
### <a name="programmatic-access"></a>程式設計存取  

 程式設計存取能夠透過程式碼，模擬由傳統滑鼠和鍵盤輸入所公開的任何互動和體驗。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 透過五個元件啟用程式設計存取：  
  
- [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構有助於巡覽 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]的結構。 此樹狀結構是由 hWnd 的集合建置而成。 如需詳細資訊，請參閱 [UI Automation Tree Overview](ui-automation-tree-overview.md)。  
  
- 自動化項目是 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]中的個別元件。 這些元件通常比 hWnd 更細微。 如需詳細資訊，請參閱 [UI Automation Control Types Overview](ui-automation-control-types-overview.md)。  
  
- 自動化屬性提供了關於 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目的特定資訊。 如需詳細資訊，請參閱 [UI Automation Properties Overview](ui-automation-properties-overview.md)。  
  
- 控制項模式定義控制項功能的特定層面，可以包含屬性、方法、事件和結構資訊。 如需詳細資訊，請參閱 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)。  
  
- 自動化事件會提供事件通知和資訊。 如需詳細資訊，請參閱 [UI Automation Events Overview](ui-automation-events-overview.md)。  
  
### <a name="key-properties-for-test-automation"></a>測試自動化的主要屬性  

 在 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中唯一識別並後續找出任何控制項的能力，可以為要在該 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]上操作的自動化測試應用程式提供基礎。 用戶端和提供者使用數個 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 屬性來輔助此項功能。  
  
#### <a name="automationid"></a>AutomationID  

 在同層級之間以唯一的方式識別自動化項目。 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 並未當地語系化，與發行多國語言版本的產品時通常會當地語系化的屬性 (例如 <xref:System.Windows.Automation.AutomationElement.NameProperty> ) 不同。 請參閱 [Use the AutomationID Property](use-the-automationid-property.md)。  
  
> [!NOTE]
> <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 不保證整個自動化樹狀結構中的唯一識別。 例如，應用程式可能包含具有多個最上層功能表項目的功能表控制項，因此也會有多個子功能表項目。 這些次要功能表項目可由「項目 1」、「項目 2」、「項目 3」(依此類推) 之類的一般配置識別，因此最上層功能表項目的子系可以有重複識別項。  
  
#### <a name="controltype"></a>ControlType  

 識別自動化項目所代表的控制項類型。 重要的資訊可以從對控制項類型的了解加以推斷。 請參閱 [UI Automation Control Types Overview](ui-automation-control-types-overview.md)。  
  
#### <a name="nameproperty"></a>NameProperty  

 這是識別或說明控制項的文字字串。 因為<xref:System.Windows.Automation.AutomationElement.NameProperty> 可以當地語系化，所以應小心使用。 請參閱 [UI Automation Properties Overview](ui-automation-properties-overview.md)。  
  
### <a name="implementing-ui-automation-in-a-test-application"></a>在測試應用程式中實作使用者介面自動化  
  
|||  
|-|-|  
|加入使用者介面自動化參考。|以下列出使用者介面自動化用戶端所需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] DLL。<br /><br /> -UIAutomationClient.dll 提供用戶端 Api 的存取權 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。<br />-UIAutomationClientSideProvider.dll 提供自動化 Win32 控制項的功能。 請參閱 [UI Automation Support for Standard Controls](ui-automation-support-for-standard-controls.md)。<br />-UIAutomationTypes.dll 提供對中所定義之特定類型的存取 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。|  
|加入 <xref:System.Windows.Automation> 命名空間。|這個命名空間包含使用者介面自動化用戶端使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 功能 (文字處理除外) 時需要的所有要件。|  
|加入 <xref:System.Windows.Automation.Text> 命名空間。|這個命名空間包含使用者介面自動化用戶端使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 文字處理時需要的所有要件。|  
|尋找想要的控制項|自動化測試指令碼會在自動化樹狀結構中尋找代表相關控制項的使用者介面自動化項目。<br /><br /> 您可透過多種方式使用程式碼取得使用者介面自動化項目。<br /><br /> - [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 使用語句來查詢 <xref:System.Windows.Automation.Condition> 。 通常會在此使用語言中性的 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 。 **注意：**  您 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 可以使用可將控制項屬性組成 Inspect.exe 的工具來取得 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。 <br /><br /> -使用 <xref:System.Windows.Automation.TreeWalker> 類別來跨越整個 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構或其子集。<br />-追蹤焦點。<br />-使用控制項的 hWnd。<br />-使用螢幕位置，例如滑鼠游標的位置。<br /><br /> 請參閱 [Obtaining UI Automation Elements](obtaining-ui-automation-elements.md)|  
|取得控制項模式|控制項模式會公開功能類似之控制項的一般行為。<br /><br /> 找到需要測試的控制項之後，自動化測試指令碼會從這些使用者介面自動化項目中取得想要的控制項模式。 例如，代表一般按鈕功能的 <xref:System.Windows.Automation.InvokePattern> 控制項模式，或是代表視窗功能的 <xref:System.Windows.Automation.WindowPattern> 控制項模式。<br /><br /> 請參閱 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)。|  
|自動化使用者介面|自動化測試指令碼現在可以使用 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 控制項模式公開的資訊和功能，從 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 架構中控制想要的任何 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。|  
  
## <a name="related-tools-and-technologies"></a>相關工具和技術  

 有一些相關工具和技術會支援使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]來進行自動化測試。  
  
- Inspect.exe 是圖形化使用者介面 (GUI) 應用程式，可用來收集 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 提供者和用戶端開發和偵測的資訊。 Inspect.exe 包含在 Windows SDK 中。  
  
- MSAABridge 會 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 將資訊公開給 Active Accessibility 用戶端。 橋接到 Active Accessibility 的主要目標 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 是要讓現有的 Active Accessibility 用戶端能夠與任何已實行的架構互動 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。  
  
## <a name="security"></a>安全性  

 如需安全性資訊，請參閱 [UI Automation Security Overview](ui-automation-security-overview.md)。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化基礎](index.md)

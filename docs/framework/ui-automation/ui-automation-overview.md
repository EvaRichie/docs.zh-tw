---
title: UI 自動化概觀
description: 閱讀 Microsoft UI 自動化的總覽，這是支援 Windows Presentation Foundation （WPF）的 Windows 作業系統協助工具架構。
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, overview
- user interface, see UI
- accessibility, UI automation
ms.assetid: 65847654-9994-4a9e-b36d-2dd5d998770b
ms.openlocfilehash: 84b176e53f16ba0676e933efe9ed679bf425abc0
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163260"
---
# <a name="ui-automation-overview"></a>UI 自動化概觀
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]是適用于 Microsoft Windows 的新協助工具架構，可在所有支援的作業系統上使用 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 會以程式設計方式存取桌面上大部分的 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 項目，啟用輔助技術產品 (例如螢幕助讀員)，以便為使用者提供 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 的相關資訊，以及使用標準輸入以外的方式來操作 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 也可以讓自動化測試指令碼與 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]互動。  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 不支援不同使用者透過 **Run as** 命令，來啟動處理序之間通訊的功能。  
  
 撰寫使用者介面自動化用戶端應用程式時，可以保證應用程式可在多個架構上運作。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 核心可以降低組成 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]各種元件之架構的任何差異。 例如，按鈕的 `Content` 屬性 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 、 `Caption` Win32 按鈕的屬性，以及 HTML 影像的屬性， `ALT` 都會對應至視圖中的單一屬性 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A> [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。  
  
使用者介面自動化會在執行 .NET Framework 的支援 Windows 作業系統上提供完整的功能（請參閱從 .NET Core 3.0 開始， [.NET Framework 系統需求](../get-started/system-requirements.md)或 .net core 版本。  
  
 使用者介面自動化提供者會透過內建的橋接服務，提供 Microsoft Active Accessibility 用戶端應用程式的一些支援。  
  
<a name="Providers_and_Clients"></a>
## <a name="providers-and-clients"></a>提供者和用戶端  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 具有四個主要元件，如下表所示。  
  
|元件|描述|  
|---------------|-----------------|  
|提供者 API （UIAutomationProvider.dll 和 UIAutomationTypes.dll）|一組由使用者介面自動化提供者實作的介面定義，提供 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目之相關資訊，以及對程式設計輸入做出回應的物件。|  
|用戶端 API (UIAutomationClient.dll 和 UIAutomationTypes.dll)|一組 Managed 程式碼，可讓使用者介面自動化用戶端應用程式取得 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 的相關資訊，並將輸入傳送至控制項。|  
|UiAutomationCore.dll|基礎程式碼 (有時稱為 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 核心) 會處理提供者和用戶端之間的通訊。|  
|UIAutomationClientsideProviders.dll|一組適用於標準舊版控制項的使用者介面自動化提供者。 （ [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 控制項具有的原生支援 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ）。用戶端應用程式會自動提供這種支援。|  
  
 就軟體開發人員的觀點而言，使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的方法有兩種：建立自訂控制項 (使用提供者 API) 的支援，以及建立使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 核心與 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目 (使用用戶端 API) 通訊的應用程式。 視您著重的部分而定，您應該參閱本文件的不同部分。 您可以深入了解這些概念，並在下列章節中取得實際的操作說明知識。  
  
|區段|主題|對象|  
|-------------|--------------------|--------------|  
|[UI 自動化基本](index.md)概念（本節）|概念概觀淺論。|All：|  
|[使用 Managed 程式碼的 UI 自動化提供者](ui-automation-providers-for-managed-code.md)|協助您使用提供者 API 的概觀及操作說明主題。|控制項開發人員。|  
|[Managed 程式碼的 UI 自動化用戶端](ui-automation-clients-for-managed-code.md)|協助您使用用戶端 API 的概觀及操作說明主題。|用戶端應用程式開發人員。|  
|[UI 自動化控制項模式](ui-automation-control-patterns.md)|提供者應如何實作控制項模式，以及哪些功能可供用戶端使用的相關資訊。|All：|  
|[UI 自動化的文字模式](ui-automation-text-pattern.md)|提供者應如何實作文字控制項模式，以及哪些功能可供用戶端使用的相關資訊。|All：|  
|[UI 自動化控制項類型](ui-automation-control-types.md)|不同控制項類型支援之屬性和控制項模式的相關資訊。|All：|  
  
 下表會列出 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間、包含這些命名空間的 DLL 以及命名空間的適用對象。  
  
|命名空間|參考的 DLL|對象|  
|---------------|---------------------|--------------|  
|<xref:System.Windows.Automation>|UIAutomationClientUIAutomationTypes|使用者介面自動化用戶端開發人員；用於尋找 <xref:System.Windows.Automation.AutomationElement> 物件、註冊 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件以及使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控制項模式。|  
|<xref:System.Windows.Automation.Provider>|UIAutomationProviderUIAutomationTypes|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]以外之架構的使用者介面自動化提供者開發人員。|  
|<xref:System.Windows.Automation.Text>|UIAutomationClientUIAutomationTypes|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]以外之架構的使用者介面自動化提供者開發人員；用於實作 TextPattern 控制項模式。|  
|<xref:System.Windows.Automation.Peers>|PresentationFramework|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]的使用者介面自動化提供者開發人員。|  
  
<a name="UI_Automation_Model"></a>
## <a name="ui-automation-model"></a>使用者介面自動化模型  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 會將 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 的每個部分公開給用戶端應用程式，做為 <xref:System.Windows.Automation.AutomationElement>。 項目包含於樹狀結構中，且桌面是根項目。 用戶端可將樹狀結構之未經處理的檢視篩選為控制項檢視或內容檢視。 應用程式也可以建立自訂檢視。  
  
 <xref:System.Windows.Automation.AutomationElement> 物件會公開其所代表之 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 項目的常見屬性。 其中一個屬性是控制項類型，它會將其基本外觀和功能定義為單一可辨識的實體：例如，按鈕或核取方塊。  
  
 此外，項目還會公開控制項模式，用以提供其控制項類型專用的屬性。 控制項模式也會公開方法，讓用戶端取得項目的進一步資訊及提供輸入。  
  
> [!NOTE]
> 控制項類型和控制項模式之間並不存在一對一的對應關係。 控制項模式可由多個控制項類型所支援，且控制項可支援多個控制項模式，每個控制項都會公開其行為的不同層面。 例如，下拉式方塊擁有至少兩個控制項模式：其中一個代表展開和折疊的能力，另一個則代表選取機制。 如需特定資訊，請參閱 [UI Automation Control Types](ui-automation-control-types.md)。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 也可以透過事件，將資訊提供給用戶端應用程式。 不同于 WinEvents， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件不是以廣播機制為基礎。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 用戶端會註冊特定事件通知，且可以要求將特定的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性和控制項模式資訊傳遞至所屬的事件處理常式。 此外， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件也包含引發事件之項目的參考。 提供者可以選擇引發事件來改善效能，取決於是否有任何用戶端接聽。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化樹狀目錄概觀](ui-automation-tree-overview.md)
- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [UI 自動化屬性概觀](ui-automation-properties-overview.md)
- [UI 自動化事件概觀](ui-automation-events-overview.md)
- [UI 自動化安全性概觀](ui-automation-security-overview.md)

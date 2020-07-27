---
title: 用戶端的 UI 自動化屬性
description: 閱讀 ui 自動化屬性的總覽，因為它們已公開至使用者介面自動化用戶端應用程式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties, UI Automation clients
- UI Automation, client properties
ms.assetid: 255905af-0b17-485c-93d4-8a2db2a6524b
ms.openlocfilehash: fe78d7da154d79a5f66ee6c190b199065675841f
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163133"
---
# <a name="ui-automation-properties-for-clients"></a>用戶端的 UI 自動化屬性
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本概觀向您介紹公開至使用者介面自動化用戶端應用程式的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性。  
  
 <xref:System.Windows.Automation.AutomationElement> 物件的屬性包含 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 項目的相關資訊，通常是控制項。 <xref:System.Windows.Automation.AutomationElement> 的屬性是泛型；也就是不專屬於某個控制項類型。 這些屬性有許多公開於 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation> 結構。  
  
 控制項模式也有屬性。 控制項模式的屬性專屬於此模式。 例如， <xref:System.Windows.Automation.ScrollPattern> 的屬性可以讓用戶端運用程式來探索視窗是可以垂直或水平捲動，以及目前檢視大小和捲動位置。 控制項模式透過結構公開其所有屬性；例如， <xref:System.Windows.Automation.ScrollPattern.ScrollPatternInformation>。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性是唯讀的。 若要設定控制項的屬性，您必須使用適當控制項模式的方法。 例如，使用 <xref:System.Windows.Automation.ScrollPattern.Scroll%2A> 來變更捲動中視窗的位置值。  
  
 若要改善效能，擷取 <xref:System.Windows.Automation.AutomationElement> 物件時，可以快取控制項和控制項模式的屬性值。 如需詳細資訊，請參閱[在 UI 自動化用戶端中](caching-in-ui-automation-clients.md)快取。  
  
## <a name="property-ids"></a>屬性識別碼  
 屬性識別碼（Id）是封裝在物件中的唯一、常數值 <xref:System.Windows.Automation.AutomationProperty> 。 使用者介面自動化用戶端應用程式會從 <xref:System.Windows.Automation.AutomationElement> 類別或適當的控制項模式類別（例如）取得這些識別碼 <xref:System.Windows.Automation.ScrollPattern> 。 使用者介面自動化提供者從 <xref:System.Windows.Automation.AutomationElementIdentifiers> 取得這些，或是從控制項模式識別項類別的其中一項取得，例如 <xref:System.Windows.Automation.ScrollPatternIdentifiers>。  
  
 提供者使用 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 的 <xref:System.Windows.Automation.AutomationProperty> 數值來識別在 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A?displayProperty=nameWithType> 方法中要查詢的屬性。 一般而言，用戶端應用程式不需要檢查 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A>。 <xref:System.Windows.Automation.AutomationIdentifier.ProgrammaticName%2A> 僅供偵錯和診斷之用。  
  
## <a name="property-conditions"></a>屬性條件  
 屬性識別碼是用 <xref:System.Windows.Automation.PropertyCondition> 來建立用來尋找物件的物件 <xref:System.Windows.Automation.AutomationElement> 。 例如，您要尋找有特定名稱的 <xref:System.Windows.Automation.AutomationElement> 或是所有已啟用的控制項。 每個 <xref:System.Windows.Automation.PropertyCondition> 都會指定一項 <xref:System.Windows.Automation.AutomationProperty> 識別項和必須與屬性相符的值。  
  
 如需詳細資訊，請參閱下列主題：  
  
- <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.FindAll%2A>  
  
- <xref:System.Windows.Automation.TreeWalker.Condition%2A>  
  
## <a name="retrieving-properties"></a>擷取屬性  
 <xref:System.Windows.Automation.AutomationElement> 的某些屬性和控制項模式類別的所有屬性公開為 `Current` 的巢狀屬性或 `Cached` 或控制項模式物件的 <xref:System.Windows.Automation.AutomationElement> 屬性。  
  
 此外，任何 <xref:System.Windows.Automation.AutomationElement> 或控制項模式屬性，包括在 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 或 <xref:System.Windows.Automation.AutomationElement.Current%2A> 結構中無法使用的屬性，可以使用下列其中一種方法來擷取。  
  
- <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>  
  
 這些方法提供稍微較佳的效能，也能存取屬性的完整範圍。  
  
 下列程式碼範例顯示兩種在 <xref:System.Windows.Automation.AutomationElement>上擷取屬性的方式。  
  
 [!code-csharp[UIAClient_snip#121](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#121)]
 [!code-vb[UIAClient_snip#121](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#121)]  
  
 若要擷取受 <xref:System.Windows.Automation.AutomationElement>支援的控制項模式的屬性，您不需要擷取控制項模式的物件。 只需傳遞其中一個模式屬性識別項至該方法即可。  
  
 下列程式碼範例顯示兩種在控制項模式上擷取屬性的方式。  
  
 [!code-csharp[UIAClient_snip#122](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#122)]
 [!code-vb[UIAClient_snip#122](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#122)]  
  
 `Get` 方法會傳回 <xref:System.Object>。 應用程式必須在使用值之前將傳回的物件轉換成適當的類型。  
  
## <a name="default-property-values"></a>預設屬性值  
 如果使用者介面自動化提供者並未實作屬性，則 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 系統便能提供預設值。 例如，如果控制項的提供者不支援 <xref:System.Windows.Automation.AutomationElement.HelpTextProperty>所識別之屬性， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 就會傳回空字串。 同樣地，如果提供者不支援 <xref:System.Windows.Automation.AutomationElement.IsDockPatternAvailableProperty>所識別之屬性， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 就會傳回 `false`。  
  
 您可以使用 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> 方法多載變更此行為。 當您指定 `true` 做為第二個參數時， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 不會傳回預設值，但相反地會傳回特殊值 <xref:System.Windows.Automation.AutomationElement.NotSupported>。  
  
 下列範例程式碼會嘗試從項目擷取屬性，如果不支援該屬性，則改用應用程式定義的值。  
  
 [!code-csharp[UIAClient_snip#123](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#123)]
 [!code-vb[UIAClient_snip#123](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#123)]  
  
 若要找出項目支援哪些屬性，請使用 <xref:System.Windows.Automation.AutomationElement.GetSupportedProperties%2A>。 這會傳回 <xref:System.Windows.Automation.AutomationProperty> 識別項的陣列。  
  
## <a name="property-changed-events"></a>屬性變更事件  
 當 <xref:System.Windows.Automation.AutomationElement> 或控制項模式的屬性值變更，便會引發事件。 應用程式可以訂閱這類事件，方法是呼叫 <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>、提供 <xref:System.Windows.Automation.AutomationProperty> 識別碼的陣列做為最後一個參數來指定想要的屬性。  
  
 在 <xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>，您可以檢查事件引數的 <xref:System.Windows.Automation.AutomationPropertyChangedEventArgs.Property%2A> 成員，辨識已變更的屬性。 引數也包含已變更的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 屬性之舊值與新值。 這些值的類型都是 <xref:System.Object> ，而且必須在使用之前轉型成正確的類型。  
  
## <a name="additional-automationelement-properties"></a>其他 AutomationElement 屬性  
 除了 <xref:System.Windows.Automation.AutomationElement.Current%2A> 和 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 屬性結構， <xref:System.Windows.Automation.AutomationElement> 具有下列屬性，這會透過簡單的屬性存取子擷取。  
  
|屬性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.Automation.AutomationElement.CachedChildren%2A>|快取中的子 <xref:System.Windows.Automation.AutomationElement> 物件集合。|  
|<xref:System.Windows.Automation.AutomationElement.CachedParent%2A>|快取中的 <xref:System.Windows.Automation.AutomationElement> 父物件。|  
|<xref:System.Windows.Automation.AutomationElement.FocusedElement%2A>|(靜態屬性) 具有輸入焦點的 <xref:System.Windows.Automation.AutomationElement> 。|  
|<xref:System.Windows.Automation.AutomationElement.RootElement%2A>|(靜態屬性) 根 <xref:System.Windows.Automation.AutomationElement>。|  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化用戶端中的快取](caching-in-ui-automation-clients.md)
- [伺服器端 UI 自動化提供者實作](server-side-ui-automation-provider-implementation.md)
- [訂閱 UI 自動化事件](subscribe-to-ui-automation-events.md)

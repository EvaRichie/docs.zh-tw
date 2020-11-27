---
title: 實作 UI 自動化 Toggle 控制項模式
description: 請參閱指導方針和慣例，以在消費者介面自動化中執行切換控制項模式。 瞭解 IToggleProvider 介面所需的成員。
ms.date: 03/30/2017
helpviewer_keywords:
- Toggle control pattern
- control patterns, Toggle
- UI Automation, Toggle control pattern
ms.assetid: 3cfe875f-b0c0-413d-9703-5f14e6a1a30e
ms.openlocfilehash: 865f225d749c29fb1ec80507daeffda82ae8816e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265631"
---
# <a name="implementing-the-ui-automation-toggle-control-pattern"></a>實作 UI 自動化 Toggle 控制項模式

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題將介紹實作 <xref:System.Windows.Automation.Provider.IToggleProvider>的方針和慣例，包括方法和屬性的相關資訊。 其他參考的連結列於主題的結尾。  
  
 <xref:System.Windows.Automation.TogglePattern> 控制項模式是用來支援可循環顯示一組狀態，並在設定之後維持狀態的控制項。 如需實作此控制項模式的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>實作方針和慣例  

 實作切換控制項模式時，請注意下列方針和慣例：  
  
- 若控制項在啟動後不會維持狀態，如按鈕、工具列按鈕和超連結，則必須改為實作 <xref:System.Windows.Automation.Provider.IInvokeProvider> 。  
  
- 控制項必須以下列順序循環其 <xref:System.Windows.Automation.ToggleState> ： <xref:System.Windows.Automation.ToggleState.On>、 <xref:System.Windows.Automation.ToggleState.Off> 以及 <xref:System.Windows.Automation.ToggleState.Indeterminate>(若支援的話)。  
  
- <xref:System.Windows.Automation.TogglePattern> 不提供 SetState(newState) 方法，因為直接設定三種狀態的核取方塊，而不依適當的 <xref:System.Windows.Automation.ToggleState> 順序循環時會發生問題。  
  
- RadioButton 控制項不會實作 <xref:System.Windows.Automation.Provider.IToggleProvider>，因為它無法循環其有效狀態。  
  
<a name="Required_Members_for_IToggleProvider"></a>

## <a name="required-members-for-itoggleprovider"></a>IToggleProvider 的必要成員  

 以下是實作 <xref:System.Windows.Automation.Provider.IToggleProvider>的必要屬性和方法。  
  
|必要成員|成員類型|備註|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.TogglePattern.Toggle%2A>|方法|無|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>|屬性|無|  
  
 此控制項模式沒有任何相關聯的事件。  
  
<a name="Exceptions"></a>

## <a name="exceptions"></a>例外狀況  

 此控制項模式沒有任何相關聯的例外狀況。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [支援 UI 自動化提供者的控制項模式](support-control-patterns-in-a-ui-automation-provider.md)
- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
- [使用 UI 自動化取得核取方塊的切換狀態](get-the-toggle-state-of-a-check-box-using-ui-automation.md)
- [UI 自動化樹狀目錄概觀](ui-automation-tree-overview.md)
- [使用 UI 自動化中的快取](use-caching-in-ui-automation.md)

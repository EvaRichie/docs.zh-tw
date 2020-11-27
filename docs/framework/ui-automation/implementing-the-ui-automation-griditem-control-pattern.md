---
title: 實作 UI 自動化 GridItem 控制項模式
description: 瞭解在消費者介面自動化中為格線專案執行 GridItemPattern 控制項模式的指導方針和慣例。 請參閱必要的 IGridItemProvider 成員。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, GridItem
- UI Automation GridItem control pattern
- GridItem control pattern
ms.assetid: bffbae08-fe2a-42fd-ab84-f37187518916
ms.openlocfilehash: 30932e630c663aabb7d26302174785d44dc1c385
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96267880"
---
# <a name="implementing-the-ui-automation-griditem-control-pattern"></a>實作 UI 自動化 GridItem 控制項模式

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題將介紹實作 <xref:System.Windows.Automation.Provider.IGridItemProvider>的方針和慣例，包括屬性的相關資訊。 其他參考的連結會在概觀的結尾列出。  
  
 <xref:System.Windows.Automation.GridItemPattern> 控制項模式是用以支援實作 <xref:System.Windows.Automation.Provider.IGridProvider> 之容器的個別子控制項。 如需實作此控制項模式的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>實作方針和慣例  

 實作 <xref:System.Windows.Automation.Provider.IGridProvider> 時，請注意下列方針和慣例：  
  
- 方格座標是以零起始，左上資料格座標為 (0, 0)。  
  
- 合併的資料格將會根據其基礎的錨定儲存格 (如使用者介面自動化提供者所定義)，報告其 <xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A> 和 <xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A> 屬性。 通常，它會是最上層或最左邊的資料列或資料行。  
  
- <xref:System.Windows.Automation.Provider.IGridItemProvider> 不提供方格的主動操作，例如合併或分割儲存格。  
  
- 通常可以使用鍵盤周遊實作 <xref:System.Windows.Automation.Provider.IGridItemProvider> 的控制項 (也就是，使用者介面自動化用戶端可以移到相鄰的控制項)。  
  
<a name="Required_Members_for_IGridItemProvider"></a>

## <a name="required-members-for-igriditemprovider"></a>IGridItemProvider 的必要成員  

 以下是實作 <xref:System.Windows.Automation.Provider.IGridItemProvider>的必要屬性和方法。  
  
|必要成員|成員類型|備註|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.RowSpan%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ColumnSpan%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A>|屬性|無|  
  
 此控制項模式沒有任何相關聯的方法或事件。  
  
<a name="Exceptions"></a>

## <a name="exceptions"></a>例外狀況  

 此控制項模式沒有任何相關聯的例外狀況。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [支援 UI 自動化提供者的控制項模式](support-control-patterns-in-a-ui-automation-provider.md)
- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
- [實作 UI 自動化 Grid 控制項模式](implementing-the-ui-automation-grid-control-pattern.md)
- [UI 自動化樹狀目錄概觀](ui-automation-tree-overview.md)
- [使用 UI 自動化中的快取](use-caching-in-ui-automation.md)

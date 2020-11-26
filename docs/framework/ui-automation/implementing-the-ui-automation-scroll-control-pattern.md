---
title: 實作 UI 自動化 Scroll 控制項模式
description: 請參閱在消費者介面自動化中執行捲軸控制項模式的指導方針和慣例。 請參閱 IScrollProvider 介面所需的成員。
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Scroll control pattern
- control patterns, Scroll
- Scroll control pattern
ms.assetid: 73d64242-6cbb-424c-92dd-dc69530b7899
ms.openlocfilehash: 4069772530d8b4db817aa1b7a9be86a3ee83881e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239259"
---
# <a name="implementing-the-ui-automation-scroll-control-pattern"></a>實作 UI 自動化 Scroll 控制項模式

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題將介紹實作 <xref:System.Windows.Automation.Provider.IScrollProvider>的方針和慣例，包括事件和屬性的相關資訊。 其他參考的連結列於主題的結尾。  
  
 <xref:System.Windows.Automation.ScrollPattern> 控制項模式是用來支援放有一組子項目的捲動式容器控制項。 控制項不一定要使用捲軸才能支援捲動功能，不過它通常會這麼做。  
  
 ![不含捲軸的 Scroll 控制項。](./media/uia-scrollpattern-without-scrollbars.PNG "UIA_ScrollPattern_Without_Scrollbars")  
不使用捲軸的捲動控制項範例  
  
 如需實作此控制項的控制項範例，請參閱 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>實作方針和慣例  

 實作捲軸控制項模式時，請注意下列方針和慣例：  
  
- 這個控制項的子系必須實作 <xref:System.Windows.Automation.Provider.IScrollItemProvider>。  
  
- 容器控制項的捲軸不支援 <xref:System.Windows.Automation.ScrollPattern> 控制項模式。 捲軸必須改成支援 <xref:System.Windows.Automation.RangeValuePattern> 控制項模式。  
  
- 若捲動是以百分比為單位，則與捲動刻度相關的所有值或數量必須標準化為 0 到 100 之間的範圍。  
  
- <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 和 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 與 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>無關。  
  
- 如果 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> = `false` ，則 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 應設為 100%，而且 <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 應設為 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>。 同樣地，如果 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> = `false` ，則 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 應設為 100%，而且 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 應設為 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>。 若用戶端不想捲動的方向啟動時，這可讓使用者介面自動化用戶端在 <xref:System.Windows.Automation.ScrollPattern.SetScrollPercent%2A> 方法中使用這些屬性值，以免發生 [競爭情形](https://support.microsoft.com/default.aspx?scid=kb;en-us;317723) 。  
  
- <xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A> 是地區設定特性。 設定 HorizontalScrollPercent = 100.0 時，必須將控制項的捲動位置設為由左至右語言 (如英文) 的最右側位置。 相反地，若為由右至左語言 (如阿拉伯文)，設定 HorizontalScrollPercent = 100.0 時，必須將捲動位置設為最左側位置。  
  
<a name="Required_Members_for_IScrollProvider"></a>

## <a name="required-members-for-iscrollprovider"></a>IScrollProvider 的必要成員  

 以下是實作 <xref:System.Windows.Automation.Provider.IScrollProvider>的必要屬性和方法。  
  
|必要成員|成員類型|備註|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalScrollPercent%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalViewSize%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalViewSize%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontallyScrollable%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticallyScrollable%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A>|方法|無|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>|方法|無|  
  
 此控制項模式沒有任何相關聯的事件。  
  
<a name="Exceptions"></a>

## <a name="exceptions"></a>例外狀況  

 提供者必須擲回下列例外狀況。  
  
|例外狀況類型|條件|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|如果控制項僅支援垂直或水平捲動的<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 值，但傳入了 <xref:System.Windows.Automation.ScrollAmount.SmallIncrement> 值， <xref:System.Windows.Automation.ScrollAmount.LargeIncrement> 就會擲回這個例外狀況。|  
|<xref:System.ArgumentException>|當傳入無法轉換成雙精度浮點數的值時，<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 便會擲回這個例外狀況。|  
|<xref:System.ArgumentOutOfRangeException>|當傳入大於 100 或小於 0 的值 (-1 例外，因為它相當於<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> ) 時， <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>就會擲回這個例外狀況。|  
|<xref:System.InvalidOperationException>|嘗試在不支援的方向捲動時， <xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 和 <xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 都會擲回這個例外狀況。|  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [支援 UI 自動化提供者的控制項模式](support-control-patterns-in-a-ui-automation-provider.md)
- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
- [UI 自動化樹狀目錄概觀](ui-automation-tree-overview.md)
- [使用 UI 自動化中的快取](use-caching-in-ui-automation.md)

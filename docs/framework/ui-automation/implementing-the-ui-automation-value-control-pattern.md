---
title: 實作 UI 自動化 Value 控制項模式
description: 請參閱指導方針和慣例，在使用者介面自動化中執行實值控制項模式。 知道 IValueProvider 介面的必要成員。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Value
- UI Automation, Value control pattern
- Value control pattern
ms.assetid: b0fcdd87-3add-4345-bca9-e891205e02ba
ms.openlocfilehash: a15c0b50996e2c0dfdc937bc9565d5f9ba20c992
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168197"
---
# <a name="implementing-the-ui-automation-value-control-pattern"></a>實作 UI 自動化 Value 控制項模式
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題將介紹實作 <xref:System.Windows.Automation.Provider.IValueProvider>的方針和慣例，包括事件和屬性的相關資訊。 其他參考的連結列於主題的結尾。  
  
 <xref:System.Windows.Automation.ValuePattern> 控制項模式用來支援不跨越某個範圍的內建值且可以表示為字串的控制項。 這個字串可以是可編輯的，視控制項及其設定而定。 如需實作此模式的控制項範例，請參閱 [T:System.Windows.Automation.Provider.IValueProvider](control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a>實作方針和慣例  
 實作值控制項模式時，請注意下列方針和慣例：  
  
- 如果任何項目的值是可編輯的，則例如 <xref:System.Windows.Automation.ControlType.ListItem> 和 <xref:System.Windows.Automation.ControlType.TreeItem> 等控制項必須支援 <xref:System.Windows.Automation.ValuePattern> ，而不論控制項目前的編輯模式為何。 如果子項目是可編輯的，父控制項也必須支援 <xref:System.Windows.Automation.ValuePattern> 。  
  
 ![可編輯的清單項目。](./media/uia-valuepattern-editable-listitem.PNG "UIA_ValuePattern_Editable_ListItem")  
可編輯的清單項目範例  
  
- 單行編輯控制項支援藉由實作 <xref:System.Windows.Automation.Provider.IValueProvider>，以程式設計方式存取其內容。 不過，多行編輯控制項不會實作 <xref:System.Windows.Automation.Provider.IValueProvider>；它們是改為藉由實作 <xref:System.Windows.Automation.Provider.ITextProvider>來提供其內容的存取。  
  
- 若要擷取多行編輯控制項的文字內容，控制項必須實作 <xref:System.Windows.Automation.Provider.ITextProvider>。 不過， <xref:System.Windows.Automation.Provider.ITextProvider> 不支援設定控制項的值。  
  
- <xref:System.Windows.Automation.Provider.IValueProvider> 不支援擷取格式設定資訊或子字串值。 在這些案例中請實作 <xref:System.Windows.Automation.Provider.ITextProvider> 。  
  
- <xref:System.Windows.Automation.Provider.IValueProvider>必須由像是 Microsoft Word 的**色彩選擇器**選取控制項（如下列所示）的控制項來執行，這可支援色彩值（例如，"黃色"）與對等的內部 RGB 結構之間的字串對應。  
  
 ![已反白顯示黃色的色彩選擇器](./media/uia-valuepattern-colorpicker.png "UIA_ValuePattern_ColorPicker")  
色樣字串對應範例  
  
- 控制項的 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> 應該設為 `true` ， <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> 應該設為 `false` ，才能允許呼叫 <xref:System.Windows.Automation.Provider.IValueProvider.SetValue%2A>。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>
## <a name="required-members-for-ivalueprovider"></a>IValueProvider 的必要成員  
 以下是實作 <xref:System.Windows.Automation.Provider.IValueProvider>的必要屬性和方法。  
  
|必要成員|成員類型|注意|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty>|屬性|None|  
|<xref:System.Windows.Automation.ValuePattern.ValueProperty>|屬性|None|  
|<xref:System.Windows.Automation.ValuePattern.SetValue%2A>|方法|None|  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a>例外狀況  
 提供者必須擲回下列例外狀況。  
  
|例外狀況類型|條件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -如果地區設定特有的資訊以不正確的格式傳遞至控制項，例如格式不正確的日期。|  
|<xref:System.ArgumentException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -如果新的值無法從字串轉換成控制項可辨識的格式。|  
|<xref:System.Windows.Automation.ElementNotEnabledException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> -嘗試操作未啟用的控制項時。|  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [支援 UI 自動化提供者的控制項模式](support-control-patterns-in-a-ui-automation-provider.md)
- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
- [ValuePattern 插入文字範例](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText)
- [UI 自動化樹狀目錄概觀](ui-automation-tree-overview.md)
- [使用 UI 自動化中的快取](use-caching-in-ui-automation.md)

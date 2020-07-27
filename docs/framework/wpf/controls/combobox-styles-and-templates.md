---
title: ComboBox 樣式和範本
description: 瞭解 Windows Presentation Foundation ComboBox 控制項的樣式和範本。 修改 ControlTemplate，讓控制項具有獨特的外觀。
ms.date: 03/30/2017
helpviewer_keywords:
- ComboBox [WPF], styles and templates
- states [WPF], ComboBox
- ControlTemplate [WPF], ComboBox
- styles [WPF], ComboBox
- templates [WPF], ComboBox
- parts [WPF], ComboBox
ms.assetid: b0662fa1-16d7-4320-b26b-c1804e565a44
ms.openlocfilehash: 5e929bafeaf849b4b5682a17ca51cb0aab963613
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165908"
---
# <a name="combobox-styles-and-templates"></a>ComboBox 樣式和範本
本主題描述控制項的樣式和範本 <xref:System.Windows.Controls.ComboBox> 。 您可以修改預設值 <xref:System.Windows.Controls.ControlTemplate> ，為控制項提供獨特的外觀。 如需詳細資訊，請參閱[建立控制項的範本](../../../desktop-wpf/themes/how-to-create-apply-template.md)。  
  
## <a name="combobox-parts"></a>ComboBox 元件  
 下表列出控制項的已命名元件 <xref:System.Windows.Controls.ComboBox> 。  
  
|部分|類型|描述|  
|-|-|-|  
|PART_EditableTextBox|<xref:System.Windows.Controls.TextBox>|包含的文字 <xref:System.Windows.Controls.ComboBox> 。|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|下拉式方塊中包含專案的下拉式方塊。|  
  
 當您建立的時 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.ComboBox> ，您的範本可能會 <xref:System.Windows.Controls.ItemsPresenter> 在中包含 <xref:System.Windows.Controls.ScrollViewer> 。 （會 <xref:System.Windows.Controls.ItemsPresenter> 顯示中的每個專案 <xref:System.Windows.Controls.ComboBox> ; 會 <xref:System.Windows.Controls.ScrollViewer> 啟用控制項內的滾動功能）。  如果不 <xref:System.Windows.Controls.ItemsPresenter> 是的直接子系 <xref:System.Windows.Controls.ScrollViewer> ，您就必須指定 <xref:System.Windows.Controls.ItemsPresenter> 名稱 `ItemsPresenter` 。  
  
## <a name="combobox-states"></a>ComboBox 狀態  
 下表列出控制項的狀態 <xref:System.Windows.Controls.ComboBox> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|已停用|CommonStates|已停用控制項。|  
|MouseOver|CommonStates|滑鼠指標位於 <xref:System.Windows.Controls.ComboBox> 控制項上。|  
|已取得焦點|FocusStates|控制項已取得焦點。|  
|未取得焦點|FocusStates|控制項未取得焦點。|  
|FocusedDropDown|FocusStates|的下拉式是 <xref:System.Windows.Controls.ComboBox> 焦點。|  
|有效|ValidationStates|控制項使用 <xref:System.Windows.Controls.Validation> 類別，而 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 附加屬性是 `false` 。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加屬性為 `true` ，且控制項具有焦點。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加屬性為 `true` ，且控制項沒有焦點。|  
|Editable|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> 屬性為 `true`。|  
|編輯|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> 屬性為 `false`。|  
  
## <a name="comboboxitem-parts"></a>ComboBoxItem 元件  
 <xref:System.Windows.Controls.ComboBoxItem>控制項沒有任何已命名的元件。  
  
## <a name="comboboxitem-states"></a>ComboBoxItem 狀態  
 下表列出控制項的狀態 <xref:System.Windows.Controls.ComboBoxItem> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|已停用|CommonStates|已停用控制項。|  
|MouseOver|CommonStates|滑鼠指標位於 <xref:System.Windows.Controls.ComboBoxItem> 控制項上。|  
|已取得焦點|FocusStates|控制項已取得焦點。|  
|未取得焦點|FocusStates|控制項未取得焦點。|  
|已選取|SelectionStates|目前已選取專案。|  
|未選取|SelectionStates|項目未獲選取。|  
|SelectedUnfocused|SelectionStates|項目已獲選取，但未取得焦點。|  
|有效|ValidationStates|控制項使用 <xref:System.Windows.Controls.Validation> 類別，而 <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 附加屬性是 `false` 。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加屬性為 `true` ，且控制項具有焦點。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加屬性為 `true` ，且控制項沒有焦點。|  
  
## <a name="combobox-controltemplate-example"></a>ComboBox ControlTemplate 範例  
 下列範例示範如何定義 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.ComboBox> 控制項和相關聯類型的。  
  
 [!code-xaml[ControlTemplateExamples#ComboBox](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/combobox.xaml#combobox)]  
  
 上述範例使用下列一或多項資源。  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 如需完整的範例，請參閱[使用 ControlTemplate 設定樣式範例](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [控制項的樣式和範本](control-styles-and-templates.md)
- [控制項自訂](control-customization.md)
- [樣式設定和範本化](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [建立控制項的範本](../../../desktop-wpf/themes/how-to-create-apply-template.md)

---
title: DataGrid 樣式和範本
description: 瞭解 Windows Presentation Foundation DataGrid 控制項的樣式和範本。 修改 ControlTemplate，讓控制項具有獨特的外觀。
ms.date: 03/30/2017
helpviewer_keywords:
- states [WPF], DataGrid
- ControlTemplate [WPF], DataGrid
- DataGrid [WPF], styles and templates
- templates [WPF], DataGrid
- styles [WPF], DataGrid
- parts [WPF], DataGrid
ms.assetid: 9cb31d63-f148-4d25-b079-816e73f988c7
ms.openlocfilehash: dd526ec64d5077dad58f31c004f47e63c57ec9de
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168325"
---
# <a name="datagrid-styles-and-templates"></a>DataGrid 樣式和範本
本主題描述控制項的樣式和範本 <xref:System.Windows.Controls.DataGrid> 。 您可以修改預設值 <xref:System.Windows.Controls.ControlTemplate> ，為控制項提供獨特的外觀。 如需詳細資訊，請參閱[建立控制項的範本](../../../desktop-wpf/themes/how-to-create-apply-template.md)。  
  
## <a name="datagrid-parts"></a>DataGrid 元件  
 下表列出控制項的已命名元件 <xref:System.Windows.Controls.DataGrid> 。  
  
|部分|類型|描述|  
|-|-|-|  
|PART_ColumnHeadersPresenter|<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>|包含資料行標頭的資料列。|  
  
 當您建立的時 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.DataGrid> ，您的範本可能會 <xref:System.Windows.Controls.ItemsPresenter> 在中包含 <xref:System.Windows.Controls.ScrollViewer> 。 （會 <xref:System.Windows.Controls.ItemsPresenter> 顯示中的每個專案 <xref:System.Windows.Controls.DataGrid> ; 會 <xref:System.Windows.Controls.ScrollViewer> 啟用控制項內的滾動功能）。  如果不 <xref:System.Windows.Controls.ItemsPresenter> 是的直接子系 <xref:System.Windows.Controls.ScrollViewer> ，您就必須指定 <xref:System.Windows.Controls.ItemsPresenter> 名稱 `ItemsPresenter` 。  
  
 的預設範本 <xref:System.Windows.Controls.DataGrid> 包含 <xref:System.Windows.Controls.ScrollViewer> 控制項。 如需所定義之元件的詳細資訊 <xref:System.Windows.Controls.ScrollViewer> ，請參閱[ScrollViewer 樣式和範本](scrollviewer-styles-and-templates.md)。  
  
## <a name="datagrid-states"></a>DataGrid 狀態  
 下表列出控制項的視覺狀態 <xref:System.Windows.Controls.DataGrid> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|已停用|CommonStates|已停用控制項。|  
|InvalidFocused|ValidationStates|控制項無效且已取得焦點。|  
|InvalidUnfocused|ValidationStates|控制項無效且未取得焦點。|  
|有效|ValidationStates|控制項有效。|  
  
## <a name="datagridcell-parts"></a>DataGridCell 元件  
 <xref:System.Windows.Controls.DataGridCell>元素沒有任何已命名的元件。  
  
## <a name="datagridcell-states"></a>DataGridCell 狀態  
 下表列出元素的視覺狀態 <xref:System.Windows.Controls.DataGridCell> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|MouseOver|CommonStates|滑鼠指標位於資料格上。|  
|已取得焦點|FocusStates|儲存格具有焦點。|  
|未取得焦點|FocusStates|儲存格沒有焦點|  
|目前|CurrentStates|儲存格是目前的儲存格。|  
|定期|CurrentStates|儲存格不是目前的儲存格。|  
|顯示|InteractionStates|資料格處於顯示模式。|  
|編輯中|InteractionStates|資料格處於編輯模式。|  
|已選取|SelectionStates|已選取儲存格。|  
|未選取|SelectionStates|未選取儲存格。|  
|InvalidFocused|ValidationStates|儲存格無效而且具有焦點。|  
|InvalidUnfocused|ValidationStates|儲存格無效，而且沒有焦點。|  
|有效|ValidationStates|儲存格有效。|  
  
## <a name="datagridrow-parts"></a>DataGridRow 元件  
 <xref:System.Windows.Controls.DataGridRow>元素沒有任何已命名的元件。  
  
## <a name="datagridrow-states"></a>DataGridRow 狀態  
 下表列出元素的視覺狀態 <xref:System.Windows.Controls.DataGridRow> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|MouseOver|CommonStates|滑鼠指標位於資料列上。|  
|MouseOver_Editing|CommonStates|滑鼠指標位於資料列上，且資料列處於編輯模式。|  
|MouseOver_Selected|CommonStates|滑鼠指標位於資料列上，而且已選取資料列。|  
|MouseOver_Unfocused_Editing|CommonStates|滑鼠指標位於資料列上、資料列處於編輯模式，而且沒有焦點。|  
|MouseOver_Unfocused_Selected|CommonStates|滑鼠指標位於資料列上、已選取資料列，而且沒有焦點。|  
|Normal_AlternatingRow|CommonStates|資料列是替代資料列。|  
|Normal_Editing|CommonStates|資料列處於編輯模式。|  
|Normal_Selected|CommonStates|已選取資料列。|  
|Unfocused_Editing|CommonStates|資料列處於編輯模式，而且沒有焦點。|  
|Unfocused_Selected|CommonStates|已選取此資料列，而且沒有焦點。|  
|InvalidFocused|ValidationStates|控制項無效且已取得焦點。|  
|InvalidUnfocused|ValidationStates|控制項無效且未取得焦點。|  
|有效|ValidationStates|控制項有效。|  
  
## <a name="datagridrowheader-parts"></a>DataGridRowHeader 元件  
 下表列出元素的已命名元件 <xref:System.Windows.Controls.Primitives.DataGridRowHeader> 。  
  
|部分|類型|描述|  
|-|-|-|  
|PART_TopHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用來調整頂端資料列行首大小的元素。|  
|PART_BottomHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用來調整資料列行首大小的元素。|  
  
## <a name="datagridrowheader-states"></a>DataGridRowHeader 狀態  
 下表列出元素的視覺狀態 <xref:System.Windows.Controls.Primitives.DataGridRowHeader> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|MouseOver|CommonStates|滑鼠指標位於資料列上。|  
|MouseOver_CurrentRow|CommonStates|滑鼠指標位於資料列上，且資料列是目前的資料列。|  
|MouseOver_CurrentRow_Selected|CommonStates|滑鼠指標位於資料列上，且資料列為 [目前] 和 [已選取]。|  
|MouseOver_EditingRow|CommonStates|滑鼠指標位於資料列上，且資料列處於編輯模式。|  
|MouseOver_Selected|CommonStates|滑鼠指標位於資料列上，而且已選取資料列。|  
|MouseOver_Unfocused_CurrentRow_Selected|CommonStates|滑鼠指標位於資料列上、資料列為最新且已選取，而且沒有焦點。|  
|MouseOver_Unfocused_EditingRow|CommonStates|滑鼠指標位於資料列上、資料列處於編輯模式，而且沒有焦點。|  
|MouseOver_Unfocused_Selected|CommonStates|滑鼠指標位於資料列上、已選取資料列，而且沒有焦點。|  
|Normal_CurrentRow|CommonStates|資料列是目前的資料列。|  
|Normal_CurrentRow_Selected|CommonStates|資料列是目前的資料列，而且已選取。|  
|Normal_EditingRow|CommonStates|資料列處於編輯模式。|  
|Normal_Selected|CommonStates|已選取資料列。|  
|Unfocused_CurrentRow_Selected|CommonStates|資料列是目前的資料列，已選取，而且沒有焦點。|  
|Unfocused_EditingRow|CommonStates|資料列處於編輯模式，而且沒有焦點。|  
|Unfocused_Selected|CommonStates|已選取此資料列，而且沒有焦點。|  
|InvalidFocused|ValidationStates|控制項無效且已取得焦點。|  
|InvalidUnfocused|ValidationStates|控制項無效且未取得焦點。|  
|有效|ValidationStates|控制項有效。|  
  
## <a name="datagridcolumnheaderspresenter-parts"></a>DataGridColumnHeadersPresenter 元件  
 下表列出元素的已命名元件 <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 。  
  
|部分|類型|描述|  
|-|-|-|  
|PART_FillerColumnHeader|<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>|資料行標頭的預留位置。|  
  
## <a name="datagridcolumnheaderspresenter-states"></a>DataGridColumnHeadersPresenter 狀態  
 下表列出元素的視覺狀態 <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|InvalidFocused|ValidationStates|儲存格無效而且具有焦點。|  
|InvalidUnfocused|ValidationStates|儲存格無效，而且沒有焦點。|  
|有效|ValidationStates|儲存格有效。|  
  
## <a name="datagridcolumnheader-parts"></a>DataGridColumnHeader 元件  
 下表列出元素的已命名元件 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 。  
  
|部分|類型|描述|  
|-|-|-|  
|PART_LeftHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用來從左邊調整資料行行首的元素。|  
|PART_RightHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用來從右調整資料行行首的元素。|  
  
## <a name="datagridcolumnheader-states"></a>DataGridColumnHeader 狀態  
 下表列出元素的視覺狀態 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 。  
  
|VisualState 名稱|VisualStateGroup 名稱|描述|  
|-|-|-|  
|正常|CommonStates|預設狀態。|  
|MouseOver|CommonStates|滑鼠指標移到控制項上。|  
|按下|CommonStates|已按下控制項。|  
|SortAscending|SortStates|資料行是以遞增順序排序。|  
|SortDescending|SortStates|資料行是以遞減順序排序。|  
|目錄名|SortStates|未排序資料行。|  
|InvalidFocused|ValidationStates|控制項無效且已取得焦點。|  
|InvalidUnfocused|ValidationStates|控制項無效且未取得焦點。|  
|有效|ValidationStates|控制項有效。|  
  
## <a name="datagrid-controltemplate-example"></a>DataGrid ControlTemplate 範例  
 下列範例示範如何定義 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.DataGrid> 控制項的和其相關聯的類型。  
  
 [!code-xaml[ControlTemplateExamples#DataGrid](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datagrid.xaml#datagrid)]  
  
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

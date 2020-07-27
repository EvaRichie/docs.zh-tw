---
title: 控制項
description: 瞭解 Windows Presentation Foundation 常見的 UI 元件（稱為控制項），但這可能不會繼承自控制項類別。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], about WPF controls
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
ms.openlocfilehash: c3d9d3a38cf5f84e21df195e113e264e5a4ac025
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165847"
---
# <a name="controls"></a>控制項
<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]隨附許多在幾乎每個 Windows 應用程式中使用的通用 UI 元件，例如、、 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.Label> <xref:System.Windows.Controls.TextBox> 、 <xref:System.Windows.Controls.Menu> 和 <xref:System.Windows.Controls.ListBox> 。 在過去，這些物件是稱為控制項。 雖然 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK 會繼續使用「控制」一詞，以鬆散表示應用程式中代表可見物件的任何類別，但請務必注意，類別不需要繼承自類別，就能 <xref:System.Windows.Controls.Control> 看到可見的狀態。 繼承自類別的類別 <xref:System.Windows.Controls.Control> 包含，可 <xref:System.Windows.Controls.ControlTemplate> 讓控制項的取用者徹底變更控制項的外觀，而不需要建立新的子類別。  本主題討論中常用的控制項（這兩者都是繼承自 <xref:System.Windows.Controls.Control> 類別，而不是那些）會在中使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。  

<a name="creating_an_instance_of_a_control"></a>
## <a name="creating-an-instance-of-a-control"></a>建立控制項的執行個體  
 您可以使用或程式碼，將控制項加入至應用程式 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 。  下列範例示範如何建立一個要求使用者輸入其名字和姓氏的簡單應用程式。  這個範例會建立六個控制項：中的兩個標籤、兩個文字方塊和兩個按鈕 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。 您可以用類似的方式建立所有控制項。  
  
 [!code-xaml[ControlsOverview#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 下列範例會以程式碼建立相同的應用程式。 為求簡潔，已 <xref:System.Windows.Controls.Grid> `grid1` 從範例中排除的建立。 `grid1`具有與前述範例中所示相同的資料行和資料列定義 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。  
  
 [!code-csharp[ControlsOverview#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)]
 [!code-vb[ControlsOverview#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>
## <a name="changing-the-appearance-of-a-control"></a>變更控制項的外觀  
 變更控制項的外觀以符合您應用程式的外觀及操作，是很常見的做法。 您可以根據想要達成的目的，執行下列其中一項操作來變更控制項的外觀：  
  
- 變更控制項的屬性值。  
  
- 建立 <xref:System.Windows.Style> 控制項的。  
  
- <xref:System.Windows.Controls.ControlTemplate>為控制項建立新的。  
  
### <a name="changing-a-controls-property-value"></a>變更控制項的屬性值  
 許多控制項都有屬性，可讓您變更控制項的顯示方式，例如的 <xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Controls.Button> 。 您可以同時在和程式碼中設定值屬性 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。 下列範例會在 <xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Controls.Control.FontSize%2A> <xref:System.Windows.Controls.Control.FontWeight%2A> 中的上設定、和屬性 <xref:System.Windows.Controls.Button> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。  
  
 [!code-xaml[ControlsOverview#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 下列範例會以程式碼設定相同的屬性。  
  
 [!code-csharp[ControlsOverview#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)]
 [!code-vb[ControlsOverview#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### <a name="creating-a-style-for-a-control"></a>為控制項建立樣式  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]藉由建立，讓您能夠指定控制項的外觀，而不是在應用程式中的每個實例上設定屬性 <xref:System.Windows.Style> 。 下列範例會建立一個 <xref:System.Windows.Style> ，它會套用至 <xref:System.Windows.Controls.Button> 應用程式中的每個。 <xref:System.Windows.Style>定義通常是在的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定義 <xref:System.Windows.ResourceDictionary> ，例如的 <xref:System.Windows.FrameworkElement.Resources%2A> 屬性 <xref:System.Windows.FrameworkElement> 。  
  
 [!code-xaml[ControlsOverview#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 您也可以藉由指派一個索引鍵給樣式，並在控制項的屬性中指定該索引鍵，將樣式套用至特定類型的某些控制項 `Style` 。  如需樣式的詳細資訊，請參閱設定樣式[和範本](../../../desktop-wpf/fundamentals/styles-templates-overview.md)。  
  
### <a name="creating-a-controltemplate"></a>建立 ControlTemplate  
 可以 <xref:System.Windows.Style> 讓您一次設定多個控制項的屬性，但有時您可能會想要自訂 <xref:System.Windows.Controls.Control> 除了建立以外的外觀 <xref:System.Windows.Style> 。 繼承自類別的類別 <xref:System.Windows.Controls.Control> 具有 <xref:System.Windows.Controls.ControlTemplate> ，它會定義的結構和外觀 <xref:System.Windows.Controls.Control> 。 的 <xref:System.Windows.Controls.Control.Template%2A> 屬性 <xref:System.Windows.Controls.Control> 是公用的，因此您可以提供與 <xref:System.Windows.Controls.Control> <xref:System.Windows.Controls.ControlTemplate> 預設值不同的。 您通常可以為指定新 <xref:System.Windows.Controls.ControlTemplate> 的， <xref:System.Windows.Controls.Control> 而不是從控制項繼承以自訂的外觀 <xref:System.Windows.Controls.Control> 。  
  
 請考慮一下非常常見的控制項 <xref:System.Windows.Controls.Button> 。  的主要行為 <xref:System.Windows.Controls.Button> 是讓應用程式在使用者按一下時採取動作。  根據預設， <xref:System.Windows.Controls.Button> 中的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 會顯示為凸起的矩形。  開發應用程式時，您可能會想要利用的行為，也 <xref:System.Windows.Controls.Button> 就是藉由處理按鈕的 click 事件--但您可能會變更按鈕的外觀，而不是藉由變更按鈕的屬性來執行。  在此情況下，您可以建立新的 <xref:System.Windows.Controls.ControlTemplate> 。  
  
 下列範例會建立的 <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.Button> 。  會 <xref:System.Windows.Controls.ControlTemplate> 建立 <xref:System.Windows.Controls.Button> 具有圓角和漸層背景的。  <xref:System.Windows.Controls.ControlTemplate>包含， <xref:System.Windows.Controls.Border> 其 <xref:System.Windows.Controls.Border.Background%2A> 為 <xref:System.Windows.Media.LinearGradientBrush> 具有兩個 <xref:System.Windows.Media.GradientStop> 物件的。  第一個會使用資料系結，將的屬性系結 <xref:System.Windows.Media.GradientStop> <xref:System.Windows.Media.GradientStop.Color%2A> <xref:System.Windows.Media.GradientStop> 至按鈕背景的色彩。  當您設定的 <xref:System.Windows.Controls.Control.Background%2A> 屬性時 <xref:System.Windows.Controls.Button> ，將會使用該值的色彩做為第一個 <xref:System.Windows.Media.GradientStop> 。 如需資料繫結的詳細資訊，請參閱[資料繫結概觀](../../../desktop-wpf/data/data-binding-overview.md)。 此範例也會建立 <xref:System.Windows.Trigger> ， <xref:System.Windows.Controls.Button> 當為時，會變更的外觀 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> `true` 。  
  
 [!code-xaml[ControlsOverview#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xaml[ControlsOverview#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
> 的 <xref:System.Windows.Controls.Control.Background%2A> 屬性 <xref:System.Windows.Controls.Button> 必須設定為， <xref:System.Windows.Media.SolidColorBrush> 範例才能正常運作。  
  
<a name="subscribing_to_events"></a>
## <a name="subscribing-to-events"></a>訂閱事件  
 您可以使用或程式碼來訂閱控制項的事件 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，但只能處理常式代碼中的事件。  下列範例顯示如何訂閱的 `Click` 事件 <xref:System.Windows.Controls.Button> 。  
  
 [!code-xaml[ControlsOverview#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)]
 [!code-vb[ControlsOverview#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 下列範例會處理的 `Click` 事件 <xref:System.Windows.Controls.Button> 。  
  
 [!code-csharp[ControlsOverview#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)]
 [!code-vb[ControlsOverview#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>
## <a name="rich-content-in-controls"></a>控制項中的多格式內容  
 大部分繼承自類別的類別 <xref:System.Windows.Controls.Control> 都具有包含豐富內容的容量。 例如， <xref:System.Windows.Controls.Label> 可以包含任何物件，例如字串、 <xref:System.Windows.Controls.Image> 或 <xref:System.Windows.Controls.Panel> 。  下列類別提供豐富內容的支援，並作為中大部分控制項的基類 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。  
  
- <xref:System.Windows.Controls.ContentControl>--繼承自這個類別的一些類別範例包括 <xref:System.Windows.Controls.Label> 、 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.ToolTip> 。  
  
- <xref:System.Windows.Controls.ItemsControl>--繼承自這個類別的一些類別範例包括 <xref:System.Windows.Controls.ListBox> 、 <xref:System.Windows.Controls.Menu> 和 <xref:System.Windows.Controls.Primitives.StatusBar> 。  
  
- <xref:System.Windows.Controls.HeaderedContentControl>--繼承自這個類別的一些類別範例包括 <xref:System.Windows.Controls.TabItem> 、 <xref:System.Windows.Controls.GroupBox> 和 <xref:System.Windows.Controls.Expander> 。  
  
- <xref:System.Windows.Controls.HeaderedItemsControl>--繼承自這個類別的一些類別範例包括 <xref:System.Windows.Controls.MenuItem> 、 <xref:System.Windows.Controls.TreeViewItem> 和 <xref:System.Windows.Controls.ToolBar> 。  

 如需這些基類的詳細資訊，請參閱[WPF 內容模型](wpf-content-model.md)。  
  
## <a name="see-also"></a>另請參閱

- [樣式設定和範本化](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [按分類區隔控制項](controls-by-category.md)
- [控制項程式庫](control-library.md)
- [資料範本化概觀](../data/data-templating-overview.md)
- [資料系結總覽](../../../desktop-wpf/data/data-binding-overview.md)
- [輸入](../advanced/input-wpf.md)
- [啟用命令](../advanced/how-to-enable-a-command.md)
- [逐步解說：建立自訂動畫按鈕](walkthroughs-create-a-custom-animated-button.md)
- [控制項自訂](control-customization.md)

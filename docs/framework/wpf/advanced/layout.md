---
title: 版面配置
description: 瞭解版面配置計算在 Windows Presentation Foundation 版面配置系統中的發生方式和時機。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF layout system [WPF]
- controls [WPF], layout system
- layout system [WPF]
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
ms.openlocfilehash: 0db3f2a6cbabc610362435d64de3fc970f01a73c
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164772"
---
# <a name="layout"></a>版面配置

本主題描述 Windows Presentation Foundation （WPF）版面配置系統。 瞭解版面配置計算的發生方式和時機，是在 WPF 中建立使用者介面的必要條件。

本主題包含下列幾節：

- [項目週框方塊](#LayoutSystem_BoundingBox)

- [配置系統](#LayoutSystem_Overview)

- [測量和排列子系](#LayoutSystem_Measure_Arrange)

- [面板項目和自訂版面配置行為](#LayoutSystem_PanelsCustom)

- [版面配置效能考量](#LayoutSystem_Performance)

- [子像素轉譯和版面配置進位](#LayoutSystem_LayoutRounding)

- [下一步](#LayoutSystem_whatsnext)

<a name="LayoutSystem_BoundingBox"></a>

## <a name="element-bounding-boxes"></a>項目週框方塊

考慮 WPF 中的版面配置時，請務必瞭解環繞所有元素的周框方塊。 配置系統所取用的每一個都 <xref:System.Windows.FrameworkElement> 可以被視為一個矩形，做為版面配置的一周框。 類別會傳回 <xref:System.Windows.Controls.Primitives.LayoutInformation> 元素的版面配置分配或位置的界限。 矩形的大小取決於計算可用的螢幕空間、任何條件約束的大小、版面配置特有的屬性（例如邊界和填補），以及父元素的個別行為 <xref:System.Windows.Controls.Panel> 。 處理此資料時，配置系統能夠計算特定的所有子系的位置 <xref:System.Windows.Controls.Panel> 。 請務必記住，父元素上定義的調整大小特性（例如 <xref:System.Windows.Controls.Border> ）會影響其子系。

下圖顯示簡單的版面配置。

![顯示一般方格的螢幕擷取畫面，沒有迭迭的周框方塊。](./media/layout/grid-no-bounding-box-superimpose.png)

使用下列 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 可達成這個版面配置。

[!code-xaml[LayoutInformation#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]

單一 <xref:System.Windows.Controls.TextBlock> 元素裝載于內 <xref:System.Windows.Controls.Grid> 。 當文字只填滿第一個資料行的左上角時，為配置的空間 <xref:System.Windows.Controls.TextBlock> 其實會大得多。 您可以使用方法來抓取任何的周框方塊 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 。 下圖顯示元素的周框方塊 <xref:System.Windows.Controls.TextBlock> 。

![螢幕擷取畫面：顯示 [TextBlock 周框] 方塊現在是可見的。](./media/layout/visible-textblock-bounding-box.png)

如黃色矩形所示，元素的已配置空間 <xref:System.Windows.Controls.TextBlock> 實際上遠大於顯示。 當其他元素加入至時 <xref:System.Windows.Controls.Grid> ，此配置可能會縮小或展開，視新增的專案類型和大小而定。

的版面配置位置 <xref:System.Windows.Controls.TextBlock> 會使用方法轉譯成 <xref:System.Windows.Shapes.Path> <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 。 這種方式可用於顯示項目的週框方塊。

[!code-csharp[LayoutInformation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
[!code-vb[LayoutInformation#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]

<a name="LayoutSystem_Overview"></a>

## <a name="the-layout-system"></a>配置系統

簡單來說，版面配置是可調整項目大小、定位項目並在螢幕上繪製項目的遞迴系統。 更明確地說，版面配置會描述測量和排列專案集合成員的進程 <xref:System.Windows.Controls.Panel> <xref:System.Windows.Controls.Panel.Children%2A> 。 版面配置是需要大量處理的程序。 <xref:System.Windows.Controls.Panel.Children%2A>集合越大，必須進行的計算次數就愈大。 也可以根據擁有集合的元素所定義的版面配置行為來導入複雜性 <xref:System.Windows.Controls.Panel> 。 相較于更複雜的效能（例如），相當簡單的（ <xref:System.Windows.Controls.Panel> 例如 <xref:System.Windows.Controls.Canvas> ）可能會明顯比更好 <xref:System.Windows.Controls.Panel> <xref:System.Windows.Controls.Grid> 。

每次子系 <xref:System.Windows.UIElement> 變更其位置時，就有可能會由配置系統觸發新的傳遞。 因此，請務必了解可叫用配置系統的事件，因為不必要的叫用可能會導致不良的應用程式效能。 下列描述在叫用配置系統時所發生的程序。

1. 子系會 <xref:System.Windows.UIElement> 先將其核心屬性測量，以開始配置處理常式。

2. 會評估定義于的大小調整屬性 <xref:System.Windows.FrameworkElement> ，例如 <xref:System.Windows.FrameworkElement.Width%2A> 、 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Margin%2A> 。

3. <xref:System.Windows.Controls.Panel>-會套用特定的邏輯，例如 <xref:System.Windows.Controls.Dock> 方向或堆疊 <xref:System.Windows.Controls.StackPanel.Orientation%2A> 。

4. 測量所有子系之後，會排列內容。

5. <xref:System.Windows.Controls.Panel.Children%2A>集合會在螢幕上繪製。

6. 如果將額外的 <xref:System.Windows.Controls.Panel.Children%2A> 新增至集合、套用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> ，或呼叫方法，則會再次叫用進程 <xref:System.Windows.UIElement.UpdateLayout%2A> 。

下列各節會詳述定義此程序和其叫用方式。

<a name="LayoutSystem_Measure_Arrange"></a>

## <a name="measuring-and-arranging-children"></a>測量和排列子系

版面配置系統會針對集合的每個成員 <xref:System.Windows.Controls.Panel.Children%2A> 、量值傳遞和排列行程完成兩次傳遞。 每個子系都提供自己的 <xref:System.Windows.Controls.Panel> <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法，以達成自己的特定版面配置行為。

在量值傳遞期間，會評估集合的每個成員 <xref:System.Windows.Controls.Panel.Children%2A> 。 進程一開始會呼叫 <xref:System.Windows.UIElement.Measure%2A> 方法。 這個方法會在父元素的執行中呼叫 <xref:System.Windows.Controls.Panel> ，而且不需要明確呼叫，就能進行版面配置。

首先，會評估的原生大小屬性 <xref:System.Windows.UIElement> ，例如 <xref:System.Windows.UIElement.Clip%2A> 和 <xref:System.Windows.UIElement.Visibility%2A> 。 這會產生名為 `constraintSize` 的值，並將它傳遞給 <xref:System.Windows.FrameworkElement.MeasureCore%2A> 。

其次，會處理定義于的 framework 屬性 <xref:System.Windows.FrameworkElement> ，這會影響的值 `constraintSize` 。 這些屬性通常會描述基礎的調整大小特性 <xref:System.Windows.UIElement> ，例如它的 <xref:System.Windows.FrameworkElement.Height%2A> 、 <xref:System.Windows.FrameworkElement.Width%2A> 、 <xref:System.Windows.FrameworkElement.Margin%2A> 和 <xref:System.Windows.FrameworkElement.Style%2A> 。 所有這些屬性都可以變更顯示項目所需的空間。 <xref:System.Windows.FrameworkElement.MeasureOverride%2A>接著會使用 `constraintSize` 做為參數來呼叫。

> [!NOTE]
> 和的屬性和和之間的差異 <xref:System.Windows.FrameworkElement.Height%2A> <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement.ActualHeight%2A> <xref:System.Windows.FrameworkElement.ActualWidth%2A> 。 例如， <xref:System.Windows.FrameworkElement.ActualHeight%2A> 屬性是以其他高度輸入和版面配置系統為基礎的計算值。 根據實際的轉譯行程，此值是由配置系統本身設定，因此可能會稍微落後屬性的設定值（例如 <xref:System.Windows.FrameworkElement.Height%2A> ，這是輸入變更的基礎）。
>
> 因為 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 是一個計算值，所以您應該注意，由於版面配置系統的各種作業，可能會有多個或累加的報告變更。 配置系統可能會計算子項目所需的測量空間、父項目的條件約束，依此類推。

量值傳遞的最終目標是讓子系判斷其 <xref:System.Windows.UIElement.DesiredSize%2A> ，這會在呼叫期間發生 <xref:System.Windows.FrameworkElement.MeasureCore%2A> 。 <xref:System.Windows.UIElement.DesiredSize%2A>值是由儲存， <xref:System.Windows.UIElement.Measure%2A> 以便在內容排列階段期間使用。

「排列」傳遞會從方法的呼叫開始 <xref:System.Windows.UIElement.Arrange%2A> 。 在排列階段期間，父 <xref:System.Windows.Controls.Panel> 元素會產生代表子系界限的矩形。 這個值會傳遞至 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 方法以進行處理。

<xref:System.Windows.FrameworkElement.ArrangeCore%2A>方法會評估子系的， <xref:System.Windows.UIElement.DesiredSize%2A> 並評估可能影響元素轉譯大小的任何其他邊界。 <xref:System.Windows.FrameworkElement.ArrangeCore%2A>產生 `arrangeSize` ，其會傳遞至的 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法 <xref:System.Windows.Controls.Panel> 做為參數。 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>產生子系的 `finalSize` 。 最後， <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 方法會對 offset 屬性進行最後的評估（例如邊界和對齊），並將子系放在其版面配置位置。 子系不需要 (通常也不會) 填入整個已配置的空間。 控制項接著會傳回父代 <xref:System.Windows.Controls.Panel> ，而且版面配置程式已完成。

<a name="LayoutSystem_PanelsCustom"></a>

## <a name="panel-elements-and-custom-layout-behaviors"></a>面板項目和自訂版面配置行為

WPF 包含一個衍生自的元素群組 <xref:System.Windows.Controls.Panel> 。 這些 <xref:System.Windows.Controls.Panel> 元素可啟用許多複雜的版面配置。 例如，您可以使用專案輕鬆地完成堆疊專案 <xref:System.Windows.Controls.StackPanel> ，而更複雜且可用的流動版面配置則是使用 <xref:System.Windows.Controls.Canvas> 。

下表摘要說明可用的版面配置 <xref:System.Windows.Controls.Panel> 元素。

|面板名稱|描述|
|----------------|-----------------|
|<xref:System.Windows.Controls.Canvas>|定義一個區域，您可以在其中以相對於區域的座標，明確地定位子項目 <xref:System.Windows.Controls.Canvas> 。|
|<xref:System.Windows.Controls.DockPanel>|定義一個區域，可供您在其中以子元素彼此間相對的水平或垂直方式排列子元素。|
|<xref:System.Windows.Controls.Grid>|定義彈性的格線區域，由欄與列組成。|
|<xref:System.Windows.Controls.StackPanel>|將子元素排成單一行，以水平或垂直方式排列。|
|<xref:System.Windows.Controls.VirtualizingPanel>|提供 <xref:System.Windows.Controls.Panel> 項目的架構，這些項目會虛擬化其子資料集合。 這是 abstract 類別。|
|<xref:System.Windows.Controls.WrapPanel>|將子項目置放於由左至右的連續位置，其中會在包含方塊的邊緣將內容換至下一行。 後續順序會依照屬性的值，從上到下或由右至左順序進行 <xref:System.Windows.Controls.WrapPanel.Orientation%2A> 。|

對於需要使用任何預先定義之元素無法進行配置的應用程式 <xref:System.Windows.Controls.Panel> ，可以藉由繼承自 <xref:System.Windows.Controls.Panel> 並覆寫 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和方法，來達成自訂配置行為 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 。

<a name="LayoutSystem_Performance"></a>

## <a name="layout-performance-considerations"></a>版面配置效能考量

版面配置是遞迴程序。 集合中的每個子專案都會 <xref:System.Windows.Controls.Panel.Children%2A> 在配置系統的每次調用期間處理。 因此，不需要時，應該避免觸發配置系統。 下列考量可協助您達到更佳的效能。

- 請注意哪些屬性值變更將會由配置系統強制遞迴更新。

  使用公用旗標，可標記其值可以初始化配置系統的相依性屬性。 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>和 <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> 會提供有用的線索，以供配置系統強制執行遞迴更新的屬性值變更。 一般而言，任何可能影響專案周框方塊大小的屬性，都應該將 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> 旗標設定為 true。 如需詳細資訊，請參閱[相依性屬性概觀](dependency-properties-overview.md)。

- 可能的話，請使用， <xref:System.Windows.UIElement.RenderTransform%2A> 而不是 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 。

  <xref:System.Windows.FrameworkElement.LayoutTransform%2A>對於會影響的內容，可能是非常有用的方式 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 。 不過，如果轉換的效果不需要影響其他元素的位置，最好改為使用 <xref:System.Windows.UIElement.RenderTransform%2A> ，因為不會叫用 <xref:System.Windows.UIElement.RenderTransform%2A> 版面配置系統。 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>套用其轉換並強制遞迴配置更新，以考慮受影響專案的新位置。

- 避免不必要的呼叫 <xref:System.Windows.UIElement.UpdateLayout%2A> 。

  <xref:System.Windows.UIElement.UpdateLayout%2A>方法會強制執行遞迴版面配置更新，而且通常不是必要的。 除非您確定需要完整更新，否則請依賴配置系統來呼叫此方法。

- 使用大型 <xref:System.Windows.Controls.Panel.Children%2A> 集合時，請考慮使用， <xref:System.Windows.Controls.VirtualizingStackPanel> 而不是一般 <xref:System.Windows.Controls.StackPanel> 。

  藉由虛擬化子集合， <xref:System.Windows.Controls.VirtualizingStackPanel> 只會將物件保留在目前位於父系之區的記憶體中。 因此，在大部分情況下，都可以大幅改善效能。

<a name="LayoutSystem_LayoutRounding"></a>

## <a name="sub-pixel-rendering-and-layout-rounding"></a>子像素轉譯和版面配置進位

WPF 圖形系統使用裝置獨立單位來啟用解析度和裝置獨立性。 每個與裝置無關的圖元都會自動以系統的每英寸（DPI）設定來調整。 這會為 WPF 應用程式提供適當的調整，以進行不同的 DPI 設定，並讓應用程式自動感知 DPI。

不過，此 DPI 獨立性可能會因為消除鋸齒而建立不規則的邊緣轉譯。 如果邊緣位置落在裝置像素中間，而不是裝置像素之間，則這些成品一般會看起來模糊或具有半透明邊緣。 配置系統提供一種方式，利用版面配置來進行這項的調整。 版面配置進位是配置系統會在版面配置階段期間將任何非整數像素值四捨五入。

預設會停用版面配置進位。 若要啟用版面配置舍入，請將 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> 屬性設定為 `true` on any <xref:System.Windows.FrameworkElement> 。 因為這是相依性屬性，所以值將會傳播到視覺樹狀結構中的所有子系。 若要啟用整個 UI 的版面配置進位，請將 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> `true` 根容器上的設定為。 如需範例，請參閱 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>。

<a name="LayoutSystem_whatsnext"></a>

## <a name="whats-next"></a>後續步驟

了解如何測量和排列項目是了解版面配置的第一個步驟。 如需可用元素的詳細資訊 <xref:System.Windows.Controls.Panel> ，請參閱[面板總覽](../controls/panels-overview.md)。 若要進一步了解會影響版面配置的各種定位屬性，請參閱[對齊、邊界和填補概觀](alignment-margins-and-padding-overview.md)。 當您準備好將它全部放在輕量應用程式中時，請參閱[逐步解說：我的第一個 WPF 桌面應用程式](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。

## <a name="see-also"></a>另請參閱

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.UIElement>
- [面板概觀](../controls/panels-overview.md)
- [對齊、邊界和填補概觀](alignment-margins-and-padding-overview.md)
- [版面配置與設計](optimizing-performance-layout-and-design.md)

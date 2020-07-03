---
title: 使用純色和漸層繪製的概觀
description: 瞭解如何在 Windows Presentation Foundation （WPF）中使用物件，以純色、線性漸層和放射狀漸層繪製。
ms.date: 03/30/2017
helpviewer_keywords:
- solid colors [WPF], painting with
- painting with gradients [WPF]
- gradients [WPF], painting with
- brushes [WPF], painting with solid colors
- brushes [WPF], painting with gradients
- painting with solid colors [WPF]
ms.assetid: f5b182f3-c5c7-4cbe-9f2f-65e690d08255
ms.openlocfilehash: 957593d758afda06db106c99f6695294d4f84f73
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853669"
---
# <a name="painting-with-solid-colors-and-gradients-overview"></a>使用純色和漸層繪製的概觀

本主題描述如何使用 <xref:System.Windows.Media.SolidColorBrush> 、 <xref:System.Windows.Media.LinearGradientBrush> 和物件， <xref:System.Windows.Media.RadialGradientBrush> 以純色、線性漸層和放射狀漸層繪製。

<a name="solidcolor"></a>

## <a name="painting-an-area-with-a-solid-color"></a>使用純色繪製區域

在任何平臺中最常見的作業之一，就是使用實線繪製一個區域 <xref:System.Windows.Media.Color> 。 為了完成這項工作，會 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供 <xref:System.Windows.Media.SolidColorBrush> 類別。 下列各節說明使用繪製的不同方式 <xref:System.Windows.Media.SolidColorBrush> 。

<a name="solidcolorinxaml"></a>

### <a name="using-a-solidcolorbrush-in-xaml"></a>在 "XAML" 中使用 SolidColorBrush

若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中使用純色繪製區域，請使用下列其中一個選項。

- 依據名稱選取預先定義的單色筆刷。  例如，您可以將按鈕的設 <xref:System.Windows.Controls.Control.Background%2A> 為 "Red" 或 "MediumBlue"。  如需其他預先定義的純色筆刷清單，請參閱類別的靜態屬性 <xref:System.Windows.Media.Brushes> 。 以下是一個範例。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushNamedColor1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushnamedcolor1xaml)]

- 選擇 32 位元色板的其中一個色彩，方法是指定紅色、綠色及藍色的量來混合成單一純色。  指定 32 位元色板中其中一個色彩的格式為 "*#rrggbb*"，其中 *rr* 是指定紅色相對量的兩位數十六進位數字、*gg* 指定綠色的量，而 *bb* 則指定藍色的量。  此外，色彩可以指定為 "#*aarrggbb*"，其中 *aa* 指定色彩的 *alpha* 值 (也就是透明度)。 這個方法可以讓您建立部分透明的色彩。  在下列範例中，的 <xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Controls.Button> 是使用十六進位標記法設定為完全不透明的紅色。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushHex1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushhex1xaml)]

- 使用屬性標記語法來描述 <xref:System.Windows.Media.SolidColorBrush> 。 這個語法比較複雜，但是可以讓您指定額外設定，例如筆刷的不透明度。 在下列範例中， <xref:System.Windows.Controls.Control.Background%2A> 兩個元素的屬性 <xref:System.Windows.Controls.Button> 會設定為完全不透明的紅色。 第一個筆刷的色彩是用預先定義的色彩名稱來描述。 第二個筆刷的色彩則是用十六進位標記法來描述。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushPropertyTag1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushpropertytag1xaml)]

<a name="solidcolorsincode"></a>

### <a name="painting-with-a-solidcolorbrush-in-code"></a>在程式碼中使用 SolidColorBrush 繪製

若要在程式碼中使用純色繪製區域，請使用下列其中一個選項。

- 使用類別所提供的其中一個預先定義的筆刷 <xref:System.Windows.Media.Brushes> 。 在下列範例中，的 <xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Controls.Button> 是設定為 <xref:System.Windows.Media.Brushes.Red%2A> 。

  [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedBrush1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedbrush1csharp)]

- 建立 <xref:System.Windows.Media.SolidColorBrush> ，並 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 使用結構來設定其屬性 <xref:System.Windows.Media.Color> 。 您可以使用類別中預先定義的色彩，也可以使用 <xref:System.Windows.Media.Colors> <xref:System.Windows.Media.Color> 靜態方法來建立 <xref:System.Windows.Media.Color.FromArgb%2A> 。

  下列範例顯示如何 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 使用預先定義的色彩來設定的屬性 <xref:System.Windows.Media.SolidColorBrush> 。

  [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedColor1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedcolor1csharp)]

靜態可 <xref:System.Windows.Media.Color.FromArgb%2A> 讓您指定色彩的 Alpha、紅色、綠色和藍色值。 這些值的範圍通常都是 0-255。 例如，Alpha 值為 0 時表示色彩是完全透明的，而值為 255 時表示色彩是完全不透明的。 同樣地，紅色值為 0 時表示色彩中沒有紅色，而值為 255 時表示色彩中具有最大量的紅色。  在下列範例中，筆刷色彩是透過指定 Alpha、紅色、綠色及藍色值來加以描述。

[!code-csharp[BrushOverviewExamples_snip#SolidColorBrushfromArgbExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushfromargbexample1csharp)]

如需指定色彩的其他方式，請參閱 <xref:System.Windows.Media.Color> 參考主題。

<a name="gradient"></a>

## <a name="painting-an-area-with-a-gradient"></a>使用漸層繪製區域

漸層筆刷會使用多種色彩繪製區域，這些色彩會沿著某個軸逐漸相互融合。 您可以使用它們來建立光影效果，讓控制項有立體的感覺。 您也可以使用它們來模擬玻璃、金屬、水和其他平滑表面。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供兩種類型的漸層筆刷： <xref:System.Windows.Media.LinearGradientBrush> 和 <xref:System.Windows.Media.RadialGradientBrush> 。

<a name="lineargradientbrush"></a>

## <a name="linear-gradients"></a>線形漸層

會 <xref:System.Windows.Media.LinearGradientBrush> 繪製一個區域，其中包含沿著線條（漸層*軸*）定義的漸層。  您可以使用物件，透過漸層軸來指定漸層的色彩和位置 <xref:System.Windows.Media.GradientStop> 。  您也可以修改漸層軸，這可讓您建立水平和垂直漸層，以及反轉漸層方向。 漸層軸會在下一節中說明。 預設會建立對角線的漸層。

下列範例顯示能建立由四個色彩組成之線形漸層的程式碼。

[!code-xaml[GradientBrushExamples_snip#DiagonalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]

這個程式碼會產生下列漸層：

![對角線性漸層](./media/wcpsdk-graphicsmm-diaglgradient-nolabel.jpg "wcpsdk_graphicsmm_diaglgradient_nolabel")

> [!NOTE]
> 本主題中的漸層範例會使用預設座標系統來設定起始點和結束點。 預設座標系統是相對於週框方塊：0 表示週框方塊的 0%，而 1 表示週框方塊的 100%。 您可以藉由將屬性設定為值來變更此座標系統 <xref:System.Windows.Media.GradientBrush.MappingMode%2A> <xref:System.Windows.Media.BrushMappingMode.Absolute> 。 絕對座標系統不會相對於週框方塊。 值會直接在本機空間中解譯。

是漸層 <xref:System.Windows.Media.GradientStop> 筆刷的基本建立區塊。  漸層停駐點會 <xref:System.Windows.Media.GradientStop.Color%2A> 在沿著漸層軸的上指定 <xref:System.Windows.Media.GradientStop.Offset%2A> 。

- 漸層停駐點的屬性會指定漸層 <xref:System.Windows.Media.GradientStop.Color%2A> 停駐點的色彩。 您可以使用預先定義的色彩（由 <xref:System.Windows.Media.Colors> 類別提供），或藉由指定 ScRGB 或 ARGB 值來設定色彩。 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，您也可以使用十六進位標記法來描述色彩。 如需詳細資訊，請參閱 <xref:System.Windows.Media.Color> 結構。

- 漸層停駐點的屬性會指定漸層 <xref:System.Windows.Media.GradientStop.Offset%2A> 停駐點的色彩在漸層軸上的位置。 Offset 是，其 <xref:System.Double> 範圍介於0到1之間。 漸層停駐點的位移值越接近 0，色彩就越接近漸層起始點。 漸層的位移值越接近 1，色彩就越接近漸層結束點。

在漸層停駐點之間每個點的色彩，都是以線性插補成由兩個連結漸層停駐點所指定的色彩結合。 下圖將上一個範例中的漸層停駐點醒目提示。 圓圈標記出漸層停駐點的位置，虛線則表示漸層軸。

![線性漸層中的漸層停駐點](./media/wcpsdk-graphicsmm-4gradientstops.png "wcpsdk_graphicsmm_4gradientstops")

第一個漸層停駐點在位移 `0.0` 處指定黃色的色彩。  第二個漸層停駐點在位移 `0.25` 處指定紅色的色彩。  沿著漸層軸從左移到右時，這兩個停駐點之間的點會逐漸從黃色變成紅色。  第三個漸層停駐點在位移 `0.75` 處指定藍色的色彩。  第二個和第三個漸層停駐點之間的點會逐漸從紅色變成藍色。 第四個漸層停駐點在位移 `1.0` 處指定淡黃綠色的色彩。 第三個和第四個漸層停駐點之間的點會逐漸從藍色變成淡黃綠色。

<a name="gradientaxis"></a>

### <a name="the-gradient-axis"></a>漸層軸

如同之前所說明的，線性漸層筆刷的漸層停駐點會落在沿著線條 (漸層軸) 的位置上。 您可以使用筆刷的和屬性來變更線條的方向和 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 大小 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 。 藉由操作筆刷 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 和 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> ，您可以建立水準和垂直漸層、反轉漸層方向、緊縮漸層分佈，以及更多。

根據預設，線性漸層筆刷的 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 和相對於所 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 繪製的區域。 點 (0,0) 表示要繪製之區域的左上角，而 (1,1) 則表示要繪製之區域的右下角。 的預設值 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> <xref:System.Windows.Media.LinearGradientBrush> 為（0，0），其預設值 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 為（1，1），它會從左上角開始建立對角線漸層，並將其延伸至所繪製區域的右下角。 下圖顯示具有預設和之線性漸層筆刷的漸層軸 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 。

![對角線性漸層的漸層軸](./media/wcpsdk-graphicsmm-diagonalgradientaxis.png "wcpsdk_graphicsmm_diagonalgradientaxis")

下列範例顯示如何藉由指定筆刷的和來建立水準漸 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 層 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 。 請注意，漸層停駐點與先前範例中的一樣：藉由直接變更 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 和，漸層已 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 從對角線變更為水準。

[!code-xaml[GradientBrushExamples_snip#HorizontalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]

下圖顯示建立的漸層。 漸層軸以虛線標示，而漸層停駐點則以圓圈標示。

![水平線性漸層的漸層軸](./media/wcpsdk-graphicsmm-horizontalgradient.jpg "wcpsdk_graphicsmm_horizontalgradient")

下一個範例顯示如何建立垂直漸層。

[!code-xaml[GradientBrushExamples_snip#VerticalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]

下圖顯示建立的漸層。 漸層軸以虛線標示，而漸層停駐點則以圓圈標示。

![垂直漸層的漸層軸](./media/wcpsdk-graphicsmm-verticalgradient.jpg "wcpsdk_graphicsmm_verticalgradient")

<a name="radialgradients"></a>

## <a name="radial-gradients"></a>放射狀漸層

就像一樣 <xref:System.Windows.Media.LinearGradientBrush> ， <xref:System.Windows.Media.RadialGradientBrush> 會繪製一個區域，其中包含沿著軸混合在一起的色彩。 前述範例顯示線性漸層筆刷的軸是條直線。 放射狀漸層筆刷的軸則是由圓圈定義，其色彩會從其原點向外「放射」。

在下列範例中，會使用放射狀漸層筆刷來繪製矩形的內部。

[!code-xaml[GradientBrushExamples_snip#RadialGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/RadialGradientBrushExample.xaml#radialgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#RadialGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/RadialGradientBrushExample.cs#radialgradient1csharp)]

下圖顯示在上一個範例中建立的漸層。 其中已將筆刷的漸層停駐點醒目提示。 請注意，雖然結果不同，但是這個範例中的漸層停駐點與先前線性漸層筆刷範例中的漸層停駐點是相同的。

![放射狀漸層中的漸層停駐點](./media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops_rg")

<xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A>指定放射狀漸層筆刷漸層軸的起點。 漸層軸會從漸層原點放射至漸層圓圈。 筆刷的漸層圓形是由其 <xref:System.Windows.Media.RadialGradientBrush.Center%2A> 、 <xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A> 和屬性所定義 <xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A> 。

下圖顯示數個具有不同、、 <xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A> <xref:System.Windows.Media.RadialGradientBrush.Center%2A> <xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A> 和設定的放射狀漸層 <xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A> 。

![RadialGradientBrush 設定](./media/wcpsdk-graphicsmm-originscirclesandradii.gif "wcpsdk_graphicsmm_originscirclesandradii")具有不同 System.windows.media.radialgradientbrush.gradientorigin、中央、RadiusX 和 RadiusY 設定的具有。

<a name="specifyinggradientcolors"></a>

## <a name="specifying-transparent-or-partially-transparent-gradient-stops"></a>指定透明或部分透明的漸層停駐點

因為漸層停駐點不會提供不透明度屬性，所以您必須在標記中使用 ARGB 十六進位標記法來指定色彩的 Alpha 色板，或使用 <xref:System.Windows.Media.Color.FromScRgb%2A?displayProperty=nameWithType> 方法來建立透明或部分透明的漸層停駐點。 下列各節會說明如何使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 和程式碼建立部分透明的漸層停駐點。

<a name="argbsyntax"></a>

### <a name="specifying-color-opacity-in-xaml"></a>在 "XAML" 中指定色彩不透明度

在中 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以使用 ARGB 十六進位標記法來指定個別色彩的不透明度。 ARGB 十六進位標記法會使用下列語法：

`#` **aa** *rrggbb*

上一行中的 *aa* 代表用來指定色彩不透明度的兩位數十六進位值。 *rr*、*gg* 和 *bb* 分別代表用來指定色彩中紅色、綠色及藍色量的兩位數十六進位值。 每個十六進位位數的值可以是 0-9 或 A-F。 0 是最小的值，F 是最大的值。 Alpha 值為 00 時會指定完全透明的色彩，而 Alpha 值為 FF 時則會建立完全不透明的色彩。  在下列範例中，會使用十六進位 ARGB 標記法來指定兩種色彩。 第一個為部分透明 (具有 x20 的 Alpha 值)，而第二個則是完全不透明。

[!code-xaml[GradientBrushExamples_snip#TransparentGradientStopExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/GradientStopsExample.xaml#transparentgradientstopexample1xaml)]

<a name="fromscrgbsyntax"></a>

### <a name="specifying-color-opacity-in-code"></a>在程式碼中指定色彩不透明度

使用程式碼時，靜態 <xref:System.Windows.Media.Color.FromArgb%2A> 方法可讓您在建立色彩時指定 Alpha 值。 方法接受四個類型的參數 <xref:System.Byte> 。 第一個參數會指定色彩的 Alpha 色板，其他三個參數則會指定色彩的紅色、綠色及藍色值。 每個值都應介於 0 到 255 之間 (含 0 和 255)。 Alpha 值為 0 時會指定色彩為完全透明，而 Alpha 值為 255 時則指定色彩為完全不透明。 在下列範例中， <xref:System.Windows.Media.Color.FromArgb%2A> 方法是用來產生兩種色彩。 第一個色彩為部分透明 (具有 32 的 Alpha 值)，而第二個色彩則是完全不透明。

[!code-csharp[GradientBrushExamples_snip#TransparentGradientStopExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/GradientStopsExample.cs#transparentgradientstopexample1csharp)]

或者，您可以使用 <xref:System.Windows.Media.Color.FromScRgb%2A> 方法，它可讓您使用 ScRGB 值來建立色彩。

<a name="otherbrushes"></a>

## <a name="painting-with-images-drawings-visuals-and-patterns"></a>使用影像、繪圖、視覺效果及圖樣繪製

<xref:System.Windows.Media.ImageBrush>、 <xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush> 類別可讓您使用影像、繪圖或視覺效果繪製區域。 如需使用影像、繪圖及圖樣繪製的相關資訊，請參閱[使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)。

## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.SolidColorBrush>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- [使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)
- [筆刷轉換概觀](brush-transformation-overview.md)
- [圖形轉譯層](../advanced/graphics-rendering-tiers.md)

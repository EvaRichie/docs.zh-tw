---
title: 筆刷總覽
description: 探索如何透過 Windows Presentation Foundation （WPF）中的漸層和模式，以簡單的純色繪製來說明概念。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: 9bfd702d7a5a9d807e2b922874119c2bb2e68f39
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853720"
---
# <a name="wpf-brushes-overview"></a>WPF 筆刷概觀
螢幕上顯示的所有專案都是可見的，因為它是由筆刷繪製。 例如，筆刷是用來描述按鈕的背景、文字的前景，以及圖形的填滿。 本主題介紹使用筆刷繪製的概念 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ，並提供範例。 筆刷可讓您以任何項目 (從簡單的純色到複雜的圖樣和影像集) 繪製 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 物件。  
  
<a name="paintingwithbrush"></a>
## <a name="painting-with-a-brush"></a>使用筆刷繪製  
 「 <xref:System.Windows.Media.Brush> 繪製」含有其輸出的區域。 不同的筆刷有不同類型的輸出。 有些筆刷會以純色繪製區域，其他則具有漸層、圖樣、影像或繪圖。 下圖顯示每個不同類型的範例 <xref:System.Windows.Media.Brush> 。  
  
 ![筆刷類型](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
筆刷範例  
  
 大部分的視覺物件都可讓您指定其繪製方式。 下表列出一些可供您使用的一般物件和屬性 <xref:System.Windows.Media.Brush> 。  
  
|類別|筆刷屬性|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 下列各節說明不同的 <xref:System.Windows.Media.Brush> 類型，並提供每個型別的範例。  
  
<a name="paintwithsolidcolorbrush"></a>
## <a name="paint-with-a-solid-color"></a>以純色繪製  
 會 <xref:System.Windows.Media.SolidColorBrush> 使用純色繪製區域 <xref:System.Windows.Media.Color> 。 有多種方式可以指定的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.SolidColorBrush> ：例如，您可以指定其 Alpha、紅色、藍色和綠色的通道，或使用類別所提供的其中一個預先定義色彩 <xref:System.Windows.Media.Colors> 。  
  
 下列範例會使用 <xref:System.Windows.Media.SolidColorBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![使用 SolidColorBrush 繪製的矩形](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
使用 SolidColorBrush 繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.SolidColorBrush> ，請參閱[使用純色和漸層繪製的色彩](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithlineargradientbrush"></a>
## <a name="paint-with-a-linear-gradient"></a>以線性漸層繪製  
 會 <xref:System.Windows.Media.LinearGradientBrush> 使用線性漸層繪製區域。 線性漸層會沿著一條線 (漸層軸) 混合兩個或更多色彩。 您可以使用 <xref:System.Windows.Media.GradientStop> 物件來指定漸層中的色彩和其位置。  
  
 下列範例會使用 <xref:System.Windows.Media.LinearGradientBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![使用 LinearGradientBrush 繪製的矩形](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
使用 LinearGradientBrush 繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.LinearGradientBrush> ，請參閱[使用純色和漸層繪製的色彩](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithradialgradientbrush"></a>
## <a name="paint-with-a-radial-gradient"></a>使用放射狀漸層繪製  
 會 <xref:System.Windows.Media.RadialGradientBrush> 繪製具有放射漸層的區域。 放射狀漸層會將兩個或多個色彩混合在一個圓形上。 如同 <xref:System.Windows.Media.LinearGradientBrush> 類別，您可以使用 <xref:System.Windows.Media.GradientStop> 物件來指定漸層中的色彩和其位置。  
  
 下列範例會使用 <xref:System.Windows.Media.RadialGradientBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![使用 RadialGradientBrush 繪製的矩形](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
使用 RadialGradientBrush 繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.RadialGradientBrush> ，請參閱[使用純色和漸層繪製的色彩](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithimage"></a>
## <a name="paint-with-an-image"></a>使用影像繪製  
 會 <xref:System.Windows.Media.ImageBrush> 使用繪製區域 <xref:System.Windows.Media.ImageSource> 。  
  
 下列範例會使用 <xref:System.Windows.Media.ImageBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![ImageBrush 所繪製的矩形](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
使用影像繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.ImageBrush> ，請參閱[使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithdrawing"></a>
## <a name="paint-with-a-drawing"></a>使用繪圖繪製  
 會 <xref:System.Windows.Media.DrawingBrush> 使用繪製區域 <xref:System.Windows.Media.Drawing> 。 <xref:System.Windows.Media.Drawing>可以包含圖形、影像、文字和媒體。  
  
 下列範例會使用 <xref:System.Windows.Media.DrawingBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![使用 DrawingBrush 繪製的矩形](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
使用 DrawingBrush 繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.DrawingBrush> ，請參閱[使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithvisual"></a>
## <a name="paint-with-a-visual"></a>使用視覺效果繪製  
 會 <xref:System.Windows.Media.VisualBrush> 使用物件繪製區域 <xref:System.Windows.Media.Visual> 。 視覺物件的範例包括 <xref:System.Windows.Controls.Button> 、 <xref:System.Windows.Controls.Page> 和 <xref:System.Windows.Controls.MediaElement> 。 <xref:System.Windows.Media.VisualBrush>也可讓您將應用程式的某個部分的內容投影到另一個區域; 它非常適合用來建立反映效果和螢幕的放大鏡部分。  
  
 下列範例會使用 <xref:System.Windows.Media.VisualBrush> 來繪製的 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle> 。 下圖顯示繪製的矩形。  
  
 ![使用 VisualBrush 繪製的矩形](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
使用 VisualBrush 繪製的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 如需類別的詳細資訊 <xref:System.Windows.Media.VisualBrush> ，請參閱[使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>
## <a name="paint-using-predefined-and-system-brushes"></a>使用預先定義和系統筆刷繪製  
 為了方便起見，Windows Presentation Foundation （WPF）提供一組預先定義和可用來繪製物件的系統筆刷。  
  
- 如需可用預先定義的筆刷清單，請參閱 <xref:System.Windows.Media.Brushes> 類別。 如需顯示如何使用預先定義筆刷的範例，請參閱[使用純色繪製區域](how-to-paint-an-area-with-a-solid-color.md)。  
  
- 如需可用系統筆刷的清單，請參閱 <xref:System.Windows.SystemColors> 類別。 如需範例，請參閱[使用系統筆刷繪製區域](how-to-paint-an-area-with-a-system-brush.md)。  
  
<a name="commonbrushfeatures"></a>
## <a name="common-brush-features"></a>一般筆刷功能  
 <xref:System.Windows.Media.Brush>物件提供 <xref:System.Windows.Media.Brush.Opacity%2A> 屬性，可用來將筆刷透明化或部分透明。 <xref:System.Windows.Media.Brush.Opacity%2A>值為0會使筆刷完全透明，而 <xref:System.Windows.Media.Brush.Opacity%2A> 值為1則會使筆刷完全不透明。 下列範例會使用 <xref:System.Windows.Media.Brush.Opacity%2A> 屬性來使 <xref:System.Windows.Media.SolidColorBrush> 25% 不透明。  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 如果筆刷包含部分透明的色彩，則色彩的不透明度值會透過乘法與筆刷的不透明度值結合。 例如，如果筆刷的不透明度值為0.5，而筆刷中使用的色彩也具有不透明度值0.5，則輸出色彩會有不透明度值0.25。  
  
> [!NOTE]
> 變更筆刷的不透明度值會比較有效率，而不是使用其屬性來變更整個專案的不透明度 <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> 。  
  
 您可以使用其或屬性來旋轉、縮放、扭曲和轉譯筆刷的 <xref:System.Windows.Media.Brush.Transform%2A> 內容 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 。 如需詳細資訊，請參閱[筆刷轉換總覽](brush-transformation-overview.md)。  
  
 因為它們是 <xref:System.Windows.Media.Animation.Animatable> 物件，所以 <xref:System.Windows.Media.Brush> 可以動畫顯示物件。 如需詳細資訊，請參閱[動畫總覽](animation-overview.md)。  
  
<a name="freezable_features"></a>
### <a name="freezable-features"></a>Freezable 功能  
 因為它繼承自 <xref:System.Windows.Freezable> 類別，所以 <xref:System.Windows.Media.Brush> 類別會提供幾個特殊功能： <xref:System.Windows.Media.Brush> 物件可以宣告為[資源](../../../desktop-wpf/fundamentals/xaml-resources-define.md)、在多個物件之間共用，以及複製。 此外， <xref:System.Windows.Media.Brush> 除了以外的所有類型都 <xref:System.Windows.Media.VisualBrush> 可以設為唯讀，以改善效能並使其成為安全線程。  
  
 如需物件所提供之不同功能的詳細資訊 <xref:System.Windows.Freezable> ，請參閱可[凍結物件總覽](../advanced/freezable-objects-overview.md)。  
  
 如需為何 <xref:System.Windows.Media.VisualBrush> 無法凍結物件的詳細資訊，請參閱 <xref:System.Windows.Media.VisualBrush> 類型頁面。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [使用純色和漸層繪製的概觀](painting-with-solid-colors-and-gradients-overview.md)
- [使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)
- [Freezable 物件概觀](../advanced/freezable-objects-overview.md)
- [筆刷範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)
- [ImageBrush 範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ImageBrush)
- [VisualBrush 範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/VisualBrush)
- [操作說明主題](brushes-how-to-topics.md)
- [其他效能建議](../advanced/optimizing-performance-other-recommendations.md)

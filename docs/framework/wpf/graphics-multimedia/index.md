---
title: 圖形和多媒體
description: 探索 Windows Presentation Foundation （WPF）的媒體功能。 將圖形、轉換效果、音效和影片新增至您的應用程式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- media [WPF], features
- video effects [WPF]
- sound effects [WPF]
- animation [WPF], features
- graphics features [WPF]
- transition effects [WPF]
ms.assetid: 1817d9dc-3d6c-46cb-afc8-63b0bae35e37
ms.openlocfilehash: ba52e78564484f7714ab0035a5e1861766b72bbf
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853678"
---
# <a name="graphics-and-multimedia"></a>圖形和多媒體

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 支援多媒體、向量圖形、動畫和內容組合，方便開發人員建置有趣的使用者介面和內容。 您可以使用 Visual Studio 建立向量圖形或複雜的動畫，並將媒體整合到您的應用程式中。

本主題介紹 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的圖形、動畫和媒體功能，其可讓您將圖形、轉換效果、音效以及視訊新增至您的應用程式。

> [!NOTE]
> 強烈建議不要在 Windows 服務中使用 WPF 類型。 如果您嘗試在 Windows 服務中使用 WPF 類型，該服務可能無法如預期般運作。

<a name="whats_new_with_graphics_and_multimedia_in_wpf_4"></a>

## <a name="whats-new-with-graphics-and-multimedia-in-wpf-4"></a>WPF 4 中圖形和多媒體的新功能

圖形和動畫有數項相關變更。

- 版面配置進位

  當物件邊緣位於像素裝置中間時，DPI 獨立圖形系統可以建立轉譯成品，例如模糊或半透明的邊緣。 先前的 WPF 版本包含像素貼齊功能來協助處理這種情況。 Silverlight 2 引進版面配置進位，這是另一種移動元素以讓邊緣落在整個像素邊界上的方法。 WPF 現在支援在上使用附加屬性進行版面配置舍入 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> <xref:System.Windows.FrameworkElement> 。

- 快取的組合

  藉由使用新的 <xref:System.Windows.Media.BitmapCache> 和 <xref:System.Windows.Media.BitmapCacheBrush> 類別，您可以將視覺化樹狀結構的複雜部分快取為點陣圖，並大幅改善轉譯時間。 點陣圖仍可持續回應滑鼠點選之類的使用者輸入，您也可以將它繪製在其他元素上，就像筆刷一般。

- 像素著色器 3 支援

  WPF 4 是以 <xref:System.Windows.Media.Effects.ShaderEffect> wpf 3.5 SP1 中引進的支援為基礎，允許應用程式使用圖元著色器（PS）3.0 版來寫入效果。 PS 3.0 著色器模型比 PS 2.0 更為複雜，其在支援的硬體上允許使用更多效果。

- Easing 函式

  您可以利用 Easing 函式讓您進一步控制動畫的行為來美化動畫。 例如，您可以將套用 <xref:System.Windows.Media.Animation.ElasticEase> 至動畫，為動畫提供 springy 的行為。 如需詳細資訊，請參閱命名空間中的緩動類型 <xref:System.Windows.Media.Animation> 。

<a name="graphics_and_rendering"></a>

## <a name="graphics-and-rendering"></a>圖形和轉譯

WPF 包含高品質2D 圖形的支援。 這些功能包括筆刷、幾何、影像、圖形及轉換。 如需詳細資訊，請參閱[圖形](graphics.md)。 圖形元素的呈現是以類別為基礎 <xref:System.Windows.Media.Visual> 。 螢幕上視覺物件的結構是由視覺化樹狀結構描繪。 如需詳細資訊，請參閱 [WPF 圖形轉譯概觀](wpf-graphics-rendering-overview.md)。

### <a name="2d-shapes"></a>2D 圖形

WPF 提供常用的向量繪製2D 圖形的程式庫，例如矩形和橢圓形，如下圖所示。

![顯示橢圓形和矩形的圖表。](./media/index/two-deminsional-shapes-ellipses-rectangles.png)

這些內部 WPF 圖形不只是圖形：它們是可程式化的專案，這些專案會實作為大部分通用控制項（包括鍵盤和滑鼠輸入）所預期的許多功能。 下列範例顯示如何藉由按一下專案來處理 <xref:System.Windows.UIElement.MouseUp> 引發的事件 <xref:System.Windows.Shapes.Ellipse> 。

```xaml
<Window
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="Window1" >
  <Ellipse Fill="LightBlue" MouseUp="ellipseButton_MouseUp" />
</Window>
```

```csharp
public partial class Window1  : Window
{
    void ellipseButton_MouseUp(object sender, MouseButtonEventArgs e)
    {
        MessageBox.Show("You clicked the ellipse!");
    }
}
```

```vb
Partial Public Class Window1
    Inherits Window
    Private Sub ellipseButton_MouseUp(ByVal sender As Object, ByVal e As MouseButtonEventArgs)
        MessageBox.Show("You clicked the ellipse!")
    End Sub
End Class
```

下圖顯示上述 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記和程式碼後置的輸出。

![指出「您已按下橢圓形！」的訊息方塊](./media/index/messagebox-text-output.png)

如需詳細資訊，請參閱[WPF 中的圖形和基本繪圖總覽](shapes-and-basic-drawing-in-wpf-overview.md)。 如需簡介範例，請參閱[圖形元素範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)。

### <a name="2d-geometries"></a>2D 幾何

當 WPF 提供的2D 圖形不夠時，您可以使用 geometry 和 path 的 WPF 支援來建立自己的幾何和路徑。 下圖顯示如何使用幾何來建立圖形、繪製筆刷，以及裁剪其他 WPF 元素。

![螢幕擷取畫面：顯示如何使用幾何來建立圖形。](./media/index/use-geometries-create-shapes.png)

如需詳細資訊，請參閱[Geometry 總覽](geometry-overview.md)。 如需簡介範例，請參閱[幾何範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Geometry)。

### <a name="2d-effects"></a>2D 效果

WPF 提供2D 類別的程式庫，可讓您用來建立各種效果。 WPF 的2D 轉譯功能可讓您繪製具有漸層 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 、點陣圖、繪圖和影片的專案，以及使用旋轉、縮放和扭曲來操作這些專案。 下圖提供使用 WPF 筆刷可以達成的許多效果範例。

![此圖顯示不同的 WPF 筆刷和油漆元素。](./media/index/brushes-paint-elements.png)

如需詳細資訊，請參閱[WPF 筆刷總覽](wpf-brushes-overview.md)。 如需簡介範例，請參閱[筆刷範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)。

<a name="rendering"></a>

## <a name="3d-rendering"></a>3D 呈現

WPF 提供一組3D 轉譯功能，可與 WPF 中的2D 圖形支援整合，讓您建立更棒的版面配置 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 和資料視覺效果。 在範圍的一端，WPF 可讓您將2D 影像轉譯到3D 圖形的表面，如下圖所示。

![顯示具有不同材質之3D 圖形的範例螢幕擷取畫面。](./media/index/visual-three-dimensional-shape.png)

如需詳細資訊，請參閱[3D 圖形總覽](3-d-graphics-overview.md)。 如需簡介範例，請參閱[3D 純色範例](https://go.microsoft.com/fwlink/?LinkID=159964)。

<a name="animation"></a>

## <a name="animation"></a>動畫

使用動畫讓控制項和元素放大、搖晃、旋轉和淡出，以及建立有趣的網頁切換及執行其他工作。 因為 WPF 可讓您以動畫顯示大部分的屬性，您不僅可以建立大部分 WPF 物件的動畫，也可以使用 WPF 以動畫顯示您所建立的自訂物件。

![動畫 cube 的螢幕擷取畫面。](./media/index/animate-custom-objects.png)

如需詳細資訊，請參閱[動畫總覽](animation-overview.md)。 如需簡介範例，請參閱[動畫範例圖庫](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationExamples)。

<a name="media"></a>

## <a name="media"></a>媒體

影像、視訊和音訊都是以媒體功能豐富的方式傳達資訊和使用者體驗。

### <a name="images"></a>影像

包括圖示、背景，甚至動畫組件的影像，是大部分應用程式的核心組件。 因為您經常需要使用影像，所以 WPF 會以各種不同的方式來公開使用它們。 下圖顯示眾多方式的其中之一。

![樣式設定範例螢幕擷取畫面](../controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")

如需詳細資訊，請參閱[影像處理總覽](imaging-overview.md)。

### <a name="video-and-audio"></a>視訊和音訊

WPF 圖形功能的核心功能是提供使用多媒體的原生支援，包括影片和音訊。 下列範例示範如何將媒體播放程式插入至應用程式。

```xaml
<MediaElement Source="media\numbers.wmv" Width="450" Height="250" />
```

<xref:System.Windows.Controls.MediaElement>能夠同時播放影片和音訊，而且可以擴充，以允許輕鬆建立自訂 Ui。

如需詳細資訊，請參閱[多媒體概觀](multimedia-overview.md)。

## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Media>
- <xref:System.Windows.Media.Animation>
- <xref:System.Windows.Media.Media3D>
- [2D 圖形和影像處理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [WPF 中圖案和基本繪圖概觀](shapes-and-basic-drawing-in-wpf-overview.md)
- [使用純色和漸層繪製的概觀](painting-with-solid-colors-and-gradients-overview.md)
- [使用影像、繪圖和視覺效果繪製](painting-with-images-drawings-and-visuals.md)
- [動畫和計時 HOW TO 主題](animation-and-timing-how-to-topics.md)
- [3D 圖形概觀](3-d-graphics-overview.md)
- [多媒體概觀](multimedia-overview.md)

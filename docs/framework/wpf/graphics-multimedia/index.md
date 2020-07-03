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
# <a name="graphics-and-multimedia"></a><span data-ttu-id="e49b6-104">圖形和多媒體</span><span class="sxs-lookup"><span data-stu-id="e49b6-104">Graphics and Multimedia</span></span>

<a name="introduction"></a>
<span data-ttu-id="e49b6-105">[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 支援多媒體、向量圖形、動畫和內容組合，方便開發人員建置有趣的使用者介面和內容。</span><span class="sxs-lookup"><span data-stu-id="e49b6-105">[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] provides support for multimedia, vector graphics, animation, and content composition, making it easy for developers to build interesting user interfaces and content.</span></span> <span data-ttu-id="e49b6-106">您可以使用 Visual Studio 建立向量圖形或複雜的動畫，並將媒體整合到您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e49b6-106">Using Visual Studio, you can create vector graphics or complex animations and integrate media into your applications.</span></span>

<span data-ttu-id="e49b6-107">本主題介紹 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的圖形、動畫和媒體功能，其可讓您將圖形、轉換效果、音效以及視訊新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49b6-107">This topic introduces the graphics, animation, and media features of [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], which enable you to add graphics, transition effects, sound, and video to your applications.</span></span>

> [!NOTE]
> <span data-ttu-id="e49b6-108">強烈建議不要在 Windows 服務中使用 WPF 類型。</span><span class="sxs-lookup"><span data-stu-id="e49b6-108">Using WPF types in a Windows service is strongly discouraged.</span></span> <span data-ttu-id="e49b6-109">如果您嘗試在 Windows 服務中使用 WPF 類型，該服務可能無法如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="e49b6-109">If you attempt to use WPF types in a Windows service, the service may not work as expected.</span></span>

<a name="whats_new_with_graphics_and_multimedia_in_wpf_4"></a>

## <a name="whats-new-with-graphics-and-multimedia-in-wpf-4"></a><span data-ttu-id="e49b6-110">WPF 4 中圖形和多媒體的新功能</span><span class="sxs-lookup"><span data-stu-id="e49b6-110">What's New with Graphics and Multimedia in WPF 4</span></span>

<span data-ttu-id="e49b6-111">圖形和動畫有數項相關變更。</span><span class="sxs-lookup"><span data-stu-id="e49b6-111">Several changes have been made related to graphics and animations.</span></span>

- <span data-ttu-id="e49b6-112">版面配置進位</span><span class="sxs-lookup"><span data-stu-id="e49b6-112">Layout Rounding</span></span>

  <span data-ttu-id="e49b6-113">當物件邊緣位於像素裝置中間時，DPI 獨立圖形系統可以建立轉譯成品，例如模糊或半透明的邊緣。</span><span class="sxs-lookup"><span data-stu-id="e49b6-113">When an object edge falls in the middle of a pixel device, the DPI-independent graphics system can create rendering artifacts, such as blurry or semi-transparent edges.</span></span> <span data-ttu-id="e49b6-114">先前的 WPF 版本包含像素貼齊功能來協助處理這種情況。</span><span class="sxs-lookup"><span data-stu-id="e49b6-114">Previous versions of WPF included pixel snapping to help handle this case.</span></span> <span data-ttu-id="e49b6-115">Silverlight 2 引進版面配置進位，這是另一種移動元素以讓邊緣落在整個像素邊界上的方法。</span><span class="sxs-lookup"><span data-stu-id="e49b6-115">Silverlight 2 introduced layout rounding, which is another way to move elements so that edges fall on whole pixel boundaries.</span></span> <span data-ttu-id="e49b6-116">WPF 現在支援在上使用附加屬性進行版面配置舍入 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> <xref:System.Windows.FrameworkElement> 。</span><span class="sxs-lookup"><span data-stu-id="e49b6-116">WPF now supports layout rounding with the <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> attached property on <xref:System.Windows.FrameworkElement>.</span></span>

- <span data-ttu-id="e49b6-117">快取的組合</span><span class="sxs-lookup"><span data-stu-id="e49b6-117">Cached Composition</span></span>

  <span data-ttu-id="e49b6-118">藉由使用新的 <xref:System.Windows.Media.BitmapCache> 和 <xref:System.Windows.Media.BitmapCacheBrush> 類別，您可以將視覺化樹狀結構的複雜部分快取為點陣圖，並大幅改善轉譯時間。</span><span class="sxs-lookup"><span data-stu-id="e49b6-118">By using the new <xref:System.Windows.Media.BitmapCache> and <xref:System.Windows.Media.BitmapCacheBrush> classes, you can cache a complex part of the visual tree as a bitmap and greatly improve rendering time.</span></span> <span data-ttu-id="e49b6-119">點陣圖仍可持續回應滑鼠點選之類的使用者輸入，您也可以將它繪製在其他元素上，就像筆刷一般。</span><span class="sxs-lookup"><span data-stu-id="e49b6-119">The bitmap remains responsive to user input, such as mouse clicks, and you can paint it onto other elements just like any brush.</span></span>

- <span data-ttu-id="e49b6-120">像素著色器 3 支援</span><span class="sxs-lookup"><span data-stu-id="e49b6-120">Pixel Shader 3 Support</span></span>

  <span data-ttu-id="e49b6-121">WPF 4 是以 <xref:System.Windows.Media.Effects.ShaderEffect> wpf 3.5 SP1 中引進的支援為基礎，允許應用程式使用圖元著色器（PS）3.0 版來寫入效果。</span><span class="sxs-lookup"><span data-stu-id="e49b6-121">WPF 4 builds on top of the <xref:System.Windows.Media.Effects.ShaderEffect> support introduced in WPF 3.5 SP1 by allowing applications to write effects by using Pixel Shader (PS) version 3.0.</span></span> <span data-ttu-id="e49b6-122">PS 3.0 著色器模型比 PS 2.0 更為複雜，其在支援的硬體上允許使用更多效果。</span><span class="sxs-lookup"><span data-stu-id="e49b6-122">The PS 3.0 shader model is more sophisticated than PS 2.0, which allows for even more effects on supported hardware.</span></span>

- <span data-ttu-id="e49b6-123">Easing 函式</span><span class="sxs-lookup"><span data-stu-id="e49b6-123">Easing Functions</span></span>

  <span data-ttu-id="e49b6-124">您可以利用 Easing 函式讓您進一步控制動畫的行為來美化動畫。</span><span class="sxs-lookup"><span data-stu-id="e49b6-124">You can enhance animations with easing functions, which give you additional control over the behavior of animations.</span></span> <span data-ttu-id="e49b6-125">例如，您可以將套用 <xref:System.Windows.Media.Animation.ElasticEase> 至動畫，為動畫提供 springy 的行為。</span><span class="sxs-lookup"><span data-stu-id="e49b6-125">For example, you can apply an <xref:System.Windows.Media.Animation.ElasticEase> to an animation to give the animation a springy behavior.</span></span> <span data-ttu-id="e49b6-126">如需詳細資訊，請參閱命名空間中的緩動類型 <xref:System.Windows.Media.Animation> 。</span><span class="sxs-lookup"><span data-stu-id="e49b6-126">For more information, see the easing types in the <xref:System.Windows.Media.Animation> namespace.</span></span>

<a name="graphics_and_rendering"></a>

## <a name="graphics-and-rendering"></a><span data-ttu-id="e49b6-127">圖形和轉譯</span><span class="sxs-lookup"><span data-stu-id="e49b6-127">Graphics and Rendering</span></span>

<span data-ttu-id="e49b6-128">WPF 包含高品質2D 圖形的支援。</span><span class="sxs-lookup"><span data-stu-id="e49b6-128">WPF includes support for high quality 2D graphics.</span></span> <span data-ttu-id="e49b6-129">這些功能包括筆刷、幾何、影像、圖形及轉換。</span><span class="sxs-lookup"><span data-stu-id="e49b6-129">The functionality includes brushes, geometries, images, shapes and transformations.</span></span> <span data-ttu-id="e49b6-130">如需詳細資訊，請參閱[圖形](graphics.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-130">For more information, see [Graphics](graphics.md).</span></span> <span data-ttu-id="e49b6-131">圖形元素的呈現是以類別為基礎 <xref:System.Windows.Media.Visual> 。</span><span class="sxs-lookup"><span data-stu-id="e49b6-131">The rendering of graphical elements is based on the <xref:System.Windows.Media.Visual> class.</span></span> <span data-ttu-id="e49b6-132">螢幕上視覺物件的結構是由視覺化樹狀結構描繪。</span><span class="sxs-lookup"><span data-stu-id="e49b6-132">The structure of visual objects on the screen is described by the visual tree.</span></span> <span data-ttu-id="e49b6-133">如需詳細資訊，請參閱 [WPF 圖形轉譯概觀](wpf-graphics-rendering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-133">For more information, see [WPF Graphics Rendering Overview](wpf-graphics-rendering-overview.md).</span></span>

### <a name="2d-shapes"></a><span data-ttu-id="e49b6-134">2D 圖形</span><span class="sxs-lookup"><span data-stu-id="e49b6-134">2D Shapes</span></span>

<span data-ttu-id="e49b6-135">WPF 提供常用的向量繪製2D 圖形的程式庫，例如矩形和橢圓形，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="e49b6-135">WPF provides a library of commonly used, vector-drawn 2D shapes, such as rectangles and ellipses, which the following illustration shows.</span></span>

![顯示橢圓形和矩形的圖表。](./media/index/two-deminsional-shapes-ellipses-rectangles.png)

<span data-ttu-id="e49b6-137">這些內部 WPF 圖形不只是圖形：它們是可程式化的專案，這些專案會實作為大部分通用控制項（包括鍵盤和滑鼠輸入）所預期的許多功能。</span><span class="sxs-lookup"><span data-stu-id="e49b6-137">These intrinsic WPF shapes are not just shapes: they are programmable elements that implement many of the features that you expect from most common controls, which include keyboard and mouse input.</span></span> <span data-ttu-id="e49b6-138">下列範例顯示如何藉由按一下專案來處理 <xref:System.Windows.UIElement.MouseUp> 引發的事件 <xref:System.Windows.Shapes.Ellipse> 。</span><span class="sxs-lookup"><span data-stu-id="e49b6-138">The following example shows how to handle the <xref:System.Windows.UIElement.MouseUp> event raised by clicking an <xref:System.Windows.Shapes.Ellipse> element.</span></span>

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

<span data-ttu-id="e49b6-139">下圖顯示上述 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 標記和程式碼後置的輸出。</span><span class="sxs-lookup"><span data-stu-id="e49b6-139">The following illustration shows the output for the preceding [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] markup and code-behind.</span></span>

![指出「您已按下橢圓形！」的訊息方塊](./media/index/messagebox-text-output.png)

<span data-ttu-id="e49b6-141">如需詳細資訊，請參閱[WPF 中的圖形和基本繪圖總覽](shapes-and-basic-drawing-in-wpf-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-141">For more information, see [Shapes and Basic Drawing in WPF Overview](shapes-and-basic-drawing-in-wpf-overview.md).</span></span> <span data-ttu-id="e49b6-142">如需簡介範例，請參閱[圖形元素範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-142">For an introductory sample, see [Shape Elements Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/ShapeElements).</span></span>

### <a name="2d-geometries"></a><span data-ttu-id="e49b6-143">2D 幾何</span><span class="sxs-lookup"><span data-stu-id="e49b6-143">2D Geometries</span></span>

<span data-ttu-id="e49b6-144">當 WPF 提供的2D 圖形不夠時，您可以使用 geometry 和 path 的 WPF 支援來建立自己的幾何和路徑。</span><span class="sxs-lookup"><span data-stu-id="e49b6-144">When the 2D shapes that WPF provides are not sufficient, you can use WPF support for geometries and paths to create your own.</span></span> <span data-ttu-id="e49b6-145">下圖顯示如何使用幾何來建立圖形、繪製筆刷，以及裁剪其他 WPF 元素。</span><span class="sxs-lookup"><span data-stu-id="e49b6-145">The following illustration shows how you can use geometries to create shapes, as a drawing brush, and to clip other WPF elements.</span></span>

![螢幕擷取畫面：顯示如何使用幾何來建立圖形。](./media/index/use-geometries-create-shapes.png)

<span data-ttu-id="e49b6-147">如需詳細資訊，請參閱[Geometry 總覽](geometry-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-147">For more information, see [Geometry Overview](geometry-overview.md).</span></span> <span data-ttu-id="e49b6-148">如需簡介範例，請參閱[幾何範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Geometry)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-148">For an introductory sample, see [Geometries Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Geometry).</span></span>

### <a name="2d-effects"></a><span data-ttu-id="e49b6-149">2D 效果</span><span class="sxs-lookup"><span data-stu-id="e49b6-149">2D Effects</span></span>

<span data-ttu-id="e49b6-150">WPF 提供2D 類別的程式庫，可讓您用來建立各種效果。</span><span class="sxs-lookup"><span data-stu-id="e49b6-150">WPF provides a library of 2D classes that you can use to create a variety of effects.</span></span> <span data-ttu-id="e49b6-151">WPF 的2D 轉譯功能可讓您繪製具有漸層 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 、點陣圖、繪圖和影片的專案，以及使用旋轉、縮放和扭曲來操作這些專案。</span><span class="sxs-lookup"><span data-stu-id="e49b6-151">The 2D rendering capability of WPF provides the ability to paint [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] elements that have gradients, bitmaps, drawings, and videos; and to manipulate them by using rotation, scaling, and skewing.</span></span> <span data-ttu-id="e49b6-152">下圖提供使用 WPF 筆刷可以達成的許多效果範例。</span><span class="sxs-lookup"><span data-stu-id="e49b6-152">The following illustration gives an example of the many effects you can achieve by using WPF brushes.</span></span>

![此圖顯示不同的 WPF 筆刷和油漆元素。](./media/index/brushes-paint-elements.png)

<span data-ttu-id="e49b6-154">如需詳細資訊，請參閱[WPF 筆刷總覽](wpf-brushes-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-154">For more information, see [WPF Brushes Overview](wpf-brushes-overview.md).</span></span> <span data-ttu-id="e49b6-155">如需簡介範例，請參閱[筆刷範例](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-155">For an introductory sample, see [Brushes Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Brushes).</span></span>

<a name="rendering"></a>

## <a name="3d-rendering"></a><span data-ttu-id="e49b6-156">3D 呈現</span><span class="sxs-lookup"><span data-stu-id="e49b6-156">3D Rendering</span></span>

<span data-ttu-id="e49b6-157">WPF 提供一組3D 轉譯功能，可與 WPF 中的2D 圖形支援整合，讓您建立更棒的版面配置 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 和資料視覺效果。</span><span class="sxs-lookup"><span data-stu-id="e49b6-157">WPF provides a set of 3D rendering capabilities that integrate with 2D graphics support in WPF in order for you to create more exciting layout, [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], and data visualization.</span></span> <span data-ttu-id="e49b6-158">在範圍的一端，WPF 可讓您將2D 影像轉譯到3D 圖形的表面，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="e49b6-158">At one end of the spectrum, WPF enables you to render 2D images onto the surfaces of 3D shapes, which the following illustration demonstrates.</span></span>

![顯示具有不同材質之3D 圖形的範例螢幕擷取畫面。](./media/index/visual-three-dimensional-shape.png)

<span data-ttu-id="e49b6-160">如需詳細資訊，請參閱[3D 圖形總覽](3-d-graphics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-160">For more information, see [3D Graphics Overview](3-d-graphics-overview.md).</span></span> <span data-ttu-id="e49b6-161">如需簡介範例，請參閱[3D 純色範例](https://go.microsoft.com/fwlink/?LinkID=159964)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-161">For an introductory sample, see [3D Solids Sample](https://go.microsoft.com/fwlink/?LinkID=159964).</span></span>

<a name="animation"></a>

## <a name="animation"></a><span data-ttu-id="e49b6-162">動畫</span><span class="sxs-lookup"><span data-stu-id="e49b6-162">Animation</span></span>

<span data-ttu-id="e49b6-163">使用動畫讓控制項和元素放大、搖晃、旋轉和淡出，以及建立有趣的網頁切換及執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="e49b6-163">Use animation to make controls and elements grow, shake, spin, and fade; and to create interesting page transitions, and more.</span></span> <span data-ttu-id="e49b6-164">因為 WPF 可讓您以動畫顯示大部分的屬性，您不僅可以建立大部分 WPF 物件的動畫，也可以使用 WPF 以動畫顯示您所建立的自訂物件。</span><span class="sxs-lookup"><span data-stu-id="e49b6-164">Because WPF enables you to animate most properties, not only can you animate most WPF objects, you can also use WPF to animate custom objects that you create.</span></span>

![動畫 cube 的螢幕擷取畫面。](./media/index/animate-custom-objects.png)

<span data-ttu-id="e49b6-166">如需詳細資訊，請參閱[動畫總覽](animation-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-166">For more information, see [Animation Overview](animation-overview.md).</span></span> <span data-ttu-id="e49b6-167">如需簡介範例，請參閱[動畫範例圖庫](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationExamples)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-167">For an introductory sample, see [Animation Example Gallery](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/AnimationExamples).</span></span>

<a name="media"></a>

## <a name="media"></a><span data-ttu-id="e49b6-168">媒體</span><span class="sxs-lookup"><span data-stu-id="e49b6-168">Media</span></span>

<span data-ttu-id="e49b6-169">影像、視訊和音訊都是以媒體功能豐富的方式傳達資訊和使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="e49b6-169">Images, video, and audio are media-rich ways of conveying information and user experiences.</span></span>

### <a name="images"></a><span data-ttu-id="e49b6-170">影像</span><span class="sxs-lookup"><span data-stu-id="e49b6-170">Images</span></span>

<span data-ttu-id="e49b6-171">包括圖示、背景，甚至動畫組件的影像，是大部分應用程式的核心組件。</span><span class="sxs-lookup"><span data-stu-id="e49b6-171">Images, which include icons, backgrounds, and even parts of animations, are a core part of most applications.</span></span> <span data-ttu-id="e49b6-172">因為您經常需要使用影像，所以 WPF 會以各種不同的方式來公開使用它們。</span><span class="sxs-lookup"><span data-stu-id="e49b6-172">Because you frequently need to use images, WPF exposes the ability to work with them in a variety of ways.</span></span> <span data-ttu-id="e49b6-173">下圖顯示眾多方式的其中之一。</span><span class="sxs-lookup"><span data-stu-id="e49b6-173">The following illustration shows just one of those ways.</span></span>

<span data-ttu-id="e49b6-174">![樣式設定範例螢幕擷取畫面](../controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")</span><span class="sxs-lookup"><span data-stu-id="e49b6-174">![Styling sample screenshot](../controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")</span></span>

<span data-ttu-id="e49b6-175">如需詳細資訊，請參閱[影像處理總覽](imaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-175">For more information, see [Imaging Overview](imaging-overview.md).</span></span>

### <a name="video-and-audio"></a><span data-ttu-id="e49b6-176">視訊和音訊</span><span class="sxs-lookup"><span data-stu-id="e49b6-176">Video and Audio</span></span>

<span data-ttu-id="e49b6-177">WPF 圖形功能的核心功能是提供使用多媒體的原生支援，包括影片和音訊。</span><span class="sxs-lookup"><span data-stu-id="e49b6-177">A core feature of the graphics capabilities of WPF is to provide native support for working with multimedia, which includes video and audio.</span></span> <span data-ttu-id="e49b6-178">下列範例示範如何將媒體播放程式插入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49b6-178">The following example shows how to insert a media player into an application.</span></span>

```xaml
<MediaElement Source="media\numbers.wmv" Width="450" Height="250" />
```

<span data-ttu-id="e49b6-179"><xref:System.Windows.Controls.MediaElement>能夠同時播放影片和音訊，而且可以擴充，以允許輕鬆建立自訂 Ui。</span><span class="sxs-lookup"><span data-stu-id="e49b6-179"><xref:System.Windows.Controls.MediaElement> is capable of playing both video and audio, and is extensible enough to allow the easy creation of custom UIs.</span></span>

<span data-ttu-id="e49b6-180">如需詳細資訊，請參閱[多媒體概觀](multimedia-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e49b6-180">For more information, see the [Multimedia Overview](multimedia-overview.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e49b6-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e49b6-181">See also</span></span>

- <xref:System.Windows.Media>
- <xref:System.Windows.Media.Animation>
- <xref:System.Windows.Media.Media3D>
- [<span data-ttu-id="e49b6-182">2D 圖形和影像處理</span><span class="sxs-lookup"><span data-stu-id="e49b6-182">2D Graphics and Imaging</span></span>](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [<span data-ttu-id="e49b6-183">WPF 中圖案和基本繪圖概觀</span><span class="sxs-lookup"><span data-stu-id="e49b6-183">Shapes and Basic Drawing in WPF Overview</span></span>](shapes-and-basic-drawing-in-wpf-overview.md)
- [<span data-ttu-id="e49b6-184">使用純色和漸層繪製的概觀</span><span class="sxs-lookup"><span data-stu-id="e49b6-184">Painting with Solid Colors and Gradients Overview</span></span>](painting-with-solid-colors-and-gradients-overview.md)
- [<span data-ttu-id="e49b6-185">使用影像、繪圖和視覺效果繪製</span><span class="sxs-lookup"><span data-stu-id="e49b6-185">Painting with Images, Drawings, and Visuals</span></span>](painting-with-images-drawings-and-visuals.md)
- [<span data-ttu-id="e49b6-186">動畫和計時 HOW TO 主題</span><span class="sxs-lookup"><span data-stu-id="e49b6-186">Animation and Timing How-to Topics</span></span>](animation-and-timing-how-to-topics.md)
- [<span data-ttu-id="e49b6-187">3D 圖形概觀</span><span class="sxs-lookup"><span data-stu-id="e49b6-187">3D Graphics Overview</span></span>](3-d-graphics-overview.md)
- [<span data-ttu-id="e49b6-188">多媒體概觀</span><span class="sxs-lookup"><span data-stu-id="e49b6-188">Multimedia Overview</span></span>](multimedia-overview.md)

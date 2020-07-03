---
title: 分鏡腳本概觀
desription: Organize and apply animations in storyboards. Use property-targeting syntax and combine timelines in Windows Presentation Foundation (WPF).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboard syntax [WPF]
- syntax [WPF], Storyboard
- timelines [WPF]
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
ms.openlocfilehash: 50f45953da3801bf73016c09b78a6a1b54878bc0
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853638"
---
# <a name="storyboards-overview"></a>分鏡腳本概觀

本主題說明如何使用 <xref:System.Windows.Media.Animation.Storyboard> 物件來組織和套用動畫。 它說明如何以互動方式操作 <xref:System.Windows.Media.Animation.Storyboard> 物件，並描述間接屬性目標語法。

## <a name="prerequisites"></a>必要條件

若要了解本主題，您應該熟悉不同的動畫類型及其基本功能。 如需動畫的簡介，請參閱[動畫概觀](animation-overview.md)。 您也應該了解如何使用附加屬性。 如需附加屬性的詳細資訊，請參閱[附加屬性概觀](../advanced/attached-properties-overview.md)。

<a name="whatisatimeline"></a>

## <a name="what-is-a-storyboard"></a>什麼是分鏡腳本？

動畫不是唯一有用的時間軸型別。 還有其他時間軸類別可以協助您組織時間軸集合，以及將時間軸套用至屬性。 容器時間軸衍生自 <xref:System.Windows.Media.Animation.TimelineGroup> 類別，並包含 <xref:System.Windows.Media.Animation.ParallelTimeline> 和 <xref:System.Windows.Media.Animation.Storyboard> 。

<xref:System.Windows.Media.Animation.Storyboard>是一種容器時間軸，可提供其所包含之時間軸的目標資訊。 分鏡腳本可以包含任何類型 <xref:System.Windows.Media.Animation.Timeline> ，包括其他容器時間軸和動畫。 <xref:System.Windows.Media.Animation.Storyboard>物件可讓您將影響各種物件和屬性的時間軸結合成單一時間軸樹狀結構，以便輕鬆地組織和控制複雜的計時行為。 例如，假設您想讓按鈕執行下列三個動作。

- 在使用者選取按鈕時放大及變更色彩。

- 按一下按鈕時縮小再放大回原本大小。

- 在停用時縮小並淡化到 50% 的不透明度。

在此案例中，您有多組套用至同一個物件的動畫，並且想要視按鈕的狀態在不同時間播放。 <xref:System.Windows.Media.Animation.Storyboard>物件可讓您組織動畫，並將它們以群組形式套用至一或多個物件。

<a name="wherecanyouuseastoryboard"></a>

## <a name="where-can-you-use-a-storyboard"></a>何處可以使用分鏡腳本？

<xref:System.Windows.Media.Animation.Storyboard>可以用來建立 animatable 類別之相依性屬性的動畫（如需如何 animatable 類別的詳細資訊，請參閱[動畫總覽](animation-overview.md)）。 不過，因為分鏡腳本是一種架構層級的功能，所以物件必須屬於 <xref:System.Windows.NameScope> <xref:System.Windows.FrameworkElement> 或的 <xref:System.Windows.FrameworkContentElement> 。

例如，您可以使用 <xref:System.Windows.Media.Animation.Storyboard> 來執行下列動作：

- 建立 <xref:System.Windows.Media.SolidColorBrush> 繪製按鈕背景的（非架構專案）動畫（類型為 <xref:System.Windows.FrameworkElement> ）、

- <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.Media.GeometryDrawing> 使用（）繪製顯示（非架構專案）填滿的（非架構元素）動畫 <xref:System.Windows.Controls.Image> <xref:System.Windows.FrameworkElement> 。

- 在程式碼中， <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.FrameworkElement> 如果 <xref:System.Windows.Media.SolidColorBrush> 已向該類別註冊其名稱，則會以動畫顯示一個也包含的類別所宣告的 <xref:System.Windows.FrameworkElement> 。

但是，您無法使用 <xref:System.Windows.Media.Animation.Storyboard> 來以動畫顯示 <xref:System.Windows.Media.SolidColorBrush> 未向或註冊其名稱的 <xref:System.Windows.FrameworkElement> <xref:System.Windows.FrameworkContentElement> ，或不會用來設定或的屬性 <xref:System.Windows.FrameworkElement> <xref:System.Windows.FrameworkContentElement> 。

<a name="applyanimationswithastoryboard"></a>

## <a name="how-to-apply-animations-with-a-storyboard"></a>如何以分鏡腳本套用動畫

若要使用 <xref:System.Windows.Media.Animation.Storyboard> 來組織和套用動畫，您可以將動畫新增為的子時間軸 <xref:System.Windows.Media.Animation.Storyboard> 。 <xref:System.Windows.Media.Animation.Storyboard>類別會提供 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> 附加屬性。 您可以設定動畫的這些屬性以指定其目標物件和屬性。

若要將動畫套用至其目標，請 <xref:System.Windows.Media.Animation.Storyboard> 使用觸發程式動作或方法開始。 在中 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 具有 <xref:System.Windows.EventTrigger> 、或的物件 <xref:System.Windows.Trigger> <xref:System.Windows.DataTrigger> 。 在程式碼中，您也可以使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。

下表顯示支援每個開始技術的不同位置 <xref:System.Windows.Media.Animation.Storyboard> ：每個實例、樣式、控制項範本和資料範本。 「每個執行個體」指的是將動畫或分鏡腳本直接套用至物件之執行個體，而非樣式、控制項範本或資料範本的技術。

|開始分鏡腳本的方法…|每個執行個體|樣式|控制項範本|資料範本|範例|
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|
|<xref:System.Windows.Media.Animation.BeginStoryboard>和<xref:System.Windows.EventTrigger>|是|是|是|是|[使用分鏡腳本建立屬性的動畫](how-to-animate-a-property-by-using-a-storyboard.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard>和屬性<xref:System.Windows.Trigger>|否|是|是|是|[在屬性值變更時觸發動畫](how-to-trigger-an-animation-when-a-property-value-changes.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard>和<xref:System.Windows.DataTrigger>|否|是|是|是|[操作說明︰在資料變更時觸發動畫](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法|是|否|否|否|[使用分鏡腳本建立屬性的動畫](how-to-animate-a-property-by-using-a-storyboard.md)|

下列範例會使用來建立專案 <xref:System.Windows.Media.Animation.Storyboard> 之的動畫 <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.Shapes.Rectangle> ，以及 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.SolidColorBrush> 用來繪製該專案之的 <xref:System.Windows.Shapes.Rectangle> 。

[!code-xaml[storyboards_ovw_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#1)]

[!code-csharp[storyboards_ovw_snip#100](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]

下列各節會 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 更詳細地描述和附加屬性。

<a name="targetingelementsandfreezables"></a>

## <a name="targeting-framework-elements-framework-content-elements-and-freezables"></a>以架構元素、架構內容元素和 Freezable 為目標

上一節提到，動畫若要尋找其目標，它必須知道目標的名稱和要建立動畫的屬性。 將屬性指定為動畫是直接的：只要 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> 使用要建立動畫的屬性名稱來設定即可。  您可以藉由設定動畫的屬性，指定您想要以動畫顯示其屬性的物件名稱 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 。

<xref:System.Windows.Setter.TargetName%2A>若要讓屬性能夠正常執行，目標物件必須具有名稱。 將名稱指派給 <xref:System.Windows.FrameworkElement> 或，與 <xref:System.Windows.FrameworkContentElement> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 指派物件的名稱不同 <xref:System.Windows.Freezable> 。

架構元素是繼承自類別的類別 <xref:System.Windows.FrameworkElement> 。 架構元素的範例包括 <xref:System.Windows.Window> 、 <xref:System.Windows.Controls.DockPanel> 、 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Shapes.Rectangle> 。 基本上所有的視窗、面板和控制項都是元素。 架構內容元素是繼承自類別的類別 <xref:System.Windows.FrameworkContentElement> 。 架構內容元素的範例包括 <xref:System.Windows.Documents.FlowDocument> 和 <xref:System.Windows.Documents.Paragraph> 。 如果您不確定某個型別是架構元素或架構內容元素，請檢查它是否具有 Name 屬性。 如果有，它可能是架構元素或架構內容元素。 為了安全起見，請檢查其型別頁面的＜繼承階層＞一節。

若要在中啟用 framework 元素或架構內容專案的目標 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以設定其 <xref:System.Windows.FrameworkElement.Name%2A> 屬性。 在程式碼中，您也必須使用 <xref:System.Windows.NameScope.RegisterName%2A> 方法，向已建立的專案註冊元素的名稱 <xref:System.Windows.NameScope> 。

下列範例取自先前的範例，它會指派的名稱 `MyRectangle` a，也就是的型別 <xref:System.Windows.Shapes.Rectangle> <xref:System.Windows.FrameworkElement> 。

[!code-xaml[storyboards_ovw_snip_XAML#2](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#2)]

[!code-csharp[storyboards_ovw_snip#102](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]

在元素具有名稱後，您就可以為該元素的屬性建立動畫。

[!code-xaml[storyboards_ovw_snip_XAML#5](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#5)]

[!code-csharp[storyboards_ovw_snip#105](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]

<xref:System.Windows.Freezable>類型是繼承自類別的類別 <xref:System.Windows.Freezable> 。 的範例 <xref:System.Windows.Freezable> 包括 <xref:System.Windows.Media.SolidColorBrush> 、 <xref:System.Windows.Media.RotateTransform> 和 <xref:System.Windows.Media.GradientStop> 。

若要 <xref:System.Windows.Freezable> 在中啟用動畫的目標 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以使用[x：Name](../../../desktop-wpf/xaml-services/xname-directive.md)指示詞為其指派名稱。 在程式碼中，您可以使用 <xref:System.Windows.NameScope.RegisterName%2A> 方法，向您已建立的元素註冊其名稱 <xref:System.Windows.NameScope> 。

下列範例會將名稱指派給 <xref:System.Windows.Freezable> 物件。

[!code-xaml[storyboards_ovw_snip_XAML#3](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#3)]

[!code-csharp[storyboards_ovw_snip#103](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]

然後物件可以作為動畫的目標。

[!code-xaml[storyboards_ovw_snip_XAML#7](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#7)]

[!code-csharp[storyboards_ovw_snip#107](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]

<xref:System.Windows.Media.Animation.Storyboard>物件會使用名稱範圍來解析 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 屬性。 如需 WPF 名稱範圍的詳細資訊，請參閱 [WPF XAML 名稱範圍](../advanced/wpf-xaml-namescopes.md)。 如果 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 省略屬性，動畫會以其定義所在的專案為目標，或在樣式的案例中，為樣式的元素。

有時無法將名稱指派給 <xref:System.Windows.Freezable> 物件。 例如，如果宣告 <xref:System.Windows.Freezable> 為資源，或用來設定樣式中的屬性值，則不能指定名稱。 因為它沒有名稱，就無法直接做為目標，但可間接做為目標。 以下各節會說明如何使用間接目標。

<a name="pathsyntaxforchangeable"></a>

## <a name="indirect-targeting"></a>間接目標

有時候 <xref:System.Windows.Freezable> 動畫無法直接設定為目標，例如當宣告 <xref:System.Windows.Freezable> 為資源時，或用來設定樣式中的屬性值時。 在這些情況下，即使您無法直接將其設為目標，仍然可以建立物件的動畫 <xref:System.Windows.Freezable> 。 您不需要使用的名稱來設定屬性，而是將「所屬」的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> <xref:System.Windows.Freezable> 元素名稱指定給它 <xref:System.Windows.Freezable> 。 例如， <xref:System.Windows.Media.SolidColorBrush> 用來設定 <xref:System.Windows.Shapes.Shape.Fill%2A> 矩形元素的屬於該矩形的。 若要以動畫顯示筆刷，您可以設定動畫的，其 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 方式是從架構專案或架構內容專案的屬性開始，而這個屬性 <xref:System.Windows.Freezable> 是用來設定，並以 <xref:System.Windows.Freezable> 要建立動畫的屬性結尾。

[!code-xaml[storyboards_ovw_snip_XAML#33](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#33)]

[!code-csharp[storyboards_ovw_snip#134](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]

請注意，如果 <xref:System.Windows.Freezable> 已凍結，則會進行複製，而該複製將會以動畫顯示。 發生這種情況時，原始物件的 <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> 屬性會繼續傳回 `false` ，因為原始物件實際上並不是動畫。 如需複製的詳細資訊，請參閱可[凍結的物件總覽](../advanced/freezable-objects-overview.md)。

另請注意，當使用間接屬性目標時，可能會以不存在的物件作為目標。 例如，您可能假設 <xref:System.Windows.Controls.Control.Background%2A> 特定按鈕的已設定為， <xref:System.Windows.Media.SolidColorBrush> 並嘗試以動畫顯示其色彩，而事實上，是 <xref:System.Windows.Media.LinearGradientBrush> 用來設定按鈕的背景。 在這些情況下，不會擲回例外狀況;動畫無法看見可見效果，因為不 <xref:System.Windows.Media.LinearGradientBrush> 會對屬性的變更做出反應 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 。

以下各節會詳細說明間接屬性目標語法。

<a name="xamlsyntaxchangeableproperty"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-xaml"></a>在 XAML 中以 Freezable 屬性為間接目標

若要以可凍結的屬性為目標 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，請使用下列語法。

| |
|-|
|*ElementPropertyName* `.` *FreezablePropertyName*|

其中

- *ElementPropertyName*是 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Freezable> 用來設定的屬性，而則是

- *FreezablePropertyName*是要建立動畫的的屬性 <xref:System.Windows.Freezable> 。

下列程式碼示範如何以動畫顯示 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.SolidColorBrush> 用來設定 <xref:System.Windows.Shapes.Shape.Fill%2A> 矩形元素之的。

[!code-xaml[storyboards_ovw_snip_XAML#32](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#32)]

有時候您需要以集合或陣列中包含的 Freezable 為目標。

若要以集合中包含的 Freezable 為目標，請使用下列路徑語法。

| |
|-|
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|

其中*CollectionIndex*是物件在其陣列或集合中的索引。

例如，假設某個矩形已將資源套用 <xref:System.Windows.Media.TransformGroup> 至其 <xref:System.Windows.UIElement.RenderTransform%2A> 屬性，而您想要建立其所包含的其中一個轉換的動畫。

[!code-xaml[storyboards_ovw_snip_XAML#34](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#34)]

下列程式碼示範如何以動畫顯示 <xref:System.Windows.Media.RotateTransform.Angle%2A> <xref:System.Windows.Media.RotateTransform> 上一個範例中所示的屬性。

[!code-xaml[storyboards_ovw_snip_XAML#35](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#35)]

<a name="targetingpropertyofchangeableincode"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-code"></a>在程式碼中以 Freezable 的屬性為間接目標

在程式碼中，您會建立 <xref:System.Windows.PropertyPath> 物件。 當您建立時 <xref:System.Windows.PropertyPath> ，您可以指定 <xref:System.Windows.PropertyPath.Path%2A> 和 <xref:System.Windows.PropertyPath.PathParameters%2A> 。

若要建立 <xref:System.Windows.PropertyPath.PathParameters%2A> ，您可以建立類型為的陣列 <xref:System.Windows.DependencyProperty> ，其中包含相依性屬性識別碼欄位的清單。 第一個識別碼欄位適用于的屬性， <xref:System.Windows.FrameworkElement> 或是 <xref:System.Windows.FrameworkContentElement> <xref:System.Windows.Freezable> 用來設定的。 下一個 [識別碼] 欄位代表 <xref:System.Windows.Freezable> 要設為目標的屬性。 將它視為將連接至物件的一環屬性 <xref:System.Windows.Freezable> <xref:System.Windows.FrameworkElement> 。

以下是相依性屬性鏈的範例，其 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.SolidColorBrush> 以用來設定 <xref:System.Windows.Shapes.Shape.Fill%2A> 矩形元素之的為目標。

[!code-csharp[storyboards_ovw_snip#135](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]

您也需要指定 <xref:System.Windows.PropertyPath.Path%2A> 。 <xref:System.Windows.PropertyPath.Path%2A>是 <xref:System.String> ，告訴您 <xref:System.Windows.PropertyPath.Path%2A> 如何解讀它的 <xref:System.Windows.PropertyPath.PathParameters%2A> 。 它會使用下列語法。

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *FreezablePropertyArrayIndex* `)`|

其中

- *OwnerPropertyArrayIndex*是陣列的索引， <xref:System.Windows.DependencyProperty> 其中包含 <xref:System.Windows.FrameworkElement> 用來設定之物件屬性的識別碼 <xref:System.Windows.Freezable> ，以及

- *FreezablePropertyArrayIndex*是陣列的索引 <xref:System.Windows.DependencyProperty> ，其中包含要設為目標之屬性的識別碼。

下列範例 <xref:System.Windows.PropertyPath.Path%2A> 會顯示 <xref:System.Windows.PropertyPath.PathParameters%2A> 先前範例中所定義的。

[!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]

下列範例會結合上述範例中的程式碼，以動畫顯示 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.SolidColorBrush> 用來設定 <xref:System.Windows.Shapes.Shape.Fill%2A> 矩形元素之的。

[!code-csharp[storyboards_ovw_snip#137](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]

有時候您需要以集合或陣列中包含的 Freezable 為目標。 例如，假設某個矩形已將資源套用 <xref:System.Windows.Media.TransformGroup> 至其 <xref:System.Windows.UIElement.RenderTransform%2A> 屬性，而您想要建立其所包含的其中一個轉換的動畫。

[!code-xaml[storyboards_ovw_snip#142](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]

若要將 <xref:System.Windows.Freezable> 包含在集合中的設為目標，您可以使用下列路徑語法。

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *CollectionChildrenPropertyArrayIndex* `)` `[` *CollectionIndex* `].(` *FreezablePropertyArrayIndex* `)`|

其中*CollectionIndex*是物件在其陣列或集合中的索引。

若要以的屬性為目標 <xref:System.Windows.Media.RotateTransform.Angle%2A> <xref:System.Windows.Media.RotateTransform> ，中的第二個轉換 <xref:System.Windows.Media.TransformGroup> ，您可以使用下列 <xref:System.Windows.PropertyPath.Path%2A> 和 <xref:System.Windows.PropertyPath.PathParameters%2A> 。

[!code-csharp[storyboards_ovw_snip#139](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]

下列範例會顯示完整的程式碼，以建立 <xref:System.Windows.Media.RotateTransform.Angle%2A> <xref:System.Windows.Media.RotateTransform> 包含在中之的的動畫 <xref:System.Windows.Media.TransformGroup> 。

[!code-csharp[storyboards_ovw_snip#138](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]

### <a name="indirectly-targeting-with-a-freezable-as-the-starting-point"></a>以 Freezable 作為起點的間接目標

先前的章節說明了如何藉 <xref:System.Windows.Freezable> 由從 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 建立屬性鏈至 <xref:System.Windows.Freezable> 子屬性，間接以為目標。 您也可以使用 <xref:System.Windows.Freezable> 做為起點，並間接以其子屬性的其中一個作為目標 <xref:System.Windows.Freezable> 。 使用做為間接目標的起點時，會有一個額外的限制 <xref:System.Windows.Freezable> ： [啟動] <xref:System.Windows.Freezable> 和 <xref:System.Windows.Freezable> [間接目標] 子屬性之間的每一個都不得凍結。

<a name="controllable_storyboards"></a>

## <a name="interactively-controlling-a-storyboard-in-xaml"></a>在 XAML 中以互動方式控制分鏡腳本

若要在中啟動分鏡腳本 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ，您可以使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 觸發程式動作。 <xref:System.Windows.Media.Animation.BeginStoryboard>將動畫散發至它們所建立動畫的物件和屬性，並啟動分鏡腳本。 （如需此程式的詳細資訊，請參閱[動畫和計時系統總覽](animation-and-timing-system-overview.md)）。如果您藉 <xref:System.Windows.Media.Animation.BeginStoryboard> 由指定其屬性來提供名稱 <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> ，則會將它設為可控制的分鏡腳本。 接著在分鏡腳本啟動後，您就可能以互動方式控制它。 以下是可控制之分鏡腳本動作的清單，您可以將這些動作與事件觸發程序搭配使用以控制分鏡腳本。

- <xref:System.Windows.Media.Animation.PauseStoryboard>：暫停分鏡腳本。

- <xref:System.Windows.Media.Animation.ResumeStoryboard>：繼續已暫停的分鏡腳本。

- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>：變更分鏡腳本的速度。

- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>：將分鏡腳本前進到其填滿期間的結尾（如果有的話）。

- <xref:System.Windows.Media.Animation.StopStoryboard>：停止分鏡腳本。

- <xref:System.Windows.Media.Animation.RemoveStoryboard>：移除分鏡腳本。

在下列範例中，會使用可控制的分鏡腳本動作以互動方式控制分鏡腳本。

[!code-xaml[animation_ovws_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]

<a name="controllable_storyboards_procedural"></a>

## <a name="interactively-controlling-a-storyboard-by-using-code"></a>使用程式碼以互動方式控制分鏡腳本

前述範例顯示如何使用觸發動作顯示動畫。 在程式碼中，您也可以使用類別的互動方法來控制分鏡腳本 <xref:System.Windows.Media.Animation.Storyboard> 。 <xref:System.Windows.Media.Animation.Storyboard>若要在程式碼中使成為互動式，您必須使用分鏡腳本的方法的適當多載， <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 並指定 `true` 讓它成為可控制的。 如需詳細資訊，請參閱<xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29>頁面。

下列清單顯示在啟動之後，可以用來操作的方法 <xref:System.Windows.Media.Animation.Storyboard> ：

- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>

- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>

使用這些方法的優點是您不需要建立 <xref:System.Windows.Trigger> 或 <xref:System.Windows.TriggerAction> 物件; 您只需要參考您想要操作的可控制 <xref:System.Windows.Media.Animation.Storyboard> 。

> [!NOTE]
> 在上採取的所有互動式動作，因此也會在下一次轉譯之前發生的 <xref:System.Windows.Media.Animation.Clock> <xref:System.Windows.Media.Animation.Storyboard> 計時引擎滴答發生。 例如，如果您使用 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 方法跳到動畫中的另一個點，則屬性值不會立即變更，而是值會在計時引擎的下一個刻度上變更。

下列範例顯示如何使用類別的互動方法來套用和控制動畫 <xref:System.Windows.Media.Animation.Storyboard> 。

[!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
[!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]

<a name="usingstoryboardsinstyles"></a>

## <a name="animate-in-a-style"></a>在樣式中建立動畫

您可以使用 <xref:System.Windows.Media.Animation.Storyboard> 物件，在中定義動畫 <xref:System.Windows.Style> 。 <xref:System.Windows.Media.Animation.Storyboard>在中以動畫 <xref:System.Windows.Style> 顯示，類似于在 <xref:System.Windows.Media.Animation.Storyboard> 其他位置使用，但有下列三個例外狀況：

- 您不指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> ; <xref:System.Windows.Media.Animation.Storyboard> 一律以套用的專案為目標 <xref:System.Windows.Style> 。 若要將物件設為目標 <xref:System.Windows.Freezable> ，您必須使用間接目標。 如需間接目標的詳細資訊，請參閱[間接目標](#pathsyntaxforchangeable)一節。

- 您不能 <xref:System.Windows.EventTrigger.SourceName%2A> 為或指定 <xref:System.Windows.EventTrigger> <xref:System.Windows.Trigger> 。

- 您不能使用動態資源參考或資料系結運算式來設定 <xref:System.Windows.Media.Animation.Storyboard> 或動畫屬性值。 這是因為內的所有專案都 <xref:System.Windows.Style> 必須是安全線程，而且計時系統必須將 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 物件設為執行緒安全。 <xref:System.Windows.Media.Animation.Storyboard>如果它或其子時間軸包含動態資源參考或資料系結運算式，則無法凍結。 如需凍結和其他功能的詳細資訊 <xref:System.Windows.Freezable> ，請參閱可[凍結物件的總覽](../advanced/freezable-objects-overview.md)。

- 在中 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您無法宣告 <xref:System.Windows.Media.Animation.Storyboard> 或動畫事件的事件處理常式。

如需示範如何在樣式中定義分鏡腳本的範例，請參閱[在樣式中建立動畫](how-to-animate-in-a-style.md)的範例。

<a name="defineAStoryboardInAControlTemplateSection"></a>

## <a name="animate-in-a-controltemplate"></a>在 ControlTemplate 中建立動畫

您可以使用 <xref:System.Windows.Media.Animation.Storyboard> 物件，在中定義動畫 <xref:System.Windows.Controls.ControlTemplate> 。 <xref:System.Windows.Media.Animation.Storyboard>在中以動畫 <xref:System.Windows.Controls.ControlTemplate> 顯示，類似于在 <xref:System.Windows.Media.Animation.Storyboard> 其他位置使用，但有下列兩個例外狀況：

- <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>只能參考的子物件 <xref:System.Windows.Controls.ControlTemplate> 。 如果 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 未指定，動畫會將目標設為要套用的元素 <xref:System.Windows.Controls.ControlTemplate> 。

- <xref:System.Windows.EventTrigger.SourceName%2A> <xref:System.Windows.EventTrigger> 或的 <xref:System.Windows.Trigger> 僅可參考的子物件 <xref:System.Windows.Controls.ControlTemplate> 。

- 您不能使用動態資源參考或資料系結運算式來設定 <xref:System.Windows.Media.Animation.Storyboard> 或動畫屬性值。 這是因為內的所有專案都 <xref:System.Windows.Controls.ControlTemplate> 必須是安全線程，而且計時系統必須將 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 物件設為執行緒安全。 <xref:System.Windows.Media.Animation.Storyboard>如果它或其子時間軸包含動態資源參考或資料系結運算式，則無法凍結。 如需凍結和其他功能的詳細資訊 <xref:System.Windows.Freezable> ，請參閱可[凍結物件的總覽](../advanced/freezable-objects-overview.md)。

- 在中 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您無法宣告 <xref:System.Windows.Media.Animation.Storyboard> 或動畫事件的事件處理常式。

如需示範如何在中定義分鏡腳本的範例 <xref:System.Windows.Controls.ControlTemplate> ，請參閱[ControlTemplate 範例中的動畫](how-to-animate-in-a-controltemplate.md)。

<a name="animateWhenAPropertyValueChanges"></a>

## <a name="animate-when-a-property-value-changes"></a>在屬性值變更時建立動畫

在樣式和控制項範本中，您可以使用 Trigger 物件在屬性變更時啟動分鏡腳本。 如需範例，請參閱[當屬性值變更時觸發動畫](how-to-trigger-an-animation-when-a-property-value-changes.md)，並[在 ControlTemplate 中建立動畫](how-to-animate-in-a-controltemplate.md)。

屬性物件所套用的動畫， <xref:System.Windows.Trigger> 其行為方式會比 <xref:System.Windows.EventTrigger> 使用方法啟動的動畫或動畫更複雜 <xref:System.Windows.Media.Animation.Storyboard> 。  它們會以其他物件所定義的動畫進行「交付」 <xref:System.Windows.Trigger> ，但會以 <xref:System.Windows.EventTrigger> 和方法觸發動畫來撰寫。

## <a name="see-also"></a>另請參閱

- [動畫概觀](animation-overview.md)
- [屬性動畫技術概觀](property-animation-techniques-overview.md)
- [Freezable 物件概觀](../advanced/freezable-objects-overview.md)

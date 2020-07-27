---
title: 控制項撰寫概觀
description: Windows Presentation Foundation 控制項的擴充性可將建立自訂控制項的需求降到最低。 如有必要，請瞭解如何建立新的控制項。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], authoring overview
- authoring overview for controls [WPF]
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
ms.openlocfilehash: 600eb193613846d7eeeb626a6dfd317d2592f809
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166347"
---
# <a name="control-authoring-overview"></a>控制項撰寫總覽

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 控制項模型由於具有擴充性，因此大幅減少了建立新控制項的需求。 不過，在某些情況下，您可能還是需要建立自訂控制項。 本主題將討論可讓您建立自訂控制項的需求降到最低的一些功能，以及 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的不同控制項撰寫模型。 本主題也將示範如何建立新的控制項。

<a name="when_to_write_a_new_control"></a>

## <a name="alternatives-to-writing-a-new-control"></a>撰寫新控制項的替代方案

在過去，若要從現有控制項自訂控制項，只能變更控制項的標準屬性，例如背景色彩、框線寬度和字型大小。 除了這些預先定義的參數外，若還想擴充控制項的外觀或行為，就需要建立新的控制項，建立的方式通常是繼承現有控制項並覆寫負責繪製控制項。  雖然您現在還是可以使用前述方式，但 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以讓您藉由使用其豐富的內容模型、樣式、範本和觸發程序來自訂現有的控制項。 下列清單提供的範例說明如何在不建立新控制項的情況下，使用這些功能來建立自訂且一致的控制項。

- **豐富內容。** 許多標準的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控制項都支援豐富內容。 例如，的 content 屬性屬於 <xref:System.Windows.Controls.Button> 類型 <xref:System.Object> ，因此理論上任何專案都可以顯示在上 <xref:System.Windows.Controls.Button> 。  若要讓按鈕顯示影像和文字，您可以將影像和加入至， <xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Controls.StackPanel> 並將指派給 <xref:System.Windows.Controls.StackPanel> <xref:System.Windows.Controls.ContentControl.Content%2A> 屬性。 因為控制項可以顯示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 視覺化項目和任意資料，就比較不需要建立新控制項或修改現有控制項來支援複雜的視覺效果。 如需 <xref:System.Windows.Controls.Button> 和中其他內容模型之內容模型的詳細資訊 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ，請參閱[WPF 內容模型](wpf-content-model.md)。

- **式樣.** <xref:System.Windows.Style>是值的集合，代表控制項的屬性。 藉由使用樣式，您可以針對所要的控制項外觀和行為，建立可重複使用的表示方式，而不需要撰寫新的控制項。 例如，假設您想要所有的 <xref:System.Windows.Controls.TextBlock> 控制項都具有紅色的 Arial 字型，字型大小為14。 您可以建立樣式作為資源，並對應地設定適當的屬性。 接著， <xref:System.Windows.Controls.TextBlock> 您新增至應用程式的每個都會有相同的外觀。

- **資料範本。** 可 <xref:System.Windows.DataTemplate> 讓您自訂在控制項上顯示資料的方式。 例如， <xref:System.Windows.DataTemplate> 可以用來指定資料在中的顯示方式 <xref:System.Windows.Controls.ListBox> 。  如需此作業的範例，請參閱[資料範本化概觀](../data/data-templating-overview.md)。  除了自訂資料的外觀之外， <xref:System.Windows.DataTemplate> 也可以包含 UI 元素，讓您在自訂 ui 中有很大的彈性。  例如，藉由使用 <xref:System.Windows.DataTemplate> ，您可以建立， <xref:System.Windows.Controls.ComboBox> 其中每個專案都包含一個核取方塊。

- **控制項範本。** 中的許多控制項都 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用 <xref:System.Windows.Controls.ControlTemplate> 來定義控制項的結構和外觀，將控制項的外觀與控制項的功能隔開。 您可以藉由重新定義控制項的外觀，以大幅變更其外觀 <xref:System.Windows.Controls.ControlTemplate> 。  例如，假設您希望控制項看起來像號誌燈。 這個控制項具有簡單的使用者介面和功能。  控制項是三個圓圈，每次只會亮其中一個。 在某些反映之後，您可能會發現，一 <xref:System.Windows.Controls.RadioButton> 次只會提供一個選取的功能，但的預設面板 <xref:System.Windows.Controls.RadioButton> 看起來不像是在交通燈上的燈光。  由於 <xref:System.Windows.Controls.RadioButton> 會使用控制項範本來定義其外觀，因此很容易就能重新定義 <xref:System.Windows.Controls.ControlTemplate> 以符合控制項的需求，並使用選項按鈕來建立您的停止項。

  > [!NOTE]
  > 雖然 <xref:System.Windows.Controls.RadioButton> 可以使用，但 <xref:System.Windows.DataTemplate> <xref:System.Windows.DataTemplate> 在此範例中並不夠。  會 <xref:System.Windows.DataTemplate> 定義控制項內容的外觀。 如果是 <xref:System.Windows.Controls.RadioButton> ，則內容會顯示在圓形右邊的任何一處，指出是否 <xref:System.Windows.Controls.RadioButton> 已選取。  在號誌燈的範例中，選項按鈕只需要是可以發亮的圓圈。 由於停止指示燈的外觀需求與的預設面板不同 <xref:System.Windows.Controls.RadioButton> ，因此必須重新定義 <xref:System.Windows.Controls.ControlTemplate> 。  一般而言 <xref:System.Windows.DataTemplate> ，會用於定義控制項的內容（或資料），而 <xref:System.Windows.Controls.ControlTemplate> 則用於定義控制項的結構化方式。

- **導致.** 可 <xref:System.Windows.Trigger> 讓您動態變更控制項的外觀和行為，而不需要建立新的控制項。 例如，假設您的 <xref:System.Windows.Controls.ListBox> 應用程式中有多個控制項，而且每個中的專案 <xref:System.Windows.Controls.ListBox> 都要以粗體顯示，而在選取時則為紅色。 您的第一個直覺可能是建立繼承自的類別， <xref:System.Windows.Controls.ListBox> 並覆寫 <xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> 方法以變更所選項目的外觀，但更好的方法是將觸發程式新增至 <xref:System.Windows.Controls.ListBoxItem> 會變更所選項目外觀的樣式。 觸發程序可讓您變更屬性值，或是依據屬性值採取動作。 可 <xref:System.Windows.EventTrigger> 讓您在事件發生時採取動作。

如需樣式、範本和觸發程序的詳細資訊，請參閱[設定樣式和範本](../../../desktop-wpf/fundamentals/styles-templates-overview.md)。

一般而言，若您的控制項可以對應到現有控制項的功能，但您希望控制項看起來不太一樣，則應該先考慮是否能使用本節中所討論的任何方法來變更現有控制項的外觀。

<a name="models_for_control_authoring"></a>

## <a name="models-for-control-authoring"></a>控制項撰寫模型

豐富的內容模型、樣式、範本和觸發程序，可以讓您將建立新控制項的需求降到最低。 然而，若有必要建立新的控制項，最好能先了解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的不同控制項撰寫模型。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供三種建立控制項的常用模型，每種模型都提供不同的功能集和不同程度的彈性。 這三個模型的基類為 <xref:System.Windows.Controls.UserControl> 、 <xref:System.Windows.Controls.Control> 和 <xref:System.Windows.FrameworkElement> 。

### <a name="deriving-from-usercontrol"></a>衍生自 UserControl

若要在中建立控制項，最簡單的方式 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是從衍生 <xref:System.Windows.Controls.UserControl> 。 當您建立繼承自的控制項時 <xref:System.Windows.Controls.UserControl> ，您可以將現有的元件加入 <xref:System.Windows.Controls.UserControl> 、命名元件，以及參考中的事件處理常式 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 。 接著，您可以在程式碼中參考該具名項目，並定義事件處理常式。 這個開發模型與 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中應用程式開發所使用的模型非常類似。

如果正確建立， <xref:System.Windows.Controls.UserControl> 可以利用豐富內容、樣式和觸發程式的優點。 不過，如果您的控制項繼承自 <xref:System.Windows.Controls.UserControl> ，則使用您的控制項的人員將無法使用 <xref:System.Windows.DataTemplate> 或 <xref:System.Windows.Controls.ControlTemplate> 來自訂其外觀。  必須從 <xref:System.Windows.Controls.Control> 類別或它的其中一個衍生類別（而非 <xref:System.Windows.Controls.UserControl> ）衍生，才能建立支援範本的自訂控制項。

#### <a name="benefits-of-deriving-from-usercontrol"></a>從 UserControl 衍生的優點

<xref:System.Windows.Controls.UserControl>如果下列所有情況都適用，請考慮從衍生：

- 您想要以類似建置應用程式的方式來建置控制項。

- 您的控制項只包含現有的元件。

- 您不需要支援複雜的自訂作業。

### <a name="deriving-from-control"></a>衍生自 Control

衍生自 <xref:System.Windows.Controls.Control> 類別是大部分現有控制項所使用的模型 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。 當您建立繼承自類別的控制項時 <xref:System.Windows.Controls.Control> ，您可以使用範本定義其外觀。 這樣做您便可以將作業邏輯與視覺表示方式分開處理。 您也可以使用命令和系結（而不是事件），並盡可能避免參考中的專案，以確保 UI 和邏輯的分離 <xref:System.Windows.Controls.ControlTemplate> 。  如果控制項的 UI 和邏輯已適當地分離，則控制項的使用者可以重新定義控制項的， <xref:System.Windows.Controls.ControlTemplate> 以自訂其外觀。 雖然建立自訂 <xref:System.Windows.Controls.Control> 並不像建立一樣簡單 <xref:System.Windows.Controls.UserControl> ，但自訂會 <xref:System.Windows.Controls.Control> 提供最大的彈性。

#### <a name="benefits-of-deriving-from-control"></a>從 Control 衍生的優點

<xref:System.Windows.Controls.Control> <xref:System.Windows.Controls.UserControl> 如果下列任何一項適用，請考慮從衍生，而不要使用類別：

- 您希望控制項的外觀可透過自訂 <xref:System.Windows.Controls.ControlTemplate> 。

- 您想要控制項支援不同的佈景主題。

### <a name="deriving-from-frameworkelement"></a>衍生自 FrameworkElement

衍生自 <xref:System.Windows.Controls.UserControl> 或 <xref:System.Windows.Controls.Control> 依賴撰寫現有元素的控制項。 在許多情況下，這是可接受的解決方案，因為繼承自的任何物件都 <xref:System.Windows.FrameworkElement> 可以在中 <xref:System.Windows.Controls.ControlTemplate> 。 然而，有時候控制項外觀需要的不僅止於簡單項目組合的功能。 在這些情況下，元件的基礎 <xref:System.Windows.FrameworkElement> 是正確的選擇。

有兩種標準方法可用於建立 <xref:System.Windows.FrameworkElement> 基礎元件：直接轉譯和自訂專案組合。 直接呈現包含覆寫的 <xref:System.Windows.UIElement.OnRender%2A> 方法 <xref:System.Windows.FrameworkElement> ，並提供 <xref:System.Windows.Media.DrawingContext> 明確定義元件視覺效果的作業。 這是和所使用的 <xref:System.Windows.Controls.Image> 方法 <xref:System.Windows.Controls.Border> 。 自訂元素撰寫牽涉到使用類型的物件 <xref:System.Windows.Media.Visual> 來撰寫元件的外觀。 如需範例，請參閱[使用 DrawingVisual 物件](../graphics-multimedia/using-drawingvisual-objects.md)。 <xref:System.Windows.Controls.Primitives.Track>是中 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ，使用自訂專案組合的控制項範例。 您也可以在同一個控制項中混合使用直接轉譯和自訂項目組合。

#### <a name="benefits-of-deriving-from-frameworkelement"></a>從 FrameworkElement 衍生的優點

<xref:System.Windows.FrameworkElement>如果下列任何一項適用，請考慮從衍生：

- 您想要精確控制控制項的外觀，而這超出了簡單項目組合所能提供的控制。

- 您想要藉由定義自己的轉譯邏輯，來定義控制項的外觀。

- 您想要以 novel 的方式撰寫現有的專案，而不會超過和的可能功能 <xref:System.Windows.Controls.UserControl> <xref:System.Windows.Controls.Control> 。

<a name="control_authoring_basics"></a>

## <a name="control-authoring-basics"></a>控制項撰寫基本概念

如稍早所討論，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 其中一個最強大的功能，在於除了設定控制項的基本屬性之外，尚有能力變更其外觀和行為，並且不需要建立自訂控制項。 樣式、資料繫結和觸發程序功能是透過 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 屬性系統和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系統來達成的。 下列各節說明您應該遵循的一些做法，而不論您是使用哪種模型來建立自訂控制項，讓自訂控制項的使用者能夠使用這些功能，就如同使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 隨附的控制項一樣。

### <a name="use-dependency-properties"></a>使用相依性屬性

當屬性是相依性屬性時，有可能會進行下列作業：

- 設定樣式中的屬性。

- 將屬性繫結至資料來源。

- 使用動態資源作為屬性值。

- 顯示屬性的動畫。

若希望控制項屬性可以支援這些任一功能，就應該將控制項實作為相依性屬性。 下列範例會藉由執行下列動作，定義名為 `Value` 的相依性屬性：

- 定義 <xref:System.Windows.DependencyProperty> 名 `ValueProperty` 為的識別碼做為 `public` `static` `readonly` 欄位。

- 呼叫以向屬性系統註冊屬性名稱， <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=nameWithType> 以指定下列各項：

  - 屬性的名稱。

  - 屬性的類型。

  - 擁有屬性的類型。

  - 屬性的中繼資料。 中繼資料包含屬性的預設值： <xref:System.Windows.CoerceValueCallback> 和 <xref:System.Windows.PropertyChangedCallback> 。

- 定義名為的 CLR 包裝函式屬性 `Value` ，這是用來註冊相依性屬性的相同名稱，方法是執行屬性的 `get` 和 `set` 存取子。 請注意， `get` 和 `set` 存取子只 <xref:System.Windows.DependencyObject.GetValue%2A> 會 <xref:System.Windows.DependencyObject.SetValue%2A> 分別呼叫和。 由於用戶端和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以略過存取子並直接呼叫和，因此建議相依性屬性的存取子不包含其他邏輯 <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A> 。 例如，在屬性繫結到資料來源時，就不會呼叫屬性的 `set` 存取子。  不需要將其他邏輯新增至 get 和 set 存取子，而是使用 <xref:System.Windows.ValidateValueCallback> 、 <xref:System.Windows.CoerceValueCallback> 和 <xref:System.Windows.PropertyChangedCallback> 委派來回應，或在變更時檢查值。  如需這些回呼的詳細資訊，請參閱[相依性屬性回呼和驗證](../advanced/dependency-property-callbacks-and-validation.md)。

- 定義名為的方法 <xref:System.Windows.CoerceValueCallback> `CoerceValue` 。 `CoerceValue` 可以確保 `Value` 大於或等於 `MinValue`，且小於或等於 `MaxValue`。

- 定義名為的方法 <xref:System.Windows.PropertyChangedCallback> `OnValueChanged` 。 `OnValueChanged`建立 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 物件並準備引發 `ValueChanged` 路由事件。 下一節中將討論路由事件。

[!code-csharp[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
[!code-vb[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]

如需詳細資訊，請參閱[自訂相依性屬性](../advanced/custom-dependency-properties.md)。

### <a name="use-routed-events"></a>使用路由事件

就像相依性屬性擴充 CLR 屬性的概念和其他功能一樣，路由事件也會擴充標準 CLR 事件的概念。 建立新的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控制項時，最好也能將事件實作為路由事件，因為路由事件支援下列行為：

- 事件可以對多個控制項的父項進行處理。 若事件是反昇事件，項目樹狀結構中的單一父項可以訂閱事件。 然後應用程式作者可以使用一個處理常式，以回應多個控制項的事件。 例如，如果您的控制項是中每個專案的一部分 <xref:System.Windows.Controls.ListBox> （因為它包含在中 <xref:System.Windows.DataTemplate> ），應用程式開發人員可以在上定義控制項事件的事件處理常式 <xref:System.Windows.Controls.ListBox> 。 每當任一控制項上發生事件時，就會呼叫事件處理常式。

- 路由事件可以在中使用 <xref:System.Windows.EventSetter> ，讓應用程式開發人員在樣式內指定事件的處理常式。

- 路由事件可以在中使用 <xref:System.Windows.EventTrigger> ，這對於使用來製作屬性的動畫很 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 有用。 如需詳細資訊，請參閱[動畫總覽](../graphics-multimedia/animation-overview.md)。

下列範例會藉由執行下列動作，定義路由事件：

- 定義 <xref:System.Windows.RoutedEvent> 名 `ValueChangedEvent` 為的識別碼做為 `public` `static` `readonly` 欄位。

- 藉由呼叫方法來註冊路由事件 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=nameWithType> 。 此範例會在呼叫時指定下列資訊 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> ：

  - 事件名稱是 `ValueChanged`。

  - 路由策略是 <xref:System.Windows.RoutingStrategy.Bubble> ，這表示會先呼叫來源（引發事件的物件）上的事件處理常式，然後再連續呼叫來源的父元素上的事件處理常式，從最接近的父元素上的事件處理常式開始。

  - 事件處理常式的型別是 <xref:System.Windows.RoutedPropertyChangedEventHandler%601> ，使用型別來建造 <xref:System.Decimal> 。

  - 事件的擁有者類型是 `NumericUpDown`。

- 宣告名為 `ValueChanged` 的公用事件，並包含事件存取子宣告。 範例會呼叫存取子宣告和存取子宣告中的 <xref:System.Windows.UIElement.AddHandler%2A> `add` <xref:System.Windows.UIElement.RemoveHandler%2A> `remove` 來使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件服務。

- 建立名為 `OnValueChanged` 的受保護虛擬方法，該方法會引發 `ValueChanged` 事件。

[!code-csharp[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
[!code-vb[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]

如需詳細資訊，請參閱[路由事件概觀](../advanced/routed-events-overview.md)和[建立自訂路由事件](../advanced/how-to-create-a-custom-routed-event.md)。

### <a name="use-binding"></a>使用繫結

若要降低控制項 UI 和邏輯間的耦合，請考慮使用資料繫結。 如果您使用來定義控制項的外觀，這就特別重要 <xref:System.Windows.Controls.ControlTemplate> 。 在您使用資料繫結時，也許可以排除從程式碼參考特定部分之 UI 的需要。 避免參考中的專案是個不錯的主意 <xref:System.Windows.Controls.ControlTemplate> ，因為當程式碼參考中的專案， <xref:System.Windows.Controls.ControlTemplate> 而且 <xref:System.Windows.Controls.ControlTemplate> 變更時，所參考的元素必須包含在新的中 <xref:System.Windows.Controls.ControlTemplate> 。

下列範例 <xref:System.Windows.Controls.TextBlock> `NumericUpDown` 會更新控制項的，並在程式碼中為其指派名稱，並依名稱參考 textbox。

[!code-xaml[UserControlNumericUpDownSimple#UIRefMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]

[!code-csharp[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
[!code-vb[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]

下列範例使用繫結達成相同目的。

[!code-xaml[UserControlNumericUpDown#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]

如需資料繫結的詳細資訊，請參閱[資料繫結概觀](../../../desktop-wpf/data/data-binding-overview.md)。

### <a name="design-for-designers"></a>設計工具的設計

若要在 Visual Studio 的 WPF 設計工具中接收自訂 WPF 控制項的支援（例如，使用屬性視窗編輯屬性），請遵循這些指導方針。  如需 WPF 設計工具開發的詳細資訊，請參閱[在 Visual Studio 中設計 XAML](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)。

#### <a name="dependency-properties"></a>相依性屬性

請務必依照先前「 `get` 使用相依性 `set` 屬性」中所述的方式來執行 CLR 和存取子。 設計工具可以使用包裝函式來偵測相依性屬性的存在，但就跟 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和控制項用戶端一樣，設計工具在取得或設定屬性時不一定要呼叫存取子。

#### <a name="attached-properties"></a>附加屬性

請使用下列方針，實作自訂控制項上的附加屬性：

- 具有 `public` `static` `readonly` <xref:System.Windows.DependencyProperty> 使用方法建立之表單*PropertyName*的 `Property` <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 。 傳遞至的屬性名稱 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 必須符合*PropertyName*。

- 實作一組 `public` `static` CLR 方法，分別名為 `Set`<屬性名稱>** 和 `Get`<屬性名稱>**。 這兩種方法都應該接受衍生自的類別 <xref:System.Windows.DependencyProperty> 做為其第一個引數。 `Set`*PropertyName* 方法也接受其型別與屬性之已註冊資料型別相符的引數。 <屬性名稱>`Get`** 方法應傳回相同類型的值。 若遺漏 <屬性名稱>`Set`** 方法，屬性就會標示為唯讀。

- `Set`*Propertyname*和 `Get` *propertyname*必須 <xref:System.Windows.DependencyObject.GetValue%2A> 分別在目標相依性物件上直接路由至和 <xref:System.Windows.DependencyObject.SetValue%2A> 方法。 藉由呼叫方法包裝函式，或直接呼叫目標相依性物件，設計工具可以存取附加屬性。

如需附加屬性的詳細資訊，請參閱[附加屬性概觀](../advanced/attached-properties-overview.md)。

### <a name="define-and-use-shared-resources"></a>定義和使用共用資源

您可以將控制項納入與應用程式相同的組件，或者將控制項封裝在不同的組件中，以用於多個應用程式。 在大多數情況下，不論使用的方法為何，本主題所討論的資訊都適用。  不過，有一項差異值得注意。  當您將控制項放入與應用程式相同的組件中時，可以任意將全域資源新增至 App.xaml 檔案。 但僅包含控制項的元件並沒有 <xref:System.Windows.Application> 相關聯的物件，因此無法使用 app.xaml 檔案。

當應用程式尋找資源時，會以下列順序在三個層級中尋找：

1. 項目層級。

   系統會從參考資源的項目開始，然後搜尋邏輯父項的資源，以此類推，直到達到根項目為止。

2. 應用程式層級。

   物件所定義的資源 <xref:System.Windows.Application> 。

3. 佈景主題層級。

   佈景主題層級字典會儲存在名為 Themes 的子資料夾。  Themes 資料夾中的檔案會與佈景主題對應。  例如，您可能有 Aero.NormalColor.xaml、Luna.NormalColor.xaml、Royale.NormalColor.xaml 等等。  您也可以有名為 generic.xaml 的檔案。  當系統在佈景主題層級尋找資源時，會先在佈景主題特定檔案中尋找資源，再到 generic.xaml 中尋找資源。

當您的控制項位於與應用程式不同的組件中時，必須將全域資源置於項目層級或佈景主題層級。 這兩種方法各有其優點。

#### <a name="defining-resources-at-the-element-level"></a>在項目層級定義資源

您可以藉由建立自訂資源字典並將它與控制項的資源字典合併，在專案層級定義共用資源。  當您使用這個方法時，可以隨意命名資源檔，而且資源檔可以與控制項位於相同的資料夾中。 項目層級的資源也可以使用簡單的字串作為索引鍵。 下列範例會建立 <xref:System.Windows.Media.LinearGradientBrush> 名為 Dictionary1 的資源檔。

[!code-xaml[SharedResources#1](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]

定義字典之後，您需要將它與控制項的資源字典合併。  您可以使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或程式碼完成這項動作。

下列範例會使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 合併資源字典。

[!code-xaml[SharedResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]

這種方法的缺點是 <xref:System.Windows.ResourceDictionary> 每次參考物件時，都會建立一個物件。  例如，如果您的程式庫中有10個自訂控制項，並使用 XAML 合併每個控制項的共用資源字典，您就會建立10個完全相同的 <xref:System.Windows.ResourceDictionary> 物件。  您可以建立一個靜態類別來合併程式碼中的資源，並傳回產生的，藉此避免這種情況 <xref:System.Windows.ResourceDictionary> 。

下列範例會建立會傳回共用的類別 <xref:System.Windows.ResourceDictionary> 。

[!code-csharp[SharedResources#3](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]

下列範例會在呼叫 `InitializeComponent` 之前，在自訂控制項的建構函式中將共用資源與該控制項的資源合併。  因為 `SharedDictionaryManager.SharedDictionary` 是靜態屬性，所以 <xref:System.Windows.ResourceDictionary> 只會建立一次。 由於資源字典是在呼叫 `InitializeComponent` 之前合併，因此控制項可在其 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 檔案中使用資源。

[!code-csharp[SharedResources#4](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]

#### <a name="defining-resources-at-the-theme-level"></a>在佈景主題層級定義資源

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可讓您為不同的 Windows 佈景主題建立資源。  身為控制項作者，您可以為特定佈景主題定義資源，以根據使用的佈景主題變更控制項的外觀。 例如， <xref:System.Windows.Controls.Button> Windows 傳統主題中的外觀（windows 2000 的預設主題）與 <xref:System.Windows.Controls.Button> windows Luna 主題（windows XP 的預設主題）中的不同，因為 <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.ControlTemplate> 每個主題都使用不同的。

某個佈景主題專屬的資源會存放在具有特定檔名的資源字典中。 這些檔案必須位於名為 `Themes` 的資料夾中，這是包含控制項之資料夾的子資料夾。 下表列出資源字典檔以及與每個檔案相關聯的佈景主題：

|資源字典檔名稱|Windows 佈景主題|
|-----------------------------------|-------------------|
|`Classic.xaml`|Windows XP 上的傳統 Windows 9x/2000 外觀|
|`Luna.NormalColor.xaml`|Windows XP 上的預設藍色佈景主題|
|`Luna.Homestead.xaml`|Windows XP 上的橄欖色佈景主題|
|`Luna.Metallic.xaml`|Windows XP 上的銀色佈景主題|
|`Royale.NormalColor.xaml`|Windows XP Media Center Edition 上的預設佈景主題|
|`Aero.NormalColor.xaml`|Windows Vista 上的預設佈景主題|

您不需要為每個佈景主題定義資源。 若未定義特定佈景主題的資源，則控制項會在 `Classic.xaml` 中檢查資源。 若在對應於目前佈景主題的檔案中或在 `Classic.xaml` 中都未定義資源，控制項會使用名為 `generic.xaml` 的資源字典檔中的一般資源。  `generic.xaml` 檔案位於與佈景主題特有資源字典檔相同的資料夾中。 雖然 `generic.xaml` 並未對應到特定 Windows 佈景主題，但它仍是佈景主題層級字典。

[C #](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp)或[Visual Basic](https://github.com/dotnet/docs/tree/master/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) NumericUpDown 自訂控制項與主題和 UI 自動化支援範例包含兩個控制項的資源字典 `NumericUpDown` ：一個是在 generic. xaml 中，另一個則位於 Luna. aero.normalcolor.xaml. xaml 中。

當您將放 <xref:System.Windows.Controls.ControlTemplate> 在任何主題特定的資源字典檔案中時，您必須為控制項建立靜態的函式，並 <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> 在上呼叫方法 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> ，如下列範例所示。

[!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
[!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]

##### <a name="defining-and-referencing-keys-for-theme-resources"></a>定義和參考佈景主題資源的索引鍵

當您在項目層級定義資源時，可以指派字串作為它的索引鍵，然後透過字串存取資源。 當您在主題層級定義資源時，您必須使用 <xref:System.Windows.ComponentResourceKey> 做為索引鍵。  下列範例會在 generic.xaml 中定義資源。

[!code-xaml[ThemeResourcesControlLibrary#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/Themes/generic.xaml#5)]

下列範例會藉由指定做為索引鍵來參考資源 <xref:System.Windows.ComponentResourceKey> 。

[!code-xaml[ThemeResourcesControlLibrary#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/NumericUpDown.xaml#6)]

##### <a name="specifying-the-location-of-theme-resources"></a>指定佈景主題資源的位置

若要尋找控制項的資源，裝載的應用程式必須知道組件是否包含控制項特定的資源。 您可以藉由將加入 <xref:System.Windows.ThemeInfoAttribute> 至包含控制項的元件來完成這項工作。 <xref:System.Windows.ThemeInfoAttribute>具有 <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 指定一般資源位置的屬性，以及 <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 指定主題特定資源位置的屬性。

下列範例 <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 會將和 <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 屬性設定為 <xref:System.Windows.ResourceDictionaryLocation.SourceAssembly> ，以指定泛型和主題特定的資源在與控制項相同的元件中。

[!code-csharp[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
[!code-vb[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]

## <a name="see-also"></a>另請參閱

- [在 Visual Studio 中設計 XAML](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [WPF 中的 Pack URI](../app-development/pack-uris-in-wpf.md)
- [控制項自訂](control-customization.md)

---
title: 繫結宣告概觀
description: 瞭解如何在 XAML 中宣告系結，以在 Windows Presentation Foundation （WPF）中開發應用程式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- markup extensions [WPF]
- data binding [WPF], declarations
- object element syntax [WPF]
- binding data [WPF], declarations
- syntax [WPF], object elements
- binding declarations [WPF]
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
ms.openlocfilehash: 8d4943de0cacb5fe0b5a0c37a5a68f15243ad528
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619633"
---
# <a name="binding-declarations-overview"></a><span data-ttu-id="530c3-103">繫結宣告概觀</span><span class="sxs-lookup"><span data-stu-id="530c3-103">Binding Declarations Overview</span></span>

<span data-ttu-id="530c3-104">本主題討論可以用來宣告繫結的不同方法。</span><span class="sxs-lookup"><span data-stu-id="530c3-104">This topic discusses the different ways you can declare a binding.</span></span>

<a name="Prereq"></a>

## <a name="prerequisites"></a><span data-ttu-id="530c3-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="530c3-105">Prerequisites</span></span>

<span data-ttu-id="530c3-106">在閱讀本主題之前，請務必先熟悉標記延伸的概念和使用方式。</span><span class="sxs-lookup"><span data-stu-id="530c3-106">Before reading this topic, it is important that you are familiar with the concept and usage of markup extensions.</span></span> <span data-ttu-id="530c3-107">如需標記延伸的詳細資訊，請參閱[標記延伸和 WPF XAML](../advanced/markup-extensions-and-wpf-xaml.md)。</span><span class="sxs-lookup"><span data-stu-id="530c3-107">For more information about markup extensions, see [Markup Extensions and WPF XAML](../advanced/markup-extensions-and-wpf-xaml.md).</span></span>

<span data-ttu-id="530c3-108">這個主題並未涵蓋資料繫結的概念。</span><span class="sxs-lookup"><span data-stu-id="530c3-108">This topic does not cover data binding concepts.</span></span> <span data-ttu-id="530c3-109">如需資料繫結概念的相關討論，請參閱[資料繫結概觀](../../../desktop-wpf/data/data-binding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="530c3-109">For a discussion of data binding concepts, see [Data Binding Overview](../../../desktop-wpf/data/data-binding-overview.md).</span></span>

<a name="BindinginXAML"></a>

## <a name="declaring-a-binding-in-xaml"></a><span data-ttu-id="530c3-110">在 XAML 中宣告繫結</span><span class="sxs-lookup"><span data-stu-id="530c3-110">Declaring a Binding in XAML</span></span>

<span data-ttu-id="530c3-111">本節討論如何在 XAML 中宣告繫結。</span><span class="sxs-lookup"><span data-stu-id="530c3-111">This section discusses how to declare a binding in XAML.</span></span>

<a name="MarkupExtensionSyntax"></a>

### <a name="markup-extension-usage"></a><span data-ttu-id="530c3-112">標記延伸使用方式</span><span class="sxs-lookup"><span data-stu-id="530c3-112">Markup Extension Usage</span></span>

<span data-ttu-id="530c3-113"><xref:System.Windows.Data.Binding> 是一種標記延伸。</span><span class="sxs-lookup"><span data-stu-id="530c3-113"><xref:System.Windows.Data.Binding> is a markup extension.</span></span> <span data-ttu-id="530c3-114">當您使用繫結延伸宣告繫結時，該宣告是由一系列子句組成，這些子句接在 `Binding` 關鍵字後面，並以逗號 (,) 分隔。</span><span class="sxs-lookup"><span data-stu-id="530c3-114">When you use the binding extension to declare a binding, the declaration consists of a series of clauses following the `Binding` keyword and separated by commas (,).</span></span> <span data-ttu-id="530c3-115">繫結宣告中的子句可以按照任何順序，而且有許多可能的組合。</span><span class="sxs-lookup"><span data-stu-id="530c3-115">The clauses in the binding declaration can be in any order and there are many possible combinations.</span></span> <span data-ttu-id="530c3-116">子句是*名稱* = *值*組，其中*name*是屬性的名稱 <xref:System.Windows.Data.Binding> ，而*值*則是您要為屬性設定的值。</span><span class="sxs-lookup"><span data-stu-id="530c3-116">The clauses are *Name*=*Value* pairs where *Name* is the name of the <xref:System.Windows.Data.Binding> property and *Value* is the value you are setting for the property.</span></span>

<span data-ttu-id="530c3-117">在標記中建立繫結宣告字串時，必須將這些字串附加至目標物件的特定相依性屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-117">When creating binding declaration strings in markup, they must be attached to the specific dependency property of a target object.</span></span> <span data-ttu-id="530c3-118">下列範例顯示如何使用系結延伸模組來系結 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 屬性，並指定 <xref:System.Windows.Data.Binding.Source%2A> 和 <xref:System.Windows.Data.Binding.Path%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-118">The following example shows how to bind the <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> property using the binding extension, specifying the <xref:System.Windows.Data.Binding.Source%2A> and <xref:System.Windows.Data.Binding.Path%2A> properties.</span></span>

[!code-xaml[SimpleBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#L37-L37)]

<span data-ttu-id="530c3-119">您可以用 <xref:System.Windows.Data.Binding> 這種方式指定類別的大部分屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-119">You can specify most of the properties of the <xref:System.Windows.Data.Binding> class this way.</span></span> <span data-ttu-id="530c3-120">如需系結延伸模組以及無法使用系結延伸模組設定之屬性清單的詳細資訊 <xref:System.Windows.Data.Binding> ，請參閱系結[標記延伸](../advanced/binding-markup-extension.md)的總覽。</span><span class="sxs-lookup"><span data-stu-id="530c3-120">For more information about the binding extension as well as for a list of <xref:System.Windows.Data.Binding> properties that cannot be set using the binding extension, see the [Binding Markup Extension](../advanced/binding-markup-extension.md) overview.</span></span>

<a name="ObjectElementSyntax"></a>

### <a name="object-element-syntax"></a><span data-ttu-id="530c3-121">物件元素語法</span><span class="sxs-lookup"><span data-stu-id="530c3-121">Object Element Syntax</span></span>

<span data-ttu-id="530c3-122">物件元素語法是建立繫結宣告的另一種選擇。</span><span class="sxs-lookup"><span data-stu-id="530c3-122">Object element syntax is an alternative to creating the binding declaration.</span></span> <span data-ttu-id="530c3-123">在大部分的情況下，使用標記延伸或物件元素語法並沒有特別的優勢。</span><span class="sxs-lookup"><span data-stu-id="530c3-123">In most cases, there is no particular advantage to using either the markup extension or the object element syntax.</span></span> <span data-ttu-id="530c3-124">但是，若標記延伸無法支援您的案例，例如當屬性值屬於非字串型別，而沒有型別轉換時，則必須使用物件元素語法。</span><span class="sxs-lookup"><span data-stu-id="530c3-124">However, in cases which the markup extension does not support your scenario, such as when your property value is of a non-string type for which no type conversion exists, you need to use the object element syntax.</span></span>

<span data-ttu-id="530c3-125">以下為物件元素語法和標記延伸的使用方式範例：</span><span class="sxs-lookup"><span data-stu-id="530c3-125">The following is an example of both the object element syntax and the markup extension usage:</span></span>

[!code-xaml[BindConversionMarkup#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]

<span data-ttu-id="530c3-126">此範例會使用延伸模組語法宣告系結來系結 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-126">The example binds the <xref:System.Windows.Controls.TextBlock.Foreground%2A> property by declaring a binding using the extension syntax.</span></span> <span data-ttu-id="530c3-127">屬性的系結宣告會 <xref:System.Windows.Controls.TextBlock.Text%2A> 使用物件元素語法。</span><span class="sxs-lookup"><span data-stu-id="530c3-127">The binding declaration for the <xref:System.Windows.Controls.TextBlock.Text%2A> property uses the object element syntax.</span></span>

<span data-ttu-id="530c3-128">如需不同詞彙的詳細資訊，請參閱 [XAML 語法詳細資料](../advanced/xaml-syntax-in-detail.md)。</span><span class="sxs-lookup"><span data-stu-id="530c3-128">For more information about the different terms, see [XAML Syntax In Detail](../advanced/xaml-syntax-in-detail.md).</span></span>

<a name="MBandPB"></a>

### <a name="multibinding-and-prioritybinding"></a><span data-ttu-id="530c3-129">MultiBinding 和 PriorityBinding</span><span class="sxs-lookup"><span data-stu-id="530c3-129">MultiBinding and PriorityBinding</span></span>

<span data-ttu-id="530c3-130"><xref:System.Windows.Data.MultiBinding>和不 <xref:System.Windows.Data.PriorityBinding> 支援 XAML 延伸模組語法。</span><span class="sxs-lookup"><span data-stu-id="530c3-130"><xref:System.Windows.Data.MultiBinding> and <xref:System.Windows.Data.PriorityBinding> do not support the XAML extension syntax.</span></span> <span data-ttu-id="530c3-131">因此，如果您要 <xref:System.Windows.Data.MultiBinding> 在 XAML 中宣告或，則必須使用物件元素語法 <xref:System.Windows.Data.PriorityBinding> 。</span><span class="sxs-lookup"><span data-stu-id="530c3-131">Therefore, you must use the object element syntax if you are declaring a <xref:System.Windows.Data.MultiBinding> or a <xref:System.Windows.Data.PriorityBinding> in XAML.</span></span>

<a name="BindinginCode"></a>

## <a name="creating-a-binding-in-code"></a><span data-ttu-id="530c3-132">在程式碼中建立繫結</span><span class="sxs-lookup"><span data-stu-id="530c3-132">Creating a Binding in Code</span></span>

<span data-ttu-id="530c3-133">另一個指定系結的方式是直接在程式碼中的物件上設定屬性 <xref:System.Windows.Data.Binding> 。</span><span class="sxs-lookup"><span data-stu-id="530c3-133">Another way to specify a binding is to set properties directly on a <xref:System.Windows.Data.Binding> object in code.</span></span> <span data-ttu-id="530c3-134">下列範例顯示如何建立 <xref:System.Windows.Data.Binding> 物件，並在程式碼中指定屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-134">The following example shows how to create a <xref:System.Windows.Data.Binding> object and specify the properties in code.</span></span>  <span data-ttu-id="530c3-135">在此範例中， `TheConverter` 是用來執行介面的物件 <xref:System.Windows.Data.IValueConverter> 。</span><span class="sxs-lookup"><span data-stu-id="530c3-135">In this example, `TheConverter` is an object that implements the <xref:System.Windows.Data.IValueConverter> interface.</span></span>

[!code-csharp[BindConversion#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
[!code-vb[BindConversion#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]

<span data-ttu-id="530c3-136">如果您要系結的物件是 <xref:System.Windows.FrameworkElement> 或， <xref:System.Windows.FrameworkContentElement> 您可以 `SetBinding` 直接在物件上呼叫方法，而不是使用 <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="530c3-136">If the object you are binding is a <xref:System.Windows.FrameworkElement> or a <xref:System.Windows.FrameworkContentElement> you can call the `SetBinding` method on your object directly instead of using <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="530c3-137">如需範例，請參閱[使用程式碼建立繫結](how-to-create-a-binding-in-code.md)。</span><span class="sxs-lookup"><span data-stu-id="530c3-137">For an example, see [Create a Binding in Code](how-to-create-a-binding-in-code.md).</span></span>

<a name="Path_Syntax"></a>

## <a name="binding-path-syntax"></a><span data-ttu-id="530c3-138">繫結路徑語法</span><span class="sxs-lookup"><span data-stu-id="530c3-138">Binding Path Syntax</span></span>

<span data-ttu-id="530c3-139">使用 <xref:System.Windows.Data.Binding.Path%2A> 屬性來指定您想要系結的來源值：</span><span class="sxs-lookup"><span data-stu-id="530c3-139">Use the <xref:System.Windows.Data.Binding.Path%2A> property to specify the source value you want to bind to:</span></span>

- <span data-ttu-id="530c3-140">在最簡單的情況下， <xref:System.Windows.Data.Binding.Path%2A> 屬性值就是要用於系結之來源物件的屬性名稱，例如 `Path=PropertyName` 。</span><span class="sxs-lookup"><span data-stu-id="530c3-140">In the simplest case, the <xref:System.Windows.Data.Binding.Path%2A> property value is the name of the property of the source object to use for the binding, such as `Path=PropertyName`.</span></span>

- <span data-ttu-id="530c3-141">屬性的子屬性可以透過與 c # 中類似的語法來指定。</span><span class="sxs-lookup"><span data-stu-id="530c3-141">Subproperties of a property can be specified by a similar syntax as in C#.</span></span> <span data-ttu-id="530c3-142">例如，子句 `Path=ShoppingCart.Order` 會將繫結設定為物件或屬性 `ShoppingCart` 的子屬性 `Order`。</span><span class="sxs-lookup"><span data-stu-id="530c3-142">For instance, the clause `Path=ShoppingCart.Order` sets the binding to the subproperty `Order` of the object or property `ShoppingCart`.</span></span>

- <span data-ttu-id="530c3-143">若要繫結至附加屬性，請在附加屬性前後加上括號。</span><span class="sxs-lookup"><span data-stu-id="530c3-143">To bind to an attached property, place parentheses around the attached property.</span></span> <span data-ttu-id="530c3-144">例如，若要系結至附加屬性 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> ，語法為 `Path=(DockPanel.Dock)` 。</span><span class="sxs-lookup"><span data-stu-id="530c3-144">For example, to bind to the attached property <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>, the syntax is `Path=(DockPanel.Dock)`.</span></span>

- <span data-ttu-id="530c3-145">屬性的索引子可以在方括弧內指定，接在套用索引子的屬性名稱後面。</span><span class="sxs-lookup"><span data-stu-id="530c3-145">Indexers of a property can be specified within square brackets following the property name where the indexer is applied.</span></span> <span data-ttu-id="530c3-146">例如，子句 `Path=ShoppingCart[0]` 會將繫結設定為索引，而該索引對應於屬性之內部索引處理常值字串 "0" 的方式。</span><span class="sxs-lookup"><span data-stu-id="530c3-146">For instance, the clause `Path=ShoppingCart[0]` sets the binding to the index that corresponds to how your property's internal indexing handles the literal string "0".</span></span> <span data-ttu-id="530c3-147">此語法也支援巢狀索引子。</span><span class="sxs-lookup"><span data-stu-id="530c3-147">Nested indexers are also supported.</span></span>

- <span data-ttu-id="530c3-148">`Path` 子句中可以混合使用索引子和子屬性；例如，`Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`</span><span class="sxs-lookup"><span data-stu-id="530c3-148">Indexers and subproperties can be mixed in a `Path` clause; for example, `Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`</span></span>

- <span data-ttu-id="530c3-149">您可以在索引子內加入多個以逗號 (,) 分隔的索引子參數。</span><span class="sxs-lookup"><span data-stu-id="530c3-149">Inside indexers you can have multiple indexer parameters separated by commas (,).</span></span> <span data-ttu-id="530c3-150">各個參數的型別可以使用括號指定。</span><span class="sxs-lookup"><span data-stu-id="530c3-150">The type of each parameter can be specified with parentheses.</span></span> <span data-ttu-id="530c3-151">例如，您可以加入 `Path="[(sys:Int32)42,(sys:Int32)24]"`，其中 `sys` 對應至 `System` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="530c3-151">For example, you can have `Path="[(sys:Int32)42,(sys:Int32)24]"`, where `sys` is mapped to the `System` namespace.</span></span>

- <span data-ttu-id="530c3-152">當來源為集合檢視時，就可以使用斜線 (/) 指定目前的項目。</span><span class="sxs-lookup"><span data-stu-id="530c3-152">When the source is a collection view, the current item can be specified with a slash (/).</span></span> <span data-ttu-id="530c3-153">例如，子句 `Path=/` 會將繫結設定為檢視中目前的項目。</span><span class="sxs-lookup"><span data-stu-id="530c3-153">For example, the clause `Path=/` sets the binding to the current item in the view.</span></span> <span data-ttu-id="530c3-154">如果來源為集合，這個語法就會指定預設集合檢視目前的項目。</span><span class="sxs-lookup"><span data-stu-id="530c3-154">When the source is a collection, this syntax specifies the current item of the default collection view.</span></span>

- <span data-ttu-id="530c3-155">屬性名稱和斜線可以組合用來周遊本身為集合的屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-155">Property names and slashes can be combined to traverse properties that are collections.</span></span> <span data-ttu-id="530c3-156">例如，`Path=/Offices/ManagerName` 會指定來源集合目前的項目，其中包含同樣為集合的 `Offices` 屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-156">For example, `Path=/Offices/ManagerName` specifies the current item of the source collection, which contains an `Offices` property that is also a collection.</span></span> <span data-ttu-id="530c3-157">其目前項目為包含 `ManagerName` 屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="530c3-157">Its current item is an object that contains a `ManagerName` property.</span></span>

- <span data-ttu-id="530c3-158">另外，可以使用句號 (.) 路徑來繫結至目前的來源。</span><span class="sxs-lookup"><span data-stu-id="530c3-158">Optionally, a period (.) path can be used to bind to the current source.</span></span> <span data-ttu-id="530c3-159">例如，`Text="{Binding}"` 等於 `Text="{Binding Path=.}"`。</span><span class="sxs-lookup"><span data-stu-id="530c3-159">For example, `Text="{Binding}"` is equivalent to `Text="{Binding Path=.}"`.</span></span>

### <a name="escaping-mechanism"></a><span data-ttu-id="530c3-160">逸出機制</span><span class="sxs-lookup"><span data-stu-id="530c3-160">Escaping Mechanism</span></span>

- <span data-ttu-id="530c3-161">在索引子 ([ ]) 內，插入號字元 (^) 會逸出下一個字元。</span><span class="sxs-lookup"><span data-stu-id="530c3-161">Inside indexers ([ ]), the caret character (^) escapes the next character.</span></span>

- <span data-ttu-id="530c3-162">如果您 <xref:System.Windows.Data.Binding.Path%2A> 在 XAML 中設定，您也需要對 xml 語言定義的特殊字元進行 escape （使用 xml 實體）：</span><span class="sxs-lookup"><span data-stu-id="530c3-162">If you set <xref:System.Windows.Data.Binding.Path%2A> in XAML, you also need to escape (using XML entities) certain characters that are special to the XML language definition:</span></span>

  - <span data-ttu-id="530c3-163">使用 `&amp;` 逸出 "&" 字元。</span><span class="sxs-lookup"><span data-stu-id="530c3-163">Use `&amp;` to escape the character "&".</span></span>

  - <span data-ttu-id="530c3-164">使用 `&gt;` 逸出 ">" 結束標記。</span><span class="sxs-lookup"><span data-stu-id="530c3-164">Use `&gt;` to escape the end tag ">".</span></span>

- <span data-ttu-id="530c3-165">此外，如果您使用標記延伸語法在屬性中描述完整的繫結，您必須逸出 (使用反斜線 \\) [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 標記延伸剖析器特有的字元：</span><span class="sxs-lookup"><span data-stu-id="530c3-165">Additionally, if you describe the entire binding in an attribute using the markup extension syntax, you need to escape (using backslash \\) characters that are special to the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] markup extension parser:</span></span>

  - <span data-ttu-id="530c3-166">反斜線 (\\) 本身是逸出字元。</span><span class="sxs-lookup"><span data-stu-id="530c3-166">Backslash (\\) is the escape character itself.</span></span>

  - <span data-ttu-id="530c3-167">等號 (=) 會分隔屬性名稱和屬性值。</span><span class="sxs-lookup"><span data-stu-id="530c3-167">The equal sign (=) separates property name from property value.</span></span>

  - <span data-ttu-id="530c3-168">逗號 (,) 會分隔屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-168">Comma (,) separates properties.</span></span>

  - <span data-ttu-id="530c3-169">右大括號 (}) 是標記延伸的結尾。</span><span class="sxs-lookup"><span data-stu-id="530c3-169">The right curly brace (}) is the end of a markup extension.</span></span>

<a name="Default"></a>

## <a name="default-behaviors"></a><span data-ttu-id="530c3-170">預設行為</span><span class="sxs-lookup"><span data-stu-id="530c3-170">Default Behaviors</span></span>

<span data-ttu-id="530c3-171">如果宣告中未指定，則預設行為如下。</span><span class="sxs-lookup"><span data-stu-id="530c3-171">The default behavior is as follows if not specified in the declaration.</span></span>

- <span data-ttu-id="530c3-172">建立預設轉換器，以嘗試在繫結來源值和繫結目標值之間執行型別轉換。</span><span class="sxs-lookup"><span data-stu-id="530c3-172">A default converter is created that tries to do a type conversion between the binding source value and the binding target value.</span></span> <span data-ttu-id="530c3-173">如果無法進行轉換，預設轉換器會傳回 `null`。</span><span class="sxs-lookup"><span data-stu-id="530c3-173">If a conversion cannot be made, the default converter returns `null`.</span></span>

- <span data-ttu-id="530c3-174">如果未設定，系結 <xref:System.Windows.Data.Binding.ConverterCulture%2A> 引擎會使用系結 `Language` 目標物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="530c3-174">If you do not set <xref:System.Windows.Data.Binding.ConverterCulture%2A>, the binding engine uses the `Language` property of the binding target object.</span></span> <span data-ttu-id="530c3-175">在 XAML 中，這個值預設為 "en-US"，但如果已明確設定，則會繼承頁面之根元素 (或任何元素) 的值。</span><span class="sxs-lookup"><span data-stu-id="530c3-175">In XAML, this defaults to "en-US" or inherits the value from the root element (or any element) of the page, if one has been explicitly set.</span></span>

- <span data-ttu-id="530c3-176">只要繫結已經有資料內容 (例如繼承的資料內容來自父元素)，而且該內容所傳回的任何項目或集合不需要進一步修改路徑即可適用於繫結，繫結宣告可以完全沒有子句：`{Binding}`。這通常是資料樣式設定指定繫結的方式，其中繫結的作用對象是集合。</span><span class="sxs-lookup"><span data-stu-id="530c3-176">As long as the binding already has a data context (for instance, the inherited data context coming from a parent element), and whatever item or collection being returned by that context is appropriate for binding without requiring further path modification, a binding declaration can have no clauses at all: `{Binding}` This is often the way a binding is specified for data styling, where the binding acts upon a collection.</span></span> <span data-ttu-id="530c3-177">如需詳細資訊，請參閱[繫結來源概觀](binding-sources-overview.md)中的＜使用整個物件做為繫結來源＞一節。</span><span class="sxs-lookup"><span data-stu-id="530c3-177">For more information, see the "Entire Objects Used as a Binding Source" section in the [Binding Sources Overview](binding-sources-overview.md).</span></span>

- <span data-ttu-id="530c3-178">預設會根據所系結的相依性屬性，在 <xref:System.Windows.Data.Binding.Mode%2A> 單向和雙向之間有所不同。</span><span class="sxs-lookup"><span data-stu-id="530c3-178">The default <xref:System.Windows.Data.Binding.Mode%2A> varies between one-way and two-way depending on the dependency property that is being bound.</span></span> <span data-ttu-id="530c3-179">您永遠都可以明確宣告繫結模式，以確保繫結具有所需的行為。</span><span class="sxs-lookup"><span data-stu-id="530c3-179">You can always declare the binding mode explicitly to ensure that your binding has the desired behavior.</span></span> <span data-ttu-id="530c3-180">一般而言，使用者可編輯的控制項屬性（例如 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=nameWithType> ）預設為雙向系結，而其他大多數屬性則預設為單向系結。</span><span class="sxs-lookup"><span data-stu-id="530c3-180">In general, user-editable control properties, such as <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> and <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=nameWithType>, default to two-way bindings, whereas most other properties default to one-way bindings.</span></span>

- <span data-ttu-id="530c3-181">根據系結的相依性 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 屬性，預設值會在和之間有所不同 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> 。</span><span class="sxs-lookup"><span data-stu-id="530c3-181">The default <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> value varies between <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> and <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> depending on the bound dependency property as well.</span></span> <span data-ttu-id="530c3-182">大多數相依性屬性的預設值為 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>，而 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 屬性具有 <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> 的預設值。</span><span class="sxs-lookup"><span data-stu-id="530c3-182">The default value for most dependency properties is <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>, while the <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> property has a default value of <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus>.</span></span>

## <a name="see-also"></a><span data-ttu-id="530c3-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="530c3-183">See also</span></span>

- [<span data-ttu-id="530c3-184">資料系結總覽</span><span class="sxs-lookup"><span data-stu-id="530c3-184">Data Binding Overview</span></span>](../../../desktop-wpf/data/data-binding-overview.md)
- [<span data-ttu-id="530c3-185">操作說明主題</span><span class="sxs-lookup"><span data-stu-id="530c3-185">How-to Topics</span></span>](data-binding-how-to-topics.md)
- [<span data-ttu-id="530c3-186">資料繫結</span><span class="sxs-lookup"><span data-stu-id="530c3-186">Data Binding</span></span>](../advanced/optimizing-performance-data-binding.md)
- [<span data-ttu-id="530c3-187">PropertyPath XAML 語法</span><span class="sxs-lookup"><span data-stu-id="530c3-187">PropertyPath XAML Syntax</span></span>](../advanced/propertypath-xaml-syntax.md)

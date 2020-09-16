---
title: XAML 2009 語言功能
ms.date: 03/30/2017
helpviewer_keywords:
- XAML 2009 [XAML Services]
- XAML [XAML Services], XAML 2009
ms.assetid: f6bb18d8-c86a-4549-8862-323e6b32a8dd
ms.openlocfilehash: dfa2841d8bc1ed1429372908f0dda97d178c4ac3
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556703"
---
# <a name="xaml-2009-language-features"></a><span data-ttu-id="6eb8c-102">XAML 2009 語言功能</span><span class="sxs-lookup"><span data-stu-id="6eb8c-102">XAML 2009 Language Features</span></span>
<span data-ttu-id="6eb8c-103">XAML 2009 是新 XAML 語言功能的縮寫詞彙，可擴充現有的 XAML 語言規格。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-103">XAML 2009 is the shorthand term for new XAML language features that extend the existing XAML language specification.</span></span> <span data-ttu-id="6eb8c-104">XAML 2009 引進了數個新的指示詞和建構。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-104">XAML 2009 introduces several new directives and constructs.</span></span> <span data-ttu-id="6eb8c-105">這些包含 [x:Arguments](xarguments-directive.md)指示詞; [x:FactoryMethod](xfactorymethod-directive.md)指示詞; [X:Reference 標記延伸](xreference-markup-extension.md); [x:TypeArguments](xtypearguments-directive.md)指示詞;以及通用語言基本類型的內建類型 (例如 `x:Char`) 。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-105">These include the [x:Arguments Directive](xarguments-directive.md); the [x:FactoryMethod Directive](xfactorymethod-directive.md); the [x:Reference Markup Extension](xreference-markup-extension.md); the [x:TypeArguments Directive](xtypearguments-directive.md); and built-in types for common language primitives (for example `x:Char`).</span></span>

## <a name="xaml-2009-support-in-wpf-and-visual-studio"></a><span data-ttu-id="6eb8c-106">WPF 和 Visual Studio 中的 XAML 2009 支援</span><span class="sxs-lookup"><span data-stu-id="6eb8c-106">XAML 2009 Support in WPF and Visual Studio</span></span>

<span data-ttu-id="6eb8c-107">在 WPF 中，您可以使用 XAML 2009 功能，但只能針對未編譯 WPF 標記的 XAML。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-107">In WPF, you can use XAML 2009 features, but only for XAML that is not WPF markup-compiled.</span></span> <span data-ttu-id="6eb8c-108">編譯標記的 XAML 和 BAML 形式的 XAML 目前不支援 XAML 2009 語言關鍵字和功能。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-108">Markup-compiled XAML and the BAML form of XAML do not currently support the XAML 2009 language keywords and features.</span></span>

<span data-ttu-id="6eb8c-109">請注意，對於 CLR 類型和類型系統，在 WPF 中載入鬆散 XAML 的現有技術，可能也會有比編譯標記的 XAML 更嚴格的安全性和存取限制。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-109">Note that existing techniques for loading loose XAML in WPF also have possible security and access restrictions to CLR types and the type system that are more restrictive than for markup-compiled XAML.</span></span> <span data-ttu-id="6eb8c-110">如需詳細資訊，請參閱 [安全性 (WPF)](/dotnet/desktop/wpf/security-wpf) 或 [WPF 安全性策略 - 平台安全性](/dotnet/desktop/wpf/wpf-security-strategy-platform-security)。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-110">For more information, see [Security (WPF)](/dotnet/desktop/wpf/security-wpf) or [WPF Security Strategy - Platform Security](/dotnet/desktop/wpf/wpf-security-strategy-platform-security).</span></span>

<span data-ttu-id="6eb8c-111">XAML 2009 也引進了額外的功能，可修改先前的 XAML 2006 建構或修改基本標記形式。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-111">XAML 2009 also introduces additional features that either modify the previous XAML 2006 constructs or that modify the basic markup forms.</span></span>

### <a name="xkey-as-an-object-element"></a><span data-ttu-id="6eb8c-112">x:Key 做為物件項目</span><span class="sxs-lookup"><span data-stu-id="6eb8c-112">x:Key as an Object Element</span></span>

<span data-ttu-id="6eb8c-113">XAML 2009 可支援 `x:Key` 做為物件 (具有物件項目值的屬性 (Property) 項目)，但 XAML 2006 僅支援 `x:Key` 做為屬性 (Attribute)。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-113">XAML 2009 can support `x:Key` as an object (a property element that has object element value); however, XAML 2006 only supported `x:Key` as an attribute.</span></span> <span data-ttu-id="6eb8c-114">請參閱 [x:Key Directive](xkey-directive.md)的＜XAML 2009＞一節。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-114">See the "XAML 2009" section of [x:Key Directive](xkey-directive.md).</span></span>

### <a name="xmlns-on-property-elements"></a><span data-ttu-id="6eb8c-115">屬性項目上的 xmlns</span><span class="sxs-lookup"><span data-stu-id="6eb8c-115">xmlns on Property Elements</span></span>

<span data-ttu-id="6eb8c-116">XAML 2009 可支援屬性項目的 XAML 命名空間 (xmlns) 定義，但 XAML 2006 僅支援物件項目上的 xmlns 定義。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-116">XAML 2009 can support XAML namespace (xmlns) definitions on property elements; however, XAML 2006 only supports xmlns definitions on object elements.</span></span>

### <a name="event-attributes"></a><span data-ttu-id="6eb8c-117">事件屬性</span><span class="sxs-lookup"><span data-stu-id="6eb8c-117">Event Attributes</span></span>

<span data-ttu-id="6eb8c-118">針對事件所支援的屬性，XAML 2006 會假定標記編譯與將事件送出到標記編譯有關。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-118">For attributes that are backed by events, XAML 2006 presumes that markup compilation is involved and submits the events to markup compilation.</span></span> <span data-ttu-id="6eb8c-119">XAML 2009 支援類似標記延伸的標記形式，這會將事件連接延遲到 XAML 的執行階段剖析和載入。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-119">XAML 2009 supports a markup form that resembles a markup extension, which defers the event wiring until run-time parsing and loading of the XAML.</span></span> <span data-ttu-id="6eb8c-120">不過，WPF 應用程式和 WPF UI 的 XAML 情節通常不會使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-120">However, WPF applications and XAML scenarios for WPF UI generally do not use this capability.</span></span> <span data-ttu-id="6eb8c-121">WPF 及其 XAML 2006 實作會使用事件處理常式連接組合進行在 <xref:System.Windows.UIElement> 層級定義的路由事件，並使用其標記編譯器步驟進行大部分的事件屬性處理。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-121">WPF and its XAML 2006 implementation uses the combination of event handler wiring for routed events defined at the <xref:System.Windows.UIElement> level and its markup compiler step for much of its event attribute processing.</span></span> <span data-ttu-id="6eb8c-122">標記編譯器也會前置處理在 XAML 中找到的任何事件屬性，建置動作會在此 XAML 中宣告使用標記編譯器。</span><span class="sxs-lookup"><span data-stu-id="6eb8c-122">The markup compiler also preprocesses any event attributes found in XAML where the build actions declare that the markup compiler is used.</span></span>

## <a name="see-also"></a><span data-ttu-id="6eb8c-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6eb8c-123">See also</span></span>

- [<span data-ttu-id="6eb8c-124">XAML 概觀 (WPF)</span><span class="sxs-lookup"><span data-stu-id="6eb8c-124">XAML Overview (WPF)</span></span>](../fundamentals/xaml.md)

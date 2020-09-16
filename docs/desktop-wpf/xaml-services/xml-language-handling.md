---
title: XAML 中的 xml:lang 處理
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:lang attribute
- xml:lang attribute [XAML Services]
- RFC 3066 standard [XAML Services]
- standards [XAML Services], RFC 3066
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
ms.openlocfilehash: 92d1eda62ff394df54d9607bab46d9950681e603
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90548204"
---
# <a name="xmllang-handling-in-xaml"></a><span data-ttu-id="84df6-102">XAML 中的 xml:lang 處理</span><span class="sxs-lookup"><span data-stu-id="84df6-102">xml:lang Handling in XAML</span></span>

<span data-ttu-id="84df6-103">`xml:lang`屬性是 xml 定義的屬性，會宣告 xml 中元素的語言和文化特性資訊。</span><span class="sxs-lookup"><span data-stu-id="84df6-103">The `xml:lang` attribute is an XML-defined attribute that declares the language and culture information for an element in XML.</span></span> <span data-ttu-id="84df6-104">在 XAML 中有保存與這個屬性相同的意義，但仍須考量一些其他事項。</span><span class="sxs-lookup"><span data-stu-id="84df6-104">This same meaning of the attribute persists in XAML; however, some additional considerations apply.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="84df6-105">XAML Attribute Usage</span><span class="sxs-lookup"><span data-stu-id="84df6-105">XAML Attribute Usage</span></span>

```xaml
<object xml:lang="rfc3066lang" />
```

## <a name="xaml-values"></a><span data-ttu-id="84df6-106">XAML 值</span><span class="sxs-lookup"><span data-stu-id="84df6-106">XAML Values</span></span>

|||
|-|-|
|<span data-ttu-id="84df6-107">*rfc3066lang*</span><span class="sxs-lookup"><span data-stu-id="84df6-107">*rfc3066lang*</span></span>|<span data-ttu-id="84df6-108">衍生自 [RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) 標準的字串，這個字串會識別語言或語言地區。</span><span class="sxs-lookup"><span data-stu-id="84df6-108">A string that is derived from the [RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) standard and identifies either a language or a language-region.</span></span> <span data-ttu-id="84df6-109">如果是後者，則語言和區域會由單一連字號分隔。</span><span class="sxs-lookup"><span data-stu-id="84df6-109">When it is the latter, the language and region are separated by a single hyphen.</span></span> <span data-ttu-id="84df6-110">如需值和格式的詳細資訊，請參閱 <xref:System.Windows.Markup.XmlLanguage> 。</span><span class="sxs-lookup"><span data-stu-id="84df6-110">See <xref:System.Windows.Markup.XmlLanguage> for more information about the values and format.</span></span>|

## <a name="remarks"></a><span data-ttu-id="84df6-111">備註</span><span class="sxs-lookup"><span data-stu-id="84df6-111">Remarks</span></span>

<span data-ttu-id="84df6-112">`xml:lang`在中，屬性的定義 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 衍生自 `xml:lang` 全球資訊網協會 (W3C) for XML 所定義為「特殊屬性」。</span><span class="sxs-lookup"><span data-stu-id="84df6-112">The definition for the `xml:lang` attribute in [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] is derived from `xml:lang` as defined as a "special attribute" by the World Wide Web Consortium (W3C) for XML.</span></span> <span data-ttu-id="84df6-113">項目在處理語言和文化特性時，其方式可能隨著不同的實作而改變，但是 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 屬性並沒有預設的 `xml:lang` 處理。</span><span class="sxs-lookup"><span data-stu-id="84df6-113">Language and culture information is potentially processed in different ways by elements, depending on their implementations; however, there is no default [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] processing of the `xml:lang` attribute.</span></span>

<span data-ttu-id="84df6-114">`xml:lang` 屬性的預設值在屬性層級為空字串。</span><span class="sxs-lookup"><span data-stu-id="84df6-114">The default value of the `xml:lang` attribute is an empty string at the attribute level.</span></span>

<span data-ttu-id="84df6-115">`xml:lang` 屬性效果和屬性的值，通常由對 `xml:lang` 值作用的系統解譯時，就會以子項目的形式永存。</span><span class="sxs-lookup"><span data-stu-id="84df6-115">The `xml:lang` attribute effects and the value of the attribute are generally perpetuated to child elements, when interpreted by systems that act on `xml:lang` values.</span></span>

<span data-ttu-id="84df6-116">當 .NET XAML 服務的 XAML 寫入器解釋時， `xml:lang` 值可以 <xref:System.Windows.Markup.XmlLanguage> <xref:System.Globalization.CultureInfo> 在基礎物件表示中建立或物件; 不過，該行為取決於指定的值是否為 `xml:lang` 這些類別的有效結構。</span><span class="sxs-lookup"><span data-stu-id="84df6-116">When interpreted by XAML writers of .NET XAML Services, an `xml:lang` value can create <xref:System.Windows.Markup.XmlLanguage> or <xref:System.Globalization.CultureInfo> objects in the underlying object representation; however, that behavior depends on whether the value specified for `xml:lang` is a valid construction for those classes.</span></span>

<span data-ttu-id="84df6-117">藉由將 `xml:lang` 套用至屬性，架構即可在架構定義的屬性和 XML 中 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 的意義之間建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="84df6-117">Frameworks can create associations between framework-defined properties and the meaning of `xml:lang` in XML by applying <xref:System.Windows.Markup.XmlLangPropertyAttribute> to the property.</span></span>

## <a name="wpf-usage-nodes"></a><span data-ttu-id="84df6-118">WPF 使用量節點</span><span class="sxs-lookup"><span data-stu-id="84df6-118">WPF Usage Nodes</span></span>

<span data-ttu-id="84df6-119">若項目是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>的衍生類別，您可以使用對等的 <xref:System.Windows.FrameworkElement.Language%2A> 相依性屬性 (Property)，而非 `xml:lang` 屬性 (Attribute)。</span><span class="sxs-lookup"><span data-stu-id="84df6-119">For elements that are derived classes of <xref:System.Windows.FrameworkElement> or <xref:System.Windows.FrameworkContentElement>, you can use the equivalent <xref:System.Windows.FrameworkElement.Language%2A> dependency property instead of the `xml:lang` attribute.</span></span> <span data-ttu-id="84df6-120">根據預設，如果沒有透過屬性 (Property) 或是透過處理 <xref:System.Windows.FrameworkElement.Language%2A> 屬性 (Attribute) 另外設定，則 `xml:lang` 屬性會使用 "en-US"。</span><span class="sxs-lookup"><span data-stu-id="84df6-120">By default, the <xref:System.Windows.FrameworkElement.Language%2A> property uses "en-US" if it is not otherwise set, either through the property or through processing the `xml:lang` attribute.</span></span>

## <a name="see-also"></a><span data-ttu-id="84df6-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84df6-121">See also</span></span>

- [<span data-ttu-id="84df6-122">WPF 的全球化</span><span class="sxs-lookup"><span data-stu-id="84df6-122">Globalization for WPF</span></span>](/dotnet/desktop/wpf/advanced/globalization-for-wpf)

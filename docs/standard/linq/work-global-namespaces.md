---
title: 使用 Visual Basic LINQ to XML 中的全域命名空間
description: 您可以使用 Imports 語句，在 Visual Basic 中宣告命名空間，這是指命名空間是預設命名空間，還是有前置詞。 本文討論匯入語句和使用命名空間的其他層面。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 0a8064d5-e02f-4315-ad48-6deaa443a2f0
ms.openlocfilehash: f05fcab6788388e36e2b68a2d4f022ea63e74280
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552816"
---
# <a name="work-with-global-namespaces-in-visual-basic-linq-to-xml"></a><span data-ttu-id="df0d3-104">使用 Visual Basic (LINQ to XML 中的全域命名空間) </span><span class="sxs-lookup"><span data-stu-id="df0d3-104">Work with global namespaces in Visual Basic (LINQ to XML)</span></span>

<span data-ttu-id="df0d3-105">Visual Basic 中 XML 常值的其中一個重要功能，就是使用語句宣告 XML 命名空間的功能 `Imports` 。</span><span class="sxs-lookup"><span data-stu-id="df0d3-105">One of the key features of XML literals in Visual Basic is the capability to declare XML namespaces by using the `Imports` statement.</span></span> <span data-ttu-id="df0d3-106">利用這個功能，您可以宣告使用前置詞的 XML 命名空間，或者，您可以宣告預設的 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-106">Using this feature, you can declare an XML namespace that uses a prefix, or you can declare a default XML namespace.</span></span>

<span data-ttu-id="df0d3-107">這項功能在兩種情況下很有用：</span><span class="sxs-lookup"><span data-stu-id="df0d3-107">This capability is useful in two situations:</span></span>

- <span data-ttu-id="df0d3-108">XML 常值中宣告的命名空間不會延續到內嵌的運算式中。</span><span class="sxs-lookup"><span data-stu-id="df0d3-108">Namespaces declared in XML literals don't carry over into embedded expressions.</span></span> <span data-ttu-id="df0d3-109">宣告全域命名空間可減少使用內嵌運算式搭配命名空間所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="df0d3-109">Declaring global namespaces reduces the amount of work needed to use embedded expressions with namespaces.</span></span>
- <span data-ttu-id="df0d3-110">您必須宣告全域命名空間，才能使用具有 XML 屬性的命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-110">You must declare global namespaces in order to use namespaces with XML properties.</span></span>

<span data-ttu-id="df0d3-111">您可以在專案層級宣告全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-111">You can declare global namespaces at the project level.</span></span> <span data-ttu-id="df0d3-112">您也可以在複寫專案層級全域命名空間的模組層級宣告全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-112">You can also declare global namespaces at the module level, which overrides the project-level global namespaces.</span></span> <span data-ttu-id="df0d3-113">最後，您可以在 XML 常值中複寫全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-113">Finally, you can override global namespaces in an XML literal.</span></span>

<span data-ttu-id="df0d3-114">使用全域宣告命名空間中的 XML 常值或 XML 屬性時，您可以在 Visual Studio 中將滑鼠游標移到 XML 常值或屬性的擴充名稱。</span><span class="sxs-lookup"><span data-stu-id="df0d3-114">When using XML literals or XML properties that are in globally declared namespaces, you can see the expanded name of XML literals or properties by hovering over them in Visual Studio.</span></span> <span data-ttu-id="df0d3-115">您將會在工具提示中看到擴充名稱。</span><span class="sxs-lookup"><span data-stu-id="df0d3-115">You will see the expanded name in a tooltip.</span></span>

<span data-ttu-id="df0d3-116">您可以使用 <xref:System.Xml.Linq.XNamespace> 方法，取得對應到全域命名空間的 `GetXmlNamespace` 物件。</span><span class="sxs-lookup"><span data-stu-id="df0d3-116">You can get an <xref:System.Xml.Linq.XNamespace> object that corresponds to a global namespace using the `GetXmlNamespace` method.</span></span>

## <a name="example-use-imports-to-declare-a-global-namespace"></a><span data-ttu-id="df0d3-117">範例：用 `Imports` 來宣告全域命名空間</span><span class="sxs-lookup"><span data-stu-id="df0d3-117">Example: Use `Imports` to declare a global namespace</span></span>

<span data-ttu-id="df0d3-118">下列範例會使用語句宣告預設的全域命名空間 `Imports` ，然後 <xref:System.Xml.Linq.XElement> 使用 XML 常值來初始化該命名空間中的物件：</span><span class="sxs-lookup"><span data-stu-id="df0d3-118">The following example declares a default global namespace with the `Imports` statement, and then initializes an <xref:System.Xml.Linq.XElement> object in that namespace with an XML literal:</span></span>

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <Root/>
        Console.WriteLine(root)
    End Sub
End Module
```

<span data-ttu-id="df0d3-119">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-119">This example produces the following output:</span></span>

```xml
<Root xmlns="http://www.adventure-works.com" />
```

## <a name="example-declare-a-global-namespace-that-has-a-prefix"></a><span data-ttu-id="df0d3-120">範例：宣告具有前置詞的全域命名空間</span><span class="sxs-lookup"><span data-stu-id="df0d3-120">Example: Declare a global namespace that has a prefix</span></span>

<span data-ttu-id="df0d3-121">下一個範例會宣告具有前置詞的全域命名空間，並使用 XML 常值來初始化元素：</span><span class="sxs-lookup"><span data-stu-id="df0d3-121">The next example declares a global namespace with a prefix, and initializes an element with an XML literal:</span></span>

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <aw:Root/>
        Console.WriteLine(root)
    End Sub
End Module
```

<span data-ttu-id="df0d3-122">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-122">This example produces the following output:</span></span>

```xml
<aw:Root xmlns:aw="http://www.adventure-works.com" />
```

## <a name="example-declare-a-default-namespace-and-use-an-embedded-expression-for-the-child-element"></a><span data-ttu-id="df0d3-123">範例：宣告預設命名空間，並針對元素使用內嵌運算式 `Child`</span><span class="sxs-lookup"><span data-stu-id="df0d3-123">Example: Declare a default namespace and use an embedded expression for the `Child` element</span></span>

<span data-ttu-id="df0d3-124">在 XML 常值中宣告的命名空間不會延續到內嵌的運算式中。</span><span class="sxs-lookup"><span data-stu-id="df0d3-124">Namespaces that are declared in XML literals don't carry over into embedded expressions.</span></span> <span data-ttu-id="df0d3-125">下列範例會宣告預設的命名空間，然後使用專案的內嵌運算式 `Child` 。</span><span class="sxs-lookup"><span data-stu-id="df0d3-125">The following example declares a default namespace, and then uses an embedded expression for the `Child` element.</span></span>

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <%= <Child/> %>
    </Root>
Console.WriteLine(root)
```

<span data-ttu-id="df0d3-126">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-126">This example produces the following output:</span></span>

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child xmlns="" />
</Root>
```

<span data-ttu-id="df0d3-127">產生的 XML 包含預設命名空間的宣告，因此 `Child` 元素不在命名空間中。</span><span class="sxs-lookup"><span data-stu-id="df0d3-127">The resulting XML includes a declaration of a default namespace so that the `Child` element is in no namespace.</span></span>

<span data-ttu-id="df0d3-128">您可以在內嵌運算式中宣告不同的命名空間，如下所示：</span><span class="sxs-lookup"><span data-stu-id="df0d3-128">You could declare a different namespace in the embedded expression, as follows:</span></span>

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <%= <Child xmlns="http://www.adventure-works.com"/> %>
    </Root>
Console.WriteLine(root)
```

<span data-ttu-id="df0d3-129">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-129">This example produces the following output:</span></span>

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child xmlns="http://www.adventure-works.com" />
</Root>
```

<span data-ttu-id="df0d3-130">不過，使用全域預設命名空間時，您可以使用 XML 常值，而不需要宣告命名空間。</span><span class="sxs-lookup"><span data-stu-id="df0d3-130">However, with the global default namespace you can use XML literals without declaring namespaces.</span></span> <span data-ttu-id="df0d3-131">產生的 XML 會在全域宣告的預設命名空間中，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="df0d3-131">The resulting XML will be in the globally-declared default namespace, as in this example:</span></span>

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <Root>
                                   <%= <Child/> %>
                               </Root>
        Console.WriteLine(root)
    End Sub
End Module
```

<span data-ttu-id="df0d3-132">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-132">This example produces the following output:</span></span>

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child />
</Root>
```

## <a name="example-use-namespaces-with-xml-properties"></a><span data-ttu-id="df0d3-133">範例：搭配使用命名空間與 XML 屬性</span><span class="sxs-lookup"><span data-stu-id="df0d3-133">Example: Use namespaces with XML properties</span></span>

<span data-ttu-id="df0d3-134">如果您使用的是命名空間中的 XML 樹狀結構，而且您使用 XML 屬性，則必須使用全域命名空間，如此 XML 屬性也會在正確的命名空間中。</span><span class="sxs-lookup"><span data-stu-id="df0d3-134">If you're working with an XML tree that's in a namespace, and you use XML properties, then you must use a global namespace so that the XML properties will also be in the correct namespace.</span></span> <span data-ttu-id="df0d3-135">下列範例會宣告命名空間中的 XML 樹狀結構，然後列印元素的計數 `Child` 。</span><span class="sxs-lookup"><span data-stu-id="df0d3-135">The following example declares an XML tree in a namespace, and then prints the count of `Child` elements.</span></span>

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <Child>content</Child>
    </Root>
Console.WriteLine(root.<Child>.Count())
```

<span data-ttu-id="df0d3-136">這個範例表示沒有 `Child` 項目。</span><span class="sxs-lookup"><span data-stu-id="df0d3-136">This example indicates that there are no `Child` elements.</span></span> <span data-ttu-id="df0d3-137">它會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-137">It produces this output:</span></span>

```output
0
```

<span data-ttu-id="df0d3-138">但是，如果您要宣告預設的全域命名空間，則 XML 常值和 XML 屬性都會位於預設的全域命名空間中：</span><span class="sxs-lookup"><span data-stu-id="df0d3-138">If, however, you declare a default global namespace, then both the XML literal and the XML property are in the default global namespace:</span></span>

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root>
                <Child>content</Child>
            </Root>
        Console.WriteLine(root.<Child>.Count())
    End Sub
End Module
```

<span data-ttu-id="df0d3-139">這個範例表示有一個 `Child` 項目，</span><span class="sxs-lookup"><span data-stu-id="df0d3-139">This example indicates that there is one `Child` element.</span></span> <span data-ttu-id="df0d3-140">它會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-140">It produces this output:</span></span>

```output
1
```

<span data-ttu-id="df0d3-141">如果您要宣告具有前置詞的全域命名空間，可以將前置詞同時用於 XML 常值和 XML 屬性：</span><span class="sxs-lookup"><span data-stu-id="df0d3-141">If you declare a global namespace that has a prefix, you can use the prefix for both XML literals and XML properties:</span></span>

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <aw:Child>content</aw:Child>
            </aw:Root>
        Console.WriteLine(root.<aw:Child>.Count())
    End Sub
End Module
```

## <a name="example-use-getxmlnamespace-to-get-an-xnamespace"></a><span data-ttu-id="df0d3-142">範例：使用 `GetXmlNamespace` 取得 `XNamespace`</span><span class="sxs-lookup"><span data-stu-id="df0d3-142">Example: Use `GetXmlNamespace` to get an `XNamespace`</span></span>

<span data-ttu-id="df0d3-143">您可以 <xref:System.Xml.Linq.XNamespace> 使用方法來取得物件 `GetXmlNamespace` ：</span><span class="sxs-lookup"><span data-stu-id="df0d3-143">You can obtain an <xref:System.Xml.Linq.XNamespace> object by using the `GetXmlNamespace` method:</span></span>

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <aw:Root/>
        Dim xn As XNamespace = GetXmlNamespace(aw)
        Console.WriteLine(xn)
    End Sub
End Module
```

<span data-ttu-id="df0d3-144">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="df0d3-144">This example produces the following output:</span></span>

```output
http://www.adventure-works.com
```

## <a name="see-also"></a><span data-ttu-id="df0d3-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df0d3-145">See also</span></span>

- [<span data-ttu-id="df0d3-146">命名空間總覽</span><span class="sxs-lookup"><span data-stu-id="df0d3-146">Namespaces overview</span></span>](namespaces-overview.md)

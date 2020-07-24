---
title: 在 C# 中建立 XML 樹狀 (LINQ to XML)
description: '瞭解如何在 c # 中建立 XML 樹狀結構，包括使用 System.xml.linq.xelement> 的函式來建立元素。'
ms.date: 08/31/2018
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
ms.openlocfilehash: 3991f461c4c870a64320853ccd1d45026a8a6bf6
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105481"
---
# <a name="creating-xml-trees-in-c-linq-to-xml"></a><span data-ttu-id="5170f-103">在 C# 中建立 XML 樹狀結構 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="5170f-103">Creating XML trees in C# (LINQ to XML)</span></span>
<span data-ttu-id="5170f-104">本節提供在 C# 中建立 XML 樹狀的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5170f-104">This section provides information about creating XML trees in C#.</span></span>  
  
 <span data-ttu-id="5170f-105">如需使用 LINQ 查詢的結果作為 <xref:System.Xml.Linq.XElement> 內容的資訊，請參閱[函數式建構 (LINQ to XML) (C#)](./functional-construction-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="5170f-105">For information about using the results of LINQ queries as the content for an <xref:System.Xml.Linq.XElement>, see [Functional Construction (LINQ to XML) (C#)](./functional-construction-linq-to-xml.md).</span></span>  
  
## <a name="constructing-elements"></a><span data-ttu-id="5170f-106">建構項目</span><span class="sxs-lookup"><span data-stu-id="5170f-106">Constructing elements</span></span>
 <span data-ttu-id="5170f-107"><xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XAttribute> 建構函式的簽章可讓您傳遞項目或屬性的內容，當做建構函式的引數。</span><span class="sxs-lookup"><span data-stu-id="5170f-107">The signatures of the <xref:System.Xml.Linq.XElement> and <xref:System.Xml.Linq.XAttribute> constructors let you pass the contents of the element or attribute as arguments to the constructor.</span></span> <span data-ttu-id="5170f-108">由於其中一個建構函式採用多個引數，因此，您可以傳遞任何數目的子項目。</span><span class="sxs-lookup"><span data-stu-id="5170f-108">Because one of the constructors takes a variable number of arguments, you can pass any number of child elements.</span></span> <span data-ttu-id="5170f-109">當然，這些子項目中的每個子項目都可以包含其自己的子項目。</span><span class="sxs-lookup"><span data-stu-id="5170f-109">Of course, each of those child elements can contain their own child elements.</span></span> <span data-ttu-id="5170f-110">對於任何項目，您可以加入任何數目的屬性。</span><span class="sxs-lookup"><span data-stu-id="5170f-110">For any element, you can add any number of attributes.</span></span>  
  
 <span data-ttu-id="5170f-111">加入 <xref:System.Xml.Linq.XNode> (包括 <xref:System.Xml.Linq.XElement>) 或 <xref:System.Xml.Linq.XAttribute> 物件時，如果新內容沒有父代，這些物件只會附加到 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="5170f-111">When adding <xref:System.Xml.Linq.XNode> (including <xref:System.Xml.Linq.XElement>) or <xref:System.Xml.Linq.XAttribute> objects, if the new content has no parent, the objects are simply attached to the XML tree.</span></span> <span data-ttu-id="5170f-112">如果新內容已經成為父代，或是其他 XML 樹狀的一部分，則會複製新內容，而且新複製的內容會附加到 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="5170f-112">If the new content already is parented, and is part of another XML tree, the new content is cloned, and the newly cloned content is attached to the XML tree.</span></span> <span data-ttu-id="5170f-113">本主題中的最後一個範例會示範這個情況。</span><span class="sxs-lookup"><span data-stu-id="5170f-113">The last example in this topic demonstrates this.</span></span>  
  
 <span data-ttu-id="5170f-114">若要建立 `contacts`<xref:System.Xml.Linq.XElement>，您可以使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5170f-114">To create a `contacts`<xref:System.Xml.Linq.XElement>, you could use the following code:</span></span>  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 <span data-ttu-id="5170f-115">如果縮排正確，建構 <xref:System.Xml.Linq.XElement> 物件的程式碼會非常接近基礎 XML 的結構。</span><span class="sxs-lookup"><span data-stu-id="5170f-115">If indented properly, the code to construct <xref:System.Xml.Linq.XElement> objects closely resembles the structure of the underlying XML.</span></span>  
  
## <a name="xelement-constructors"></a><span data-ttu-id="5170f-116">XElement 建構函式</span><span class="sxs-lookup"><span data-stu-id="5170f-116">XElement constructors</span></span>  
 <span data-ttu-id="5170f-117"><xref:System.Xml.Linq.XElement> 類別會將下列建構函式用於功能結構。</span><span class="sxs-lookup"><span data-stu-id="5170f-117">The <xref:System.Xml.Linq.XElement> class uses the following constructors for functional construction.</span></span> <span data-ttu-id="5170f-118">請注意，<xref:System.Xml.Linq.XElement> 還有其他建構函式，但是它們不用於功能結構，因此未在此處列出。</span><span class="sxs-lookup"><span data-stu-id="5170f-118">Note that there are some other constructors for <xref:System.Xml.Linq.XElement>, but because they are not used for functional construction they are not listed here.</span></span>  
  
|<span data-ttu-id="5170f-119">建構函式</span><span class="sxs-lookup"><span data-stu-id="5170f-119">Constructor</span></span>|<span data-ttu-id="5170f-120">描述</span><span class="sxs-lookup"><span data-stu-id="5170f-120">Description</span></span>|  
|-----------------|-----------------|  
|`XElement(XName name, object content)`|<span data-ttu-id="5170f-121">建立 <xref:System.Xml.Linq.XElement>。</span><span class="sxs-lookup"><span data-stu-id="5170f-121">Creates an <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="5170f-122">`name` 參數會指定項目的名稱；`content` 會指定項目的內容。</span><span class="sxs-lookup"><span data-stu-id="5170f-122">The `name` parameter specifies the name of the element; `content` specifies the content of the element.</span></span>|  
|`XElement(XName name)`|<span data-ttu-id="5170f-123">在將其 <xref:System.Xml.Linq.XElement> 初始化為指定之名稱的情況下，建立 <xref:System.Xml.Linq.XName>。</span><span class="sxs-lookup"><span data-stu-id="5170f-123">Creates an <xref:System.Xml.Linq.XElement> with its <xref:System.Xml.Linq.XName> initialized to the specified name.</span></span>|  
|`XElement(XName name, params object[] content)`|<span data-ttu-id="5170f-124">在將其 <xref:System.Xml.Linq.XElement> 初始化為指定之名稱的情況下，建立 <xref:System.Xml.Linq.XName>。</span><span class="sxs-lookup"><span data-stu-id="5170f-124">Creates an <xref:System.Xml.Linq.XElement> with its <xref:System.Xml.Linq.XName> initialized to the specified name.</span></span> <span data-ttu-id="5170f-125">系統會從參數清單的內容建立屬性和/或子項目。</span><span class="sxs-lookup"><span data-stu-id="5170f-125">The attributes and/or child elements are created from the contents of the parameter list.</span></span>|  
  
 <span data-ttu-id="5170f-126">`content` 參數非常有彈性。</span><span class="sxs-lookup"><span data-stu-id="5170f-126">The `content` parameter is extremely flexible.</span></span> <span data-ttu-id="5170f-127">它支援物件為 <xref:System.Xml.Linq.XElement> 之有效子系的任何型別。</span><span class="sxs-lookup"><span data-stu-id="5170f-127">It supports any type of object that is a valid child of an <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="5170f-128">下列規則適用於傳入此參數的不同型別物件：</span><span class="sxs-lookup"><span data-stu-id="5170f-128">The following rules apply to different types of objects passed in this parameter:</span></span>  
  
- <span data-ttu-id="5170f-129">字串當做文字內容加入。</span><span class="sxs-lookup"><span data-stu-id="5170f-129">A string is added as text content.</span></span>  
  
- <span data-ttu-id="5170f-130"><xref:System.Xml.Linq.XElement> 當做子項目加入。</span><span class="sxs-lookup"><span data-stu-id="5170f-130">An <xref:System.Xml.Linq.XElement> is added as a child element.</span></span>  
  
- <span data-ttu-id="5170f-131"><xref:System.Xml.Linq.XAttribute> 當做屬性加入。</span><span class="sxs-lookup"><span data-stu-id="5170f-131">An <xref:System.Xml.Linq.XAttribute> is added as an attribute.</span></span>  
  
- <span data-ttu-id="5170f-132"><xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment> 或 <xref:System.Xml.Linq.XText> 當做子內容加入。</span><span class="sxs-lookup"><span data-stu-id="5170f-132">An <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment>, or <xref:System.Xml.Linq.XText> is added as child content.</span></span>  
  
- <span data-ttu-id="5170f-133">系統會列舉 <xref:System.Collections.IEnumerable>，並將這些規則遞迴地套用到結果。</span><span class="sxs-lookup"><span data-stu-id="5170f-133">An <xref:System.Collections.IEnumerable> is enumerated, and these rules are applied recursively to the results.</span></span>  
  
- <span data-ttu-id="5170f-134">若是其他任何型別，則會呼叫其 `ToString` 方法，並將結果當做文字內容加入。</span><span class="sxs-lookup"><span data-stu-id="5170f-134">For any other type, its `ToString` method is called and the result is added as text content.</span></span>  
  
### <a name="creating-an-xelement-with-content"></a><span data-ttu-id="5170f-135">建立包含內容的 XElement</span><span class="sxs-lookup"><span data-stu-id="5170f-135">Creating an XElement with content</span></span>  
 <span data-ttu-id="5170f-136">您可以建立包含具有單一方法呼叫之簡單內容的 <xref:System.Xml.Linq.XElement>。</span><span class="sxs-lookup"><span data-stu-id="5170f-136">You can create an <xref:System.Xml.Linq.XElement> that contains simple content with a single method call.</span></span> <span data-ttu-id="5170f-137">如果要這樣做，請將內容指定為第二個參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5170f-137">To do this, specify the content as the second parameter, as follows:</span></span>  
  
```csharp  
XElement n = new XElement("Customer", "Adventure Works");  
Console.WriteLine(n);  
```  
  
 <span data-ttu-id="5170f-138">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-138">This example produces the following output:</span></span>  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
 <span data-ttu-id="5170f-139">您可以傳遞任何型別的物件當做內容。</span><span class="sxs-lookup"><span data-stu-id="5170f-139">You can pass any type of object as the content.</span></span> <span data-ttu-id="5170f-140">例如，下列程式碼會建立包含浮點數的項目當做內容：</span><span class="sxs-lookup"><span data-stu-id="5170f-140">For example, the following code creates an element that contains a floating point number as content:</span></span>  
  
```csharp  
XElement n = new XElement("Cost", 324.50);  
Console.WriteLine(n);  
```  
  
 <span data-ttu-id="5170f-141">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-141">This example produces the following output:</span></span>  
  
```xml  
<Cost>324.5</Cost>  
```  
  
 <span data-ttu-id="5170f-142">浮點數為 Boxed 而且會傳入建構函式。</span><span class="sxs-lookup"><span data-stu-id="5170f-142">The floating point number is boxed and passed in to the constructor.</span></span> <span data-ttu-id="5170f-143">Boxed 數字會轉換為字串，並當做項目的內容使用。</span><span class="sxs-lookup"><span data-stu-id="5170f-143">The boxed number is converted to a string and used as the content of the element.</span></span>  
  
### <a name="creating-an-xelement-with-a-child-element"></a><span data-ttu-id="5170f-144">建立包含子項目的 XElement</span><span class="sxs-lookup"><span data-stu-id="5170f-144">Creating an XElement with a child element</span></span>  
 <span data-ttu-id="5170f-145">如果您要針對內容引數傳遞 <xref:System.Xml.Linq.XElement> 類別的執行個體，建構函式會建立包含子項目的項目：</span><span class="sxs-lookup"><span data-stu-id="5170f-145">If you pass an instance of the <xref:System.Xml.Linq.XElement> class for the content argument, the constructor creates an element with a child element:</span></span>  
  
```csharp  
XElement shippingUnit = new XElement("ShippingUnit",  
    new XElement("Cost", 324.50)  
);  
Console.WriteLine(shippingUnit);  
```  
  
 <span data-ttu-id="5170f-146">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-146">This example produces the following output:</span></span>  
  
```xml  
<ShippingUnit>  
  <Cost>324.5</Cost>  
</ShippingUnit>  
```  
  
### <a name="creating-an-xelement-with-multiple-child-elements"></a><span data-ttu-id="5170f-147">建立包含多個子項目的 XElement</span><span class="sxs-lookup"><span data-stu-id="5170f-147">Creating an XElement with multiple child elements</span></span>  
 <span data-ttu-id="5170f-148">您可以針對內容傳入多個 <xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="5170f-148">You can pass in a number of <xref:System.Xml.Linq.XElement> objects for the content.</span></span> <span data-ttu-id="5170f-149">每個 <xref:System.Xml.Linq.XElement> 物件都會當做子項目包含在內。</span><span class="sxs-lookup"><span data-stu-id="5170f-149">Each of the <xref:System.Xml.Linq.XElement> objects is included as a child element.</span></span>  
  
```csharp  
XElement address = new XElement("Address",  
    new XElement("Street1", "123 Main St"),  
    new XElement("City", "Mercer Island"),  
    new XElement("State", "WA"),  
    new XElement("Postal", "68042")  
);  
Console.WriteLine(address);  
```  
  
 <span data-ttu-id="5170f-150">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-150">This example produces the following output:</span></span>  
  
```xml  
<Address>  
  <Street1>123 Main St</Street1>  
  <City>Mercer Island</City>  
  <State>WA</State>  
  <Postal>68042</Postal>  
</Address>  
```  
  
 <span data-ttu-id="5170f-151">藉由延伸以上的範例，您可以建立完整的 XML 樹狀結構，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5170f-151">By extending the above example, you can create an entire XML tree, as follows:</span></span>  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
Console.WriteLine(contacts);  
```  
  
 <span data-ttu-id="5170f-152">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-152">This example produces the following output:</span></span>  
  
```xml  
<Contacts>  
  <Contact>  
    <Name>Patrick Hines</Name>  
    <Phone>206-555-0144</Phone>  
    <Address>  
      <Street1>123 Main St</Street1>  
      <City>Mercer Island</City>  
      <State>WA</State>  
      <Postal>68042</Postal>  
    </Address>  
  </Contact>  
</Contacts>  
```  

### <a name="creating-an-xelement-with-an-xattribute"></a><span data-ttu-id="5170f-153">建立具有 XAttribute 的 XElement</span><span class="sxs-lookup"><span data-stu-id="5170f-153">Creating an XElement with an XAttribute</span></span>
 <span data-ttu-id="5170f-154">如果您針對內容引數傳遞 <xref:System.Xml.Linq.XAttribute> 類別的執行個體，建構函式會建立具有屬性的元素：</span><span class="sxs-lookup"><span data-stu-id="5170f-154">If you pass an instance of the <xref:System.Xml.Linq.XAttribute> class for the content argument, the constructor creates an element with an attribute:</span></span>

```csharp  
XElement phone = new XElement("Phone",  
    new XAttribute("Type", "Home"),  
    "555-555-5555");  
Console.WriteLine(phone);  
```  
  
 <span data-ttu-id="5170f-155">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-155">This example produces the following output:</span></span>  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>
```

### <a name="creating-an-empty-element"></a><span data-ttu-id="5170f-156">建立空項目</span><span class="sxs-lookup"><span data-stu-id="5170f-156">Creating an empty element</span></span>  
 <span data-ttu-id="5170f-157">若要建立空的 <xref:System.Xml.Linq.XElement>，您不用將任何內容傳遞到建構函式。</span><span class="sxs-lookup"><span data-stu-id="5170f-157">To create an empty <xref:System.Xml.Linq.XElement>, you do not pass any content to the constructor.</span></span> <span data-ttu-id="5170f-158">下列範例會建立空項目：</span><span class="sxs-lookup"><span data-stu-id="5170f-158">The following example creates an empty element:</span></span>  
  
```csharp  
XElement n = new XElement("Customer");  
Console.WriteLine(n);  
```  
  
 <span data-ttu-id="5170f-159">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5170f-159">This example produces the following output:</span></span>  
  
```xml  
<Customer />  
```  
  
### <a name="attaching-vs-cloning"></a><span data-ttu-id="5170f-160">附加與複製</span><span class="sxs-lookup"><span data-stu-id="5170f-160">Attaching vs. cloning</span></span>  
 <span data-ttu-id="5170f-161">如先前所述，加入 <xref:System.Xml.Linq.XNode> (包括 <xref:System.Xml.Linq.XElement>) 或 <xref:System.Xml.Linq.XAttribute> 物件時，如果新內容沒有父代，這些物件只會附加到 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="5170f-161">As mentioned previously, when adding <xref:System.Xml.Linq.XNode> (including <xref:System.Xml.Linq.XElement>) or <xref:System.Xml.Linq.XAttribute> objects, if the new content has no parent, the objects are simply attached to the XML tree.</span></span> <span data-ttu-id="5170f-162">如果新內容已經成為父代，或是其他 XML 樹狀的一部分，則會複製新內容，而且新複製的內容會附加到 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="5170f-162">If the new content already is parented and is part of another XML tree, the new content is cloned, and the newly cloned content is attached to the XML tree.</span></span>  

<span data-ttu-id="5170f-163">下列範例示範將成為父代的項目加入到樹狀結構時，以及將沒有父代的項目加入樹狀結構時的行為。</span><span class="sxs-lookup"><span data-stu-id="5170f-163">The following example demonstrates the behavior when you add a parented element to a tree, and when you add an element with no parent to a tree.</span></span>

```csharp  
// Create a tree with a child element.  
XElement xmlTree1 = new XElement("Root",  
    new XElement("Child1", 1)  
);  
  
// Create an element that is not parented.  
XElement child2 = new XElement("Child2", 2);  
  
// Create a tree and add Child1 and Child2 to it.  
XElement xmlTree2 = new XElement("Root",  
    xmlTree1.Element("Child1"),  
    child2  
);  
  
// Compare Child1 identity.  
Console.WriteLine("Child1 was {0}",  
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?  
    "attached" : "cloned");  
  
// Compare Child2 identity.  
Console.WriteLine("Child2 was {0}",  
    child2 == xmlTree2.Element("Child2") ?  
    "attached" : "cloned");  

// The example displays the following output:  
//    Child1 was cloned  
//    Child2 was attached  
```

## <a name="see-also"></a><span data-ttu-id="5170f-164">請參閱</span><span class="sxs-lookup"><span data-stu-id="5170f-164">See also</span></span>

- [<span data-ttu-id="5170f-165">建立 XML 樹狀結構 (C#)</span><span class="sxs-lookup"><span data-stu-id="5170f-165">Creating XML Trees (C#)</span></span>](./linq-to-xml-overview.md)

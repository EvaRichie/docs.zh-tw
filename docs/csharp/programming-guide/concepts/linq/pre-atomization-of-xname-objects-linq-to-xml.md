---
title: 預先不可部分完成 XName 物件 (LINQ to XML) (C#)
description: 瞭解 XName 物件的預先不可部分完成。 預先 atomizing 的物件可在建立會重複特定名稱的大型 XML 樹狀結構時，改善效能。
ms.date: 07/20/2015
ms.assetid: e84fbbe7-f072-4771-bfbb-059d18e1ad15
ms.openlocfilehash: 4d217f6c78dc5d83ce424fb3ba95785f2dac0b73
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302824"
---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-c"></a><span data-ttu-id="f2128-104">預先不可部分完成 XName 物件 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="f2128-104">Pre-Atomization of XName Objects (LINQ to XML) (C#)</span></span>
<span data-ttu-id="f2128-105">在 LINQ to XML 中，改善效能的其中一種方式就是預先不可部分完成 <xref:System.Xml.Linq.XName> 物件。</span><span class="sxs-lookup"><span data-stu-id="f2128-105">One way to improve performance in LINQ to XML is to pre-atomize <xref:System.Xml.Linq.XName> objects.</span></span> <span data-ttu-id="f2128-106">預先不可部分完成是表示，您先指派字串給 <xref:System.Xml.Linq.XName> 物件，然後再使用 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XAttribute> 類別 (Class) 的建構函式 (Constructor) 來建立 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f2128-106">Pre-atomization means that you assign a string to an <xref:System.Xml.Linq.XName> object before you create the XML tree by using the constructors of the <xref:System.Xml.Linq.XElement> and  <xref:System.Xml.Linq.XAttribute> classes.</span></span> <span data-ttu-id="f2128-107">接著，您會傳遞初始化的 <xref:System.Xml.Linq.XName> 物件，而非將字串傳遞至建構函式 (會使用隱含轉換，從字串轉換成 <xref:System.Xml.Linq.XName>)。</span><span class="sxs-lookup"><span data-stu-id="f2128-107">Then, instead of passing a string to the constructor, which would use the implicit conversion from string to <xref:System.Xml.Linq.XName>, you pass the initialized <xref:System.Xml.Linq.XName> object.</span></span>  
  
 <span data-ttu-id="f2128-108">當您建立重複特定名稱的大型 XML 樹狀結構時，這樣做可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="f2128-108">This improves performance when you create a large XML tree in which specific names are repeated.</span></span> <span data-ttu-id="f2128-109">若要這樣做，請在建構 XML 樹狀結構之前宣告並初始化 <xref:System.Xml.Linq.XName> 物件，然後使用 <xref:System.Xml.Linq.XName> 物件，而非指定項目和屬性名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="f2128-109">To do this, you declare and initialize <xref:System.Xml.Linq.XName> objects before you construct the XML tree, and then use the <xref:System.Xml.Linq.XName> objects instead of specifying strings for the element and attribute names.</span></span> <span data-ttu-id="f2128-110">如果您使用相同的名稱來建立大量項目 (或屬性)，這項技巧可能會大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="f2128-110">This technique can yield significant performance gains if you are creating a large number of elements (or attributes) with the same name.</span></span>  
  
 <span data-ttu-id="f2128-111">您應該使用自己的案例來測試預先不可部分完成，以便決定是否應該使用此作業。</span><span class="sxs-lookup"><span data-stu-id="f2128-111">You should test pre-atomization with your scenario to decide if you should use it.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f2128-112">範例</span><span class="sxs-lookup"><span data-stu-id="f2128-112">Example</span></span>  
 <span data-ttu-id="f2128-113">下列範例示範此作業。</span><span class="sxs-lookup"><span data-stu-id="f2128-113">The following example demonstrates this.</span></span>  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="f2128-114">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="f2128-114">This example produces the following output:</span></span>  
  
```xml  
<Root>  
  <Data ID="1">4,100,000</Data>  
  <Data ID="2">3,700,000</Data>  
  <Data ID="3">1,150,000</Data>  
</Root>  
```  
  
 <span data-ttu-id="f2128-115">下列範例顯示 XML 文件位於命名空間中的相同技巧：</span><span class="sxs-lookup"><span data-stu-id="f2128-115">The following example shows the same technique where the XML document is in a namespace:</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XName Root = aw + "Root";  
XName Data = aw + "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XAttribute(XNamespace.Xmlns + "aw", aw),  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="f2128-116">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="f2128-116">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Data ID="1">4,100,000</aw:Data>  
  <aw:Data ID="2">3,700,000</aw:Data>  
  <aw:Data ID="3">1,150,000</aw:Data>  
</aw:Root>  
```  
  
 <span data-ttu-id="f2128-117">下列範例更類似於您可能會在真實世界中遇到的狀況。</span><span class="sxs-lookup"><span data-stu-id="f2128-117">The following example is more similar to what you will likely encounter in the real world.</span></span> <span data-ttu-id="f2128-118">在此範例中，項目的內容是由查詢提供：</span><span class="sxs-lookup"><span data-stu-id="f2128-118">In this example, the content of the element is supplied by a query:</span></span>  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
DateTime t1 = DateTime.Now;  
XElement root = new XElement(Root,  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement(Data,  
        new XAttribute(ID, i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
 <span data-ttu-id="f2128-119">上一則範例的執行效能比下列範例要好，因為其名稱並非預先不可部分完成：</span><span class="sxs-lookup"><span data-stu-id="f2128-119">The previous example performs better than the following example, in which names are not pre-atomized:</span></span>  
  
```csharp  
DateTime t1 = DateTime.Now;  
XElement root = new XElement("Root",  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement("Data",  
        new XAttribute("ID", i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
## <a name="see-also"></a><span data-ttu-id="f2128-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f2128-120">See also</span></span>

- [<span data-ttu-id="f2128-121">不可部分完成的 XName 和 XNamespace 物件 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="f2128-121">Atomized XName and XNamespace Objects (LINQ to XML) (C#)</span></span>](./atomized-xname-and-xnamespace-objects-linq-to-xml.md)

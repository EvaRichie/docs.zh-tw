---
title: LINQ to XML 事件 (C#)
description: '將 c # 中的 LINQ to XML 事件新增至任何 XObject 的實例。 當修改該 XObject 的 XML 樹狀結構時，事件處理常式會接收事件。'
ms.date: 07/20/2015
ms.assetid: ce7de951-cba7-4870-9962-733eb01cd680
ms.openlocfilehash: 576b0a5d0472bddd66e01d3bef8f3affa1c9458b
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165422"
---
# <a name="linq-to-xml-events-c"></a><span data-ttu-id="38a36-104">LINQ to XML 事件 (C#)</span><span class="sxs-lookup"><span data-stu-id="38a36-104">LINQ to XML Events (C#)</span></span>
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="38a36-105">事件可讓您在 XML 樹狀結構有所更改時收到通知。</span><span class="sxs-lookup"><span data-stu-id="38a36-105">events enable you to be notified when an XML tree is altered.</span></span>  
  
 <span data-ttu-id="38a36-106">您可以將事件加入到任何 <xref:System.Xml.Linq.XObject> 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="38a36-106">You can add events to an instance of any <xref:System.Xml.Linq.XObject>.</span></span> <span data-ttu-id="38a36-107">接著，事件處理常式將會收到修改該 <xref:System.Xml.Linq.XObject> 及其任何子代的事件。</span><span class="sxs-lookup"><span data-stu-id="38a36-107">The event handler will then receive events for modifications to that <xref:System.Xml.Linq.XObject> and any of its descendants.</span></span> <span data-ttu-id="38a36-108">例如，您可以將事件處理常式加入到樹狀結構的根目錄，並從該事件處理常式處理樹狀結構的所有修改。</span><span class="sxs-lookup"><span data-stu-id="38a36-108">For example, you can add an event handler to the root of the tree, and handle all modifications to the tree from that event handler.</span></span>  
  
 <span data-ttu-id="38a36-109">如需 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 事件的範例，請參閱 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed>。</span><span class="sxs-lookup"><span data-stu-id="38a36-109">For examples of [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] events, see <xref:System.Xml.Linq.XObject.Changing> and <xref:System.Xml.Linq.XObject.Changed>.</span></span>  
  
## <a name="types-and-events"></a><span data-ttu-id="38a36-110">型別與事件</span><span class="sxs-lookup"><span data-stu-id="38a36-110">Types and Events</span></span>  
 <span data-ttu-id="38a36-111">使用事件時，您可以使用下列型別：</span><span class="sxs-lookup"><span data-stu-id="38a36-111">You use the following types when working with events:</span></span>  
  
|<span data-ttu-id="38a36-112">類型</span><span class="sxs-lookup"><span data-stu-id="38a36-112">Type</span></span>|<span data-ttu-id="38a36-113">說明</span><span class="sxs-lookup"><span data-stu-id="38a36-113">Description</span></span>|  
|----------|-----------------|  
|<xref:System.Xml.Linq.XObjectChange>|<span data-ttu-id="38a36-114">引發 <xref:System.Xml.Linq.XObject> 的事件時，指定事件型別。</span><span class="sxs-lookup"><span data-stu-id="38a36-114">Specifies the event type when an event is raised for an <xref:System.Xml.Linq.XObject>.</span></span>|  
|<xref:System.Xml.Linq.XObjectChangeEventArgs>|<span data-ttu-id="38a36-115">提供 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed> 事件的資料。</span><span class="sxs-lookup"><span data-stu-id="38a36-115">Provides data for the <xref:System.Xml.Linq.XObject.Changing> and <xref:System.Xml.Linq.XObject.Changed> events.</span></span>|  
  
 <span data-ttu-id="38a36-116">修改 XML 樹狀結構時，會引發下列事件：</span><span class="sxs-lookup"><span data-stu-id="38a36-116">The following events are raised when you modify an XML tree:</span></span>  
  
|<span data-ttu-id="38a36-117">事件</span><span class="sxs-lookup"><span data-stu-id="38a36-117">Event</span></span>|<span data-ttu-id="38a36-118">描述</span><span class="sxs-lookup"><span data-stu-id="38a36-118">Description</span></span>|  
|-----------|-----------------|  
|<xref:System.Xml.Linq.XObject.Changing>|<span data-ttu-id="38a36-119">只會在此 <xref:System.Xml.Linq.XObject> 或其任何子代即將變更前發生。</span><span class="sxs-lookup"><span data-stu-id="38a36-119">Occurs just before this <xref:System.Xml.Linq.XObject> or any of its descendants is going to change.</span></span>|  
|<xref:System.Xml.Linq.XObject.Changed>|<span data-ttu-id="38a36-120"><xref:System.Xml.Linq.XObject> 已變更時或其任何子代已變更時發生。</span><span class="sxs-lookup"><span data-stu-id="38a36-120">Occurs when an <xref:System.Xml.Linq.XObject> has changed or any of its descendants have changed.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="38a36-121">範例</span><span class="sxs-lookup"><span data-stu-id="38a36-121">Example</span></span>  
  
### <a name="description"></a><span data-ttu-id="38a36-122">描述</span><span class="sxs-lookup"><span data-stu-id="38a36-122">Description</span></span>  
 <span data-ttu-id="38a36-123">當您想要維護 XML 樹狀結構中的特定彙總資訊時，這些事件相當實用。</span><span class="sxs-lookup"><span data-stu-id="38a36-123">Events are useful when you want to maintain some aggregate information in an XML tree.</span></span> <span data-ttu-id="38a36-124">例如，您可能想要維護發票明細項目總計的發票總數。</span><span class="sxs-lookup"><span data-stu-id="38a36-124">For example, you may want maintain an invoice total that is the sum of the line items of the invoice.</span></span> <span data-ttu-id="38a36-125">此範例使用事件維護複雜項目 `Items` 下，所有子項目的總計。</span><span class="sxs-lookup"><span data-stu-id="38a36-125">This example uses events to maintain the total of all of the child elements under the complex element `Items`.</span></span>  
  
### <a name="code"></a><span data-ttu-id="38a36-126">程式碼</span><span class="sxs-lookup"><span data-stu-id="38a36-126">Code</span></span>  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Total", "0"),  
    new XElement("Items")  
);  
XElement total = root.Element("Total");  
XElement items = root.Element("Items");  
items.Changed += (object sender, XObjectChangeEventArgs cea) =>  
{  
    switch (cea.ObjectChange)  
    {  
        case XObjectChange.Add:  
            if (sender is XElement)  
                total.Value = ((int)total + (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total + (int)((XText)sender).Parent).ToString();  
            break;  
        case XObjectChange.Remove:  
            if (sender is XElement)  
                total.Value = ((int)total - (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total - Int32.Parse(((XText)sender).Value)).ToString();  
            break;  
    }  
    Console.WriteLine("Changed {0} {1}",  
      sender.GetType().ToString(), cea.ObjectChange.ToString());  
};  
items.SetElementValue("Item1", 25);  
items.SetElementValue("Item2", 50);  
items.SetElementValue("Item2", 75);  
items.SetElementValue("Item3", 133);  
items.SetElementValue("Item1", null);  
items.SetElementValue("Item4", 100);  
Console.WriteLine("Total:{0}", (int)total);  
Console.WriteLine(root);  
```  
  
### <a name="comments"></a><span data-ttu-id="38a36-127">註解</span><span class="sxs-lookup"><span data-stu-id="38a36-127">Comments</span></span>  
 <span data-ttu-id="38a36-128">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38a36-128">This code produces the following output:</span></span>  
  
```output  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XText Remove  
Changed System.Xml.Linq.XText Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Remove  
Changed System.Xml.Linq.XElement Add  
Total:308  
<Root>  
  <Total>308</Total>  
  <Items>  
    <Item2>75</Item2>  
    <Item3>133</Item3>  
    <Item4>100</Item4>  
  </Items>  
</Root>  
```  
  
---
title: 為 DOM 中的項目建立新屬性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
ms.openlocfilehash: 1cb37e47bedf955ea2c6f9faad628df2175fb703
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826023"
---
# <a name="creating-new-attributes-for-elements-in-the-dom"></a><span data-ttu-id="3a878-102">為 DOM 中的項目建立新屬性</span><span class="sxs-lookup"><span data-stu-id="3a878-102">Creating New Attributes for Elements in the DOM</span></span>

<span data-ttu-id="3a878-103">建立新屬性不同於建立其他的節點型別，因為屬性不是節點，而是項目節點的屬性且包含於與項目相關的 **XmlAttributeCollection** 中。</span><span class="sxs-lookup"><span data-stu-id="3a878-103">Creating new attributes is different than creating other node types, because attributes are not nodes, but are properties of an element node and are contained in an **XmlAttributeCollection** associated with the element.</span></span> <span data-ttu-id="3a878-104">有許多方法可以建立屬性並且將它附加於項目：</span><span class="sxs-lookup"><span data-stu-id="3a878-104">There are multiple ways to create an attribute and attach it to an element:</span></span>

- <span data-ttu-id="3a878-105">取得項目節點並且使用 **SetAttribute** 將屬性加入此項目的屬性集合。</span><span class="sxs-lookup"><span data-stu-id="3a878-105">Get the element node and use **SetAttribute** to add an attribute to the attribute collection of that element.</span></span>

- <span data-ttu-id="3a878-106">使用 **CreateAttribute** 方法建立 **XmlAttribute** 節點，取得項目節點，然後使用 **SetAttributeNode** 將節點加入此項目的屬性集合。</span><span class="sxs-lookup"><span data-stu-id="3a878-106">Create an **XmlAttribute** node using the **CreateAttribute** method, get the element node, then use **SetAttributeNode** to add the node to the attribute collection of that element.</span></span>

<span data-ttu-id="3a878-107">下列範例示範如何使用 **SetAttribute** 方法，將屬性新增至元素：</span><span class="sxs-lookup"><span data-stu-id="3a878-107">The following example shows how to add an attribute to an element using the **SetAttribute** method:</span></span>

```vb
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()

        Dim doc As New XmlDocument()
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _
                    "<title>Pride And Prejudice</title>" & _
                    "</book>")
        Dim root As XmlElement = doc.DocumentElement

        ' Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel")

        Console.WriteLine("Display the modified XML...")
        Console.WriteLine(doc.InnerXml)
    End Sub
End Class
```  
  
```csharp
using System;
using System.IO;
using System.Xml;

public class Sample
{
    public static void Main()
    {
        var doc = new XmlDocument();
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +
                    "<title>Pride And Prejudice</title>" +
                    "</book>");
        XmlElement root = doc.DocumentElement;

        // Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel");

        Console.WriteLine("Display the modified XML...");
        Console.WriteLine(doc.InnerXml);
    }
}
```

<span data-ttu-id="3a878-108">下列範例顯示使用 **CreateAttribute** 方法建立的新屬性。</span><span class="sxs-lookup"><span data-stu-id="3a878-108">The following example shows a new attribute being created using the **CreateAttribute** method.</span></span> <span data-ttu-id="3a878-109">接著它使用 **SetAttributeNode** 方法，顯示加入 **book** 項目之屬性集合的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a878-109">It then shows the attribute added to the attribute collection of the **book** element using the **SetAttributeNode** method.</span></span>

<span data-ttu-id="3a878-110">假設有下列的 XML：</span><span class="sxs-lookup"><span data-stu-id="3a878-110">Given the following XML:</span></span>
  
```xml
<book genre='novel' ISBN='1-861001-57-5'>
<title>Pride And Prejudice</title>
</book>
```

<span data-ttu-id="3a878-111">建立新屬性並指定其值：</span><span class="sxs-lookup"><span data-stu-id="3a878-111">create a new attribute and give it a value:</span></span>

```vb
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")
attr.Value = "WorldWide Publishing"
```

```csharp
XmlAttribute attr = doc.CreateAttribute("publisher");
attr.Value = "WorldWide Publishing";
```

<span data-ttu-id="3a878-112">將它附加於項目：</span><span class="sxs-lookup"><span data-stu-id="3a878-112">and attach it to the element:</span></span>

```vb
doc.DocumentElement.SetAttributeNode(attr)
```

```csharp
doc.DocumentElement.SetAttributeNode(attr);
```

<span data-ttu-id="3a878-113">**輸出**</span><span class="sxs-lookup"><span data-stu-id="3a878-113">**Output**</span></span>

```xml
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">
<title>Pride And Prejudice</title>
</book>
```

<span data-ttu-id="3a878-114">如需完整的程式碼範例，請參閱 <xref:System.Xml.XmlDocument.CreateAttribute%2A>。</span><span class="sxs-lookup"><span data-stu-id="3a878-114">The full code sample can be found at <xref:System.Xml.XmlDocument.CreateAttribute%2A>.</span></span>

<span data-ttu-id="3a878-115">您也可以建立 **XmlAttribute** 節點並且使用 **InsertBefore** 或 **InsertAfter** 方法將它置於集合的適當位置中。</span><span class="sxs-lookup"><span data-stu-id="3a878-115">You can also create an **XmlAttribute** node and use the **InsertBefore** or **InsertAfter** methods to place it in the appropriate position in the collection.</span></span> <span data-ttu-id="3a878-116">如果屬性集合中已經有相同名稱的屬性存在，那麼現有的 **XmlAttribute** 節點會從集合中移除，而且新 **XmlAttribute** 節點會插入。</span><span class="sxs-lookup"><span data-stu-id="3a878-116">If an attribute with the same name is already present in the attribute collection, the existing **XmlAttribute** node is removed from the collection and the new **XmlAttribute** node is inserted.</span></span> <span data-ttu-id="3a878-117">執行方法與 **SetAttribute** 方法相同。</span><span class="sxs-lookup"><span data-stu-id="3a878-117">This performs the same way as the **SetAttribute** method.</span></span> <span data-ttu-id="3a878-118">如同參數，這些方法會以現有節點作為參考點來執行 **InsertBefore** 與 **InsertAfter**。</span><span class="sxs-lookup"><span data-stu-id="3a878-118">These methods take, as a parameter, an existing node as a reference point to do the **InsertBefore** and **InsertAfter**.</span></span> <span data-ttu-id="3a878-119">若未提供可指出要在何處插入新節點的參考節點，根據預設，**InsertAfter** 方法會將新節點插入集合的開頭。</span><span class="sxs-lookup"><span data-stu-id="3a878-119">If you do not provide a reference node indicating where to insert the new node, the default for the **InsertAfter** method is to insert the new node at the beginning of the collection.</span></span> <span data-ttu-id="3a878-120">若未提供參考節點，根據預設，**InsertBefore** 的位置將是在集合的結尾。</span><span class="sxs-lookup"><span data-stu-id="3a878-120">The default position for the **InsertBefore**, if no reference node is provided, is at the end of the collection.</span></span>

<span data-ttu-id="3a878-121">如果您已建立屬性的 **XmlNamedNodeMap** ，您可以使用方法，依名稱加入屬性 <xref:System.Xml.XmlNamedNodeMap.SetNamedItem%2A> 。</span><span class="sxs-lookup"><span data-stu-id="3a878-121">If you created an **XmlNamedNodeMap** of attributes, you can add an attribute by name using the <xref:System.Xml.XmlNamedNodeMap.SetNamedItem%2A> method.</span></span> <span data-ttu-id="3a878-122">如需詳細資訊，請參閱 [NamedNodeMap 和 NodeList 中的節點集合](node-collections-in-namednodemaps-and-nodelists.md)。</span><span class="sxs-lookup"><span data-stu-id="3a878-122">For more information, see [Node Collections in NamedNodeMaps and NodeLists](node-collections-in-namednodemaps-and-nodelists.md).</span></span>

## <a name="default-attributes"></a><span data-ttu-id="3a878-123">預設屬性</span><span class="sxs-lookup"><span data-stu-id="3a878-123">Default attributes</span></span>

<span data-ttu-id="3a878-124">如果您建立了宣告要有預設屬性的項目，那麼具有預設值的新預設屬性會由 XML 文件物件模型 (DOM) 建立並且附加於項目。</span><span class="sxs-lookup"><span data-stu-id="3a878-124">If you create an element that is declared to have a default attribute, then a new default attribute with its default value is created by the XML Document Object Model (DOM) and attached to the element.</span></span> <span data-ttu-id="3a878-125">預設屬性的子節點也會在此時建立。</span><span class="sxs-lookup"><span data-stu-id="3a878-125">The child nodes of the default attribute are also created at this time.</span></span>

## <a name="attribute-child-nodes"></a><span data-ttu-id="3a878-126">屬性子節點</span><span class="sxs-lookup"><span data-stu-id="3a878-126">Attribute child nodes</span></span>

<span data-ttu-id="3a878-127">屬性節點的值會成為它的子節點。</span><span class="sxs-lookup"><span data-stu-id="3a878-127">The value of an attribute node becomes its child nodes.</span></span> <span data-ttu-id="3a878-128">有效的子節點只有兩種類型： **XmlText** 節點和 **XmlEntityReference** 節點。</span><span class="sxs-lookup"><span data-stu-id="3a878-128">There are only two types of valid child nodes: **XmlText** nodes and **XmlEntityReference** nodes.</span></span> <span data-ttu-id="3a878-129">這些子節點讓像 **FirstChild** 和 **LastChild** 的方法能夠將它們當成子節點處理。</span><span class="sxs-lookup"><span data-stu-id="3a878-129">These are child nodes in the sense that methods such as **FirstChild** and **LastChild** process them as child nodes.</span></span> <span data-ttu-id="3a878-130">這種擁有子節點的屬性的區別在嘗試移除屬性或屬性子節點時很重要。</span><span class="sxs-lookup"><span data-stu-id="3a878-130">This distinction of an attribute having child nodes is important when trying to remove attributes or attribute child nodes.</span></span> <span data-ttu-id="3a878-131">如需詳細資訊，請參閱[移除 DOM 中項目節點的屬性](removing-attributes-from-an-element-node-in-the-dom.md)。</span><span class="sxs-lookup"><span data-stu-id="3a878-131">For more information, see [Removing Attributes from an Element Node in the DOM](removing-attributes-from-an-element-node-in-the-dom.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3a878-132">請參閱</span><span class="sxs-lookup"><span data-stu-id="3a878-132">See also</span></span>

- [<span data-ttu-id="3a878-133">XML 文件物件模型 (DOM)</span><span class="sxs-lookup"><span data-stu-id="3a878-133">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)

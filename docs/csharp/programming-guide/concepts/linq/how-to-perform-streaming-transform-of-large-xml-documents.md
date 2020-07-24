---
title: '如何執行大型 XML 檔的串流轉換（c #）'
description: '瞭解如何在 c # 中執行文字到 XML 的資料流程轉換，以避免某些檔案使用過多記憶體。'
ms.date: 07/20/2015
ms.assetid: 5f16d1f8-5370-4b55-b0c8-e497df163037
ms.openlocfilehash: e1ab2866079b2244dc764271d7ba63173349e2f3
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104858"
---
# <a name="how-to-perform-streaming-transform-of-large-xml-documents-c"></a><span data-ttu-id="8a0ee-103">如何執行大型 XML 檔的串流轉換（c #）</span><span class="sxs-lookup"><span data-stu-id="8a0ee-103">How to perform streaming transform of large XML documents (C#)</span></span>
<span data-ttu-id="8a0ee-104">有時候您必須轉換大型 XML 檔案並撰寫您的應用程式，讓應用程式的記憶體使用量可以預測。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-104">Sometimes you have to transform large XML files, and write your application so that the memory footprint of the application is predictable.</span></span> <span data-ttu-id="8a0ee-105">如果您嘗試使用非常大的 XML 檔案填入 XML 樹狀結構，您的記憶體使用量將與檔案大小成正比 (也就是，變成過度)。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-105">If you try to populate an XML tree with a very large XML file, your memory usage will be proportional to the size of the file (that is, excessive).</span></span> <span data-ttu-id="8a0ee-106">因此，您應該改用資料流技術。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-106">Therefore, you should use a streaming technique instead.</span></span>  
  
 <span data-ttu-id="8a0ee-107">在您僅需要處理一次來源文件的情況下，最適合使用資料流技術，而且您可以用文件的順序處理項目。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-107">Streaming techniques are best applied in situations where you need to process the source document only once, and you can process the elements in document order.</span></span> <span data-ttu-id="8a0ee-108">特定的標準查詢運算子 (例如，<xref:System.Linq.Enumerable.OrderBy%2A>) 會反覆查看其來源、收集所有資料、排序這些資料，最後產生順序中的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-108">Certain standard query operators, such as <xref:System.Linq.Enumerable.OrderBy%2A>, iterate their source, collect all of the data, sort it, and then finally yield the first item in the sequence.</span></span> <span data-ttu-id="8a0ee-109">請注意，如果您在產生第一個項目前使用具體化其來源的查詢運算子，您將不會為應用程式保留小的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-109">Note that if you use a query operator that materializes its source before yielding the first item, you will not retain a small memory footprint for your application.</span></span>  
  
<span data-ttu-id="8a0ee-110">即使您使用[如何串流 xml 片段並存取標頭資訊（c #）](./how-to-stream-xml-fragments-with-access-to-header-information.md)中所述的技術，如果您嘗試組合包含已轉換之檔的 xml 樹狀結構，記憶體使用量將會太大。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-110">Even if you use the technique described in [How to stream XML fragments with access to header information (C#)](./how-to-stream-xml-fragments-with-access-to-header-information.md), if you try to assemble an XML tree that contains the transformed document, memory usage will be too great.</span></span>
  
 <span data-ttu-id="8a0ee-111">有兩個主要方法。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-111">There are two main approaches.</span></span> <span data-ttu-id="8a0ee-112">其中一個方法是使用 <xref:System.Xml.Linq.XStreamingElement> 的延緩處理特性。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-112">One approach is to use the deferred processing characteristics of <xref:System.Xml.Linq.XStreamingElement>.</span></span> <span data-ttu-id="8a0ee-113">另一個方法則是建立 <xref:System.Xml.XmlWriter>，然後使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的功能，將項目寫入到 <xref:System.Xml.XmlWriter> 中。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-113">Another approach is to create an <xref:System.Xml.XmlWriter>, and use the capabilities of [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] to write elements to an <xref:System.Xml.XmlWriter>.</span></span> <span data-ttu-id="8a0ee-114">這個主題會示範這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-114">This topic demonstrates both approaches.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8a0ee-115">範例</span><span class="sxs-lookup"><span data-stu-id="8a0ee-115">Example</span></span>  
 <span data-ttu-id="8a0ee-116">下列範例是以[如何串流 XML 片段並存取標頭資訊（c #）](./how-to-stream-xml-fragments-with-access-to-header-information.md)中的範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-116">The following example builds on the example in [How to stream XML fragments with access to header information (C#)](./how-to-stream-xml-fragments-with-access-to-header-information.md).</span></span>
  
 <span data-ttu-id="8a0ee-117">這個範例會使用 <xref:System.Xml.Linq.XStreamingElement> 的延後執行功能來串流輸出。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-117">This example uses the deferred execution capabilities of <xref:System.Xml.Linq.XStreamingElement> to stream the output.</span></span> <span data-ttu-id="8a0ee-118">此範例可以轉換非常大的文件，同時維護小的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-118">This example can transform a very large document while maintaining a small memory footprint.</span></span>  
  
 <span data-ttu-id="8a0ee-119">請注意，自訂座標軸 (`StreamCustomerItem`) 是特別撰寫的，讓它預備擁有 `Customer`、`Name` 和 `Item` 項目的文件，並預期這些項目將會與下列 Source.xml 文件的排列方式相同。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-119">Note that the custom axis (`StreamCustomerItem`) is specifically written so that it expects a document that has `Customer`, `Name`, and `Item` elements, and that those elements will be arranged as in the following Source.xml document.</span></span> <span data-ttu-id="8a0ee-120">不過，較為複雜的實作方法則用於剖析無效的文件。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-120">A more robust implementation, however, would be prepared to parse an invalid document.</span></span>  
  
 <span data-ttu-id="8a0ee-121">下列是來源文件 Source.xml：</span><span class="sxs-lookup"><span data-stu-id="8a0ee-121">The following is the source document, Source.xml:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null)  
                        {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XStreamingElement root = new XStreamingElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    root.Save("Test.xml");  
    Console.WriteLine(File.ReadAllText("Test.xml"));  
}  
```  
  
 <span data-ttu-id="8a0ee-122">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="8a0ee-122">This code produces the following output:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="example"></a><span data-ttu-id="8a0ee-123">範例</span><span class="sxs-lookup"><span data-stu-id="8a0ee-123">Example</span></span>  
<span data-ttu-id="8a0ee-124">下列範例也是以[如何串流 XML 片段並存取標頭資訊（c #）](./how-to-stream-xml-fragments-with-access-to-header-information.md)中的範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-124">The following example also builds on the example in [How to stream XML fragments with access to header information (C#)](./how-to-stream-xml-fragments-with-access-to-header-information.md).</span></span>
  
 <span data-ttu-id="8a0ee-125">此範例會使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的功能，將項目寫入到 <xref:System.Xml.XmlWriter> 中。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-125">This example uses the capability of [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] to write elements to an <xref:System.Xml.XmlWriter>.</span></span> <span data-ttu-id="8a0ee-126">此範例可以轉換非常大的文件，同時維護小的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-126">This example can transform a very large document while maintaining a small memory footprint.</span></span>  
  
 <span data-ttu-id="8a0ee-127">請注意，自訂座標軸 (`StreamCustomerItem`) 是特別撰寫的，讓它預備擁有 `Customer`、`Name` 和 `Item` 項目的文件，並預期這些項目將會與下列 Source.xml 文件的排列方式相同。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-127">Note that the custom axis (`StreamCustomerItem`) is specifically written so that it expects a document that has `Customer`, `Name`, and `Item` elements, and that those elements will be arranged as in the following Source.xml document.</span></span> <span data-ttu-id="8a0ee-128">不過，較為複雜的實作方法將會使用 XSD 驗證來源文件，或做為剖析無效文件的準備。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-128">A more robust implementation, however, would either validate the source document with an XSD, or would be prepared to parse an invalid document.</span></span>  
  
 <span data-ttu-id="8a0ee-129">此範例會使用相同的來源文件 Source.xml 做為本主題中的上一個範例。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-129">This example uses the same source document, Source.xml, as the previous example in this topic.</span></span> <span data-ttu-id="8a0ee-130">它也會產生完全相同的輸出。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-130">It also produces exactly the same output.</span></span>  
  
 <span data-ttu-id="8a0ee-131">使用 <xref:System.Xml.Linq.XStreamingElement> 串流輸出 XML 優於寫入 <xref:System.Xml.XmlWriter>。</span><span class="sxs-lookup"><span data-stu-id="8a0ee-131">Using <xref:System.Xml.Linq.XStreamingElement> for streaming the output XML is preferred over writing to an <xref:System.Xml.XmlWriter>.</span></span>  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    IEnumerable<XElement> srcTree =  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        );  
    XmlWriterSettings xws = new XmlWriterSettings();  
    xws.OmitXmlDeclaration = true;  
    xws.Indent = true;  
    using (XmlWriter xw = XmlWriter.Create("Output.xml", xws)) {  
        xw.WriteStartElement("Root");  
        foreach (XElement el in srcTree)  
            el.WriteTo(xw);  
        xw.WriteEndElement();  
    }  
  
    string str = File.ReadAllText("Output.xml");  
    Console.WriteLine(str);  
}  
```  
  
 <span data-ttu-id="8a0ee-132">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="8a0ee-132">This code produces the following output:</span></span>  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
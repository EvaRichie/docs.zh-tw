---
title: 鬆散型別延伸範例
ms.date: 03/30/2017
ms.assetid: 56ce265b-8163-4b85-98e7-7692a12c4357
ms.openlocfilehash: 5d3defacc4a0acee69e32667d0d9213320b3ccec
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202220"
---
# <a name="loosely-typed-extensions-sample"></a><span data-ttu-id="29bb8-102">鬆散型別延伸範例</span><span class="sxs-lookup"><span data-stu-id="29bb8-102">Loosely-Typed Extensions Sample</span></span>
<span data-ttu-id="29bb8-103">新聞訂閱物件模型對使用延伸資料 (即以新聞訂閱摘要 XML 表示法呈現，但是尚未經由像是 <xref:System.ServiceModel.Syndication.SyndicationFeed> 和 <xref:System.ServiceModel.Syndication.SyndicationItem> 等類別明確公開的資訊) 提供大量支援。</span><span class="sxs-lookup"><span data-stu-id="29bb8-103">The Syndication object model provides rich support for working with extension data—information that is present in a syndication feed's XML representation but not explicitly exposed by classes such as <xref:System.ServiceModel.Syndication.SyndicationFeed> and <xref:System.ServiceModel.Syndication.SyndicationItem>.</span></span> <span data-ttu-id="29bb8-104">這個範例說明使用延伸資料的基本技術。</span><span class="sxs-lookup"><span data-stu-id="29bb8-104">This sample illustrates the basic techniques for working with extension data.</span></span>  
  
 <span data-ttu-id="29bb8-105">基於示範用途，此範例會使用 <xref:System.ServiceModel.Syndication.SyndicationFeed> 類別。</span><span class="sxs-lookup"><span data-stu-id="29bb8-105">The sample uses the <xref:System.ServiceModel.Syndication.SyndicationFeed> class for the purposes of the example.</span></span> <span data-ttu-id="29bb8-106">不過在此範例中所示範的模式，可以與所有支援延伸資料的新聞訂閱類別一起使用：</span><span class="sxs-lookup"><span data-stu-id="29bb8-106">However, the patterns demonstrated in this sample can be used with all of the Syndication classes that support extension data:</span></span>  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
 <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
 <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
## <a name="sample-xml"></a><span data-ttu-id="29bb8-107">範例 XML</span><span class="sxs-lookup"><span data-stu-id="29bb8-107">Sample XML</span></span>  
 <span data-ttu-id="29bb8-108">對於參考，這個範例使用下列 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="29bb8-108">For reference, the following XML document is used in this sample.</span></span>  
  
```xml  
<?xml version="1.0" encoding="IBM437"?>  
<feed myAttribute="someValue" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text"></title>  
  <id>uuid:8f60c7b3-a3c0-4de7-a642-2165d77ce3c1;id=1</id>  
  <updated>2007-09-07T22:15:34Z</updated>  
  <simpleString xmlns="">hello, world!</simpleString>  
  <simpleString xmlns="">another simple string</simpleString>  
  <DataContractExtension xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.d  
atacontract.org/2004/07/Microsoft.Syndication.Samples">  
    <Key>X</Key>  
    <Value>4</Value>  
  </DataContractExtension>  
  <XmlSerializerExtension xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://ww  
w.w3.org/2001/XMLSchema" xmlns="">  
    <Key>Y</Key>  
    <Value>8</Value>  
  </XmlSerializerExtension>  
  <xElementExtension xmlns="">  
    <Key attr1="someValue">Z</Key>  
    <Value attr1="someValue">15</Value>  
  </xElementExtension>  
</feed>  
```  
  
 <span data-ttu-id="29bb8-109">這份文件包含下列延伸資料片段：</span><span class="sxs-lookup"><span data-stu-id="29bb8-109">This document contains the following pieces of extension data:</span></span>  
  
- <span data-ttu-id="29bb8-110">`myAttribute` 元素的 `<feed>` 屬性。</span><span class="sxs-lookup"><span data-stu-id="29bb8-110">The `myAttribute` attribute of the `<feed>` element.</span></span>  
  
- <span data-ttu-id="29bb8-111">`<simpleString>` 元素。</span><span class="sxs-lookup"><span data-stu-id="29bb8-111">`<simpleString>` element.</span></span>  
  
- <span data-ttu-id="29bb8-112">`<DataContractExtension>` 元素。</span><span class="sxs-lookup"><span data-stu-id="29bb8-112">`<DataContractExtension>` element.</span></span>  
  
- <span data-ttu-id="29bb8-113">`<XmlSerializerExtension>` 元素。</span><span class="sxs-lookup"><span data-stu-id="29bb8-113">`<XmlSerializerExtension>` element.</span></span>  
  
- <span data-ttu-id="29bb8-114">`<xElementExtension>` 元素。</span><span class="sxs-lookup"><span data-stu-id="29bb8-114">`<xElementExtension>` element.</span></span>  
  
## <a name="writing-extension-data"></a><span data-ttu-id="29bb8-115">撰寫延伸資料</span><span class="sxs-lookup"><span data-stu-id="29bb8-115">Writing Extension Data</span></span>  
 <span data-ttu-id="29bb8-116">將項目新增至 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 集合便可以建立屬性延申，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-116">Attribute extensions are created by adding entries to the <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> collection as shown in the following sample code.</span></span>  
  
```csharp  
//Attribute extensions are stored in a dictionary indexed by
// XmlQualifiedName  
feed.AttributeExtensions.Add(new XmlQualifiedName("myAttribute", ""), "someValue");  
```  
  
 <span data-ttu-id="29bb8-117">將項目新增至 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A> 集合便可以建立項目延伸。</span><span class="sxs-lookup"><span data-stu-id="29bb8-117">Element extensions are created by adding entries to the <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A> collection.</span></span> <span data-ttu-id="29bb8-118">這些延伸可以是像是字串、.NET Framework 物件的 XML 序列化 (Serialization) 或手動撰寫的 XML 節點等基本值。</span><span class="sxs-lookup"><span data-stu-id="29bb8-118">These extensions can by basic values such as strings, XML serializations of .NET Framework objects, or XML nodes coded by hand.</span></span>  
  
 <span data-ttu-id="29bb8-119">下列範例程式碼會建立名為 `simpleString` 的延伸項目。</span><span class="sxs-lookup"><span data-stu-id="29bb8-119">The following sample code creates an extension element named `simpleString`.</span></span>  
  
```csharp  
feed.ElementExtensions.Add("simpleString", "", "hello, world!");  
```  
  
 <span data-ttu-id="29bb8-120">這個元素的 XML 命名空間是空的命名空間（""），而其值是包含字串 "hello，world！" 的文位元組點。</span><span class="sxs-lookup"><span data-stu-id="29bb8-120">The XML namespace for this element is the empty namespace ("") and its value is a text node that contains the string "hello, world!".</span></span>  
  
 <span data-ttu-id="29bb8-121">建立由許多巢狀項目所組成之複雜項目延伸的其中一種方法，便是使用 .NET Framework API 進行序列化 (同時支援 和)，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-121">One way to create complex element extensions that consist of many nested elements is to use the .NET Framework APIs for serialization (both the <xref:System.Runtime.Serialization.DataContractSerializer> and the <xref:System.Xml.Serialization.XmlSerializer> are supported) as shown in the following examples.</span></span>  
  
```csharp  
feed.ElementExtensions.Add( new DataContractExtension() { Key = "X", Value = 4 } );  
feed.ElementExtensions.Add( new XmlSerializerExtension { Key = "Y", Value = 8 }, new XmlSerializer( typeof( XmlSerializerExtension ) ) );  
```  
  
 <span data-ttu-id="29bb8-122">在這個範例中，`DataContractExtension` 和 `XmlSerializerExtension` 是針對搭配序列化程式所撰寫的自訂型別。</span><span class="sxs-lookup"><span data-stu-id="29bb8-122">In this example, the `DataContractExtension` and `XmlSerializerExtension` are custom types written for use with a serializer.</span></span>  
  
 <span data-ttu-id="29bb8-123"><xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection> 類別也可以用來建立 <xref:System.Xml.XmlReader> 執行個體的項目延伸。</span><span class="sxs-lookup"><span data-stu-id="29bb8-123">The <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection> class can also be used to create element extensions from an <xref:System.Xml.XmlReader> instance.</span></span> <span data-ttu-id="29bb8-124">這樣便可以與像是 <xref:System.Xml.Linq.XElement> 的 XML 處理 API 輕鬆整合，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-124">This allows for easy integration with XML processing APIs such as <xref:System.Xml.Linq.XElement> as shown in the following sample code.</span></span>  
  
```csharp  
feed.ElementExtensions.Add(new XElement("xElementExtension",  
        new XElement("Key", new XAttribute("attr1", "someValue"), "Z"),  
        new XElement("Value", new XAttribute("attr1", "someValue"),
        "15")).CreateReader());  
```  
  
## <a name="reading-extension-data"></a><span data-ttu-id="29bb8-125">讀取延伸資料</span><span class="sxs-lookup"><span data-stu-id="29bb8-125">Reading Extension Data</span></span>  
 <span data-ttu-id="29bb8-126">在 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 集合中根據 <xref:System.Xml.XmlQualifiedName> 查閱屬性，便可取得該屬性延伸的值，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-126">The values for attribute extensions can be obtained by looking up the attribute in the <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> collection by its <xref:System.Xml.XmlQualifiedName> as shown in the following sample code.</span></span>  
  
```csharp  
Console.WriteLine( feed.AttributeExtensions[ new XmlQualifiedName( "myAttribute", "" )]);  
```  
  
 <span data-ttu-id="29bb8-127">項目延伸是使用 `ReadElementExtensions<T>` 方法來存取。</span><span class="sxs-lookup"><span data-stu-id="29bb8-127">Element extensions are accessed using the `ReadElementExtensions<T>` method.</span></span>  
  
```csharp  
foreach( string s in feed2.ElementExtensions.ReadElementExtensions<string>("simpleString", ""))  
{  
    Console.WriteLine(s);  
}  
  
foreach (DataContractExtension dce in feed2.ElementExtensions.ReadElementExtensions<DataContractExtension>("DataContractExtension",  
"http://schemas.datacontract.org/2004/07/SyndicationExtensions"))  
{  
    Console.WriteLine(dce.ToString());  
}  
  
foreach (XmlSerializerExtension xse in feed2.ElementExtensions.ReadElementExtensions<XmlSerializerExtension>("XmlSerializerExtension", "", new XmlSerializer(typeof(XmlSerializerExtension))))  
{  
    Console.WriteLine(xse.ToString());  
}  
```  
  
 <span data-ttu-id="29bb8-128">使用 `XmlReader` 方法，也可以取得位在個別項目延伸的 <xref:System.ServiceModel.Syndication.SyndicationElementExtension.GetReader>。</span><span class="sxs-lookup"><span data-stu-id="29bb8-128">It is also possible to obtain an `XmlReader` at individual element extensions by using the <xref:System.ServiceModel.Syndication.SyndicationElementExtension.GetReader> method.</span></span>  
  
```csharp  
foreach (SyndicationElementExtension extension in feed2.ElementExtensions.Where<SyndicationElementExtension>(x => x.OuterName == "xElementExtension"))  
{  
    XNode xelement = XElement.ReadFrom(extension.GetReader());  
    Console.WriteLine(xelement.ToString());  
}  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="29bb8-129">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="29bb8-129">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="29bb8-130">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="29bb8-130">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="29bb8-131">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-131">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="29bb8-132">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="29bb8-132">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="29bb8-133">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="29bb8-133">The samples may already be installed on your machine.</span></span> <span data-ttu-id="29bb8-134">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="29bb8-134">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="29bb8-135">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="29bb8-135">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="29bb8-136">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="29bb8-136">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Syndication\LooselyTypedExtensions`  
  
## <a name="see-also"></a><span data-ttu-id="29bb8-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="29bb8-137">See also</span></span>

- [<span data-ttu-id="29bb8-138">強型別延伸</span><span class="sxs-lookup"><span data-stu-id="29bb8-138">Strongly typed Extensions</span></span>](../../../../docs/framework/wcf/samples/strongly-typed-extensions-sample.md)
- [<span data-ttu-id="29bb8-139">WCF 新聞訂閱</span><span class="sxs-lookup"><span data-stu-id="29bb8-139">WCF Syndication</span></span>](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)

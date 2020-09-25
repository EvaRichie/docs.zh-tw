---
title: 在資料集中使用 XML
ms.date: 03/30/2017
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
ms.openlocfilehash: e133da727887271af3bc5330a5779df4af58a37e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201183"
---
# <a name="using-xml-in-a-dataset"></a><span data-ttu-id="84dd7-102">在資料集中使用 XML</span><span class="sxs-lookup"><span data-stu-id="84dd7-102">Using XML in a DataSet</span></span>

<span data-ttu-id="84dd7-103">透過 ADO.NET，您可以從 XML 資料流或文件填滿 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="84dd7-103">With ADO.NET you can fill a <xref:System.Data.DataSet> from an XML stream or document.</span></span> <span data-ttu-id="84dd7-104">您可以使用 XML 資料流或文件，為 <xref:System.Data.DataSet> 提供資料、結構描述資訊或同時提供這兩者。</span><span class="sxs-lookup"><span data-stu-id="84dd7-104">You can use the XML stream or document to supply to the <xref:System.Data.DataSet> either data, schema information, or both.</span></span> <span data-ttu-id="84dd7-105">由 XML 資料流或文件提供的資訊，可與 <xref:System.Data.DataSet> 中的現有資料或結構描述資訊結合。</span><span class="sxs-lookup"><span data-stu-id="84dd7-105">The information supplied from the XML stream or document can be combined with existing data or schema information already present in the <xref:System.Data.DataSet>.</span></span>  
  
 <span data-ttu-id="84dd7-106">ADO.NET 也可讓您建立 <xref:System.Data.DataSet> 的 XML 表示 (可具備或不具備其結構描述)，以便透過 HTTP 將 <xref:System.Data.DataSet> 傳輸給另一個應用程式或啟用 XML 的平台使用。</span><span class="sxs-lookup"><span data-stu-id="84dd7-106">ADO.NET also allows you to create an XML representation of a <xref:System.Data.DataSet>, with or without its schema, in order to transport the <xref:System.Data.DataSet> across HTTP for use by another application or XML-enabled platform.</span></span> <span data-ttu-id="84dd7-107">在 <xref:System.Data.DataSet> 的 XML 表示中，資料是以 XML 撰寫的；而結構描述如果是內嵌在表示中，則是以 XML 結構描述定義語言 (XSD) 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="84dd7-107">In an XML representation of a <xref:System.Data.DataSet>, the data is written in XML and the schema, if it is included inline in the representation, is written using the XML Schema definition language (XSD).</span></span> <span data-ttu-id="84dd7-108">XML 和 XML 結構描述可讓您用方便的格式將 <xref:System.Data.DataSet> 的內容傳輸給遠端用戶端，也可以從遠端用戶端傳出。</span><span class="sxs-lookup"><span data-stu-id="84dd7-108">XML and XML Schema provide a convenient format for transferring the contents of a <xref:System.Data.DataSet> to and from remote clients.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="84dd7-109">本節內容</span><span class="sxs-lookup"><span data-stu-id="84dd7-109">In This Section</span></span>  

 [<span data-ttu-id="84dd7-110">DiffGram</span><span class="sxs-lookup"><span data-stu-id="84dd7-110">DiffGrams</span></span>](diffgrams.md)  
 <span data-ttu-id="84dd7-111">提供 DiffGram 的詳細資訊，這是用來讀取和寫入 <xref:System.Data.DataSet> 內容的 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="84dd7-111">Provides details on the DiffGram, an XML format used to read and write the contents of a <xref:System.Data.DataSet>.</span></span>  
  
 [<span data-ttu-id="84dd7-112">從 XML 載入資料集</span><span class="sxs-lookup"><span data-stu-id="84dd7-112">Loading a DataSet from XML</span></span>](loading-a-dataset-from-xml.md)  
 <span data-ttu-id="84dd7-113">討論從 XML 文件載入 <xref:System.Data.DataSet> 內容時，需要考慮的不同選項。</span><span class="sxs-lookup"><span data-stu-id="84dd7-113">Discusses different options to consider when loading the contents of a <xref:System.Data.DataSet> from an XML document.</span></span>  
  
 [<span data-ttu-id="84dd7-114">將資料集內容當做 XML 資料寫入</span><span class="sxs-lookup"><span data-stu-id="84dd7-114">Writing DataSet Contents as XML Data</span></span>](writing-dataset-contents-as-xml-data.md)  
 <span data-ttu-id="84dd7-115">討論如何將 <xref:System.Data.DataSet> 的內容產生為 XML 資料，以及您可以使用的不同 XML 格式選項。</span><span class="sxs-lookup"><span data-stu-id="84dd7-115">Discusses how to generate the contents of a <xref:System.Data.DataSet> as XML data, and the different XML format options you can use.</span></span>  
  
 [<span data-ttu-id="84dd7-116">從 XML 載入資料集結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="84dd7-116">Loading DataSet Schema Information from XML</span></span>](loading-dataset-schema-information-from-xml.md)  
 <span data-ttu-id="84dd7-117">討論可從 XML 載入 <xref:System.Data.DataSet> 之結構描述的 <xref:System.Data.DataSet> 方法。</span><span class="sxs-lookup"><span data-stu-id="84dd7-117">Discusses the <xref:System.Data.DataSet> methods used to load the schema of a <xref:System.Data.DataSet> from XML.</span></span>  
  
 [<span data-ttu-id="84dd7-118">將資料集結構描述資訊當做 XSD 寫入</span><span class="sxs-lookup"><span data-stu-id="84dd7-118">Writing DataSet Schema Information as XSD</span></span>](writing-dataset-schema-information-as-xsd.md)  
 <span data-ttu-id="84dd7-119">討論 XML 結構描述的使用方式，以及如何從 <xref:System.Data.DataSet> 產生 XML 結構描述。</span><span class="sxs-lookup"><span data-stu-id="84dd7-119">Discusses the uses for an XML Schema and how to generate one from a <xref:System.Data.DataSet>.</span></span>  
  
 [<span data-ttu-id="84dd7-120">資料集和 XmlDataDocument 同步處理</span><span class="sxs-lookup"><span data-stu-id="84dd7-120">DataSet and XmlDataDocument Synchronization</span></span>](dataset-and-xmldatadocument-synchronization.md)  
 <span data-ttu-id="84dd7-121">討論 .NET Framework 中有哪些可用功能可同步存取單一資料集的關聯式和階層式檢閱，以及如何在 <xref:System.Data.DataSet> 與 <xref:System.Xml.XmlDataDocument> 之間建立同步關係。</span><span class="sxs-lookup"><span data-stu-id="84dd7-121">Discusses the capability available in the .NET Framework of synchronous access to both relational and hierarchical views of a single set of data, and shows how to create a synchronous relationship between a <xref:System.Data.DataSet> and an <xref:System.Xml.XmlDataDocument>.</span></span>  
  
 [<span data-ttu-id="84dd7-122">巢狀 DataRelation</span><span class="sxs-lookup"><span data-stu-id="84dd7-122">Nesting DataRelations</span></span>](nesting-datarelations.md)  
 <span data-ttu-id="84dd7-123">討論將 <xref:System.Data.DataRelation> 的內容表示為 XML 資料時，巢狀 <xref:System.Data.DataSet> 物件的重要性，並描述如何建立這些關聯性。</span><span class="sxs-lookup"><span data-stu-id="84dd7-123">Discusses the importance of nested <xref:System.Data.DataRelation> objects when representing the contents of a <xref:System.Data.DataSet> as XML data, and describes how to create them.</span></span>  
  
 [<span data-ttu-id="84dd7-124">從 XML 結構描述 (XSD) 衍生資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="84dd7-124">Deriving DataSet Relational Structure from XML Schema (XSD)</span></span>](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 <span data-ttu-id="84dd7-125">說明從 XML 結構描述中建立的 <xref:System.Data.DataSet> 之關聯式結構 (或結構描述)。</span><span class="sxs-lookup"><span data-stu-id="84dd7-125">Describes the relational structure, or schema, of a <xref:System.Data.DataSet> that is created from XML Schema.</span></span>  
  
 [<span data-ttu-id="84dd7-126">從 XML 推斷資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="84dd7-126">Inferring DataSet Relational Structure from XML</span></span>](inferring-dataset-relational-structure-from-xml.md)  
 <span data-ttu-id="84dd7-127">說明從 XML 項目推斷時所建立的 <xref:System.Data.DataSet> 關聯式結構或結構描述。</span><span class="sxs-lookup"><span data-stu-id="84dd7-127">Describes the resulting relational structure, or schema, of a <xref:System.Data.DataSet> that is created when inferred from XML elements.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="84dd7-128">相關章節</span><span class="sxs-lookup"><span data-stu-id="84dd7-128">Related Sections</span></span>  

 <span data-ttu-id="84dd7-129">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="84dd7-129">[ADO.NET Overview](../ado-net-overview.md)</span></span>  
 <span data-ttu-id="84dd7-130">說明 ADO.NET 的架構和元件，以及如何使用它們來存取現有資料來源和管理應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="84dd7-130">Describes the ADO.NET architecture and components, and how to use them to access existing data sources as well as to manage application data.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="84dd7-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84dd7-131">See also</span></span>

- [<span data-ttu-id="84dd7-132">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="84dd7-132">DataSets, DataTables, and DataViews</span></span>](index.md)
- <span data-ttu-id="84dd7-133">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="84dd7-133">[ADO.NET Overview](../ado-net-overview.md)</span></span>

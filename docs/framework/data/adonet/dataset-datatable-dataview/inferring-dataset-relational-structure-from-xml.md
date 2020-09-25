---
title: 從 XML 推斷資料集關聯式結構
ms.date: 03/30/2017
ms.assetid: cd2f41c6-6785-420e-aa43-3ceb0bdccdce
ms.openlocfilehash: fca50491120346dea3e09c82324225f2114380fc
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177575"
---
# <a name="inferring-dataset-relational-structure-from-xml"></a><span data-ttu-id="31493-102">從 XML 推斷資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="31493-102">Inferring DataSet Relational Structure from XML</span></span>

<span data-ttu-id="31493-103"><xref:System.Data.DataSet> 的關聯式結構或結構描述是由資料表、資料行、條件約束和關聯所組成。</span><span class="sxs-lookup"><span data-stu-id="31493-103">The relational structure, or schema, of a <xref:System.Data.DataSet> is made up of tables, columns, constraints, and relations.</span></span> <span data-ttu-id="31493-104">從 XML 載入 <xref:System.Data.DataSet> 時，可預先定義結構描述，也可從正在載入的 XML 中，明確或透過介面建立。</span><span class="sxs-lookup"><span data-stu-id="31493-104">When loading a <xref:System.Data.DataSet> from XML, the schema can be predefined, or it can be created, either explicitly or through inference, from the XML being loaded.</span></span> <span data-ttu-id="31493-105">如需從 xml 載入架構和內容的詳細資訊 <xref:System.Data.DataSet> ，請參閱從 [Xml 載入資料集](loading-a-dataset-from-xml.md) 和 [從 Xml 載入資料集架構資訊](loading-dataset-schema-information-from-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="31493-105">For more information about loading the schema and contents of a <xref:System.Data.DataSet> from XML, see [Loading a DataSet from XML](loading-a-dataset-from-xml.md) and [Loading DataSet Schema Information from XML](loading-dataset-schema-information-from-xml.md).</span></span>  
  
 <span data-ttu-id="31493-106">如果 <xref:System.Data.DataSet> 是從 xml 建立的架構，則慣用的方法是使用 Xml 架構定義語言 (xsd)  (來明確指定架構，如 [從 xml 架構衍生資料集關聯式結構 (xsd) ](deriving-dataset-relational-structure-from-xml-schema-xsd.md)) 或 xml 資料縮減 (XDR) 中所述。</span><span class="sxs-lookup"><span data-stu-id="31493-106">If the schema of a <xref:System.Data.DataSet> is being created from XML, the preferred method is to explicitly specify the schema using either the XML Schema definition language (XSD) (as described in [Deriving DataSet Relational Structure from XML Schema (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)) or the XML-Data Reduced (XDR).</span></span> <span data-ttu-id="31493-107">如果 XML 中沒有可用的 XML 結構描述或 XDR 結構描述，可從 XML 項目和屬性的結構推斷出 <xref:System.Data.DataSet> 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="31493-107">If no XML Schema or XDR schema is available in the XML, the schema of the <xref:System.Data.DataSet> can be inferred from the structure of the XML elements and attributes.</span></span>  
  
 <span data-ttu-id="31493-108">本節藉由顯示 XML 項目和屬性及其結構，以及產生的推斷 <xref:System.Data.DataSet> 結構描述，說明 <xref:System.Data.DataSet> 結構描述的推斷規則。</span><span class="sxs-lookup"><span data-stu-id="31493-108">This section describes the rules for <xref:System.Data.DataSet> schema inference by showing XML elements and attributes and their structure, and the resulting inferred <xref:System.Data.DataSet> schema.</span></span>  
  
 <span data-ttu-id="31493-109">推斷程序中並不需要包含 XML文件中的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="31493-109">Not all attributes present in an XML document should be included in the inference process.</span></span> <span data-ttu-id="31493-110">符合命名空間的屬性可包含對 XML 文件重要、但對 <xref:System.Data.DataSet> 結構描述不重要的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="31493-110">Namespace-qualified attributes can include metadata that is important for the XML document but not for the <xref:System.Data.DataSet> schema.</span></span> <span data-ttu-id="31493-111">您可以使用 <xref:System.Data.DataSet.InferXmlSchema%2A>，指定在推斷處理序中要忽略的命名空間。</span><span class="sxs-lookup"><span data-stu-id="31493-111">Using <xref:System.Data.DataSet.InferXmlSchema%2A>, you can specify namespaces to be ignored during the inference process.</span></span> <span data-ttu-id="31493-112">如需詳細資訊，請參閱 [從 XML 載入資料集架構資訊](loading-dataset-schema-information-from-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="31493-112">For more information, see [Loading DataSet Schema Information from XML](loading-dataset-schema-information-from-xml.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="31493-113">本節內容</span><span class="sxs-lookup"><span data-stu-id="31493-113">In This Section</span></span>  

 [<span data-ttu-id="31493-114">資料集結構描述推斷程序摘要</span><span class="sxs-lookup"><span data-stu-id="31493-114">Summary of the DataSet Schema Inference Process</span></span>](summary-of-the-dataset-schema-inference-process.md)  
 <span data-ttu-id="31493-115">提供進階摘要，說明從 XML 推斷 <xref:System.Data.DataSet> 結構描述的規則。</span><span class="sxs-lookup"><span data-stu-id="31493-115">Provides a high-level summary of the rules for inferring the schema of a <xref:System.Data.DataSet> from XML.</span></span>  
  
 [<span data-ttu-id="31493-116">推斷資料表</span><span class="sxs-lookup"><span data-stu-id="31493-116">Inferring Tables</span></span>](inferring-tables.md)  
 <span data-ttu-id="31493-117">說明被推斷為 <xref:System.Data.DataSet> 中資料表的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="31493-117">Describes the XML elements that are inferred as tables in a <xref:System.Data.DataSet>.</span></span>  
  
 [<span data-ttu-id="31493-118">推斷資料行</span><span class="sxs-lookup"><span data-stu-id="31493-118">Inferring Columns</span></span>](inferring-columns.md)  
 <span data-ttu-id="31493-119">說明被推斷為資料表資料行的 XML 項目和屬性。</span><span class="sxs-lookup"><span data-stu-id="31493-119">Describes the XML elements and attributes that are inferred as table columns.</span></span>  
  
 [<span data-ttu-id="31493-120">推斷關聯性</span><span class="sxs-lookup"><span data-stu-id="31493-120">Inferring Relationships</span></span>](inferring-relationships.md)  
 <span data-ttu-id="31493-121">說明針對巢狀推斷資料表建立的 <xref:System.Data.DataRelation> 和 <xref:System.Data.ForeignKeyConstraint> 物件。</span><span class="sxs-lookup"><span data-stu-id="31493-121">Describes the <xref:System.Data.DataRelation> and <xref:System.Data.ForeignKeyConstraint> objects created for nested, inferred tables.</span></span>  
  
 [<span data-ttu-id="31493-122">推斷項目文字</span><span class="sxs-lookup"><span data-stu-id="31493-122">Inferring Element Text</span></span>](inferring-element-text.md)  
 <span data-ttu-id="31493-123">說明建立為 XML 項目內文字的資料行，並說明 XML 項目中的文字何時會被忽略。</span><span class="sxs-lookup"><span data-stu-id="31493-123">Describes the columns that are created for text in XML elements, and explains when text in XML elements is ignored.</span></span>  
  
 [<span data-ttu-id="31493-124">推斷限制</span><span class="sxs-lookup"><span data-stu-id="31493-124">Inference Limitations</span></span>](inference-limitations.md)  
 <span data-ttu-id="31493-125">討論結構描述推論的限制。</span><span class="sxs-lookup"><span data-stu-id="31493-125">Discusses the limitations of schema inference.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="31493-126">相關章節</span><span class="sxs-lookup"><span data-stu-id="31493-126">Related Sections</span></span>  

 [<span data-ttu-id="31493-127">在資料集中使用 XML</span><span class="sxs-lookup"><span data-stu-id="31493-127">Using XML in a DataSet</span></span>](using-xml-in-a-dataset.md)  
 <span data-ttu-id="31493-128">說明 <xref:System.Data.DataSet> 物件如何與 XML 資料互動。</span><span class="sxs-lookup"><span data-stu-id="31493-128">Describes how the <xref:System.Data.DataSet> object interacts with XML data.</span></span>  
  
 [<span data-ttu-id="31493-129">從 XML 結構描述 (XSD) 衍生資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="31493-129">Deriving DataSet Relational Structure from XML Schema (XSD)</span></span>](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 <span data-ttu-id="31493-130">說明根據 XML 結構描述定義語言 (XSD) 結構描述所建立的 <xref:System.Data.DataSet> 關聯式結構 (或結構描述)。</span><span class="sxs-lookup"><span data-stu-id="31493-130">Describes the relational structure, or schema, of a <xref:System.Data.DataSet> that is created from XML Schema definition language (XSD) schema.</span></span>  
  
 <span data-ttu-id="31493-131">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="31493-131">[ADO.NET Overview](../ado-net-overview.md)</span></span>  
 <span data-ttu-id="31493-132">描述 ADO.NET 的架構和元件，以及如何使用它們來存取現有資料來源和管理應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="31493-132">Describes the ADO.NET architecture and components and how to use them to access existing data sources and manage application data.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="31493-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="31493-133">See also</span></span>

- <span data-ttu-id="31493-134">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="31493-134">[ADO.NET Overview](../ado-net-overview.md)</span></span>

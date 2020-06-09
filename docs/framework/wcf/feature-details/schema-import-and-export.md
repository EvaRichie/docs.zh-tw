---
title: 結構描述匯入和匯出
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, schema import and export
- XsdDataContractExporter class
- XsdDataContractImporter class
ms.assetid: 0da32b50-ccd9-463a-844c-7fe803d3bf44
ms.openlocfilehash: 942ade69d92d8a213f65a3a2e463b6924e2f986e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590211"
---
# <a name="schema-import-and-export"></a><span data-ttu-id="4a27c-102">結構描述匯入和匯出</span><span class="sxs-lookup"><span data-stu-id="4a27c-102">Schema Import and Export</span></span>
<span data-ttu-id="4a27c-103">Windows Communication Foundation （WCF）包含新的序列化引擎，也就是 <xref:System.Runtime.Serialization.DataContractSerializer> 。</span><span class="sxs-lookup"><span data-stu-id="4a27c-103">Windows Communication Foundation (WCF) includes a new serialization engine, the <xref:System.Runtime.Serialization.DataContractSerializer>.</span></span> <span data-ttu-id="4a27c-104">會在 `DataContractSerializer` .NET Framework 物件和 XML 之間轉譯（雙向）。</span><span class="sxs-lookup"><span data-stu-id="4a27c-104">The `DataContractSerializer` translates between .NET Framework objects and XML (in both directions).</span></span> <span data-ttu-id="4a27c-105">除了序列化程式本身之外，WCF 還包含關聯的架構匯入與架構匯出機制。</span><span class="sxs-lookup"><span data-stu-id="4a27c-105">In addition to the serializer itself, WCF includes associated schema import and schema export mechanisms.</span></span> <span data-ttu-id="4a27c-106">「架構」（ *Schema* ）是序列化程式所產生之 XML 形式的正式、精確且電腦可讀取的描述，或可存取的。</span><span class="sxs-lookup"><span data-stu-id="4a27c-106">*Schema* is a formal, precise, and machine-readable description of the shape of XML that the serializer produces or that the deserializer can access.</span></span> <span data-ttu-id="4a27c-107">WCF 會使用全球資訊網協會（W3C） XML 架構定義語言（XSD）做為其架構表示，這可與許多協力廠商平臺廣泛互通。</span><span class="sxs-lookup"><span data-stu-id="4a27c-107">WCF uses the World Wide Web Consortium (W3C) XML Schema definition language (XSD) as its schema representation, which is widely interoperable with numerous third-party platforms.</span></span>  
  
 <span data-ttu-id="4a27c-108">架構匯入元件 <xref:System.Runtime.Serialization.XsdDataContractImporter> 會採用 XSD 架構檔，並產生 .NET Framework 類別（通常是資料合約類別），使序列化的表單對應至指定的架構。</span><span class="sxs-lookup"><span data-stu-id="4a27c-108">The schema import component, <xref:System.Runtime.Serialization.XsdDataContractImporter>, takes an XSD schema document and generates .NET Framework classes (normally data contract classes) such that the serialized forms correspond to the given schema.</span></span>  
  
 <span data-ttu-id="4a27c-109">例如，下列結構描述片段：</span><span class="sxs-lookup"><span data-stu-id="4a27c-109">For example, the following schema fragment:</span></span>  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
 <span data-ttu-id="4a27c-110">會產生下列型別 (已因應提高可讀性而稍微簡化)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-110">generates the following type (simplified slightly for better readability).</span></span>  
  
 [!code-csharp[c_SchemaImportExport#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#1)]
 [!code-vb[c_SchemaImportExport#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#1)]  
  
 <span data-ttu-id="4a27c-111">請注意，產生的類型會遵循數個數據合約最佳做法（可在[最佳做法：資料合約版本控制](../best-practices-data-contract-versioning.md)中找到）：</span><span class="sxs-lookup"><span data-stu-id="4a27c-111">Note that the generated type follows several data contract best practices (found in [Best Practices: Data Contract Versioning](../best-practices-data-contract-versioning.md)):</span></span>  
  
- <span data-ttu-id="4a27c-112">此型別會實作 <xref:System.Runtime.Serialization.IExtensibleDataObject> 介面。</span><span class="sxs-lookup"><span data-stu-id="4a27c-112">The type implements the <xref:System.Runtime.Serialization.IExtensibleDataObject> interface.</span></span> <span data-ttu-id="4a27c-113">如需詳細資訊，請參閱[向前相容資料合約](forward-compatible-data-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-113">For more information, see [Forward-Compatible Data Contracts](forward-compatible-data-contracts.md).</span></span>  
  
- <span data-ttu-id="4a27c-114">資料成員會實作為包裝私用欄位的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="4a27c-114">Data members are implemented as public properties that wrap private fields.</span></span>  
  
- <span data-ttu-id="4a27c-115">此類別是部份類別，而且透過不需要修改產生之程式碼來新增項目。</span><span class="sxs-lookup"><span data-stu-id="4a27c-115">The class is a partial class, and additions can be made without modifying generated code.</span></span>  
  
 <span data-ttu-id="4a27c-116"><xref:System.Runtime.Serialization.XsdDataContractExporter> 讓您能夠進行相反的動作，也就是接受可使用 `DataContractSerializer` 序列化的型別，並產生 XSD 結構描述文件。</span><span class="sxs-lookup"><span data-stu-id="4a27c-116">The <xref:System.Runtime.Serialization.XsdDataContractExporter> enables you to do the reverse—take types that are serializable with the `DataContractSerializer` and generate an XSD Schema document.</span></span>  
  
## <a name="fidelity-is-not-guaranteed"></a><span data-ttu-id="4a27c-117">不保證精確度</span><span class="sxs-lookup"><span data-stu-id="4a27c-117">Fidelity Is Not Guaranteed</span></span>  
 <span data-ttu-id="4a27c-118">這個類別不保證結構描述或型別在來回行程中絕對保有完整的精確度 </span><span class="sxs-lookup"><span data-stu-id="4a27c-118">It is not guaranteed that schema or types make a round trip with total fidelity.</span></span> <span data-ttu-id="4a27c-119">（*來回行程*表示匯入架構以建立一組類別，並將結果匯出以再次建立架構）。可能不會傳回相同的架構。</span><span class="sxs-lookup"><span data-stu-id="4a27c-119">(A *round trip* means to import a schema to create a set of classes, and export the result to create a schema again.) The same schema may not be returned.</span></span> <span data-ttu-id="4a27c-120">反向進行此程序時也不能保證維持精確度 </span><span class="sxs-lookup"><span data-stu-id="4a27c-120">Reversing the process is also not guaranteed to preserve fidelity.</span></span> <span data-ttu-id="4a27c-121">(匯出型別以產生其結構描述，然後再將該型別匯入回來。</span><span class="sxs-lookup"><span data-stu-id="4a27c-121">(Export a type to generate its schema, and then import the type back.</span></span> <span data-ttu-id="4a27c-122">不太可能會傳回相同的型別)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-122">It is unlikely the same type is returned.)</span></span>  
  
## <a name="supported-types"></a><span data-ttu-id="4a27c-123">支援的型別</span><span class="sxs-lookup"><span data-stu-id="4a27c-123">Supported Types</span></span>  
 <span data-ttu-id="4a27c-124">資料合約模型只支援有限的 WC3 結構描述子集。</span><span class="sxs-lookup"><span data-stu-id="4a27c-124">The data contract model supports only a limited subset of the WC3 schema.</span></span> <span data-ttu-id="4a27c-125">不符合這個子集的任何結構描述，都會在匯入程序進行時造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a27c-125">Any schema that does not conform to this subset will cause an exception during the import process.</span></span> <span data-ttu-id="4a27c-126">例如，沒有任何方式能夠指定資料合約的成員應該要序列化為 XML 屬性。</span><span class="sxs-lookup"><span data-stu-id="4a27c-126">For example, there is no way to specify that a data member of a data contract should be serialized as an XML attribute.</span></span> <span data-ttu-id="4a27c-127">這樣一來，因為不可能以正確的 XML 規劃來產生資料合約，所以就不會支援需要使用 XML 屬性的結構描述，進而會在匯入期間造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a27c-127">Thus, schemas that require the use of XML attributes are not supported and will cause exceptions during import, because it is impossible to generate a data contract with the correct XML projection.</span></span>  
  
 <span data-ttu-id="4a27c-128">例如，下列結構描述片段無法使用預設的匯入設定來進行匯入。</span><span class="sxs-lookup"><span data-stu-id="4a27c-128">For example, the following schema fragment cannot be imported using the default import settings.</span></span>  
  
 [!code-xml[c_SchemaImportExport#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#9)]  
  
 <span data-ttu-id="4a27c-129">如需詳細資訊，請參閱[資料合約架構參考](data-contract-schema-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-129">For more information, see [Data Contract Schema Reference](data-contract-schema-reference.md).</span></span> <span data-ttu-id="4a27c-130">如果結構描述不符合資料合約規則，請使用不同的序列化引擎。</span><span class="sxs-lookup"><span data-stu-id="4a27c-130">If a schema does not conform to the data contract rules, use a different serialization engine.</span></span> <span data-ttu-id="4a27c-131">例如，<xref:System.Xml.Serialization.XmlSerializer> 會使用自己的個別結構描述匯入機制。</span><span class="sxs-lookup"><span data-stu-id="4a27c-131">For example, the <xref:System.Xml.Serialization.XmlSerializer> uses its own separate schema import mechanism.</span></span> <span data-ttu-id="4a27c-132">另外，還有一種可用來擴充受支援結構描述之範圍的特殊匯入模式。</span><span class="sxs-lookup"><span data-stu-id="4a27c-132">Also, there is a special import mode in which the range of supported schema is expanded.</span></span> <span data-ttu-id="4a27c-133">如需詳細資訊，請參閱關於 <xref:System.Xml.Serialization.IXmlSerializable> 在匯入架構中產生類型[以產生類別](importing-schema-to-generate-classes.md)一節。</span><span class="sxs-lookup"><span data-stu-id="4a27c-133">For more information, see the section about generating <xref:System.Xml.Serialization.IXmlSerializable> types in [Importing Schema to Generate Classes](importing-schema-to-generate-classes.md).</span></span>  
  
 <span data-ttu-id="4a27c-134">`XsdDataContractExporter`支援可以使用序列化的任何 .NET Framework 類型 `DataContractSerializer` 。</span><span class="sxs-lookup"><span data-stu-id="4a27c-134">The `XsdDataContractExporter` supports any .NET Framework types that can be serialized with the `DataContractSerializer`.</span></span> <span data-ttu-id="4a27c-135">如需詳細資訊，請參閱[資料合約序列化程式支援的類型](types-supported-by-the-data-contract-serializer.md)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-135">For more information, see [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md).</span></span> <span data-ttu-id="4a27c-136">請注意，使用 `XsdDataContractExporter` 產生的型別，通常是 `XsdDataContractImporter` 可使用的有效資料 (除非 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 是用於自訂結構描述)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-136">Note that schema generated using the `XsdDataContractExporter` is normally valid data that the `XsdDataContractImporter` can use (unless the <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> is used to customize the schema).</span></span>  
  
 <span data-ttu-id="4a27c-137">如需使用的詳細資訊 <xref:System.Runtime.Serialization.XsdDataContractImporter> ，請參閱匯[入架構以產生類別](importing-schema-to-generate-classes.md)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-137">For more information about using the <xref:System.Runtime.Serialization.XsdDataContractImporter>, see [Importing Schema to Generate Classes](importing-schema-to-generate-classes.md).</span></span>  
  
 <span data-ttu-id="4a27c-138">如需使用的詳細資訊 <xref:System.Runtime.Serialization.XsdDataContractExporter> ，請參閱[從類別匯出架構](exporting-schemas-from-classes.md)。</span><span class="sxs-lookup"><span data-stu-id="4a27c-138">For more information about using the <xref:System.Runtime.Serialization.XsdDataContractExporter>, see [Exporting Schemas from Classes](exporting-schemas-from-classes.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4a27c-139">請參閱</span><span class="sxs-lookup"><span data-stu-id="4a27c-139">See also</span></span>

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- <xref:System.Runtime.Serialization.XsdDataContractExporter>
- [<span data-ttu-id="4a27c-140">匯入結構描述以產生類別</span><span class="sxs-lookup"><span data-stu-id="4a27c-140">Importing Schema to Generate Classes</span></span>](importing-schema-to-generate-classes.md)
- [<span data-ttu-id="4a27c-141">從類別匯出結構描述</span><span class="sxs-lookup"><span data-stu-id="4a27c-141">Exporting Schemas from Classes</span></span>](exporting-schemas-from-classes.md)

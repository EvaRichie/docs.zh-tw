---
title: 使用 XmlSchemaSet 驗證 XML 結構描述 (XSD)
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 359b10eb-ec05-4cc6-ac96-c2b060afc4de
ms.openlocfilehash: 1729380180d4440ac107885a39eff706c7fc8e5c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290288"
---
# <a name="xml-schema-xsd-validation-with-xmlschemaset"></a><span data-ttu-id="95d64-102">使用 XmlSchemaSet 驗證 XML 架構（XSD）</span><span class="sxs-lookup"><span data-stu-id="95d64-102">XML schema (XSD) validation with XmlSchemaSet</span></span>

<span data-ttu-id="95d64-103">可以根據 <xref:System.Xml.Schema.XmlSchemaSet> 中的 XML 結構描述定義語言 (XSD) 結構描述來驗證 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="95d64-103">XML documents can be validated against an XML schema definition language (XSD) schema in an <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
## <a name="validate-xml-documents"></a><span data-ttu-id="95d64-104">驗證 XML 檔</span><span class="sxs-lookup"><span data-stu-id="95d64-104">Validate XML documents</span></span>  
 <span data-ttu-id="95d64-105">XML 文件是透過 <xref:System.Xml.XmlReader.Create%2A> 類別的 <xref:System.Xml.XmlReader> 方法來驗證的。</span><span class="sxs-lookup"><span data-stu-id="95d64-105">XML documents are validated by the <xref:System.Xml.XmlReader.Create%2A> method of the <xref:System.Xml.XmlReader> class.</span></span> <span data-ttu-id="95d64-106">若要驗證 XML 文件，請建構 <xref:System.Xml.XmlReaderSettings> 物件，該物件包含可用於驗證 XML 文件的 XML 結構描述定義語言 (XSD) 結構描述。</span><span class="sxs-lookup"><span data-stu-id="95d64-106">To validate an XML document, construct an <xref:System.Xml.XmlReaderSettings> object that contains an XML schema definition language (XSD) schema with which to validate the XML document.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="95d64-107"><xref:System.Xml.Schema> 命名空間包含的擴充方法可在使用 [LINQ to XML (C#)](../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md) 和 [LINQ to XML (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md) 時，輕鬆地針對 XSD 檔案驗證 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="95d64-107">The <xref:System.Xml.Schema> namespace contains extension methods that make it easy to validate an XML tree against an XSD file when using [LINQ to XML (C#)](../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md) and [LINQ to XML (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md).</span></span> <span data-ttu-id="95d64-108">如需有關使用 LINQ to XML 來驗證 XML 檔的詳細資訊，請參閱[如何使用 xsd 進行驗證（LINQ to XML）（c #）](../../../csharp/programming-guide/concepts/linq/how-to-validate-using-xsd-linq-to-xml.md)和[如何：使用 xsd 進行驗證（LINQ to XML）（Visual Basic）](../../../visual-basic/programming-guide/concepts/linq/how-to-validate-using-xsd-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="95d64-108">For more information on validating XML documents with LINQ to XML, see [How to validate using XSD (LINQ to XML) (C#)](../../../csharp/programming-guide/concepts/linq/how-to-validate-using-xsd-linq-to-xml.md) and [How to: Validate Using XSD (LINQ to XML) (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/how-to-validate-using-xsd-linq-to-xml.md).</span></span>
  
 <span data-ttu-id="95d64-109">可以將個別結構描述或一組結構描述 (當做 <xref:System.Xml.Schema.XmlSchemaSet>) 加入至 <xref:System.Xml.Schema.XmlSchemaSet>，其方式是將其中一個當做參數傳遞給 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 的 <xref:System.Xml.Schema.XmlSchemaSet> 方法。</span><span class="sxs-lookup"><span data-stu-id="95d64-109">An individual schema or a set of schemas (as an <xref:System.Xml.Schema.XmlSchemaSet>) can be added to an <xref:System.Xml.Schema.XmlSchemaSet> by passing either one as a parameter to the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method of <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="95d64-110">驗證檔時，檔的目標命名空間必須符合架構集中架構的目標命名空間。</span><span class="sxs-lookup"><span data-stu-id="95d64-110">When validating a document the target namespace of the document must match the target namespace of the schema in the schema set.</span></span>  
  
 <span data-ttu-id="95d64-111">下列是範例 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="95d64-111">The following is an example XML document.</span></span>  
  
 [!code-xml[XSDInference Examples #5](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xml#5)]  
  
 <span data-ttu-id="95d64-112">下列是驗證範例 XML 文件的結構描述。</span><span class="sxs-lookup"><span data-stu-id="95d64-112">The following is the schema that validates the example XML document.</span></span>  
  
 [!code-xml[XSDInference Examples #6](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xsd#6)]  
  
 <span data-ttu-id="95d64-113">在下面的程式碼範例中，會將以上結構描述加入至 <xref:System.Xml.XmlReaderSettings.Schemas%2A> 物件的 <xref:System.Xml.XmlReaderSettings> 屬性。</span><span class="sxs-lookup"><span data-stu-id="95d64-113">In the code example that follows, the schema above is added to the <xref:System.Xml.XmlReaderSettings.Schemas%2A> property of the <xref:System.Xml.XmlReaderSettings> object.</span></span> <span data-ttu-id="95d64-114">將 <xref:System.Xml.XmlReaderSettings> 物件當做參數，傳遞至驗證以上 XML 文件之 <xref:System.Xml.XmlReader.Create%2A> 物件的 <xref:System.Xml.XmlReader> 方法。</span><span class="sxs-lookup"><span data-stu-id="95d64-114">The <xref:System.Xml.XmlReaderSettings> object is passed as a parameter to the <xref:System.Xml.XmlReader.Create%2A> method of the <xref:System.Xml.XmlReader> object, which validates the XML document above.</span></span>  
  
 <span data-ttu-id="95d64-115"><xref:System.Xml.XmlReaderSettings.ValidationType%2A> 物件的 <xref:System.Xml.XmlReaderSettings> 屬性會設為 `Schema`，以透過 <xref:System.Xml.XmlReader.Create%2A> 物件的 <xref:System.Xml.XmlReader> 方法，來強制驗證 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="95d64-115">The <xref:System.Xml.XmlReaderSettings.ValidationType%2A> property of the <xref:System.Xml.XmlReaderSettings> object is set to `Schema` to enforce validation of the XML document by the <xref:System.Xml.XmlReader.Create%2A> method of the <xref:System.Xml.XmlReader> object.</span></span> <span data-ttu-id="95d64-116">將 <xref:System.Xml.Schema.ValidationEventHandler> 加入至 <xref:System.Xml.XmlReaderSettings> 物件，以處理在驗證 XML 文件及結構描述期間找到的錯誤所引發的任意 <xref:System.Xml.Schema.XmlSeverityType.Warning> 或 <xref:System.Xml.Schema.XmlSeverityType.Error> 事件。</span><span class="sxs-lookup"><span data-stu-id="95d64-116">A <xref:System.Xml.Schema.ValidationEventHandler> is added to the <xref:System.Xml.XmlReaderSettings> object to handle any <xref:System.Xml.Schema.XmlSeverityType.Warning> or <xref:System.Xml.Schema.XmlSeverityType.Error> events raised by errors found during the validation process of both the XML document and the schema.</span></span>  
  
 [!code-cpp[XmlSchemaSetOverall Example #1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaSetOverall Example/CPP/xmlschemasetexample.cpp#1)]
 [!code-csharp[XmlSchemaSetOverall Example #1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaSetOverall Example/CS/xmlschemasetexample.cs#1)]
 [!code-vb[XmlSchemaSetOverall Example #1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaSetOverall Example/VB/xmlschemasetexample.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="95d64-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="95d64-117">See also</span></span>

- [<span data-ttu-id="95d64-118">用於結構描述編譯的 XmlSchemaSet</span><span class="sxs-lookup"><span data-stu-id="95d64-118">XmlSchemaSet for Schema Compilation</span></span>](xmlschemaset-for-schema-compilation.md)
- [<span data-ttu-id="95d64-119">使用 XML 結構描述</span><span class="sxs-lookup"><span data-stu-id="95d64-119">Working with XML Schemas</span></span>](working-with-xml-schemas.md)

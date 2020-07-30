---
title: '如何使用 XSD 進行驗證（LINQ to XML）（c #）'
description: 瞭解如何根據 XML 架構定義語言（XSD）檔案來驗證 XML 樹狀結構。 請參閱程式碼範例，並查看其他資源。
ms.date: 07/20/2015
ms.assetid: 6a7f83a9-2d74-4c2b-8417-0a8595879516
ms.openlocfilehash: 3b4d2137d511efbe20e4d31ad27e4975d5444ec9
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302629"
---
# <a name="how-to-validate-using-xsd-linq-to-xml-c"></a><span data-ttu-id="38274-104">如何使用 XSD 進行驗證（LINQ to XML）（c #）</span><span class="sxs-lookup"><span data-stu-id="38274-104">How to validate using XSD (LINQ to XML) (C#)</span></span>
<span data-ttu-id="38274-105"><xref:System.Xml.Schema> 命名空間包含的擴充方法可針對 XML 結構描述定義語言 (XSD) 檔，簡化 XML 樹狀結構的驗證。</span><span class="sxs-lookup"><span data-stu-id="38274-105">The <xref:System.Xml.Schema> namespace contains extension methods that make it easy to validate an XML tree against an XML Schema Definition Language (XSD) file.</span></span> <span data-ttu-id="38274-106">如需詳細資訊，請參閱 <xref:System.Xml.Schema.Extensions.Validate%2A> 方法的文件。</span><span class="sxs-lookup"><span data-stu-id="38274-106">For more information, see the <xref:System.Xml.Schema.Extensions.Validate%2A> method documentation.</span></span>  
  
## <a name="example"></a><span data-ttu-id="38274-107">範例</span><span class="sxs-lookup"><span data-stu-id="38274-107">Example</span></span>  
 <span data-ttu-id="38274-108">下列範例會建立 <xref:System.Xml.Schema.XmlSchemaSet>，然後針對結構描述設定驗證兩個 <xref:System.Xml.Linq.XDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="38274-108">The following example creates an <xref:System.Xml.Schema.XmlSchemaSet>, then validates two <xref:System.Xml.Linq.XDocument> objects against the schema set.</span></span> <span data-ttu-id="38274-109">其中一個文件有效，另一個無效。</span><span class="sxs-lookup"><span data-stu-id="38274-109">One of the documents is valid, the other is not.</span></span>  
  
```csharp  
string xsdMarkup =  
    @"<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'>  
       <xsd:element name='Root'>  
        <xsd:complexType>  
         <xsd:sequence>  
          <xsd:element name='Child1' minOccurs='1' maxOccurs='1'/>  
          <xsd:element name='Child2' minOccurs='1' maxOccurs='1'/>  
         </xsd:sequence>  
        </xsd:complexType>  
       </xsd:element>  
      </xsd:schema>";  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", XmlReader.Create(new StringReader(xsdMarkup)));  
  
XDocument doc1 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child2", "content1")  
    )  
);  
  
XDocument doc2 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child3", "content1")  
    )  
);  
  
Console.WriteLine("Validating doc1");  
bool errors = false;  
doc1.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc1 {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
Console.WriteLine("Validating doc2");  
errors = false;  
doc2.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc2 {0}", errors ? "did not validate" : "validated");  
```  
  
 <span data-ttu-id="38274-110">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38274-110">This example produces the following output:</span></span>  
  
```output  
Validating doc1  
doc1 validated  
  
Validating doc2  
The element 'Root' has invalid child element 'Child3'. List of possible elements expected: 'Child2'.  
doc2 did not validate  
```  
  
## <a name="example"></a><span data-ttu-id="38274-111">範例</span><span class="sxs-lookup"><span data-stu-id="38274-111">Example</span></span>  
 <span data-ttu-id="38274-112">下列範例會根據[範例 XSD 檔：客戶和訂單](./sample-xsd-file-customers-and-orders1.md)中的結構描述，驗證[範例 XML 檔：客戶和訂單 (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md) 中的 XML 文件是否有效。</span><span class="sxs-lookup"><span data-stu-id="38274-112">The following example validates that the XML document from [Sample XML File: Customers and Orders (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md) is valid per the schema from [Sample XSD File: Customers and Orders](./sample-xsd-file-customers-and-orders1.md).</span></span> <span data-ttu-id="38274-113">接著，它會修改 XML 來源文件。</span><span class="sxs-lookup"><span data-stu-id="38274-113">It then modifies the source XML document.</span></span> <span data-ttu-id="38274-114">它會變更第一個客戶上的 `CustomerID` 屬性。</span><span class="sxs-lookup"><span data-stu-id="38274-114">It changes the `CustomerID` attribute on the first customer.</span></span> <span data-ttu-id="38274-115">變更後，這些訂單將會參考不存在的客戶，因此 XML 文件將不再有效。</span><span class="sxs-lookup"><span data-stu-id="38274-115">After the change, orders will then refer to a customer that does not exist, so the XML document will no longer validate.</span></span>  
  
 <span data-ttu-id="38274-116">此範例使用下列 XML 文件︰[範例 XML 檔：客戶和訂單 (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md)。</span><span class="sxs-lookup"><span data-stu-id="38274-116">This example uses the following XML document: [Sample XML File: Customers and Orders (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).</span></span>  
  
 <span data-ttu-id="38274-117">此範例使用下列 XSD 結構描述︰[範例 XSD 檔：客戶和訂單](./sample-xsd-file-customers-and-orders1.md)。</span><span class="sxs-lookup"><span data-stu-id="38274-117">This example uses the following XSD schema: [Sample XSD File: Customers and Orders](./sample-xsd-file-customers-and-orders1.md).</span></span>  
  
```csharp  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", "CustomersOrders.xsd");  
  
Console.WriteLine("Attempting to validate");  
XDocument custOrdDoc = XDocument.Load("CustomersOrders.xml");  
bool errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
// Modify the source document so that it will not validate.  
custOrdDoc.Root.Element("Orders").Element("Order").Element("CustomerID").Value = "AAAAA";  
Console.WriteLine("Attempting to validate after modification");  
errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
```  
  
 <span data-ttu-id="38274-118">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38274-118">This example produces the following output:</span></span>  
  
```output  
Attempting to validate  
custOrdDoc validated  
  
Attempting to validate after modification  
The key sequence 'AAAAA' in Keyref fails to refer to some key.  
custOrdDoc did not validate  
```  
  
## <a name="see-also"></a><span data-ttu-id="38274-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="38274-119">See also</span></span>

- <xref:System.Xml.Schema.Extensions.Validate%2A>
- [<span data-ttu-id="38274-120">建立 XML 樹狀結構 (C#)</span><span class="sxs-lookup"><span data-stu-id="38274-120">Creating XML Trees (C#)</span></span>](creating-xml-trees-linq-to-xml-2.md)

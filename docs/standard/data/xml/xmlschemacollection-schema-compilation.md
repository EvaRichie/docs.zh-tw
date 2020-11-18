---
title: XmlSchemaCollection 結構描述編譯
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 76f28770-7126-428f-9ed5-7b5ae8bad5ee
ms.openlocfilehash: 7e93331d106dc74878e4d211c4dc6458c37088a3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94819119"
---
# <a name="xmlschemacollection-schema-compilation"></a><span data-ttu-id="deac4-102">XmlSchemaCollection 結構描述編譯</span><span class="sxs-lookup"><span data-stu-id="deac4-102">XmlSchemaCollection Schema Compilation</span></span>
<span data-ttu-id="deac4-103">**XmlSchemaCollection** 是一種快取 (Cache) 或程式庫，您可在此儲存和驗證 XML 資料精簡 (XDR) 和 XML 結構描述定義語言 (XSD) 結構描述。</span><span class="sxs-lookup"><span data-stu-id="deac4-103">The **XmlSchemaCollection** is a cache or library where XML-Data Reduced (XDR) and XML Schema definition language (XSD) schemas can be stored and validated.</span></span> <span data-ttu-id="deac4-104">**XmlSchemaCollection** 會藉由在記憶體中快取結構描述，而不是從檔案或 URL 存取它們的方式來提升效能。</span><span class="sxs-lookup"><span data-stu-id="deac4-104">**XmlSchemaCollection** improves performance by caching schemas in memory instead of accessing them from a file or URL.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="deac4-105">雖然 **XmlSchemaCollection** 類別同時儲存了 XDR 結構描述和 XML 結構描述，但任何會使用或傳回 **XmlSchema** 物件的方法和屬性都只能支援 XML 結構描述。</span><span class="sxs-lookup"><span data-stu-id="deac4-105">Although the **XmlSchemaCollection** class stores both XDR schemas and XML Schemas, any method and property that takes or returns an **XmlSchema** object supports XML Schemas only.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="deac4-106"><xref:System.Xml.Schema.XmlSchemaCollection> 類別目前已過時，並已由 <xref:System.Xml.Schema.XmlSchemaSet> 類別取代。</span><span class="sxs-lookup"><span data-stu-id="deac4-106">The <xref:System.Xml.Schema.XmlSchemaCollection> class is now obsolete and has been replaced with the <xref:System.Xml.Schema.XmlSchemaSet> class.</span></span> <span data-ttu-id="deac4-107">如需有關 <xref:System.Xml.Schema.XmlSchemaSet> 類別的詳細資訊，請參閱[用於結構描述編譯的 XmlSchemaSet](xmlschemaset-for-schema-compilation.md)。</span><span class="sxs-lookup"><span data-stu-id="deac4-107">For more information about the <xref:System.Xml.Schema.XmlSchemaSet> class see, [XmlSchemaSet for Schema Compilation](xmlschemaset-for-schema-compilation.md).</span></span>  
  
## <a name="add-schemas-to-the-collection"></a><span data-ttu-id="deac4-108">將結構描述加入集合</span><span class="sxs-lookup"><span data-stu-id="deac4-108">Add Schemas to the Collection</span></span>  
 <span data-ttu-id="deac4-109">**XmlSchemaCollection** 的 **Add** 方法會將結構描述載入集合，這時結構描述會和命名空間 URI 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="deac4-109">Schemas are loaded to the collection using the **Add** method of **XmlSchemaCollection**, at which time the schema is associated with a namespace URI.</span></span> <span data-ttu-id="deac4-110">對 XML 結構描述來說，命名空間 URI 通常是結構描述的目標命名空間。</span><span class="sxs-lookup"><span data-stu-id="deac4-110">For XML Schemas, the namespace URI will typically be the target namespace for the schema.</span></span> <span data-ttu-id="deac4-111">對 XDR 結構描述來說，命名空間 URI 是當將結構描述加入集合時指定的命名空間。</span><span class="sxs-lookup"><span data-stu-id="deac4-111">For XDR schemas, the namespace URI is the namespace specified when the schema was added to the collection.</span></span>  
  
## <a name="check-for-a-schema-in-the-collection"></a><span data-ttu-id="deac4-112">檢查集合中的結構描述</span><span class="sxs-lookup"><span data-stu-id="deac4-112">Check for a Schema in the Collection</span></span>  
 <span data-ttu-id="deac4-113">您可使用 **Contains** 方法來檢查結構描述是否在集合中。</span><span class="sxs-lookup"><span data-stu-id="deac4-113">You can check to see if a schema is in the collection by using the **Contains** method.</span></span> <span data-ttu-id="deac4-114">**Contains** 方法會使用 **XmlSchema** 物件 (僅限 XML 結構描述) 或表示與結構描述相關的命名空間 URI 的字串 (用於 XML 結構描述和 XDR 結構描述)。</span><span class="sxs-lookup"><span data-stu-id="deac4-114">The **Contains** method takes either an **XmlSchema** object (for XML Schemas only) or a string representing the namespace URI associated with the schema (for XML Schemas and XDR schemas).</span></span>  
  
## <a name="retrieve-a-schema-from-the-collection"></a><span data-ttu-id="deac4-115">從集合擷取結構描述</span><span class="sxs-lookup"><span data-stu-id="deac4-115">Retrieve a Schema from the Collection</span></span>  
 <span data-ttu-id="deac4-116">您可使用 **Item** 屬性來從集合擷取結構描述。</span><span class="sxs-lookup"><span data-stu-id="deac4-116">You can retrieve a schema from the collection by using the **Item** property.</span></span> <span data-ttu-id="deac4-117">**Item** 屬性會使用表示與結構描述相關的命名空間 URI 的字串 (通常是它的目標命名空間)，並且傳回 **XmlSchema** 物件。</span><span class="sxs-lookup"><span data-stu-id="deac4-117">The **Item** property takes a string representing the namespace URI associated with the schema, typically its target namespace, and returns an **XmlSchema** object.</span></span> <span data-ttu-id="deac4-118">**Item** 屬性只適用於 XML 結構描述。</span><span class="sxs-lookup"><span data-stu-id="deac4-118">The **Item** property applies to XML Schemas only.</span></span> <span data-ttu-id="deac4-119">對 XDR 結構描述來說，傳回值永遠是 Null 參考，因為它們並沒有可用的物件模型。</span><span class="sxs-lookup"><span data-stu-id="deac4-119">The return value is always a null reference for XDR schemas because they do not have an object model available.</span></span>  
  
## <a name="validate-xml-documents-using-xmlschemacollection"></a><span data-ttu-id="deac4-120">使用 XmlSchemaCollection 驗證 XML 文件</span><span class="sxs-lookup"><span data-stu-id="deac4-120">Validate XML Documents Using XmlSchemaCollection</span></span>  
 <span data-ttu-id="deac4-121">您可以藉由建立 **XmlSchemaCollection** 物件、將您的結構描述加入至集合中，然後設定 **XmlValidatingReader** 上的 **Schemas** 屬性，將建立的 **XmlSchemaCollection** 指派給 **XmlValidatingReader**，就可以利用 **XmlSchemaCollection** 來驗證 XML 執行個體文件。</span><span class="sxs-lookup"><span data-stu-id="deac4-121">You can validate an XML instance document using an **XmlSchemaCollection** by creating the **XmlSchemaCollection** object, adding your schemas to the collection, and setting the **Schemas** property on the **XmlValidatingReader** to assign the created **XmlSchemaCollection** to the **XmlValidatingReader**.</span></span>  
  
### <a name="improved-performance"></a><span data-ttu-id="deac4-122">改良的效能</span><span class="sxs-lookup"><span data-stu-id="deac4-122">Improved Performance</span></span>  
 <span data-ttu-id="deac4-123">如果您要依照相同的結構描述驗證多個文件，建議您使用 **XmlSchemaCollection**，因為它能夠提供比在記憶體中快取結構描述更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="deac4-123">It is recommended, if you are validating more than one document against the same schema, that you use the **XmlSchemaCollection** because it provides better performance by caching schemas in memory.</span></span>  
  
 <span data-ttu-id="deac4-124">下列程式碼範例會建立 **XmlSchemaCollection** 物件、將結構描述加入集合中並設定 **Schemas** 屬性。</span><span class="sxs-lookup"><span data-stu-id="deac4-124">The following code example creates the **XmlSchemaCollection** object, adds schemas to the collection, and sets the **Schemas** property.</span></span>  
  
```vb  
Dim tr as XmlTextReader = new XmlTextReader("Books.xml")  
Dim vr as XmlValidatingReader = new XmlValidatingReader(tr)  
Dim xsc as XmlSchemaCollection = new XmlSchemaCollection  
xsc.Add("urn:bookstore-schema", "Books.xsd")  
vr.Schemas.Add(xsc)  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("Books.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
xsc.Add("urn:bookstore-schema", "Books.xsd");
vr.Schemas.Add(xsc);  
```  
  
## <a name="see-also"></a><span data-ttu-id="deac4-125">請參閱</span><span class="sxs-lookup"><span data-stu-id="deac4-125">See also</span></span>

- [<span data-ttu-id="deac4-126">使用 XmlSchemaCollection 的 XDR 驗證</span><span class="sxs-lookup"><span data-stu-id="deac4-126">XDR Validation with XmlSchemaCollection</span></span>](xdr-validation-with-xmlschemacollection.md)
- [<span data-ttu-id="deac4-127">使用 XmlSchemaCollection 進行 XML 結構描述 (XSD) 驗證</span><span class="sxs-lookup"><span data-stu-id="deac4-127">XML Schema (XSD) Validation with XmlSchemaCollection</span></span>](xml-schema-xsd-validation-with-xmlschemacollection.md)

---
title: XPath 查詢及命名空間
description: 瞭解 & 命名空間的 XPath 查詢。 XPath 查詢會知道 XML 檔中的命名空間 & 可以使用命名空間前置詞來限定元素 & 屬性名稱。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ef6402be-2f8e-4be2-8d3e-a80891cdef8b
ms.openlocfilehash: 74dbe6b84c8d9400790f763f811da5542c732892
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720876"
---
# <a name="xpath-queries-and-namespaces"></a><span data-ttu-id="1a70d-104">XPath 查詢及命名空間</span><span class="sxs-lookup"><span data-stu-id="1a70d-104">XPath Queries and Namespaces</span></span>

<span data-ttu-id="1a70d-105">XPath 查詢可辨識 XML文件中的命名空間，並可使用命名空間前置詞來限定項目及屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1a70d-105">XPath queries are aware of namespaces in an XML document and can use namespace prefixes to qualify element and attribute names.</span></span> <span data-ttu-id="1a70d-106">使用命名空間前置詞限定項目及屬性名稱，會將 XPath 查詢傳回的節點限制為那些只屬於特定命名空間的節點。</span><span class="sxs-lookup"><span data-stu-id="1a70d-106">Qualifying element and attribute names with a namespace prefix limits the nodes returned by an XPath query to only those nodes that belong to a specific namespace.</span></span>  
  
 <span data-ttu-id="1a70d-107">例如，如果前置詞 `books` 對應命名空間 `http://www.contoso.com/books`，則下列 XPath 查詢 `/books:books/books:book` 只會選取命名空間 `book` 中的那些 `http://www.contoso.com/books` 項目。</span><span class="sxs-lookup"><span data-stu-id="1a70d-107">For example if the prefix `books` maps to the namespace `http://www.contoso.com/books`, then the following XPath query `/books:books/books:book` selects only those `book` elements in the namespace `http://www.contoso.com/books`.</span></span>  
  
## <a name="the-xmlnamespacemanager"></a><span data-ttu-id="1a70d-108">XmlNamespaceManager</span><span class="sxs-lookup"><span data-stu-id="1a70d-108">The XmlNamespaceManager</span></span>  

 <span data-ttu-id="1a70d-109">若要在 XPath 查詢中使用命名空間，需使用要包含在該 XPath 查詢中的命名空間 URI 及前置詞，建構自 <xref:System.Xml.IXmlNamespaceResolver> 介面衍生的物件，如 <xref:System.Xml.XmlNamespaceManager> 類別。</span><span class="sxs-lookup"><span data-stu-id="1a70d-109">To use namespaces in an XPath query, an object derived from the <xref:System.Xml.IXmlNamespaceResolver> interface like the <xref:System.Xml.XmlNamespaceManager> class is constructed with the namespace URI and prefix to include in the XPath query.</span></span>  
  
 <span data-ttu-id="1a70d-110">可以透過下列每一種方式將 <xref:System.Xml.XmlNamespaceManager> 物件用於查詢中。</span><span class="sxs-lookup"><span data-stu-id="1a70d-110">The <xref:System.Xml.XmlNamespaceManager> object may be used in the query in each of the following ways.</span></span>  
  
- <span data-ttu-id="1a70d-111">可藉由使用 <xref:System.Xml.XmlNamespaceManager> 物件的 <xref:System.Xml.XPath.XPathExpression> 方法，使 <xref:System.Xml.XPath.XPathExpression.SetContext%2A> 物件與現有 <xref:System.Xml.XPath.XPathExpression> 物件產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1a70d-111">The <xref:System.Xml.XmlNamespaceManager> object is associated with an existing <xref:System.Xml.XPath.XPathExpression> object by using the <xref:System.Xml.XPath.XPathExpression.SetContext%2A> method of the <xref:System.Xml.XPath.XPathExpression> object.</span></span> <span data-ttu-id="1a70d-112">您也可使用靜態 <xref:System.Xml.XPath.XPathExpression> 方法編譯新的 <xref:System.Xml.XPath.XPathExpression.Compile%2A> 物件；該方法會採用表示 XPath 運算式的字串及 <xref:System.Xml.XmlNamespaceManager> 物件做為參數，並傳回新的 <xref:System.Xml.XPath.XPathExpression> 物件。</span><span class="sxs-lookup"><span data-stu-id="1a70d-112">You may also compile a new <xref:System.Xml.XPath.XPathExpression> object using the static <xref:System.Xml.XPath.XPathExpression.Compile%2A> method which takes a string representing the XPath expression and an <xref:System.Xml.XmlNamespaceManager> object as parameters and returns a new <xref:System.Xml.XPath.XPathExpression> object.</span></span>  
  
- <span data-ttu-id="1a70d-113"><xref:System.Xml.XmlNamespaceManager> 物件本身會做為參數，連同表示 XPath 運算式的字串一起傳遞至接受的 <xref:System.Xml.XPath.XPathNavigator> 類別方法。</span><span class="sxs-lookup"><span data-stu-id="1a70d-113">The <xref:System.Xml.XmlNamespaceManager> object itself is passed as a parameter to an accepting <xref:System.Xml.XPath.XPathNavigator> class method along with a string representing the XPath expression.</span></span>  
  
 <span data-ttu-id="1a70d-114">下列是 <xref:System.Xml.XPath.XPathNavigator> 類別的方法，其接受衍生自 <xref:System.Xml.IXmlNamespaceResolver> 介面的物件做為參數。</span><span class="sxs-lookup"><span data-stu-id="1a70d-114">The following are the methods of the <xref:System.Xml.XPath.XPathNavigator> class that accept an object derived from the <xref:System.Xml.IXmlNamespaceResolver> interface as a parameter.</span></span>  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
### <a name="the-default-namespace"></a><span data-ttu-id="1a70d-115">預設命名空間</span><span class="sxs-lookup"><span data-stu-id="1a70d-115">The Default Namespace</span></span>  

 <span data-ttu-id="1a70d-116">在下面的 XML 文件中，會使用具有空前置詞的預設命名空間來宣告 `http://www.contoso.com/books` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="1a70d-116">In the XML document that follows, the default namespace with an empty prefix is used to declare the `http://www.contoso.com/books` namespace.</span></span>  
  
```xml  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <author>Author Name</author>  
        <price>5.50</price>  
    </book>  
</books>  
```  
  
 <span data-ttu-id="1a70d-117">XPath 將空前置詞視為 `null` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="1a70d-117">XPath treats the empty prefix as the `null` namespace.</span></span> <span data-ttu-id="1a70d-118">換句話說，只有對應至命名空間的前置詞可用於 XPath 查詢。</span><span class="sxs-lookup"><span data-stu-id="1a70d-118">In other words, only prefixes mapped to namespaces can be used in XPath queries.</span></span> <span data-ttu-id="1a70d-119">這表示如果您要根據 XML 文件中的命名空間查詢，則即使它是預設命名空間，您也需要定義它的前置詞。</span><span class="sxs-lookup"><span data-stu-id="1a70d-119">This means that if you want to query against a namespace in an XML document, even if it is the default namespace, you need to define a prefix for it.</span></span>  
  
 <span data-ttu-id="1a70d-120">例如，如果不定義上述 XML 文件的前置詞，XPath 查詢 `/books/book` 就不會傳回任何結果。</span><span class="sxs-lookup"><span data-stu-id="1a70d-120">For example, without defining a prefix for the XML document above, the XPath query `/books/book` would not return any results.</span></span>  
  
 <span data-ttu-id="1a70d-121">如果在有些節點不在命名空間中，有些節點在預設命名空間中的狀況下查詢文件，則必須繫結前置詞以避免模糊不清的情況。</span><span class="sxs-lookup"><span data-stu-id="1a70d-121">A prefix must be bound to prevent ambiguity when querying documents with some nodes not in a namespace, and some in a default namespace.</span></span>  
  
 <span data-ttu-id="1a70d-122">下列程式碼定義預設命名空間的前置詞，並從 `book` 命名空間選取所有的 `http://www.contoso.com/books` 項目。</span><span class="sxs-lookup"><span data-stu-id="1a70d-122">The following code defines a prefix for the default namespace and selects all the `book` elements from the `http://www.contoso.com/books` namespace.</span></span>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim query As XPathExpression = navigator.Compile("/books:books/books:book")  
Dim manager As XmlNamespaceManager = New XmlNamespaceManager(navigator.NameTable)  
manager.AddNamespace("books", "http://www.contoso.com/books")  
query.SetContext(manager)  
Dim nodes As XPathNodeIterator = navigator.Select(query)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathExpression query = navigator.Compile("/books:books/books:book");  
XmlNamespaceManager manager = new XmlNamespaceManager(navigator.NameTable);  
manager.AddNamespace("books", "http://www.contoso.com/books");  
query.SetContext(manager);  
XPathNodeIterator nodes = navigator.Select(query);  
```  
  
## <a name="see-also"></a><span data-ttu-id="1a70d-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1a70d-123">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="1a70d-124">使用 XPath 資料模型處理 XML 資料</span><span class="sxs-lookup"><span data-stu-id="1a70d-124">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="1a70d-125">使用 XPathNavigator 選取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="1a70d-125">Select XML Data Using XPathNavigator</span></span>](select-xml-data-using-xpathnavigator.md)
- [<span data-ttu-id="1a70d-126">使用 XPathNavigator 評估 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="1a70d-126">Evaluate XPath Expressions using XPathNavigator</span></span>](evaluate-xpath-expressions-using-xpathnavigator.md)
- [<span data-ttu-id="1a70d-127">使用 XPathNavigator 比對節點</span><span class="sxs-lookup"><span data-stu-id="1a70d-127">Matching Nodes using XPathNavigator</span></span>](matching-nodes-using-xpathnavigator.md)
- [<span data-ttu-id="1a70d-128">在 XPath 查詢中辨識的節點型別</span><span class="sxs-lookup"><span data-stu-id="1a70d-128">Node Types Recognized with XPath Queries</span></span>](node-types-recognized-with-xpath-queries.md)
- [<span data-ttu-id="1a70d-129">編譯 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="1a70d-129">Compiled XPath Expressions</span></span>](compiled-xpath-expressions.md)

---
title: 管理 XML 文件中的命名空間
description: 瞭解如何管理 XML 檔中的命名空間。 XML 命名空間會將 XML 文件中的項目與屬性名稱連結到自訂和預定的 URI。
ms.date: 03/30/2017
ms.assetid: 682643fc-b848-4e42-8c0d-50deeaeb5f2a
ms.openlocfilehash: 120493de430c2372f3f71d1d1498ba880feda3d1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720148"
---
# <a name="managing-namespaces-in-an-xml-document"></a><span data-ttu-id="8ad93-104">管理 XML 文件中的命名空間</span><span class="sxs-lookup"><span data-stu-id="8ad93-104">Managing Namespaces in an XML Document</span></span>

<span data-ttu-id="8ad93-105">XML 命名空間會將 XML 文件中的項目與屬性名稱連結到自訂和預定的 URI。</span><span class="sxs-lookup"><span data-stu-id="8ad93-105">XML namespaces associate element and attribute names in an XML document with custom and predefined URIs.</span></span> <span data-ttu-id="8ad93-106">若要建立這些關聯，請為命名空間 URI 定義前置詞，並使用這些前置詞來限定 XML 資料中的元素與屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="8ad93-106">To create these associations, you define prefixes for namespace URIs, and use those prefixes to qualify element and attribute names in XML data.</span></span> <span data-ttu-id="8ad93-107">命名空間可用來避免元素和屬性名稱發生衝突，並讓相同名稱的元素和屬性以不同方式處理和驗證。</span><span class="sxs-lookup"><span data-stu-id="8ad93-107">Namespaces prevent element and attribute name collisions, and enable elements and attributes of the same name to be handled and validated differently.</span></span>  
  
<a name="declare"></a>

## <a name="declaring-namespaces"></a><span data-ttu-id="8ad93-108">宣告命名空間</span><span class="sxs-lookup"><span data-stu-id="8ad93-108">Declaring namespaces</span></span>  

 <span data-ttu-id="8ad93-109">若要在元素上宣告命名空間，請使用 `xmlns:` 屬性：</span><span class="sxs-lookup"><span data-stu-id="8ad93-109">To declare a namespace on an element, you use the `xmlns:` attribute:</span></span>  
  
 `xmlns:<name>=<"uri">`  
  
 <span data-ttu-id="8ad93-110">其中 `<name>` 是命名空間前置詞，而 `<"uri">` 則是識別命名空間的 URI。</span><span class="sxs-lookup"><span data-stu-id="8ad93-110">where `<name>` is the namespace prefix and `<"uri">` is the URI that identifies the namespace.</span></span> <span data-ttu-id="8ad93-111">在宣告前置詞之後，您可以用它來限定 XML 文件中的元素和屬性，並將其與命名空間 URI 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="8ad93-111">After you declare the prefix, you can use it to qualify elements and attributes in an XML document and associate them with the namespace URI.</span></span> <span data-ttu-id="8ad93-112">因為命名空間前置詞會用於整份文件，所以其長度應該短一點。</span><span class="sxs-lookup"><span data-stu-id="8ad93-112">Because the namespace prefix is used throughout a document, it should be short in length.</span></span>  
  
 <span data-ttu-id="8ad93-113">這個範例會定義兩個 `BOOK` 元素。</span><span class="sxs-lookup"><span data-stu-id="8ad93-113">This example defines two `BOOK` elements.</span></span> <span data-ttu-id="8ad93-114">第一個元素由前置詞 `mybook` 所限定，而第二個元素則由前置詞 `bb` 所限定。</span><span class="sxs-lookup"><span data-stu-id="8ad93-114">The first element is qualified by the prefix, `mybook`, and the second element is qualified by the prefix, `bb`.</span></span> <span data-ttu-id="8ad93-115">每個前置詞都與不同的命名空間 URI 相關：</span><span class="sxs-lookup"><span data-stu-id="8ad93-115">Each prefix is associated with a different namespace URI:</span></span>  
  
```xml  
<mybook:BOOK xmlns:mybook="http://www.contoso.com/books.dtd">  
<bb:BOOK xmlns:bb="urn:blueyonderairlines" />
</mybook>
```  
  
 <span data-ttu-id="8ad93-116">若要表示某元素是特定命名空間的一部分，請將命名空間前置詞加到其中。</span><span class="sxs-lookup"><span data-stu-id="8ad93-116">To signify that an element is a part of a particular namespace, add the namespace prefix to it.</span></span> <span data-ttu-id="8ad93-117">例如，如果 `Author` 元素屬於 `mybook` 命名空間，便會將它宣告為 `<mybook:Author>`。</span><span class="sxs-lookup"><span data-stu-id="8ad93-117">For example, if a `Author` element belongs to the `mybook` namespace, it is declared as `<mybook:Author>`.</span></span>  
  
<a name="scope"></a>

## <a name="declaration-scope"></a><span data-ttu-id="8ad93-118">宣告範圍</span><span class="sxs-lookup"><span data-stu-id="8ad93-118">Declaration scope</span></span>  

 <span data-ttu-id="8ad93-119">命名空間的有效範圍，是從宣告點至宣告該命名空間之元素的結尾。</span><span class="sxs-lookup"><span data-stu-id="8ad93-119">A namespace is effective from its point of declaration until the end of the element it was declared in.</span></span> <span data-ttu-id="8ad93-120">在此範例中，於 `BOOK` 元素中定義的命名空間並不適用於 `BOOK` 元素以外的元素，如 `Publisher` 元素：</span><span class="sxs-lookup"><span data-stu-id="8ad93-120">In this example, the namespace defined in the `BOOK` element doesn't apply to elements outside the `BOOK` element, such as the `Publisher` element:</span></span>  
  
```xml  
<Author>Joe Smith</Author>  
<BOOK xmlns:book="http://www.contoso.com">  
    <title>My Wonderful Day</title>  
      <price>$3.95</price>  
</BOOK>  
<Publisher>  
    <Name>MSPress</Name>  
</Publisher>  
```  
  
 <span data-ttu-id="8ad93-121">雖然命名空間必須先行宣告才能使用，但它不必出現在 XML 文件的最前面。</span><span class="sxs-lookup"><span data-stu-id="8ad93-121">A namespace must be declared before it can be used, but it doesn't have to appear at the top of the XML document.</span></span>  
  
 <span data-ttu-id="8ad93-122">當您在 XML 文件中使用多個命名空間時，您可以定義一個命名空間當做預設命名空間，以便建立更易讀取的文件。</span><span class="sxs-lookup"><span data-stu-id="8ad93-122">When you use multiple namespaces in an XML document, you can define one namespace as the default namespace to create a cleaner looking document.</span></span> <span data-ttu-id="8ad93-123">預設命名空間會在根元素中宣告，並且套用到文件中所有非限定的元素。</span><span class="sxs-lookup"><span data-stu-id="8ad93-123">The default namespace is declared in the root element and applies to all unqualified elements in the document.</span></span> <span data-ttu-id="8ad93-124">預設命名空間僅適用於元素，不適用於屬性。</span><span class="sxs-lookup"><span data-stu-id="8ad93-124">Default namespaces apply to elements only, not to attributes.</span></span>  
  
 <span data-ttu-id="8ad93-125">若要使用預設命名空間，請在元素的宣告中省略前置詞和冒號：</span><span class="sxs-lookup"><span data-stu-id="8ad93-125">To use the default namespace, omit the prefix and the colon from the declaration on the element:</span></span>  
  
```xml  
<BOOK xmlns="http://www.contoso.com/books.dtd">  
...
</BOOK>
```  
  
## <a name="managing-namespaces"></a><span data-ttu-id="8ad93-126">管理命名空間</span><span class="sxs-lookup"><span data-stu-id="8ad93-126">Managing namespaces</span></span>  

 <span data-ttu-id="8ad93-127"><xref:System.Xml.XmlNamespaceManager> 類別會保存命名空間 URI 和其前置詞的集合，並讓您從這個集合查詢、加入及移除命名空間。</span><span class="sxs-lookup"><span data-stu-id="8ad93-127">The <xref:System.Xml.XmlNamespaceManager> class stores a collection of namespace URIs and their prefixes, and lets you look up, add, and remove namespaces from this collection.</span></span> <span data-ttu-id="8ad93-128">某些內容中需要使用這個類別，才能改善 XML 處理效能。</span><span class="sxs-lookup"><span data-stu-id="8ad93-128">In certain contexts, this class is required for better XML processing performance.</span></span> <span data-ttu-id="8ad93-129">例如，<xref:System.Xml.Xsl.XsltContext> 類別會使用 <xref:System.Xml.XmlNamespaceManager>，以提供 XPath 支援。</span><span class="sxs-lookup"><span data-stu-id="8ad93-129">For example, the <xref:System.Xml.Xsl.XsltContext> class uses <xref:System.Xml.XmlNamespaceManager> for XPath support.</span></span>  
  
 <span data-ttu-id="8ad93-130">命名空間管理員不會在命名空間上執行任何驗證，而是會假設前置詞和命名空間已經過驗證並且符合 [W3C 命名空間](https://www.w3.org/TR/REC-xml-names/)規格。</span><span class="sxs-lookup"><span data-stu-id="8ad93-130">The namespace manager doesn't perform any validation on the namespaces, but assumes that prefixes and namespaces have already been verified and conform to the [W3C Namespaces](https://www.w3.org/TR/REC-xml-names/) specification.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8ad93-131">[C#](../../linq/linq-xml-overview.md) 和 [Visual Basic](../../linq/linq-xml-overview.md) 中的 LINQ TO XML 不會使用 <xref:System.Xml.XmlNamespaceManager> 管理命名空間。</span><span class="sxs-lookup"><span data-stu-id="8ad93-131">LINQ TO XML in [C#](../../linq/linq-xml-overview.md) and [Visual Basic](../../linq/linq-xml-overview.md) don't use <xref:System.Xml.XmlNamespaceManager> to manage namespaces.</span></span> <span data-ttu-id="8ad93-132">如需在使用 LINQ to XML 時管理命名空間的資訊，請參閱 LINQ 文件中的[處理 XML 命名空間 (C#)](../../linq/namespaces-overview.md) 和[處理 XML 命名空間 (Visual Basic)](../../linq/namespaces-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ad93-132">See [Working with XML Namespaces (C#)](../../linq/namespaces-overview.md) and [Working with XML Namespaces (Visual Basic)](../../linq/namespaces-overview.md) in the LINQ documentation for information about managing namespaces when using LINQ to XML.</span></span>  
  
 <span data-ttu-id="8ad93-133">以下是您可以使用 <xref:System.Xml.XmlNamespaceManager> 類別執行的一些管理和查詢工作。</span><span class="sxs-lookup"><span data-stu-id="8ad93-133">Here are some of the management and lookup tasks you can perform with the <xref:System.Xml.XmlNamespaceManager> class.</span></span> <span data-ttu-id="8ad93-134">如需詳細資訊和範例，請追蹤每個方法或屬性的參考頁面連結。</span><span class="sxs-lookup"><span data-stu-id="8ad93-134">For more information and examples, follow the links to the reference page for each method or property.</span></span>  
  
|<span data-ttu-id="8ad93-135">收件者</span><span class="sxs-lookup"><span data-stu-id="8ad93-135">To</span></span>|<span data-ttu-id="8ad93-136">用途</span><span class="sxs-lookup"><span data-stu-id="8ad93-136">Use</span></span>|  
|--------|---------|  
|<span data-ttu-id="8ad93-137">加入命名空間</span><span class="sxs-lookup"><span data-stu-id="8ad93-137">Add a namespace</span></span>|<span data-ttu-id="8ad93-138"><xref:System.Xml.XmlNamespaceManager.AddNamespace%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-138"><xref:System.Xml.XmlNamespaceManager.AddNamespace%2A> method</span></span>|  
|<span data-ttu-id="8ad93-139">移除命名空間</span><span class="sxs-lookup"><span data-stu-id="8ad93-139">Remove a namespace</span></span>|<span data-ttu-id="8ad93-140"><xref:System.Xml.XmlNamespaceManager.RemoveNamespace%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-140"><xref:System.Xml.XmlNamespaceManager.RemoveNamespace%2A> method</span></span>|  
|<span data-ttu-id="8ad93-141">尋找預設命名空間的 URI</span><span class="sxs-lookup"><span data-stu-id="8ad93-141">Find the URI for the default namespace</span></span>|<span data-ttu-id="8ad93-142"><xref:System.Xml.XmlNamespaceManager.DefaultNamespace%2A> 屬性</span><span class="sxs-lookup"><span data-stu-id="8ad93-142"><xref:System.Xml.XmlNamespaceManager.DefaultNamespace%2A> property</span></span>|  
|<span data-ttu-id="8ad93-143">尋找命名空間前置詞的 URI</span><span class="sxs-lookup"><span data-stu-id="8ad93-143">Find the URI for a namespace prefix</span></span>|<span data-ttu-id="8ad93-144"><xref:System.Xml.XmlNamespaceManager.LookupNamespace%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-144"><xref:System.Xml.XmlNamespaceManager.LookupNamespace%2A> method</span></span>|  
|<span data-ttu-id="8ad93-145">尋找命名空間 URI 的前置詞</span><span class="sxs-lookup"><span data-stu-id="8ad93-145">Find the prefix for a namespace URI</span></span>|<span data-ttu-id="8ad93-146"><xref:System.Xml.XmlNamespaceManager.LookupPrefix%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-146"><xref:System.Xml.XmlNamespaceManager.LookupPrefix%2A> method</span></span>|  
|<span data-ttu-id="8ad93-147">取得目前節點中的命名空間清單</span><span class="sxs-lookup"><span data-stu-id="8ad93-147">Get a list of namespaces in the current node</span></span>|<span data-ttu-id="8ad93-148"><xref:System.Xml.XmlNamespaceManager.GetNamespacesInScope%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-148"><xref:System.Xml.XmlNamespaceManager.GetNamespacesInScope%2A> method</span></span>|  
|<span data-ttu-id="8ad93-149">設定命名空間的範圍</span><span class="sxs-lookup"><span data-stu-id="8ad93-149">Scope a namespace</span></span>|<span data-ttu-id="8ad93-150"><xref:System.Xml.XmlNamespaceManager.PushScope%2A> 和 <xref:System.Xml.XmlNamespaceManager.PopScope%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-150"><xref:System.Xml.XmlNamespaceManager.PushScope%2A> and <xref:System.Xml.XmlNamespaceManager.PopScope%2A> methods</span></span>|  
|<span data-ttu-id="8ad93-151">檢查前置詞是否定義於目前範圍中</span><span class="sxs-lookup"><span data-stu-id="8ad93-151">Check whether a prefix is defined in the current scope</span></span>|<span data-ttu-id="8ad93-152"><xref:System.Xml.XmlNamespaceManager.HasNamespace%2A> 方法</span><span class="sxs-lookup"><span data-stu-id="8ad93-152"><xref:System.Xml.XmlNamespaceManager.HasNamespace%2A> method</span></span>|  
|<span data-ttu-id="8ad93-153">取得用來查詢前置詞與 URI 的名稱資料表</span><span class="sxs-lookup"><span data-stu-id="8ad93-153">Get the name table used to look up prefixes and URIs</span></span>|<span data-ttu-id="8ad93-154"><xref:System.Xml.XmlNamespaceManager.NameTable%2A> 屬性</span><span class="sxs-lookup"><span data-stu-id="8ad93-154"><xref:System.Xml.XmlNamespaceManager.NameTable%2A> property</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="8ad93-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8ad93-155">See also</span></span>

- <xref:System.Xml.XmlNamespaceManager>
- [<span data-ttu-id="8ad93-156">XML 文件和資料</span><span class="sxs-lookup"><span data-stu-id="8ad93-156">XML Documents and Data</span></span>](index.md)

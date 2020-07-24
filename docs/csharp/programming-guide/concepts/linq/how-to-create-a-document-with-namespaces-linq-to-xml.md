---
title: '如何使用命名空間建立檔（c #）（LINQ to XML）'
description: '瞭解如何使用 XNamespace 物件，將命名空間與本機名稱結合，以在 c # 的 LINQ to XML 中建立具有命名空間的檔。'
ms.date: 07/20/2015
ms.assetid: 37e63c57-f86d-47ac-88a7-2c2d107def30
ms.openlocfilehash: 6472baefc73285af1c6dca0bfe7d874003940fc4
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103391"
---
# <a name="how-to-create-a-document-with-namespaces-c-linq-to-xml"></a><span data-ttu-id="718a8-103">如何使用命名空間建立檔（c #）（LINQ to XML）</span><span class="sxs-lookup"><span data-stu-id="718a8-103">How to create a document with namespaces (C#) (LINQ to XML)</span></span>
<span data-ttu-id="718a8-104">本主題顯示如何利用命名空間建立文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-104">This topic shows how to create documents with namespaces.</span></span>  
  
## <a name="example"></a><span data-ttu-id="718a8-105">範例</span><span class="sxs-lookup"><span data-stu-id="718a8-105">Example</span></span>  
 <span data-ttu-id="718a8-106">若要建立位於命名空間中的項目或屬性，您必須先宣告並初始化 <xref:System.Xml.Linq.XNamespace> 物件。</span><span class="sxs-lookup"><span data-stu-id="718a8-106">To create an element or an attribute that is in a namespace, you first declare and initialize an <xref:System.Xml.Linq.XNamespace> object.</span></span> <span data-ttu-id="718a8-107">然後，您可以使用加法運算子多載來結合命名空間與本機名稱 (以字串表示)。</span><span class="sxs-lookup"><span data-stu-id="718a8-107">You then use the addition operator overload to combine the namespace with the local name, expressed as a string.</span></span>  
  
 <span data-ttu-id="718a8-108">下列範例會使用一個命名空間建立文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-108">The following example creates a document with one namespace.</span></span> <span data-ttu-id="718a8-109">根據預設，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會使用預設命名空間來序列化此文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-109">By default, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] serializes this document with a default namespace.</span></span>  
  
```csharp  
// Create an XML tree in a namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="718a8-110">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="718a8-110">This example produces the following output:</span></span>  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child>child content</Child>  
</Root>  
```  
  
## <a name="example"></a><span data-ttu-id="718a8-111">範例</span><span class="sxs-lookup"><span data-stu-id="718a8-111">Example</span></span>  
 <span data-ttu-id="718a8-112">下列範例會使用一個命名空間建立文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-112">The following example creates a document with one namespace.</span></span> <span data-ttu-id="718a8-113">該範例也會建立宣告具有命名空間前置詞之命名空間的屬性。</span><span class="sxs-lookup"><span data-stu-id="718a8-113">It also creates an attribute that declares the namespace with a namespace prefix.</span></span> <span data-ttu-id="718a8-114">若要建立宣告具有前置詞之命名空間的屬性，您可以建立屬性，其中屬性的名稱是命名空間前置詞，而這個名稱位於 <xref:System.Xml.Linq.XNamespace.Xmlns%2A> 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="718a8-114">To create an attribute that declares a namespace with a prefix, you create an attribute where the name of the attribute is the namespace prefix, and this name is in the <xref:System.Xml.Linq.XNamespace.Xmlns%2A> namespace.</span></span> <span data-ttu-id="718a8-115">這個屬性的值為命名空間的 URI。</span><span class="sxs-lookup"><span data-stu-id="718a8-115">The value of this attribute is the URI of the namespace.</span></span>  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="718a8-116">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="718a8-116">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="example"></a><span data-ttu-id="718a8-117">範例</span><span class="sxs-lookup"><span data-stu-id="718a8-117">Example</span></span>  
 <span data-ttu-id="718a8-118">下列範例顯示如何建立包含兩個命名空間的文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-118">The following example shows the creation of a document that contains two namespaces.</span></span> <span data-ttu-id="718a8-119">一個是預設命名空間。</span><span class="sxs-lookup"><span data-stu-id="718a8-119">One is the default namespace.</span></span> <span data-ttu-id="718a8-120">另一個是具有前置詞的命名空間。</span><span class="sxs-lookup"><span data-stu-id="718a8-120">Another is a namespace with a prefix.</span></span>  
  
 <span data-ttu-id="718a8-121">藉由將命名空間屬性包含到根項目中，系統會序列化命名空間，讓 `http://www.adventure-works.com` 成為預設命名空間，而 `www.fourthcoffee.com` 則利用 "fc" 的前置詞序列化。</span><span class="sxs-lookup"><span data-stu-id="718a8-121">By including namespace attributes in the root element, the namespaces are serialized so that `http://www.adventure-works.com` is the default namespace, and `www.fourthcoffee.com` is serialized with a prefix of "fc".</span></span> <span data-ttu-id="718a8-122">若要建立宣告預設命名空間的屬性，您可以建立名稱為 "xmlns"，而且沒有命名空間的屬性。</span><span class="sxs-lookup"><span data-stu-id="718a8-122">To create an attribute that declares a default namespace, you create an attribute with the name "xmlns", without a namespace.</span></span> <span data-ttu-id="718a8-123">屬性的值為預設的命名空間 URI。</span><span class="sxs-lookup"><span data-stu-id="718a8-123">The value of the attribute is the default namespace URI.</span></span>  
  
```csharp  
// The http://www.adventure-works.com namespace is forced to be the default namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute("xmlns", "http://www.adventure-works.com"),  
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="718a8-124">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="718a8-124">This example produces the following output:</span></span>  
  
```xml  
<Root xmlns="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <DifferentChild>other content</DifferentChild>  
  </fc:Child>  
  <Child2>c2 content</Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</Root>  
```  
  
## <a name="example"></a><span data-ttu-id="718a8-125">範例</span><span class="sxs-lookup"><span data-stu-id="718a8-125">Example</span></span>  
 <span data-ttu-id="718a8-126">下列範例會建立包含兩個命名空間 (兩者皆擁有命名空間前置詞) 的文件。</span><span class="sxs-lookup"><span data-stu-id="718a8-126">The following example creates a document that contains two namespaces, both with namespace prefixes.</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", aw.NamespaceName),  
    new XAttribute(XNamespace.Xmlns + "fc", fc.NamespaceName),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="718a8-127">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="718a8-127">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="example"></a><span data-ttu-id="718a8-128">範例</span><span class="sxs-lookup"><span data-stu-id="718a8-128">Example</span></span>  
 <span data-ttu-id="718a8-129">達到相同結果的另一個方法是，使用擴充名稱來代替宣告和建立 <xref:System.Xml.Linq.XNamespace> 物件。</span><span class="sxs-lookup"><span data-stu-id="718a8-129">Another way to accomplish the same result is to use expanded names instead of declaring and creating an <xref:System.Xml.Linq.XNamespace> object.</span></span>  
  
 <span data-ttu-id="718a8-130">這個方法會有效能隱含作用。</span><span class="sxs-lookup"><span data-stu-id="718a8-130">This approach has performance implications.</span></span> <span data-ttu-id="718a8-131">每次您將包含展開名稱的字串傳遞到 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 時，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 就必須剖析名稱、尋找不可部分完成的命名空間，然後尋找不可部分完成的名稱。</span><span class="sxs-lookup"><span data-stu-id="718a8-131">Each time you pass a string that contains an expanded name to [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] must parse the name, find the atomized namespace, and find the atomized name.</span></span> <span data-ttu-id="718a8-132">這個程序會使用 CPU 時間。</span><span class="sxs-lookup"><span data-stu-id="718a8-132">This process takes CPU time.</span></span> <span data-ttu-id="718a8-133">如果效能對您很重要，您可能會想要明確宣告並使用 <xref:System.Xml.Linq.XNamespace> 物件。</span><span class="sxs-lookup"><span data-stu-id="718a8-133">If performance is important, you might want to declare and use an <xref:System.Xml.Linq.XNamespace> object explicitly.</span></span>  
  
 <span data-ttu-id="718a8-134">如果效能是很重要的問題，請參閱[預先同質化 XName 物件 (LINQ to XML) (C#)](./pre-atomization-of-xname-objects-linq-to-xml.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="718a8-134">If performance is an important issue, see [Pre-Atomization of XName Objects (LINQ to XML) (C#)](./pre-atomization-of-xname-objects-linq-to-xml.md) for more information</span></span>  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XElement root = new XElement("{http://www.adventure-works.com}Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement("{http://www.adventure-works.com}Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="718a8-135">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="718a8-135">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="see-also"></a><span data-ttu-id="718a8-136">請參閱</span><span class="sxs-lookup"><span data-stu-id="718a8-136">See also</span></span>

- [<span data-ttu-id="718a8-137">命名空間概觀 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="718a8-137">Namespaces Overview (LINQ to XML) (C#)</span></span>](namespaces-overview-linq-to-xml.md)

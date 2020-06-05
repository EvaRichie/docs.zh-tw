---
title: 函式建構 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
ms.openlocfilehash: f42cd6f31134c5f4c7d6a75f38997b2be0c317f3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398060"
---
# <a name="functional-construction-linq-to-xml-visual-basic"></a><span data-ttu-id="808ed-102">功能結構（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="808ed-102">Functional Construction (LINQ to XML) (Visual Basic)</span></span>
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="808ed-103">提供一種強大的方式來建立 XML 元素，稱為「函數式建構」\*\*。</span><span class="sxs-lookup"><span data-stu-id="808ed-103">provides a powerful way to create XML elements called *functional construction*.</span></span> <span data-ttu-id="808ed-104">功能結構是在單一陳述式中建立 XML 樹狀結構的能力。</span><span class="sxs-lookup"><span data-stu-id="808ed-104">Functional construction is the ability to create an XML tree in a single statement.</span></span>  
  
 <span data-ttu-id="808ed-105">[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 程式介面有數種主要功能可以使用功能結構：</span><span class="sxs-lookup"><span data-stu-id="808ed-105">There are several key features of the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] programming interface that enable functional construction:</span></span>  
  
- <span data-ttu-id="808ed-106"><xref:System.Xml.Linq.XElement> 建構函式會針對內容採用各種引數類型。</span><span class="sxs-lookup"><span data-stu-id="808ed-106">The <xref:System.Xml.Linq.XElement> constructor takes various types of arguments for content.</span></span> <span data-ttu-id="808ed-107">例如，您可以傳遞變成子項目的其他 <xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="808ed-107">For example, you can pass another <xref:System.Xml.Linq.XElement> object, which becomes a child element.</span></span> <span data-ttu-id="808ed-108">您可以傳遞變成項目屬性的 <xref:System.Xml.Linq.XAttribute> 物件。</span><span class="sxs-lookup"><span data-stu-id="808ed-108">You can pass an <xref:System.Xml.Linq.XAttribute> object, which becomes an attribute of the element.</span></span> <span data-ttu-id="808ed-109">或者，您可以傳遞轉換成字串的其他類物件型，然後變成項目的文字內容。</span><span class="sxs-lookup"><span data-stu-id="808ed-109">Or you can pass any other type of object, which is converted to a string and becomes the text content of the element.</span></span>  
  
- <span data-ttu-id="808ed-110"><xref:System.Xml.Linq.XElement> 建構函式會採用 `params` 類型的 <xref:System.Object> 陣列，讓您可以將任何數目的物件傳遞到建構函式。</span><span class="sxs-lookup"><span data-stu-id="808ed-110">The <xref:System.Xml.Linq.XElement> constructor takes a `params` array of type <xref:System.Object>, so that you can pass any number of objects to the constructor.</span></span> <span data-ttu-id="808ed-111">這可讓您建立包含複雜內容的項目。</span><span class="sxs-lookup"><span data-stu-id="808ed-111">This enables you to create an element that has complex content.</span></span>  
  
- <span data-ttu-id="808ed-112">如果物件實作 <xref:System.Collections.Generic.IEnumerable%601>，系統列舉物件中的集合，並加入集合中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="808ed-112">If an object implements <xref:System.Collections.Generic.IEnumerable%601>, the collection in the object is enumerated, and all items in the collection are added.</span></span> <span data-ttu-id="808ed-113">如果集合包含 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute> 物件，系統會個別加入集合中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="808ed-113">If the collection contains <xref:System.Xml.Linq.XElement> or <xref:System.Xml.Linq.XAttribute> objects, each item in the collection is added separately.</span></span> <span data-ttu-id="808ed-114">這很重要，因為它可讓您將 LINQ 查詢的結果傳遞給此函式。</span><span class="sxs-lookup"><span data-stu-id="808ed-114">This is important because it lets you pass the results of a LINQ query to the constructor.</span></span>  
  
 <span data-ttu-id="808ed-115">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="808ed-115">The following is an example:</span></span>  
  
 <span data-ttu-id="808ed-116">這些功能可讓您使用 XML 常值來撰寫程式碼，以建立 XML 樹狀結構，以及撰寫在建立 XML 樹狀結構時使用 LINQ 查詢結果的程式碼：</span><span class="sxs-lookup"><span data-stu-id="808ed-116">These features enable you to write code using XML literals to create an XML tree, and also to write code that uses the results of LINQ queries when you create an XML tree:</span></span>  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 <span data-ttu-id="808ed-117">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="808ed-117">This example produces the following output:</span></span>  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a><span data-ttu-id="808ed-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="808ed-118">See also</span></span>

- [<span data-ttu-id="808ed-119">建立 XML 樹狀結構（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="808ed-119">Creating XML Trees (Visual Basic)</span></span>](creating-xml-trees.md)

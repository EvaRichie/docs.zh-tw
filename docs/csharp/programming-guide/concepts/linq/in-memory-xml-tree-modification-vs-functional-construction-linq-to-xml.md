---
title: '記憶體中的 XML 樹狀結構修改與功能結構（LINQ to XML）（c #）'
description: '這些範例會變更 XML 檔的形狀，方法是就地修改它，並使用 c # 中的 LINQ to XML 功能結構。'
ms.date: 07/20/2015
ms.assetid: b5afc31d-a325-4ec6-bf17-0ff90a20ffca
ms.openlocfilehash: 7a2e3d2ddcd452cf6a58e9d5cc886f3e8b8dd325
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165788"
---
# <a name="in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml-c"></a><span data-ttu-id="a2f22-103">記憶體中的 XML 樹狀結構修改與功能結構（LINQ to XML）（c #）</span><span class="sxs-lookup"><span data-stu-id="a2f22-103">In-Memory XML Tree Modification vs. Functional Construction (LINQ to XML) (C#)</span></span>
<span data-ttu-id="a2f22-104">就地修改 XML 樹狀結構是變更 XML 文件組織結構的傳統方式。</span><span class="sxs-lookup"><span data-stu-id="a2f22-104">Modifying an XML tree in place is a traditional approach to changing the shape of an XML document.</span></span> <span data-ttu-id="a2f22-105">一般應用程式會將文件載入到資料存放區，例如 DOM 或 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]；使用程式設計介面插入節點、刪除節點或變更節點的內容；然後將 XML 儲存到檔案或透過網路傳輸。</span><span class="sxs-lookup"><span data-stu-id="a2f22-105">A typical application loads a document into a data store such as DOM or [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]; uses a programming interface to insert nodes, delete nodes, or change the content of nodes; and then saves the XML to a file or transmits it over a network.</span></span>  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="a2f22-106">可啟用在許多案例中有用的其他方法：「函數式建構」\*\*。</span><span class="sxs-lookup"><span data-stu-id="a2f22-106">enables another approach that is useful in many scenarios: *functional construction*.</span></span> <span data-ttu-id="a2f22-107">功能結構會將修改資料視為轉換的問題，而不是資料存放區的詳細管理。</span><span class="sxs-lookup"><span data-stu-id="a2f22-107">Functional construction treats modifying data as a problem of transformation, rather than as detailed manipulation of a data store.</span></span> <span data-ttu-id="a2f22-108">如果您可以表示資料，並將其有效地從一個表單轉換到另一個表單，結果會與您取得一個資料存放區，然後以相同的方式管理該資料存放區取得其他組織結構相同。</span><span class="sxs-lookup"><span data-stu-id="a2f22-108">If you can take a representation of data and transform it efficiently from one form to another, the result is the same as if you took one data store and manipulated it in some way to take another shape.</span></span> <span data-ttu-id="a2f22-109">功能結構方法的關鍵在於將查詢結果傳遞到 <xref:System.Xml.Linq.XDocument> 和 <xref:System.Xml.Linq.XElement> 建構函式。</span><span class="sxs-lookup"><span data-stu-id="a2f22-109">A key to the functional construction approach is to pass the results of queries to <xref:System.Xml.Linq.XDocument> and <xref:System.Xml.Linq.XElement> constructors.</span></span>  
  
 <span data-ttu-id="a2f22-110">在許多情況下，您可以用管理資料存放區的少數時間撰寫轉換程式碼，而且該程式碼更穩定、更容易維護。</span><span class="sxs-lookup"><span data-stu-id="a2f22-110">In many cases you can write the transformational code in a fraction of the time that it would take to manipulate the data store, and that code is more robust and easier to maintain.</span></span> <span data-ttu-id="a2f22-111">在這些情況下，即使轉換方法可以取得更大的處理能力，這都是更有效的修改資料方式。</span><span class="sxs-lookup"><span data-stu-id="a2f22-111">In these cases, even though the transformational approach can take more processing power, it is a more effective way to modify data.</span></span> <span data-ttu-id="a2f22-112">在許多情況下，如果開發人員熟悉功能性方法，產生的程式碼較容易了解。</span><span class="sxs-lookup"><span data-stu-id="a2f22-112">If a developer is familiar with the functional approach, the resulting code in many cases is easier to understand.</span></span> <span data-ttu-id="a2f22-113">尋找修改樹狀結構每個部分的程式碼非常容易。</span><span class="sxs-lookup"><span data-stu-id="a2f22-113">It is easy to find the code that modifies each part of the tree.</span></span>  
  
 <span data-ttu-id="a2f22-114">您就地修改 XML 樹狀結構的方法對於許多 DOM 程式設計人員而言更為熟悉，而使用功能性方法撰寫的程式碼對於還不了解該方法的開發人員而言，似乎比較不熟悉。</span><span class="sxs-lookup"><span data-stu-id="a2f22-114">The approach where you modify an XML tree in-place is more familiar to many DOM programmers, whereas code written using the functional approach might look unfamiliar to a developer who doesn't yet understand that approach.</span></span> <span data-ttu-id="a2f22-115">如果您必須針對大型 XML 樹狀結構進行小小的修改，您就地修改樹狀結構的方法在大部分的情況下，將會需要較少的 CPU 時間。</span><span class="sxs-lookup"><span data-stu-id="a2f22-115">If you have to only make a small modification to a large XML tree, the approach where you modify a tree in place in many cases will take less CPU time.</span></span>  
  
 <span data-ttu-id="a2f22-116">本主題提供利用兩種方法實作的範例。</span><span class="sxs-lookup"><span data-stu-id="a2f22-116">This topic provides an example that is implemented with both approaches.</span></span>  
  
## <a name="transforming-attributes-into-elements"></a><span data-ttu-id="a2f22-117">將屬性轉換為項目</span><span class="sxs-lookup"><span data-stu-id="a2f22-117">Transforming Attributes into Elements</span></span>  
 <span data-ttu-id="a2f22-118">針對這個範例，假設您想要修改下列簡單的 XML 文件，讓屬性變成項目。</span><span class="sxs-lookup"><span data-stu-id="a2f22-118">For this example, suppose you want to modify the following simple XML document so that the attributes become elements.</span></span> <span data-ttu-id="a2f22-119">這個主題會先呈現傳統的就地修改方法。</span><span class="sxs-lookup"><span data-stu-id="a2f22-119">This topic first presents the traditional in-place modification approach.</span></span> <span data-ttu-id="a2f22-120">然後它會顯示功能結構方法。</span><span class="sxs-lookup"><span data-stu-id="a2f22-120">It then shows the functional construction approach.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root Data1="123" Data2="456">  
  <Child1>Content</Child1>  
</Root>  
```  
  
### <a name="modifying-the-xml-tree"></a><span data-ttu-id="a2f22-121">修改 XML 樹狀結構</span><span class="sxs-lookup"><span data-stu-id="a2f22-121">Modifying the XML Tree</span></span>  
 <span data-ttu-id="a2f22-122">您可以撰寫特定的程序性程式碼以便從屬性建立項目，然後刪除該屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a2f22-122">You can write some procedural code to create elements from the attributes, and then delete the attributes, as follows:</span></span>  
  
```csharp  
XElement root = XElement.Load("Data.xml");  
foreach (XAttribute att in root.Attributes()) {  
    root.Add(new XElement(att.Name, (string)att));  
}  
root.Attributes().Remove();  
Console.WriteLine(root);  
```  
  
 <span data-ttu-id="a2f22-123">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="a2f22-123">This code produces the following output:</span></span>  
  
```xml  
<Root>  
  <Child1>Content</Child1>  
  <Data1>123</Data1>  
  <Data2>456</Data2>  
</Root>  
```  
  
### <a name="functional-construction-approach"></a><span data-ttu-id="a2f22-124">功能結構方法</span><span class="sxs-lookup"><span data-stu-id="a2f22-124">Functional Construction Approach</span></span>  
 <span data-ttu-id="a2f22-125">相較之下，功能性方法會從來源樹狀結構挑選並選擇項目和屬性，然後在加入到新的樹狀結構時，適當地加以轉換，藉以包含形成新樹狀結構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a2f22-125">By contrast, a functional approach consists of code to form a new tree, picking and choosing elements and attributes from the source tree, and transforming them as appropriate as they are added to the new tree.</span></span> <span data-ttu-id="a2f22-126">功能性方法的外觀如下所示：</span><span class="sxs-lookup"><span data-stu-id="a2f22-126">The functional approach looks like the following:</span></span>  
  
```csharp  
XElement root = XElement.Load("Data.xml");  
XElement newTree = new XElement("Root",  
    root.Element("Child1"),  
    from att in root.Attributes()  
    select new XElement(att.Name, (string)att)  
);  
Console.WriteLine(newTree);  
```  
  
 <span data-ttu-id="a2f22-127">這個範例會與第一個範例輸出相同的 XML。</span><span class="sxs-lookup"><span data-stu-id="a2f22-127">This example outputs the same XML as the first example.</span></span> <span data-ttu-id="a2f22-128">但是請注意，您實際上可以用功能性方法查看所產生的新 XML 結構。</span><span class="sxs-lookup"><span data-stu-id="a2f22-128">However, notice that you can actually see the resulting structure of the new XML in the functional approach.</span></span> <span data-ttu-id="a2f22-129">您可以查看 `Root` 項目的建立、從來源樹狀結構提取 `Child1` 項目的程式碼，以及將屬性從來源樹狀結構轉換到新樹狀結構中的項目之程式碼。</span><span class="sxs-lookup"><span data-stu-id="a2f22-129">You can see the creation of the `Root` element, the code that pulls the `Child1` element from the source tree, and the code that transforms the attributes from the source tree to elements in the new tree.</span></span>  
  
 <span data-ttu-id="a2f22-130">在這個情況下，比起第一個範例，功能性範例更短而且更簡單。</span><span class="sxs-lookup"><span data-stu-id="a2f22-130">The functional example in this case is not any shorter than the first example, and it is not really any simpler.</span></span> <span data-ttu-id="a2f22-131">不過，如果您有針對 XML 樹狀結構進行許多變更，非功能性方法將會變成相當複雜，而且有些遲鈍。</span><span class="sxs-lookup"><span data-stu-id="a2f22-131">However, if you have many changes to make to an XML tree, the non functional approach will become quite complex and somewhat obtuse.</span></span> <span data-ttu-id="a2f22-132">相反地，使用功能性方法時，您仍然可以在適當地內嵌查詢和運算式，只形成所需的 XML，以便在所需的內容中提取。</span><span class="sxs-lookup"><span data-stu-id="a2f22-132">In contrast, when using the functional approach, you still just form the desired XML, embedding queries and expressions as appropriate, to pull in the desired content.</span></span> <span data-ttu-id="a2f22-133">功能性方法會產生容易維護的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a2f22-133">The functional approach yields code that is easier to maintain.</span></span>  
  
 <span data-ttu-id="a2f22-134">請注意，在這個情況下，功能性方法可能不會實際與樹狀結構管理方法一起執行。</span><span class="sxs-lookup"><span data-stu-id="a2f22-134">Notice that in this case the functional approach probably would not perform quite as well as the tree manipulation approach.</span></span> <span data-ttu-id="a2f22-135">主要的問題在於功能性方法會建立更多短期存在的物件。</span><span class="sxs-lookup"><span data-stu-id="a2f22-135">The main issue is that the functional approach creates more short lived objects.</span></span> <span data-ttu-id="a2f22-136">不過，如果使用功能性方法能讓程式設計人員的產能更大，進行取捨是有效的方法。</span><span class="sxs-lookup"><span data-stu-id="a2f22-136">However, the tradeoff is an effective one if using the functional approach allows for greater programmer productivity.</span></span>  
  
 <span data-ttu-id="a2f22-137">這是非常簡單的範例，但是它有助於顯示兩種方法間的觀點差異。</span><span class="sxs-lookup"><span data-stu-id="a2f22-137">This is a very simple example, but it serves to show the difference in philosophy between the two approaches.</span></span> <span data-ttu-id="a2f22-138">功能性方法在轉換大型 XML 文件時，會產生較大的產能。</span><span class="sxs-lookup"><span data-stu-id="a2f22-138">The functional approach yields greater productivity gains for transforming larger XML documents.</span></span>  
  
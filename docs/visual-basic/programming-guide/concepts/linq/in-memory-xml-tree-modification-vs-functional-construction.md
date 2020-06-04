---
title: 記憶體中 XML 樹狀修改與函式建構 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: d91c4ebf-6549-43cc-9961-26d4a82f722b
ms.openlocfilehash: efdbf51efa0f502ac9991d520defe45bb95678b7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397605"
---
# <a name="in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml-visual-basic"></a><span data-ttu-id="c8095-102">記憶體中的 XML 樹狀結構修改與功能結構（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="c8095-102">In-Memory XML Tree Modification vs. Functional Construction (LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="c8095-103">就地修改 XML 樹狀結構是變更 XML 文件組織結構的傳統方式。</span><span class="sxs-lookup"><span data-stu-id="c8095-103">Modifying an XML tree in place is a traditional approach to changing the shape of an XML document.</span></span> <span data-ttu-id="c8095-104">一般應用程式會將文件載入到資料存放區，例如 DOM 或 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]；使用程式設計介面插入節點、刪除節點或變更節點的內容；然後將 XML 儲存到檔案或透過網路傳輸。</span><span class="sxs-lookup"><span data-stu-id="c8095-104">A typical application loads a document into a data store such as DOM or [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]; uses a programming interface to insert nodes, delete nodes, or change the content of nodes; and then saves the XML to a file or transmits it over a network.</span></span>  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<span data-ttu-id="c8095-105">啟用在許多案例中有用的另一種方法 *：功能結構*。</span><span class="sxs-lookup"><span data-stu-id="c8095-105">enables another approach that is useful in many scenarios *: functional construction*.</span></span> <span data-ttu-id="c8095-106">功能結構會將修改資料視為轉換的問題，而不是資料存放區的詳細管理。</span><span class="sxs-lookup"><span data-stu-id="c8095-106">Functional construction treats modifying data as a problem of transformation, rather than as detailed manipulation of a data store.</span></span> <span data-ttu-id="c8095-107">如果您可以表示資料，並將其有效地從一個表單轉換到另一個表單，結果會與您取得一個資料存放區，然後以相同的方式管理該資料存放區取得其他組織結構相同。</span><span class="sxs-lookup"><span data-stu-id="c8095-107">If you can take a representation of data and transform it efficiently from one form to another, the result is the same as if you took one data store and manipulated it in some way to take another shape.</span></span> <span data-ttu-id="c8095-108">功能結構方法的關鍵在於將查詢結果傳遞到 <xref:System.Xml.Linq.XDocument> 和 <xref:System.Xml.Linq.XElement> 建構函式。</span><span class="sxs-lookup"><span data-stu-id="c8095-108">A key to the functional construction approach is to pass the results of queries to <xref:System.Xml.Linq.XDocument> and <xref:System.Xml.Linq.XElement> constructors.</span></span>  
  
 <span data-ttu-id="c8095-109">在許多情況下，您可以用管理資料存放區的少數時間撰寫轉換程式碼，而且該程式碼更穩定、更容易維護。</span><span class="sxs-lookup"><span data-stu-id="c8095-109">In many cases you can write the transformational code in a fraction of the time that it would take to manipulate the data store, and that code is more robust and easier to maintain.</span></span> <span data-ttu-id="c8095-110">在這些情況下，即使轉換方法可以取得更大的處理能力，這都是更有效的修改資料方式。</span><span class="sxs-lookup"><span data-stu-id="c8095-110">In these cases, even though the transformational approach can take more processing power, it is a more effective way to modify data.</span></span> <span data-ttu-id="c8095-111">在許多情況下，如果開發人員熟悉功能性方法，產生的程式碼較容易了解。</span><span class="sxs-lookup"><span data-stu-id="c8095-111">If a developer is familiar with the functional approach, the resulting code in many cases is easier to understand.</span></span> <span data-ttu-id="c8095-112">尋找修改樹狀結構每個部分的程式碼非常容易。</span><span class="sxs-lookup"><span data-stu-id="c8095-112">It is easy to find the code that modifies each part of the tree.</span></span>  
  
 <span data-ttu-id="c8095-113">您就地修改 XML 樹狀結構的方法對於許多 DOM 程式設計人員而言更為熟悉，而使用功能性方法撰寫的程式碼對於還不了解該方法的開發人員而言，似乎比較不熟悉。</span><span class="sxs-lookup"><span data-stu-id="c8095-113">The approach where you modify an XML tree in-place is more familiar to many DOM programmers, whereas code written using the functional approach might look unfamiliar to a developer who doesn't yet understand that approach.</span></span> <span data-ttu-id="c8095-114">如果您必須針對大型 XML 樹狀結構進行小小的修改，您就地修改樹狀結構的方法在大部分的情況下，將會需要較少的 CPU 時間。</span><span class="sxs-lookup"><span data-stu-id="c8095-114">If you have to only make a small modification to a large XML tree, the approach where you modify a tree in place in many cases will take less CPU time.</span></span>  
  
 <span data-ttu-id="c8095-115">本主題提供利用兩種方法實作的範例。</span><span class="sxs-lookup"><span data-stu-id="c8095-115">This topic provides an example that is implemented with both approaches.</span></span>  
  
## <a name="transforming-attributes-into-elements"></a><span data-ttu-id="c8095-116">將屬性轉換為項目</span><span class="sxs-lookup"><span data-stu-id="c8095-116">Transforming Attributes into Elements</span></span>  
 <span data-ttu-id="c8095-117">針對這個範例，假設您想要修改下列簡單的 XML 文件，讓屬性變成項目。</span><span class="sxs-lookup"><span data-stu-id="c8095-117">For this example, suppose you want to modify the following simple XML document so that the attributes become elements.</span></span> <span data-ttu-id="c8095-118">這個主題會先呈現傳統的就地修改方法。</span><span class="sxs-lookup"><span data-stu-id="c8095-118">This topic first presents the traditional in-place modification approach.</span></span> <span data-ttu-id="c8095-119">然後它會顯示功能結構方法。</span><span class="sxs-lookup"><span data-stu-id="c8095-119">It then shows the functional construction approach.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root Data1="123" Data2="456">  
  <Child1>Content</Child1>  
</Root>  
```  
  
### <a name="modifying-the-xml-tree"></a><span data-ttu-id="c8095-120">修改 XML 樹狀結構</span><span class="sxs-lookup"><span data-stu-id="c8095-120">Modifying the XML Tree</span></span>  
 <span data-ttu-id="c8095-121">您可以撰寫特定的程序性程式碼以便從屬性建立項目，然後刪除該屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c8095-121">You can write some procedural code to create elements from the attributes, and then delete the attributes, as follows:</span></span>  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
For Each att As XAttribute In root.Attributes()  
    root.Add(New XElement(att.Name, att.Value))  
Next  
root.Attributes().Remove()  
Console.WriteLine(root)  
```  
  
 <span data-ttu-id="c8095-122">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="c8095-122">This code produces the following output:</span></span>  
  
```xml  
<Root>  
  <Child1>Content</Child1>  
  <Data1>123</Data1>  
  <Data2>456</Data2>  
</Root>  
```  
  
### <a name="functional-construction-approach"></a><span data-ttu-id="c8095-123">功能結構方法</span><span class="sxs-lookup"><span data-stu-id="c8095-123">Functional Construction Approach</span></span>  
 <span data-ttu-id="c8095-124">相較之下，功能性方法會從來源樹狀結構挑選並選擇項目和屬性，然後在加入到新的樹狀結構時，適當地加以轉換，藉以包含形成新樹狀結構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8095-124">By contrast, a functional approach consists of code to form a new tree, picking and choosing elements and attributes from the source tree, and transforming them as appropriate as they are added to the new tree.</span></span> <span data-ttu-id="c8095-125">功能性方法的外觀如下所示：</span><span class="sxs-lookup"><span data-stu-id="c8095-125">The functional approach looks like the following:</span></span>  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
Dim newTree As XElement = _  
    <Root>  
        <%= root.<Child1> %>  
        <%= From att In root.Attributes() _  
            Select New XElement(att.Name, att.Value) %>  
    </Root>  
Console.WriteLine(newTree)  
```  
  
 <span data-ttu-id="c8095-126">這個範例會與第一個範例輸出相同的 XML。</span><span class="sxs-lookup"><span data-stu-id="c8095-126">This example outputs the same XML as the first example.</span></span> <span data-ttu-id="c8095-127">但是請注意，您實際上可以用功能性方法查看所產生的新 XML 結構。</span><span class="sxs-lookup"><span data-stu-id="c8095-127">However, notice that you can actually see the resulting structure of the new XML in the functional approach.</span></span> <span data-ttu-id="c8095-128">您可以查看 `Root` 項目的建立、從來源樹狀結構提取 `Child1` 項目的程式碼，以及將屬性從來源樹狀結構轉換到新樹狀結構中的項目之程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8095-128">You can see the creation of the `Root` element, the code that pulls the `Child1` element from the source tree, and the code that transforms the attributes from the source tree to elements in the new tree.</span></span>  
  
 <span data-ttu-id="c8095-129">在這個情況下，比起第一個範例，功能性範例更短而且更簡單。</span><span class="sxs-lookup"><span data-stu-id="c8095-129">The functional example in this case is not any shorter than the first example, and it is not really any simpler.</span></span> <span data-ttu-id="c8095-130">不過，如果您有針對 XML 樹狀結構進行許多變更，非功能性方法將會變成相當複雜，而且有些遲鈍。</span><span class="sxs-lookup"><span data-stu-id="c8095-130">However, if you have many changes to make to an XML tree, the non functional approach will become quite complex and somewhat obtuse.</span></span> <span data-ttu-id="c8095-131">相反地，使用功能性方法時，您仍然可以在適當地內嵌查詢和運算式，只形成所需的 XML，以便在所需的內容中提取。</span><span class="sxs-lookup"><span data-stu-id="c8095-131">In contrast, when using the functional approach, you still just form the desired XML, embedding queries and expressions as appropriate, to pull in the desired content.</span></span> <span data-ttu-id="c8095-132">功能性方法會產生容易維護的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8095-132">The functional approach yields code that is easier to maintain.</span></span>  
  
 <span data-ttu-id="c8095-133">請注意，在這個情況下，功能性方法可能不會實際與樹狀結構管理方法一起執行。</span><span class="sxs-lookup"><span data-stu-id="c8095-133">Notice that in this case the functional approach probably would not perform quite as well as the tree manipulation approach.</span></span> <span data-ttu-id="c8095-134">主要的問題在於功能性方法會建立更多短期存在的物件。</span><span class="sxs-lookup"><span data-stu-id="c8095-134">The main issue is that the functional approach creates more short lived objects.</span></span> <span data-ttu-id="c8095-135">不過，如果使用功能性方法能讓程式設計人員的產能更大，進行取捨是有效的方法。</span><span class="sxs-lookup"><span data-stu-id="c8095-135">However, the tradeoff is an effective one if using the functional approach allows for greater programmer productivity.</span></span>  
  
 <span data-ttu-id="c8095-136">這是非常簡單的範例，但是它有助於顯示兩種方法間的觀點差異。</span><span class="sxs-lookup"><span data-stu-id="c8095-136">This is a very simple example, but it serves to show the difference in philosophy between the two approaches.</span></span> <span data-ttu-id="c8095-137">功能性方法在轉換大型 XML 文件時，會產生較大的產能。</span><span class="sxs-lookup"><span data-stu-id="c8095-137">The functional approach yields greater productivity gains for transforming larger XML documents.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c8095-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c8095-138">See also</span></span>

- [<span data-ttu-id="c8095-139">修改 XML 樹狀結構（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="c8095-139">Modifying XML Trees (LINQ to XML) (Visual Basic)</span></span>](modifying-xml-trees-linq-to-xml.md)

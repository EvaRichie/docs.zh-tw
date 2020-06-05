---
title: 功能性程序性程式設計 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: ea1015a5-d4c8-4d79-8e1e-ba17a40a4f39
ms.openlocfilehash: 0b525f13298e7402369b890516434cec47e01542
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398431"
---
# <a name="functional-vs-procedural-programming-linq-to-xml-visual-basic"></a><span data-ttu-id="8c8d6-102">功能與程式性程式設計（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="8c8d6-102">Functional vs. Procedural Programming (LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="8c8d6-103">XML 應用程式有很多種：</span><span class="sxs-lookup"><span data-stu-id="8c8d6-103">There are various types of XML applications:</span></span>  
  
- <span data-ttu-id="8c8d6-104">有些應用程式會採用 XML 來源文件，然後以不同於來源文件的組織結構產生新的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-104">Some applications take source XML documents, and produce new XML documents that are in a different shape than the source documents.</span></span>  
  
- <span data-ttu-id="8c8d6-105">有些應用程式會採用 XML 來源文件，然後以完全不同的形式 (例如，HTML 或 CSV 文字檔)，產生結果文件。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-105">Some applications take source XML documents, and produce result documents in an entirely different form, such as HTML or CSV text files.</span></span>  
  
- <span data-ttu-id="8c8d6-106">有些應用程式會採用 XML 來源文件，然後將記錄插入到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-106">Some applications take source XML documents, and insert records into a database.</span></span>  
  
- <span data-ttu-id="8c8d6-107">有些應用程式會從其他來源 (例如，資料庫) 取得資料，然後從其中建立 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-107">Some applications take data from another source, such as a database, and create XML documents from it.</span></span>  
  
 <span data-ttu-id="8c8d6-108">這些並非 XML 應用程式的全部類型，但是這些是 XML 程式設計人員必須實作的一組代表性的功能類型。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-108">These are not all of the types of XML applications, but these are a representative set of the types of functionality that an XML programmer has to implement.</span></span>  
  
 <span data-ttu-id="8c8d6-109">利用所有這些應用程式類型，開發人員可以採用兩種明顯不同的方法：</span><span class="sxs-lookup"><span data-stu-id="8c8d6-109">With all of these types of applications, there are two contrasting approaches that a developer can take:</span></span>  
  
- <span data-ttu-id="8c8d6-110">使用宣告式方法的功能結構。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-110">Functional construction using a declarative approach.</span></span>  
  
- <span data-ttu-id="8c8d6-111">使用程序性程式碼進行記憶體中 XML 樹狀結構修改。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-111">In-memory XML tree modification using procedural code.</span></span>  
  
 <span data-ttu-id="8c8d6-112">LINQ to XML 同時支援這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-112">LINQ to XML supports both approaches.</span></span>  
  
 <span data-ttu-id="8c8d6-113">使用功能性方法時，您可以撰寫採用來源文件的轉換，然後利用所需的組織結構產生全新的結果文件。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-113">When using the functional approach, you write transformations that take the source documents and generate completely new result documents with the desired shape.</span></span>  
  
 <span data-ttu-id="8c8d6-114">就地修改 XML 樹狀結構時，您可以撰寫可在記憶體中 XML 樹狀結構內周遊與導覽程式碼的程式碼，藉以在必要時插入、刪除與修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-114">When modifying an XML tree in place, you write code that traverses and navigates through nodes in an in-memory XML tree, inserting, deleting, and modifying nodes as necessary.</span></span>  
  
 <span data-ttu-id="8c8d6-115">您可以搭配任一種方法使用 LINQ to XML。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-115">You can use LINQ to XML with either approach.</span></span> <span data-ttu-id="8c8d6-116">您可以使用相同的類別，在某些情況下，也可以使用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-116">You use the same classes, and in some cases the same methods.</span></span> <span data-ttu-id="8c8d6-117">但是，兩種方法的結構與目標差異相當大。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-117">However, the structure and goals of the two approaches are very different.</span></span> <span data-ttu-id="8c8d6-118">例如，在不同的情況下，其中一種方法的效能通常會比較好，而且或多或少會使用到記憶體。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-118">For example, in different situations, one or the other approach will often have better performance, and use more or less memory.</span></span> <span data-ttu-id="8c8d6-119">此外，其中一種方法會比較容易撰寫，並產生較容易維護的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-119">In addition, one or the other approach will be easier to write and yield more maintainable code.</span></span>  
  
 <span data-ttu-id="8c8d6-120">若要查看這兩種方法的對比，請參閱[記憶體中的 XML 樹狀結構修改與功能結構（LINQ to XML）（Visual Basic）](in-memory-xml-tree-modification-vs-functional-construction.md)。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-120">To see the two approaches contrasted, see [In-Memory XML Tree Modification vs. Functional Construction (LINQ to XML) (Visual Basic)](in-memory-xml-tree-modification-vs-functional-construction.md).</span></span>  
  
 <span data-ttu-id="8c8d6-121">如需撰寫功能性轉換的教學課程，請參閱[XML 的純功能性轉換（Visual Basic）](pure-functional-transformations-of-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="8c8d6-121">For a tutorial on writing functional transformations, see [Pure Functional Transformations of XML (Visual Basic)](pure-functional-transformations-of-xml.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8c8d6-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8c8d6-122">See also</span></span>

- [<span data-ttu-id="8c8d6-123">LINQ to XML 程式設計總覽（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="8c8d6-123">LINQ to XML Programming Overview (Visual Basic)</span></span>](linq-to-xml-programming-overview.md)

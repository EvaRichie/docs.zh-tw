---
title: 使用 LINQ to XML 處理 XML 資料
ms.date: 03/30/2017
ms.assetid: 059d6b9d-63f7-4011-9ba8-8406f0bbae7d
ms.openlocfilehash: 782a14303a9ec35750530d2506a046dd53d37fc0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95686991"
---
# <a name="process-xml-data-using-linq-to-xml"></a><span data-ttu-id="8e390-102">使用 LINQ to XML 處理 XML 資料</span><span class="sxs-lookup"><span data-stu-id="8e390-102">Process XML Data Using LINQ to XML</span></span>

<span data-ttu-id="8e390-103">LINQ to XML 是 .NET Framework 3.5 版中用來處理 XML 資料的新模型。</span><span class="sxs-lookup"><span data-stu-id="8e390-103">LINQ to XML is the new model in the .NET Framework version 3.5 for processing XML data.</span></span> <span data-ttu-id="8e390-104">LINQ to XML 可讓開發人員進行預期對 XML 資料做的所有事情：查詢、修改、建立、儲存和序列化 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="8e390-104">LINQ to XML allows developers to do everything they would expect with XML data: querying, modifying, creating, saving, and serializing XML documents.</span></span> <span data-ttu-id="8e390-105">真正的優點則在於查詢和建立功能。</span><span class="sxs-lookup"><span data-stu-id="8e390-105">The real advantages lie in the query and creation capabilities.</span></span>  
  
 <span data-ttu-id="8e390-106">LINQ to XML 中的查詢非常簡潔且具表達性，使用的語法比較類似於 SQL，而比較不像 XPath 或 XQuery。</span><span class="sxs-lookup"><span data-stu-id="8e390-106">Queries in LINQ to XML are succinct and expressive, using syntax more similar to SQL than to XPath or XQuery.</span></span> <span data-ttu-id="8e390-107">由於查詢結果可以當做項目或屬性的集合傳回，而且可以當做 XElement 物件的參數使用，所以 XML 樹狀結構可以輕鬆地在不同形狀之間轉換。</span><span class="sxs-lookup"><span data-stu-id="8e390-107">Because query results can be returned as collections of elements or attributes and can be used as parameters for XElement objects, XML trees can be easily transformed from one shape to another.</span></span>  
  
 <span data-ttu-id="8e390-108">LINQ to XML 會利用 .NET Framework 3.5 版中的 Language-integrated Query (LINQ) 技術。</span><span class="sxs-lookup"><span data-stu-id="8e390-108">LINQ to XML leverages the language-integrated query (LINQ) technology in the .NET Framework version 3.5.</span></span> <span data-ttu-id="8e390-109">LINQ 會擴充 C# 和 Visual Basic 的語言語法，以提供可擴充至任何可能資料存放區的強大查詢功能。</span><span class="sxs-lookup"><span data-stu-id="8e390-109">LINQ extends the language syntax of C# and Visual Basic to provide powerful query capabilities that can be extended to potentially any data store.</span></span>  
  
 <span data-ttu-id="8e390-110">如需其用法的詳細討論，請參閱 [LINQ to XML (C#)](../../linq/linq-xml-overview.md) 和 [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8e390-110">For a detailed discussion of its use, see [LINQ to XML (C#)](../../linq/linq-xml-overview.md) and [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md).</span></span> <span data-ttu-id="8e390-111">如需 LINQ 架構的概觀，請參閱 [Language-Integrated Query (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md) 或 [Language-Integrated Query (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8e390-111">For an overview of the LINQ framework, see [Language-Integrated Query (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md) or [Language-Integrated Query (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8e390-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8e390-112">See also</span></span>

- <xref:System.Xml.Linq>
- <xref:System.Linq>
- [<span data-ttu-id="8e390-113">LINQ to XML 與 DOM (c # ) </span><span class="sxs-lookup"><span data-stu-id="8e390-113">LINQ to XML vs. DOM (C#)</span></span>](../../linq/linq-xml-vs-dom.md)
- [<span data-ttu-id="8e390-114">LINQ to XML 與 DOM (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="8e390-114">LINQ to XML vs. DOM (Visual Basic)</span></span>](../../linq/linq-xml-vs-dom.md)
- [<span data-ttu-id="8e390-115">LINQ to XML 與其他 XML 技術的比較 (c # ) </span><span class="sxs-lookup"><span data-stu-id="8e390-115">LINQ to XML vs. Other XML Technologies (C#)</span></span>](../../linq/linq-xml-vs-xml-technologies.md)
- [<span data-ttu-id="8e390-116">LINQ to XML 與其他 XML 技術 (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="8e390-116">LINQ to XML vs. Other XML Technologies (Visual Basic)</span></span>](../../linq/linq-xml-vs-xml-technologies.md)

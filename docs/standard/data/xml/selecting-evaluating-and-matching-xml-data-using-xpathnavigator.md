---
title: 使用 XPathNavigator 選取、評估及比對 XML 資料
ms.date: 03/30/2017
ms.assetid: 46e059f8-4dc8-4185-9236-784be95228ed
ms.openlocfilehash: 3096582055dc17d5724cebd79e74d2aa24154bcb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734669"
---
# <a name="selecting-evaluating-and-matching-xml-data-using-xpathnavigator"></a><span data-ttu-id="3a58e-102">使用 XPathNavigator 選取、評估及比對 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-102">Selecting, Evaluating and Matching XML Data using XPathNavigator</span></span>

<span data-ttu-id="3a58e-103"><xref:System.Xml.XPath.XPathNavigator> 類別會提供使用 XPath 查詢選取 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中節點的方法，評估及檢查 XPath 運算式的結果，以及決定 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中的節點是否符合指定的 XPath 運算式。</span><span class="sxs-lookup"><span data-stu-id="3a58e-103">The <xref:System.Xml.XPath.XPathNavigator> class provides methods to select nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using an XPath query, evaluate and examine the results of an XPath expression, and determine if a node in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object matches a given XPath expression.</span></span> <span data-ttu-id="3a58e-104">下列主題說明了這些及其他與選取、評估及比對 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中之節點相關的概念。</span><span class="sxs-lookup"><span data-stu-id="3a58e-104">These and other concepts that relate to selecting, evaluating and matching nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object are described in the following topics.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="3a58e-105">本節內容</span><span class="sxs-lookup"><span data-stu-id="3a58e-105">In This Section</span></span>  

 [<span data-ttu-id="3a58e-106">使用 XPathNavigator 選取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-106">Select XML Data Using XPathNavigator</span></span>](select-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="3a58e-107">說明一組 <xref:System.Xml.XPath.XPathNavigator> 類別方法，其用於使用 XPath 運算式選取 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中的一組節點。</span><span class="sxs-lookup"><span data-stu-id="3a58e-107">Describes the set of <xref:System.Xml.XPath.XPathNavigator> class methods used to select a set of nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using an XPath expression.</span></span>  
  
 [<span data-ttu-id="3a58e-108">使用 XPathNavigator 評估 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="3a58e-108">Evaluate XPath Expressions using XPathNavigator</span></span>](evaluate-xpath-expressions-using-xpathnavigator.md)  
 <span data-ttu-id="3a58e-109">說明用於評估 XPath 運算式之 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 類別的 <xref:System.Xml.XPath.XPathNavigator> 方法。</span><span class="sxs-lookup"><span data-stu-id="3a58e-109">Describes the <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> method of the <xref:System.Xml.XPath.XPathNavigator> class used to evaluate an XPath expression.</span></span>  
  
 [<span data-ttu-id="3a58e-110">使用 XPathNavigator 比對節點</span><span class="sxs-lookup"><span data-stu-id="3a58e-110">Matching Nodes using XPathNavigator</span></span>](matching-nodes-using-xpathnavigator.md)  
 <span data-ttu-id="3a58e-111">說明用於決定節點是否符合 XPath 運算式之 <xref:System.Xml.XPath.XPathNavigator.Matches%2A> 類別的 <xref:System.Xml.XPath.XPathNavigator> 方法。</span><span class="sxs-lookup"><span data-stu-id="3a58e-111">Describes the <xref:System.Xml.XPath.XPathNavigator.Matches%2A> method of the <xref:System.Xml.XPath.XPathNavigator> class used to determine if a node matches an XPath expression.</span></span>  
  
 [<span data-ttu-id="3a58e-112">在 XPath 查詢中辨識的節點型別</span><span class="sxs-lookup"><span data-stu-id="3a58e-112">Node Types Recognized with XPath Queries</span></span>](node-types-recognized-with-xpath-queries.md)  
 <span data-ttu-id="3a58e-113">說明 XPath 查詢中辨識的節點型別。</span><span class="sxs-lookup"><span data-stu-id="3a58e-113">Describes the types of nodes recognized in an XPath query.</span></span>  
  
 [<span data-ttu-id="3a58e-114">XPath 查詢及命名空間</span><span class="sxs-lookup"><span data-stu-id="3a58e-114">XPath Queries and Namespaces</span></span>](xpath-queries-and-namespaces.md)  
 <span data-ttu-id="3a58e-115">說明 XPath 查詢中命名空間的使用。</span><span class="sxs-lookup"><span data-stu-id="3a58e-115">Describes the use of namespaces in an XPath query.</span></span>  
  
 [<span data-ttu-id="3a58e-116">編譯 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="3a58e-116">Compiled XPath Expressions</span></span>](compiled-xpath-expressions.md)  
 <span data-ttu-id="3a58e-117">說明表示已編譯 XPath 查詢的 <xref:System.Xml.XPath.XPathExpression> 類別。</span><span class="sxs-lookup"><span data-stu-id="3a58e-117">Describes the <xref:System.Xml.XPath.XPathExpression> class that represents a compiled XPath query.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3a58e-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3a58e-118">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="3a58e-119">使用 XPath 資料模型處理 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-119">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="3a58e-120">使用 XPathDocument 及 XmlDocument 讀取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-120">Reading XML Data using XPathDocument and XmlDocument</span></span>](reading-xml-data-using-xpathdocument-and-xmldocument.md)
- [<span data-ttu-id="3a58e-121">使用 XPathNavigator 存取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-121">Accessing XML Data using XPathNavigator</span></span>](accessing-xml-data-using-xpathnavigator.md)
- [<span data-ttu-id="3a58e-122">使用 XPathNavigator 編輯 XML 資料</span><span class="sxs-lookup"><span data-stu-id="3a58e-122">Editing XML Data using XPathNavigator</span></span>](editing-xml-data-using-xpathnavigator.md)
- [<span data-ttu-id="3a58e-123">使用 XPathNavigator 進行結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="3a58e-123">Schema Validation using XPathNavigator</span></span>](schema-validation-using-xpathnavigator.md)

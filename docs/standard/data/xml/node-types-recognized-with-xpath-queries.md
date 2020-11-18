---
title: 在 XPath 查詢中辨識的節點型別
ms.date: 03/30/2017
ms.assetid: 1d33e22d-18e5-43f8-a466-2e3d0a8dd094
ms.openlocfilehash: 87f4ed0c8182e250f6926d6c3d82893e6f8b985c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830099"
---
# <a name="node-types-recognized-with-xpath-queries"></a><span data-ttu-id="806ae-102">在 XPath 查詢中辨識的節點型別</span><span class="sxs-lookup"><span data-stu-id="806ae-102">Node Types Recognized with XPath Queries</span></span>
<span data-ttu-id="806ae-103">在 XPath 查詢中辨識的節點型別不同於在文件物件模型 (DOM) 中找到的節點型別。</span><span class="sxs-lookup"><span data-stu-id="806ae-103">The types of nodes recognized in an XPath query are not the same node types found in the Document Object Model (DOM).</span></span>  
  
## <a name="w3c-xpath-node-types"></a><span data-ttu-id="806ae-104">W3C XPath 節點型別</span><span class="sxs-lookup"><span data-stu-id="806ae-104">W3C XPath Node Types</span></span>  
 <span data-ttu-id="806ae-105">在 XPath 查詢中辨識的節點型別並非在文件物件模型 (DOM) 中找到的節點型別。</span><span class="sxs-lookup"><span data-stu-id="806ae-105">The types of nodes recognized in an XPath query are not the types of nodes found in the Document Object Model (DOM).</span></span> <span data-ttu-id="806ae-106">以下是由 <xref:System.Xml.XPath.XPathNodeType> 列舉表示的 XPath 節點型別。</span><span class="sxs-lookup"><span data-stu-id="806ae-106">The following are the XPath node types represented by the <xref:System.Xml.XPath.XPathNodeType> enumeration.</span></span>  
  
- <xref:System.Xml.XPath.XPathNodeType.All>  
  
- <xref:System.Xml.XPath.XPathNodeType.Attribute>  
  
- <xref:System.Xml.XPath.XPathNodeType.Comment>  
  
- <xref:System.Xml.XPath.XPathNodeType.Element>  
  
- <xref:System.Xml.XPath.XPathNodeType.Namespace>  
  
- <xref:System.Xml.XPath.XPathNodeType.ProcessingInstruction>  
  
- <xref:System.Xml.XPath.XPathNodeType.Root>  
  
- <xref:System.Xml.XPath.XPathNodeType.SignificantWhitespace>  
  
- <xref:System.Xml.XPath.XPathNodeType.Text>  
  
- <xref:System.Xml.XPath.XPathNodeType.Whitespace>  
  
 <span data-ttu-id="806ae-107">這些節點型別以 XPath 資料模型為基礎，其中節點均衍生自 XML 資訊集。</span><span class="sxs-lookup"><span data-stu-id="806ae-107">These node types are based on the XPath data model, where the nodes are derived from the XML Information Set.</span></span> <span data-ttu-id="806ae-108"><xref:System.Xml.XPath.XPathNodeType.SignificantWhitespace> 及 <xref:System.Xml.XPath.XPathNodeType.Whitespace> 節點型別是 XPath 資料模型中所說明之基底節點型別的 Microsoft .NET Framework 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="806ae-108">The <xref:System.Xml.XPath.XPathNodeType.SignificantWhitespace> and <xref:System.Xml.XPath.XPathNodeType.Whitespace> node types are Microsoft .NET Framework extensions to the base node types described in the XPath data model.</span></span>  
  
 <span data-ttu-id="806ae-109">屬性節點型別在 XPath 資料模型中的使用方式與在 DOM 中的不同。</span><span class="sxs-lookup"><span data-stu-id="806ae-109">The attribute node type is used differently in the XPath data model than it is in the DOM.</span></span> <span data-ttu-id="806ae-110">在 XPath 資料模型中，項目節點具有相關的屬性節點集，且項目節點是每個屬性節點的父代。</span><span class="sxs-lookup"><span data-stu-id="806ae-110">In the XPath data model, the element node has a set of attribute nodes related to it and the element node is the parent of each attribute node.</span></span> <span data-ttu-id="806ae-111">不過，在 DOM 中，項目節點是擁有者，並不是父代。</span><span class="sxs-lookup"><span data-stu-id="806ae-111">However, in the DOM, the element node is the owner and not the parent.</span></span> <span data-ttu-id="806ae-112">在這兩個模型中，屬性及命名空間節點都不被視為項目節點的子節點。</span><span class="sxs-lookup"><span data-stu-id="806ae-112">In both models, attribute and namespace nodes are not considered child nodes of the element node.</span></span>  
  
 <span data-ttu-id="806ae-113">命名空間節點型別是 XPath 資料模型中的新加入型別，並不是可辨識的 DOM 節點型別。</span><span class="sxs-lookup"><span data-stu-id="806ae-113">The namespace node type is an addition to the XPath data model and is not a recognized DOM node type.</span></span>  
  
 <span data-ttu-id="806ae-114">如需有關巡覽項目、屬性和命名空間節點的詳細資訊，請參閱[使用 XPathNavigator 巡覽節點集](node-set-navigation-using-xpathnavigator.md)以及[使用 XPathNavigator 巡覽屬性及命名空間節點](attribute-and-namespace-node-navigation-using-xpathnavigator.md)主題。</span><span class="sxs-lookup"><span data-stu-id="806ae-114">For more information about navigating element, attribute, and namespace nodes, see the [Node Set Navigation Using XPathNavigator](node-set-navigation-using-xpathnavigator.md) and [Attribute and Namespace Node Navigation Using XPathNavigator](attribute-and-namespace-node-navigation-using-xpathnavigator.md) topics.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="806ae-115">請參閱</span><span class="sxs-lookup"><span data-stu-id="806ae-115">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="806ae-116">使用 XPath 資料模型處理 XML 資料</span><span class="sxs-lookup"><span data-stu-id="806ae-116">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="806ae-117">使用 XPathNavigator 選取 XML 資料</span><span class="sxs-lookup"><span data-stu-id="806ae-117">Select XML Data Using XPathNavigator</span></span>](select-xml-data-using-xpathnavigator.md)
- [<span data-ttu-id="806ae-118">使用 XPathNavigator 評估 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="806ae-118">Evaluate XPath Expressions using XPathNavigator</span></span>](evaluate-xpath-expressions-using-xpathnavigator.md)
- [<span data-ttu-id="806ae-119">使用 XPathNavigator 比對節點</span><span class="sxs-lookup"><span data-stu-id="806ae-119">Matching Nodes using XPathNavigator</span></span>](matching-nodes-using-xpathnavigator.md)
- [<span data-ttu-id="806ae-120">XPath 查詢及命名空間</span><span class="sxs-lookup"><span data-stu-id="806ae-120">XPath Queries and Namespaces</span></span>](xpath-queries-and-namespaces.md)
- [<span data-ttu-id="806ae-121">編譯 XPath 運算式</span><span class="sxs-lookup"><span data-stu-id="806ae-121">Compiled XPath Expressions</span></span>](compiled-xpath-expressions.md)

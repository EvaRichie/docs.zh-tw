---
title: 在 DOM 中建立新節點
ms.date: 03/30/2017
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
ms.openlocfilehash: dea7add100fbdbb9e761fe39d0d824d27975757f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95704743"
---
# <a name="create-new-nodes-in-the-dom"></a><span data-ttu-id="8c2d1-102">在 DOM 中建立新節點</span><span class="sxs-lookup"><span data-stu-id="8c2d1-102">Create New Nodes in the DOM</span></span>

<span data-ttu-id="8c2d1-103"><xref:System.Xml.XmlDocument> 有一個適用於所有節點型別的建立方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-103">The <xref:System.Xml.XmlDocument> has a create method for all of the node types.</span></span> <span data-ttu-id="8c2d1-104">必要時請為該方法提供名稱，並針對具有內容的節點 (例如，文字節點) 提供內容或其他參數，即可建立節點。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-104">Supply the method with a name when required, and content or other parameters for those nodes that have content (for example, a text node), and the node is created.</span></span> <span data-ttu-id="8c2d1-105">下列方法需要填入名稱及一些其他參數來建立適當的節點。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-105">The following methods are ones that need a name and a few other parameters filled to create an appropriate node.</span></span>  
  
- <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
- <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
- <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
- <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
- <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 <span data-ttu-id="8c2d1-106">其他節點型別除了需為參數提供資料以外，還有更多需求。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-106">Other node types have more requirements than just providing data to parameters.</span></span>  
  
 <span data-ttu-id="8c2d1-107">如需屬性的詳細資訊，請參閱[為 DOM 中的項目建立新屬性](creating-new-attributes-for-elements-in-the-dom.md)。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-107">For information on attributes, see [Creating New Attributes for Elements in the DOM](creating-new-attributes-for-elements-in-the-dom.md).</span></span> <span data-ttu-id="8c2d1-108">如需項目及屬性名稱驗證的詳細資訊，請參閱[建立新節點時的 XML 項目和屬性名稱驗證](xml-element-and-attribute-name-verification-when-creating-new-nodes.md)。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-108">For information on element and attribute name validation, see [XML Element and Attribute Name Verification when Creating New Nodes](xml-element-and-attribute-name-verification-when-creating-new-nodes.md).</span></span> <span data-ttu-id="8c2d1-109">若要建立實體參考，請參閱[建立新實體參考](creating-new-entity-references.md)。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-109">For creating entity references, see [Creating New Entity References](creating-new-entity-references.md).</span></span> <span data-ttu-id="8c2d1-110">如需命名空間如何影響實體參考之擴充的詳細資訊，請參閱[命名空間對包含項目和屬性的新節點之實體參考擴充的影響](namespace-affect-on-entity-ref-expansion-for-new-nodes.md)。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-110">For information on how namespaces affect the expansion of entity references, see [Namespace Affect on Entity Reference Expansion for New Nodes Containing Elements and Attributes](namespace-affect-on-entity-ref-expansion-for-new-nodes.md).</span></span>  
  
 <span data-ttu-id="8c2d1-111">一旦建立新節點，即有數個方法可用來將其插入樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-111">Once new nodes are created, there are several methods available to insert them into the tree.</span></span> <span data-ttu-id="8c2d1-112">該表格會列出這些方法，並說明新節點在 XML 文件物件模型 (DOM) 中會出現於何處。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-112">The table lists the methods with a description of where the new node appears in the XML Document Object Model (DOM).</span></span>  
  
|<span data-ttu-id="8c2d1-113">方法</span><span class="sxs-lookup"><span data-stu-id="8c2d1-113">Method</span></span>|<span data-ttu-id="8c2d1-114">節點取代</span><span class="sxs-lookup"><span data-stu-id="8c2d1-114">Node placement</span></span>|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|<span data-ttu-id="8c2d1-115">在參考節點之前插入。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-115">Inserted before the reference node.</span></span> <span data-ttu-id="8c2d1-116">例如，若要在位置 5 插入新節點：</span><span class="sxs-lookup"><span data-stu-id="8c2d1-116">For example, to insert the new node in position 5:</span></span><br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> <span data-ttu-id="8c2d1-117">如需詳細資訊，請參閱 <xref:System.Xml.XmlNode.InsertBefore%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-117">For more information, see the <xref:System.Xml.XmlNode.InsertBefore%2A> method.</span></span>|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|<span data-ttu-id="8c2d1-118">在參考節點之後插入。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-118">Inserted after the reference node.</span></span> <span data-ttu-id="8c2d1-119">例如：</span><span class="sxs-lookup"><span data-stu-id="8c2d1-119">For example:</span></span><br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> <span data-ttu-id="8c2d1-120">如需詳細資訊，請參閱 <xref:System.Xml.XmlNode.InsertAfter%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-120">For more information, see the <xref:System.Xml.XmlNode.InsertAfter%2A> method.</span></span>|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|<span data-ttu-id="8c2d1-121">將節點加入至指定節點之子節點的清單結尾處。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-121">Adds the node to the end of the list of child nodes for the given node.</span></span> <span data-ttu-id="8c2d1-122">如果加入的節點為 <xref:System.Xml.XmlDocumentFragment>，則文件片段的全部內容都會移至此節點的子清單中。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-122">If the node being added is an <xref:System.Xml.XmlDocumentFragment>, the entire contents of the document fragment are moved into the child list of this node.</span></span> <span data-ttu-id="8c2d1-123">如需詳細資訊，請參閱 <xref:System.Xml.XmlNode.AppendChild%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-123">For more information, see the <xref:System.Xml.XmlNode.AppendChild%2A> method.</span></span>|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|<span data-ttu-id="8c2d1-124">將節點加入至指定節點之子節點的清單開頭。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-124">Adds the node to the beginning of the list of child nodes of the given node.</span></span> <span data-ttu-id="8c2d1-125">如果加入的節點為 <xref:System.Xml.XmlDocumentFragment>，則文件片段的全部內容都會移至此節點的子清單中。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-125">If the node being added is an <xref:System.Xml.XmlDocumentFragment>, the entire contents of the document fragment are moved into the child list of this node.</span></span> <span data-ttu-id="8c2d1-126">如需詳細資訊，請參閱 <xref:System.Xml.XmlNode.PrependChild%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-126">For more information, see the <xref:System.Xml.XmlNode.PrependChild%2A> method.</span></span>|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|<span data-ttu-id="8c2d1-127">將 <xref:System.Xml.XmlAttribute> 節點附加至與項目關聯之屬性集合的結尾。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-127">Appends an <xref:System.Xml.XmlAttribute> node to the end of the attribute collection associated with an element.</span></span> <span data-ttu-id="8c2d1-128">如需詳細資訊，請參閱 <xref:System.Xml.XmlAttributeCollection.Append%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="8c2d1-128">For more information, see the <xref:System.Xml.XmlAttributeCollection.Append%2A> method.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="8c2d1-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8c2d1-129">See also</span></span>

- [<span data-ttu-id="8c2d1-130">XML 文件物件模型 (DOM)</span><span class="sxs-lookup"><span data-stu-id="8c2d1-130">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)

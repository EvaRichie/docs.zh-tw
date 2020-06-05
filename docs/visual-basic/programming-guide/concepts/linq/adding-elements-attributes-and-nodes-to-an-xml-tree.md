---
title: 將項目、屬性和節點新增至 XML 樹狀結構
ms.date: 07/20/2015
ms.assetid: e243e694-c987-43aa-8b22-1e33dace582c
ms.openlocfilehash: 5b80a19c952388c2591536077f382df2f69fe80f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84383893"
---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-visual-basic"></a><span data-ttu-id="47a33-102">將專案、屬性和節點加入至 XML 樹狀結構（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="47a33-102">Adding Elements, Attributes, and Nodes to an XML Tree (Visual Basic)</span></span>
<span data-ttu-id="47a33-103">您可以將內容 (項目、屬性、註解、處理指示、文字和 CDATA) 加入到現有的 XML 樹狀結構中。</span><span class="sxs-lookup"><span data-stu-id="47a33-103">You can add content (elements, attributes, comments, processing instructions, text, and CDATA) to an existing XML tree.</span></span>  
  
## <a name="methods-for-adding-content"></a><span data-ttu-id="47a33-104">加入內容的方法</span><span class="sxs-lookup"><span data-stu-id="47a33-104">Methods for Adding Content</span></span>  
 <span data-ttu-id="47a33-105">下列方法會將子內容加入到 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument>：</span><span class="sxs-lookup"><span data-stu-id="47a33-105">The following methods add child content to an <xref:System.Xml.Linq.XElement> or an <xref:System.Xml.Linq.XDocument>:</span></span>  
  
|<span data-ttu-id="47a33-106">方法</span><span class="sxs-lookup"><span data-stu-id="47a33-106">Method</span></span>|<span data-ttu-id="47a33-107">Description</span><span class="sxs-lookup"><span data-stu-id="47a33-107">Description</span></span>|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|<span data-ttu-id="47a33-108">將內容加入到 <xref:System.Xml.Linq.XContainer> 之子內容的結尾。</span><span class="sxs-lookup"><span data-stu-id="47a33-108">Adds content at the end of the child content of the <xref:System.Xml.Linq.XContainer>.</span></span>|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|<span data-ttu-id="47a33-109">將內容加入到 <xref:System.Xml.Linq.XContainer> 之子內容的開頭。</span><span class="sxs-lookup"><span data-stu-id="47a33-109">Adds content at the beginning of the child content of the <xref:System.Xml.Linq.XContainer>.</span></span>|  
  
 <span data-ttu-id="47a33-110">下列方法會加入內容，做為 <xref:System.Xml.Linq.XNode> 的同層級節點。</span><span class="sxs-lookup"><span data-stu-id="47a33-110">The following methods add content as sibling nodes of an <xref:System.Xml.Linq.XNode>.</span></span> <span data-ttu-id="47a33-111">雖然您可以將有效的同層級內容加入到節點的其他型別 (例如，<xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XText>)，但是您加入同層級內容的最常見目標節點為 <xref:System.Xml.Linq.XComment>。</span><span class="sxs-lookup"><span data-stu-id="47a33-111">The most common node to which you add sibling content is <xref:System.Xml.Linq.XElement>, although you can add valid sibling content to other types of nodes such as <xref:System.Xml.Linq.XText> or <xref:System.Xml.Linq.XComment>.</span></span>  
  
|<span data-ttu-id="47a33-112">方法</span><span class="sxs-lookup"><span data-stu-id="47a33-112">Method</span></span>|<span data-ttu-id="47a33-113">Description</span><span class="sxs-lookup"><span data-stu-id="47a33-113">Description</span></span>|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|<span data-ttu-id="47a33-114">將內容加入到 <xref:System.Xml.Linq.XNode> 之後。</span><span class="sxs-lookup"><span data-stu-id="47a33-114">Adds content after the <xref:System.Xml.Linq.XNode>.</span></span>|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|<span data-ttu-id="47a33-115">將內容加入到 <xref:System.Xml.Linq.XNode> 之前。</span><span class="sxs-lookup"><span data-stu-id="47a33-115">Adds content before the <xref:System.Xml.Linq.XNode>.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="47a33-116">範例</span><span class="sxs-lookup"><span data-stu-id="47a33-116">Example</span></span>  
  
### <a name="description"></a><span data-ttu-id="47a33-117">描述</span><span class="sxs-lookup"><span data-stu-id="47a33-117">Description</span></span>  
 <span data-ttu-id="47a33-118">下列範例會建立兩個 XML 樹狀結構，然後修改其中一個樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="47a33-118">The following example creates two XML trees, and then modifies one of the trees.</span></span>  
  
### <a name="code"></a><span data-ttu-id="47a33-119">程式碼</span><span class="sxs-lookup"><span data-stu-id="47a33-119">Code</span></span>  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element1>1</Element1>  
        <Element2>2</Element2>  
        <Element3>3</Element3>  
        <Element4>4</Element4>  
        <Element5>5</Element5>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child2>2</Child2>  
        <Child3>3</Child3>  
        <Child4>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
xmlTree.Add(<NewChild>new content</NewChild>)  
xmlTree.Add( _  
    From el In srcTree.Elements() _  
    Where CInt(el) > 3 _  
    Select el)  
  
' Even though Child9 does not exist in srcTree, the following statement  
' will not throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"))  
Console.WriteLine(xmlTree)  
```  
  
### <a name="comments"></a><span data-ttu-id="47a33-120">註解</span><span class="sxs-lookup"><span data-stu-id="47a33-120">Comments</span></span>  
 <span data-ttu-id="47a33-121">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="47a33-121">This code produces the following output:</span></span>  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a><span data-ttu-id="47a33-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="47a33-122">See also</span></span>

- [<span data-ttu-id="47a33-123">修改 XML 樹狀結構（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="47a33-123">Modifying XML Trees (LINQ to XML) (Visual Basic)</span></span>](modifying-xml-trees-linq-to-xml.md)

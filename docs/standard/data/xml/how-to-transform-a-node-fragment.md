---
title: 作法：轉換節點片段
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
ms.openlocfilehash: f5eb8e7826dd132fd46f6f476335416e7dd03269
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722683"
---
# <a name="how-to-transform-a-node-fragment"></a><span data-ttu-id="0a004-102">作法：轉換節點片段</span><span class="sxs-lookup"><span data-stu-id="0a004-102">How to: Transform a Node Fragment</span></span>

<span data-ttu-id="0a004-103">當您轉換包含於 <xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument> 物件的資料時，XSLT 轉換會套用至整個文件。</span><span class="sxs-lookup"><span data-stu-id="0a004-103">When you transform data contained in an <xref:System.Xml.XmlDocument> or <xref:System.Xml.XPath.XPathDocument> object the XSLT transformations apply to a document as a whole.</span></span> <span data-ttu-id="0a004-104">換言之，如果您要傳入的節點不是文件的根節點，則不會阻止轉換程序取得已載入文件中的所有節點。</span><span class="sxs-lookup"><span data-stu-id="0a004-104">In other words, if you pass in a node other than the document root node, this does not prevent the transformation process from accessing all nodes in the loaded document.</span></span> <span data-ttu-id="0a004-105">若要轉換節點片段，您必須建立僅含有該節點片段的單獨物件，再將該物件傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="0a004-105">To transform a node fragment, you must create a separate object containing just the node fragment, and pass that object to the <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> method.</span></span>  
  
## <a name="procedures"></a><span data-ttu-id="0a004-106">程序</span><span class="sxs-lookup"><span data-stu-id="0a004-106">Procedures</span></span>  
  
#### <a name="to-transform-a-node-fragment"></a><span data-ttu-id="0a004-107">轉換節點片段</span><span class="sxs-lookup"><span data-stu-id="0a004-107">To transform a node fragment</span></span>  
  
1. <span data-ttu-id="0a004-108">建立包含來源文件的物件。</span><span class="sxs-lookup"><span data-stu-id="0a004-108">Create an object containing the source document.</span></span>  
  
2. <span data-ttu-id="0a004-109">尋找要轉換的節點片段。</span><span class="sxs-lookup"><span data-stu-id="0a004-109">Locate the node fragment you wish to transform.</span></span>  
  
3. <span data-ttu-id="0a004-110">建立僅具有該節點片段的單獨物件。</span><span class="sxs-lookup"><span data-stu-id="0a004-110">Create separate object with just the node fragment.</span></span>  
  
4. <span data-ttu-id="0a004-111">將該節點片段傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="0a004-111">Pass the node fragment to the <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> method.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0a004-112">範例</span><span class="sxs-lookup"><span data-stu-id="0a004-112">Example</span></span>  

 <span data-ttu-id="0a004-113">下列範例會轉換節點片段，並將結果輸出至主控台。</span><span class="sxs-lookup"><span data-stu-id="0a004-113">The following example transforms a node fragment and outputs the results to the console.</span></span>  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### <a name="input"></a><span data-ttu-id="0a004-114">輸入</span><span class="sxs-lookup"><span data-stu-id="0a004-114">Input</span></span>  
  
##### <a name="booksxml"></a><span data-ttu-id="0a004-115">books.xml</span><span class="sxs-lookup"><span data-stu-id="0a004-115">books.xml</span></span>  

 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### <a name="singlexsl"></a><span data-ttu-id="0a004-116">single.xsl</span><span class="sxs-lookup"><span data-stu-id="0a004-116">single.xsl</span></span>  

 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### <a name="output"></a><span data-ttu-id="0a004-117">輸出</span><span class="sxs-lookup"><span data-stu-id="0a004-117">Output</span></span>  

 <span data-ttu-id="0a004-118">書名為《The Confidence Man》。</span><span class="sxs-lookup"><span data-stu-id="0a004-118">Book title is The Confidence Man.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0a004-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0a004-119">See also</span></span>

- [<span data-ttu-id="0a004-120">使用 XslCompiledTransform 類別</span><span class="sxs-lookup"><span data-stu-id="0a004-120">Using the XslCompiledTransform Class</span></span>](using-the-xslcompiledtransform-class.md)

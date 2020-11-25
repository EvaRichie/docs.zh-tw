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
# <a name="how-to-transform-a-node-fragment"></a>作法：轉換節點片段

當您轉換包含於 <xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument> 物件的資料時，XSLT 轉換會套用至整個文件。 換言之，如果您要傳入的節點不是文件的根節點，則不會阻止轉換程序取得已載入文件中的所有節點。 若要轉換節點片段，您必須建立僅含有該節點片段的單獨物件，再將該物件傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-transform-a-node-fragment"></a>轉換節點片段  
  
1. 建立包含來源文件的物件。  
  
2. 尋找要轉換的節點片段。  
  
3. 建立僅具有該節點片段的單獨物件。  
  
4. 將該節點片段傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。  
  
## <a name="example"></a>範例  

 下列範例會轉換節點片段，並將結果輸出至主控台。  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### <a name="input"></a>輸入  
  
##### <a name="booksxml"></a>books.xml  

 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### <a name="singlexsl"></a>single.xsl  

 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### <a name="output"></a>輸出  

 書名為《The Confidence Man》。  
  
## <a name="see-also"></a>另請參閱

- [使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)

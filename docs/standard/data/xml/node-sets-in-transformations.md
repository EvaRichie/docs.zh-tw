---
title: 轉換中的節點集
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: ad034f0e-ff8b-4a71-9a4c-528c754263c4
ms.openlocfilehash: 33cbae05cf35904903189ce767090d3d3cca8e4d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288741"
---
# <a name="node-sets-in-transformations"></a>轉換中的節點集
節點集是 XML 路徑語言 (XPath) 運算式傳回的四種基本資料型別之一。 節點集是一個沒有順序、不重複的節點集合，它依據文件的順序建立，可以指定給樣式表中的變數。  
  
> [!NOTE]
> 在 .NET Framework 2.0 中，<xref:System.Xml.Xsl.XslTransform> 類別已過時。 您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行可延伸樣式表語言轉換 (XSLT)。 如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。  
  
 節點集是 XPath 運算式傳回的四種基本資料型別之一。 節點集是一個沒有順序、不重複的節點集合，它依據文件的順序建立，可以指定給樣式表中的變數。 這個節點集是轉換中 `select` 屬性所使用之 XPath 運算式的結果，具有與 XML 文件物件模型 (DOM) 的節點集相同的行為。 您可以使用[使用 XPathNavigator 巡覽節點集](node-set-navigation-using-xpathnavigator.md)中所顯示的一組方法來巡覽節點集，而不需像 result tree fragment 一樣使用 <xref:System.Xml.XPath.XPathNodeIterator> 進行巡覽。  
  
 下列程式碼範例說明，當樣式表中的 `variable` 或 `parameter` 項目評估為節點集時，應該如何反覆查看節點集。  
  
## <a name="style-sheet"></a>樣式表  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
    <xsl:variable name="x" select="bookstore/book/title"></xsl:variable>  
  
    <xsl:template match="/">  
        <xsl:for-each select="$x">  
            ******  
            <xsl:value-of select="."></xsl:value-of>  
            ******  
        </xsl:for-each>  
    </xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="input"></a>輸入  
  
```xml  
<bookstore>  
   <book style="autobiography">  
      <title>Seven Years in Trenton</title>  
   </book>  
  
   <book style="autobiography">  
      <title>Seven Years in Trenton2</title>  
   </book>  
  
   <book style="textbook">  
      <title>History of Trenton Vol 3</title>  
   </book>  
</bookstore>  
```  
  
## <a name="output"></a>輸出  
  
```output  
******  
Seven Years in Trenton  
******  
  
******  
Seven Years in Trenton2  
******  
  
******  
History of Trenton Vol 3  
******  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.XPath.XPathNodeIterator>
- [使用 XslTransform 類別進行 XSLT 轉換](xslt-transformations-with-the-xsltransform-class.md)
- [XslTransform 類別實作 XSLT 處理器](xsltransform-class-implements-the-xslt-processor.md)

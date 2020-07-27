---
title: LINQ to XML 座標軸概觀 (C#)
description: '瞭解 c # 中的軸方法，也稱為「軸」。 您可以在 LINQ 中查詢 XML 樹狀結構，以尋找專案和屬性，並透過軸來取得其值。'
ms.date: 07/20/2015
ms.assetid: 516792fb-461d-40a8-8a50-9993a51258fc
ms.openlocfilehash: bbda844e8cb2e3b1ff116fd834c6ab1fdd20c1f8
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165450"
---
# <a name="linq-to-xml-axes-overview-c"></a>LINQ to XML 座標軸概觀 (C#)
建立 XML 樹狀結構，或將 XML 文件載入到 XML 樹狀結構後，您可以進行查詢以尋找項目和屬性並擷取其值。 您可以透過「座標軸方法」** 擷取集合，也稱為「座標軸」**。 有些座標軸是 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 類別中，傳回 <xref:System.Collections.Generic.IEnumerable%601> 集合的方法。 有些座標軸是 <xref:System.Xml.Linq.Extensions> 類別中的擴充方法。 當做擴充方法實作的座標軸會在集合上運算，然後傳回集合。  
  
 如 [XElement 類別概觀](./xelement-class-overview.md)中所述，<xref:System.Xml.Linq.XElement> 物件代表單一元素節點。 項目的內容可能很複雜 (有時候稱為結構化的內容)，或者，它可能是簡單的項目。 簡單的項目可以是空的，也可以包含值。 如果節點包含結構化的內容，您可以使用各種座標軸方法來擷取子代項目的列舉。 最常使用的座標軸方法為 <xref:System.Xml.Linq.XContainer.Elements%2A> 和 <xref:System.Xml.Linq.XContainer.Descendants%2A>。  
  
 除了會傳回集合的座標軸方法之外，還有其他兩個常用於 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢的方法。 <xref:System.Xml.Linq.XContainer.Element%2A> 方法會傳回單一的 <xref:System.Xml.Linq.XElement>。 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法會傳回單一的 <xref:System.Xml.Linq.XAttribute>。  
  
 就許多用途而言，LINQ 查詢提供最強大的方式來檢查樹狀結構、將資料從其解壓縮，然後加以轉換。 LINQ 查詢會在執行的物件上運作 <xref:System.Collections.Generic.IEnumerable%601> ，而座標軸會傳回 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> 集合的 <xref:System.Collections.Generic.IEnumerable%601> 以及 <xref:System.Xml.Linq.XAttribute> 集合的。 您需要這些集合，才能執行您的查詢。  
  
 除了擷取項目和屬性之集合的座標軸方法之外，還有其他座標軸方法可讓您仔細逐一查看樹狀結構。 例如，您可以使用樹狀結構的節點，而不是處理項目和屬性。 這些節點是比項目和屬性還要細微的位移單位等級。 使用節點時，您可以檢查 XML 註解、文字節點、處理指示等等。 這個功能對於撰寫字組處理器與想要將文件另存為 XML 之類的人而言，相當重要。 不過，多數的 XML 程式設計人員關心的都是項目、屬性及其值。  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>擷取項目集合的方法  
 下列為 <xref:System.Xml.Linq.XElement> 類別 (或其基礎類別) 之方法的摘要，您可以在 <xref:System.Xml.Linq.XElement> 上呼叫這些方法來傳回項目的集合。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|傳回此項目祖系之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回其祖系具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>|傳回此項目子代之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回其子代具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|傳回此項目的子項目之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回其子項目具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType>|傳回此項目後的項目之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的這個項目後之項目的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType>|傳回此項目前的項目之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的這個項目前之項目的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|傳回此項目及其祖系之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回其項目具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType>|傳回此項目及其子代之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 多載會傳回其項目具有指定之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement> 之 <xref:System.Xml.Linq.XName>。|  
  
## <a name="method-for-retrieving-a-single-element"></a>擷取單一項目的方法  
 下列方法會從 <xref:System.Xml.Linq.XElement> 物件擷取單一子系。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=nameWithType>|傳回具有指定之 <xref:System.Xml.Linq.XElement> 的第一個 <xref:System.Xml.Linq.XName> 子物件。|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>擷取屬性集合的方法  
 下列方法會從 <xref:System.Xml.Linq.XElement> 物件擷取屬性。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|傳回所有屬性之 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XAttribute>。|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>擷取單一屬性的方法  
 下列方法會從 <xref:System.Xml.Linq.XElement> 物件擷取單一屬性。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType>|傳回具有指定之 <xref:System.Xml.Linq.XAttribute> 的 <xref:System.Xml.Linq.XName>。|  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 座標軸 (C#)](linq-to-xml-axes-overview.md)

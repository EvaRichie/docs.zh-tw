---
title: LINQ to XML 軸
ms.date: 07/20/2015
ms.assetid: ecd3bd00-28e5-4517-a59f-53bff39fd478
ms.openlocfilehash: 757c765062b1d1ca1cddb0c559fa46ef6a0fe796
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84368981"
---
# <a name="linq-to-xml-axes-visual-basic"></a>LINQ to XML 軸 (Visual Basic)
建立 XML 樹狀結構，或將 XML 文件載入到 XML 樹狀結構後，您可以進行查詢以尋找項目和屬性並擷取其值。  
  
 在撰寫任何查詢之前，您必須了解 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 座標軸。 有兩種類型的座標軸方法：首先，有可以在單一 <xref:System.Xml.Linq.XElement> 物件、<xref:System.Xml.Linq.XDocument> 物件或 <xref:System.Xml.Linq.XNode> 物件上呼叫的方法。 這些方法會在單一物件上運算，然後傳回 <xref:System.Xml.Linq.XElement>、<xref:System.Xml.Linq.XAttribute> 或 <xref:System.Xml.Linq.XNode> 物件的集合。 第二，在集合上有可運算的擴充方法，並傳回集合。 擴充方法會列舉來源集合、在集合的每個項目上呼叫適當的座標軸方法，然後串連結果。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|說明|  
|-----------|-----------------|  
|[LINQ to XML 軸概觀 (Visual Basic)](linq-to-xml-axes-overview.md)|定義座標軸並說明如何在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢的內容中使用這些座標軸。|  
|[如何：取出元素的集合（LINQ to XML）（Visual Basic）](how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|介紹 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法。 此方法會擷取項目之子項目的集合。|  
|[如何：取出元素的值（LINQ to XML）（Visual Basic）](how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|示範如何取得項目的值。|  
|[如何：篩選元素名稱（LINQ to XML）（Visual Basic）](how-to-filter-on-element-names-linq-to-xml.md)|顯示使用座標軸時，如何在項目名稱上篩選。|  
|[如何：連鎖軸方法呼叫（LINQ to XML）（Visual Basic）](how-to-chain-axis-method-calls-linq-to-xml.md)|示範如何將呼叫鏈結到座標軸方法。|  
|[如何：取出單一子項目（LINQ to XML）（Visual Basic）](how-to-retrieve-a-single-child-element-linq-to-xml.md)|顯示如何擷取項目的單一子項目 (假設有子項目的標記名稱)。|  
|[如何：取出屬性的集合（LINQ to XML）（Visual Basic）](how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|介紹 <xref:System.Xml.Linq.XElement.Attributes%2A> 方法。 這個方法會擷取項目的屬性。|  
|[如何：取出單一屬性（LINQ to XML）（Visual Basic）](how-to-retrieve-a-single-attribute-linq-to-xml.md)|顯示如何擷取項目的單一屬性 (假設有屬性名稱)。|  
|[如何：取出屬性的值（LINQ to XML）（Visual Basic）](how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|示範如何取得屬性的值。|  
|[如何：取出元素的淺層值（Visual Basic）](how-to-retrieve-the-shallow-value-of-an-element.md)|示範如何擷取項目的表層值。|  
|[Visual Basic 中已整合語言的軸心方法 (LINQ to XML)](language-integrated-axes.md)|摘要說明 Visual Basic 的整合式軸。|  
  
## <a name="see-also"></a>另請參閱

- [程式設計指南（LINQ to XML）（Visual Basic）](programming-guide-linq-to-xml.md)

---
title: LINQ to XML 類別概觀 (C#)
description: '本文摘要說明 System.Xml 中 c # 中的 LINQ to XML 類別。Linq 命名空間，其中每個都有簡短的描述。'
ms.date: 07/20/2015
ms.assetid: bf666100-5392-4968-97f4-f6b9d3287d7b
ms.openlocfilehash: 34508f86792cdc7589569b8f12584ffc4379a5fb
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165436"
---
# <a name="linq-to-xml-classes-overview-c"></a>LINQ to XML 類別概觀 (C#)
本主題提供 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 命名空間 (Namespace) 中的 <xref:System.Xml.Linq> 類別 (Class) 清單，以及每個類別的簡短說明。  
  
## <a name="linq-to-xml-classes"></a>LINQ to XML 類別  
  
### <a name="xattribute-class"></a>XAttribute 類別  
 <xref:System.Xml.Linq.XAttribute> 代表 XML 屬性。 如需詳細的資訊和範例，請參閱 [XAttribute 類別概觀 (C#)](./xattribute-class-overview.md)。  
  
### <a name="xcdata-class"></a>XCData 類別  
 <xref:System.Xml.Linq.XCData> 代表 CDATA 文字節點。  
  
### <a name="xcomment-class"></a>XComment 類別  
 <xref:System.Xml.Linq.XComment> 代表 XML 註解。  
  
### <a name="xcontainer-class"></a>XContainer 類別  
 <xref:System.Xml.Linq.XContainer> 對於可能擁有子節點的所有節點而言，是抽象基底類別。 下列類別衍生自 <xref:System.Xml.Linq.XContainer> 類別：  
  
- <xref:System.Xml.Linq.XElement>  
  
- <xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>XDeclaration 類別  
 <xref:System.Xml.Linq.XDeclaration> 代表 XML 宣告。 XML 宣告用於宣告 XML 版本與文件的編碼。 此外，XML 宣告會指定 XML 文件是否為獨立的。 如果文件是獨立的，外部 DTD 或內部子集所參考的外部參數實體 (Entity) 就不會包含任何外部標記宣告。  
  
### <a name="xdocument-class"></a>XDocument 類別  
 <xref:System.Xml.Linq.XDocument> 代表 XML 文件。 如需詳細的資訊和範例，請參閱 [XDocument 類別概觀 (C#)](./xdocument-class-overview.md)。  
  
### <a name="xdocumenttype-class"></a>XDocumentType 類別  
 <xref:System.Xml.Linq.XDocumentType> 代表 XML 文件類型定義 (DTD)。  
  
### <a name="xelement-class"></a>XElement 類別  
 <xref:System.Xml.Linq.XElement> 代表 XML 項目。 如需詳細的資訊和範例，請參閱 [XElement 類別概觀 (C#)](./xelement-class-overview.md)。  
  
### <a name="xname-class"></a>XName 類別  
 <xref:System.Xml.Linq.XName> 代表項目的名稱 (<xref:System.Xml.Linq.XElement>) 與屬性 (<xref:System.Xml.Linq.XAttribute>)。 如需詳細的資訊和範例，請參閱 [XDocument 類別概觀 (C#)](./xdocument-class-overview.md)。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的設計是讓 XML 名稱盡可能直接。 由於其複雜性的緣故，XML 名稱通常被視為 XML 的進階主題。 在論證上，這個複雜性不是來自於開發人員一般用於程式設計的命名空間，而是來自於命名空間前置詞。 命名空間前置詞在減少輸入 XML 時所需的按鍵或在讓 XML 更容易讀取上，可能相當實用。 不過，前置詞通常只是用來使用完整 XML 命名空間的捷徑，因此大部分情況中都不需要。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會將所有前置詞解析為其對應的 XML 命名空間，藉以簡化 XML 名稱。 如果需要前置詞，可透過 <xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A> 方法使用。  
  
 如有需要，可以控制命名空間前置詞。 在某些情況下，如果您要使用其他 XML 系統 (例如，XSLT 或 XAML)，您必須控制命名空間前置詞。 例如，如果您所擁有的 XPath 運算式使用內嵌在 XSLT 樣式表中的命名空間前置詞，您就必須確認 XML 文件有利用符合 XPath 運算式中使用之命名空間前置詞的命名空間前置詞進行序列化。  
  
### <a name="xnamespace-class"></a>XNamespace 類別  
 <xref:System.Xml.Linq.XNamespace> 代表 <xref:System.Xml.Linq.XElement> or <xref:System.Xml.Linq.XAttribute> 的命名空間。 命名空間是 <xref:System.Xml.Linq.XName> 的元件。  
  
### <a name="xnode-class"></a>XNode 類別  
 <xref:System.Xml.Linq.XNode> 是代表 XML 樹狀結構節點的抽象類別。 下列類別衍生自 <xref:System.Xml.Linq.XNode> 類別：  
  
- <xref:System.Xml.Linq.XText>  
  
- <xref:System.Xml.Linq.XContainer>  
  
- <xref:System.Xml.Linq.XComment>  
  
- <xref:System.Xml.Linq.XProcessingInstruction>  
  
- <xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>XNodeDocumentOrderComparer 類別  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer> 會提供功能，針對其文件順序比較節點。  
  
### <a name="xnodeequalitycomparer-class"></a>XNodeEqualityComparer 類別  
 <xref:System.Xml.Linq.XNodeEqualityComparer> 會提供功能，針對值的相等性比較節點。  
  
### <a name="xobject-class"></a>XObject 類別  
 <xref:System.Xml.Linq.XObject> 是 <xref:System.Xml.Linq.XNode> 和 <xref:System.Xml.Linq.XAttribute> 的抽象基底類別。 它提供附註和事件的功能。  
  
### <a name="xobjectchange-class"></a>XObjectChange 類別  
 引發 <xref:System.Xml.Linq.XObjectChange> 的事件時，<xref:System.Xml.Linq.XObject> 會指定事件類型。  
  
### <a name="xobjectchangeeventargs-class"></a>XObjectChangeEventArgs 類別  
 <xref:System.Xml.Linq.XObjectChangeEventArgs> 會提供 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed> 事件的資料。  
  
### <a name="xprocessinginstruction-class"></a>XProcessingInstruction 類別  
 <xref:System.Xml.Linq.XProcessingInstruction> 代表 XML 處理指示。 處理指示會將資訊傳達到處理 XML 的應用程式。  
  
### <a name="xtext-class"></a>XText 類別  
 <xref:System.Xml.Linq.XText> 代表文字節點。 在大部分的情況下，您不必使用這個類別。 這個類別主要用於混合的內容。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 程式設計概觀 (C#)](./linq-to-xml-overview.md)

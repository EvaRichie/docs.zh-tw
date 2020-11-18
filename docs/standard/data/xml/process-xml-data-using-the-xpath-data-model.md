---
title: 使用 XPath 資料模型處理 XML 資料
ms.date: 03/30/2017
ms.assetid: 536c6fce-1453-4654-9c72-bca54d47e081
ms.openlocfilehash: cc35b570c592557658cd3dda0c844847c8b23763
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829280"
---
# <a name="process-xml-data-using-the-xpath-data-model"></a>使用 XPath 資料模型處理 XML 資料
<xref:System.Xml?displayProperty=nameWithType> 命名空間會使用 <xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument> 類別，以程式設計方式來表示 XML 文件、片段、節點或記憶體中的節點集。  
  
 <xref:System.Xml.XPath.XPathDocument> 類別會使用 XPath 資料模型，以快速且唯讀的方式來表示記憶體中的 XML 文件。 <xref:System.Xml.XmlDocument> 類別則會實作 W3C 文件物件模型 (DOM) 層級 1 核心及核心 DOM 層級 2，來呈現記憶體中可編輯的 XML 文件。 這兩個類別都會實作 <xref:System.Xml.XPath.IXPathNavigable> 介面，並傳回用於選取、評估、巡覽，以及可在某些情況下編輯基礎 XML 資料的 <xref:System.Xml.XPath.XPathNavigator> 物件。  
  
 下列各節將根據會傳回 <xref:System.Xml.XPath.XPathNavigator> 類別的類別來說明此類別的功能。  
  
## <a name="in-this-section"></a>本節內容  
 [使用 XPathDocument 及 XmlDocument 讀取 XML 資料](reading-xml-data-using-xpathdocument-and-xmldocument.md)  
 說明如何建立唯讀 <xref:System.Xml.XPath.XPathDocument> 類別物件以讀取 XML 文件，以及如何建立可編輯的 <xref:System.Xml.XmlDocument> 類別物件以讀取及編輯 XML 文件。 本主題還說明如何從每個類別傳回 <xref:System.Xml.XPath.XPathNavigator> 物件，以巡覽及編輯 XML 文件。  
  
 [使用 XPathNavigator 選取、評估及比對 XML 資料](selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)  
 說明 <xref:System.Xml.XPath.XPathNavigator> 類別的方法，其用於使用 XPath 查詢來選取 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中的節點、評估及檢查 XPath 運算式的結果，以及決定 XML 文件中的節點是否符合指定的 XPath 運算式。  
  
 [使用 XPathNavigator 存取 XML 資料](accessing-xml-data-using-xpathnavigator.md)  
 說明 <xref:System.Xml.XPath.XPathNavigator> 類別的方法，其用於巡覽 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中的節點、擷取 XML 資料及存取強型別 XML 資料。  
  
 [使用 XPathNavigator 編輯 XML 資料](editing-xml-data-using-xpathnavigator.md)  
 說明 <xref:System.Xml.XPath.XPathNavigator> 類別的方法，其用於插入、修改及移除 <xref:System.Xml.XmlDocument> 物件中包含之 XML 文件中的節點與值。  
  
 [使用 XPathNavigator 進行結構描述驗證](schema-validation-using-xpathnavigator.md)  
 說明驗證 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 物件中包含之 XML 內容的方式。  
  
## <a name="see-also"></a>請參閱

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [使用 DOM 模型處理 XML 資料](process-xml-data-using-the-dom-model.md)

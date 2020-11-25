---
title: XML 文件物件模型 (DOM) 階層架構
ms.date: 03/30/2017
ms.assetid: 9d187d4f-c76e-4223-a670-cc290783ce47
ms.openlocfilehash: 24ef51a18392fe3034e64bd585d879941fca4b95
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718354"
---
# <a name="xml-document-object-model-dom-hierarchy"></a>XML 文件物件模型 (DOM) 階層架構

下圖顯示 XML 文件物件模型 (DOM) 的類別階層架構，括弧中有全球資訊網協會 (W3C) 名稱和相關的類別名稱。  
  
 ![XML 檔物件模型 &#40;DOM&#41; 階層](media/dom-class-hierarchy.gif "Dom_class_hierarchy")  
XML 文件物件模型 (DOM) 階層  
  
 下列類別不是繼承自 **XmlNode**：  
  
- **XmlImplementation**  
  
- **XmlNamedNodeMap**  
  
- **XmlNodeList**  
  
- **XmlNodeChangedEventArgs**  
  
 **XmlImplementation** 類別是用來建立 XML 文件。 如需詳細資訊，請參閱 [XML 文件建立](xml-document-creation.md)。  
  
 **XmlNamedNodeMap** 類別處理未排序的節點組。 如需詳細資訊，請參閱[根據名稱或索引擷取的未排序節點](unordered-node-retrieval-by-name-or-index.md)。  
  
 **XmlNodeList** 類別處理已排序的節點清單。 如需詳細資訊，請參閱[根據索引擷取的已排序節點](ordered-node-retrieval-by-index.md)。  
  
 **XmlNodeChangedEventArgs** 類別處理在 **XmlDocument** 上註冊的事件處理常式。 如需詳細資訊，請參閱[使用 XmlNodeChangedEventArgs 之 XML 文件中的事件處理](event-handling-in-an-xml-document-using-the-xmlnodechangedeventargs.md)。  
  
 **XmlLinkedNode** 類別繼承自 **XmlNode**。 其目的在於覆寫 **XmlNode** 的兩個方法：**PreviousSibling** 與 **NextSibling** 方法。 這些覆寫的方法會由擁有之前同層級和之後同層級的類別 **XmlCharacterData**、**XmlDeclaration**、**XmlDocumentType**、**XmlElement**、**XmlEntityReference** 和 **XmlProcessingInstruction** 繼承和使用。  
  
## <a name="see-also"></a>另請參閱

- [XML 文件物件模型 (DOM)](xml-document-object-model-dom.md)

---
title: LINQ to XML Annotations2
ms.date: 07/20/2015
ms.assetid: c3e8b3ff-fceb-4428-b0ca-1ed6f128aac8
ms.openlocfilehash: 917129a06483ce2001e178d744440504533d28d6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84369007"
---
# <a name="linq-to-xml-annotations"></a>LINQ to XML 註釋
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的註釋可讓您將任意型別的任意物件與 XML 樹狀結構中的任何 XML 元件產生關聯。  
  
 若要將附註加入到 XML 元件 (例如，<xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute>) 中，您可以呼叫 <xref:System.Xml.Linq.XObject.AddAnnotation%2A> 方法。 您可以按照型別擷取附註。  
  
 請注意，這些附註不是 XML 資訊集的一部分；它們無法進行序列化或還原序列化。  
  
## <a name="methods"></a>方法  
 使用附註時，您可以使用下列方法：  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XObject.AddAnnotation%2A>|將物件加入到 <xref:System.Xml.Linq.XObject> 的附註清單。|  
|<xref:System.Xml.Linq.XObject.Annotation%2A>|從 <xref:System.Xml.Linq.XObject> 取得指定之型別的第一個附註物件。|  
|<xref:System.Xml.Linq.XObject.Annotations%2A>|針對 <xref:System.Xml.Linq.XObject> 取得指定之型別的附註集合。|  
|<xref:System.Xml.Linq.XObject.RemoveAnnotations%2A>|從 <xref:System.Xml.Linq.XObject> 移除指定之型別的附註。|  
  
## <a name="see-also"></a>另請參閱

- [Advanced LINQ to XML 程式設計（Visual Basic）](advanced-linq-to-xml-programming.md)

---
title: 如何：建立 XML 常值
ms.date: 07/20/2015
helpviewer_keywords:
- XML literals [Visual Basic], creating
ms.assetid: 573a6db5-b14d-4e42-b356-8cc7e2d77745
ms.openlocfilehash: c7ad8d684dde31550b6e1b74c098d152b227f6c1
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91058218"
---
# <a name="how-to-create-xml-literals-visual-basic"></a>如何：建立 XML 常值 (Visual Basic)

您可以使用 XML 常值，直接在程式碼中建立 XML 檔、片段或元素。 本主題中的範例將示範如何建立包含三個子項目的 XML 專案，以及如何建立 XML 檔。  
  
 您也可以使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] api 來建立 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 物件。 如需詳細資訊，請參閱<xref:System.Xml.Linq.XElement>。  
  
### <a name="to-create-an-xml-element"></a>若要建立 XML 元素  
  
- 使用 XML 常值語法建立 XML 內嵌，這與實際的 XML 語法相同。  
  
     [!code-vb[VbXMLSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
     執行程式碼。 此程式碼的輸出為：  
  
     `<contact>`  
  
     `<name>Patrick Hines</name>`  
  
     `<phone type="home">206-555-0144</phone>`  
  
     `<phone type="work">425-555-0145</phone>`  
  
     `</contact>`  
  
### <a name="to-create-an-xml-document"></a>建立 XML 檔  
  
- 建立內嵌的 XML 檔。 下列程式碼會建立一個 XML 檔，其中包含常值語法、XML 宣告、處理指示、批註，以及包含其他元素的元素。  
  
     [!code-vb[VbXMLSamples#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#30)]  
  
     執行程式碼。 此程式碼的輸出為：  
  
     `<?xml-stylesheet type="text/xsl" href="show_book.xsl"?>`  
  
     `<!-- Tests that the application works. -->`  
  
     `<books>`  
  
     `<book/>`  
  
     `</books>`  
  
## <a name="see-also"></a>另請參閱

- [XML](index.md)
- [在 Visual Basic 中建立 XML](creating-xml.md)
- [XML 元素常值](../../../language-reference/xml-literals/xml-element-literal.md)
- [XML 文件常值](../../../language-reference/xml-literals/xml-document-literal.md)

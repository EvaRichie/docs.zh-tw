---
title: XML 處理指示常值
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralProcessingInstruction
helpviewer_keywords:
- XML literals [Visual Basic], processing instruction
- XML processing instruction literal [Visual Basic]
- processing instruction literal [Visual Basic]
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
ms.openlocfilehash: 9bd1781e01bc4cbf1ce5da8c454ab2f5a679aead
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400172"
---
# <a name="xml-processing-instruction-literal-visual-basic"></a>XML 處理指示常值 (Visual Basic)
代表物件的常值 <xref:System.Xml.Linq.XProcessingInstruction> 。  
  
## <a name="syntax"></a>語法  
  
```xml  
<?piName [ = piData ] ?>  
```  
  
## <a name="parts"></a>組件  
 `<?`  
 必要。 表示 XML 處理指示常值的開頭。  
  
 `piName`  
 必要。 指出處理指示以哪個應用程式為目標的名稱。 不能以 "xml" 或 "XML" 開頭。  
  
 `piData`  
 選擇性。 字串，指出以為目標的應用程式 `piName` 應該如何處理 XML 檔。  
  
 `?>`  
 必要。 表示處理指示的結尾。  
  
## <a name="return-value"></a>傳回值  
 <xref:System.Xml.Linq.XProcessingInstruction> 物件。  
  
## <a name="remarks"></a>備註  
 XML 處理指示常值指出應用程式應該如何處理 XML 檔。 當應用程式載入 XML 檔時，應用程式可以檢查 XML 處理指示，以決定如何處理檔。 應用程式會解讀和的 `piName` 意義 `piData` 。  
  
 XML 檔常值會使用類似于 XML 處理指示的語法。 如需詳細資訊，請參閱[XML 檔常](xml-document-literal.md)值。  
  
> [!NOTE]
> `piName`元素的開頭不能是 "xml" 或 "xml" 字串，因為 xml 1.0 規格會保留這些識別碼。  
  
 您可以將 XML 處理指示常值指派給變數，或將它包含在 XML 檔常值中。  
  
> [!NOTE]
> XML 常值可以跨越多行，而不需要行接續字元。 這可讓您從 XML 檔案複製內容，並將它直接貼到 Visual Basic 程式中。  
  
 Visual Basic 編譯器會將 XML 處理指示常值轉換為對此函式呼叫的呼叫 <xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A> 。  
  
## <a name="example"></a>範例  
 下列範例會建立一個處理指示，以識別 XML 檔的樣式表單。  
  
 [!code-vb[VbXMLSamples#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#28)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Linq.XProcessingInstruction>
- [XML 文件常值](xml-document-literal.md)
- [XML 常值](index.md)
- [在 Visual Basic 中建立 XML](../../programming-guide/language-features/xml/creating-xml.md)

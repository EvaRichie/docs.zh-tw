---
title: GetXmlNamespace 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.GetXmlNamespace
- GetXmlNamespace
helpviewer_keywords:
- GetXmlNamespace operator [Visual Basic]
- GetXmlNamespace keyword [Visual Basic]
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
ms.openlocfilehash: 660474c1193076755889fd885c1b78bec78f0a2c
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873471"
---
# <a name="getxmlnamespace-operator-visual-basic"></a>GetXmlNamespace 運算子 (Visual Basic)

取得 <xref:System.Xml.Linq.XNamespace> 對應到指定 XML 命名空間前置詞的物件。  
  
## <a name="syntax"></a>Syntax  
  
```vb  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## <a name="parts"></a>組件  

 `xmlNamespacePrefix`  
 選擇性。 識別 XML 命名空間前置詞的字串。 如果有提供，此字串必須是有效的 XML 識別碼。 如需詳細資訊，請參閱宣告 [的 XML 元素和屬性的名稱](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。 如果未指定前置詞，則會傳回預設命名空間。 如果未指定預設命名空間，則會傳回空的命名空間。  
  
## <a name="return-value"></a>傳回值  

 <xref:System.Xml.Linq.XNamespace>對應至 XML 命名空間前置詞的物件。  
  
## <a name="remarks"></a>備註  

 `GetXmlNamespace`運算子 <xref:System.Xml.Linq.XNamespace> 會取得對應至 XML 命名空間前置詞的物件 `xmlNamespacePrefix` 。  
  
 您可以直接在 XML 常值和 XML 軸屬性中使用 XML 命名空間前置詞。 不過，您必須使用 `GetXmlNamespace` 運算子將命名空間前置詞轉換成 <xref:System.Xml.Linq.XNamespace> 物件，才能在程式碼中使用它。 您可以將不合格的元素名稱附加至 <xref:System.Xml.Linq.XNamespace> 物件，以取得 <xref:System.Xml.Linq.XName> 許多方法需要的完整物件 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 。  
  
## <a name="example"></a>範例  

 下列範例會匯入 `ns` 為 XML 命名空間前置詞。 然後，它會使用命名空間的前置詞來建立 XML 常值，並存取具有限定名稱的第一個子節點 `ns:phone` 。 然後，它會將該子節點傳遞至 `ShowName` 副程式，以使用運算子來建立限定名稱 `GetXmlNamespace` 。 然後，副程式會將 `ShowName` 限定名稱傳遞給 <xref:System.Xml.Linq.XNode.Ancestors%2A> 方法，以取得父 `ns:contact` 節點。  
  
 [!code-vb[VbXMLSamples#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/GetXmlNamespace.vb#38)]  
  
 當您呼叫時 `TestGetXmlNamespace.RunSample()` ，它會顯示訊息方塊，其中包含下列文字：  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>另請參閱

- [Imports 陳述式 (XML 命名空間)](../statements/imports-statement-xml-namespace.md)
- [在 Visual Basic 中存取 XML](../../programming-guide/language-features/xml/accessing-xml.md)

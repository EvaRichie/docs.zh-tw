---
title: XML 功能性轉換 (C#)
description: '瞭解如何在 c # 中使用純功能性轉換方法來修改 XML 檔，以及這與程式性方法的不同之處。'
ms.date: 07/20/2015
ms.assetid: 0ccb9251-38d7-44e3-9b84-1b5fe25e4b59
ms.openlocfilehash: 4ccc6859f3663eb3760c7faeaf115a5e88a2278a
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103667"
---
# <a name="functional-transformation-of-xml-c"></a>XML 功能性轉換 (C#)
本主題討論修改 XML 文件的純功能性轉換方法，並與程序性方法對照。  
  
## <a name="modifying-an-xml-document"></a>修改 XML 文件  
 XML 程式設計人員其中一個最常見的工做為，將 XML 從一個組織結構轉換為另一個組織結構。 XML 文件的組織結構就是文件的結構，其中包括：  
  
- 以文件表示的階層。  
  
- 項目和屬性名稱。  
  
- 項目和屬性的資料型別。  
  
 一般而言，將 XML 從一個組織結構轉換為另一個組織結構最有效的方法是，純功能性轉換的方法。 以此種方法，程式設計人員的主要工做為建立適用於整個 XML 文件 (或者一或多個嚴格定義的程式碼) 的轉換。 在論證上，功能性轉換對程式碼而言是最簡單的 (在程式設計人員熟悉方法之後)，它會產生最容易維護的程式碼，而且通常比替代方法更精簡。  
  
### <a name="xml-functional-transformational-technologies"></a>XML 功能性轉換技術  
 Microsoft 提供兩個可用於 XML 文件的功能性轉換技術：XSLT 和 LINQ to XML。 在 <xref:System.Xml.Xsl> Managed 命名空間與 MSXML 的原始 COM 實作中支援 XSLT。 雖然 XSLT 是強大的管理 XML 文件技術，但是它需要特殊領域的專業知識，也就是 XSLT 語言及其支援的 API。  
  
 LINQ to XML 在 C# 或 Visual Basic 程式碼中，提供以明確而且強大的方式撰寫純功能性轉換之程式碼所需的工具。 例如，LINQ to XML 文件中的許多範例都使用純功能性方法。 同時，在[教學課程：管理 WordprocessingML 文件中的內容 (C#)](./shape-of-wordprocessingml-documents.md) 中，我們以功能性方法使用 LINQ to XML 來管理 Microsoft Word 文件中的資訊。  
  
 如需更完整的 LINQ to XML 與其他 Microsoft XML 技術的比較，請參閱[LINQ to XML 與其他 Xml 技術](./linq-to-xml-vs-other-xml-technologies.md)。  
  
當來源文件具有不規則的結構時，XSLT 是文件中心轉換的建議工具。 不過，LINQ to XML 也可以執行文件中心的轉換。 如需詳細資訊，請參閱[如何使用批註以 XSLT 樣式轉換 LINQ to XML 樹狀結構（c #）](./how-to-use-annotations-to-transform-linq-to-xml-trees-in-an-xslt-style.md)。
  
## <a name="see-also"></a>請參閱

- [純函數式轉換簡介 (C#)](./introduction-to-pure-functional-transformations.md)
- [教學課程：管理 WordprocessingML 文件中的內容 (C#)](./shape-of-wordprocessingml-documents.md)
- [LINQ to XML 比較其他 XML 技術之比較](./linq-to-xml-vs-other-xml-technologies.md)

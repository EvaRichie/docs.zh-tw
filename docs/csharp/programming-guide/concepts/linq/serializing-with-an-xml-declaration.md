---
title: 使用 XML 宣告序列化 (C#)
description: '瞭解 c # 中的序列化會產生 XML 宣告的設定，包括序列化為檔案、不帶和 XmlWriter。'
ms.date: 07/20/2015
ms.assetid: c237fa4a-a042-40fd-886f-17b54c66bb75
ms.openlocfilehash: 7e91b61f037d28149f7c2355f4233dc319b54627
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302356"
---
# <a name="serializing-with-an-xml-declaration-c"></a>使用 XML 宣告序列化 (C#)
這個主題描述如何控制序列化是否產生 XML 宣告。  
  
## <a name="xml-declaration-generation"></a>XML 宣告產生  
 使用 <xref:System.IO.File> 方法或 <xref:System.IO.TextWriter> 方法序列化為 <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType> 或 <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType> 會產生 XML 宣告。 當您序列化為 <xref:System.Xml.XmlWriter> 時，寫入器設定 (在 <xref:System.Xml.XmlWriterSettings> 物件中指定) 會決定是否產生 XML 宣告。  
  
 如果您要使用 `ToString` 方法序列化為字串，所產生的 XML 將不會包含 XML 宣告。  
  
### <a name="serializing-with-an-xml-declaration"></a>使用 XML 宣告進行序列化  
 下列範例會建立 <xref:System.Xml.Linq.XElement>、將文件儲存為檔案，然後將檔案列印到主控台：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", "child content")  
);  
root.Save("Root.xml");  
string str = File.ReadAllText("Root.xml");  
Console.WriteLine(str);  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>不使用 XML 宣告序列化  
 下列範例顯示如何將 <xref:System.Xml.Linq.XElement> 儲存為 <xref:System.Xml.XmlWriter>。  
  
```csharp  
StringBuilder sb = new StringBuilder();  
XmlWriterSettings xws = new XmlWriterSettings();  
xws.OmitXmlDeclaration = true;  
  
using (XmlWriter xw = XmlWriter.Create(sb, xws)) {  
    XElement root = new XElement("Root",  
        new XElement("Child", "child content")  
    );  
    root.Save(xw);  
}  
Console.WriteLine(sb.ToString());  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>另請參閱

- [序列化 XML 樹狀結構 (C#)](serializing-to-files-textwriters-and-xmlwriters.md)

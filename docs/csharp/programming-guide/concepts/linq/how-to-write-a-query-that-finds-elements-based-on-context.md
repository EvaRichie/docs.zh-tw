---
title: '如何撰寫可根據內容尋找專案的查詢（c #）'
description: 瞭解如何撰寫查詢，以根據內容來尋找元素。 請參閱程式碼範例，並查看其他資源。
ms.date: 07/20/2015
ms.assetid: 3ff79ef0-fc8b-42fe-8cc0-10dc32b06b4e
ms.openlocfilehash: 64f09a41c2c1d01b0be8f776461f9be9df9ecb5f
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303188"
---
# <a name="how-to-write-a-query-that-finds-elements-based-on-context-c"></a>如何撰寫可根據內容尋找專案的查詢（c #）
有時候您可能必須撰寫會依其內容選取項目的查詢。 您可能想要依據前面或後面的同層級項目進行篩選。 您可能想要依據子系或祖系項目進行篩選。  
  
 您僅能撰寫查詢並使用 `where` 子句中的查詢結果來達到這個目的。 如果您必須先依據 Null 進行測試，然後再測試值，在 `let` 子句中進行查詢，然後使用 `where` 子句中的結果會比較方便。  
  
## <a name="example"></a>範例  
 下列範例會選取緊跟著 `p` 項目後面的所有 `ul` 項目。  
  
```csharp  
XElement doc = XElement.Parse(@"<Root>  
    <p id=""1""/>  
    <ul>abc</ul>  
    <Child>  
        <p id=""2""/>  
        <notul/>  
        <p id=""3""/>  
        <ul>def</ul>  
        <p id=""4""/>  
    </Child>  
    <Child>  
        <p id=""5""/>  
        <notul/>  
        <p id=""6""/>  
        <ul>abc</ul>  
        <p id=""7""/>  
    </Child>  
</Root>");  
  
IEnumerable<XElement> items =  
    from e in doc.Descendants("p")  
    let z = e.ElementsAfterSelf().FirstOrDefault()  
    where z != null && z.Name.LocalName == "ul"  
    select e;  
  
foreach (XElement e in items)  
    Console.WriteLine("id = {0}", (string)e.Attribute("id"));  
```  
  
 此程式碼會產生下列輸出：  
  
```output  
id = 1  
id = 3  
id = 6  
```  
  
## <a name="example"></a>範例  
 下列範例顯示命名空間中之 XML 的相同查詢。 如需詳細資訊，請參閱[命名空間概觀 (LINQ to XML) (C#)](namespaces-overview-linq-to-xml.md)。  
  
```csharp  
XElement doc = XElement.Parse(@"<Root xmlns='http://www.adatum.com'>  
    <p id=""1""/>  
    <ul>abc</ul>  
    <Child>  
        <p id=""2""/>  
        <notul/>  
        <p id=""3""/>  
        <ul>def</ul>  
        <p id=""4""/>  
    </Child>  
    <Child>  
        <p id=""5""/>  
        <notul/>  
        <p id=""6""/>  
        <ul>abc</ul>  
        <p id=""7""/>  
    </Child>  
</Root>");  
  
XNamespace ad = "http://www.adatum.com";  
  
IEnumerable<XElement> items =  
    from e in doc.Descendants(ad + "p")  
    let z = e.ElementsAfterSelf().FirstOrDefault()  
    where z != null && z.Name == ad.GetName("ul")  
    select e;  
  
foreach (XElement e in items)  
    Console.WriteLine("id = {0}", (string)e.Attribute("id"));  
```  
  
 此程式碼會產生下列輸出：  
  
```output  
id = 1  
id = 3  
id = 6  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Linq.XElement.Parse%2A>
- <xref:System.Xml.Linq.XContainer.Descendants%2A>
- <xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A>
- <xref:System.Linq.Enumerable.FirstOrDefault%2A>

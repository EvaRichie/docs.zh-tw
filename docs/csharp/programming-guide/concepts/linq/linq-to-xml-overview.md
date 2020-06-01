---
title: LINQ to XML 概觀 (C#)
ms.date: 10/30/2018
ms.assetid: 716b94d3-0091-4de1-8e05-41bc069fa9dd
ms.openlocfilehash: dd41d8607ef3f2e6e6be9a1f3964ef0ae937e2ac
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241834"
---
# <a name="linq-to-xml-overview-c"></a>LINQ to XML 概觀 (C#)

LINQ to XML 提供運用 .NET Language-Integrated Query (LINQ) Framework 的記憶體中 XML 程式開發介面。 LINQ to XML 會使用 .NET 功能，而且相當於更新的、重新設計的文件物件模型 (DOM) XML 程式發展介面。

XML 已被廣泛採用為格式化許多內容之資料的方式。 例如，您可以在 Web、組態檔、Microsoft Office Word 檔案與資料庫中發現 XML。

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 是經過重新設計，用以進行 XML 程式設計的最新方法。 它提供檔物件模型（DOM）的記憶體中檔修改功能，並支援 LINQ 查詢運算式。 雖然這些查詢運算式在語法上與 XPath 不同，但是它們會提供類似的功能。

## <a name="linq-to-xml-developers"></a>LINQ to XML 開發人員

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的目標為各種開發人員。 對於只想要完成某些事情的一般開發人員而言，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會提供類似 SQL 的查詢經驗，讓 XML 更容易。 只要稍微研究，程式設計人員就可以學會如何以自己選擇的程式語言來撰寫簡潔而且功能強大的查詢。

專業開發人員可以使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 大量增加其產能。 他們可以利用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 撰寫更明確、更精簡而且功能更強大的較少程式碼。 他們可以同時使用多個資料網域的查詢運算式。

## <a name="what-is-linq-to-xml"></a>何謂 LINQ to XML？

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]是啟用 LINQ 的記憶體內部 XML 程式設計介面，可讓您從 .NET 程式設計語言內使用 XML。

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 如同文件物件模型 (DOM)，它會將 XML 文件帶到記憶體中。 您可以查詢與修改文件，並在修改後儲存到檔案，或將其序列化並透過網際網路傳送。 不過，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 與 DOM 不同：它所提供的新物件模型較為輕量且更容易使用，而且會利用 C# 的語言功能。

最重要的優點 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 是它與語言整合式查詢（LINQ）的整合。 這種整合可讓您在記憶體中 XML 文件上撰寫查詢以擷取項目和屬性的集合。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的查詢功能相當於 (雖然語法上不同) XPath 和 Xquery 的功能。 C # 中的 LINQ 整合提供更強的類型、編譯時間檢查，以及改善的偵錯工具支援。

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的另一項優點是將查詢結果當做 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XAttribute> 物件建構函式參數的功能，可提供建立 XML 樹狀結構的強大方法。 此方法稱為「功能建構」**，可讓開發人員輕鬆將 XML 樹狀結構從某種圖形轉換為另一種圖形。

例如，您可能具有[ XML 檔範例：典型訂購單 (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml-1.md) 中所述的典型 XML 訂購單。 您可以使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 執行下列查詢，以便在採購訂單中取得每個項目的零件編號屬行值：

```csharp
// Load the XML file from our project directory containing the purchase orders
var filename = "PurchaseOrder.xml";
var currentDirectory = Directory.GetCurrentDirectory();
var purchaseOrderFilepath = Path.Combine(currentDirectory, filename);

XElement purchaseOrder = XElement.Load(purchaseOrderFilepath);

IEnumerable<string> partNos =  from item in purchaseOrder.Descendants("Item")
                               select (string) item.Attribute("PartNumber");
```

這可以用方法語法的形式改寫：

```csharp
IEnumerable<string> partNos = purchaseOrder.Descendants("Item").Select(x => (string) x.Attribute("PartNumber"));
```

另一個範例是，您可能會想要一份值大於 $100 之項目的清單 (以零件編號排序)。 若要取得此資訊，您可以執行下列查詢：

```csharp
// Load the XML file from our project directory containing the purchase orders
var filename = "PurchaseOrder.xml";
var currentDirectory = Directory.GetCurrentDirectory();
var purchaseOrderFilepath = Path.Combine(currentDirectory, filename);

XElement purchaseOrder = XElement.Load(purchaseOrderFilepath);

IEnumerable<XElement> pricesByPartNos =  from item in purchaseOrder.Descendants("Item")
                                 where (int) item.Element("Quantity") * (decimal) item.Element("USPrice") > 100
                                 orderby (string)item.Element("PartNumber")
                                 select item;
```

同樣地，這可以用方法語法的形式改寫：

```csharp
IEnumerable<XElement> pricesByPartNos = purchaseOrder.Descendants("Item")
                                        .Where(item => (int)item.Element("Quantity") * (decimal)item.Element("USPrice") > 100)
                                        .OrderBy(order => order.Element("PartNumber"));
```

除了這些 LINQ 功能之外， [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 還提供改良的 XML 程式設計介面。 利用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]，您可以：

- [從檔案](how-to-load-xml-from-a-file.md)或[資料流程](how-to-stream-xml-fragments-from-an-xmlreader.md)載入 XML。

- 將 XML 序列化為檔案或資料流。

- 使用功能結構從頭開始建立 XML。

- 使用類似 XPath 的座標軸查詢 XML。

- 使用 <xref:System.Xml.Linq.XContainer.Add%2A>、<xref:System.Xml.Linq.XNode.Remove%2A>、<xref:System.Xml.Linq.XNode.ReplaceWith%2A> 和 <xref:System.Xml.Linq.XElement.SetValue%2A> 之類的方法管理記憶體中 XML 樹狀結構。

- 使用 XSD 驗證 XML 樹狀結構。

- 使用這些功能的組合，將 XML 樹狀結構從一個組織結構轉換為另一個組織結構。

## <a name="creating-xml-trees"></a>建立 XML 樹狀結構

使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 進行程式設計其中一項最重要的優點是，建立 XML 樹狀結構很容易。 例如，若要建立小型 XML 樹狀結構，您可以使用下列方式來撰寫程式碼：

```csharp
XElement contacts =
new XElement("Contacts",
    new XElement("Contact",
        new XElement("Name", "Patrick Hines"),
        new XElement("Phone", "206-555-0144",
            new XAttribute("Type", "Home")),
        new XElement("phone", "425-555-0145",
            new XAttribute("Type", "Work")),
        new XElement("Address",
            new XElement("Street1", "123 Main St"),
            new XElement("City", "Mercer Island"),
            new XElement("State", "WA"),
            new XElement("Postal", "68042")
        )
    )
);
```

如需詳細資訊，請參閱[建立 XML 樹狀結構 (C#)](./creating-xml-trees-linq-to-xml-2.md)。

## <a name="see-also"></a>另請參閱

- [參考 (LINQ to XML)](./reference-linq-to-xml.md)
- [LINQ to XML 與 DOM 的比較（c #）](./linq-to-xml-vs-dom.md)
- [LINQ to XML 比較其他 XML 技術之比較](./linq-to-xml-vs-other-xml-technologies.md)
- <xref:System.Xml.Linq>

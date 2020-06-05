---
title: 作法：聯結兩個集合 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 5a5758d4-906b-4285-908d-5b930db192e6
ms.openlocfilehash: dc3cfd19d990fa81e00f4781cb15bf07eb9a80ea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398047"
---
# <a name="how-to-join-two-collections-linq-to-xml-visual-basic"></a>如何：聯結兩個集合（LINQ to XML）（Visual Basic）
XML 文件中的項目或屬性有時候會參考其他項目或屬性。 例如，[範例 XML 檔：客戶和訂單 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md) XML 文件包含客戶清單與訂單清單。 每個 `Customer` 項目都包含一個 `CustomerID` 屬性。 每個 `Order` 項目都包含一個 `CustomerID` 項目。 每個訂單中的 `CustomerID` 項目都會參考客戶中的 `CustomerID` 屬性。  
  
 [範例 XSD 檔：客戶和訂單](sample-xsd-file-customers-and-orders.md)主題包含可用於驗證此文件的 XSD。 它會使用 XSD 的 `xs:key` 和 `xs:keyref` 功能來建立 `CustomerID` 項目的 `Customer` 屬性為索引鍵，並在每個 `CustomerID` 項目中的 `Order` 項目和每個 `CustomerID` 項目中的 `Customer` 屬性之間建立關聯性。  
  
 利用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]，您可以使用 `Join` 子句來利用此關聯性。  
  
 請注意，因為沒有可用的索引，所以這種聯結的執行階段效能會比較差。  
  
 如需有關的詳細資訊 `Join` ，請參閱[聯結作業（Visual Basic）](join-operations.md)。  
  
## <a name="example"></a>範例  
 下列範例會將 `Customer` 項目聯結到 `Order` 項目，並在訂單中產生包含 `CompanyName` 項目的新 XML 文件。  
  
 執行查詢前，此範例會驗證文件是否使用[範例 XSD 檔：客戶和訂單](sample-xsd-file-customers-and-orders.md)中的結構描述進行編譯。 這可確保聯結子句永遠可以運作。  
  
 此查詢會先擷取所有 `Customer` 項目，然後將這些項目聯結到 `Order` 項目。 它僅會選取 `CustomerID` 大於 "K" 之客戶的訂單。 接著，它會規劃包含每個訂單內客戶資訊的新 `Order` 項目。  
  
 此範例使用下列 XML 文件︰[範例 XML 檔：客戶和訂單 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)。  
  
 此範例使用下列 XSD 結構描述︰[範例 XSD 檔：客戶和訂單](sample-xsd-file-customers-and-orders.md)。  
  
 請注意，以這種方式聯結的效能不會很好。 聯結會透過線性搜尋執行。 沒有雜湊資料表或索引協助執行。  
  
```vb  
Public Class Program  
    Public Shared errors As Boolean = False  
  
    Public Shared Function LamValidEvent(ByVal o As Object, _  
                 ByVal e As ValidationEventArgs) As Boolean  
        Console.WriteLine("{0}", e.Message)  
        errors = True  
    End Function  
  
    Shared Sub Main()  
        Dim schemas As New XmlSchemaSet()  
        schemas.Add("", "CustomersOrders.xsd")  
  
        Console.Write("Attempting to validate, ")  
        Dim custOrdDoc As XDocument = XDocument.Load("CustomersOrders.xml")  
  
        custOrdDoc.Validate(schemas, Function(o, e) LamValidEvent(0, e))  
        If errors Then  
            Console.WriteLine("custOrdDoc did not validate")  
        Else  
            Console.WriteLine("custOrdDoc validated")  
        End If  
  
        If Not errors Then  
            'Join customers and orders, and create a new XML document with  
            ' a different shape.  
            'The new document contains orders only for customers with a  
            ' CustomerID > 'K'.  
            Dim custOrd As XElement = custOrdDoc.<Root>.FirstOrDefault  
            Dim newCustOrd As XElement = _  
                <Root>  
                    <%= From c In custOrd.<Customers>.<Customer> _  
                        Join o In custOrd.<Orders>.<Order> _  
                        On c.@CustomerID Equals o.<CustomerID>.Value _  
                        Where c.@CustomerID.CompareTo("K") > 0 _  
                        Select _  
                        <Order>  
                            <CustomerID><%= c.@CustomerID %></CustomerID>  
                            <%= c.<CompanyName> %>  
                            <%= c.<ContactName> %>  
                            <%= o.<EmployeeID> %>  
                            <%= o.<OrderDate> %>  
                        </Order> _  
                    %>  
                </Root>  
            Console.WriteLine(newCustOrd)  
        End If  
    End Sub  
End Class  
```  
  
 此程式碼會產生下列輸出：  
  
```console
Attempting to validate, custOrdDoc validated  
<Root>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-03-21T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-05-22T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-06-25T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-10-27T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>6</EmployeeID>  
    <OrderDate>1997-11-10T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>4</EmployeeID>  
    <OrderDate>1998-02-12T00:00:00</OrderDate>  
  </Order>  
</Root>  
```  
  
## <a name="see-also"></a>另請參閱

- [先進的查詢技術（LINQ to XML）（Visual Basic）](advanced-query-techniques-linq-to-xml.md)

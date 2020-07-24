---
title: '如何從 XML 產生文字檔（c #）'
description: '瞭解如何從 c # 中的 XML 檔案產生 .csv 檔案。 這個範例會使用方法語法和匯總運算子。'
ms.date: 07/20/2015
ms.assetid: 9ad283f7-7cac-42ff-bf32-92aa866e6883
ms.openlocfilehash: a6e9ce803ddfac3f1609d60a4f51661232cbb2f4
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105065"
---
# <a name="how-to-generate-text-files-from-xml-c"></a><span data-ttu-id="38de5-104">如何從 XML 產生文字檔（c #）</span><span class="sxs-lookup"><span data-stu-id="38de5-104">How to generate text files from XML (C#)</span></span>
<span data-ttu-id="38de5-105">此範例顯示如何從 XML 檔案產生以逗號分隔的 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="38de5-105">This example shows how to generate a comma-separated values (CSV) file from an XML file.</span></span>  
  
## <a name="example"></a><span data-ttu-id="38de5-106">範例</span><span class="sxs-lookup"><span data-stu-id="38de5-106">Example</span></span>  
 <span data-ttu-id="38de5-107">此範例的 C# 版本會使用方法語法和 `Aggregate` 運算子，以單一運算式產生 XML 文件的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="38de5-107">The C# version of this example uses method syntax and the `Aggregate` operator to generate a CSV file from an XML document in a single expression.</span></span> <span data-ttu-id="38de5-108">如需詳細資訊，請參閱 [LINQ 中的查詢語法及方法語法](./query-syntax-and-method-syntax-in-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="38de5-108">For more information, see [Query Syntax and Method Syntax in LINQ](./query-syntax-and-method-syntax-in-linq.md).</span></span>  
  
 <span data-ttu-id="38de5-109">此範例使用下列 XML 文件︰[範例 XML 檔：客戶和訂單 (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md)。</span><span class="sxs-lookup"><span data-stu-id="38de5-109">This example uses the following XML document: [Sample XML File: Customers and Orders (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).</span></span>  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
string csv =  
    (from el in custOrd.Element("Customers").Elements("Customer")  
    select  
        String.Format("{0},{1},{2},{3},{4},{5},{6},{7},{8},{9}{10}",  
            (string)el.Attribute("CustomerID"),  
            (string)el.Element("CompanyName"),  
            (string)el.Element("ContactName"),  
            (string)el.Element("ContactTitle"),  
            (string)el.Element("Phone"),  
            (string)el.Element("FullAddress").Element("Address"),  
            (string)el.Element("FullAddress").Element("City"),  
            (string)el.Element("FullAddress").Element("Region"),  
            (string)el.Element("FullAddress").Element("PostalCode"),  
            (string)el.Element("FullAddress").Element("Country"),  
            Environment.NewLine  
        )  
    )  
    .Aggregate(  
        new StringBuilder(),  
        (sb, s) => sb.Append(s),  
        sb => sb.ToString()  
    );  
Console.WriteLine(csv);  
```  
  
 <span data-ttu-id="38de5-110">此程式碼會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="38de5-110">This code produces the following output:</span></span>  
  
```output  
GREAL,Great Lakes Food Market,Howard Snyder,Marketing Manager,(503) 555-7555,2732 Baker Blvd.,Eugene,OR,97403,USA  
HUNGC,Hungry Coyote Import Store,Yoshi Latimer,Sales Representative,(503) 555-6874,City Center Plaza 516 Main St.,Elgin,OR,97827,USA  
LAZYK,Lazy K Kountry Store,John Steel,Marketing Manager,(509) 555-7969,12 Orchestra Terrace,Walla Walla,WA,99362,USA  
LETSS,Let's Stop N Shop,Jaime Yorres,Owner,(415) 555-5938,87 Polk St. Suite 5,San Francisco,CA,94117,USA  
```  
  
## <a name="see-also"></a><span data-ttu-id="38de5-111">請參閱</span><span class="sxs-lookup"><span data-stu-id="38de5-111">See also</span></span>

- [<span data-ttu-id="38de5-112">投影和轉換 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="38de5-112">Projections and Transformations (LINQ to XML) (C#)</span></span>](how-to-work-with-dictionaries-using-linq-to-xml.md)

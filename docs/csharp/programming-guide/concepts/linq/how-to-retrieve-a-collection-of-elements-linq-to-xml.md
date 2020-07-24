---
title: '如何取出元素的集合（LINQ to XML）（c #）'
description: 'C # 中的 Elements 方法會抓取元素的子項目集合。 這個 LINQ to XML 範例會逐一查看專案的子項目。'
ms.date: 07/20/2015
ms.assetid: b849668c-7976-4974-b8e1-1cd587d34258
ms.openlocfilehash: 4f9b6ae4713af9ce1a4eeb5257f57cd9724f68b2
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103360"
---
# <a name="how-to-retrieve-a-collection-of-elements-linq-to-xml-c"></a><span data-ttu-id="c997a-104">如何取出元素的集合（LINQ to XML）（c #）</span><span class="sxs-lookup"><span data-stu-id="c997a-104">How to retrieve a collection of elements (LINQ to XML) (C#)</span></span>
<span data-ttu-id="c997a-105">這個主題會示範 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="c997a-105">This topic demonstrates the <xref:System.Xml.Linq.XContainer.Elements%2A> method.</span></span> <span data-ttu-id="c997a-106">此方法會擷取項目之子項目的集合。</span><span class="sxs-lookup"><span data-stu-id="c997a-106">This method retrieves a collection of the child elements of an element.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c997a-107">範例</span><span class="sxs-lookup"><span data-stu-id="c997a-107">Example</span></span>  
 <span data-ttu-id="c997a-108">此範例會逐一查看 `purchaseOrder` 項目的子項目。</span><span class="sxs-lookup"><span data-stu-id="c997a-108">This example iterates through the child elements of the `purchaseOrder` element.</span></span>  
  
 <span data-ttu-id="c997a-109">此範例使用下列 XML 文件︰[範例 XML 檔：典型採購訂單 (LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md)。</span><span class="sxs-lookup"><span data-stu-id="c997a-109">This example uses the following XML document: [Sample XML File: Typical Purchase Order (LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md).</span></span>  
  
```csharp  
XElement po = XElement.Load("PurchaseOrder.xml");  
IEnumerable<XElement> childElements =  
    from el in po.Elements()  
    select el;  
foreach (XElement el in childElements)  
    Console.WriteLine("Name: " + el.Name);  
```  
  
 <span data-ttu-id="c997a-110">此範例會產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="c997a-110">This example produces the following output.</span></span>  
  
```output  
Name: Address  
Name: Address  
Name: DeliveryNotes  
Name: Items  
```  
  
## <a name="see-also"></a><span data-ttu-id="c997a-111">請參閱</span><span class="sxs-lookup"><span data-stu-id="c997a-111">See also</span></span>

- [<span data-ttu-id="c997a-112">LINQ to XML 座標軸 (C#)</span><span class="sxs-lookup"><span data-stu-id="c997a-112">LINQ to XML Axes (C#)</span></span>](./linq-to-xml-axes-overview.md)

---
title: 作法：擷取項目的淺層值
ms.date: 07/20/2015
ms.assetid: 730a6670-fb8c-41fc-8a1b-eb97a837e432
ms.openlocfilehash: 24e6b128481f56941f0a61da9766f02813a46e97
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397813"
---
# <a name="how-to-retrieve-the-shallow-value-of-an-element-visual-basic"></a><span data-ttu-id="26eec-102">如何：取出元素的淺層值（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="26eec-102">How to: Retrieve the Shallow Value of an Element (Visual Basic)</span></span>

<span data-ttu-id="26eec-103">本主題說明如何取得項目的表層值。</span><span class="sxs-lookup"><span data-stu-id="26eec-103">This topic shows how to get the shallow value of an element.</span></span> <span data-ttu-id="26eec-104">表層值僅是特定項目的值。與深層值不同的是，深層值包含了由所有子代項目連結成單一字串的值。</span><span class="sxs-lookup"><span data-stu-id="26eec-104">The shallow value is the value of the specific element only, as opposed to the deep value, which includes the values of all descendent elements concatenated into a single string.</span></span>

<span data-ttu-id="26eec-105">當您使用轉換或 <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> 屬性，您擷取的是深層值。</span><span class="sxs-lookup"><span data-stu-id="26eec-105">When you retrieve an element value by using either casting or the <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> property, you retrieve the deep value.</span></span> <span data-ttu-id="26eec-106">若要擷取表層值，您可以使用 `ShallowValue` 擴充方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="26eec-106">To retrieve the shallow value, you can use the `ShallowValue` extension method, as shown in the following example.</span></span> <span data-ttu-id="26eec-107">當您想要根據項目的內容進行選取時，擷取表層值就非常有用。</span><span class="sxs-lookup"><span data-stu-id="26eec-107">Retrieving the shallow value is useful when you want to select elements based on their content.</span></span>

<span data-ttu-id="26eec-108">下列範例會宣告擷取項目表層值的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="26eec-108">The following example declares an extension method that retrieves the shallow value of an element.</span></span> <span data-ttu-id="26eec-109">接著會在查詢中使用此擴充方法，將所有包含計算值的項目列出。</span><span class="sxs-lookup"><span data-stu-id="26eec-109">It then uses the extension method in a query to list all elements that contain a calculated value.</span></span>

## <a name="example"></a><span data-ttu-id="26eec-110">範例</span><span class="sxs-lookup"><span data-stu-id="26eec-110">Example</span></span>

<span data-ttu-id="26eec-111">下列文字檔 Report.xml 是此範例的原始檔。</span><span class="sxs-lookup"><span data-stu-id="26eec-111">The following text file, Report.xml, is the source for this example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Report>
  <Section>
    <Heading>
      <Column Name="CustomerId">=Customer.CustomerId.Heading</Column>
      <Column Name="Name">=Customer.Name.Heading</Column>
    </Heading>
    <Detail>
      <Column Name="CustomerId">=Customer.CustomerId</Column>
      <Column Name="Name">=Customer.Name</Column>
    </Detail>
  </Section>
</Report>
```

```vb
Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function ShallowValue(ByVal xe As XElement)
        Return xe _
               .Nodes() _
               .OfType(Of XText)() _
               .Aggregate(New StringBuilder(), _
                              Function(s, c) s.Append(c), _
                              Function(s) s.ToString())
    End Function

    Sub Main()
        Dim root As XElement = XElement.Load("Report.xml")

        Dim query As IEnumerable(Of XElement) = _
            From el In root.Descendants() _
            Where (el.ShallowValue().StartsWith("=")) _
            Select el

        For Each q As XElement In query
            Console.WriteLine("{0}{1}{2}", _
                q.Name.ToString().PadRight(8), _
                q.Attribute("Name").ToString().PadRight(20), _
                q.ShallowValue())
        Next
    End Sub
End Module
```

<span data-ttu-id="26eec-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="26eec-112">This example produces the following output:</span></span>

```console
Column  Name="CustomerId"   =Customer.CustomerId.Heading
Column  Name="Name"         =Customer.Name.Heading
Column  Name="CustomerId"   =Customer.CustomerId
Column  Name="Name"         =Customer.Name
```

## <a name="see-also"></a><span data-ttu-id="26eec-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="26eec-113">See also</span></span>

- [<span data-ttu-id="26eec-114">LINQ to XML 軸 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="26eec-114">LINQ to XML Axes (Visual Basic)</span></span>](linq-to-xml-axes.md)

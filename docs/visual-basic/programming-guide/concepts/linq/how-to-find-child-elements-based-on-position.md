---
title: 作法：根據位置尋找子項目 (XPath-LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 6831e1db-5e97-444f-a7a1-d0a87104b005
ms.openlocfilehash: d6dd1150ae3e4ad586e476b777b1f7d47d60c261
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405257"
---
# <a name="how-to-find-child-elements-based-on-position-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="deb1e-102">如何：根據位置尋找子項目（XPath-LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="deb1e-102">How to: Find Child Elements Based on Position (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="deb1e-103">有時候您會想要根據項目的位置尋找這些項目。</span><span class="sxs-lookup"><span data-stu-id="deb1e-103">Sometimes you want to find elements based on their position.</span></span> <span data-ttu-id="deb1e-104">您可能想要尋找第二個項目，或者想要尋找第三到第五個項目。</span><span class="sxs-lookup"><span data-stu-id="deb1e-104">You might want to find the second element, or you might want to find the third through the fifth element.</span></span>  
  
 <span data-ttu-id="deb1e-105">XPath 運算式為：</span><span class="sxs-lookup"><span data-stu-id="deb1e-105">The XPath expression is:</span></span>  
  
 `Test[position() >= 2 and position() <= 4]`  
  
 <span data-ttu-id="deb1e-106">以延遲的方式撰寫這個 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="deb1e-106">There are two approaches to writing this [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] query in a lazy way.</span></span> <span data-ttu-id="deb1e-107">您可以使用 <xref:System.Linq.Enumerable.Skip%2A> 和 <xref:System.Linq.Enumerable.Take%2A> 運算子，或者，您可以使用採用索引的 <xref:System.Linq.Enumerable.Where%2A> 多載。</span><span class="sxs-lookup"><span data-stu-id="deb1e-107">You can use the <xref:System.Linq.Enumerable.Skip%2A> and <xref:System.Linq.Enumerable.Take%2A> operators, or you can use the <xref:System.Linq.Enumerable.Where%2A> overload that takes an index.</span></span> <span data-ttu-id="deb1e-108">當您使用 <xref:System.Linq.Enumerable.Where%2A> 多載時，您可以使用採用兩個引數的 Lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="deb1e-108">When you use the <xref:System.Linq.Enumerable.Where%2A> overload, you use a lambda expression that takes two arguments.</span></span> <span data-ttu-id="deb1e-109">下列範例顯示根據位置進行選擇的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="deb1e-109">The following example shows both methods of selecting based on position.</span></span>  
  
## <a name="example"></a><span data-ttu-id="deb1e-110">範例</span><span class="sxs-lookup"><span data-stu-id="deb1e-110">Example</span></span>  
 <span data-ttu-id="deb1e-111">這個範例會尋找第二到第四個 `Test` 項目。</span><span class="sxs-lookup"><span data-stu-id="deb1e-111">This example finds the second through the fourth `Test` element.</span></span> <span data-ttu-id="deb1e-112">結果為項目的集合。</span><span class="sxs-lookup"><span data-stu-id="deb1e-112">The result is a collection of elements.</span></span>  
  
 <span data-ttu-id="deb1e-113">此範例使用下列 XML 文件︰[範例 XML 檔：測試組態 (LINQ to XML)](sample-xml-file-test-configuration-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="deb1e-113">This example uses the following XML document: [Sample XML File: Test Configuration (LINQ to XML)](sample-xml-file-test-configuration-linq-to-xml.md).</span></span>  
  
```vb  
Dim testCfg As XElement = XElement.Load("TestConfig.xml")  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    testCfg.Elements("Test").Skip(1).Take(3)  
  
'LINQ to XML query  
Dim list2 As IEnumerable(Of XElement) = _  
    testCfg.Elements("Test"). _  
    Where(Function(ByVal el, ByVal idx) idx >= 1 And idx <= 3)  
  
' XPath expression  
Dim list3 As IEnumerable(Of XElement) = _  
    testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]")  
  
If list1.Count() = list2.Count() And _  
       list1.Count() = list3.Count() And _  
       list1.Intersect(list2).Count() = list1.Count() And _  
       list1.Intersect(list3).Count() = list1.Count() Then  
  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
  
For Each el As XElement In list1  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="deb1e-114">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="deb1e-114">This example produces the following output:</span></span>  
  
```console  
Results are identical  
<Test TestId="0002" TestType="CMD">  
  <Name>Find succeeding characters</Name>  
  <CommandLine>Examp2.EXE</CommandLine>  
  <Input>abc</Input>  
  <Output>def</Output>  
</Test>  
<Test TestId="0003" TestType="GUI">  
  <Name>Convert multiple numbers to strings</Name>  
  <CommandLine>Examp2.EXE /Verbose</CommandLine>  
  <Input>123</Input>  
  <Output>One Two Three</Output>  
</Test>  
<Test TestId="0004" TestType="GUI">  
  <Name>Find correlated key</Name>  
  <CommandLine>Examp3.EXE</CommandLine>  
  <Input>a1</Input>  
  <Output>b1</Output>  
</Test>  
```  
  
## <a name="see-also"></a><span data-ttu-id="deb1e-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="deb1e-115">See also</span></span>

- [<span data-ttu-id="deb1e-116">XPath 使用者的 LINQ to XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="deb1e-116">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

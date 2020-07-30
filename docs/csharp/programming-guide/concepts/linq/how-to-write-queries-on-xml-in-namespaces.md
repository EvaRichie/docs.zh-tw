---
title: '如何在命名空間中撰寫 XML 的查詢（c #）'
description: 瞭解如何在命名空間中撰寫 XML 的查詢。 針對這些查詢，您必須使用具有正確命名空間的 XName 物件。
ms.date: 07/20/2015
ms.assetid: 7c54df81-15e4-4091-8c81-a87637029130
ms.openlocfilehash: 64eb9df1cde3b434a11e2e5410aab96993dc0fa1
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303175"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-c"></a><span data-ttu-id="ce1b4-104">如何在命名空間中撰寫 XML 的查詢（c #）</span><span class="sxs-lookup"><span data-stu-id="ce1b4-104">How to write queries on XML in namespaces (C#)</span></span>
<span data-ttu-id="ce1b4-105">若要撰寫命名空間 (Namespace) 中的 XML 查詢，您必須使用具有正確命名空間的 <xref:System.Xml.Linq.XName> 物件。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-105">To write a query on XML that is in a namespace, you must use <xref:System.Xml.Linq.XName> objects that have the correct namespace.</span></span>  
  
 <span data-ttu-id="ce1b4-106">若為 C#，最常見的方法是使用包含 URI 的字串初始化 <xref:System.Xml.Linq.XNamespace>，然後使用加法運算子多載結合命名空間與區域名稱。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-106">For C#, the most common approach is to initialize an <xref:System.Xml.Linq.XNamespace> using a string that contains the URI, then use the addition operator overload to combine the namespace with the local name.</span></span>  
  
 <span data-ttu-id="ce1b4-107">本主題中的第一組範例會示範如何在預設命名空間中建立 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-107">The first set of examples in this topic shows how to create an XML tree in a default namespace.</span></span> <span data-ttu-id="ce1b4-108">第二組範例則示範如何在具有前置詞的命名空間中建立 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-108">The second set shows how to create an XML tree in a namespace with a prefix.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ce1b4-109">範例</span><span class="sxs-lookup"><span data-stu-id="ce1b4-109">Example</span></span>  
 <span data-ttu-id="ce1b4-110">下列範例會建立位於預設命名空間中的 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-110">The following example creates an XML tree that is in a default namespace.</span></span> <span data-ttu-id="ce1b4-111">接著，它會擷取項目的集合。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-111">It then retrieves a collection of elements.</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 <span data-ttu-id="ce1b4-112">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ce1b4-112">This example produces the following output:</span></span>  
  
```output  
1  
2  
3  
```  
  
## <a name="example"></a><span data-ttu-id="ce1b4-113">範例</span><span class="sxs-lookup"><span data-stu-id="ce1b4-113">Example</span></span>  
 <span data-ttu-id="ce1b4-114">在 C# 中，不論您要針對使用具有前置詞之命名空間的 XML 樹狀，還是針對具有預設命名空間的 XML 樹狀撰寫查詢，查詢的撰寫方式都相同。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-114">In C#, you write queries in the same way regardless of whether you are writing queries on an XML tree that uses a namespace with a prefix or on an XML tree with a default namespace.</span></span>  
  
 <span data-ttu-id="ce1b4-115">下列範例會建立位於命名空間中，具有前置詞的 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-115">The following example creates an XML tree that is in a namespace with a prefix.</span></span> <span data-ttu-id="ce1b4-116">接著，它會擷取項目的集合。</span><span class="sxs-lookup"><span data-stu-id="ce1b4-116">It then retrieves a collection of elements.</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<aw:Root xmlns:aw='http://www.adventure-works.com'>  
    <aw:Child>1</aw:Child>  
    <aw:Child>2</aw:Child>  
    <aw:Child>3</aw:Child>  
    <aw:AnotherChild>4</aw:AnotherChild>  
    <aw:AnotherChild>5</aw:AnotherChild>  
    <aw:AnotherChild>6</aw:AnotherChild>  
</aw:Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 <span data-ttu-id="ce1b4-117">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ce1b4-117">This example produces the following output:</span></span>  
  
```output  
1  
2  
3  
```  
  
## <a name="see-also"></a><span data-ttu-id="ce1b4-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ce1b4-118">See also</span></span>

- [<span data-ttu-id="ce1b4-119">命名空間概觀 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="ce1b4-119">Namespaces Overview (LINQ to XML) (C#)</span></span>](namespaces-overview-linq-to-xml.md)

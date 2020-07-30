---
title: C# 中的預設命名空間範圍
description: '瞭解如何在 c # 中 LINQ to XML 的預設 XML 命名空間中查詢。 使用 XNamespace 變數和區功能變數名稱稱來建立查詢的限定名稱。'
ms.date: 07/20/2015
ms.assetid: fe826236-830f-457a-9027-7ad62c909fae
ms.openlocfilehash: 912e47099f89daa9b80ac58b422d39d598509ac9
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302395"
---
# <a name="scope-of-default-namespaces-in-c"></a><span data-ttu-id="24dd4-104">C\# 中的預設命名空間範圍</span><span class="sxs-lookup"><span data-stu-id="24dd4-104">Scope of Default Namespaces in C\#</span></span>
<span data-ttu-id="24dd4-105">在 XML 樹狀結構中表示的預設命名空間不在查詢的範圍內。</span><span class="sxs-lookup"><span data-stu-id="24dd4-105">Default namespaces as represented in the XML tree are not in scope for queries.</span></span> <span data-ttu-id="24dd4-106">如果您擁有的 XML 位於預設命名空間中，您仍然必須宣告 <xref:System.Xml.Linq.XNamespace> 變數，然後將它與區域名稱結合，讓限定名稱 (Qualified Name) 得以用於查詢中。</span><span class="sxs-lookup"><span data-stu-id="24dd4-106">If you have XML that is in a default namespace, you still must declare an <xref:System.Xml.Linq.XNamespace> variable, and combine it with the local name to make a qualified name to be used in the query.</span></span>  
  
 <span data-ttu-id="24dd4-107">查詢 XML 時所遇到的其中一個最常見的問題是，如果 XML 樹狀結構有預設的命名空間，即使 XML 不在命名空間中，開發人員有時候還是會撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="24dd4-107">One of the most common problems when querying XML trees is that if the XML tree has a default namespace, the developer sometimes writes the query as though the XML were not in a namespace.</span></span>  
  
 <span data-ttu-id="24dd4-108">本主題中的第一組範例會顯示載入預設命名空間中的 XML 但查詢錯誤的常見方式。</span><span class="sxs-lookup"><span data-stu-id="24dd4-108">The first set of examples in this topic shows a typical way that XML in a default namespace is loaded, but is queried improperly.</span></span>  
  
 <span data-ttu-id="24dd4-109">第二組範例顯示所需的修正，讓您可以在命名空間中查詢 XML。</span><span class="sxs-lookup"><span data-stu-id="24dd4-109">The second set of examples show the necessary corrections so that you can query XML in a namespace.</span></span>  
  
## <a name="example"></a><span data-ttu-id="24dd4-110">範例</span><span class="sxs-lookup"><span data-stu-id="24dd4-110">Example</span></span>  
 <span data-ttu-id="24dd4-111">此範例顯示在命名空間中建立 XML，以及傳回空結果集的查詢。</span><span class="sxs-lookup"><span data-stu-id="24dd4-111">This example shows the creation of XML in a namespace, and a query that returns an empty result set.</span></span>  
  
### <a name="code"></a><span data-ttu-id="24dd4-112">程式碼</span><span class="sxs-lookup"><span data-stu-id="24dd4-112">Code</span></span>  
  
```csharp  
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
    from el in root.Elements("Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a><span data-ttu-id="24dd4-113">註解</span><span class="sxs-lookup"><span data-stu-id="24dd4-113">Comments</span></span>  
 <span data-ttu-id="24dd4-114">此範例會產生下列結果：</span><span class="sxs-lookup"><span data-stu-id="24dd4-114">This example produces the following result:</span></span>  
  
```output  
Result set follows:  
End of result set  
```  
  
## <a name="example"></a><span data-ttu-id="24dd4-115">範例</span><span class="sxs-lookup"><span data-stu-id="24dd4-115">Example</span></span>  
 <span data-ttu-id="24dd4-116">此範例顯示在命名空間中建立 XML，以及編碼正確的查詢。</span><span class="sxs-lookup"><span data-stu-id="24dd4-116">This example shows the creation of XML in a namespace, and a query that is coded properly.</span></span>  
  
 <span data-ttu-id="24dd4-117">相較於上述編碼錯誤的範例，使用 C# 時的正確方法為宣告與初始化 <xref:System.Xml.Linq.XNamespace> 物件，並在指定 <xref:System.Xml.Linq.XName> 物件時使用它。</span><span class="sxs-lookup"><span data-stu-id="24dd4-117">In contrast to the incorrectly coded example above, the correct approach when using C# is to declare and initialize an <xref:System.Xml.Linq.XNamespace> object, and to use it when specifying <xref:System.Xml.Linq.XName> objects.</span></span> <span data-ttu-id="24dd4-118">在這個情況下，<xref:System.Xml.Linq.XContainer.Elements%2A> 方法的引數為 <xref:System.Xml.Linq.XName> 物件。</span><span class="sxs-lookup"><span data-stu-id="24dd4-118">In this case, the argument to the <xref:System.Xml.Linq.XContainer.Elements%2A> method is an <xref:System.Xml.Linq.XName> object.</span></span>  
  
### <a name="code"></a><span data-ttu-id="24dd4-119">程式碼</span><span class="sxs-lookup"><span data-stu-id="24dd4-119">Code</span></span>  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
XNamespace aw = "http://www.adventure-works.com";  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a><span data-ttu-id="24dd4-120">註解</span><span class="sxs-lookup"><span data-stu-id="24dd4-120">Comments</span></span>  
 <span data-ttu-id="24dd4-121">此範例會產生下列結果：</span><span class="sxs-lookup"><span data-stu-id="24dd4-121">This example produces the following result:</span></span>  
  
```output  
Result set follows:  
1  
2  
3  
End of result set  
```  
  
## <a name="see-also"></a><span data-ttu-id="24dd4-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="24dd4-122">See also</span></span>

- [<span data-ttu-id="24dd4-123">命名空間概觀 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="24dd4-123">Namespaces Overview (LINQ to XML) (C#)</span></span>](namespaces-overview-linq-to-xml.md)

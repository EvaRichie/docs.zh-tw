---
title: 作法：建立包含命名空間的文件 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: cc5b0d4d-360c-4ada-94fa-2d2916e989be
ms.openlocfilehash: a440c9d810798eb5ebd025a336cbb17fface23b4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414630"
---
# <a name="how-to-create-a-document-with-namespaces-linq-to-xml-visual-basic"></a><span data-ttu-id="2e94b-102">如何：建立包含命名空間的文件 (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2e94b-102">How to: Create a Document with Namespaces (LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="2e94b-103">本主題顯示如何在 Visual Basic 中建立具有命名空間 (Namespace) 的文件。</span><span class="sxs-lookup"><span data-stu-id="2e94b-103">This topic shows how to create a document with namespaces in Visual Basic.</span></span>  
  
 <span data-ttu-id="2e94b-104">在 Visual Basic 中使用 XML 常值時，使用者可以定義一個預設的 XML 全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="2e94b-104">When using XML literals in Visual Basic, users can define one global default XML namespace.</span></span> <span data-ttu-id="2e94b-105">這個命名空間同時為 XML 常值和 XML 屬性的預設命名空間。</span><span class="sxs-lookup"><span data-stu-id="2e94b-105">This namespace is the default namespace for both XML literals and XML properties.</span></span> <span data-ttu-id="2e94b-106">XML 預設命名空間可在專案層級或檔案層級定義。</span><span class="sxs-lookup"><span data-stu-id="2e94b-106">The default XML namespace can be defined at either the project level or the file level.</span></span> <span data-ttu-id="2e94b-107">如果是在檔案層級定義，該命名空間會覆寫專案層級的預設命名空間。</span><span class="sxs-lookup"><span data-stu-id="2e94b-107">If it is defined at the file level, it overrides the default namespace at the project level.</span></span>  
  
 <span data-ttu-id="2e94b-108">您也可以定義其他命名空間，並為這些命名空間指定命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="2e94b-108">You can also define other namespaces, and specify the namespace prefixes for those namespaces.</span></span>  
  
 <span data-ttu-id="2e94b-109">您可以使用 `Imports` 關鍵字，同時定義預設命名空間與具有前置詞的命名空間。</span><span class="sxs-lookup"><span data-stu-id="2e94b-109">You define both default namespaces and namespaces with a prefix by using the `Imports` keyword.</span></span>  
  
 <span data-ttu-id="2e94b-110">如需詳細資訊，請參閱[Visual Basic 中的 XML 常值簡介](introduction-to-xml-literals.md)。</span><span class="sxs-lookup"><span data-stu-id="2e94b-110">For more information, see [Introduction to XML Literals in Visual Basic](introduction-to-xml-literals.md).</span></span>  
  
 <span data-ttu-id="2e94b-111">請注意，XML 預設命名空間僅適用於項目，而不適用於屬性。</span><span class="sxs-lookup"><span data-stu-id="2e94b-111">Note that the default XML namespace only applies to elements and not to attributes.</span></span> <span data-ttu-id="2e94b-112">根據預設，屬性一定會在沒有命名空間中。</span><span class="sxs-lookup"><span data-stu-id="2e94b-112">Attributes are by default always in no namespace.</span></span> <span data-ttu-id="2e94b-113">不過，您可以使用命名空間前置詞，將屬性放到命名空間中。</span><span class="sxs-lookup"><span data-stu-id="2e94b-113">However, you can use a namespace prefix to put an attribute in a namespace.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2e94b-114">範例</span><span class="sxs-lookup"><span data-stu-id="2e94b-114">Example</span></span>  
 <span data-ttu-id="2e94b-115">此範例會建立包含命名空間的文件。</span><span class="sxs-lookup"><span data-stu-id="2e94b-115">This example creates a document that contains a namespace.</span></span>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child aw:Att="attvalue"/>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="2e94b-116">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2e94b-116">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child aw:Att="attvalue" />  
</aw:Root>  
```  
  
## <a name="example"></a><span data-ttu-id="2e94b-117">範例</span><span class="sxs-lookup"><span data-stu-id="2e94b-117">Example</span></span>  
 <span data-ttu-id="2e94b-118">此範例會建立包含兩個命名空間 (其中一個為預設命名空間) 的文件。</span><span class="sxs-lookup"><span data-stu-id="2e94b-118">This example creates a document that contains two namespaces, one of which is the default namespace.</span></span>  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child Att="attvalue"/>  
                <fc:Child2>child2 content</fc:Child2>  
            </Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 <span data-ttu-id="2e94b-119">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2e94b-119">This example produces the following output:</span></span>  
  
```xml  
<Root xmlns:fc="www.fourthcoffee.com" xmlns="http://www.adventure-works.com">  
  <Child Att="attvalue" />  
  <fc:Child2>child2 content</fc:Child2>  
</Root>  
```  
  
## <a name="example"></a><span data-ttu-id="2e94b-120">範例</span><span class="sxs-lookup"><span data-stu-id="2e94b-120">Example</span></span>  
 <span data-ttu-id="2e94b-121">下列範例會建立包含多個命名空間 (兩者皆擁有命名空間前置詞) 的文件。</span><span class="sxs-lookup"><span data-stu-id="2e94b-121">The following example creates a document that contains multiple namespaces, both with namespace prefixes.</span></span>  
  
 <span data-ttu-id="2e94b-122">序列化 XML 樹狀結構時，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會在必要時發出命名空間宣告，讓每個項目都位於其指定的命名空間中。</span><span class="sxs-lookup"><span data-stu-id="2e94b-122">When serializing an XML tree, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] emits namespace declarations as required so that each element is in its designated namespace.</span></span>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <fc:Child>  
                    <aw:DifferentChild>other content</aw:DifferentChild>  
                </fc:Child>  
                <aw:Child2>c2 content</aw:Child2>  
                <fc:Child3>c3 content</fc:Child3>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 <span data-ttu-id="2e94b-123">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2e94b-123">This example produces the following output:</span></span>  
  
```xml  
<aw:Root xmlns:fc="www.fourthcoffee.com" xmlns:aw="http://www.adventure-works.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a><span data-ttu-id="2e94b-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2e94b-124">See also</span></span>

- [<span data-ttu-id="2e94b-125">命名空間總覽（LINQ to XML）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="2e94b-125">Namespaces Overview (LINQ to XML) (Visual Basic)</span></span>](namespaces-overview-linq-to-xml.md)

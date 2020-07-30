---
title: 擷取段落的文字 (C#)
description: '瞭解如何使用 LINQ 查詢，以 c # 中的字串取得 WordprocessingML 檔中每個段落的文字。 這個範例會使用連鎖的查詢。'
ms.date: 07/20/2015
ms.assetid: 127d635e-e559-408f-90c8-2bb621ca50ac
ms.openlocfilehash: 58a07ab848307c886927815e4e49e90806f61346
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302590"
---
# <a name="retrieving-the-text-of-the-paragraphs-c"></a><span data-ttu-id="6c901-104">擷取段落的文字 (C#)</span><span class="sxs-lookup"><span data-stu-id="6c901-104">Retrieving the Text of the Paragraphs (C#)</span></span>
<span data-ttu-id="6c901-105">這個範例是根據上述範例 ([擷取段落及其樣式 (C#)](./retrieving-the-paragraphs-and-their-styles.md)) 所建置。</span><span class="sxs-lookup"><span data-stu-id="6c901-105">This example builds on the previous example, [Retrieving the Paragraphs and Their Styles (C#)](./retrieving-the-paragraphs-and-their-styles.md).</span></span> <span data-ttu-id="6c901-106">這個新的範例會將每個段落的文字當做字串擷取。</span><span class="sxs-lookup"><span data-stu-id="6c901-106">This new example retrieves the text of each paragraph as a string.</span></span>  
  
 <span data-ttu-id="6c901-107">若要擷取文字，此範例可加入逐一查看匿名型別之集合的其他查詢，並規劃加入新成員 `Text` 之匿名型別的新集合。</span><span class="sxs-lookup"><span data-stu-id="6c901-107">To retrieve the text, this example adds an additional query that iterates through the collection of anonymous types and projects a new collection of an anonymous type with the addition of a new member, `Text`.</span></span> <span data-ttu-id="6c901-108">它會使用 <xref:System.Linq.Enumerable.Aggregate%2A> 標準查詢運算子，將多個字串串連到一個字串。</span><span class="sxs-lookup"><span data-stu-id="6c901-108">It uses the <xref:System.Linq.Enumerable.Aggregate%2A> standard query operator to concatenate multiple strings into one string.</span></span>  
  
 <span data-ttu-id="6c901-109">此技術 (也就是，先規劃為匿名型別的集合，然後使用此集合規劃為匿名型別的新集合) 是實用的常見慣用句。</span><span class="sxs-lookup"><span data-stu-id="6c901-109">This technique (that is, first projecting to a collection of an anonymous type, then using this collection to project to a new collection of an anonymous type) is a common and useful idiom.</span></span> <span data-ttu-id="6c901-110">在沒有規劃為第一個匿名型別的情況下，可能已經撰寫這個查詢。</span><span class="sxs-lookup"><span data-stu-id="6c901-110">This query could have been written without projecting to the first anonymous type.</span></span> <span data-ttu-id="6c901-111">不過，因為延遲評估的緣故，這麼做不會使用太多額外的處理電源。</span><span class="sxs-lookup"><span data-stu-id="6c901-111">However, because of lazy evaluation, doing so does not use much additional processing power.</span></span> <span data-ttu-id="6c901-112">此慣用句會在堆積上建立更多短期存在的物件，但實質上，這不會降低效能。</span><span class="sxs-lookup"><span data-stu-id="6c901-112">The idiom creates more short lived objects on the heap, but this does not substantially degrade performance.</span></span>  
  
 <span data-ttu-id="6c901-113">當然，此慣用句可能會撰寫包含功能的單一查詢以擷取段落、每個段落的樣式，以及每個段落的文字。</span><span class="sxs-lookup"><span data-stu-id="6c901-113">Of course, it would be possible to write a single query that contains the functionality to retrieve the paragraphs, the style of each paragraph, and the text of each paragraph.</span></span> <span data-ttu-id="6c901-114">不過，這通常有助於將更複雜的查詢分割為多個查詢，因為所產生的程式碼更為模組化而且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="6c901-114">However, it often is useful to break up a more complicated query into multiple queries because the resulting code is more modular and easier to maintain.</span></span> <span data-ttu-id="6c901-115">此外，如果您需要重複使用某部分查詢，當查詢以此種方式撰寫時，重構比較容易。</span><span class="sxs-lookup"><span data-stu-id="6c901-115">Furthermore, if you need to reuse a portion of the query, it is easier to refactor if the queries are written in this manner.</span></span>  
  
 <span data-ttu-id="6c901-116">這些鏈結在一起的查詢會使用在[教學課程：將查詢鏈結在一起 (C#)](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md) 主題中詳細檢查的處理模型。</span><span class="sxs-lookup"><span data-stu-id="6c901-116">These queries, which are chained together, use the processing model that is examined in detail in the topic [Tutorial: Chaining Queries Together (C#)](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="6c901-117">範例</span><span class="sxs-lookup"><span data-stu-id="6c901-117">Example</span></span>  
 <span data-ttu-id="6c901-118">此範例會處理 WordprocessingML 文件，以判斷項目節點、樣式名稱，以及每個段落的文字。</span><span class="sxs-lookup"><span data-stu-id="6c901-118">This example processes a WordprocessingML document, determining the element node, the style name, and the text of each paragraph.</span></span> <span data-ttu-id="6c901-119">此範例在這個教學課程中，會在先前的範例上建置。</span><span class="sxs-lookup"><span data-stu-id="6c901-119">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="6c901-120">新的查詢會在以下程式碼的註解中叫出。</span><span class="sxs-lookup"><span data-stu-id="6c901-120">The new query is called out in comments in the code below.</span></span>  
  
 <span data-ttu-id="6c901-121">如需建立此範例之來源文件的指示，請參閱[建立來源 Office Open XML 文件 (C#)](./creating-the-source-office-open-xml-document.md)。</span><span class="sxs-lookup"><span data-stu-id="6c901-121">For instructions for creating the source document for this example, see [Creating the Source Office Open XML Document (C#)](./creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="6c901-122">這個範例會使用 WindowsBase 組件的類別。</span><span class="sxs-lookup"><span data-stu-id="6c901-122">This example uses classes from the WindowsBase assembly.</span></span> <span data-ttu-id="6c901-123">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="6c901-123">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
string defaultStyle =
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
// Find all paragraphs in the document.  
var paragraphs =  
    from para in xDoc  
                 .Root  
                 .Element(w + "body")  
                 .Descendants(w + "p")  
    let styleNode = para  
                    .Elements(w + "pPr")  
                    .Elements(w + "pStyle")  
                    .FirstOrDefault()  
    select new  
    {  
        ParagraphNode = para,  
        StyleName = styleNode != null ?  
            (string)styleNode.Attribute(w + "val") :  
            defaultStyle  
    };  
  
// Following is the new query that retrieves the text of  
// each paragraph.  
var paraWithText =  
    from para in paragraphs  
    select new  
    {  
        ParagraphNode = para.ParagraphNode,  
        StyleName = para.StyleName,  
        Text = para  
               .ParagraphNode  
               .Elements(w + "r")  
               .Elements(w + "t")  
               .Aggregate(  
                   new StringBuilder(),  
                   (s, i) => s.Append((string)i),  
                   s => s.ToString()  
               )  
    };  
  
foreach (var p in paraWithText)  
    Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text);  
```  
  
 <span data-ttu-id="6c901-124">這個範例會在套用至[建立來源 Office Open XML 文件 (C#)](./creating-the-source-office-open-xml-document.md) 中所述的文件時產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="6c901-124">This example produces the following output when applied to the document described in [Creating the Source Office Open XML Document (C#)](./creating-the-source-office-open-xml-document.md).</span></span>  
  
```output  
StyleName:Heading1 >Parsing WordprocessingML with LINQ to XML<  
StyleName:Normal ><  
StyleName:Normal >The following example prints to the console.<  
StyleName:Normal ><  
StyleName:Code >using System;<  
StyleName:Code ><  
StyleName:Code >class Program {<  
StyleName:Code >    public static void (string[] args) {<  
StyleName:Code >        Console.WriteLine("Hello World");<  
StyleName:Code >    }<  
StyleName:Code >}<  
StyleName:Normal ><  
StyleName:Normal >This example produces the following output:<  
StyleName:Normal ><  
StyleName:Code >Hello World<  
```  
  
## <a name="next-steps"></a><span data-ttu-id="6c901-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c901-125">Next Steps</span></span>  
 <span data-ttu-id="6c901-126">下一個範例顯示如何使用擴充方法 (而非 <xref:System.Linq.Enumerable.Aggregate%2A>)，將多個字串串連到一個字串。</span><span class="sxs-lookup"><span data-stu-id="6c901-126">The next example shows how to use an extension method, instead of <xref:System.Linq.Enumerable.Aggregate%2A>, to concatenate multiple strings into a single string.</span></span>  
  
- [<span data-ttu-id="6c901-127">使用擴充方法進行重構 (C#)</span><span class="sxs-lookup"><span data-stu-id="6c901-127">Refactoring Using an Extension Method (C#)</span></span>](./refactoring-using-an-extension-method.md)  
  
## <a name="see-also"></a><span data-ttu-id="6c901-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6c901-128">See also</span></span>

- [<span data-ttu-id="6c901-129">教學課程：管理 WordprocessingML 文件中的內容 (C#)</span><span class="sxs-lookup"><span data-stu-id="6c901-129">Tutorial: Manipulating Content in a WordprocessingML Document (C#)</span></span>](shape-of-wordprocessingml-documents.md)
- [<span data-ttu-id="6c901-130">LINQ to XML 中的延後執行和延遲評估 (C#)</span><span class="sxs-lookup"><span data-stu-id="6c901-130">Deferred Execution and Lazy Evaluation in LINQ to XML (C#)</span></span>](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

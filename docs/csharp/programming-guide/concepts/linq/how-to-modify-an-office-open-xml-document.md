---
title: '如何修改 Office Open XML 檔（c #）'
description: '瞭解如何開啟 Office Open XML 檔、加以修改並加以儲存。 這個 c # 範例會使用在 WindowsBase 元件中找到的類別。'
ms.date: 07/20/2015
ms.assetid: 467d489c-2b1b-453b-a757-8ac180e82a96
ms.openlocfilehash: 1155851696a0a6ed651c5f84290a3879e73276db
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104810"
---
# <a name="how-to-modify-an-office-open-xml-document-c"></a><span data-ttu-id="7dd6c-104">如何修改 Office Open XML 檔（c #）</span><span class="sxs-lookup"><span data-stu-id="7dd6c-104">How to modify an Office Open XML document (C#)</span></span>
<span data-ttu-id="7dd6c-105">這個主題顯示會開啟、修改以及儲存 Office Open XML 文件的範例。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-105">This topic presents an example that opens an Office Open XML document, modifies it, and saves it.</span></span>  
  
 <span data-ttu-id="7dd6c-106">如需 Office Open XML 的詳細資訊，請參閱 [Open XML SDK](https://github.com/OfficeDev/Open-XML-SDK) \(英文\) 和 [www.ericwhite.com](http://ericwhite.com/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-106">For more information on Office Open XML, see [Open XML SDK](https://github.com/OfficeDev/Open-XML-SDK) and [www.ericwhite.com](http://ericwhite.com/).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7dd6c-107">範例</span><span class="sxs-lookup"><span data-stu-id="7dd6c-107">Example</span></span>  
 <span data-ttu-id="7dd6c-108">這個範例會尋找文件中的第一個段落元件。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-108">This example finds the first paragraph element in the document.</span></span> <span data-ttu-id="7dd6c-109">它會從段落擷取文字，然後刪除段落中的所有文字執行。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-109">It retrieves the text from the paragraph, and then deletes all text runs in the paragraph.</span></span> <span data-ttu-id="7dd6c-110">它所建立的新文字執行包含已轉換為大寫的第一個段落文字。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-110">It creates a new text run that consists of the first paragraph text that has been converted to upper case.</span></span> <span data-ttu-id="7dd6c-111">接著，它會將變更的 XML 序列化為 Open XML 封裝並加以關閉。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-111">It then serializes the changed XML into the Open XML package and closes it.</span></span>  
  
 <span data-ttu-id="7dd6c-112">這個範例會使用在 WindowsBase 組件中找到的類別。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-112">This example uses classes found in the WindowsBase assembly.</span></span> <span data-ttu-id="7dd6c-113">它會使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-113">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```csharp  
public static class LocalExtensions  
{  
    public static string StringConcatenate(this IEnumerable<string> source)  
    {  
        StringBuilder sb = new StringBuilder();  
        foreach (string s in source)  
            sb.Append(s);  
        return sb.ToString();  
    }  
  
    public static string StringConcatenate<T>(this IEnumerable<T> source,  
        Func<T, string> func)  
    {  
        StringBuilder sb = new StringBuilder();  
        foreach (T item in source)  
            sb.Append(func(item));  
        return sb.ToString();  
    }  
  
    public static string StringConcatenate(this IEnumerable<string> source, string separator)  
    {  
        StringBuilder sb = new StringBuilder();  
        foreach (string s in source)  
            sb.Append(s).Append(separator);  
        return sb.ToString();  
    }  
  
    public static string StringConcatenate<T>(this IEnumerable<T> source,  
        Func<T, string> func, string separator)  
    {  
        StringBuilder sb = new StringBuilder();  
        foreach (T item in source)  
            sb.Append(func(item)).Append(separator);  
        return sb.ToString();  
    }  
}  
  
class Program  
{  
    public static string ParagraphText(XElement e)  
    {  
        XNamespace w = e.Name.Namespace;  
        return e  
               .Elements(w + "r")  
               .Elements(w + "t")  
               .StringConcatenate(element => (string)element);  
    }  
  
    static void Main(string[] args)  
    {  
        const string fileName = "SampleDoc.docx";  
  
        const string documentRelationshipType =  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
        const string stylesRelationshipType =  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
        const string wordmlNamespace =  
          "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
        XNamespace w = wordmlNamespace;  
  
        using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.ReadWrite))  
        {  
            PackageRelationship docPackageRelationship =  
              wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
            if (docPackageRelationship != null)  
            {  
                Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
                  docPackageRelationship.TargetUri);  
                PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
                //  Load the document XML in the part into an XDocument instance.  
                XDocument xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
                //  Find the styles part. There will only be one.  
                PackageRelationship styleRelation =  
                  documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
                PackagePart stylePart = null;  
                XDocument styleDoc = null;  
  
                if (styleRelation != null)  
                {  
                    Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
                    stylePart = wdPackage.GetPart(styleUri);  
  
                    //  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
                }  
  
                XElement paraNode = xDoc  
                                    .Root  
                                    .Element(w + "body")  
                                    .Descendants(w + "p")  
                                    .FirstOrDefault();  
  
                string paraText = ParagraphText(paraNode);  
  
                // remove all text runs  
                paraNode.Descendants(w + "r").Remove();  
  
                paraNode.Add(  
                    new XElement(w + "r",  
                        new XElement(w + "t", paraText.ToUpper())  
                    )  
                );  
  
                //  Save the XML into the package  
                using (XmlWriter xw =  
                  XmlWriter.Create(documentPart.GetStream(FileMode.Create, FileAccess.Write)))  
                {  
                    xDoc.Save(xw);  
                }  
  
                Console.WriteLine("New first paragraph: >{0}<", paraText.ToUpper());  
            }  
        }  
    }  
}  
```  
  
 <span data-ttu-id="7dd6c-114">如果您在執行此程式後開啟 `SampleDoc.docx`，就可以看到此程式已將文件中第一個段落轉換成大寫。</span><span class="sxs-lookup"><span data-stu-id="7dd6c-114">If you open `SampleDoc.docx` after running this program, you can see that this program converted the first paragraph in the document to upper case.</span></span>  
  
 <span data-ttu-id="7dd6c-115">執行[建立來源 Office Open XML 文件 (C#)](./creating-the-source-office-open-xml-document.md) 中所描述的範例 Open XML 文件時，此範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7dd6c-115">When run with the sample Open XML document described in [Creating the Source Office Open XML Document (C#)](./creating-the-source-office-open-xml-document.md), this example produces the following output:</span></span>  
  
```output  
New first paragraph: >PARSING WORDPROCESSINGML WITH LINQ TO XML<  
```  
